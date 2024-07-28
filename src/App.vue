<script setup>
import { onMounted, ref } from "vue";

const name = ref("Antonio");
const status = ref("active");
const tasks = ref(["eijd", "jijief", "jijecj"]);

const newTask = ref("");

const changeStatus = () => {
  status.value = !status.value;
};

const addTask = () => {
  if (newTask.value.trim() !== "") tasks.value.push(newTask.value);
};

const clear = () => {
  tasks.value = [];
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await response.json();
    tasks.value = data.map((t) => t.title);
  } catch (error) {
    console.log("error fetching tasks.");
  }
});
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status">User is active.</p>
  <p v-else>User is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="task" name="task" v-model="newTask" />
    <button type="submit">Add</button>
    <button type="button" @click="clear">Clear</button>
  </form>

  <h3>
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        {{ task }}
        <button @click="deleteTask(index)">Delete</button>
      </li>
    </ul>
  </h3>

  <button @click="changeStatus">Change Status</button>
</template>

<style scoped></style>
