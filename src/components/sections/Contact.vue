<script setup>
defineProps({
  socialLinks: {
    type: Array,
    default: () => [],
  },
})
</script>

<template>
  <section id="contact" class="section">
    <div class="container contact-grid">
      <div class="contact-copy">
        <p class="eyebrow">Ultimo ritual</p>
        <h2>Conversemos</h2>
        <p>
          Si necesitas una interfaz con identidad, rendimiento y criterio tecnico, este es el punto de entrada.
        </p>
        <div class="social-links">
          <a v-for="link in socialLinks" :key="link.label" :href="link.href" target="_blank" rel="noreferrer">
            {{ link.label }}
          </a>
        </div>
      </div>
      <form class="contact-form">
        <label>
          Nombre
          <input type="text" name="name" placeholder="Tu nombre" />
        </label>
        <label>
          Email
          <input type="email" name="email" placeholder="tu@email.com" />
        </label>
        <label>
          Mensaje
          <textarea name="message" rows="5" placeholder="Describe el proyecto"></textarea>
        </label>
        <button class="button-primary" type="submit">Abrir portal</button>
      </form>
    </div>
  </section>
</template>
