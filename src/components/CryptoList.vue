<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const props = defineProps({
  darkMode: Boolean,
});

const cryptos = ref([]);
const cryptosPerPage = ref(3);
const page = ref(1);
const totalLoaded = ref(0);
const maxCryptos = 20;
const apiKey = "CG-3odEqH1JGDWQMm24Nfk7PtMh";

const getIconPath = (iconName) => {
  const path = props.darkMode
    ? new URL(`../assets/icons/dark/${iconName}.svg`, import.meta.url).href
    : new URL(`../assets/icons/light/${iconName}.svg`, import.meta.url).href;
  console.log(`Path for ${iconName}:`, path);
  return path;
};

const fetchCryptos = async () => {
  if (totalLoaded.value >= maxCryptos) return;
  try {
    const response = await axios.get(
      "https://api.coingecko.com/api/v3/coins/markets",
      {
        params: {
          vs_currency: "usd",
          order: "market_cap_desc",
          per_page: cryptosPerPage.value,
          page: page.value,
        },
        headers: {
          "x-cg-demo-api-key": apiKey,
        },
      }
    );
    const newItems = response.data.filter(
      (item) => !cryptos.value.some((crypto) => crypto.id === item.id)
    );
    cryptos.value.push(...newItems);
    totalLoaded.value += newItems.length;
    page.value += 1;
  } catch (error) {
    console.error("Erro ao buscar os dados das criptomoedas:", error);
  }
};

const onScroll = (event) => {
  const { scrollTop, scrollHeight, clientHeight } = event.target;
  if (scrollTop + clientHeight >= scrollHeight - 5) {
    fetchCryptos();
  }
};

onMounted(() => {
  fetchCryptos();
});
</script>

<template>
  <div class="crypto-list" @scroll="onScroll">
    <div class="crypto-list__item" v-for="crypto in cryptos" :key="crypto.id">
      <div class="crypto-list__item-header">
        <img
          class="crypto-list__item-image"
          :src="crypto.image"
          :alt="crypto.name"
        />
        <div class="crypto-list__item-info">
          <h3 class="crypto-list__item-name">
            {{ crypto.name }} ({{ crypto.symbol.toUpperCase() }})
          </h3>
          <p>${{ crypto.current_price.toFixed(2) }}</p>
        </div>
      </div>
      <div class="crypto-list__item-stats">
        <div
          class="crypto-list__item-percentage"
          :class="{
            positive: crypto.price_change_percentage_24h > 0,
            negative: crypto.price_change_percentage_24h < 0,
          }"
        >
          <p class="crypto-list__item-percentage-value">
            {{ crypto.price_change_percentage_24h.toFixed(2) }}%
          </p>
        </div>
        <div class="crypto-list__item-price"></div>
        <div class="crypto-list__item-options">
          <button class="crypto-list__item-options-icon">
            <img :src="getIconPath('button')" alt="Options" />
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="css" scoped>
.crypto-list {
  width: clamp(300px, 60vw, 875px);
  height: clamp(200px, 40vh, 355px);
  background-color: var(--bg-list);
  overflow-y: scroll;
  scrollbar-color: var(--bg-list-item-hover-icon) var(--bg-list);
  border-radius: 35px 0 0 35px;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  gap: 15px;
  transition: background-color 0.3s;
}
.crypto-list__item:hover {
  background-color: var(--bg-list-item-hover);
}
.crypto-list__item {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: flex-start;
  min-height: 100px;
  width: 100%;
  border-radius: 25px;
  background-color: var(--bg-list-item);
}
.crypto-list__item-header {
  display: flex;
  flex-direction: row;
  align-items: center;
  width: 100%;
  height: 100%;
  gap: 15px;
  padding: clamp(10px, 1vw, 15px) clamp(20px, 1vw, 25px);
}
.crypto-list__item-image {
  height: clamp(1rem, 5vw, 4rem);
  width: clamp(1rem, 5vw, 4rem);
}
.crypto-list__item-info {
  display: flex;
  flex-direction: column;
  align-items: start;
  gap: 5px;
}
.crypto-list__item-stats {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: end;
  background-color: var(--bg-list-stats);
  border-radius: 0 0 0 65px;
  width: 100%;
  height: 100%;
  padding: 15px 25px;
  gap: 15px;
}
.crypto-list__item-percentage {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 5px;
}
h3 {
  color: var(--text-color-coins);
  font-size: clamp(1.1rem, 2vw, 1.7rem);
}
p {
  font-size: clamp(0.8rem, 2vw, 1.3rem);
}
.crypto-list__item-percentage-value {
  font-size: clamp(1.5rem, 2vw, 1.7rem);
}
.crypto-list__item-options-icon {
  cursor: pointer;
  height: clamp(1rem, 5vw, 4rem);
  width: clamp(1rem, 5vw, 4rem);
  border: none;
  background: transparent;
  & img {
    width: 100%;
    height: 100%;
  }
}
.crypto-list__item-options-icon:hover {
  filter: drop-shadow(0 0 1px var(--bg-list-item-hover-icon));
}
.crypto-list__item-percentage.positive p {
  color: #4caf50;
}
.crypto-list__item-percentage.negative p {
  color: #f44336;
}
@media (width > 1200px) {
  .crypto-list__item-stats {
    gap: 45px;
  }
}
@media (width <= 480px) {
  .crypto-list {
    width: 100%;
  }
  .crypto-list__item-image {
    height: 45px;
    width: 45px;
  }
  .crypto-list__item-options-icon {
    height: 45px;
    width: 45px;
    background-size: 45px 45px;
  }
}
</style>
