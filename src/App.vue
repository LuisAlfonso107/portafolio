<script setup>
import aboutPortrait from './assets/Captura de pantalla 2026-03-19 133450.png'
import Footer from './components/layout/Footer.vue'
import Navbar from './components/layout/Navbar.vue'
import About from './components/sections/About.vue'
import Contact from './components/sections/Contact.vue'
import Hero from './components/sections/Hero.vue'
import Projects from './components/sections/Projects.vue'
import Skills from './components/sections/Skills.vue'

const navItems = [
  { label: 'Invocacion', href: '#hero' },
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
</script>

<template>
  <div class="app-shell">
    <Navbar :items="navItems" />
    <Hero
      name="Luis Alfonso Garcia "
      title="Full-Stack"
      summary="Desarrollo experiencias web con presencia oscura, precision visual y rendimiento disciplinado desde Espana."
    />
    <About
      name="Luis Alfonso Garcia "
      role="Full-Stack "
      bio="Soy Luis Alfonso Garcia Lagos, desarrollador Full-Stack desde Espana. Me especializo en crear experiencias web que aterrorizan por su calidad: Vue, React, Tailwind, Node.js y mas. Actualmente invoco interfaces desde el abismo."
      :links="aboutLinks"
      :image-url="aboutPortrait"
    />
    <Projects :projects="projects" />
    <Skills :items="skills" />
    <Contact :social-links="socialLinks" />
    <Footer github-url="https://github.com/LuisAlfonso107" />
  </div>
</template>
