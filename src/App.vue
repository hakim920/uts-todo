<template>
  <div>
    <h1>To-Do List</h1>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Tulis tugas..." />
    <button @click="addTask">Tambah</button>

    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <label>
          <input type="checkbox" v-model="task.done" />
          <span>{{ task.text }}</span>
        </label>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const newTask = ref('')
const tasks = ref([])

const addTask = () => {
  if (newTask.value.trim()) {
    tasks.value.push({ text: newTask.value.trim(), done: false })
    newTask.value = ''
  }
}
</script>
