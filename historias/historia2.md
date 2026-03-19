# Historia de Usuario - Portafolio Personal Terrorifico

**US-001**  
**Crear Portafolio Web Personal con Estetica de Bosque Maldito y Niebla Azul**  
**Como** Luis Alfonso Garcia Lagos, desarrollador frontend con experiencia en Vue, React y Tailwind,  
**Quiero** un portafolio online impactante, oscuro y terrorifico inspirado en un bosque embrujado con mano esqueletica y glow azul,  
**Para** mostrar mi identidad como "FULL-STACK DEMON ENGINEER", destacar mis proyectos realizados y atraer oportunidades laborales o freelance.

**Criterios de Aceptacion Generales**  
- El sitio debe ser 100% responsive (mobile-first).  
- Usar **Vue 3 + Composition API** + **Tailwind CSS v4**.  
- Paleta de colores exacta:  
  - Fondo principal: #0A1324  
  - Niebla/frio: #1B3A5F  
  - Glow electrico: #4A9EFF  
  - Hueso/texto claro: #B8C8E0  
- Fuentes: UnifrakturCook (titulos goticos), Creepster (detalles creepy), fallback sans-serif.  
- Animaciones sutiles: niebla flotante, glow en hover, lift en tarjetas.  
- Accesibilidad basica (contraste suficiente en textos).  
- Deploy en Vercel al finalizar.  
- Performance: Lighthouse >= 95 en desktop y mobile.

**Escenario principal - Visualizacion del portafolio**  
Dado que un visitante (recruiter, cliente o curioso) accede a https://tu-portafolio.vercel.app  
Cuando carga la pagina  
Entonces:  
- Ve un hero impactante con fondo de bosque oscuro + niebla animada + mano esqueletica saliendo del suelo  
- Lee mi nombre grande con glow: **Luis Alfonso** o **Luis Alfonso Garcia Lagos**  
- Ve subtitulo: "Full-Stack Demon Engineer" o "Frontend del Inframundo"  
- Puede navegar facilmente a: Sobre mi · Proyectos · Habilidades · Contacto  
- Todo con tema terrorifico coherente (sin ser ilegible)

**Seccion "Sobre mi" - Informacion personal**  
Dado que el usuario esta en la seccion #about  
Cuando lee mi bio  
Entonces ve:  
- Foto mia (estilo oscuro/filtro azul si es posible)  
- Texto aproximado:  
  "Soy Luis Alfonso Garcia Lagos, desarrollador Full-Stack desde Espana. Me especializo en crear experiencias web que aterrorizan por su calidad: Vue, React, Tailwind, Node.js y mas. Actualmente invoco interfaces desde el abismo."  
- Enlaces visibles:  
  - GitHub: https://github.com/LuisAlfonso107  
  - LinkedIn: https://www.linkedin.com/in/luis-alfonso-garcia-lagos-27b70722a  
  - Discord: oneoseven107

**Seccion "Proyectos Resucitados" - Mis trabajos realizados**  
Dado que el usuario esta en la seccion #projects  
Cuando observa la grid de tarjetas  
Entonces ve al menos estas 4 tarjetas (con imagen representativa, titulo, descripcion corta, botones):  

1. **Restaurante Amalur**  
   - Descripcion: Sitio web para Smash Burger Amalur (Barakaldo) - Menu de hamburguesas smash, historia, reservas por WhatsApp.  
   - Enlace demo: https://retaurante-amalur.vercel.app/  
   - Enlace repo: (agrega tu repo de GitHub si existe, o solo demo)  

2. **Reserva Negra**  
   - Descripcion: Landing para cafe de especialidad premium (granos de Nicaragua) - Historia, perfil de taza, lista de espera.  
   - Enlace demo: https://reseva-negra.vercel.app/  
   - Enlace repo: (agrega si tienes)  

3. **Kaboomfot - Football Recruitment**  
   - Descripcion: Plataforma / sitio relacionado con reclutamiento deportivo / futbol en Espana.  
   - Enlace demo: https://actividad-deportiva.vercel.app/  
   - Enlace repo: (agrega si tienes)  

4. **Symphony Store - Tienda de Instrumentos**  
   - Descripcion: E-commerce online de instrumentos musicales.  
   - Enlace demo: https://tineda-de-instrumentos.vercel.app/  
   - Enlace repo: (agrega si tienes)  

Cada tarjeta debe tener:  
- Imagen (screenshot o placeholder terrorifico)  
- Titulo con glow  
- Descripcion breve  
- Boton "VER DEMO" -> link Vercel  
- Boton "GITHUB" -> link repo (si existe, sino oculto o placeholder)

**Seccion Contacto / Invocame**  
Dado que el usuario quiere contactarme  
Cuando llega al final o seccion #contact  
Entonces ve:  
- Formulario simple (nombre, email, mensaje) -> opcional con EmailJS o solo visual  
- Links grandes:  
  - GitHub -> https://github.com/LuisAlfonso107  
  - LinkedIn -> https://www.linkedin.com/in/luis-alfonso-garcia-lagos-27b70722a  
  - Discord: oneoseven107 (con icono o texto clickable)  
- Texto creepy: "Invocame... si te atreves"

**Tareas asociadas (para ir marcando progreso)**

**Pendiente**  
(sin tareas pendientes de esta historia)

**Haciendo**  
(nada por ahora - actualiza segun avances)

**Hecho**  
- TK-001-01 Crear layout base + Navbar terrorifico  
- TK-001-02 Implementar Hero con fondo bosque + niebla + mano  
- TK-001-03 Crear componente ProjectCard reutilizable  
- TK-001-04 Implementar seccion Projects con los 4 proyectos reales  
- TK-001-05 Crear seccion About con bio + foto + enlaces GitHub/LinkedIn/Discord  
- TK-001-06 Crear seccion Skills (Vue, Tailwind, React, Node, etc.)  
- TK-001-07 Crear seccion Contacto con enlaces  
- TK-001-08 Anadir footer con copyright + GitHub link  
- TK-001-09 Cambiar la foto de la seccion de mi historia maldita y poner la captura de pantalla que se encuentra en la carpeta assets

**Notas adicionales**  
- Mi GitHub real: https://github.com/LuisAlfonso107  
- Mi vibe: "FULL-STACK DEMON ENGINEER" - mantener humor oscuro en textos.  
- Si agrego mas proyectos despues, solo actualizar el array en `src/App.vue`.  
- Usar assets locales para imagenes (forest-horror.jpg, mi-foto.jpg, screenshots de proyectos).
