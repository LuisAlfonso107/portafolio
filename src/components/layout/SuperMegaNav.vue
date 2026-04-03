<script setup>
import { computed, onBeforeUnmount, onMounted, ref, watch } from 'vue'

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
const isReducedMotion = ref(false)
const revealProgress = ref(0)

let ticking = false
let lastScrollY = 0

const photoStyles = computed(() => {
  const progress = revealProgress.value
  const progressTwo = Math.min(1, Math.max(0, (progress - 0.28) / 0.72))
  const progressThree = Math.min(1, Math.max(0, (progress - 0.54) / 0.46))

  return {
    '--scroll-progress': progress.toFixed(3),
    '--scroll-progress-2': progressTwo.toFixed(3),
    '--scroll-progress-3': progressThree.toFixed(3),
    '--veil-opacity': (0.24 + progress * 0.44).toFixed(3),
    '--parallax-shift': `${(progress * 68).toFixed(2)}px`,
    '--grain-opacity': (0.12 + progress * 0.18).toFixed(3),
    '--distortion-opacity': (0.06 + progress * 0.15).toFixed(3),
    '--nav-height': compact.value ? '4.9rem' : '6.8rem',
  }
})

const syncScrollState = () => {
  const y = window.scrollY || window.pageYOffset || 0
  const nextProgress = Math.min(1, y / 720)
  const delta = y - lastScrollY

  revealProgress.value = nextProgress
  compact.value = y > 36

  if (!menuOpen.value) {
    if (y > 160 && delta > 6) {
      hidden.value = true
    } else if (delta < -6 || y < 48) {
      hidden.value = false
    }
  } else {
    hidden.value = false
  }

  lastScrollY = y
}

const onScroll = () => {
  if (ticking) return
  ticking = true
  window.requestAnimationFrame(() => {
    syncScrollState()
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

const toggleMenu = () => {
  menuOpen.value = !menuOpen.value
}

const closeMenu = () => {
  menuOpen.value = false
}

watch(menuOpen, (open) => {
  document.body.style.overflow = open ? 'hidden' : ''
  if (open) {
    hidden.value = false
  }
})

onMounted(() => {
  isReducedMotion.value = window.matchMedia('(prefers-reduced-motion: reduce)').matches
  lastScrollY = window.scrollY || window.pageYOffset || 0
  syncScrollState()
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
    :class="{
      'is-compact': compact,
      'is-hidden': hidden,
      'menu-open': menuOpen,
      'reduced-motion': isReducedMotion,
    }"
    :style="photoStyles"
  >
    <div class="super-nav-backdrop" aria-hidden="true">
      <div class="super-nav-photo photo-primary" aria-hidden="true"></div>
      <div class="super-nav-photo photo-secondary" aria-hidden="true"></div>
      <div class="super-nav-photo photo-tertiary" aria-hidden="true"></div>
      <div class="super-nav-fog fog-one" aria-hidden="true"></div>
      <div class="super-nav-fog fog-two" aria-hidden="true"></div>
      <div class="super-nav-vignette" aria-hidden="true"></div>
      <div class="super-nav-grain" aria-hidden="true"></div>
      <div class="super-nav-distortion" aria-hidden="true"></div>
      <div class="super-nav-scanlines" aria-hidden="true"></div>
    </div>

    <nav class="super-nav-shell container" aria-label="Navegacion principal">
      <a class="super-brand" href="#hero" aria-label="Ir al inicio del portafolio">
        <span class="brand-glyph" aria-hidden="true">XIII</span>
        <span class="brand-copy">
          <span class="brand-title">Obsidian Archive</span>
          <span class="brand-subtitle">Portafolio de Luis Alfonso</span>
        </span>
      </a>

      <div class="super-links">
        <a
          v-for="item in props.items"
          :key="item.href"
          class="super-link"
          :href="item.href"
        >
          <span class="super-link-label">{{ item.label }}</span>
        </a>
      </div>

      <button
        class="super-menu-btn"
        type="button"
        :aria-expanded="menuOpen ? 'true' : 'false'"
        aria-controls="super-mobile-menu"
        :aria-label="menuOpen ? 'Cerrar menu de navegacion' : 'Abrir menu de navegacion'"
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
        <div class="mobile-header">
          <p class="mobile-kicker">Umbral cinematografico</p>
          <p class="mobile-copy">
            Explora las secciones mientras el archivo emerge desde la niebla.
          </p>
        </div>

        <a
          v-for="(item, index) in props.items"
          :key="`${item.href}-mobile`"
          class="mobile-link"
          :href="item.href"
          @click="closeMenu"
        >
          <span class="mobile-link-index" aria-hidden="true">0{{ index + 1 }}</span>
          <span class="mobile-link-label">{{ item.label }}</span>
        </a>
      </div>
    </div>
  </header>
</template>

<style scoped>
.super-nav {
  position: sticky;
  top: 0;
  z-index: 70;
  isolation: isolate;
  min-height: var(--nav-height);
  padding: 0.6rem 0 0;
  transition:
    transform 300ms cubic-bezier(0.22, 1, 0.36, 1),
    min-height 280ms ease,
    opacity 220ms ease;
  will-change: transform;
}

.super-nav.is-hidden {
  transform: translate3d(0, calc(-100% - 1rem), 0);
  opacity: 0;
  pointer-events: none;
}

.super-nav-backdrop {
  position: absolute;
  inset: 0;
  overflow: hidden;
  pointer-events: none;
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
}

.super-nav-photo,
.super-nav-vignette,
.super-nav-grain,
.super-nav-distortion,
.super-nav-scanlines,
.super-nav-fog {
  position: absolute;
  inset: 0;
}

.super-nav-photo {
  transform: translate3d(0, calc(var(--parallax-shift) * -1), 0) scale(1.08);
  transform-origin: center top;
  will-change: transform, opacity, filter;
}

.photo-primary {
  background:
    radial-gradient(circle at 48% 30%, rgba(238, 227, 204, 0.54) 0 8%, transparent 16%),
    radial-gradient(circle at 45% 31%, rgba(7, 6, 4, 0.84) 0 1.7%, transparent 4.6%),
    radial-gradient(circle at 53% 31%, rgba(7, 6, 4, 0.84) 0 1.7%, transparent 4.6%),
    radial-gradient(circle at 49% 40%, rgba(10, 9, 7, 0.42) 0 3%, transparent 7%),
    radial-gradient(circle at 49% 53%, rgba(21, 15, 11, 0.88) 0 12%, transparent 21%),
    radial-gradient(circle at 18% 72%, rgba(255, 239, 214, 0.14) 0 8%, transparent 22%),
    linear-gradient(180deg, rgba(39, 24, 12, 0.16), rgba(4, 4, 4, 0.82)),
    repeating-linear-gradient(90deg, rgba(255, 244, 221, 0.05) 0 2px, transparent 2px 8px);
  opacity: calc(0.14 + var(--scroll-progress) * 0.72);
  filter: grayscale(1) sepia(0.55) contrast(calc(1 + var(--scroll-progress) * 0.3));
}

.photo-secondary {
  background:
    radial-gradient(circle at 22% 50%, rgba(228, 214, 188, 0.18) 0 10%, transparent 24%),
    radial-gradient(circle at 19% 53%, rgba(8, 7, 5, 0.82) 0 1.6%, transparent 4.4%),
    radial-gradient(circle at 25% 53%, rgba(8, 7, 5, 0.82) 0 1.6%, transparent 4.4%),
    radial-gradient(circle at 78% 48%, rgba(228, 214, 188, 0.18) 0 10%, transparent 24%),
    radial-gradient(circle at 75% 51%, rgba(8, 7, 5, 0.82) 0 1.8%, transparent 4.5%),
    radial-gradient(circle at 81% 51%, rgba(8, 7, 5, 0.82) 0 1.8%, transparent 4.5%),
    linear-gradient(180deg, rgba(27, 18, 10, 0.12), rgba(6, 4, 3, 0.88));
  opacity: calc(var(--scroll-progress-2) * 0.62);
  mix-blend-mode: screen;
  transform:
    translate3d(0, calc(var(--parallax-shift) * -1.35), 0)
    scale(calc(1.02 + var(--scroll-progress-2) * 0.06));
}

.photo-tertiary {
  background:
    radial-gradient(circle at 50% 18%, rgba(255, 247, 232, 0.16), transparent 22%),
    radial-gradient(circle at 50% 32%, rgba(255, 243, 220, 0.1), transparent 18%),
    linear-gradient(180deg, rgba(11, 11, 12, 0.06), rgba(2, 2, 2, 0.92));
  opacity: calc(var(--scroll-progress-3) * 0.44);
  mix-blend-mode: overlay;
  transform:
    translate3d(0, calc(var(--parallax-shift) * -1.8), 0)
    scale(calc(1 + var(--scroll-progress-3) * 0.04));
}

.super-nav-fog {
  mix-blend-mode: screen;
  filter: blur(12px);
}

.fog-one {
  background: radial-gradient(circle at 18% 40%, rgba(216, 222, 232, 0.12), transparent 28%);
  opacity: calc(0.12 + var(--scroll-progress) * 0.08);
  transform: translate3d(calc(var(--parallax-shift) * 0.18), 0, 0);
}

.fog-two {
  background: radial-gradient(circle at 82% 52%, rgba(216, 222, 232, 0.1), transparent 32%);
  opacity: calc(0.08 + var(--scroll-progress-2) * 0.14);
  transform: translate3d(calc(var(--parallax-shift) * -0.14), 0, 0);
}

.super-nav-vignette {
  background:
    radial-gradient(circle at 50% 38%, transparent 16%, rgba(0, 0, 0, 0.68) 82%),
    linear-gradient(180deg, rgba(6, 8, 12, 0.2), rgba(1, 1, 1, 0.88));
  opacity: var(--veil-opacity);
}

.super-nav-grain {
  background:
    repeating-linear-gradient(72deg, rgba(255, 250, 241, 0.07) 0 2px, transparent 2px 6px),
    repeating-radial-gradient(circle at 28% 64%, rgba(255, 245, 226, 0.08) 0 1px, transparent 1px 3px);
  opacity: var(--grain-opacity);
  mix-blend-mode: soft-light;
  animation: navGrain 0.9s infinite steps(5, end);
}

.super-nav-distortion {
  background:
    linear-gradient(180deg, transparent 0 18%, rgba(255, 255, 255, 0.08) 34%, transparent 48%, rgba(255, 255, 255, 0.06) 66%, transparent 82%),
    radial-gradient(circle at 52% 34%, rgba(255, 255, 255, 0.08), transparent 28%);
  opacity: var(--distortion-opacity);
  mix-blend-mode: screen;
  animation: navDistort 3.6s infinite steps(3, end);
}

.super-nav-scanlines {
  background:
    repeating-linear-gradient(180deg, rgba(255, 255, 255, 0.04) 0 1px, transparent 1px 4px),
    linear-gradient(180deg, rgba(8, 12, 18, 0.1), transparent 24%, rgba(0, 0, 0, 0.36));
  opacity: 0.16;
}

.super-nav-shell {
  position: relative;
  z-index: 1;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  min-height: calc(var(--nav-height) - 0.6rem);
  padding: 0.85rem 1rem;
  border: 1px solid rgba(255, 248, 232, 0.14);
  border-radius: 28px;
  background:
    linear-gradient(180deg, rgba(9, 11, 16, 0.68), rgba(4, 5, 9, 0.84)),
    radial-gradient(circle at 12% 18%, rgba(150, 160, 181, 0.16), transparent 24%);
  backdrop-filter: blur(22px);
  box-shadow:
    0 20px 44px rgba(0, 0, 0, 0.42),
    0 0 0 1px rgba(255, 255, 255, 0.04),
    0 0 34px rgba(111, 124, 146, 0.12);
  transition:
    min-height 280ms ease,
    padding 280ms ease,
    border-radius 280ms ease,
    background 280ms ease,
    box-shadow 280ms ease;
}

.is-compact .super-nav-shell {
  padding-top: 0.62rem;
  padding-bottom: 0.62rem;
  border-radius: 22px;
  background:
    linear-gradient(180deg, rgba(5, 7, 11, 0.78), rgba(2, 3, 7, 0.9)),
    radial-gradient(circle at 12% 18%, rgba(150, 160, 181, 0.12), transparent 24%);
  box-shadow:
    0 14px 32px rgba(0, 0, 0, 0.46),
    0 0 0 1px rgba(255, 255, 255, 0.04),
    0 0 28px rgba(111, 124, 146, 0.08);
}

.super-brand {
  display: inline-flex;
  align-items: center;
  gap: 0.85rem;
  min-width: 0;
}

.brand-glyph {
  display: grid;
  place-items: center;
  width: 2.8rem;
  height: 2.8rem;
  flex: none;
  border: 1px solid rgba(255, 248, 232, 0.24);
  border-radius: 999px;
  background: radial-gradient(circle at 50% 34%, rgba(231, 223, 207, 0.32), rgba(39, 33, 26, 0.2) 62%, rgba(7, 7, 8, 0.86));
  color: #f4eee2;
  font-family: 'UnifrakturCook', serif;
  font-size: 1rem;
  text-shadow: 0 0 12px rgba(255, 245, 225, 0.2);
  box-shadow: 0 0 22px rgba(244, 238, 226, 0.08);
}

.brand-copy {
  display: grid;
  gap: 0.12rem;
  min-width: 0;
}

.brand-title {
  font-family: 'UnifrakturCook', serif;
  font-size: clamp(1.08rem, 2vw, 1.34rem);
  line-height: 1;
  color: #faf5ea;
  letter-spacing: 0.05em;
}

.brand-subtitle {
  color: rgba(223, 228, 238, 0.72);
  font-size: 0.72rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
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
  min-height: 2.9rem;
  padding: 0.65rem 1rem;
  border: 1px solid rgba(255, 248, 232, 0.08);
  border-radius: 999px;
  color: rgba(233, 238, 246, 0.84);
  background: rgba(255, 255, 255, 0.02);
  text-transform: uppercase;
  letter-spacing: 0.13em;
  font-size: 0.73rem;
  overflow: hidden;
  transition:
    transform 180ms ease,
    color 180ms ease,
    border-color 180ms ease,
    box-shadow 180ms ease,
    background-color 180ms ease;
}

.super-link::before,
.super-link::after {
  content: '';
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.super-link::before {
  background: linear-gradient(90deg, transparent, rgba(255, 248, 232, 0.12), transparent);
  opacity: 0;
  transform: translateX(-100%);
  transition:
    transform 240ms ease,
    opacity 180ms ease;
}

.super-link::after {
  inset: auto 18% 0.55rem;
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(255, 248, 232, 0.72), transparent);
  opacity: 0;
  transition: opacity 180ms ease;
}

.super-link:hover,
.super-link:focus-visible {
  color: #fffdf6;
  border-color: rgba(255, 248, 232, 0.18);
  background: rgba(255, 255, 255, 0.04);
  box-shadow:
    0 0 0 1px rgba(255, 248, 232, 0.08),
    0 0 20px rgba(255, 248, 232, 0.08),
    0 12px 20px rgba(0, 0, 0, 0.24);
  transform: translateY(-1px);
}

.super-link:hover::before,
.super-link:focus-visible::before {
  opacity: 1;
  transform: translateX(100%);
}

.super-link:hover::after,
.super-link:focus-visible::after {
  opacity: 1;
}

.super-link:focus-visible,
.super-menu-btn:focus-visible,
.mobile-link:focus-visible,
.super-brand:focus-visible {
  outline: 2px solid rgba(255, 248, 232, 0.82);
  outline-offset: 2px;
}

.super-menu-btn {
  display: none;
  position: relative;
  width: 3.5rem;
  height: 3.5rem;
  flex: none;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 0.34rem;
  padding: 0.72rem;
  border: 1px solid rgba(255, 248, 232, 0.16);
  border-radius: 999px;
  background:
    radial-gradient(circle at 50% 32%, rgba(241, 232, 213, 0.16), transparent 42%),
    linear-gradient(180deg, rgba(17, 17, 20, 0.84), rgba(4, 4, 6, 0.96));
  box-shadow:
    0 0 0 1px rgba(255, 255, 255, 0.04),
    0 0 18px rgba(255, 248, 232, 0.08);
  transition:
    transform 180ms ease,
    border-color 180ms ease,
    box-shadow 180ms ease;
}

.super-menu-btn:hover,
.super-menu-btn:focus-visible {
  transform: scale(1.02);
  border-color: rgba(255, 248, 232, 0.28);
  box-shadow:
    0 0 0 1px rgba(255, 255, 255, 0.08),
    0 0 24px rgba(255, 248, 232, 0.12);
}

.menu-bar {
  width: 100%;
  height: 2px;
  border-radius: 999px;
  background: linear-gradient(90deg, rgba(255, 248, 232, 0.96), rgba(181, 189, 202, 0.58));
  transform-origin: center;
  transition:
    transform 220ms ease,
    opacity 220ms ease;
}

.menu-open .menu-bar:nth-child(1) {
  transform: translateY(0.36rem) rotate(45deg);
}

.menu-open .menu-bar:nth-child(2) {
  opacity: 0;
}

.menu-open .menu-bar:nth-child(3) {
  transform: translateY(-0.36rem) rotate(-45deg);
}

.super-mobile-menu {
  position: fixed;
  inset: 0;
  z-index: 90;
  pointer-events: none;
  opacity: 0;
  background: rgba(0, 0, 0, 0.74);
  backdrop-filter: blur(8px);
  transition: opacity 220ms ease;
}

.super-mobile-menu.open {
  opacity: 1;
  pointer-events: auto;
}

.mobile-panel {
  position: absolute;
  inset: 0;
  display: grid;
  align-content: start;
  gap: 0.9rem;
  padding: 6.2rem 1.2rem 1.4rem;
  background:
    radial-gradient(circle at 50% 18%, rgba(228, 218, 197, 0.12), transparent 18%),
    linear-gradient(180deg, rgba(12, 12, 14, 0.94), rgba(3, 3, 5, 0.98)),
    repeating-linear-gradient(180deg, rgba(255, 255, 255, 0.03) 0 1px, transparent 1px 4px);
  transform: translate3d(0, -3%, 0) scale(1.02);
  transition: transform 260ms cubic-bezier(0.22, 1, 0.36, 1);
}

.super-mobile-menu.open .mobile-panel {
  transform: translate3d(0, 0, 0) scale(1);
}

.mobile-panel::before,
.mobile-panel::after {
  content: '';
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.mobile-panel::before {
  background:
    radial-gradient(circle at 50% 32%, rgba(234, 225, 208, 0.12), transparent 22%),
    radial-gradient(circle at 46% 33%, rgba(7, 6, 4, 0.76) 0 1.4%, transparent 4.6%),
    radial-gradient(circle at 54% 33%, rgba(7, 6, 4, 0.76) 0 1.4%, transparent 4.6%),
    radial-gradient(circle at 50% 44%, rgba(7, 6, 4, 0.4) 0 2.8%, transparent 7%),
    linear-gradient(180deg, transparent 0 16%, rgba(0, 0, 0, 0.44) 48%, rgba(0, 0, 0, 0.8));
  opacity: 0.2;
  mix-blend-mode: screen;
}

.mobile-panel::after {
  background: radial-gradient(circle at 50% 38%, transparent 18%, rgba(0, 0, 0, 0.74) 86%);
}

.mobile-header,
.mobile-link {
  position: relative;
  z-index: 1;
}

.mobile-header {
  margin-bottom: 0.65rem;
}

.mobile-kicker {
  margin: 0;
  color: rgba(233, 238, 246, 0.66);
  font-size: 0.74rem;
  letter-spacing: 0.28em;
  text-transform: uppercase;
}

.mobile-copy {
  max-width: 32ch;
  margin: 0.7rem 0 0;
  color: rgba(233, 238, 246, 0.82);
  font-size: 0.98rem;
  line-height: 1.55;
}

.mobile-link {
  display: grid;
  grid-template-columns: auto 1fr;
  align-items: center;
  gap: 1rem;
  min-height: 4.2rem;
  padding: 1rem 1rem 1rem 1.1rem;
  border: 1px solid rgba(255, 248, 232, 0.14);
  border-radius: 18px;
  background:
    linear-gradient(180deg, rgba(18, 19, 23, 0.72), rgba(5, 5, 7, 0.94)),
    radial-gradient(circle at 12% 50%, rgba(255, 248, 232, 0.08), transparent 24%);
  color: #f5f1e8;
  box-shadow:
    0 16px 28px rgba(0, 0, 0, 0.28),
    inset 0 0 0 1px rgba(255, 255, 255, 0.02);
  transition:
    transform 180ms ease,
    border-color 180ms ease,
    box-shadow 180ms ease,
    background-color 180ms ease;
}

.mobile-link:hover,
.mobile-link:focus-visible {
  transform: translateX(4px);
  border-color: rgba(255, 248, 232, 0.28);
  box-shadow:
    0 18px 30px rgba(0, 0, 0, 0.32),
    0 0 22px rgba(255, 248, 232, 0.08);
}

.mobile-link-index {
  font-family: 'UnifrakturCook', serif;
  font-size: 1.3rem;
  color: rgba(255, 248, 232, 0.7);
}

.mobile-link-label {
  text-transform: uppercase;
  letter-spacing: 0.16em;
  font-size: 0.82rem;
}

@keyframes navGrain {
  0% { transform: translate(0, 0); }
  25% { transform: translate(-1.4px, 1px); }
  50% { transform: translate(1px, -1px); }
  100% { transform: translate(0.6px, 0.8px); }
}

@keyframes navDistort {
  0%, 86%, 100% { opacity: var(--distortion-opacity); }
  90% { opacity: calc(var(--distortion-opacity) + 0.08); }
  94% { opacity: calc(var(--distortion-opacity) - 0.02); }
}

@media (max-width: 900px) {
  .super-nav {
    padding-top: 0.35rem;
  }

  .super-nav-shell {
    min-height: 4.8rem;
    padding: 0.72rem 0.85rem;
    border-radius: 22px;
  }

  .super-links {
    display: none;
  }

  .super-menu-btn {
    display: inline-flex;
  }

  .brand-title {
    font-size: 1.06rem;
  }

  .brand-subtitle {
    font-size: 0.65rem;
    letter-spacing: 0.16em;
  }
}

@media (max-width: 640px) {
  .super-nav {
    --nav-height: 4.65rem;
  }

  .super-nav-shell {
    padding-inline: 0.75rem;
  }

  .brand-glyph {
    width: 2.45rem;
    height: 2.45rem;
    font-size: 0.92rem;
  }

  .brand-subtitle {
    max-width: 16ch;
    line-height: 1.2;
  }

  .mobile-panel {
    padding-top: 5.5rem;
  }
}

@media (prefers-reduced-motion: reduce) {
  .super-nav,
  .super-nav * {
    animation: none !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
</style>
