<script setup>
import { ref, onMounted } from 'vue';

const name = ref('John Doe');
const status = ref('active');
const tasks = ref([
  'Task 1',
  'Task 2',
  'Task 3',
  'Task 4',
])
const newTask = ref('');

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'inactive'
  } else {
    status.value = 'active'
  }
}

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
    newTask.value = '';
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
}

onMounted(async () => {
  try {
    const response = await fetch('http://jsonplaceholder.typicode.com/todos')
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.log('Error fetching tasks');
  }
})

</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is <b>active</b></p>
  <p v-else-if="status === 'pending'">User is <b>pending</b></p>
  <p v-else>User is <b>inactive</b></p>
  <button @click="toggleStatus">Change Status</button>


  <h2>Tasks:</h2>
  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Add</button>
  </form>

  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">X</button>
    </li>
  </ul>

</template>

<style scoped>
h1 {
  color: rgb(166, 244, 78)
}

b {
  font-weight: 800;
}

span {
  margin-inline-end: 5px;
}

input {
  margin-inline-start: 10px;
  margin-inline-end: 10px;
}
</style>