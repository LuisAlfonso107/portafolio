### Historia de Usuario 
**Crear componente inicial independiente "FormalPortfolio" como primera vista del portafolio**

**Como** Luis Alfonso García Lagos, desarrollador Full Stack  
**Quiero** crear un componente completamente independiente dentro de la carpeta `src/components/sections/` llamado `FormalPortfolio.vue`  
**Para** que sea la **primera sección** que se muestre al cargar la página, con un estilo totalmente formal, serio y profesional, totalmente diferente al resto del portafolio terrorífico.

**Criterios de Aceptación**

**Escenario 1: Diseño y Estilo**
Dado que el usuario entra por primera vez al portafolio  
Cuando se carga la página  
Entonces debe mostrarse el componente `FormalPortfolio.vue` con:
- Estilo **100% formal y serio** (nada de elementos terroríficos, glows azules ni atmósfera oscura)
- Fondo blanco hueso elegante (`#F8F4ED` o `#FAF6F0`)
- Tipografía limpia y profesional (Inter, System UI o similar)
- Layout limpio, minimalista y bien estructurado
- Aspecto similar a un portafolio corporativo premium

**Escenario 2: Contenido del componente**
El componente debe mostrar de forma clara y concreta toda mi información general:
- Foto profesional mía (usar la imagen ubicada en `src/assets/images/man_in_dungeon_portrait.png` con filtro limpio)
- Nombre completo: **Luis Alfonso García**
- Título profesional: **Desarrollador de Software Full Stack**
- Breve bio profesional (3-4 líneas)
- Información clave:
  - Ubicación (si deseas incluirla)
  - Enlaces directos a:
    - GitHub → https://github.com/LuisAlfonso107
    - LinkedIn → https://www.linkedin.com/in/luis-alfonso-garcia-lagos-27b70722a
    - Discord → oneoseven107
- Botón o enlace claro para "Ver mi trabajo" o "Continuar al portafolio"

**Escenario 3: Independencia**
- Este componente debe ser **totalmente independiente** del resto de secciones terroríficas.
- No debe heredar estilos globales terroríficos (glow, niebla, etc.).
- Debe poder funcionar como una página independiente si es necesario.
- Debe estar dentro de la carpeta: `src/components/sections/FormalPortfolio.vue`

**Escenario 4: Comportamiento**
- Este componente será el **primero** que se renderice al abrir la página (en App.vue).
- Debe tener una transición suave hacia el resto del portafolio terrorífico (opcional, pero recomendado).
- Totalmente responsive (excelente experiencia en móvil y desktop).

**Notas**
- Este es el "portafolio formal" que se muestra al inicio.
- El estilo debe transmitir profesionalismo, confianza y seriedad.
- Usa Tailwind CSS para mantener consistencia con el proyecto.
- La foto debe verse limpia y profesional (puedes aplicar un filtro suave si es necesario).
- Mantén el texto claro, concreto y bien redactado.

**Tareas**

**Pendiente**
(ninguna)

**Haciendo**
(ninguna)

**Hecho**
* [x] TK-032-01 Crear el archivo `FormalPortfolio.vue` dentro de `src/components/sections/`
* [x] TK-032-02 Diseñar el layout formal con fondo blanco hueso y tipografía limpia
* [x] TK-032-03 Incluir foto, nombre, título, bio y enlaces reales (GitHub, LinkedIn, Discord)
* [x] TK-032-04 Hacer el componente totalmente responsive
* [x] TK-032-05 Integrar `FormalPortfolio.vue` como primera sección en `App.vue`
* [x] TK-032-06 Preparar transición suave hacia el diseño terrorífico (opcional)

**Prioridad**  
Alta

**Dependencias**
- Imagen en `src/assets/images/man_in_dungeon_portrait.png`
- Tailwind CSS configurado
- GSAP (si se quiere añadir transición)

**Instrucciones para la IA:**
Crea el componente `FormalPortfolio.vue` como un módulo independiente, con estilo formal serio y profesional. No uses ninguna clase terrorífica ni colores oscuros. El componente debe ser limpio, elegante y contener toda la información personal de Luis Alfonso García de forma clara y concreta.