### Historia de Usuario US-031
**Crear componente de Primera Impresión Formal que se transforma en Tema Terrorífico al interactuar**

**Como** Luis Alfonso García Lagos, desarrollador Full Stack  
**Quiero** un componente inicial que muestre una versión **seria, limpia y formal** de mi información personal (fondo blanco hueso),  
**Para** generar una primera impresión profesional y luego, al detectar cualquier interacción del usuario (scroll o movimiento del mouse), transformarse inmediatamente en el actual diseño terrorífico oscuro del portafolio.

**Criterios de Aceptación**

**Escenario 1: Estado Inicial (Formal)**
Dado que el usuario entra por primera vez al portafolio  
Cuando se carga la página  
Entonces se debe mostrar:
- Un diseño **totalmente formal y profesional**
- Fondo en tono blanco hueso (`#F8F1E9` o `#F5F0E6`)
- Foto mía centrada o en layout elegante
- Nombre completo: **Luis Alfonso García** en tipografía limpia y elegante
- Subtítulo: **Desarrollador de Software Full Stack**
- Breve descripción profesional (2-3 líneas)
- Enlaces discretos a GitHub, LinkedIn y Discord
- Aspecto minimalista, serio y corporativo nada del diseño actual

**Escenario 2: Transformación al Interactuar**
Dado que el usuario realiza cualquier acción (scroll hacia abajo o mueve el mouse)  
Cuando se detecta la primera interacción  
Entonces:
- El componente debe **transformarse inmediatamente** al diseño terrorífico actual (fondo #0A1324, niebla azul, glow #4A9EFF, atmósfera de calabozo)
- La transición debe ser cinematográfica y fluida (usando GSAP)
- La foto, el texto y los colores y toda la pagina deben cambiar progresivamente al estado actual
- Una vez transformado, debe quedarse en el estado actualdurante toda la sesión

**Escenario 3: Comportamiento Técnico**
- La transformación debe activarse con el **primer movimiento** del mouse o el primer scroll
- Solo debe ocurrir **una sola vez** por visita (usar sessionStorage)
- La transición debe ser suave pero impactante (glitch sutil, color shift, inner glow azul, revelado de niebla, etc.)
- Mantener todas las animaciones GSAP del diseño terrorífico actual

**Escenario 4: Responsive**
- El estado formal debe verse exceleQuiero que evalues este achivo y que realices las tareas que ahi se solicitan C:\Users\Luis Alfonso\portafolio\historias\historia7.mdnte en móvil y desktop
- La transición debe funcionar correctamente en todos los dispositivos

**Notas**
- Este componente reemplazará o envolverá al Hero actual.
- Usa la misma foto que ya tienes en assets (`man_in_dungeon_portrait.png`), aplicando diferentes filtros y estilos según el estado.
- El estado formal debe sentirse como un portafolio tradicional de desarrollador serio.
- El estado terrorífico debe ser exactamente el que ya tenemos (calabozo, niebla azul, glow, etc.).
- Puedes crear un componente llamado `HeroTransform.vue` o `InitialHero.vue`.

**Tareas**

**Pendiente**
* TK-031-01 Crear componente `InitialHero.vue` con estado formal (fondo blanco hueso)
* TK-031-02 Implementar detección de primera interacción (mousemove + scroll)
* TK-031-03 Crear timeline de transformación con GSAP (de formal → terrorífico)
* TK-031-04 Añadir efectos cinematográficos durante la transición (color shift, glow, niebla, glitch sutil)
* TK-031-05 Asegurar que la transformación ocurra solo una vez por sesión
* TK-031-06 Hacer el componente totalmente responsive
* TK-031-07 Integrar el nuevo componente en `App.vue` reemplazando el Hero actual
* TK-031-08 Optimizar rendimiento y limpiar código

**Haciendo**
(ninguna)

**Hecho**
(marcar al completar)

**Prioridad**  
Muy Alta

**Dependencias**
- Archivo de estilos global (`src/style.css` o `main.css`)
- GSAP ya instalado
- Imagen de portada en `src/assets/images/man_in_dungeon_portrait.png`
- Paleta actual de colores terroríficos (#0A1324, #1B3A5F, #4A9EFF, #B8C8E0)

**Instrucciones para OpenCode / IA:**
Usa el archivo de estilos global para mantener consistencia. Implementa todo con Vue 3 Composition API + GSAP. Quiero una transición cinematográfica fuerte pero elegante. El estado inicial debe ser serio y profesional, y la transformación debe revelar el verdadero estilo terrorífico del portafolio.