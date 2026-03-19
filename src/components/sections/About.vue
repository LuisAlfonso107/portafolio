<script setup>
defineProps({
  name: {
    type: String,
    required: true,
  },
  role: {
    type: String,
    required: true,
  },
  bio: {
    type: String,
    required: true,
  },
  imageUrl: {
    type: String,
    required: true,
  },
  links: {
    type: Array,
    default: () => [],
  },
})
</script>

<template>
  <section id="about" class="section">
    <div class="container about-grid">
      <div class="about-media">
        <img :src="imageUrl" :alt="name" loading="lazy" />
      </div>
      <div class="about-copy">
        <p class="eyebrow">Mi historia maldita</p>
        <h2>{{ name }}</h2>
        <p class="about-role">{{ role }}</p>
        <p>{{ bio }}</p>
        <div class="social-links about-links">
          <a v-for="link in links" :key="link.label" :href="link.href" target="_blank" rel="noreferrer">
            {{ link.label }}<span v-if="link.text">: {{ link.text }}</span>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>
