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
      <div :class="['project-image', project.imageClass]" :aria-label="project.title" role="img"></div>
    </div>
    <div class="project-body">
      <h3>{{ project.title }}</h3>
      <p>{{ project.description }}</p>
      <div class="project-actions">
        <a :href="project.demoUrl" target="_blank" rel="noreferrer">VER DEMO</a>
        <a v-if="project.githubUrl" :href="project.githubUrl" target="_blank" rel="noreferrer">GITHUB</a>
      </div>
    </div>
  </article>
</template>
