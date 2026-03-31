### Historia de Usuario US-020
**Implementar una animación infernal, satánica, turbia y bizarra en el Hero Section (nueva animación)**

**Como** desarrollador frontend  
**Quiero** crear una animación completamente nueva, oscura, perturbadora y caótica en la sección Hero.vue  
**Para** generar una atmósfera infernal, siniestra y memorable que impacte visualmente al usuario desde el primer segundo

**Criterios de Aceptación**

**Escenario 1: Identificación del elemento**
Dado que estoy trabajando en el archivo:  
`/home/penascalf5/portafolio/src/components/sections/Hero.vue`  

Cuando busco un contenedor adecuado para la nueva animación (puede ser un div nuevo con clase `infernal-element` o similar)  
Entonces debo implementar una animación **totalmente diferente** a la mano esquelética anterior.

**Escenario 2: Animación infernal, turbia y satánica**
Dado que el usuario entra en la página Hero  
Cuando la animación se activa (al cargar o al hacer scroll)  

Entonces debe aparecer una animación con las siguientes características:

- Elemento central bizarro (un sigilo demoníaco flotante, un orbe negro con venas rojas, humo negro con formas grotescas, o una entidad oscura amorfa)
- Movimientos lentos, caóticos y antinaturales
- Pulsaciones agresivas y respiraciones demoníacas
- Distorsiones turbias, ruido visual sutil y glows rojos/negros intermitentes
- Rotaciones lentas combinadas con deformaciones orgánicas
- Partículas oscuras o cenizas flotando alrededor del elemento
- Cambios de opacidad y brillo infernal que den sensación de profundidad y maldad
- Animación infinita pero impredecible (variaciones en velocidad e intensidad)

**Escenario 3: Aspecto visual infernal y bizarro**
La animación debe transmitir:

- Atmósfera oscura, satánica y perturbadora
- Colores dominantes: negro profundo, rojo sangre, púrpura oscuro y tonos turbios
- Sensación de algo vivo y maligno (no estático)
- Armonía con el estilo general del Hero (glassmorphism, gradientes oscuros, tipografía fuerte)
- Alto impacto visual sin llegar a ser molesto o lento

**Escenario 4: Rendimiento y accesibilidad**
- La animación debe correr fluida a 60fps en desktop y móvil
- Usar transformaciones GPU y optimizaciones de rendimiento
- Mantener `aria-hidden="true"` ya que es un elemento puramente decorativo
- No interferir con la legibilidad del texto principal del Hero
- Poder pausarse o reducir intensidad en dispositivos de bajo rendimiento (opcional)

**Notas**
- Esta animación **no debe tener nada que ver** con la mano esquelética anterior
- Crear un nuevo elemento visual (sigilo, orbe infernal, entidad oscura, humo viviente, etc.)
- Se puede usar CSS Animations avanzadas con @keyframes o Framer Motion
- El objetivo es una animación impactante, oscura, turbia y bizarra que deje huella
- Mantener coherencia con el estilo general del portafolio

**Tareas**
TK-020-01 Crear un nuevo contenedor para la animación infernal en Hero.vue  
TK-020-02 Diseñar el elemento visual base (sigilo/orbe/entidad oscura) con estilos siniestros  
TK-020-03 Implementar animaciones principales (pulsación demoníaca, distorsión, rotación caótica)  
TK-020-04 Añadir efectos turbios (glow rojo, partículas oscuras, ruido visual)  
TK-020-05 Crear variación caótica en timing para que la animación se sienta viva y perturbadora  
TK-020-06 Optimizar rendimiento con GPU y `will-change`  
TK-020-07 Probar la animación en desktop y móvil  
TK-020-08 Commit: “US-020: Animación infernal, satánica y bizarra implementada en Hero”

**Prioridad**  
Alta – Impacta fuertemente la primera impresión visual del portafolio

**Dependencias**  
- Componente Hero.vue ya existente