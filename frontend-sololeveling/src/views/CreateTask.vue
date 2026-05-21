<template>
  <div class="form">

    <h1>Neuer Task</h1>

    <!-- NAME -->
    <input v-model="name" placeholder="Task Name" />

    <!-- DESCRIPTION -->
    <textarea v-model="description" placeholder="Beschreibung"></textarea>

    <!-- TYPE -->
    <div class="type-select">
      <label>
        <input type="radio" value="once" v-model="type" />
        Einmalig
      </label>

      <label>
        <input type="radio" value="repeat" v-model="type" />
        Mehrfach
      </label>
    </div>

    <!-- EINMALIG -->
    <div v-if="type === 'once'">
      <input v-model="deadline" placeholder="Zeitlimit (z.B. 2h / 3 Tage)" />
    </div>

    <!-- MEHRFACH -->
    <div v-if="type === 'repeat'">
      <input v-model="interval" placeholder="Wiederholung (z.B. täglich / 3 Tage)" />
    </div>

    <button @click="createTask">
      Task erstellen
    </button>

  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const name = ref('')
const description = ref('')
const type = ref('once')

const deadline = ref('')
const interval = ref('')

async function createTask() {
  const payload = {
    name: name.value,
    description: description.value,
    type: type.value,
    deadline: type.value === 'once' ? deadline.value : null,
    interval: type.value === 'repeat' ? interval.value : null
  }

  try {
    await fetch('http://127.0.0.1:3000/tasks', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(payload)
    })

    alert('Task erstellt')
    router.push('/tasks')
    
  } catch (err) {
  console.error('CREATE TASK FEHLER:', err)

  alert(
    'Fehler beim Erstellen\n\n' +
    (err?.message || 'Unbekannter Fehler')
  )
  }
}
</script>

<style scoped>
.form {
  padding: 40px;
  color: white;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

input, textarea {
  padding: 10px;
  border-radius: 8px;
  border: none;
}

.type-select {
  display: flex;
  gap: 20px;
}
</style>