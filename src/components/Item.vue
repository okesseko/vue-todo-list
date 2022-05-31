<script setup>
import { ref, toRefs } from "vue";

const props = defineProps({
  data: Object,
  removeData: Function,
  index: Number,
});

const { data, index } = toRefs(props);
const isHover = ref(false);

const remove = () => {
  props.removeData(index);
};
</script>

<template>
  <li @mouseenter="isHover = true" @mouseleave="isHover = false">
    <label>
      <input type="checkbox" v-model="data.isCompleted" />
      <span>{{ data.text }}</span>
    </label>
    <button v-show="isHover" @click="remove">刪除</button>
  </li>
</template>

<style scoped>
li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 30px;
  margin: 4px 0;
  padding-right: 8px;
}
li:hover {
  color: #e0f2e9;
}

label {
  cursor: pointer;
}
input {
  margin-right: 8px;
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
</style>
