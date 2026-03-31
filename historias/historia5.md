### Historia de Usuario US-021
**Implementar animación de manos calavéricas y arañas espeluznantes caminando infinitamente en el Hero Section**

**Como** desarrollador frontend  
**Quiero** crear una animación oscura y perturbadora con manos calavéricas y arañas en el Hero.vue  
**Para** generar una atmósfera infernal, siniestra y bizarra que impacte visualmente al usuario desde el primer instante

**Criterios de Aceptación**

**Escenario 1: Identificación del elemento**
Dado que estoy trabajando en el archivo:  
`/home/penascalf5/portafolio/src/components/sections/Hero.vue`  

Cuando creo o localizo un contenedor adecuado (por ejemplo: `<div class="horror-elements" aria-hidden="true">`)  
Entonces debo implementar la animación completa dentro de ese contenedor.

**Escenario 2: Animación principal - Manos calavéricas**
Dado que la animación se activa al cargar la página  
Entonces deben aparecer varias manos calavéricas con los siguientes comportamientos:

- Movimientos lentos, convulsivos y antinaturales
- Dedos que se flexionan y se estiran de forma espasmódica
- Manos que se arrastran, se retuercen o intentan "agarrar" el aire
- Efectos de opacidad y glow rojizo/negro intermitente
- Varias manos apareciendo en diferentes posiciones y profundidades

**Escenario 3: Animación secundaria - Arañas espeluznantes**
Dado que la animación está activa  
Entonces deben aparecer arañas negras realistas o estilizadas con los siguientes comportamientos:

- Arañas caminando de forma aleatoria e infinita por toda la pantalla
- Movimientos realistas de patas (crawling)
- Algunas arañas subiendo, bajando o cruzando por encima de las manos calavéricas
- Efecto de velocidad variable (algunas lentas y amenazantes, otras más rápidas)
- Animación completamente infinita (loop seamless)

**Escenario 4: Atmósfera general infernal y bizarra**
La animación completa debe transmitir:

- Sensación oscura, turbia y perturbadora
- Colores dominantes: negro profundo, gris óseo, toques de rojo sangre y púrpura oscuro
- Iluminación dramática con sombras y brillos malignos
- Combinación caótica entre las manos calavéricas y las arañas
- Atmósfera siniestra pero elegante, acorde con el estilo del Hero

**Escenario 5: Rendimiento y accesibilidad**
- La animación debe ser fluida (60fps) en desktop y móvil
- Usar transformaciones GPU para óptimo rendimiento
- Mantener `aria-hidden="true"` (elemento decorativo)
- No interferir con la legibilidad del texto principal del Hero
- Opción de reducir o pausar intensidad en dispositivos móviles (opcional)

**Notas**
- Esta animación es **completamente nueva** y diferente a la anterior mano esquelética
- Debe ser impactante, espeluznante y bizarra sin llegar a ser molesta
- Se puede usar CSS Animations avanzadas o Framer Motion
- Las arañas y manos deben moverse de forma infinita y aleatoria
- Mantener coherencia con el estilo general del portafolio (oscuro y premium)

**Tareas**
TK-021-01 Crear contenedor para elementos de terror en Hero.vue  
TK-021-02 Diseñar y estilizar múltiples manos calavéricas con movimientos espasmódicos  
TK-021-03 Crear y animar arañas espeluznantes caminando por la pantalla  
TK-021-04 Implementar animaciones infinitas y aleatorias (manos + arañas)  
TK-021-05 Añadir efectos visuales turbios (glow, sombras, opacidad)  
TK-021-06 Optimizar rendimiento con GPU y `will-change`  
TK-021-07 Probar la animación en desktop y móvil  
TK-021-08 Commit: “US-021: Animación de manos calavéricas y arañas infernales implementada”

**Prioridad**  
Alta – Impacta fuertemente la primera impresión visual del portafolio

**Dependencias**  
- Componente Hero.vue ya existente