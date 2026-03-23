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
        <h2>Proyectos</h2>
        <p>
          Trabajos realizados recientemente...
        </p>
      </div>
      <div class="projects-grid">
        <ProjectCard v-for="project in projects" :key="project.title" :project="project" />
      </div>
    </div>
  </section>
</template>
