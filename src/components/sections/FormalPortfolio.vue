<script setup>
const emit = defineEmits(['continue'])

// Usamos new URL para evitar que Vite rompa el build si la imagen aún no existe.
const profilePic = new URL('../../assets/IMG20220207183712.jpg', import.meta.url).href

const links = [
  { 
    label: 'GitHub', 
    url: 'https://github.com/LuisAlfonso107', 
    icon: 'M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z' 
  },
  { 
    label: 'LinkedIn', 
    url: 'https://www.linkedin.com/in/luis-alfonso-garcia-lagos-27b70722a', 
    icon: 'M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z' 
  },
  { 
    label: 'Discord', 
    url: 'https://discord.com/users/oneoseven107', 
    icon: 'M20.317 4.3698a19.7913 19.7913 0 00-4.8851-1.5152.0741.0741 0 00-.0785.0371c-.211.3753-.4447.8648-.6083 1.2495-1.8447-.2762-3.68-.2762-5.4868 0-.1636-.3933-.4058-.8742-.6177-1.2495a.077.077 0 00-.0785-.037 19.7363 19.7363 0 00-4.8852 1.515.0699.0699 0 00-.0321.0277C.5334 9.0458-.319 13.5799.0992 18.0578a.0824.0824 0 00.0312.0561c2.0528 1.5076 4.0413 2.4228 5.9929 3.0294a.0777.0777 0 00.0842-.0276c.4616-.6304.8731-1.2952 1.226-1.9942a.076.076 0 00-.0416-.1057c-.6528-.2476-1.2743-.5495-1.8722-.8923a.077.077 0 01-.0076-.1277c.1258-.0943.2517-.1923.3718-.2914a.0743.0743 0 01.0776-.0105c3.9278 1.7933 8.18 1.7933 12.0614 0a.0739.0739 0 01.0785.0095c.1202.099.246.1981.3728.2924a.077.077 0 01-.0066.1276 12.2986 12.2986 0 01-1.873.8914.0766.0766 0 00-.0407.1067c.3604.698.7719 1.3628 1.225 1.9932a.076.076 0 00.0842.0286c1.961-.6067 3.9495-1.5219 6.0023-3.0294a.077.077 0 00.0313-.0552c.5004-5.177-.8382-9.6739-3.5485-13.6604a.061.061 0 00-.0312-.0286zM8.02 15.3312c-1.1825 0-2.1569-1.0857-2.1569-2.419 0-1.3332.9555-2.4189 2.157-2.4189 1.2108 0 2.1757 1.0952 2.1568 2.419 0 1.3332-.9555 2.4189-2.1569 2.4189zm7.9748 0c-1.1825 0-2.1569-1.0857-2.1569-2.419 0-1.3332.9554-2.4189 2.1569-2.4189 1.2108 0 2.1757 1.0952 2.1568 2.419 0 1.3332-.946 2.4189-2.1568 2.4189z' 
  }
]
</script>

<template>
  <div class="fixed inset-0 z-50 bg-[#F8F4ED] overflow-hidden flex items-center justify-center font-sans text-gray-900 transition-opacity duration-1000 w-full p-4 md:p-8">
    
    <!-- Decorative background blobs for Glassmorphism contrast -->
    <div class="absolute top-[-10%] left-[-10%] w-[30rem] h-[30rem] bg-indigo-100/40 rounded-full mix-blend-multiply filter blur-3xl opacity-70 animate-blob"></div>
    <div class="absolute top-[20%] right-[-5%] w-[25rem] h-[25rem] bg-stone-200/50 rounded-full mix-blend-multiply filter blur-3xl opacity-70 animate-blob animation-delay-2000"></div>
    <div class="absolute bottom-[-10%] left-[20%] w-[28rem] h-[28rem] bg-slate-200/40 rounded-full mix-blend-multiply filter blur-3xl opacity-70 animate-blob animation-delay-4000"></div>

    <div class="relative z-10 max-w-4xl w-full mx-auto p-8 md:p-12 bg-white/40 backdrop-blur-2xl rounded-3xl shadow-[0_8px_30px_rgb(0,0,0,0.06)] flex flex-col md:flex-row items-center gap-12 border border-white/60">
      
      <div class="w-48 h-48 md:w-64 md:h-64 rounded-2xl md:rounded-full overflow-hidden shrink-0 shadow-[0_10px_40px_rgb(0,0,0,0.1)] border-4 border-white/80 bg-white/50 backdrop-blur-sm flex items-center justify-center transform transition-transform duration-700 hover:scale-105">
        <!-- Utilizamos un fallback por si la imagen no se carga y una clase para imagen limpia -->
        <img 
          :src="profilePic" 
          alt="Luis Alfonso Garcia" 
          class="w-full h-full object-cover filter contrast-105 brightness-105" 
          onerror="this.src='https://via.placeholder.com/400?text=Luis+Alfonso'"
        />
      </div>

      <div class="flex-1 text-center md:text-left space-y-6">
        <div class="space-y-2">
          <h1 class="text-4xl md:text-5xl font-bold tracking-tight text-gray-900">Luis Alfonso García</h1>
          <h2 class="text-lg md:text-xl font-medium text-gray-500 tracking-wide uppercase">Desarrollador de Software Full Stack</h2>
        </div>

        <p class="text-lg text-gray-600 leading-relaxed max-w-2xl font-light">
          Soy un desarrollador altamente motivado con experiencia en la creación de aplicaciones web escalables, intuitivas y eficientes. 
          Me especializo en diseñar soluciones tecnológicas robustas que conectan rendimiento y estética para ofrecer la mejor experiencia de usuario.
        </p>

        <div class="flex flex-wrap items-center justify-center md:justify-start gap-4 pt-4">
          <a v-for="link in links" :key="link.label" :href="link.url" target="_blank" rel="noopener noreferrer" 
             class="group flex items-center gap-2 px-6 py-3 rounded-2xl bg-white/50 hover:bg-white/80 backdrop-blur-md text-gray-700 hover:text-gray-950 font-medium transition-all duration-300 border border-white/60 hover:shadow-lg hover:-translate-y-1">
            <svg class="w-5 h-5 fill-current opacity-80 group-hover:opacity-100 transition-opacity" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
              <path :d="link.icon" />
            </svg>
            {{ link.label }}
          </a>
        </div>

        <div class="pt-8 border-t border-gray-900/5 mt-4">
          <button @click="emit('continue')" 
                  class="group relative inline-flex items-center justify-center px-8 py-4 text-base font-semibold text-gray-900 transition-all duration-500 bg-white/70 backdrop-blur-xl rounded-2xl border border-white/80 hover:bg-white focus:outline-none hover:shadow-[0_15px_30px_rgba(0,0,0,0.1)] focus:ring-2 focus:ring-gray-300 focus:ring-offset-2 overflow-hidden hover:scale-[1.02]">
            <span class="relative z-10 flex items-center gap-3">
              Descubre mas sobre mi
              <div class="relative w-7 h-7 flex items-center justify-center overflow-hidden border-2 border-gray-800 rounded-sm bg-white/50 transition-all duration-500 group-hover:border-transparent group-hover:bg-transparent">
                <!-- Ventana que se abre (puertas) -->
                <div class="absolute inset-y-0 left-0 w-1/2 bg-gray-800 transition-transform duration-500 origin-left group-hover:-rotate-y-90 group-hover:opacity-0"></div>
                <div class="absolute inset-y-0 right-0 w-1/2 bg-gray-800 transition-transform duration-500 origin-right group-hover:rotate-y-90 group-hover:opacity-0"></div>
                <!-- Flecha que aparece y avanza -->
                <svg class="w-5 h-5 absolute transform translate-x-[-150%] opacity-0 transition-all duration-500 group-hover:translate-x-0 group-hover:opacity-100 text-gray-900" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                </svg>
              </div>
            </span>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
div {
  box-sizing: border-box;
}

@keyframes blob {
  0% { transform: translate(0px, 0px) scale(1); }
  33% { transform: translate(30px, -50px) scale(1.1); }
  66% { transform: translate(-20px, 20px) scale(0.9); }
  100% { transform: translate(0px, 0px) scale(1); }
}
.animate-blob {
  animation: blob 7s infinite;
}
.animation-delay-2000 {
  animation-delay: 2s;
}
.animation-delay-4000 {
  animation-delay: 4s;
}
.rotate-y-90 {
  transform: rotateY(90deg);
}
.-rotate-y-90 {
  transform: rotateY(-90deg);
}
</style>
