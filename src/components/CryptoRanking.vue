<template>
  <div class="crypto-ranking">
    <div
      v-for="(crypto, index) in topRankingCryptos"
      :key="crypto.id"
      class="crypto-ranking__item"
    >
      <div class="crypto-ranking__position">
        <span>#{{ index + 1 }}</span>
      </div>
      <img
        class="crypto-ranking__image"
        :src="crypto.image"
        :alt="crypto.name"
      />
      <ul class="crypto-ranking__details">
        <li class="crypto-ranking__name">
          <h2>{{ crypto.name }} ({{ crypto.symbol.toUpperCase() }})</h2>
        </li>
        <li class="crypto-ranking__market-cap">
          <p>{{ formatar(crypto.market_cap) }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const topRankingCryptos = ref([]);

const fetchCryptos = async () => {
  try {
    const response = await axios.get(
      "https://api.coingecko.com/api/v3/coins/markets",
      {
        params: {
          vs_currency: "usd",
          order: "market_cap_desc",
          per_page: 3,
          page: 1,
        },
      }
    );
    topRankingCryptos.value = response.data;
  } catch (error) {
    console.error("Erro ao buscar os dados das criptomoedas:", error);
  }
};

const formatar = (valor) => {
  if (valor >= 1e12) {
    return `$${(valor / 1e12).toFixed(2)} Trillion`;
  } else if (valor >= 1e9) {
    return `$${(valor / 1e9).toFixed(2)} Billion`;
  } else if (valor >= 1e6) {
    return `$${(valor / 1e6).toFixed(2)} Million`;
  } else {
    return `$${valor.toFixed(2)}`;
  }
};

onMounted(() => {
  fetchCryptos();
});
</script>

<style lang="css" scoped>
.crypto-ranking {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 20px;

  width: clamp(250px, 40%, 335px);
  height: clamp(200px, 40vh, 355px);
  background-color: var(--bg-ranking);
  transition: background-color 0.3s;

  border-radius: 35px;
  padding: 20px 0;
}
.crypto-ranking__item {
  width: 90%;
  height: 100%;
  border-radius: 25px;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: flex-start;
  padding-left: clamp(16px, 2vw, 18px);
  gap: 8px;
  background-color: var(--bg-ranking-item);
  position: relative;
}
.crypto-ranking__position {
  position: absolute;
  top: 0;
  right: 0;
  font-size: clamp(1.2rem, 5vw, 1.6rem);
  width: clamp(15%, 5vw, 25%);
  height: clamp(20%, 5vw, 30%);
  border-radius: 8px 25px 0 25px;
  background-color: #f0f0f0;
  color: var(--text-color);
  display: flex;
  align-items: center;
  justify-content: center;
}
.crypto-ranking__position > span {
  font-size: clamp(1rem, 5vw, 1.6rem);
}
.crypto-ranking__image {
  height: clamp(1rem, 5vw, 4rem);
  width: clamp(1rem, 5vw, 4rem);
}
.crypto-ranking__details {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
  gap: 5px;
}
.crypto-ranking__name > h2 {
  font-size: clamp(1rem, 5vw, 1.2rem);
}
.crypto-ranking__market-cap > p {
  font-size: clamp(0.8rem, 5vw, 0.9rem);
}
li {
  list-style: none;
}
@media (width > 1280px) {
  .crypto-ranking {
    width: clamp(300px, 40%, 500px);
    flex-direction: row;
  }
  .crypto-ranking__item {
    flex-direction: column;
    align-items: start;
    justify-content: center;
    padding: 0 clamp(16px, 2vw, 18px);
    gap: 45px;
  }
  .crypto-ranking__name {
    word-wrap: normal;
  }
}
@media (width<= 480px) {
  .crypto-ranking {
    width: 100%;
  }
  .crypto-ranking__item {
    width: 100%;
  }
  .crypto-ranking__image {
    height: 45px;
    width: 45px;
  }
}
</style>
