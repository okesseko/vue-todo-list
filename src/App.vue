<script setup>
import Header from "./components/Header.vue";
import List from "./components/List.vue";
import Footer from "./components/Footer.vue";
import { onMounted, ref, watch } from "vue";

const DEFAULT_LIST_DATA = [
  { id: 1, text: "吃飯", isCompleted: false },
  { id: 2, text: "打掃", isCompleted: true },
  { id: 3, text: "喝水", isCompleted: false },
];

let listData = ref([]);

onMounted(() => {
  const storageData = localStorage.getItem("list_data");
  listData.value = storageData ? JSON.parse(storageData) : DEFAULT_LIST_DATA;
});

const addDataToList = (data) => {
  listData.value.unshift(data);
};

const removeData = (index) => {
  listData.value.splice(index, 1);
};

const removeSelectedData = () => {
  console.log(listData.value.filter((data) => !data.isCompleted));
  listData.value = listData.value.filter((data) => !data.isCompleted);
};

const selectAll = (isSelected) => {
  listData.value.forEach((data) => {
    data.isCompleted = isSelected;
  });
};

watch(
  listData,
  (val) => {
    localStorage.setItem("list_data", JSON.stringify(val));
  },
  { deep: true }
);
</script>

<template>
  <h1>Vue3 todo list practice</h1>
  <Header :addDataToList="addDataToList" />
  <List :list="listData" :removeData="removeData" />
  <Footer
    :list="listData"
    :onSelect="selectAll"
    :removeSelectedData="removeSelectedData"
  />
</template>

<style>
body {
  background-color: #e0f2e9;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #ceb5a7;

  width: 360px;
  margin: 60px auto;

  border: 2px solid #a17c6b;
  border-radius: 8px;
  padding: 24px 36px;

  text-align: center;
  color: #1f2421;
}
button {
  border: 1px solid #a17c6b;
  border-radius: 4px;
  padding: 4px;
  cursor: pointer;
}
button:hover {
  color: #a17c6b;
}
input[type="checkbox"] {
  margin-right: 8px;
}
</style>
