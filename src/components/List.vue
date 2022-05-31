<script setup>
import Item from "./Item.vue";
import Modal from "./Modal.vue";
import { ref, toRefs } from "vue";

const props = defineProps({
  list: Array,
  removeData: Function,
});

const { list } = toRefs(props);
let isModalOpen = ref(false);
let removedIndex = ref(0);

const closeModal = () => {
  isModalOpen.value = false;
};

const onConfirm = () => {
  props.removeData(removedIndex);
  closeModal();
};

const remove = (index) => {
  removedIndex.value = index;
  isModalOpen.value = true;
};
</script>

<template>
  <ul>
    <Item
      v-for="(data, index) in list"
      :key="data.id"
      :data="data"
      :removeData="remove"
      :index="index"
    />
  </ul>
  <Modal
    :onClose="closeModal"
    :onConfirm="onConfirm"
    :isVisible="isModalOpen"
  />
</template>

<style scoped>
ul {
  width: 100%;
  margin: 16px auto;
  padding: 0;
  list-style: none;
}
</style>
