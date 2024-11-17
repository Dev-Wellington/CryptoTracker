<script setup>
import { ref } from "vue";

import SearchBar from "./components/SearchBar.vue";
import VerticalNavbar from "./components/VerticalNavbar.vue";
import CryptoChart from "./components/CryptoChart.vue";
import UserProfile from "./components/UserProfile.vue";
import CryptoList from "./components/CryptoList.vue";
import CryptoRanking from "./components/CryptoRanking.vue";

const moeda = ref("polkadot");
</script>

<template>
  <div class="grid-container">
    <VerticalNavbar class="verticalNavbar1" />
    <VerticalNavbar class="verticalNavbar" />
    <SearchBar v-model="moeda" class="searchBar" />

    <div class="main-content">
      <div class="left-section">
        <CryptoChart :moeda="moeda" class="cryptoChart" />
        <UserProfile class="userProfile" />
      </div>
      <div class="right-section">
        <CryptoList class="cryptoList" />
        <CryptoRanking class="cryptoRanking" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.grid-container {
  display: grid;
  grid-template-areas:
    "verticalNavbar searchBar"
    "verticalNavbar main-content";
  grid-template-columns: auto 1fr;
  grid-template-rows: auto 1fr;
  height: 100vh;
  gap: 0;
}
.verticalNavbar {
  grid-area: verticalNavbar;
  margin: 0;
}
.verticalNavbar1 {
  position: absolute;
  z-index: 2;
}
.searchBar {
  grid-area: searchBar;
  margin: 0;
}
.main-content {
  grid-area: main-content;
  gap: 20px;
  padding: 15px;
  display: flex;
  flex-direction: column;
}
.left-section,
.right-section {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  gap: 20px;
}
.cryptoChart,
.userProfile,
.cryptoList,
.cryptoRanking {
  padding: 15px;
  margin: 0;
}
@media (width >= 768px) {
  .left-section,
  .right-section {
    width: 100%;
    justify-content: center;
  }
  .main-content {
    align-items: center;
    justify-content: center;
  }
}
@media (width <= 480px) {
  .verticalNavbar,
  .verticalNavbar1 {
    display: none;
  }

  .left-section,
  .right-section {
    flex-direction: column;
  }
  .left-section {
    flex-direction: column-reverse;
  }
}
</style>
