<script setup>
import { ref, onMounted, watch } from "vue";
import { Chart, registerables } from "chart.js";
import axios from "axios";

Chart.register(...registerables);

const props = defineProps({
  moeda: String,
});

const cryptoChart = ref(null);
let chartInstance = null;

const apiKey = "CG-3odEqH1JGDWQMm24Nfk7PtMh";

const fetchChartData = async (days) => {
  try {
    const response = await axios.get(
      `https://api.coingecko.com/api/v3/coins/${props.moeda}/market_chart`,
      {
        params: {
          vs_currency: "usd",
          days,
          x_cg_demo_api_key: apiKey,
        },
      }
    );

    const data = {
      labels: response.data.prices.map((price) =>
        new Date(price[0]).toLocaleDateString()
      ),
      values: response.data.prices.map((price) => price[1]),
    };

    updateChart(data);
  } catch (error) {
    console.error("Erro ao buscar os dados das criptomoedas:", error);
  }
};

const updateChart = (data) => {
  if (chartInstance) {
    chartInstance.destroy();
  }

  const ctx = cryptoChart.value.getContext("2d");
  const gradient = ctx.createLinearGradient(0, 0, 0, 400);
  gradient.addColorStop(0, "rgba(176, 236, 105, 0.6)");
  gradient.addColorStop(1, "rgba(2, 34, 19, 0.1)");

  chartInstance = new Chart(cryptoChart.value, {
    type: "line",
    data: {
      labels: data.labels,
      datasets: [
        {
          label: `Preço da ${props.moeda} (USD)`,
          data: data.values,
          borderColor: "#b0ec69",
          backgroundColor: gradient,
          fill: true,
          tension: 0.3,
        },
      ],
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: { display: false },
      },
      scales: {
        x: { display: false },
        y: {
          grid: { display: false },
          ticks: { color: "#b0ec69" },
        },
      },
    },
  });
};

watch(
  () => props.moeda,
  () => {
    fetchChartData("365");
  }
);
onMounted(() => {
  fetchChartData("365");
});
</script>

<template>
  <div class="cryptoChart__container">
    <div class="buttons__position">
      <div class="buttons__container">
        <button class="btn btn__all" disabled>ALL</button>
        <button class="btn btn__one-day" @click="fetchChartData('1')">
          1D
        </button>
        <button class="btn btn__one-week" @click="fetchChartData('7')">
          1W
        </button>
        <button class="btn btn__one-year" @click="fetchChartData('365')">
          1Y
        </button>
      </div>
    </div>
    <div class="grafico">
      <canvas ref="cryptoChart"></canvas>
    </div>
  </div>
</template>

<style lang="css" scoped>
.cryptoChart__container {
  width: clamp(300px, 60vw, 875px);
  height: clamp(200px, 40vh, 355px);
  border-radius: 35px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  padding: 15px 30px;
  background-color: #022213;
  position: relative;
}
.grafico {
  width: 100%;
  height: 100%;
  padding-top: 15px;
  display: flex;
  align-items: center;
}
canvas {
  width: 100% !important;
  height: 100% !important;
  max-width: 100%;
  max-height: 100%;
}
.buttons__position {
  position: absolute;
  right: 0;
  top: 0;
  background-color: #011b0f;
  border-radius: 0 35px 0 65px;
  width: 50%;
  height: 25%;
}
.buttons__container {
  padding: 20px 30px;
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  gap: 25px;
  width: 100%;
  height: 100%;
}
.btn {
  font-size: 24px;
  width: 75px;
  height: 38px;
  background-color: #b0ec69;
  color: #011b0f;
  border: none;
  border-radius: 50px;
  cursor: pointer;
}
.btn:hover {
  background-color: #8fdc5a;
}
.btn__all {
  cursor: not-allowed;
  background-color: #6a6a6a;
}
.btn__all:hover {
  background-color: #6a6a6a;
}
.btn__all:disabled {
  opacity: 0.6;
}
@media (max-width: 1024px) {
  .buttons__position {
    width: 60%;
  }
  .buttons__container {
    padding: 10px 15px;
    gap: 10px;
    align-items: center;
  }
  .btn {
    width: 20%;
    font-size: 1rem;
  }
}
@media (max-width: 768px) {
  .grafico {
    height: 80%;
  }
  .cryptoChart__container {
    justify-content: flex-end;
    padding: 10px 15px;
  }
  .buttons__position {
    width: 100%;
    border-radius: 25px 25px 0 0;
  }
  .buttons__container {
    gap: 20px;
    justify-content: center;
  }
  .btn {
    width: 20%;
  }
}
@media (width <= 480px) {
  .cryptoChart__container {
    width: 100%;
  }
}
</style>
