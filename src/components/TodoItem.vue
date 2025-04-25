<script setup>
// 1. Props 定義
const props = defineProps({
  task: {
    type: Object,
    required: true,
  },
});

// 2. Events 定義
const emit = defineEmits(["toggle-done", "delete-task"]);

// 3. 方法定義
const handleToggleDone = () => {
  emit("toggle-done", props.task.id);
};

const handleDelete = () => {
  emit("delete-task", props.task.id);
};
</script>

<template>
  <li class="todo-item">
    <input type="checkbox" :checked="task.done" @change="handleToggleDone" />
    <span :class="{ completed: task.done }">{{ task.text }}</span>
    <button @click="handleDelete">刪除</button>
  </li>
</template>

<style scoped>
.todo-item {
  width: 100%;
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 5px;
}
.completed {
  text-decoration: line-through;
  color: #999;
}
button {
  margin-left: auto;
}
</style>
