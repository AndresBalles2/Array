<script setup>
import {ref} from 'vue'

let newTask = ref('')

let taskList = ref([
  
])

function setDone(index){
  taskList.value[index].done = true
}

function addTask(){
  if(newTask.value.trim() === '') return 
  taskList.value.push({
    name: newTask.value,
    done: false
  })
  newTask.value= ''
}

</script>

<template>
  <div class="container">
    <h1>Lista de tareas</h1>
    <p class="subtitle">{{ newTask }}</p>

    <div>
      <div class="task" :class="{done: task.done}" v-for="(task, index) in taskList" :key="index">{{ task.name }} <span @click="setDone(index)" class="button">x</span></div>
    </div>

    <input v-model="newTask" @keypress.enter="addTask" type="text" placeholder="escribe tu tarea">
    <p v-show="newTask != ''" class="help">Presiona enter para agregar la tarea</p>
  </div>
</template>

<style scoped>

  .done{
    text-decoration: line-through;
  }
  .container{
    color: #595959;
    padding: 6px 12px;
    font-family: 'Kite One', sans-serif;
    background-color: #D9CDB8;
    border-radius: 6px;
    max-width: 420px;
    margin: 0 auto;
  }

  .subtitle{
    font-size: 10px;
    margin: 0;
    margin-bottom: 16px;
    text-align: center;
    opacity: 0.7;
  }

  h1{
    text-transform: uppercase;
    font-size: 20px;
    margin-bottom: 0;
    margin-top: 12px;
    text-align: center;
  }

  .button{
    background-color: #D9CDB8;
    display: inline-block;
    padding: 0 6px;
    border-radius: 3px;
    color: azure;
  }

  .button:hover{
    cursor: pointer;
  }

  .task{
    background-color: #F2E6CE;
    border-radius: 3px;
    margin-bottom: 3px;
    padding: 2px 2px 2px 6px;
    display: flex;
    justify-content: space-between;
  }

  input{
    border: none;
    border-radius: 3px;
    padding: 2px 6px;
    outline: none;
    width: 100%;
    box-sizing: border-box;
    margin-top: 10px;
    margin-bottom: 6px;
    text-align: center;
    font-size: 12px;
  }

  input::placeholder{
    opacity: 0.4;
  }

  .task:hover{
    background-color: rgba(242, 242, 242, 0.4);
  }

  .help{
    font-size: 10px;
    margin: 0;
    text-align: center;
    opacity: 0.8;
  }

</style>
