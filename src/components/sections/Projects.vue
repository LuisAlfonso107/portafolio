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
          Productos y experiencias donde el detalle visual convive con arquitectura clara y tiempos de carga disciplinados.
        </p>
      </div>
      <div class="projects-grid">
        <ProjectCard v-for="project in projects" :key="project.title" :project="project" />
      </div>
    </div>
  </section>
</template>
