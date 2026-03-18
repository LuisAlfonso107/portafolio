<script setup>
import Footer from './components/layout/Footer.vue'
import Navbar from './components/layout/Navbar.vue'
import About from './components/sections/About.vue'
import Contact from './components/sections/Contact.vue'
import Hero from './components/sections/Hero.vue'
import Projects from './components/sections/Projects.vue'
import Skills from './components/sections/Skills.vue'

const navItems = [
  { label: 'Invocacion', href: '#hero' },
  { label: 'Reliquias', href: '#projects' },
  { label: 'Historia', href: '#about' },
  { label: 'Poderes', href: '#skills' },
  { label: 'Contacto', href: '#contact' },
]

const projects = [
  {
    title: 'Cryptic Commerce',
    description:
      'E-commerce performante con experiencia inmersiva, catalogo dinamico y checkout optimizado para conversion.',
    image:
      'https://images.unsplash.com/photo-1516321318423-f06f85e504b3?auto=format&fit=crop&w=1200&q=80',
    demoUrl: 'https://vercel.com/',
    githubUrl: 'https://github.com/',
  },
  {
    title: 'Phantom Dashboard',
    description:
      'Panel analitico con visualizaciones en tiempo real, estados criticos y flujos claros para equipos operativos.',
    image:
      'https://images.unsplash.com/photo-1551288049-bebda4e38f71?auto=format&fit=crop&w=1200&q=80',
    demoUrl: 'https://vercel.com/',
    githubUrl: 'https://github.com/',
  },
  {
    title: 'Ritual Booking',
    description:
      'Aplicacion de reservas mobile-first con transiciones suaves, formularios robustos y UX enfocada en velocidad.',
    image:
      'https://images.unsplash.com/photo-1498050108023-c5249f4df085?auto=format&fit=crop&w=1200&q=80',
    demoUrl: 'https://vercel.com/',
    githubUrl: 'https://github.com/',
  },
]

const skills = [
  { name: 'Vue 3', icon: 'V' },
  { name: 'JavaScript', icon: 'JS' },
  { name: 'Tailwind', icon: 'TW' },
  { name: 'GSAP', icon: 'G' },
  { name: 'Vite', icon: 'Vi' },
  { name: 'UI Motion', icon: 'FX' },
]

const socialLinks = [
  { label: 'GitHub', href: 'https://github.com/' },
  { label: 'LinkedIn', href: 'https://www.linkedin.com/' },
  { label: 'Email', href: 'mailto:luis@example.com' },
]
</script>

<template>
  <div class="app-shell">
    <Navbar :items="navItems" />
    <Hero name="Luis Alfonso" />
    <Projects :projects="projects" />
    <About
      name="Luis Alfonso"
      role="Frontend Developer"
      bio="Construyo interfaces memorables con foco en claridad, performance y una direccion visual que no se parece al resto. Me interesan los productos que mezclan narrativa, velocidad y precision tecnica."
      image-url="https://images.unsplash.com/photo-1500648767791-00dcc994a43e?auto=format&fit=crop&w=900&q=80"
    />
    <Skills :items="skills" />
    <Contact :social-links="socialLinks" />
    <Footer />
  </div>
</template>
