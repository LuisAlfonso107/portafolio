<script setup>
import { gsap } from 'gsap'
import { onMounted, ref } from 'vue'

defineProps({
  name: {
    type: String,
    required: true,
  },
})

const heroRoot = ref(null)

onMounted(() => {
  const root = heroRoot.value
  if (!root) return

  const timeline = gsap.timeline({ defaults: { ease: 'power3.out' } })
  timeline
    .from(root.querySelector('.hero-kicker'), { y: 24, opacity: 0, duration: 0.7 })
    .from(root.querySelector('.hero-title'), { y: 42, opacity: 0, duration: 0.9 }, '-=0.3')
    .from(root.querySelector('.hero-copy'), { y: 24, opacity: 0, duration: 0.7 }, '-=0.45')
    .from(root.querySelector('.hero-actions'), { y: 24, opacity: 0, duration: 0.6 }, '-=0.35')
    .from(root.querySelectorAll('.fog-layer'), { opacity: 0, duration: 1 }, '-=0.7')
})
</script>

<template>
  <section id="hero" ref="heroRoot" class="hero-section section">
    <div class="hero-backdrop"></div>
    <div class="fog-layer fog-layer-one"></div>
    <div class="fog-layer fog-layer-two"></div>
    <div class="container hero-content">
      <p class="hero-kicker">Bosque maldito. Niebla azul. Frontend de alto impacto.</p>
      <h1 class="hero-title">{{ name }}</h1>
      <p class="hero-copy">
        Portafolio experimental en Vue 3 con una presencia oscura, escalable y lista para convertir curiosidad en entrevistas.
      </p>
      <div class="hero-actions">
        <a class="button-primary" href="#projects">ENTRA SI TE ATREVES</a>
        <a class="button-secondary" href="#contact">Invocar contacto</a>
      </div>
    </div>
  </section>
</template>
