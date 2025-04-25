<script setup>
import { ref } from "vue";

// 1. Props 定義
const props = defineProps({
  modelValue: {
    type: String,
    required: true,
  },
});

// 2. Events 定義
const emit = defineEmits(["update:modelValue"]);

// 3. 響應式數據
const isEditing = ref(false);

// 4. 方法定義
const handleClick = () => {
  isEditing.value = true;
};

const handleInput = (event) => {
  emit("update:modelValue", event.target.value);
};

const handleBlur = () => {
  isEditing.value = false;
};

const handleKeyup = (event) => {
  if (event.key === "Enter") {
    isEditing.value = false;
  }
};
</script>

<template>
  <div class="user-name" @click="handleClick">
    <input
      v-if="isEditing"
      type="text"
      :value="modelValue"
      @input="handleInput"
      @blur="handleBlur"
      @keyup="handleKeyup"
      ref="inputRef"
      placeholder="輸入你的名字"
      class="title-input"
    />
    <h1 v-else class="title-text">{{ modelValue }}'s Todo List</h1>
  </div>
</template>

<style scoped>
.user-name {
  margin-bottom: 20px;
  cursor: pointer;
  min-width: 400px;
}

.title-input,
.title-text {
  width: 100%;
  min-width: 200px;
  font-size: 24px;
  font-weight: bold;
  padding: 8px;
  margin: 0;
  border: none;
  outline: none;
  background: transparent;
  box-sizing: border-box;
  display: block;
}

.title-input {
  border-bottom: 2px solid #42b983;
}

.title-text {
  border-bottom: 2px solid transparent;
}
</style>
