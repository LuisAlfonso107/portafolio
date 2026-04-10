<script setup>
defineProps({
  name: {
    type: String,
    required: true,
  },
  role: {
    type: String,
    required: true,
  },
  bio: {
    type: String,
    required: true,
  },
  imageUrl: {
    type: String,
    required: true,
  },
  links: {
    type: Array,
    default: () => [],
  },
})
</script>

<template>
  <section id="about" class="section">
    <div class="container overflow-visible">
      <div class="about-card relative overflow-hidden rounded-[2.5rem] bg-black/30 backdrop-blur-xl border border-white/5 shadow-[0_20px_50px_rgba(0,0,0,0.5)] group">
        <!-- Grid Unificado -->
        <div class="grid grid-cols-1 md:grid-cols-2 items-stretch">
          
          <!-- Lado de la imagen: Integrado -->
          <div class="about-media relative min-h-[400px] md:min-h-full overflow-hidden">
            <img :src="imageUrl" :alt="name" class="absolute inset-0 w-full h-full object-cover transition-transform duration-1000 group-hover:scale-110 saturate-[0.8] contrast-[1.1]" loading="lazy" />
            <!-- Overlay de gradiente para suavizar transición -->
            <div class="absolute inset-0 bg-gradient-to-t md:bg-gradient-to-r from-transparent via-transparent to-black/40"></div>
          </div>

          <!-- Lado del texto: Integrado -->
          <div class="about-copy relative p-8 md:p-14 flex flex-col justify-center">
            <!-- Elementos decorativos de fondo internos -->
            <div class="absolute -top-24 -right-24 w-64 h-64 bg-blue-500/5 rounded-full blur-3xl"></div>
            
            <div class="relative z-10">
              <p class="eyebrow inline-flex items-center gap-2 px-4 py-1.5 rounded-full bg-blue-500/10 border border-blue-500/20 text-blue-400 text-xs font-bold uppercase tracking-[0.2em] mb-6">
                <span class="w-1.5 h-1.5 rounded-full bg-blue-500 animate-pulse"></span>
                Sobre mí
              </p>
              
              <h2 class="text-5xl md:text-7xl font-bold mb-3 tracking-tighter text-white drop-shadow-2xl">
                {{ name }}
              </h2>
              
              <p class="about-role text-2xl text-blue-400/90 font-medium mb-8 italic tracking-wide">
                {{ role }}
              </p>
              
              <div class="space-y-6 text-gray-300/90 leading-relaxed text-lg font-light">
                <p v-for="(paragraph, index) in bio.split('\n')" :key="index">
                  {{ paragraph }}
                </p>
              </div>

              <div class="social-links about-links flex flex-wrap gap-4 mt-12">
                <a v-for="link in links" :key="link.label" :href="link.href" target="_blank" rel="noreferrer"
                   class="flex items-center gap-3 px-6 py-3 rounded-2xl bg-white/5 border border-white/10 hover:bg-white/10 hover:border-blue-500/50 hover:shadow-[0_0_30px_rgba(59,130,246,0.2)] transition-all duration-500 group/link">
                  <span class="text-sm font-bold tracking-widest uppercase group-hover/link:text-blue-400 transition-colors">
                    {{ link.label }}
                  </span>
                  <span v-if="link.text" class="text-xs text-gray-500 group-hover/link:text-gray-400 transition-colors font-medium">
                    | {{ link.text }}
                  </span>
                  <div class="w-5 h-5 flex items-center justify-center opacity-40 group-hover/link:opacity-100 group-hover/link:translate-x-1 transition-all">
                    <svg class="w-full h-full text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                    </svg>
                  </div>
                </a>
              </div>
            </div>
          </div>
        </div>

        <!-- Detalles de acabado premium -->
        <div class="absolute top-0 left-0 w-full h-[1px] bg-gradient-to-r from-transparent via-white/20 to-transparent"></div>
        <div class="absolute bottom-0 left-0 w-full h-[1px] bg-gradient-to-r from-transparent via-white/10 to-transparent shadow-[0_0_20px_rgba(255,255,255,0.05)]"></div>
      </div>
    </div>
  </section>
</template>
