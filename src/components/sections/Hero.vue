<script setup>
import { gsap } from 'gsap'
import { onBeforeUnmount, onMounted, ref } from 'vue'

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

const birdStyles = Array.from({ length: 14 }, (_, index) => ({
  '--bird-index': index,
  left: `${6 + ((index * 11) % 84)}%`,
  top: `${14 + ((index * 17) % 46)}%`,
  opacity: `${0.24 + (index % 6) * 0.1}`,
  transform: `scale(${0.56 + (index % 5) * 0.12})`,
}))

const dustStyles = Array.from({ length: 24 }, (_, index) => ({
  '--particle-index': index,
  left: `${(index * 17) % 100}%`,
  top: `${56 + ((index * 13) % 42)}%`,
  opacity: `${0.08 + (index % 7) * 0.06}`,
  transform: `scale(${0.42 + (index % 5) * 0.18})`,
}))

let observer = null
let introTimeline = null
const loops = []

const setLoopState = (isActive) => {
  loops.forEach((loop) => {
    if (isActive) {
      loop.play()
      return
    }
    loop.pause()
  })
}

onMounted(() => {
  const root = heroRoot.value
  if (!root) return

  introTimeline = gsap.timeline({ defaults: { ease: 'power3.out' } })
  introTimeline
    .from(root.querySelector('.hero-title'), { y: 42, opacity: 0, duration: 0.9 })
    .from(root.querySelector('.hero-subtitle'), { y: 22, opacity: 0, duration: 0.6 }, '-=0.42')

  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    root.classList.add('reduced-motion')
    return
  }

  const hangingFigures = root.querySelectorAll('.hanging-figure')
  const entities = root.querySelectorAll('.demon-entity')
  const head = root.querySelector('.floating-head')
  const tentacles = root.querySelectorAll('.tentacle')
  const birds = root.querySelectorAll('.bird')
  const fogLayers = root.querySelectorAll('.hero-fog')
  const moon = root.querySelector('.hero-moon')
  const grain = root.querySelector('.hero-grain')
  const flicker = root.querySelector('.hero-flicker')
  const hands = root.querySelectorAll('.horror-hand')
  const spiders = root.querySelectorAll('.spider')

  loops.push(
    gsap.to(hangingFigures, {
      y: () => gsap.utils.random(-10, 12),
      rotation: () => gsap.utils.random(-9, 9),
      duration: () => gsap.utils.random(3.8, 6.4),
      ease: 'sine.inOut',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      stagger: {
        each: 0.35,
        from: 'random',
      },
    }),
  )

  loops.push(
    gsap.to(entities, {
      y: () => gsap.utils.random(-26, 22),
      x: () => gsap.utils.random(-14, 14),
      rotation: () => gsap.utils.random(-4, 4),
      duration: () => gsap.utils.random(5.2, 8.8),
      ease: 'sine.inOut',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      stagger: {
        each: 0.45,
      },
    }),
  )

  loops.push(
    gsap.to(head, {
      y: () => gsap.utils.random(-22, 12),
      x: () => gsap.utils.random(-10, 10),
      rotation: () => gsap.utils.random(-3, 3),
      duration: () => gsap.utils.random(5.6, 9.2),
      ease: 'sine.inOut',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
    }),
  )

  loops.push(
    gsap.to(tentacles, {
      rotation: () => gsap.utils.random(-15, 15),
      x: () => gsap.utils.random(-10, 10),
      scaleY: () => gsap.utils.random(0.86, 1.24),
      duration: () => gsap.utils.random(2.6, 4.8),
      ease: 'sine.inOut',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      stagger: {
        each: 0.12,
      },
    }),
  )

  birds.forEach((bird, index) => {
    loops.push(
      gsap.to(bird, {
        x: () => gsap.utils.random(-220, 220),
        y: () => gsap.utils.random(-90, 90),
        rotation: () => gsap.utils.random(-44, 44),
        duration: () => gsap.utils.random(5.1, 9.4),
        ease: 'sine.inOut',
        repeat: -1,
        yoyo: true,
        repeatRefresh: true,
        delay: index * 0.14,
      }),
    )
  })

  loops.push(
    gsap.to(fogLayers, {
      xPercent: () => gsap.utils.random(-7, 7),
      yPercent: () => gsap.utils.random(-6, 6),
      duration: () => gsap.utils.random(8, 14),
      ease: 'sine.inOut',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      stagger: {
        each: 0.5,
      },
    }),
  )

  loops.push(
    gsap.to(moon, {
      scale: () => gsap.utils.random(0.97, 1.06),
      opacity: () => gsap.utils.random(0.5, 0.82),
      duration: () => gsap.utils.random(4.5, 8.5),
      ease: 'sine.inOut',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
    }),
  )

  loops.push(
    gsap.to(grain, {
      opacity: () => gsap.utils.random(0.22, 0.34),
      duration: () => gsap.utils.random(0.35, 0.72),
      ease: 'steps(4)',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
    }),
  )

  loops.push(
    gsap.to(flicker, {
      opacity: () => gsap.utils.random(0.04, 0.2),
      duration: () => gsap.utils.random(0.2, 0.55),
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      ease: 'steps(2)',
    }),
  )

  loops.push(
    gsap.to(hands, {
      y: () => gsap.utils.random(-10, 8),
      x: () => gsap.utils.random(-8, 8),
      rotation: () => gsap.utils.random(-6, 6),
      duration: () => gsap.utils.random(3.5, 6.8),
      ease: 'sine.inOut',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      stagger: {
        each: 0.24,
      },
    }),
  )

  loops.push(
    gsap.to(spiders, {
      y: () => gsap.utils.random(-20, 18),
      x: () => gsap.utils.random(-18, 18),
      duration: () => gsap.utils.random(5.2, 9.6),
      ease: 'sine.inOut',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      stagger: {
        each: 0.2,
      },
    }),
  )

  observer = new IntersectionObserver(
    (entries) => {
      const [entry] = entries
      if (!entry) return
      setLoopState(entry.isIntersecting)
    },
    {
      threshold: 0.15,
    },
  )

  observer.observe(root)
})

onBeforeUnmount(() => {
  if (observer) {
    observer.disconnect()
    observer = null
  }

  loops.forEach((loop) => loop.kill())
  loops.length = 0

  introTimeline?.kill()
  introTimeline = null
})
</script>

<template>
  <section id="hero" ref="heroRoot" class="hero-abyss section" aria-labelledby="hero-title">
    <div class="hero-nightmare" aria-hidden="true">
      <div class="hero-backdrop" aria-hidden="true"></div>
      <div class="hero-vignette" aria-hidden="true"></div>
      <div class="hero-moon" aria-hidden="true"></div>

      <div class="hero-fog fog-far" aria-hidden="true"></div>
      <div class="hero-fog fog-near" aria-hidden="true"></div>
      <div class="hero-fog fog-ground" aria-hidden="true"></div>

      <div class="hero-ruins" aria-hidden="true">
        <span class="ruin ruin-left"></span>
        <span class="ruin ruin-center"></span>
        <span class="ruin ruin-right"></span>
      </div>

      <div class="hanging-rack" aria-hidden="true">
        <article class="hanging-figure figure-a" aria-hidden="true">
          <span class="rope"></span>
          <span class="body"></span>
          <span class="legs"></span>
        </article>
        <article class="hanging-figure figure-b" aria-hidden="true">
          <span class="rope"></span>
          <span class="body"></span>
          <span class="legs"></span>
        </article>
        <article class="hanging-figure figure-c" aria-hidden="true">
          <span class="rope"></span>
          <span class="body"></span>
          <span class="legs"></span>
        </article>
      </div>

      <div class="demon-cluster" aria-hidden="true">
        <article class="demon-entity demon-a" aria-hidden="true">
          <span class="horn horn-left"></span>
          <span class="horn horn-right"></span>
          <span class="core"></span>
        </article>
        <article class="demon-entity demon-b" aria-hidden="true">
          <span class="horn horn-left"></span>
          <span class="horn horn-right"></span>
          <span class="core"></span>
        </article>
        <article class="demon-entity demon-c" aria-hidden="true">
          <span class="horn horn-left"></span>
          <span class="horn horn-right"></span>
          <span class="core"></span>
        </article>
      </div>

      <article class="floating-head" aria-hidden="true">
        <span class="head-skull"></span>
        <span class="head-eye eye-left"></span>
        <span class="head-eye eye-right"></span>
        <span class="head-mouth"></span>
        <span class="tentacle-wrap">
          <i class="tentacle tentacle-1"></i>
          <i class="tentacle tentacle-2"></i>
          <i class="tentacle tentacle-3"></i>
          <i class="tentacle tentacle-4"></i>
          <i class="tentacle tentacle-5"></i>
        </span>
      </article>

      <div class="bird-flock" aria-hidden="true">
        <span v-for="(style, index) in birdStyles" :key="`bird-${index}`" class="bird" :style="style"></span>
      </div>

      <div class="dust-field" aria-hidden="true">
        <span
          v-for="(style, index) in dustStyles"
          :key="`dust-${index}`"
          class="dust-particle"
          :style="style"
        ></span>
      </div>

      <div class="horror-elements" aria-hidden="true">
        <div class="skeletal-hand horror-hand hand-a">
          <span class="bone palm"></span>
          <span class="bone finger finger-1"><i></i></span>
          <span class="bone finger finger-2"><i></i></span>
          <span class="bone finger finger-3"><i></i></span>
          <span class="bone finger finger-4"><i></i></span>
        </div>
        <div class="skeletal-hand horror-hand hand-b">
          <span class="bone palm"></span>
          <span class="bone finger finger-1"><i></i></span>
          <span class="bone finger finger-2"><i></i></span>
          <span class="bone finger finger-3"><i></i></span>
          <span class="bone finger finger-4"><i></i></span>
        </div>
        <div class="skeletal-hand horror-hand hand-c">
          <span class="bone palm"></span>
          <span class="bone finger finger-1"><i></i></span>
          <span class="bone finger finger-2"><i></i></span>
          <span class="bone finger finger-3"><i></i></span>
          <span class="bone finger finger-4"><i></i></span>
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
      </div>

      <div class="hero-grain" aria-hidden="true"></div>
      <div class="hero-flicker" aria-hidden="true"></div>
    </div>

    <div class="container hero-content">
      <h1 id="hero-title" class="hero-title">{{ name }}</h1>
      <p class="hero-subtitle">Desarrollador de Software Full Stack</p>
    </div>
  </section>
</template>

<style scoped>
.hero-abyss {
  position: relative;
  min-height: min(115vh, 980px);
  padding: 0;
  display: flex;
  align-items: flex-end;
  overflow: hidden;
  isolation: isolate;
  color: #f1f1f1;
}

.hero-abyss::after {
  content: '';
  position: absolute;
  inset: 0;
  z-index: 1;
  pointer-events: none;
  background:
    radial-gradient(circle at 80% 20%, rgba(74, 158, 255, 0.08), transparent 42%),
    linear-gradient(180deg, rgba(9, 16, 30, 0.28), rgba(4, 8, 16, 0.22));
  box-shadow:
    inset 0 -18px 28px rgba(0, 0, 0, 0.28),
    0 0 28px rgba(74, 158, 255, 0.12);
}

.hero-nightmare {
  position: absolute;
  inset: 0;
  z-index: 0;
  pointer-events: none;
  overflow: hidden;
  filter: grayscale(1) contrast(1.16);
}

.hero-backdrop,
.hero-vignette,
.hero-grain,
.hero-flicker {
  position: absolute;
  inset: 0;
}

.hero-backdrop {
  background:
    radial-gradient(circle at 50% 16%, rgba(242, 242, 242, 0.16), transparent 21%),
    radial-gradient(circle at 84% 74%, rgba(220, 220, 220, 0.08), transparent 30%),
    linear-gradient(180deg, rgba(16, 16, 16, 0.64), rgba(1, 1, 1, 0.98)),
    repeating-linear-gradient(
      90deg,
      rgba(4, 4, 4, 0.92) 0 4%,
      rgba(12, 12, 12, 0.9) 4% 8%,
      rgba(8, 8, 8, 0.94) 8% 12%
    );
}

.hero-vignette {
  background:
    radial-gradient(circle at 50% 50%, transparent 14%, rgba(0, 0, 0, 0.72) 76%),
    linear-gradient(180deg, rgba(0, 0, 0, 0.16), rgba(0, 0, 0, 0.6));
}

.hero-moon {
  position: absolute;
  top: 11%;
  left: 50%;
  width: clamp(6.2rem, 12vw, 9.8rem);
  aspect-ratio: 1;
  transform: translateX(-50%);
  border-radius: 999px;
  background:
    radial-gradient(circle at 34% 34%, rgba(255, 255, 255, 0.98), rgba(232, 232, 232, 0.8) 35%, rgba(150, 150, 150, 0.42) 58%, rgba(56, 56, 56, 0.12) 66%, transparent 72%),
    radial-gradient(circle at 60% 56%, rgba(255, 255, 255, 0.2), transparent 52%);
  filter: blur(0.35px) drop-shadow(0 0 22px rgba(255, 255, 255, 0.32));
  opacity: 0.7;
  animation: moonPulse 6.6s infinite ease-in-out;
}

.hero-fog {
  position: absolute;
  left: -16%;
  width: 132%;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(210, 210, 210, 0.2), rgba(85, 85, 85, 0.06) 44%, transparent 70%);
  filter: blur(16px);
  mix-blend-mode: screen;
  animation: fogDrift 13.8s infinite ease-in-out alternate;
}

.fog-far {
  top: 2%;
  height: 36%;
  opacity: 0.26;
}

.fog-near {
  top: 18%;
  height: 44%;
  opacity: 0.32;
  animation-duration: 17.4s;
  animation-direction: alternate-reverse;
}

.fog-ground {
  top: 58%;
  height: 44%;
  opacity: 0.38;
  animation-duration: 12.4s;
}

.hero-ruins {
  position: absolute;
  inset: auto 0 -2% 0;
  height: 68%;
}

.ruin {
  position: absolute;
  bottom: 0;
  width: clamp(4.8rem, 8vw, 8.5rem);
  border-radius: 9px 9px 0 0;
  background:
    linear-gradient(180deg, rgba(192, 192, 192, 0.2), rgba(20, 20, 20, 0.95) 45%),
    repeating-linear-gradient(180deg, rgba(255, 255, 255, 0.08) 0 4px, transparent 4px 11px);
  box-shadow: 0 -12px 36px rgba(255, 255, 255, 0.08), 0 24px 44px rgba(0, 0, 0, 0.65);
}

.ruin-left {
  left: 8%;
  height: 56%;
  transform: skewX(-5deg);
}

.ruin-center {
  left: 48%;
  height: 70%;
  transform: translateX(-50%);
}

.ruin-right {
  right: 7%;
  height: 62%;
  transform: skewX(4deg);
}

.hanging-rack {
  position: absolute;
  inset: 14% 10% auto;
  height: 48%;
}

.hanging-rack::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 6px;
  border-radius: 99px;
  background: linear-gradient(90deg, rgba(40, 40, 40, 0.9), rgba(160, 160, 160, 0.24), rgba(40, 40, 40, 0.9));
  box-shadow: 0 0 0 1px rgba(255, 255, 255, 0.12), 0 0 24px rgba(0, 0, 0, 0.85);
}

.hanging-figure {
  position: absolute;
  top: 0;
  width: clamp(1.8rem, 3.2vw, 2.8rem);
  transform-origin: 50% 0;
  animation: rackSway 5.4s infinite ease-in-out;
}

.figure-a {
  left: 14%;
  animation-duration: 6.2s;
}

.figure-b {
  left: 48%;
  animation-duration: 5.2s;
  animation-delay: -1.8s;
}

.figure-c {
  right: 11%;
  animation-duration: 6.8s;
  animation-delay: -2.7s;
}

.rope {
  display: block;
  width: 2px;
  height: clamp(5rem, 11vw, 8rem);
  margin: 0 auto;
  background: linear-gradient(180deg, rgba(216, 216, 216, 0.66), rgba(22, 22, 22, 0.95));
}

.body {
  position: absolute;
  top: clamp(5rem, 11vw, 8rem);
  left: 50%;
  width: 92%;
  height: clamp(4.4rem, 9vw, 7.2rem);
  transform: translateX(-50%);
  border-radius: 42% 42% 38% 38% / 24% 24% 76% 76%;
  background:
    radial-gradient(circle at 50% 22%, rgba(236, 236, 236, 0.44), transparent 32%),
    linear-gradient(180deg, rgba(232, 232, 232, 0.24), rgba(8, 8, 8, 0.94) 56%);
  box-shadow: inset 0 -18px 20px rgba(0, 0, 0, 0.52), 0 10px 20px rgba(0, 0, 0, 0.64);
}

.legs {
  position: absolute;
  top: calc(clamp(5rem, 11vw, 8rem) + clamp(4.1rem, 8.4vw, 6.7rem));
  left: 50%;
  width: 100%;
  height: clamp(3.2rem, 8vw, 5.4rem);
  transform: translateX(-50%);
}

.legs::before,
.legs::after {
  content: '';
  position: absolute;
  width: 2px;
  height: 100%;
  background: linear-gradient(180deg, rgba(222, 222, 222, 0.48), rgba(16, 16, 16, 0.9));
}

.legs::before {
  left: 35%;
  transform: rotate(4deg);
}

.legs::after {
  right: 35%;
  transform: rotate(-4deg);
}

.demon-cluster {
  position: absolute;
  inset: 22% 5% auto;
  height: 48%;
}

.demon-entity {
  position: absolute;
  width: clamp(4.6rem, 9.8vw, 8.5rem);
  height: clamp(9.6rem, 20vw, 16.5rem);
  border-radius: 50% 50% 42% 42% / 16% 16% 84% 84%;
  background:
    radial-gradient(circle at 50% 38%, rgba(255, 255, 255, 0.2), transparent 35%),
    linear-gradient(180deg, rgba(196, 196, 196, 0.26), rgba(18, 18, 18, 0.96) 54%);
  box-shadow:
    inset 0 -14px 24px rgba(0, 0, 0, 0.72),
    0 18px 28px rgba(0, 0, 0, 0.54),
    0 0 18px rgba(240, 240, 240, 0.1);
  animation: entityBlink 8.2s infinite steps(2, end);
}

.demon-a {
  left: 8%;
  top: 12%;
}

.demon-b {
  left: 46%;
  top: -8%;
}

.demon-c {
  right: 10%;
  top: 9%;
}

.horn {
  position: absolute;
  top: -1.4rem;
  width: clamp(0.9rem, 1.8vw, 1.4rem);
  height: clamp(1.6rem, 3vw, 2.6rem);
  border: 1px solid rgba(240, 240, 240, 0.42);
  border-bottom: none;
  border-radius: 100% 100% 0 0;
  background: linear-gradient(180deg, rgba(212, 212, 212, 0.3), rgba(34, 34, 34, 0.96));
}

.horn-left {
  left: 18%;
  transform: rotate(-26deg);
}

.horn-right {
  right: 18%;
  transform: rotate(26deg);
}

.core {
  position: absolute;
  inset: 35% 28% auto;
  height: 22%;
  border-radius: 999px;
  background: radial-gradient(circle, rgba(238, 238, 238, 0.58), rgba(35, 35, 35, 0.12));
  opacity: 0.35;
}

.floating-head {
  position: absolute;
  left: 50%;
  top: 36%;
  width: clamp(5.5rem, 11vw, 9.2rem);
  transform: translateX(-50%);
  transform-origin: 50% 28%;
  filter: drop-shadow(0 0 22px rgba(255, 255, 255, 0.14)) drop-shadow(0 18px 26px rgba(0, 0, 0, 0.66));
  animation: headHover 7.4s infinite ease-in-out;
}

.head-skull {
  display: block;
  width: 100%;
  aspect-ratio: 0.82;
  border-radius: 44% 44% 40% 40% / 42% 42% 58% 58%;
  background:
    radial-gradient(circle at 30% 32%, rgba(255, 255, 255, 0.76), transparent 30%),
    radial-gradient(circle at 72% 68%, rgba(0, 0, 0, 0.46), transparent 42%),
    linear-gradient(180deg, rgba(218, 218, 218, 0.92), rgba(60, 60, 60, 0.88) 62%, rgba(14, 14, 14, 0.96));
}

.head-eye {
  position: absolute;
  top: 34%;
  width: 16%;
  aspect-ratio: 1;
  border-radius: 999px;
  background: radial-gradient(circle, rgba(244, 244, 244, 0.95), rgba(40, 40, 40, 0.2));
  box-shadow: 0 0 8px rgba(255, 255, 255, 0.45);
}

.eye-left {
  left: 28%;
}

.eye-right {
  right: 28%;
}

.head-mouth {
  position: absolute;
  top: 58%;
  left: 50%;
  width: 30%;
  height: 6%;
  transform: translateX(-50%);
  border-radius: 999px;
  background: rgba(6, 6, 6, 0.88);
}

.tentacle-wrap {
  position: absolute;
  left: 50%;
  top: 92%;
  width: 130%;
  height: clamp(6rem, 12vw, 10rem);
  transform: translateX(-50%);
}

.tentacle {
  position: absolute;
  top: 0;
  width: 2px;
  height: 100%;
  border-radius: 999px;
  background: linear-gradient(180deg, rgba(220, 220, 220, 0.62), rgba(24, 24, 24, 0.94));
  transform-origin: top center;
  animation: tentacleWave 4.6s infinite ease-in-out;
}

.tentacle-1 {
  left: 10%;
  animation-delay: -0.9s;
}

.tentacle-2 {
  left: 28%;
  animation-delay: -1.7s;
}

.tentacle-3 {
  left: 50%;
  animation-delay: -2.5s;
}

.tentacle-4 {
  left: 72%;
  animation-delay: -1.2s;
}

.tentacle-5 {
  left: 90%;
  animation-delay: -2.1s;
}

.bird-flock,
.dust-field {
  position: absolute;
  inset: 0;
}

.bird {
  position: absolute;
  width: 1.4rem;
  height: 0.72rem;
  transform-origin: center;
}

.bird::before,
.bird::after {
  content: '';
  position: absolute;
  top: 0.25rem;
  width: 0.9rem;
  height: 0.44rem;
  border-top: 2px solid rgba(240, 240, 240, 0.8);
  border-radius: 100% 100% 0 0;
  animation: wingBeat 0.34s infinite ease-in-out alternate;
}

.bird::before {
  left: 0;
  transform: rotate(-12deg);
}

.bird::after {
  right: 0;
  transform: rotate(12deg);
  animation-delay: -0.18s;
}

.dust-particle {
  position: absolute;
  width: 3px;
  aspect-ratio: 1;
  border-radius: 999px;
  background: rgba(220, 220, 220, 0.78);
  filter: blur(0.3px);
  animation: dustRise calc(7.5s + var(--particle-index) * 0.3s) infinite linear;
  animation-delay: calc(var(--particle-index) * -0.18s);
}

.hero-grain {
  background:
    repeating-radial-gradient(circle at 26% 64%, rgba(240, 240, 240, 0.14) 0 1px, transparent 1px 3px),
    repeating-linear-gradient(
      72deg,
      rgba(210, 210, 210, 0.08) 0 2px,
      transparent 2px 6px,
      rgba(30, 30, 30, 0.1) 6px 9px
    );
  mix-blend-mode: soft-light;
  opacity: 0.26;
  animation: grainShift 0.82s infinite steps(6, end);
}

.hero-flicker {
  background:
    linear-gradient(180deg, rgba(255, 255, 255, 0.06), transparent 32%, rgba(255, 255, 255, 0.05) 64%, transparent),
    radial-gradient(circle at 50% 38%, rgba(255, 255, 255, 0.1), transparent 44%);
  mix-blend-mode: screen;
  opacity: 0.08;
  animation: flicker 3.6s infinite steps(2, end);
}

.hero-content {
  position: relative;
  z-index: 2;
  margin-left: 8%;
  width: min(60% - 1rem);
  margin-bottom: clamp(5rem, 14vw, 12rem);
  padding: clamp(1.4rem, 3.4vw, 2.2rem);
  border: none;
  background: transparent;
  background-image: none;
  box-shadow: none;
  backdrop-filter: none;
}

.hero-kicker {
  margin: 0;
  color: rgba(230, 230, 230, 0.92);
  text-transform: uppercase;
  letter-spacing: 0.2em;
  font-size: clamp(0.7rem, 1.8vw, 0.88rem);
}

.hero-title {
  margin: 0.4rem 0 0;
  font-family: 'UnifrakturCook', serif;
  font-size: clamp(2.4rem, 8vw, 6.6rem);
  line-height: 0.92;
  color: #fff;
  text-shadow: 0 0 20px rgba(255, 255, 255, 0.2), 0 0 66px rgba(255, 255, 255, 0.12);
}

.hero-subtitle {
  margin: 0.8rem 0 0;
  color: rgba(244, 244, 244, 0.94);
  font-family: 'Creepster', cursive;
  letter-spacing: 0.05em;
  font-size: clamp(1.3rem, 3vw, 2rem);
}

.hero-copy {
  margin: 0.9rem 0 0;
  max-width: 58ch;
  color: rgba(230, 230, 230, 0.88);
  font-size: clamp(0.96rem, 2.2vw, 1.16rem);
}

.hero-manifesto {
  margin: 0.9rem 0 0;
  color: rgba(216, 216, 216, 0.8);
  max-width: 62ch;
  font-size: clamp(0.9rem, 2vw, 1.04rem);
}

.hero-cta {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  margin-top: 1.2rem;
  padding: 0.7rem 1.05rem;
  border-radius: 999px;
  border: 1px solid rgba(255, 255, 255, 0.28);
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.08), rgba(0, 0, 0, 0.44));
  color: #fff;
  transition:
    transform 180ms ease,
    box-shadow 180ms ease,
    border-color 180ms ease;
}

.hero-cta:hover,
.hero-cta:focus-visible {
  transform: translateY(-2px);
  border-color: rgba(255, 255, 255, 0.46);
  box-shadow: 0 0 18px rgba(255, 255, 255, 0.14);
}

@keyframes moonPulse {
  0% {
    opacity: 0.62;
    transform: translateX(-50%) scale(0.97);
  }
  55% {
    opacity: 0.82;
    transform: translateX(-50%) scale(1.03);
  }
  100% {
    opacity: 0.64;
    transform: translateX(-50%) scale(0.98);
  }
}

@keyframes fogDrift {
  from {
    transform: translate(-6%, -2%) scale(0.96);
  }
  to {
    transform: translate(5%, 4%) scale(1.08);
  }
}

@keyframes rackSway {
  0% {
    transform: rotate(-2deg) translateY(0);
  }
  50% {
    transform: rotate(2.2deg) translateY(6px);
  }
  100% {
    transform: rotate(-1.8deg) translateY(0);
  }
}

@keyframes entityBlink {
  0%,
  87%,
  100% {
    opacity: 0.8;
    filter: drop-shadow(0 0 0 rgba(255, 255, 255, 0));
  }
  90% {
    opacity: 0.46;
  }
  94% {
    opacity: 0.92;
    filter: drop-shadow(0 0 12px rgba(255, 255, 255, 0.24));
  }
}

@keyframes headHover {
  0% {
    transform: translateX(-50%) translateY(0);
  }
  50% {
    transform: translateX(-50%) translateY(-12px);
  }
  100% {
    transform: translateX(-50%) translateY(0);
  }
}

@keyframes tentacleWave {
  0% {
    transform: rotate(0deg) scaleY(0.92);
  }
  35% {
    transform: rotate(8deg) scaleY(1.05);
  }
  70% {
    transform: rotate(-9deg) scaleY(1.18);
  }
  100% {
    transform: rotate(0deg) scaleY(1);
  }
}

@keyframes wingBeat {
  from {
    transform: translateY(0) rotate(-8deg);
  }
  to {
    transform: translateY(-2px) rotate(-18deg);
  }
}

@keyframes dustRise {
  0% {
    transform: translateY(12px) scale(0.4);
    opacity: 0;
  }
  28% {
    opacity: 0.44;
  }
  100% {
    transform: translateY(-120px) scale(1);
    opacity: 0;
  }
}

@keyframes grainShift {
  0% {
    transform: translate(0, 0);
  }
  25% {
    transform: translate(-1.5px, 1px);
  }
  50% {
    transform: translate(1px, -1.2px);
  }
  100% {
    transform: translate(0.6px, 0.8px);
  }
}

@keyframes flicker {
  0%,
  84%,
  100% {
    opacity: 0.06;
  }
  86% {
    opacity: 0.22;
  }
  90% {
    opacity: 0.04;
  }
  94% {
    opacity: 0.14;
  }
}

@media (max-width: 900px) {
  .hero-abyss {
    min-height: 94vh;
  }

  .figure-c,
  .demon-c,
  .hand-c {
    display: none;
  }

  .hero-content {
    margin-bottom: 1.5rem;
  }

  .hero-moon {
    top: 8%;
  }
}

@media (max-width: 640px) {
  .hero-abyss {
    min-height: 86vh;
  }

  .demon-b {
    left: 58%;
    top: 4%;
    transform: scale(0.76);
  }

  .floating-head {
    top: 44%;
    width: 5.2rem;
  }

  .bird:nth-child(n + 9),
  .dust-particle:nth-child(n + 16),
  .spider-c {
    display: none;
  }

  .hero-content {
    width: calc(100% - 1.25rem);
    padding: 1.05rem;
  }
}

@media (prefers-reduced-motion: reduce) {
  .hero-abyss * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}

.reduced-motion .bird,
.reduced-motion .dust-particle,
.reduced-motion .tentacle,
.reduced-motion .hanging-figure,
.reduced-motion .demon-entity,
.reduced-motion .hero-fog,
.reduced-motion .hero-moon,
.reduced-motion .hero-grain,
.reduced-motion .hero-flicker,
.reduced-motion .floating-head,
.reduced-motion .horror-hand,
.reduced-motion .spider {
  animation: none;
}
</style>
