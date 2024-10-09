<template>
  <div>
    <nav
      class="navbar-vertical"
      :class="{ 'navbar-vertical__extendido': clicar }"
    >
      <div class="navbar-vertical__menu-container">
        <div class="navbar-vertical__item navbar-vertical__item--menu">
          <button class="navbar-vertical__menu-button" @click="click">
            <img src="../assets/icons/menu.svg" alt="" srcset="" />
          </button>
          <p class="navbar-vertical__item-text" v-if="clicar">Menu</p>
        </div>
        <div class="navbar-vertical__list-container">
          <ul class="navbar-vertical__list">
            <li class="navbar-vertical__item navbar-vertical__item--profile">
              <button class="navbar-vertical__button">
                <img src="../assets/icons/profile.svg" alt="" />
              </button>
              <p class="navbar-vertical__item-text" v-if="clicar">Profile</p>
            </li>
            <li class="navbar-vertical__item navbar-vertical__item--wallet">
              <button class="navbar-vertical__button">
                <img src="../assets/icons/wallet.svg" alt="" />
              </button>
              <p class="navbar-vertical__item-text" v-if="clicar">Wallets</p>
            </li>
            <li
              class="navbar-vertical__item navbar-vertical__item--communities"
            >
              <button class="navbar-vertical__button">
                <img src="../assets/icons/communities.svg" alt="" />
              </button>
              <p class="navbar-vertical__item-text" v-if="clicar">
                Communities
              </p>
            </li>
            <li
              class="navbar-vertical__item navbar-vertical__item--notifications"
            >
              <button class="navbar-vertical__button">
                <img src="../assets/icons/notifications.svg" alt="" />
              </button>
              <p class="navbar-vertical__item-text" v-if="clicar">
                Notifications
              </p>
            </li>
          </ul>
        </div>
      </div>
      <div class="navbar-vertical__dark-mode-container">
        <button class="navbar-vertical__dark-mode-button">
          <img
            class="navbar-vertical__dark-mode-icon"
            src="../assets/icons/light_mode.svg"
            alt=""
          />
        </button>
        <p class="navbar-vertical__item-text" v-if="clicar">Mode</p>
      </div>
    </nav>
  </div>
</template>

<script setup>
import { ref } from "vue";
const clicar = ref(false);

const click = () => {
  clicar.value = !clicar.value;
};

</script>

<style lang="css" scoped>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
li {
  list-style: none;
}
.navbar-vertical {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100dvh;
  padding:20px 10px 50px 10px;
  background-color: #022213;
  color: white;
}
.navbar-vertical__extendido {
  width: 300px;
  max-width: 300px;
  padding:20px 10px 50px 10px;
}
.navbar-vertical__item,
.navbar-vertical__dark-mode-container {
  display: flex;
  align-items: center;
  justify-content: start;
  gap: 15px;
}
.navbar-vertical__menu-container {
  display: flex;
  flex-direction: column;
  gap: 30px;
}
.navbar-vertical__item--menu,
.navbar-vertical__item--profile,
.navbar-vertical__item--wallet,
.navbar-vertical__item--communities,
.navbar-vertical__item--notifications,
.navbar-vertical__dark-mode-container {
  padding: 10px ;
  border-radius: 5px;
}
.navbar-vertical__list {
  display: flex;
  flex-direction: column;
  gap: 25px;
}
.navbar-vertical__item:hover,
.navbar-vertical__dark-mode-container:hover {
  background-color: #011b0f;
  & img {
    background-color: #011b0f;
  }
  & button {
    background-color: #011b0f;
  }
}

.navbar-vertical__item-text {
  font-size: 28px;
}

.ativo {
  width: 300px;
}
.navbar-vertical__button,
.navbar-vertical__menu-button,
.navbar-vertical__dark-mode-button {
  border: none;
  background-color: #022213;
  cursor: pointer;
}
</style>
