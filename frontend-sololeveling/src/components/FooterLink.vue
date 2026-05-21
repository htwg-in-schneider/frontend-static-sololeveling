<template>
  <a class="footer-link" :href="href">
    <slot />
  </a>
</template>

<script setup>
defineProps({
  href: {
    type: String,
    default: '#'
  }
})
</script>

<style scoped>
.footer-link {
  color: white;
  opacity: 0.8;
  text-decoration: none;
  font-size: 14px;
  transition: 0.2s;
}

.footer-link:hover {
  opacity: 1;
  text-decoration: underline;
}
</style>