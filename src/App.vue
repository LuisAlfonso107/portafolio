<script setup>
import { ref } from 'vue'
import FormalPortfolio from './components/sections/FormalPortfolio.vue'
import aboutPortrait from './assets/Captura de pantalla 2026-03-19 133450.png'
import Footer from './components/layout/Footer.vue'
import SuperMegaNav from './components/layout/SuperMegaNav.vue'
import About from './components/sections/About.vue'
import Contact from './components/sections/Contact.vue'
import Hero from './components/sections/Hero.vue'
import Projects from './components/sections/Projects.vue'
import Skills from './components/sections/Skills.vue'

const navItems = [
  { label: 'Inicio', href: '#hero' },
  { label: 'Sobre mi', href: '#about' },
  { label: 'Proyectos', href: '#projects' },
  { label: 'Habilidades', href: '#skills' },
  { label: 'Contacto', href: '#contact' },
]

const projects = [
  {
    title: 'Restaurante Amalur',
    description:
      'Sitio web para Smash Burger Amalur en Barakaldo con menu de hamburguesas smash, relato de marca y reservas por WhatsApp.',
    imageClass: 'project-art-amalur',
    demoUrl: 'https://retaurante-amalur.vercel.app/',
  },
  {
    title: 'Reserva Negra',
    description:
      'Landing para cafe de especialidad premium con historia de origen, perfil de taza y lista de espera para nuevos clientes.',
    imageClass: 'project-art-reserva',
    demoUrl: 'https://reseva-negra.vercel.app/',
  },
  {
    title: 'Kaboomfot - Football Recruitment',
    description:
      'Proyecto orientado al reclutamiento deportivo y futbol en Espana, con propuesta clara para descubrir talento y conectar perfiles.',
    imageClass: 'project-art-kaboom',
    demoUrl: 'https://actividad-deportiva.vercel.app/',
  },
  {
    title: 'Symphony Store - Tienda de Instrumentos',
    description:
      'E-commerce de instrumentos musicales con catalogo visual, categorias destacadas y una experiencia enfocada en conversion.',
    imageClass: 'project-art-symphony',
    demoUrl: 'https://tineda-de-instrumentos.vercel.app/',
  },
]

const skills = [
  { name: 'Vue 3', icon: 'V3' },
  { name: 'React', icon: 'Re' },
  { name: 'Tailwind CSS', icon: 'TW' },
  { name: 'Node.js', icon: 'Nd' },
  { name: 'JavaScript', icon: 'JS' },
  { name: 'Vite', icon: 'Vi' },
]

const aboutLinks = [
  { label: 'GitHub', href: 'https://github.com/LuisAlfonso107' },
  { label: 'LinkedIn', href: 'https://www.linkedin.com/in/luis-alfonso-garcia-lagos-27b70722a' },
  { label: 'Discord', href: 'https://discord.com/users/oneoseven107', text: 'oneoseven107' },
]

const socialLinks = [
  { label: 'GitHub', href: 'https://github.com/LuisAlfonso107' },
  { label: 'LinkedIn', href: 'https://www.linkedin.com/in/luis-alfonso-garcia-lagos-27b70722a' },
  { label: 'Discord', href: 'https://discord.com/users/oneoseven107', text: 'oneoseven107' },
]

const showFormalPortfolio = ref(true)

const continueToHorrorTheme = () => {
  showFormalPortfolio.value = false
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>

<template>
  <Transition name="fade" mode="out-in">
    <FormalPortfolio v-if="showFormalPortfolio" @continue="continueToHorrorTheme" />
    <div v-else class="app-shell">
      <SuperMegaNav :items="navItems" />
      <div class="fusion-zone zone-black seep-blue edge-black-to-blue">
        <span class="fusion-branches" aria-hidden="true"></span>
        <span class="fusion-rift" aria-hidden="true"></span>
        <span class="fusion-presence" aria-hidden="true"></span>
        <Hero
          name="Luis Alfonso Garcia "
          title="Full-Stack"
          summary="Desarrollo experiencias web con precision visual y rendimiento."
        />
      </div>

      <div class="fusion-zone zone-blue devoured-by-black edge-blue-to-black">
        <span class="fusion-branches" aria-hidden="true"></span>
        <span class="fusion-rift" aria-hidden="true"></span>
        <span class="fusion-presence" aria-hidden="true"></span>
        <About
          name="Luis Alfonso Garcia "
          role="Full-Stack "
          bio="Soy Luis Alfonso Garcia Lagos, desarrollador Full-Stack. Me especializo en crear experiencia por su calidad y la capacidad de adaptarme a nuevas tecnologias: Vue, React, Tailwind, Node.js y mas. Actualmente invoco interfaces desde el abismo."
          :links="aboutLinks"
          :image-url="aboutPortrait"
        />
      </div>

      <div class="fusion-zone zone-black seep-blue edge-black-to-blue">
        <span class="fusion-branches" aria-hidden="true"></span>
        <span class="fusion-rift" aria-hidden="true"></span>
        <span class="fusion-presence" aria-hidden="true"></span>
        <Projects :projects="projects" />
      </div>

      <div class="fusion-zone zone-blue devoured-by-black edge-blue-to-black">
        <span class="fusion-branches" aria-hidden="true"></span>
        <span class="fusion-rift" aria-hidden="true"></span>
        <span class="fusion-presence" aria-hidden="true"></span>
        <Skills :items="skills" />
      </div>

      <div class="fusion-zone zone-black seep-blue">
        <span class="fusion-branches" aria-hidden="true"></span>
        <span class="fusion-rift" aria-hidden="true"></span>
        <span class="fusion-presence" aria-hidden="true"></span>
        <Contact :social-links="socialLinks" />
      </div>
      <Footer github-url="https://github.com/LuisAlfonso107" />
    </div>
  </Transition>
</template>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 1.2s ease-in-out;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
