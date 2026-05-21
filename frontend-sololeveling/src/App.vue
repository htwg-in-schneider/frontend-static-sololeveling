<template>
  <div class="app">
    <Navbar />

    <router-view />

    <Footer />
  </div>
</template>

<script setup>
import Navbar from './components/Navbar.vue'
import Footer from './components/Footer.vue'
</script>

<style>
.app {
  min-height: 100vh;
  width: 100%;
  background: linear-gradient(180deg, #500D87 0%, #2C064B 100%);
  color: white;
}

html, body {
  margin: 0;
  padding: 0;
  width: 100%;
  min-height: 100vh;
}

#app {
  width: 100%;
  min-height: 100vh;
}
</style>