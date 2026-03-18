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
      </div>
    </div>
  </section>
</template>
