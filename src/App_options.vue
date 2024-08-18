<script>
export default {
  data() {
    return {
      name: 'John Doe',
      status: 'pending',
      tasks: [
        'Task 1',
        'Task 2',
        'Task 3',
        'Task 4',
        'Task 5',
      ],
      link: 'https://www.oceanscurse.com'
    }
  },
  methods: {
    toggleStatus() {
      if (this.status === 'active') {
        this.status = 'inactive'
      } else {
        this.status = 'active'
      }
    }
  }
}
</script>

<template>
  <h1>{{ name }}</h1>
  
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <h3>Tasks</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>

  <a :href="link">View my awesome website!</a>
  
  <br/>

  <button @click="toggleStatus">Change Status</button>
</template>

<style scoped>
h1 {
  color: red
}
</style>
