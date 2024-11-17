<script setup>
import { ref } from 'vue';
import NewToDo from './NewToDo.vue';
import ToDoItem from './ToDoItem.vue';
import CardPattern from './CardPattern.vue';

const toDoTasks = ref([])

function addTask(data) {
  toDoTasks.value.push(data)
}

function deleteTask(id) {
  toDoTasks.value = toDoTasks.value.filter((el) => el.id !== id)
  console.log('hi')
}

const editTask = (data) => {
  toDoTasks.value = toDoTasks.value.map((el) => {
    if (el.id === data.id) {
      return {
        ...data
      }
    }
  })
  toDoTasks.value = []
}

const cards = [
  {
    id: 1,
    isImportant: true,
  },
  {
    id: 2,
    isImportant: false,
  },
  {
    id: 3,
    isImportant: true,
  },
]
</script>

<template>
<div class="background-container">
  <div class="container">
    <h1 class="headerText">My To Do List</h1>
    <div class="tasks">
      <ToDoItem
        v-for="(task, i) in toDoTasks"
        :key="i"
        :task="task"
        @delete-task="deleteTask(task.id)"
        @editTask="editTask"
      >
      </ToDoItem>
    </div>
    <NewToDo @add-task="addTask">

    </NewToDo>
  </div>
</div>
<div class="cards">
    <CardPattern v-for="(card, index) in cards" :key="index" :is-important="card.isImportant"/>
  </div>
</template>

<style>
.container {
  display: flex;
  justify-content: center;
  flex-direction: column;
  gap: 15px;
  background-color: #D5CCFF;
  padding: 24px;
  width: 560px;
  border-radius: 16px;
  box-shadow: 10px 5px 50px rgb(26, 1, 71);
}

.headerText {
  display: flex;
  justify-content: center;
  color: #2B1887;
  font-size: 32px;
}

.background-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 50px;
}

body {
  background-color: #2B1887;
}

.cards {
  display: flex;
  gap: 20px;
  justify-content: center;
}

</style>

