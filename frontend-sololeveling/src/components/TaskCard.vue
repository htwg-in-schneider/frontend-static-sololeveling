<template>
  <div class="card">

    <h3>{{ task.name }}</h3>
    <p>{{ task.description }}</p>

    <p v-if="task.type">Typ: {{ task.type }}</p>
    <p v-if="task.deadline">Deadline: {{ task.deadline }}</p>
    <p v-if="task.interval_field">Intervall: {{ task.interval_field }}</p>

    <div class="actions">

      <button @click="goToEdit(task.id)">
        Bearbeiten
      </button>

      <button class="delete" @click="deleteTask(task.id)">
        Löschen
      </button>

    </div>

  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'

const props = defineProps({
  task: Object
})

const emit = defineEmits(['deleted'])

const router = useRouter()

function goToEdit(id) {
  router.push(`/task/edit/${id}`)
}

async function deleteTask(id) {
  try {
    const res = await fetch(`http://127.0.0.1:3000/tasks/${id}`, {
      method: 'DELETE'
    })

    if (!res.ok) throw new Error('Delete failed')

    // 👉 sag Parent: Task wurde gelöscht
    emit('deleted', id)

  } catch (err) {
    console.error(err)
    alert('Task konnte nicht gelöscht werden')
  }
}
</script>

<style scoped>
.card {
  padding: 16px;
  border-radius: 12px;
  background: rgba(0, 0, 0, 0.2);
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.actions {
  margin-top: 10px;
  display: flex;
  gap: 10px;
}

button {
  padding: 8px 12px;
  border-radius: 8px;
  border: none;
  cursor: pointer;
  background: #500D87;
  color: white;
}

.delete {
  background: #b00020;
}
</style>