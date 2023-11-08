<script setup>
import { ref } from 'vue'

let newTask = ref('')
let taskList = ref([
  { text: 'Estudiar', done: false },
  { text: 'Jugar play', done: true }
])

function addTask() {
  if (newTask.value.trim() == '') return

  taskList.value.push({
    text: newTask.value,
    done: false
  })

  newTask.value = ''
}

function setDone(index) {
  // if(taskList.value.done){

  taskList.value[index].done = !taskList.value[index].done

  // }else{
  //   taskList.value[index].done =false;
  // }
}

function deleteTask(index) {
  taskList.value.splice(index, 1)
}
</script>

<template>
  <div class="card">
    <h1>Lista de cosas</h1>
    <p class="subtittle">{{ newTask }}</p>
    <div>
      <!-- <div class="task" >Tarea 1 <span  class="button">x</span></div>| -->
      <div v-for="(task, index) in taskList" :key="index" class="task" :class="{ done: task.done }">
        {{ task.text }}
        <span @dblclick="deleteTask(index)" @click="setDone(index)" class="button">x</span>
      </div>
    </div>

    <div>
      <input
        v-model="newTask"
        @keypress.enter="addTask"
        type="text"
        placeholder="Escribe tu tarea"
      />

      <p class="help" v-show="newTask != ''">Presiona enter para confirmar</p>
    </div>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
  background-color: #161f30;
}

.card {
  font-family: 'Lato', sans-serif;
  background-color: #b4bec9;
  max-width: 520px;
  border-radius: 8px;
  padding: 18px 16px;
  margin: 0 auto;
}

h1 {
  text-transform: uppercase;
  text-align: center;
  padding: 0;
  margin: 0;
  font-size: 24px;
}

.subtittle {
  text-align: center;
  margin: 0;
  padding: 0;
  opacity: 0.6;
  margin-bottom: 12px;
}

.task {
  background-color: #deefe7;
  border-radius: 4px;
  padding: 2px 8px;
  padding-right: 2px;
  margin-bottom: 4px;
  display: flex;
  justify-content: space-between;
}

.task:hover {
  background-color: #159a9c;
}

.button {
  background-color: #b4bec9;
  padding: 0 5px;
  border-radius: 2px;
  color: white;
}

.button:hover {
  cursor: pointer;
  background-color: #84b026;
}

input {
  width: 100%;
  border: none;
  outline: none;
  padding: 3px 4px;
  border-radius: 4px;
  box-sizing: border-box;
}

.help {
  margin: 0;
  font-size: 12px;
  opacity: 0.4;
}
</style>
