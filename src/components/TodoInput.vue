<script setup>
import { ref } from "vue";

// 1. Events 定義
const emit = defineEmits(["add-task"]);

// 2. 響應式數據
const newTask = ref("");

// 3. 方法定義
const handleAddTask = () => {
  if (newTask.value.trim() !== "") {
    emit("add-task", newTask.value.trim());
    newTask.value = "";
  }
};
</script>

<template>
  <div class="todo-input">
    <input
      type="text"
      v-model="newTask"
      @keyup.enter="handleAddTask"
      placeholder="輸入一件事"
    />
  </div>
</template>

<style scoped>
.todo-input {
  margin-bottom: 20px;
}
input {
  width: 100%;
  padding: 8px;
}
</style>
