<script setup>
import { ref } from 'vue'

const props = defineProps({
  task: Object,
})

const emit = defineEmits(['deleteTask', 'editTask'])

const title = ref(props.task.taskName)
const description = ref(props.task.taskDescription)

function deleteTask() {
  emit('deleteTask')
}

const editMode = ref(false)

function setMode(text) {
  if (text === 'edit') {
    editMode.value = true
  } else {
    const data = {
      ...props.task,
      taskName: title.value,
      taskDescription: description.value
    }
    emit('editTask', data)
    editMode.value = false
  }
}
</script>

<template>
  <div class="toDoContainer">
    <label class="custom-checkbox">
      <input type="checkbox" />
    </label>
    <div class="textContainer">
      <div>
        <div v-if="editMode">
          <input v-model="title" type="text" />
        </div>
        <div v-else class="taskName">
          {{ task.taskName }}
        </div>
      </div>
      <div v-if="editMode">
        <input v-model="description" type="text"/>
      </div>
      <div v-else class="taskDescription">
        {{ task.taskDescription }}
      </div>
    </div>
    <div class="buttonsContainer">
      <button @click="deleteTask" class="button">Удалить</button>
      <button v-if="editMode === false" @click="setMode('edit')" class="button-two">
        <img src="./assets/edit.jpeg" alt="edit button" class="image-button" />
      </button>
      <button v-else @click="setMode('save')" class="button-two">
        <img src="./assets/save.jpeg" alt="save button" class="image-button" />
      </button>
    </div>
  </div>
</template>

<style scoped>
.toDoContainer {
  width: 512px;
  height: 130px;
  border-radius: 12px;
  padding: 24px;
  gap: 16px;
  margin-bottom: 20px;
  background-color: #f4f2ff;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.textContainer {
  display: flex;
  flex-direction: column;
}

.image-button {
  width: 20px;
  height: 20px;
}

.button {
  border-radius: 10px;
    color: white;
    transition: .2s linear;
    background: #2B1887;
    margin-top: 8px;
    padding: 5px;
}

.button:hover {
  box-shadow: 0 0 0 2px white, 0 0 0 4px #2B1887;
}

.button-two {
  border-radius: 10px;
    color: white;
    transition: .2s linear;
    background: #ffffff;
    margin-top: 8px;
    padding: 5px;
}

.button-two:hover {
  box-shadow: 0 0 0 2px white, 0 0 0 4px #2B1887;
}

.buttonsContainer {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
}

.custom-checkbox {
  background-color: rgba(219, 157, 252, 0.303);
  border-radius: 5px;
}

.taskName {
 font-size: 25px;
 font-weight: 500;
}

.taskDescription {
  font-size: 20px;
  font-style: italic;
  color: #2B1887;
  ;
}
</style>
