<script setup>
import { toRefs } from "vue";

const props = defineProps({
  isVisible: Boolean,
  onClose: Function,
  onConfirm: Function,
});

const { isVisible, onClose, onConfirm } = toRefs(props);
</script>

<template>
  <Teleport to="body">
    <div v-show="isVisible" class="mask">
      <div class="modal">
        <h2>確定要刪除嗎?</h2>
        <div class="btn-group">
          <button @click="onClose">取消</button>
          <button @click="onConfirm">確定</button>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
.mask {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.5);
}
.modal {
  background-color: #ceb5a7;
  width: 420px;
  margin: 60px auto;
  padding: 20px 0;
  text-align: center;
  border: 4px solid #a17c6b;
  border-radius: 8px;
  color: #1f2421;
}
h2 {
  margin-bottom: 60px;
}
.btn-group {
  margin: 20px 0;
}

button {
  margin: 8px;
  font-size: 20px;
  padding: 6px 12px;
  border: 2px solid #a17c6b;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  color: #a17c6b;
}
</style>
