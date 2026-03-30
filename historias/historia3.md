<div class="skeletal-hand" aria-hidden="true"> Escenario 2: Animación más dinámica y escalofriante
Dado que la mano esquelética está visible en el Hero
Cuando se cargue la página o al hacer scroll
Entonces la mano debe tener los siguientes comportamientos animados:

* Movimientos sutiles pero inquietantes (ligero temblor constante y natural)

* Flexión lenta y orgánica de los dedos (como si estuviera "viva")

* Efecto de "respiración" o pulso lento (escala suave y constante)

* Rotación mínima y orgánica en diferentes ejes

* Cambios sutiles de opacidad y brillo para dar sensación de profundidad 3D

* Transiciones suaves entre todos los estados de animación

* Animación infinita pero con variación en timing para evitar que se sienta repetitiva

Escenario 3: Aspecto visual mejorado
La mano esquelética debe mantener su estilo calavérico/esquelético, pero verse:

* Más detallada y realista (mejor definición de huesos y articulaciones)

* Con iluminación dramática (sombras y brillos que se mueven con la animación)

* Con un toque siniestro, elegante y escalofriante

* Armoniosa con el estilo general del Hero (glassmorphism, gradientes, atmósfera oscura)

Escenario 4: Rendimiento y accesibilidad

* La animación debe ser fluida (60fps) en desktop y dispositivos móviles

* Usar transformaciones GPU (translate, scale, rotate) para mejor rendimiento

* Mantener el atributo aria-hidden="true" ya que es un elemento decorativo

* La animación no debe interferir con la legibilidad del texto del Hero

* Debe funcionar correctamente tanto en desktop como en móvil

Notas

* Solo se debe modificar el contenido dentro del div con clase skeletal-hand

* Se puede usar CSS Animations + @keyframes o Framer Motion (según lo que ya esté integrado en el proyecto)

* Mantener el estilo oscuro y esquelético actual, solo hacerlo más dinámico y vivo

* La animación debe transmitir una sensación "escalofriante" pero profesional y atractiva

* No modificar la estructura HTML fuera de ese div a menos que sea estrictamente necesario

Tareas

* TK-019-01 Localizar y analizar el div .skeletal-hand en Hero.vue

* TK-019-02 Mejorar los estilos base de la mano (sombras, detalles óseos, profundidad y textura)

* TK-019-03 Crear animaciones (temblor, flexión de dedos, pulso, rotación sutil y cambios de opacidad)

* TK-019-04 Añadir variación en timing y keyframes para que la animación no se sienta repetitiva

* TK-019-05 Optimizar rendimiento usando will-change y transformaciones GPU

* TK-019-06 Probar la animación en desktop y móvil (fluidez y efecto visual)

* TK-019-07 Commit: “US-019: Animación de mano esquelética mejorada - más dinámica y escalofriante”

Prioridad: Media-Alta
Dependencias: Componente Hero.vue ya existente