<template>
  <div class="todo-container">
    <h1>📝 To-Do List</h1>

    <div class="input-group">
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Tulis tugasnya di sini..." />
      <button @click="addTask">Tambah</button>
    </div>

    <label class="filter-toggle">
      <input type="checkbox" v-model="showUnfinishedOnly" />
      Tampilkan hanya yang belum selesai
    </label>

    <ul>
      <li v-for="(task, index) in filteredTasks" :key="index" class="task-item" :class="{ done: task.done }">
        <label>
          <input type="checkbox" v-model="task.done" />
          <span>{{ task.text }}</span>
        </label>
        <button @click="removeTask(index)">❌</button>
      </li>
    </ul>

    <p v-if="filteredTasks.length === 0" class="empty">Tidak ada kegiatan yang ditampilkan ✨</p>
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

<style scoped>
.todo-container {
  max-width: 400px;
  margin: 2rem auto;
  background: #fff0f5;
  padding: 2rem;
  border-radius: 20px;
  box-shadow: 0 5px 15px rgba(255, 192, 203, 0.3);
  text-align: center;
  font-family: 'Comic Sans MS', cursive, sans-serif;
}

h1 {
  margin-bottom: 1rem;
  color: #ff69b4;
}

.input-group {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

input[type="text"] {
  flex: 1;
  padding: 0.5rem;
  border: 2px solid #ffc0cb;
  border-radius: 10px;
  font-size: 1rem;
}

button {
  background-color: #ffb6c1;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 10px;
  cursor: pointer;
  font-weight: bold;
  color: white;
  transition: background-color 0.2s;
}

button:hover {
  background-color: #ff69b4;
}

ul {
  list-style: none;
  padding: 0;
}

.task-item {
  background-color: #ffe4e1;
  border-radius: 10px;
  padding: 0.5rem 1rem;
  margin-bottom: 0.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task-item.done span {
  text-decoration: line-through;
  color: #999;
}

.filter-toggle {
  display: block;
  margin-bottom: 1rem;
  color: #d87093;
  font-size: 0.9rem;
}

.empty {
  color: #d87093;
  font-style: italic;
}
</style>
