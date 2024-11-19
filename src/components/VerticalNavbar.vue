<script setup>
import { ref } from "vue";
const clicar = ref(false);

const click = () => {
  clicar.value = !clicar.value;
};
</script>

<template>
  <div class="container">
    <nav class="navbar-vertical" :class="{ 'navbar-vertical__extend': clicar }">
      <div class="navbar-vertical__menu-container">
        <div class="navbar-vertical__item navbar-vertical__item--menu">
          <button class="navbar-vertical__menu-button" @click="click">
            <img src="../assets/icons/menu.svg" alt="Menu Icon" />
          </button>
          <p class="navbar-vertical__item-text" v-if="clicar">Menu</p>
        </div>
        <div class="navbar-vertical__list-container">
          <ul class="navbar-vertical__list">
            <li class="navbar-vertical__item navbar-vertical__item--profile">
              <button class="navbar-vertical__button">
                <img src="../assets/icons/profile.svg" alt="Profile Icon" />
              </button>
              <p class="navbar-vertical__item-text" v-if="clicar">Profile</p>
            </li>
            <li class="navbar-vertical__item navbar-vertical__item--wallet">
              <button class="navbar-vertical__button">
                <img src="../assets/icons/wallet.svg" alt="Wallet Icon" />
              </button>
              <p class="navbar-vertical__item-text" v-if="clicar">Wallets</p>
            </li>
            <li
              class="navbar-vertical__item navbar-vertical__item--communities"
            >
              <button class="navbar-vertical__button">
                <img
                  src="../assets/icons/communities.svg"
                  alt="Communities Icon"
                />
              </button>
              <p class="navbar-vertical__item-text" v-if="clicar">
                Communities
              </p>
            </li>
            <li
              class="navbar-vertical__item navbar-vertical__item--notifications"
            >
              <button class="navbar-vertical__button">
                <img
                  src="../assets/icons/notifications.svg"
                  alt="Notifications Icon"
                />
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
            alt="Change mode Icon"
          />
        </button>
        <p class="navbar-vertical__item-text" v-if="clicar">Mode</p>
      </div>
    </nav>
  </div>
</template>

<style lang="css" scoped>
.container {
  margin-right: 6%;
}
li {
  list-style: none;
}
.navbar-vertical {
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  height: 100dvh;
  padding: clamp(10px, 2vw, 20px) clamp(5px, 1vw, 10px) clamp(25px, 5vw, 50px)
    clamp(5px, 1vw, 10px);
  width: clamp(50px, 100%, 85px);
  background-color: var(--bg-navbar);
  color: var(--text-color-coins);
  transition: width 0.5s ease-in-out;
}

.navbar-vertical__extend {
  width: clamp(150px, 20vw, 300px);
  max-width: 300px;
  padding: clamp(10px, 2vw, 20px) clamp(5px, 1vw, 10px) clamp(25px, 5vw, 50px)
    clamp(5px, 1vw, 10px);
  box-shadow: 2px 0 5px rgba(0, 0, 0, 0.5);
}
.navbar-vertical__item,
.navbar-vertical__dark-mode-container {
  display: flex;
  align-items: center;
  justify-content: start;
  gap: clamp(5px, 1.5vw, 15px);
}
.navbar-vertical__menu-container {
  display: flex;
  flex-direction: column;
  gap: clamp(10px, 3vw, 30px);
}
.navbar-vertical__item--menu,
.navbar-vertical__item--profile,
.navbar-vertical__item--wallet,
.navbar-vertical__item--communities,
.navbar-vertical__item--notifications,
.navbar-vertical__dark-mode-container {
  padding: clamp(5px, 1.5vw, 10px);
  border-radius: 5px;
}
.navbar-vertical__list {
  display: flex;
  flex-direction: column;
  gap: clamp(10px, 3vw, 25px);
}
.navbar-vertical__item:hover,
.navbar-vertical__dark-mode-container:hover {
  background-color: var(--bg-navbar-icon-hover);
  & img {
    background-color: var(--bg-navbar-icon-hover);
  }
  & button {
    background-color: var(--bg-navbar-icon-hover);
  }
}

.navbar-vertical__item-text {
  font-size: clamp(14px, 2vw, 28px);
}
.navbar-vertical__button,
.navbar-vertical__menu-button,
.navbar-vertical__dark-mode-button {
  border: none;
  background-color: var(--bg-navbar);
  cursor: pointer;
}
button > img {
  width: clamp(18px, 3vw, 45px);
  height: clamp(18px, 3vw, 45px);
}
</style>
