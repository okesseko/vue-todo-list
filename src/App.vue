<script setup>
import Header from "./components/Header.vue";
import List from "./components/List.vue";
import Footer from "./components/Footer.vue";
import { reactive, ref } from "vue";

let listData = reactive([
  { id: 1, text: "吃飯", isCompleted: false },
  { id: 2, text: "打掃", isCompleted: true },
  { id: 3, text: "喝水", isCompleted: false },
]);

const addDataToList = (data) => {
  listData.unshift(data);
};

const removeData = (index) => {
  console.log("remove");
  listData.splice(index, 1);
};
</script>

<template>
  <Header :addDataToList="addDataToList" />
  <List :list="listData" :removeData="removeData" />
  <Footer />
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
</style>
