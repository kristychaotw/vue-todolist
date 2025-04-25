<script setup>
import { ref, watch } from "vue";
import TodoInput from "./components/TodoInput.vue";
import TodoItem from "./components/TodoItem.vue";
import UserName from "./components/UserName.vue";

// 1. 響應式數據
const tasks = ref([]);
const title = ref("Kristy's Todo List");

// 2. 方法定義
const loadTasks = () => {
  const savedTasks = localStorage.getItem("tasks");
  const savedTitle = localStorage.getItem("title");
  if (savedTasks) {
    tasks.value = JSON.parse(savedTasks);
  }
  if (savedTitle) {
    title.value = savedTitle;
  }
};

const saveTasks = () => {
  localStorage.setItem("tasks", JSON.stringify(tasks.value));
  localStorage.setItem("title", title.value);
};

const handleAddTask = (text) => {
  tasks.value.push({
    id: Date.now(),
    text,
    done: false,
  });
};

const handleToggleDone = (id) => {
  const task = tasks.value.find((task) => task.id === id);
  if (task) {
    task.done = !task.done;
  }
};

const handleDeleteTask = (id) => {
  tasks.value = tasks.value.filter((task) => task.id !== id);
};

// 3. 監聽器
watch(
  [tasks, title],
  () => {
    saveTasks();
  },
  { deep: true }
);

// 4. 生命週期鉤子
loadTasks();
</script>

<template>
  <div class="app">
    <!-- 使用者名稱 -->
    <UserName v-model="title" />
    <!-- 輸入元件 -->
    <TodoInput @add-task="handleAddTask" />
    <!-- 任務列表 -->
    <ul>
      <TodoItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @toggle-done="handleToggleDone"
        @delete-task="handleDeleteTask"
      />
    </ul>
  </div>
</template>

<style scoped>
.app {
  max-width: 500px;
  width: 100%;
  margin: 40px auto;
  font-family: sans-serif;
}

ul {
  list-style-type: none;
  padding: 0;
  width: 100%;
}
</style>
