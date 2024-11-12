<script setup>
import { computed, ref } from 'vue';
import { v4 as uuidv4 } from 'uuid';

const emit = defineEmits(['addTask'])

const taskName = ref('')
const taskDescription = ref('')

function addTask() {
  const newTask = {
    taskName: taskName.value,
    taskDescription:taskDescription.value,
    id: uuidv4(),
    status: false,
  }
  emit('addTask', newTask)
  taskName.value = ''
  taskDescription.value = ''
}
const isDisabled = computed(() => {
  console.log(taskName.value && taskDescription.value)
  return !(taskName.value && taskDescription.value)
})
</script>

<template>
  <div class="new-task-layout">
    <input v-model="taskName" type="text" />
    <input v-model="taskDescription" type="text" />
    <button class="new-todo-btn" @click="addTask" :disabled="!!isDisabled" >Добавить новую задачу</button>
  </div>
</template>

<style>
.new-todo-btn {
  border-radius: 10px;
    color: white;
    transition: .2s linear;
    background: #2B1887;
    margin-top: 8px;
    padding: 5px;
}

.new-todo-btn:hover {
  box-shadow: 0 0 0 2px white, 0 0 0 4px #2B1887;
}

.new-todo-btn:disabled {
  box-shadow: 0 0 0 2px white, 0 0 0 4px #f9f5f5;
  cursor: not-allowed;
}

.new-task-layout {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  gap: 5px;
}
</style>
