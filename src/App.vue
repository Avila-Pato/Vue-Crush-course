<script setup>
import { ref } from 'vue'

const name = ref('Jon Doe')
const status = ref('active') // Reactivo
const tasks = ref(['Task: 1', 'Task: 2', 'Task: 3'])
const link = ref('http://google.com')
const newTask = ref('')

const ToogleButton = () => {
  if (status.value === 'active') {
    status.value = 'pending'
  } else if (status.value === 'pending') {
    status.value = 'inactive'
  } else {
    status.value = 'active'
  }
}

const addTask = () => {
  // vorra los espacion e blanco y verifica que no este vacio
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value)
    newTask.value = ''
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}
</script>

<template>
  <div>
    <h1>{{ name }}</h1>
    <br />
    <p v-if="status === 'active'">User is active</p>
    <p v-else-if="status === 'pending'">User is pending</p>
    <p v-else>User is inactive</p>
    <br />
    <button @click="ToogleButton">PushMe</button>

    <!-- Formulario -->

    <form @submit.prevent="addTask">
      addTask
      <label for="newTask">Add Task</label>
      <input
        type="text"
        placeholder="add a new task"
        id="newTask"
        name="newTask"
        v-model="newTask"
      />
      <button type="submit">submit</button>
    </form>
    <!-- Recorrer array de tareas -->
    <ul>
      <li v-for="(task, index) in tasks" :key="task">
        {{ task }}
        <button @click="deleteTask(index)">delete</button>
      </li>
    </ul>
    <!-- Enlace dinámico -->
    <a :href="link" target="_blank">Click to Google</a>
  </div>
</template>
