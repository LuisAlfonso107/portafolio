<script setup>
import { gsap } from 'gsap'
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'

const props = defineProps({
  projects: {
    type: Array,
    default: () => [],
  },
})

const projectRoot = ref(null)

const sigilStyles = Array.from({ length: 18 }, (_, index) => ({
  '--sigil-index': index,
  left: `${4 + ((index * 11) % 90)}%`,
  top: `${6 + ((index * 17) % 72)}%`,
  opacity: `${0.12 + (index % 5) * 0.08}`,
  transform: `scale(${0.52 + (index % 4) * 0.22})`,
}))

const ashStyles = Array.from({ length: 30 }, (_, index) => ({
  '--ash-index': index,
  left: `${(index * 13) % 100}%`,
  top: `${58 + ((index * 9) % 42)}%`,
  opacity: `${0.08 + (index % 6) * 0.07}`,
  transform: `scale(${0.38 + (index % 5) * 0.18})`,
}))

const projectItems = computed(() =>
  props.projects.map((project, index) => ({
    ...project,
    id: `${project.title}-${index}`,
    rune: String(project.title)
      .split(' ')
      .slice(0, 2)
      .map((chunk) => chunk[0]?.toUpperCase() || '')
      .join(''),
    tone: `tone-${(index % 4) + 1}`,
    codex: `PROTOCOLO-${String(index + 1).padStart(2, '0')}`,
  })),
)

let observer = null
let introTimeline = null
const loops = []

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
  const root = projectRoot.value
  if (!root) return

  introTimeline = gsap.timeline({ defaults: { ease: 'power3.out' } })
  introTimeline
    .from(root.querySelector('.projects-kicker'), { y: 20, opacity: 0, duration: 0.6 })
    .from(root.querySelector('.projects-title'), { y: 42, opacity: 0, duration: 0.9 }, '-=0.35')
    .from(root.querySelector('.projects-summary'), { y: 24, opacity: 0, duration: 0.7 }, '-=0.42')
    .from(root.querySelectorAll('.ritual-card'), { y: 30, opacity: 0, duration: 0.65, stagger: 0.1 }, '-=0.35')

  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    root.classList.add('reduced-motion')
    return
  }

  const rings = root.querySelectorAll('.orbit-ring')
  const sigils = root.querySelectorAll('.sigil')
  const obelisks = root.querySelectorAll('.obelisk')
  const ashes = root.querySelectorAll('.ash')
  const cards = root.querySelectorAll('.ritual-card')
  const scanline = root.querySelector('.void-scan')
  const noise = root.querySelector('.void-noise')
  const pulse = root.querySelector('.void-pulse')

  rings.forEach((ring, index) => {
    loops.push(
      gsap.to(ring, {
        rotation: index % 2 === 0 ? 360 : -360,
        duration: 20 + index * 3,
        ease: 'none',
        repeat: -1,
      }),
    )
  })

  loops.push(
    gsap.to(obelisks, {
      y: () => gsap.utils.random(-18, 14),
      scaleY: () => gsap.utils.random(0.9, 1.16),
      opacity: () => gsap.utils.random(0.4, 0.86),
      duration: () => gsap.utils.random(4.2, 8.2),
      ease: 'sine.inOut',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      stagger: {
        each: 0.3,
      },
    }),
  )

  loops.push(
    gsap.to(sigils, {
      x: () => gsap.utils.random(-120, 120),
      y: () => gsap.utils.random(-50, 50),
      rotation: () => gsap.utils.random(-65, 65),
      opacity: () => gsap.utils.random(0.06, 0.42),
      duration: () => gsap.utils.random(6.8, 12.6),
      ease: 'sine.inOut',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      stagger: {
        each: 0.08,
        from: 'random',
      },
    }),
  )

  loops.push(
    gsap.to(cards, {
      rotateX: () => gsap.utils.random(-4, 4),
      rotateY: () => gsap.utils.random(-5, 5),
      x: () => gsap.utils.random(-6, 6),
      duration: () => gsap.utils.random(3.8, 6.2),
      ease: 'sine.inOut',
      transformPerspective: 950,
      transformOrigin: 'center center',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
      stagger: {
        each: 0.1,
      },
    }),
  )

  ashes.forEach((ash, index) => {
    loops.push(
      gsap.to(ash, {
        y: () => gsap.utils.random(-180, -70),
        x: () => gsap.utils.random(-26, 26),
        opacity: () => gsap.utils.random(0.02, 0.4),
        duration: () => gsap.utils.random(5.4, 11.4),
        ease: 'none',
        repeat: -1,
        yoyo: false,
        repeatRefresh: true,
        delay: index * 0.08,
      }),
    )
  })

  loops.push(
    gsap.fromTo(
      scanline,
      { yPercent: -120, opacity: 0.05 },
      {
        yPercent: 130,
        opacity: 0.24,
        duration: 3.4,
        ease: 'steps(9)',
        repeat: -1,
        repeatDelay: 0.5,
      },
    ),
  )

  loops.push(
    gsap.to(noise, {
      opacity: () => gsap.utils.random(0.14, 0.34),
      duration: () => gsap.utils.random(0.22, 0.66),
      ease: 'steps(4)',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
    }),
  )

  loops.push(
    gsap.to(pulse, {
      scale: () => gsap.utils.random(0.95, 1.08),
      opacity: () => gsap.utils.random(0.22, 0.62),
      duration: () => gsap.utils.random(4.8, 8.8),
      ease: 'sine.inOut',
      repeat: -1,
      yoyo: true,
      repeatRefresh: true,
    }),
  )

  observer = new IntersectionObserver(
    (entries) => {
      const [entry] = entries
      if (!entry) return
      setLoopState(entry.isIntersecting)
    },
    {
      threshold: 0.16,
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
  <section id="projects" ref="projectRoot" class="projects-void section" aria-labelledby="projects-title">
    <div class="void-scene" aria-hidden="true">
      <div class="void-backdrop" aria-hidden="true"></div>
      <div class="void-vignette" aria-hidden="true"></div>
      <div class="void-pulse" aria-hidden="true"></div>

      <div class="orbits" aria-hidden="true">
        <span class="orbit-ring ring-a"></span>
        <span class="orbit-ring ring-b"></span>
        <span class="orbit-ring ring-c"></span>
      </div>

      <div class="obelisks" aria-hidden="true">
        <span class="obelisk obelisk-a"></span>
        <span class="obelisk obelisk-b"></span>
        <span class="obelisk obelisk-c"></span>
      </div>

      <div class="sigils" aria-hidden="true">
        <span v-for="(style, index) in sigilStyles" :key="`sigil-${index}`" class="sigil" :style="style"></span>
      </div>

      <div class="ash-field" aria-hidden="true">
        <span v-for="(style, index) in ashStyles" :key="`ash-${index}`" class="ash" :style="style"></span>
      </div>

      <div class="void-noise" aria-hidden="true"></div>
      <div class="void-scan" aria-hidden="true"></div>
    </div>

    <div class="container projects-shell">
      <p class="projects-kicker">Catalogo Del Vacio</p>
      <h2 id="projects-title" class="projects-title">Proyectos Invocados</h2>
      <p class="projects-summary">
        Cada artefacto abre una salida real: demostraciones activas y codigo cuando esta disponible.
      </p>

      <ul class="projects-grid-ritual">
        <li v-for="project in projectItems" :key="project.id">
          <article class="ritual-card">
            <div class="ritual-visual" :class="project.tone">
              <span class="visual-grid" aria-hidden="true"></span>
              <span class="visual-core" aria-hidden="true"></span>
              <span class="visual-rune" aria-hidden="true">{{ project.rune }}</span>
              <span class="visual-codex">{{ project.codex }}</span>
            </div>

            <div class="ritual-body">
              <h3>{{ project.title }}</h3>
              <p>{{ project.description }}</p>
              <div class="ritual-actions">
                <a :href="project.demoUrl" target="_blank" rel="noreferrer">VER DEMO</a>
                <a v-if="project.githubUrl" :href="project.githubUrl" target="_blank" rel="noreferrer">GITHUB</a>
              </div>
            </div>
          </article>
        </li>
      </ul>
    </div>
  </section>
</template>

<style scoped>
.projects-void {
  position: relative;
  min-height: min(100vh, 960px);
  padding: 0;
  overflow: hidden;
  isolation: isolate;
  border-top: 1px solid rgba(255, 255, 255, 0.08);
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
}

.void-scene {
  position: absolute;
  inset: 0;
  pointer-events: none;
  overflow: hidden;
  filter: grayscale(1) contrast(1.16);
}

.void-backdrop,
.void-vignette,
.void-noise,
.void-scan {
  position: absolute;
  inset: 0;
}

.void-backdrop {
  background:
    radial-gradient(circle at 50% 12%, rgba(244, 244, 244, 0.14), transparent 18%),
    radial-gradient(circle at 14% 84%, rgba(210, 210, 210, 0.09), transparent 28%),
    linear-gradient(180deg, rgba(12, 12, 12, 0.62), rgba(2, 2, 2, 0.98)),
    repeating-linear-gradient(
      90deg,
      rgba(8, 8, 8, 0.94) 0 4%,
      rgba(14, 14, 14, 0.92) 4% 8%,
      rgba(10, 10, 10, 0.96) 8% 12%
    );
}

.void-vignette {
  background:
    radial-gradient(circle at 50% 48%, transparent 10%, rgba(0, 0, 0, 0.76) 78%),
    linear-gradient(180deg, rgba(0, 0, 0, 0.12), rgba(0, 0, 0, 0.62));
}

.void-pulse {
  position: absolute;
  top: 14%;
  left: 50%;
  width: clamp(9rem, 18vw, 14rem);
  aspect-ratio: 1;
  transform: translateX(-50%);
  border-radius: 999px;
  background:
    radial-gradient(circle at 50% 46%, rgba(255, 255, 255, 0.74), rgba(168, 168, 168, 0.4) 44%, transparent 68%),
    radial-gradient(circle at 26% 30%, rgba(255, 255, 255, 0.28), transparent 40%);
  opacity: 0.46;
  filter: blur(0.4px) drop-shadow(0 0 26px rgba(255, 255, 255, 0.16));
}

.orbits {
  position: absolute;
  top: 2%;
  left: 50%;
  width: min(42rem, 90vw);
  aspect-ratio: 1;
  transform: translateX(-50%);
}

.orbit-ring {
  position: absolute;
  inset: 0;
  border-radius: 999px;
  border: 1px solid rgba(245, 245, 245, 0.14);
}

.ring-a {
  transform: scale(1);
}

.ring-b {
  transform: scale(0.78);
  border-style: dashed;
}

.ring-c {
  transform: scale(0.56);
  border-color: rgba(245, 245, 245, 0.2);
}

.obelisks {
  position: absolute;
  inset: auto 0 0;
  height: 58%;
}

.obelisk {
  position: absolute;
  bottom: -2%;
  width: clamp(3rem, 7vw, 6rem);
  border-radius: 12px 12px 0 0;
  background:
    linear-gradient(180deg, rgba(230, 230, 230, 0.2), rgba(20, 20, 20, 0.96) 52%),
    repeating-linear-gradient(180deg, rgba(255, 255, 255, 0.09) 0 4px, transparent 4px 11px);
  box-shadow: inset 0 -16px 24px rgba(0, 0, 0, 0.54), 0 16px 30px rgba(0, 0, 0, 0.62);
}

.obelisk-a {
  left: 7%;
  height: 58%;
  transform: skewX(-4deg);
}

.obelisk-b {
  left: 50%;
  height: 72%;
  transform: translateX(-50%);
}

.obelisk-c {
  right: 8%;
  height: 62%;
  transform: skewX(4deg);
}

.sigils,
.ash-field {
  position: absolute;
  inset: 0;
}

.sigil {
  position: absolute;
  width: 1.4rem;
  aspect-ratio: 1;
  border: 1px solid rgba(240, 240, 240, 0.28);
  border-radius: 3px;
  transform-origin: center;
}

.sigil::before,
.sigil::after {
  content: '';
  position: absolute;
  inset: 24%;
  border: 1px solid rgba(240, 240, 240, 0.36);
}

.sigil::after {
  inset: 43%;
  border-radius: 999px;
}

.ash {
  position: absolute;
  width: 3px;
  aspect-ratio: 1;
  border-radius: 999px;
  background: rgba(226, 226, 226, 0.8);
  filter: blur(0.3px);
}

.void-noise {
  background:
    repeating-radial-gradient(circle at 22% 64%, rgba(240, 240, 240, 0.14) 0 1px, transparent 1px 3px),
    repeating-linear-gradient(
      74deg,
      rgba(212, 212, 212, 0.08) 0 2px,
      transparent 2px 6px,
      rgba(30, 30, 30, 0.12) 6px 9px
    );
  mix-blend-mode: soft-light;
  opacity: 0.22;
}

.void-scan {
  background: linear-gradient(
    180deg,
    transparent 0%,
    rgba(245, 245, 245, 0.08) 34%,
    rgba(245, 245, 245, 0.16) 52%,
    rgba(245, 245, 245, 0.08) 70%,
    transparent 100%
  );
  opacity: 0.08;
}

.projects-shell {
  position: relative;
  z-index: 2;
  padding-top: clamp(5rem, 11vw, 7.2rem);
  padding-bottom: clamp(4rem, 10vw, 6.8rem);
}

.projects-kicker {
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 0.24em;
  color: rgba(232, 232, 232, 0.86);
  font-size: clamp(0.68rem, 1.8vw, 0.86rem);
}

.projects-title {
  margin: 0.5rem 0 0;
  font-family: 'UnifrakturCook', serif;
  font-size: clamp(2.3rem, 8vw, 6rem);
  line-height: 0.95;
  color: #fff;
  text-shadow: 0 0 20px rgba(255, 255, 255, 0.2), 0 0 72px rgba(255, 255, 255, 0.1);
}

.projects-summary {
  margin: 1rem 0 0;
  max-width: 60ch;
  color: rgba(232, 232, 232, 0.86);
  font-size: clamp(0.95rem, 2.2vw, 1.16rem);
}

.projects-grid-ritual {
  list-style: none;
  margin: 1.9rem 0 0;
  padding: 0;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
}

.ritual-card {
  position: relative;
  height: 100%;
  border: 1px solid rgba(12, 65, 91, 0.16);
  border-radius: 18px;
  background: linear-gradient(180deg, rgba(3, 3, 3, 0.5), rgba(0, 0, 0, 0.84));
  box-shadow: 0 14px 28px rgba(15, 62, 98, 0.44), inset 0 0 0 1px rgba(255, 255, 255, 0.04);
  overflow: hidden;
  transform-style: preserve-3d;
  transition:
    transform 180ms ease,
    border-color 180ms ease,
    box-shadow 180ms ease;
}

.ritual-card:hover {
  transform: translateY(-5px);
  border-color: rgba(53, 165, 218, 0.36);
  box-shadow: 0 20px 32px rgba(0, 0, 0, 0.56), 0 0 20px rgba(255, 255, 255, 0.1);
}

.ritual-visual {
  position: relative;
  min-height: 148px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.14);
  overflow: hidden;
}

.ritual-visual::before,
.ritual-visual::after {
  content: '';
  position: absolute;
  inset: 0;
}

.ritual-visual::before {
  background:
    radial-gradient(circle at 50% 44%, var(--tone-bright, rgba(240, 240, 240, 0.2)), transparent 44%),
    linear-gradient(180deg, rgba(0, 0, 0, 0.18), rgba(0, 0, 0, 0.78));
}

.ritual-visual::after {
  background:
    repeating-linear-gradient(
      90deg,
      rgba(255, 255, 255, 0.05) 0 4%,
      rgba(0, 0, 0, 0.08) 4% 8%
    );
  opacity: 0.6;
  mix-blend-mode: soft-light;
}

.tone-1 {
  --tone-bright: rgba(244, 244, 244, 0.24);
}

.tone-2 {
  --tone-bright: rgba(214, 214, 214, 0.2);
}

.tone-3 {
  --tone-bright: rgba(228, 228, 228, 0.22);
}

.tone-4 {
  --tone-bright: rgba(202, 202, 202, 0.18);
}

.visual-grid,
.visual-core,
.visual-rune,
.visual-codex {
  position: absolute;
}

.visual-grid {
  inset: 14% 10%;
  border: 1px solid rgba(255, 255, 255, 0.16);
  border-radius: 8px;
  background:
    linear-gradient(90deg, transparent 0 18%, rgba(255, 255, 255, 0.12) 18% 19%, transparent 19% 50%, rgba(255, 255, 255, 0.12) 50% 51%, transparent 51% 82%, rgba(255, 255, 255, 0.12) 82% 83%, transparent 83%),
    linear-gradient(180deg, transparent 0 25%, rgba(255, 255, 255, 0.12) 25% 26%, transparent 26% 74%, rgba(255, 255, 255, 0.12) 74% 75%, transparent 75%);
}

.visual-core {
  left: 50%;
  top: 50%;
  width: 4.4rem;
  aspect-ratio: 1;
  transform: translate(-50%, -50%);
  border-radius: 999px;
  border: 1px solid rgba(255, 255, 255, 0.24);
  background:
    radial-gradient(circle at 50% 45%, rgba(255, 255, 255, 0.84), rgba(104, 104, 104, 0.36) 55%, transparent 70%);
  animation: coreOrbit 4.2s infinite ease-in-out;
}

.visual-rune {
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  font-size: 1.08rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  color: rgba(250, 250, 250, 0.88);
  text-shadow: 0 0 12px rgba(255, 255, 255, 0.24);
  z-index: 1;
}

.visual-codex {
  left: 0.75rem;
  bottom: 0.7rem;
  font-size: 0.66rem;
  letter-spacing: 0.12em;
  color: rgba(232, 232, 232, 0.7);
  text-transform: uppercase;
}

.ritual-body {
  padding: 1rem;
}

.ritual-body h3 {
  margin: 0;
  color: #fff;
}

.ritual-body p {
  margin: 0.75rem 0 0;
  color: rgba(232, 232, 232, 0.84);
}

.ritual-actions {
  margin-top: 1rem;
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
}

.ritual-actions a {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.6rem 0.9rem;
  border-radius: 999px;
  border: 1px solid rgba(255, 255, 255, 0.22);
  color: #fff;
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.08), rgba(0, 0, 0, 0.42));
  transition:
    transform 160ms ease,
    border-color 160ms ease,
    box-shadow 160ms ease;
}

.ritual-actions a:hover,
.ritual-actions a:focus-visible {
  transform: translateY(-2px);
  border-color: rgba(255, 255, 255, 0.42);
  box-shadow: 0 0 16px rgba(255, 255, 255, 0.16);
}

@keyframes coreOrbit {
  0% {
    transform: translate(-50%, -50%) scale(0.92);
    opacity: 0.62;
  }
  45% {
    transform: translate(-50%, -50%) scale(1.08);
    opacity: 0.9;
  }
  100% {
    transform: translate(-50%, -50%) scale(0.95);
    opacity: 0.66;
  }
}

@media (max-width: 900px) {
  .projects-void {
    min-height: 88vh;
  }

  .ring-c,
  .obelisk-c {
    display: none;
  }
}

@media (max-width: 640px) {
  .projects-void {
    min-height: 80vh;
  }

  .projects-shell {
    padding-top: 4.4rem;
    padding-bottom: 3.4rem;
  }

  .sigil:nth-child(n + 13),
  .ash:nth-child(n + 20) {
    display: none;
  }
}

@media (prefers-reduced-motion: reduce) {
  .projects-void * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}

.reduced-motion .orbit-ring,
.reduced-motion .sigil,
.reduced-motion .obelisk,
.reduced-motion .ash,
.reduced-motion .void-noise,
.reduced-motion .void-scan,
.reduced-motion .void-pulse,
.reduced-motion .ritual-card,
.reduced-motion .visual-core {
  animation: none;
}
</style>
