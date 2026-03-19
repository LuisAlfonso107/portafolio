<script setup>
import ProjectCard from '../ui/ProjectCard.vue'

defineProps({
  projects: {
    type: Array,
    default: () => [],
  },
})
</script>

<template>
  <section id="projects" class="section section-panel">
    <div class="container">
      <div class="section-heading">
        <p class="eyebrow">Archivo oscuro</p>
        <h2>Proyectos resucitados</h2>
        <p>
          Cuatro trabajos reales donde producto, narrativa visual y ejecucion tecnica comparten la misma tumba.
        </p>
      </div>
      <div class="projects-grid">
        <ProjectCard v-for="project in projects" :key="project.title" :project="project" />
      </div>
    </div>
  </section>
</template>
