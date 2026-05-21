<template>
  <div class="page">


   

    <!-- HERO -->
    <section class="hero" id="home">

      <div class="hero-left">

        <p class="subtitle">Solo Leveling</p>

        <h2>Verwandle dein Leben in ein episches Abenteuer</h2>

        <p class="description">
          Hör auf, mit Motivation und Durchhaltevermögen zu kämpfen.
          Unser bewährtes System verwandelt langweilige Gewohnheiten in spannende Herausforderungen und macht persönliches Wachstum sichtbar und unvermeidlich.
          <br><br>
          Der ultimative „Solo Leveling“-Habit-Tracker, der deine persönliche Entwicklung in ein RPG-Abenteuer verwandelt.
          Sammle XP und steige anhand deiner realen Erfolge vom F-Rang bis zum S-Rang auf.
        </p>

       <SpecialBanner />

        

      </div>

      <div class="hero-right">
        <img :src="flame" alt="Flamme">
      </div>

    </section>

   

    <!-- FEATURES -->
    <section class="features" id="features">

  <div class="card">
    <h3>Freunde</h3>
    <p>
      Du kannst dich mit deinen Freunden connecten und dich mit ihnen messen.
      Werde der beste und sei im Ranking immer ganz oben.
    </p>
  </div>

  <div class="card">
    <h3>Tasks</h3>
    <p>
      Tasks sind wie deine Währung. Du erstellst deine eigenen Tasks mit zugehörigen Zeiten um sie zu schaffen.
      Wenn du deinen Task abschließt bekommst du XP und steigst im Level auf.
      Wenn du es jedoch nicht schaffst verlierst du XP und möglicherweise auch ein Level.
    </p>
  </div>

  <div class="card">
    <h3>Level</h3>
    <p>
      Level zeigen deinen Fortschritt. Für die ersten 2 Ranks musst du jeweils 5 Level aufsteigen und für alle weiteren bis S 10 Level pro Rank.
      Wenn du Rank S erreichst bist du Teil der besten 5%.
    </p>
  </div>

</section>

<TaskFilter @filter="applyFilter" />

<section class="tasks">
  <TaskCard
    v-for="task in filteredTasks"
    :key="task.id"
    :task="task"
  />
  

  <p v-if="filteredTasks.length === 0">
    Keine Tasks vorhanden
  </p>
</section>

 <!-- CTA optional -->
        <button class="cta" @click="$router.push('/tasks')">
          Zu deinen Tasks
        </button>

        

    <Footer />

  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'

import Navbar from '../components/Navbar.vue'
import Footer from '../components/Footer.vue'
import SpecialBanner from '../components/SpecialBanner.vue'
import TaskCard from '../components/TaskCard.vue'
import TaskFilter from '../components/TaskFilter.vue'

import flame from '../assets/img/Flame.jpeg'

const tasks = ref([])

const filters = ref({
  search: '',
  type: ''
})

const filteredTasks = computed(() => {
  return tasks.value.filter(task => {

    const matchSearch =
      task.name?.toLowerCase().includes(filters.value.search.toLowerCase())

    const matchType =
      !filters.value.type || task.type === filters.value.type

    return matchSearch && matchType
  })
})

function applyFilter(newFilters) {
  filters.value = newFilters
}

const loadTasks = async () => {
  try {
    const res = await fetch('http://127.0.0.1:3000/tasks')
    const data = await res.json()

    tasks.value = Array.isArray(data) ? data : (data.tasks || [])
  } catch (err) {
    console.error(err)
  }
}

onMounted(() => {
  loadTasks()
})
</script>

<style scoped>
.page {
  width: 100%;
  min-height: 100vh;
  color: white;
}

/* HERO */
.hero {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 40px;
  padding: 80px 6vw;
  flex-wrap: wrap;
}

.hero-left {
  flex: 1;
  min-width: 280px;
}

.hero-right {
  flex: 1;
  display: flex;
  justify-content: center;
}

.hero-right img {
  width: 100%;
  max-width: 350px;
  filter: drop-shadow(0 0 30px #9333ea);
  border-radius: 0 0 50% 50%;
}

/* FEATURES */
.features {
  display: flex;
  gap: 20px;
  padding: 40px 80px;
}

.card {
  flex: 1;
  padding: 20px;
  border-radius: 12px;
  background: rgba(0,0,0,0.15);
}

/* BUTTON */
.cta {
  margin-top: 20px;
  padding: 10px 16px;
  border: none;
  border-radius: 10px;
  background: #11001C;
  color: white;
  cursor: pointer;
}

/* MOBILE */
@media (max-width: 768px) {
  .hero {
    flex-direction: column;
    text-align: center;
  }

  .features {
    flex-direction: column;
    padding: 20px;
  }
}
</style>