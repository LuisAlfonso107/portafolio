<script setup>
defineProps({
  items: {
    type: Array,
    default: () => [],
  },
})
</script>

<template>
  <section id="skills" class="section section-panel">
    <div class="container">
      <div class="section-heading">
        <p class="eyebrow">Poderes invocados</p>
        <h2>Stack de combate</h2>
      </div>
      <div class="skills-grid">
        <article v-for="item in items" :key="item.name" class="skill-card">
          <span class="skill-icon">{{ item.icon }}</span>
          <h3>{{ item.name }}</h3>
        </article>
      </div>
    </div>
  </section>
</template>
