<script>
export default {
  name: 'TextComponent',
  data() {
    return {
      name: 'Jhon Doe',
      status: 'active',
      task: ['Task: 1', 'Task: 2', 'Task: 3', 'Task: 4'],
      link: 'http://google.com',
    }
  },
  methods: {
    ToogleButton() {
      if (this.status === 'active') {
        this.status = 'pending'
      } else if (this.status === 'pending') {
        this.status = 'inactive'
      } else {
        this.status = 'active'
      }
    },
  },
}
</script>

<template>
  <h1>{{ name }}</h1>
  <br />
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>
  <br />
  <button @click="ToogleButton">PushMe</button>
  <!-- Metodo para recorrer un array de objetos  -->
  <ul>
    <li v-for="task in task" :key="task">
      {{ task }}
    </li>
  </ul>
  <a :href="link" target="_blank">Click to Google</a>
  <br />
</template>
