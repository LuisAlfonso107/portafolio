<script setup>
import { gsap } from 'gsap'
import { onMounted, ref } from 'vue'

defineProps({
  name: {
    type: String,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
  summary: {
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
    <div class="horror-elements" aria-hidden="true">
      <div class="skeletal-hand horror-hand hand-a">
        <span class="bone palm"></span>
        <span class="bone finger finger-1"></span>
        <span class="bone finger finger-2"></span>
        <span class="bone finger finger-3"></span>
        <span class="bone finger finger-4"></span>
      </div>
      <div class="skeletal-hand horror-hand hand-b">
        <span class="bone palm"></span>
        <span class="bone finger finger-1"></span>
        <span class="bone finger finger-2"></span>
        <span class="bone finger finger-3"></span>
        <span class="bone finger finger-4"></span>
      </div>
      <div class="skeletal-hand horror-hand hand-c">
        <span class="bone palm"></span>
        <span class="bone finger finger-1"></span>
        <span class="bone finger finger-2"></span>
        <span class="bone finger finger-3"></span>
        <span class="bone finger finger-4"></span>
      </div>
      <div class="spider spider-a">
        <span class="spider-body"></span>
        <span class="spider-leg leg-1"></span>
        <span class="spider-leg leg-2"></span>
        <span class="spider-leg leg-3"></span>
        <span class="spider-leg leg-4"></span>
      </div>
      <div class="spider spider-b">
        <span class="spider-body"></span>
        <span class="spider-leg leg-1"></span>
        <span class="spider-leg leg-2"></span>
        <span class="spider-leg leg-3"></span>
        <span class="spider-leg leg-4"></span>
      </div>
      <div class="spider spider-c">
        <span class="spider-body"></span>
        <span class="spider-leg leg-1"></span>
        <span class="spider-leg leg-2"></span>
        <span class="spider-leg leg-3"></span>
        <span class="spider-leg leg-4"></span>
      </div>
      <div class="horror-grain"></div>
      <div class="horror-haze"></div>
      <div class="horror-embers">
        <span class="horror-ember ember-1"></span>
        <span class="horror-ember ember-2"></span>
        <span class="horror-ember ember-3"></span>
        <span class="horror-ember ember-4"></span>
      </div>
    </div>
    <div class="container hero-content">
      <h1 class="hero-title">{{ name }}</h1>
      <p class="hero-subtitle">{{ title }}</p>
      <p class="hero-copy">{{ summary }}</p>
    </div>
  </section>
</template>
