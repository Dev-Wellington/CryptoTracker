<template>
  <form @submit.prevent="updateInput" class="search-form">
    <input
      type="text"
      placeholder="Search for a cryptocurrency (e.g., Polkadot)"
      v-model="localValue"
      class="search-input"
    />
    <button class="btn" type="submit">
      <img :src="getIconPath('search')" alt="Search" class="search-icon" />
    </button>
  </form>
</template>

<script setup>
import { ref, watch } from "vue";

const props = defineProps({
  modelValue: {
    type: String,
    required: true,
  },
  darkMode: {
    type: Boolean,
    default: false,
  },
});

const getIconPath = (iconName) => {
  return props.darkMode
    ? new URL(`../assets/icons/dark/${iconName}.svg`, import.meta.url).href
    : new URL(`../assets/icons/light/${iconName}.svg`, import.meta.url).href;
};

const emit = defineEmits(["update:modelValue"]);
const localValue = ref("");

const updateInput = () => {
  emit("update:modelValue", localValue.value);
};

watch(
  () => props.modelValue,
  (newValue) => {
    if (!localValue.value) {
      localValue.value = newValue || "";
    }
  }
);
</script>

<style lang="css" scoped>
form {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  gap: clamp(10px, 3vw, 30px);
  width: 100%;
  background-color: var(--bg-search);
  padding: clamp(10px, 2vw, 20px);
  transition: background-color 0.3s;
}

input {
  display: block;
  width: clamp(300px, 50%, 700px);
  height: clamp(18px, 3vw, 75px);
  background-color: #f0f0f0;
  color: var(--text-color);
  border-radius: 15px;
  font-size: clamp(12px, 2vw, 16px);
  border: none;
  padding-left: clamp(10px, 2vw, 20px);
}
input:focus {
  outline: none;
}
input::placeholder {
  color: var(--text-color);
  font-size: clamp(12px, 2vw, 16px);
}

.btn {
  border: none;
  position: absolute;
  width: clamp(18px, 3vw, 45px);
  height: clamp(18px, 3vw, 45px);
  cursor: pointer;
  background-color: transparent;
  margin-right: clamp(10px, 2vw, 20px);
  & img {
    width: 100%;
    height: 100%;
  }
}

.btn:hover {
  filter: drop-shadow(0 0 10px var(--bg-buttons-hover));
}

@media (width <= 480px) {
  input {
    height: 35px;
  }
}
</style>
