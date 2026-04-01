<script setup>
import { onBeforeUnmount, onMounted, ref, watch } from 'vue'

const props = defineProps({
  items: {
    type: Array,
    default: () => [],
  },
})

const navRoot = ref(null)
const menuOpen = ref(false)
const compact = ref(false)
const hidden = ref(false)

let ticking = false
let lastScrollY = 0

const applyReveal = () => {
  const root = navRoot.value
  if (!root) return

  const y = window.scrollY || window.pageYOffset || 0
  const reveal = Math.min(1, y / 520)
  const revealTwo = Math.min(1, Math.max(0, (y - 180) / 420))
  const parallax = y * 0.14
  const corruption = Math.min(1, Math.max(0, (y - 70) / 360))

  compact.value = y > 46

  if (menuOpen.value) {
    hidden.value = false
  } else {
    const delta = y - lastScrollY
    if (y > 92 && delta > 3) {
      hidden.value = true
    } else if (delta < -3 || y < 24) {
      hidden.value = false
    }
  }

  lastScrollY = y

  root.style.setProperty('--reveal', reveal.toFixed(3))
  root.style.setProperty('--reveal-two', revealTwo.toFixed(3))
  root.style.setProperty('--parallax', parallax.toFixed(2))
  root.style.setProperty('--corruption', corruption.toFixed(3))
}

const onScroll = () => {
  if (ticking) return
  ticking = true
  window.requestAnimationFrame(() => {
    applyReveal()
    ticking = false
  })
}

const onResize = () => {
  if (window.innerWidth > 900 && menuOpen.value) {
    menuOpen.value = false
  }
}

const onKeydown = (event) => {
  if (event.key === 'Escape' && menuOpen.value) {
    menuOpen.value = false
  }
}

const closeMenu = () => {
  menuOpen.value = false
}

const toggleMenu = () => {
  menuOpen.value = !menuOpen.value
}

watch(menuOpen, (open) => {
  document.body.style.overflow = open ? 'hidden' : ''
  if (open) {
    hidden.value = false
  }
})

onMounted(() => {
  lastScrollY = window.scrollY || window.pageYOffset || 0
  applyReveal()
  window.addEventListener('scroll', onScroll, { passive: true })
  window.addEventListener('resize', onResize, { passive: true })
  window.addEventListener('keydown', onKeydown)
})

onBeforeUnmount(() => {
  document.body.style.overflow = ''
  window.removeEventListener('scroll', onScroll)
  window.removeEventListener('resize', onResize)
  window.removeEventListener('keydown', onKeydown)
})
</script>

<template>
  <header
    ref="navRoot"
    class="super-nav"
    :class="{ 'is-compact': compact, 'menu-open': menuOpen, 'is-hidden': hidden }"
  >
    <div class="super-nav-cinematic" aria-hidden="true">
      <div class="old-photo photo-a" aria-hidden="true"></div>
      <div class="old-photo photo-b" aria-hidden="true"></div>
      <div class="cinema-vignette" aria-hidden="true"></div>
      <div class="cinema-grain" aria-hidden="true"></div>
      <div class="cinema-distortion" aria-hidden="true"></div>
    </div>

    <nav class="super-nav-bar container" aria-label="Navegacion principal">
      <a class="super-brand" href="#hero" aria-label="Ir al inicio del portafolio">
        <span class="brand-main">OBSIDIAN</span>
        <span class="brand-sub">CHRONICLE</span>
      </a>

      <div class="super-links" aria-label="Enlaces principales">
        <a
          v-for="item in props.items"
          :key="item.href"
          class="super-link"
          :href="item.href"
        >
          {{ item.label }}
        </a>
      </div>

      <button
        class="super-menu-btn"
        type="button"
        aria-label="Abrir menu de navegacion"
        :aria-expanded="menuOpen ? 'true' : 'false'"
        aria-controls="super-mobile-menu"
        @click="toggleMenu"
      >
        <span class="menu-bar"></span>
        <span class="menu-bar"></span>
        <span class="menu-bar"></span>
      </button>
    </nav>

    <div
      id="super-mobile-menu"
      class="super-mobile-menu"
      :class="{ open: menuOpen }"
      :aria-hidden="menuOpen ? 'false' : 'true'"
      @click.self="closeMenu"
    >
      <div class="mobile-panel">
        <p class="mobile-kicker">Umbral De Navegacion</p>
        <a
          v-for="item in props.items"
          :key="`${item.href}-mobile`"
          class="mobile-link"
          :href="item.href"
          @click="closeMenu"
        >
          {{ item.label }}
        </a>
      </div>
    </div>
  </header>
</template>

<style scoped>
.super-nav {
  --reveal: 0;
  --reveal-two: 0;
  --parallax: 0;
  --corruption: 0;
  position: sticky;
  top: 0;
  z-index: 60;
  isolation: isolate;
  transition:
    transform 300ms cubic-bezier(0.22, 1, 0.36, 1),
    opacity 200ms ease;
}

.super-nav.is-hidden {
  transform: translateY(calc(-100% - 1.2rem));
  opacity: 0;
  pointer-events: none;
}

.super-nav-cinematic {
  display: none;
}

.old-photo,
.cinema-vignette,
.cinema-grain,
.cinema-distortion {
  position: absolute;
  inset: 0;
}

.old-photo {
  transform-origin: center;
}

.photo-a {
  background:
    radial-gradient(circle at 52% 31%, rgba(238, 224, 194, 0.32) 0 12%, transparent 30%),
    radial-gradient(circle at 46% 34%, rgba(0, 0, 0, 0.64) 0 1.7%, transparent 4.6%),
    radial-gradient(circle at 58% 34%, rgba(0, 0, 0, 0.64) 0 1.7%, transparent 4.6%),
    radial-gradient(circle at 52% 46%, rgba(0, 0, 0, 0.34) 0 2.8%, transparent 5.8%),
    radial-gradient(circle at 50% 58%, rgba(22, 16, 10, 0.44) 0 10%, transparent 24%),
    linear-gradient(180deg, rgba(32, 22, 12, 0.48), rgba(8, 6, 4, 0.76)),
    repeating-linear-gradient(84deg, rgba(255, 243, 220, 0.08) 0 2px, transparent 2px 6px);
  opacity: calc(0.22 + (var(--reveal) * 0.54));
  transform: translateY(calc(var(--parallax) * -0.25px)) scale(calc(1 + (var(--reveal) * 0.06)));
}

.photo-b {
  background:
    radial-gradient(circle at 20% 54%, rgba(220, 210, 190, 0.2) 0 10%, transparent 26%),
    radial-gradient(circle at 34% 56%, rgba(0, 0, 0, 0.62) 0 2.2%, transparent 5.5%),
    radial-gradient(circle at 44% 56%, rgba(0, 0, 0, 0.62) 0 2.2%, transparent 5.5%),
    radial-gradient(circle at 76% 54%, rgba(220, 210, 190, 0.2) 0 10%, transparent 26%),
    radial-gradient(circle at 69% 55%, rgba(0, 0, 0, 0.62) 0 2.2%, transparent 5.5%),
    radial-gradient(circle at 81% 55%, rgba(0, 0, 0, 0.62) 0 2.2%, transparent 5.5%),
    linear-gradient(180deg, rgba(20, 14, 8, 0.62), rgba(5, 4, 3, 0.84));
  mix-blend-mode: screen;
  opacity: calc(0.02 + (var(--reveal-two) * 0.7));
  transform: translateY(calc(var(--parallax) * -0.42px)) scale(calc(1 + (var(--reveal-two) * 0.08)));
}

.cinema-vignette {
  background:
    radial-gradient(circle at 50% 50%, transparent 20%, rgba(0, 0, 0, 0.76) 82%),
    linear-gradient(180deg, rgba(0, 0, 0, 0.42), rgba(0, 0, 0, 0.68));
}

.cinema-grain {
  background:
    repeating-radial-gradient(circle at 26% 64%, rgba(255, 244, 222, 0.1) 0 1px, transparent 1px 3px),
    repeating-linear-gradient(72deg, rgba(255, 244, 222, 0.08) 0 2px, transparent 2px 6px);
  mix-blend-mode: soft-light;
  opacity: calc(0.18 + (var(--corruption) * 0.18));
  animation: navNoise 0.9s infinite steps(6, end);
}

.cinema-distortion {
  background:
    linear-gradient(180deg, transparent 0 20%, rgba(255, 255, 255, 0.08) 35%, transparent 52%, rgba(255, 255, 255, 0.08) 74%, transparent),
    radial-gradient(circle at 50% 34%, rgba(255, 255, 255, 0.08), transparent 34%);
  mix-blend-mode: screen;
  opacity: calc(0.06 + (var(--corruption) * 0.22));
  animation: navDistort 3.8s infinite steps(3, end);
}

.super-nav-bar {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  padding: clamp(0.95rem, 2.1vw, 1.25rem) clamp(1rem, 2vw, 1.4rem);
  border: none;
  border-radius: 0;
  margin-top: 0.35rem;
  background: transparent;
  backdrop-filter: none;
  box-shadow: none;
  transition:
    padding 260ms ease,
    transform 260ms ease;
}

.is-compact .super-nav-bar {
  padding-top: 0.66rem;
  padding-bottom: 0.66rem;
}

.super-brand {
  display: grid;
  line-height: 0.9;
  gap: 0.15rem;
}

.brand-main {
  font-family: 'UnifrakturCook', serif;
  letter-spacing: 0.08em;
  font-size: clamp(1.08rem, 2.2vw, 1.34rem);
  color: #f1f3f7;
  text-shadow: 0 0 14px rgba(74, 158, 255, 0.2);
}

.brand-sub {
  font-size: 0.62rem;
  letter-spacing: 0.32em;
  text-transform: uppercase;
  color: rgba(214, 223, 238, 0.72);
}

.super-links {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-end;
  gap: 0.62rem;
}

.super-link {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.48rem 0.82rem;
  border-radius: 999px;
  color: rgba(224, 234, 248, 0.85);
  border: none;
  transition:
    transform 180ms ease,
    color 180ms ease,
    box-shadow 180ms ease,
    background-color 180ms ease;
}

.super-link::before {
  content: '';
  position: absolute;
  inset: auto 22% 16% 22%;
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.58), transparent);
  opacity: 0;
  transition: opacity 180ms ease;
}

.super-link:hover,
.super-link:focus-visible {
  color: #fff;
  transform: translateY(-1px);
  background: transparent;
  box-shadow: 0 0 16px rgba(74, 158, 255, 0.2);
}

.super-link:hover::before,
.super-link:focus-visible::before {
  opacity: 1;
}

.super-menu-btn {
  display: none;
  width: 3rem;
  height: 3rem;
  border-radius: 999px;
  border: none;
  background: transparent;
  box-shadow: none;
  padding: 0.58rem;
  gap: 0.3rem;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.menu-bar {
  width: 100%;
  height: 2px;
  border-radius: 99px;
  background: linear-gradient(90deg, rgba(255, 255, 255, 0.88), rgba(74, 158, 255, 0.62));
}

.super-mobile-menu {
  position: fixed;
  inset: 0;
  z-index: 90;
  pointer-events: none;
  opacity: 0;
  background: rgba(2, 4, 9, 0.62);
  backdrop-filter: blur(5px);
  transition: opacity 220ms ease;
}

.super-mobile-menu.open {
  opacity: 1;
  pointer-events: auto;
}

.mobile-panel {
  position: absolute;
  inset: 0;
  margin-left: auto;
  width: min(28rem, 92vw);
  padding: 5.4rem 1rem 1rem;
  display: grid;
  align-content: start;
  gap: 0.7rem;
  background:
    linear-gradient(180deg, rgba(8, 13, 24, 0.92), rgba(2, 4, 9, 0.96)),
    radial-gradient(circle at 76% 16%, rgba(74, 158, 255, 0.2), transparent 34%);
  border-left: 1px solid rgba(255, 255, 255, 0.14);
  box-shadow: -18px 0 34px rgba(0, 0, 0, 0.48);
  transform: translateX(100%);
  transition: transform 260ms ease;
}

.super-mobile-menu.open .mobile-panel {
  transform: translateX(0);
}

.mobile-kicker {
  margin: 0 0 0.3rem;
  text-transform: uppercase;
  letter-spacing: 0.24em;
  color: rgba(224, 234, 248, 0.7);
  font-size: 0.7rem;
}

.mobile-link {
  display: inline-flex;
  align-items: center;
  min-height: 3.2rem;
  padding: 0.8rem 0.9rem;
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.16);
  color: rgba(234, 241, 252, 0.9);
  background: linear-gradient(180deg, rgba(11, 19, 33, 0.64), rgba(3, 6, 12, 0.82));
  transition:
    transform 170ms ease,
    border-color 170ms ease,
    box-shadow 170ms ease;
}

.mobile-link:hover,
.mobile-link:focus-visible {
  transform: translateX(3px);
  border-color: rgba(255, 255, 255, 0.32);
  box-shadow:
    0 0 0 1px rgba(74, 158, 255, 0.26),
    0 0 18px rgba(74, 158, 255, 0.2);
}

@keyframes navNoise {
  0% {
    transform: translate(0, 0);
  }
  25% {
    transform: translate(-1.2px, 0.8px);
  }
  50% {
    transform: translate(1px, -1px);
  }
  100% {
    transform: translate(0.5px, 0.6px);
  }
}

@keyframes navDistort {
  0%,
  84%,
  100% {
    opacity: 0.05;
  }
  88% {
    opacity: 0.16;
  }
  94% {
    opacity: 0.08;
  }
}

@media (max-width: 900px) {
  .super-links {
    display: none;
  }

  .super-menu-btn {
    display: inline-flex;
  }

  .super-nav-bar {
    margin-top: 0.15rem;
  }
}

@media (prefers-reduced-motion: reduce) {
  .super-nav-cinematic *,
  .super-nav-bar,
  .mobile-panel,
  .super-mobile-menu {
    animation: none !important;
    transition-duration: 0.01ms !important;
  }
}
</style>
