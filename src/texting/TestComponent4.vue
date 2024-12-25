<script setup name="TestFourComponentExample">
import { onMounted, ref } from 'vue'

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
  // Borra los espacios en blanco y verifica que no esté vacío
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value)
    newTask.value = ''
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}

onMounted(async () => {
  try {
    const response = await fetch('https://pokeapi.co/api/v2/pokemon?offset=20&limit=20')
    const data = await response.json()
    tasks.value = data.results.map((task) => task.name)
  } catch (error) {
    console.log('Error fetching tasks', error)
    tasks.value = ['Error loading tasks']
  }
  // defineComponent is not needed in <script setup>
})
</script>

<template>
  <div class="bg-red-500 text-green-400 p-4">Tailwind está funcionando.</div>

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
      <label for="newTask">Add Task</label>
      <input
        type="text"
        placeholder="add a new task"
        id="newTask"
        name="newTask"
        v-model="newTask"
      />
      <button type="submit">Submit</button>
    </form>

    <!-- Recorrer array de tareas -->
    <ul class="text-red-500">
      <li v-for="(task, index) in tasks" :key="`${task}-${index}`">
        {{ task }}
        <button @click="deleteTask(index)" class="ml-2 text-blue-500 hover:underline">
          Delete
        </button>
      </li>
    </ul>

    <!-- Enlace dinámico -->
    <a :href="link" target="_blank">Click to Google</a>
  </div>
</template>
