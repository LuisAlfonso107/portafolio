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
        <h2>Stack</h2>
        <p>Vue, Python, Flask, JavaScript, HTML, CSS, Postman, SQLite, Git, GitHub, etc.</p>
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
