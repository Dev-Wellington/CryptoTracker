<script setup>
import { ref } from "vue";

const props = defineProps({
  darkMode: Boolean,
});
const emit = defineEmits(["toggle-dark-mode"]);
const clicar = ref(false);

const click = () => {
  clicar.value = !clicar.value;
};
const toggleDarkMode = () => {
  emit("toggle-dark-mode");
};
const getIconPath = (iconName) => {
  const path = props.darkMode
    ? new URL(`../assets/icons/dark/${iconName}.svg`, import.meta.url).href
    : new URL(`../assets/icons/light/${iconName}.svg`, import.meta.url).href;
  return path;
};
</script>

<template>
  <div class="container">
    <nav class="navbar-vertical" :class="{ 'navbar-vertical__extend': clicar }">
      <div class="navbar-vertical__menu-container">
        <div class="navbar-vertical__item navbar-vertical__item--menu">
          <button class="navbar-vertical__menu-button" @click="click">
            <img :src="getIconPath('menu')" alt="Menu Icon" />
            <p class="navbar-vertical__item-text" v-if="clicar">Menu</p>
          </button>
        </div>
        <div class="navbar-vertical__list-container">
          <ul class="navbar-vertical__list">
            <li class="navbar-vertical__item navbar-vertical__item--profile">
              <button class="navbar-vertical__button">
                <img :src="getIconPath('profile')" alt="Profile Icon" />
                <p class="navbar-vertical__item-text" v-if="clicar">Profile</p>
              </button>
            </li>
            <li class="navbar-vertical__item navbar-vertical__item--wallet">
              <button class="navbar-vertical__button">
                <img :src="getIconPath('wallet')" alt="Wallet Icon" />
                <p class="navbar-vertical__item-text" v-if="clicar">Wallets</p>
              </button>
            </li>
            <li
              class="navbar-vertical__item navbar-vertical__item--communities"
            >
              <button class="navbar-vertical__button">
                <img :src="getIconPath('communities')" alt="Communities Icon" />
                <p class="navbar-vertical__item-text" v-if="clicar">
                  Communities
                </p>
              </button>
            </li>
            <li
              class="navbar-vertical__item navbar-vertical__item--notifications"
            >
              <button class="navbar-vertical__button">
                <img
                  :src="getIconPath('notifications')"
                  alt="Notifications Icon"
                />
                <p class="navbar-vertical__item-text" v-if="clicar">
                  Notifications
                </p>
              </button>
            </li>
          </ul>
        </div>
      </div>
      <div class="navbar-vertical__dark-mode-container">
        <button
          class="navbar-vertical__dark-mode-button"
          @click="toggleDarkMode"
        >
          <img
            class="navbar-vertical__dark-mode-icon"
            :src="getIconPath('dark_mode')"
            alt="Change mode Icon"
          />
          <p class="navbar-vertical__item-text" v-if="clicar">Mode</p>
        </button>
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
  transition: width 0.5s ease, background-color 0.3s ease-in-out;
}

.navbar-vertical__extend {
  width: clamp(150px, 20vw, 300px);
  max-width: 300px;
  padding: clamp(10px, 2vw, 20px) clamp(5px, 1vw, 10px) clamp(25px, 5vw, 50px)
    clamp(5px, 1vw, 10px);
  box-shadow: 2px 0 5px rgba(0, 0, 0, 0.5);
  transition: width 0.5s ease, background-color 0.3s ease-in-out;
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
  transition: background-color 0.3s ease-in-out;
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
  display: flex;
  align-items: center;
  gap: clamp(5px, 1.5vw, 15px);
  width: 100%;
  border: none;
  background-color: var(--bg-navbar);
  cursor: pointer;

  transition: background-color 0.3s ease-in-out;
}

button > img {
  width: clamp(18px, 3vw, 45px);
  height: clamp(18px, 3vw, 45px);
}
</style>
