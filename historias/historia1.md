# Historia de Usuario - Portafolio Terrorifico Vue 3

**US-001**  
**Construir Portafolio Personal con Tema Terrorifico Oscuro**  
**Como** desarrollador frontend Luis Alfonso,  
**Quiero** un portafolio web impactante con estetica de bosque maldito y niebla azul,  
**Para** impresionar a recruiters y clientes con un diseno unico y profesional.

---

## Criterios de Aceptacion Generales
- Todo el proyecto debe estar estructurado en componentes Vue 3 (Composition API).
- Usar Tailwind CSS v4 con la paleta exacta: `#0A1324` (bg), `#1B3A5F` (mist), `#4A9EFF` (glow), `#B8C8E0` (bone).
- Fuentes: UnifrakturCook (titulos), Creepster (detalles) + sistema por defecto.
- Responsive 100% (mobile-first).
- Animaciones suaves con GSAP o Tailwind (niebla, glow, hover escalado).
- Performance excelente (Lighthouse > 95).
- Links funcionales a Vercel y GitHub en cada proyecto.

---

## Tareas

### Pendiente

* Reemplazar las imagenes remotas por assets locales definitivos, incluyendo `src/assets/images/forest-horror.jpg`
* Sustituir links placeholder de Vercel/GitHub por URLs reales de proyectos
* Conectar el formulario de contacto a un backend o servicio de envio

### Haciendo

* Refinamiento visual, contenido real y optimizacion de Lighthouse con assets finales

### Hecho

* TK-001-01 Crear componente `Navbar.vue` con efecto glassmorphism y glow azul
* TK-001-02 Crear componente `Hero.vue` con fondo de bosque remoto, niebla animada y texto principal "Luis Alfonso"
* TK-001-03 Crear componente `ProjectCard.vue` reutilizable con hover terrorifico
* TK-001-04 Crear componente `Projects.vue` que contenga la grid de tarjetas
* TK-001-05 Crear componente `About.vue` con foto personal y bio oscura
* TK-001-06 Crear componente `Skills.vue` con iconos y efecto glow al hover
* TK-001-07 Crear componente `Contact.vue` con formulario simple + links sociales
* TK-001-08 Crear componente `Footer.vue`
* TK-001-09 Configurar navegacion por ID de secciones con smooth scroll
* TK-001-10 Integrar GSAP para animaciones de entrada y niebla

---

## Detalle de Tareas (para copiar y pegar a la IA)

**TK-001-01 Crear componente Navbar.vue**  
Crear un navbar fijo, oscuro, con glassmorphism, logo "NECROMANCER.dev" y enlaces a las secciones. Debe tener hover glow azul.

**TK-001-02 Crear componente Hero.vue**  
Seccion completa de altura de pantalla con la imagen del bosque como fondo, overlay oscuro, niebla animada sutil, titulo grande con glow, subtitulo y boton "ENTRA SI TE ATREVES". Usar props para el nombre.

**TK-001-03 Crear componente ProjectCard.vue**  
Tarjeta reutilizable con imagen, titulo, descripcion corta, boton "VER DEMO" (Vercel) y "GITHUB". Efecto hover: borde glow + ligero lift + escala en imagen.

**TK-001-04 Crear componente Projects.vue**  
Seccion con titulo "Proyectos Resucitados", grid responsive y array de proyectos (titulo, descripcion, imagen, vercel link, github link). Usar v-for con ProjectCard.

**TK-001-05 Crear componente About.vue**  
Seccion "Mi Historia Maldita" con foto personal (estilo oscuro) y texto biografico. Layout dos columnas en desktop.

*(Puedes agregar mas tareas aqui segun vayas avanzando)*

---

## Notas Importantes

- Mantener siempre la estructura de carpetas:  
  `src/components/layout/` -> Navbar, Footer  
  `src/components/sections/` -> Hero, About, Projects, Skills, Contact  
  `src/components/ui/` -> ProjectCard

- Todos los componentes deben recibir props cuando sea necesario y emitir eventos si hace falta.

- Usar clases Tailwind consistentes con la paleta definida.

- La imagen del bosque debe estar en `src/assets/images/forest-horror.jpg`

- Mi nombre es **Luis Alfonso**
