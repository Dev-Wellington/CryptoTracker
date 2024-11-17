<template>
  <form @submit.prevent="updateInput">
    <input
      type="text"
      placeholder="Search for a cryptocurrency (e.g., Polkadot)"
      v-model="localValue"
    />
    <button class="btn" type="submit"></button>
  </form>
</template>
<script setup>
import { ref, watch } from "vue";

const props = defineProps(["modelValue"]);
const emit = defineEmits(["update:modelValue"]);
const localValue = ref("");

const updateInput = () => {
  emit("update:modelValue", localValue.value || props.modelValue);
};

watch(
  () => props.modelValue,
  (newValue) => {
    if (!localValue.value) {
      localValue.value = "";
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
  background-color: #011b0f;
  padding: clamp(10px, 2vw, 20px);
}

input {
  display: block;
  width: clamp(300px, 50%, 700px);
  height: clamp(18px, 3vw, 75px);
  background-color: #f0f0f0;
  color: #011b0f;
  border-radius: 15px;
  font-size: clamp(12px, 2vw, 16px);
  border: none;
  padding-left: clamp(10px, 2vw, 20px);
}

input::placeholder {
  color: #011b0f;
  font-size: clamp(12px, 2vw, 16px);
}

.btn {
  border: none;
  position: absolute;
  width: clamp(18px, 3vw, 45px);
  height: clamp(18px, 3vw, 45px);
  cursor: pointer;
  background-color: transparent;
  background-image: url("../assets/icons/search.svg");
  background-repeat: no-repeat;
  background-size: clamp(18px, 3vw, 45px) clamp(18px, 3vw, 45px);
  margin-right: clamp(10px, 2vw, 20px);
}

.btn:hover {
  filter: drop-shadow(0 0 10px #b0ec69);
}

@media (width <= 480px) {
  input {
    height: 35px;
  }
}
</style>
