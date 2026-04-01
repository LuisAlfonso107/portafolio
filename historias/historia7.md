### Historia de Usuario US-025
**Implementar un Super Mega Nav con scroll revelador de imágenes terroríficas antiguas y efectos cinematográficos**

**Como** desarrollador frontend  
**Quiero** crear un navbar avanzado ("Super Mega Nav") que al hacer scroll muestre y revele imágenes antiguas terroríficas  
**Para** generar una experiencia inmersiva, oscura y perturbadora desde el primer momento que el usuario navega por la página

**Criterios de Aceptación**

**Escenario 1: Diseño general del Super Mega Nav**
Dado que el usuario carga cualquier página  
Cuando aparece el navbar  
Entonces debe ser un **Super Mega Nav** con:
- Diseño oscuro, premium y cinematográfico
- Altura variable (se expande o contrae según scroll)
- Fondo con efecto glassmorphism oscuro o semi-transparente
- Logo a la izquierda con estilo terrorífico
- Enlaces de navegación elegantes (Home, Portafolio, Sobre mí, Contacto, etc.)

**Escenario 2: Efecto de scroll revelador de imágenes terroríficas**
Dado que el usuario hace scroll hacia abajo  
Cuando el navbar detecta el movimiento  
Entonces:
- Se revela progresivamente una imagen antigua aterradora (del estilo de las fotos antiguas de creepypasta: niños victorianos siniestros, retratos perturbadores, imágenes antiguas con daño, etc.)
- La imagen debe aparecer con efecto parallax, fade, o blend mode que se sienta como si estuviera "emergiendo" desde el fondo
- La imagen cambia o evoluciona sutilmente mientras se sigue scrolleando (efecto cinematográfico)
- La imagen debe ser grande, de alta calidad y con fuerte impacto visual (blanco y negro o con tonos sepia/oscuros)

**Escenario 3: Comportamiento en móvil**
Dado que el usuario está en dispositivo móvil  
Cuando se carga el navbar  
Entonces:
- Se activa una media query que transforma el nav en versión móvil
- Aparece un botón de hamburguesa grande y terrorífico
- Al hacer clic se abre un menú lateral o fullscreen con animaciones siniestras
- Los enlaces del menú también deben tener efectos hover perturbadores
- La imagen reveladora por scroll debe seguir funcionando correctamente en móvil

**Escenario 4: Efectos muy geniales durante el scroll**
La interacción con el scroll debe incluir efectos cinematográficos y premium:
- Parallax avanzado en la imagen de fondo
- Efectos de grain, distorsión sutil o vignette al scrollear
- Transiciones suaves entre estados del navbar (expandido / contraído)
- Glows, sombras volumétricas y cambios de opacidad en los enlaces
- Animación fluida a 60fps sin lag

**Escenario 5: Rendimiento y accesibilidad**
- Todo el navbar debe ser fluido y de alto rendimiento (GPU accelerated)
- Mantener buena accesibilidad (aria-labels, keyboard navigation, focus states)
- La imagen reveladora debe tener `aria-hidden="true"` ya que es decorativa
- Responsive perfecto en todos los tamaños de pantalla

**Notas**
- La imagen principal debe ser de estilo "fotos antiguas aterradoras" (estilo creepypasta, victorianas perturbadoras, retratos siniestros, etc.)
- Se puede usar Framer Motion, GSAP o CSS Scroll-Driven Animations para los efectos
- El navbar debe sentirse premium, oscuro y coherente con el estilo bizarro/terrorífico del portafolio
- La imagen reveladora debe ser impactante pero no distraer demasiado de la navegación

**Tareas**
TK-025-01 Crear el componente SuperMegaNav.vue con estructura base  
TK-025-02 Implementar el efecto de scroll revelador de imagen terrorífica antigua  
TK-025-03 Añadir media queries y menú hamburguesa completo para móvil  
TK-025-04 Crear efectos cinematográficos avanzados durante el scroll (parallax, blend, grain, etc.)  
TK-025-05 Diseñar el navbar con estilo oscuro y premium  
TK-025-06 Optimizar rendimiento y fluidez en desktop y móvil  
TK-025-07 Integrar el Super Mega Nav en App.vue  
TK-025-08 Commit: “US-025: Super Mega Nav con scroll revelador de imágenes terroríficas implementado”

**Prioridad**  
Muy Alta – Es el primer elemento que ve el usuario y define la experiencia completa del portafolio

**Dependencias**  
- Componente Hero.vue (para probar el scroll)  
- Estilo general oscuro del portafolio