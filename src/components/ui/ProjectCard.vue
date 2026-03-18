<script setup>
defineProps({
  project: {
    type: Object,
    required: true,
  },
})
</script>

<template>
  <article class="project-card">
    <div class="project-image-wrap">
      <img :src="project.image" :alt="project.title" class="project-image" loading="lazy" />
    </div>
    <div class="project-body">
      <h3>{{ project.title }}</h3>
      <p>{{ project.description }}</p>
      <div class="project-actions">
        <a :href="project.demoUrl" target="_blank" rel="noreferrer">Ver demo</a>
        <a :href="project.githubUrl" target="_blank" rel="noreferrer">GitHub</a>
      </div>
    </div>
  </article>
</template>
