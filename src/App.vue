<template>
  <div>
    <h1>To-Do List</h1>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Tulis tugas..." />
    <button @click="addTask">Tambah</button>

    <label>
      <input type="checkbox" v-model="showUnfinishedOnly" />
      Tampilkan hanya yang belum selesai
    </label>

    <ul>
      <li v-for="(task, index) in filteredTasks" :key="index">
        <label>
          <input type="checkbox" v-model="task.done" />
          <span>{{ task.text }}</span>
        </label>
        <button @click="removeTask(index)">❌</button>
      </li>
    </ul>

    <p v-if="filteredTasks.length === 0">Tidak ada kegiatan yang ditampilkan ✨</p>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const newTask = ref('')
const tasks = ref([])
const showUnfinishedOnly = ref(false)

const addTask = () => {
  if (newTask.value.trim()) {
    tasks.value.push({ text: newTask.value.trim(), done: false })
    newTask.value = ''
  }
}

const removeTask = (index) => {
  tasks.value.splice(index, 1)
}

const filteredTasks = computed(() =>
  showUnfinishedOnly.value
    ? tasks.value.filter(task => !task.done)
    : tasks.value
)
</script>
