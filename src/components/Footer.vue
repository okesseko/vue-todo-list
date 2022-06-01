<script setup>
import { ref, computed, toRefs } from "vue";
import Modal from "./Modal.vue";

const props = defineProps({
  list: Object,
  onSelect: Function,
  removeSelectedData: Function,
});

const { list } = toRefs(props);

let isModalOpen = ref(false);

const finishedItemCount = computed(() => {
  return list.value.reduce((prev, curr) => (curr.isCompleted ? prev + 1 : prev), 0);
});

const selectAll = (event) => {
  props.onSelect(event.target.checked);
};

const closeModal = () => {
  isModalOpen.value = false;
};

const onConfirm = () => {
  props.removeSelectedData();
  closeModal();
};
</script>

<template>
  <div class="wrapper">
    <div>
      <input
        type="checkbox"
        :checked="finishedItemCount === list.length"
        @click="selectAll"
      />
      <span>已完成: {{ finishedItemCount }} / 總共 {{ list.length }} </span>
    </div>
    <button @click="isModalOpen = true">刪除勾選事項</button>
  </div>
  <Modal
    :onClose="closeModal"
    :onConfirm="onConfirm"
    :isVisible="isModalOpen"
  />
</template>

<style scoped>
.wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
