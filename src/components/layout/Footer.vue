<script setup>
defineProps({
  githubUrl: {
    type: String,
    required: true,
  },
})
</script>

<template>
  <footer class="site-footer">
    <div class="container footer-content">
      <p>© 2026 Luis Alfonso Garcia Lagos.</p>
      <div class="footer-links">
        <a :href="githubUrl" target="_blank" rel="noreferrer">GitHub</a>
        <a href="#hero">Volver</a>
      </div>
    </div>
  </footer>
</template>
