<script setup>
import { ref } from "vue";

const props = defineProps({
  addDataToList: Function,
});

const text = ref("");

const add = () => {
  if (!text.value.trim()) return;

  props.addDataToList({
    id: Date.now(),
    text: text.value,
    isCompleted: false,
  });
  text.value = "";
};
</script>

<template>
  <input v-model="text" @keyup.enter="add" placeholder="輸入代辦事項" />
</template>

<style scoped>
input {
  box-sizing: border-box;
  width: 100%;
  padding: 4px 8px;
  border: 2px solid #a17c6b;
  border-radius: 4px;
  font-size: 16px;
  outline: none;
}
</style>
