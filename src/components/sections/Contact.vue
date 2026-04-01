<script setup>
import { gsap } from 'gsap'
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'

const props = defineProps({
  socialLinks: {
    type: Array,
    default: () => [],
  },
})

const contactRoot = ref(null)

const ravenStyles = Array.from({ length: 12 }, (_, index) => ({
  '--raven-index': index,
  left: `${5 + ((index * 9) % 86)}%`,
  top: `${8 + ((index * 13) % 62)}%`,
  opacity: `${0.2 + (index % 5) * 0.11}`,
  transform: `scale(${0.52 + (index % 6) * 0.11})`,
}))

const contactLinks = computed(() =>
  props.socialLinks.map((link, index) => ({
    ...link,
    id: `${link.label}-${index}`,
    glyph: getGlyph(link.label),
    detail: formatDetail(link),
  })),
)

let observer = null
let introTimeline = null
const loops = []

function getGlyph(label = '') {
  const normalized = label.toLowerCase()
  if (normalized.includes('github')) return 'GH'
  if (normalized.includes('linkedin')) return 'IN'
  if (normalized.includes('discord')) return 'DS'
  if (normalized.includes('mail') || normalized.includes('email')) return '@'
  if (normalized.includes('whatsapp')) return 'WA'
  if (normalized.includes('x') || normalized.includes('twitter')) return 'X'
  return '##'
}

function formatDetail(link) {
  if (link.text) return link.text
  return String(link.href).replace(/^https?:\/\//, '').replace(/\/$/, '')
}

function setLoopState(isActive) {
  loops.forEach((loop) => {
    if (isActive) {
      loop.play()
      return
    }
    loop.pause()
  })
}

onMounted(() => {
  const root = contactRoot.value
  if (!root) return

  introTimeline = gsap.timeline({ defaults: { ease: 'power3.out' } })
  introTimeline
    .from(root.querySelector('.contact-kicker'), { y: 18, opacity: 0, duration: 0.55 })
    .from(root.querySelector('.contact-title'), { y: 40, opacity: 0, duration: 0.86 }, '-=0.32')
    .from(root.querySelector('.contact-summary'), { y: 20, opacity: 0, duration: 0.68 }, '-=0.42')
    .from(root.querySelectorAll('.contact-link'), { y: 24, opacity: 0, duration: 0.55, stagger: 0.08 }, '-=0.36')

  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    root.classList.add('reduced-motion')
    return
  }

  const ravens = root.querySelectorAll('.raven')
  const tentacles = root.querySelectorAll('.contact-tentacle')
  const chains = root.querySelectorAll('.chain-ghost')
  const fogLayers = root.querySelectorAll('.contact-fog')
  const halo = root.querySelector('.contact-halo')
  const distortion = root.querySelector('.contact-distortion')
  const grain = root.querySelector('.contact-grain')
  const links = root.querySelectorAll('.contact-link')

  loops.push(
    gsap.to(tentacles, {
      rotation: () => gsap.utils.random(-18, 18),
      x: () => gsap.utils.random(-14, 14),
      scaleY: () => gsap.utils.random(0.84, 1.26),
      duration: () => gsap.utils.random(2.7, 4.9),
      ease: 'sine.inOut',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      stagger: {
        each: 0.14,
      },
    }),
  )

  loops.push(
    gsap.to(chains, {
      y: () => gsap.utils.random(-24, 24),
      x: () => gsap.utils.random(-8, 8),
      duration: () => gsap.utils.random(4.8, 8.4),
      ease: 'sine.inOut',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      stagger: {
        each: 0.28,
      },
    }),
  )

  loops.push(
    gsap.to(fogLayers, {
      xPercent: () => gsap.utils.random(-8, 8),
      yPercent: () => gsap.utils.random(-8, 8),
      duration: () => gsap.utils.random(8.5, 14.2),
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
    gsap.to(halo, {
      scale: () => gsap.utils.random(0.94, 1.07),
      opacity: () => gsap.utils.random(0.36, 0.74),
      duration: () => gsap.utils.random(4.6, 8.8),
      ease: 'sine.inOut',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
    }),
  )

  loops.push(
    gsap.to(distortion, {
      opacity: () => gsap.utils.random(0.05, 0.2),
      duration: () => gsap.utils.random(0.2, 0.6),
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      ease: 'steps(2)',
    }),
  )

  loops.push(
    gsap.to(grain, {
      opacity: () => gsap.utils.random(0.2, 0.35),
      duration: () => gsap.utils.random(0.35, 0.82),
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      ease: 'steps(5)',
    }),
  )

  loops.push(
    gsap.to(links, {
      y: () => gsap.utils.random(-4, 4),
      duration: () => gsap.utils.random(2.7, 4.1),
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      ease: 'sine.inOut',
      stagger: {
        each: 0.1,
      },
    }),
  )

  ravens.forEach((raven, index) => {
    loops.push(
      gsap.to(raven, {
        x: () => gsap.utils.random(-260, 260),
        y: () => gsap.utils.random(-120, 120),
        rotation: () => gsap.utils.random(-40, 40),
        duration: () => gsap.utils.random(5.2, 9.6),
        ease: 'sine.inOut',
        repeat: -1,
        yoyo: true,
        repeatRefresh: true,
        delay: index * 0.12,
      }),
    )
  })

  observer = new IntersectionObserver(
    (entries) => {
      const [entry] = entries
      if (!entry) return
      setLoopState(entry.isIntersecting)
    },
    {
      threshold: 0.18,
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
  <section id="contact" ref="contactRoot" class="contact-ritual section" aria-labelledby="contact-title">
    <div class="contact-nightmare" aria-hidden="true">
      <div class="contact-backdrop" aria-hidden="true"></div>
      <div class="contact-vignette" aria-hidden="true"></div>
      <div class="contact-halo" aria-hidden="true"></div>

      <div class="contact-fog fog-alpha" aria-hidden="true"></div>
      <div class="contact-fog fog-beta" aria-hidden="true"></div>
      <div class="contact-fog fog-gamma" aria-hidden="true"></div>

      <div class="chain-field" aria-hidden="true">
        <span class="chain-ghost ghost-a"></span>
        <span class="chain-ghost ghost-b"></span>
        <span class="chain-ghost ghost-c"></span>
      </div>

      <div class="contact-tentacles" aria-hidden="true">
        <span class="contact-tentacle tentacle-a"></span>
        <span class="contact-tentacle tentacle-b"></span>
        <span class="contact-tentacle tentacle-c"></span>
        <span class="contact-tentacle tentacle-d"></span>
        <span class="contact-tentacle tentacle-e"></span>
      </div>

      <div class="raven-flock" aria-hidden="true">
        <span v-for="(style, index) in ravenStyles" :key="`raven-${index}`" class="raven" :style="style"></span>
      </div>

      <div class="contact-grain" aria-hidden="true"></div>
      <div class="contact-distortion" aria-hidden="true"></div>
    </div>

    <div class="container contact-shell">
      <p class="contact-kicker">Ritual De Contacto</p>
      <h2 id="contact-title" class="contact-title">Abre El Portal</h2>
      <p class="contact-summary">
        Sin formulario. Solo puertas directas para hablar conmigo en redes y canales activos.
      </p>

      <ul class="contact-links">
        <li v-for="link in contactLinks" :key="link.id">
          <a class="contact-link" :href="link.href" target="_blank" rel="noreferrer">
            <span class="contact-glyph">{{ link.glyph }}</span>
            <span class="contact-meta">
              <span class="contact-label">{{ link.label }}</span>
              <span class="contact-detail">{{ link.detail }}</span>
            </span>
            <span class="contact-arrow" aria-hidden="true">-&gt;</span>
          </a>
        </li>
      </ul>
    </div>
  </section>
</template>

<style scoped>
.contact-ritual {
  position: relative;
  min-height: min(100vh, 900px);
  padding: 0;
  overflow: hidden;
  isolation: isolate;
  border-top: 1px solid rgba(255, 255, 255, 0.08);
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
}

.contact-nightmare {
  position: absolute;
  inset: 0;
  pointer-events: none;
  overflow: hidden;
  filter: grayscale(1) contrast(1.14);
}

.contact-backdrop,
.contact-vignette,
.contact-grain,
.contact-distortion {
  position: absolute;
  inset: 0;
}

.contact-backdrop {
  background:
    radial-gradient(circle at 50% 14%, rgba(242, 242, 242, 0.14), transparent 18%),
    radial-gradient(circle at 20% 82%, rgba(208, 208, 208, 0.08), transparent 30%),
    linear-gradient(180deg, rgba(12, 12, 12, 0.64), rgba(2, 2, 2, 0.96)),
    repeating-linear-gradient(
      90deg,
      rgba(6, 6, 6, 0.95) 0 4%,
      rgba(12, 12, 12, 0.92) 4% 8%,
      rgba(8, 8, 8, 0.96) 8% 12%
    );
}

.contact-vignette {
  background:
    radial-gradient(circle at 50% 44%, transparent 12%, rgba(0, 0, 0, 0.75) 76%),
    linear-gradient(180deg, rgba(0, 0, 0, 0.16), rgba(0, 0, 0, 0.66));
}

.contact-halo {
  position: absolute;
  top: 12%;
  left: 50%;
  width: clamp(8rem, 16vw, 12rem);
  aspect-ratio: 1;
  transform: translateX(-50%);
  border-radius: 999px;
  background:
    radial-gradient(circle at 50% 44%, rgba(255, 255, 255, 0.8), rgba(188, 188, 188, 0.45) 45%, rgba(60, 60, 60, 0.1) 66%, transparent 70%),
    radial-gradient(circle at 28% 32%, rgba(255, 255, 255, 0.4), transparent 40%);
  opacity: 0.58;
  filter: blur(0.3px) drop-shadow(0 0 24px rgba(255, 255, 255, 0.22));
  animation: haloPulse 6.6s infinite ease-in-out;
}

.contact-fog {
  position: absolute;
  left: -18%;
  width: 136%;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(220, 220, 220, 0.18), rgba(70, 70, 70, 0.08) 44%, transparent 70%);
  filter: blur(16px);
  mix-blend-mode: screen;
  animation: fogGlide 12.8s infinite ease-in-out alternate;
}

.fog-alpha {
  top: 4%;
  height: 36%;
  opacity: 0.22;
}

.fog-beta {
  top: 24%;
  height: 40%;
  opacity: 0.3;
  animation-duration: 16.4s;
  animation-direction: alternate-reverse;
}

.fog-gamma {
  top: 62%;
  height: 40%;
  opacity: 0.36;
  animation-duration: 10.6s;
}

.chain-field {
  position: absolute;
  inset: 10% 0 auto;
  height: 56%;
}

.chain-ghost {
  position: absolute;
  width: 2px;
  height: 100%;
  background:
    repeating-linear-gradient(
      180deg,
      rgba(228, 228, 228, 0.72) 0 8px,
      rgba(18, 18, 18, 0.95) 8px 16px
    );
  box-shadow: 0 0 16px rgba(255, 255, 255, 0.14);
  animation: chainSway 5.8s infinite ease-in-out;
}

.ghost-a {
  left: 10%;
  animation-duration: 6.4s;
}

.ghost-b {
  left: 50%;
  animation-duration: 5.2s;
  animation-delay: -1.5s;
}

.ghost-c {
  right: 12%;
  animation-duration: 6.8s;
  animation-delay: -2.1s;
}

.contact-tentacles {
  position: absolute;
  inset: auto 0 -2% 0;
  height: 42%;
}

.contact-tentacle {
  position: absolute;
  bottom: 0;
  width: clamp(2px, 0.22vw, 4px);
  height: clamp(7rem, 22vw, 16rem);
  border-radius: 999px 999px 0 0;
  transform-origin: bottom center;
  background: linear-gradient(180deg, rgba(235, 235, 235, 0.56), rgba(18, 18, 18, 0.96));
  animation: tentacleCurl 4.6s infinite ease-in-out;
}

.tentacle-a {
  left: 16%;
  animation-delay: -1.4s;
}

.tentacle-b {
  left: 33%;
  animation-delay: -2.1s;
}

.tentacle-c {
  left: 50%;
  animation-delay: -0.9s;
}

.tentacle-d {
  left: 68%;
  animation-delay: -2.6s;
}

.tentacle-e {
  left: 84%;
  animation-delay: -1.8s;
}

.raven-flock {
  position: absolute;
  inset: 0;
}

.raven {
  position: absolute;
  width: 1.5rem;
  height: 0.8rem;
  transform-origin: center;
}

.raven::before,
.raven::after {
  content: '';
  position: absolute;
  top: 0.22rem;
  width: 0.94rem;
  height: 0.48rem;
  border-top: 2px solid rgba(238, 238, 238, 0.86);
  border-radius: 100% 100% 0 0;
  animation: wingFlap 0.32s infinite ease-in-out alternate;
}

.raven::before {
  left: 0;
  transform: rotate(-14deg);
}

.raven::after {
  right: 0;
  transform: rotate(14deg);
  animation-delay: -0.14s;
}

.contact-grain {
  background:
    repeating-radial-gradient(circle at 24% 62%, rgba(240, 240, 240, 0.14) 0 1px, transparent 1px 3px),
    repeating-linear-gradient(
      75deg,
      rgba(215, 215, 215, 0.08) 0 2px,
      transparent 2px 6px,
      rgba(30, 30, 30, 0.11) 6px 9px
    );
  mix-blend-mode: soft-light;
  opacity: 0.26;
  animation: grainJitter 0.84s infinite steps(6, end);
}

.contact-distortion {
  background:
    linear-gradient(180deg, rgba(255, 255, 255, 0.06), transparent 34%, rgba(255, 255, 255, 0.05) 66%, transparent),
    radial-gradient(circle at 50% 46%, rgba(255, 255, 255, 0.1), transparent 44%);
  mix-blend-mode: screen;
  opacity: 0.08;
  animation: distortionBlink 3.8s infinite steps(2, end);
}

.contact-shell {
  position: relative;
  z-index: 2;
  padding-top: clamp(5rem, 12vw, 8rem);
  padding-bottom: clamp(4rem, 10vw, 7rem);
}

.contact-kicker {
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 0.24em;
  color: rgba(232, 232, 232, 0.88);
  font-size: clamp(0.68rem, 1.8vw, 0.88rem);
}

.contact-title {
  margin: 0.5rem 0 0;
  font-family: 'UnifrakturCook', serif;
  font-size: clamp(2.2rem, 8vw, 5.8rem);
  line-height: 0.94;
  color: #fff;
  text-shadow: 0 0 20px rgba(255, 255, 255, 0.2), 0 0 70px rgba(255, 255, 255, 0.12);
}

.contact-summary {
  margin: 1rem 0 0;
  max-width: 56ch;
  color: rgba(232, 232, 232, 0.85);
  font-size: clamp(0.96rem, 2.2vw, 1.16rem);
}

.contact-links {
  list-style: none;
  margin: 1.8rem 0 0;
  padding: 0;
  display: grid;
  gap: 0.9rem;
  max-width: min(760px, 100%);
}

.contact-link {
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  gap: 0.95rem;
  padding: clamp(0.9rem, 2.6vw, 1.2rem);
  border: 1px solid rgba(255, 255, 255, 0.18);
  border-radius: 14px;
  background: linear-gradient(180deg, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.8));
  box-shadow: 0 14px 24px rgba(0, 0, 0, 0.42), inset 0 0 0 1px rgba(255, 255, 255, 0.05);
  transition:
    transform 180ms ease,
    border-color 180ms ease,
    box-shadow 180ms ease,
    background-color 180ms ease;
}

.contact-link:hover,
.contact-link:focus-visible {
  transform: translateY(-3px);
  border-color: rgba(255, 255, 255, 0.42);
  box-shadow: 0 18px 30px rgba(0, 0, 0, 0.5), 0 0 24px rgba(255, 255, 255, 0.12);
  background: linear-gradient(180deg, rgba(12, 12, 12, 0.64), rgba(0, 0, 0, 0.86));
}

.contact-glyph {
  width: 2.5rem;
  aspect-ratio: 1;
  border-radius: 999px;
  display: grid;
  place-items: center;
  border: 1px solid rgba(255, 255, 255, 0.24);
  background: radial-gradient(circle at 30% 28%, rgba(255, 255, 255, 0.3), rgba(32, 32, 32, 0.92));
  color: #f3f3f3;
  font-weight: 700;
  letter-spacing: 0.05em;
  font-size: 0.84rem;
}

.contact-meta {
  min-width: 0;
  display: grid;
}

.contact-label {
  color: #fff;
  font-weight: 700;
}

.contact-detail {
  color: rgba(228, 228, 228, 0.8);
  font-size: 0.92rem;
  overflow: hidden;
  text-overflow: ellipsis;
}

.contact-arrow {
  color: rgba(240, 240, 240, 0.72);
  font-size: 0.88rem;
  letter-spacing: 0.1em;
}

@keyframes haloPulse {
  0% {
    opacity: 0.54;
    transform: translateX(-50%) scale(0.95);
  }
  50% {
    opacity: 0.74;
    transform: translateX(-50%) scale(1.04);
  }
  100% {
    opacity: 0.56;
    transform: translateX(-50%) scale(0.97);
  }
}

@keyframes fogGlide {
  from {
    transform: translate(-6%, -3%) scale(0.96);
  }
  to {
    transform: translate(5%, 4%) scale(1.08);
  }
}

@keyframes chainSway {
  0% {
    transform: rotate(-1.8deg) translateY(0);
  }
  50% {
    transform: rotate(2deg) translateY(6px);
  }
  100% {
    transform: rotate(-1.4deg) translateY(0);
  }
}

@keyframes tentacleCurl {
  0% {
    transform: rotate(-3deg) scaleY(0.9);
  }
  40% {
    transform: rotate(7deg) scaleY(1.08);
  }
  80% {
    transform: rotate(-8deg) scaleY(1.2);
  }
  100% {
    transform: rotate(-2deg) scaleY(0.96);
  }
}

@keyframes wingFlap {
  from {
    transform: translateY(0) rotate(-8deg);
  }
  to {
    transform: translateY(-2px) rotate(-18deg);
  }
}

@keyframes grainJitter {
  0% {
    transform: translate(0, 0);
  }
  30% {
    transform: translate(-1.4px, 1px);
  }
  60% {
    transform: translate(1px, -1.2px);
  }
  100% {
    transform: translate(0.7px, 0.8px);
  }
}

@keyframes distortionBlink {
  0%,
  82%,
  100% {
    opacity: 0.07;
  }
  86% {
    opacity: 0.22;
  }
  91% {
    opacity: 0.04;
  }
  95% {
    opacity: 0.16;
  }
}

@media (max-width: 860px) {
  .contact-ritual {
    min-height: 88vh;
  }

  .ghost-c,
  .tentacle-e {
    display: none;
  }
}

@media (max-width: 640px) {
  .contact-ritual {
    min-height: 78vh;
  }

  .contact-shell {
    padding-top: 4.4rem;
    padding-bottom: 3.4rem;
  }

  .contact-title {
    line-height: 0.98;
  }

  .contact-link {
    grid-template-columns: auto 1fr;
    gap: 0.8rem;
  }

  .contact-arrow {
    display: none;
  }

  .raven:nth-child(n + 9) {
    display: none;
  }
}

@media (prefers-reduced-motion: reduce) {
  .contact-ritual * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}

.reduced-motion .contact-fog,
.reduced-motion .contact-halo,
.reduced-motion .chain-ghost,
.reduced-motion .contact-tentacle,
.reduced-motion .raven,
.reduced-motion .contact-grain,
.reduced-motion .contact-distortion,
.reduced-motion .contact-link {
  animation: none;
}
</style>
