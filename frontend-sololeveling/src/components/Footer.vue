<template>
  <footer class="footer">

    <p>© 2026 Solo Leveling Tracker</p>

    <div class="links">
      <FooterLink href="/impressum">Impressum</FooterLink>
      <FooterLink href="/kontakt">Kontakt</FooterLink>
    </div>

  </footer>
</template>

<script setup>
import FooterLink from './FooterLink.vue'
</script>

<style scoped>
.footer {
  text-align: center;
  padding: 30px;
  opacity: 0.7;
}

.links {
  margin-top: 10px;
  display: flex;
  justify-content: center;
  gap: 15px;
}
</style>