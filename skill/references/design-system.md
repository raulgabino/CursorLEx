# Sistema de Diseño — ReglaBot

Referencia completa de CSS para la guía de cumplimiento interactiva. Copia estas propiedades personalizadas al inicio de tu `<style>` — son los cimientos de todo lo visual.

---

## Propiedades personalizadas CSS

```css
:root {
  /* ─── PALETA DE COLORES ─── */

  /* --- FONDOS --- */
  --color-bg:            #FAF7F2;     /* off-white papel envejecido — fondo principal */
  --color-bg-warm:       #F5F0E8;     /* variante cálida para módulos alternos */
  --color-bg-code:       #1E1E2E;     /* charcoal índigo para bloques de texto legal */
  --color-bg-card:       #FFFFFF;     /* blanco tarjeta — solo para tarjetas elevadas */

  /* --- TEXTO --- */
  --color-text:          #2C2A28;     /* casi-negro cálido — texto primario */
  --color-text-secondary:#6B6560;     /* gris medio — texto de soporte */
  --color-text-muted:    #9C9590;     /* gris claro — timestamps, metadata */
  --color-text-inverse:  #FAF7F2;     /* para texto sobre fondos oscuros */

  /* --- ACENTO (adaptar por regulación — elige UN color seguro) ---
     Default: teal (confianza institucional). Alternativas: vermillion (#D94F30),
     coral (#E06B56), ámbar (#D4A843), verde bosque (#2D8B55). Evitar degradados morados. */
  --color-accent:        #2A7B9B;
  --color-accent-hover:  #236A87;
  --color-accent-light:  #E4F2F7;
  --color-accent-muted:  #5A9DB5;

  /* --- COLORES DE ENTIDAD (asignar a actores regulatorios) ---
     Cada "entidad" principal en el panorama regulatorio recibe un color distinto
     para diagramas de flujo, tarjetas de obligación y resaltados */
  --color-entity-1:      #2A7B9B;     /* teal — el alumno/sujeto regulado */
  --color-entity-2:      #D94F30;     /* vermillion — autoridad competente */
  --color-entity-3:      #7B6DAA;     /* ciruela — terceros */
  --color-entity-4:      #D4A843;     /* dorado — titulares/partes afectadas */
  --color-entity-5:      #2D8B55;     /* verde bosque — estado de cumplimiento */

  /* --- SEVERIDAD DE SANCIONES --- */
  --color-sanction-low:       #D4A843;  /* ámbar — apercibimientos, multas menores */
  --color-sanction-low-bg:    #FDF6E3;
  --color-sanction-medium:    #E06B56;  /* coral — multas significativas */
  --color-sanction-medium-bg: #FDEEE9;
  --color-sanction-high:      #C93B3B;  /* rojo — multas mayores, clausura, penal */
  --color-sanction-high-bg:   #FDE8E8;

  /* --- FEEDBACK --- */
  --color-success:       #2D8B55;
  --color-success-light: #E8F5EE;
  --color-error:         #C93B3B;
  --color-error-light:   #FDE8E8;

  /* --- BORDES --- */
  --color-border:        #E5E0D8;
  --color-border-light:  #F0EBE3;


  /* ─── TIPOGRAFÍA ─── */

  /* --- FAMILIAS --- */
  --font-display:  'Bricolage Grotesque', system-ui, sans-serif;  /* geométrica, con personalidad */
  --font-body:     'DM Sans', system-ui, sans-serif;              /* legible con carácter */
  --font-mono:     'JetBrains Mono', 'Fira Code', monospace;     /* para texto legal en bloques */

  /* --- ESCALA TIPOGRÁFICA (ratio 1.25) --- */
  --text-xs:    0.75rem;    /* 12px — labels, metadata */
  --text-sm:    0.875rem;   /* 14px — texto pequeño, badges */
  --text-base:  1rem;       /* 16px — cuerpo */
  --text-md:    1.125rem;   /* 18px — cuerpo grande */
  --text-lg:    1.25rem;    /* 20px — encabezados pequeños */
  --text-xl:    1.563rem;   /* 25px — encabezados de sección */
  --text-2xl:   1.953rem;   /* 31px — títulos de módulo */
  --text-3xl:   2.441rem;   /* 39px — números de módulo */
  --text-4xl:   3.052rem;   /* 49px — display grande */
  --text-hero:  3.75rem;    /* 60px — número de módulo hero */

  /* --- ALTURAS DE LÍNEA --- */
  --leading-tight:    1.15;   /* encabezados */
  --leading-snug:     1.3;    /* subtítulos */
  --leading-normal:   1.5;    /* párrafos */
  --leading-relaxed:  1.8;    /* lectura extendida, tooltips */

  /* --- PESOS --- */
  --font-normal:   400;
  --font-medium:   500;
  --font-semibold: 600;
  --font-bold:     700;
  --font-black:    900;


  /* ─── ESPACIADO ─── */
  --space-1:   0.25rem;    /*  4px */
  --space-2:   0.5rem;     /*  8px */
  --space-3:   0.75rem;    /* 12px */
  --space-4:   1rem;       /* 16px */
  --space-5:   1.25rem;    /* 20px */
  --space-6:   1.5rem;     /* 24px */
  --space-8:   2rem;       /* 32px */
  --space-10:  2.5rem;     /* 40px */
  --space-12:  3rem;       /* 48px */
  --space-16:  4rem;       /* 64px */
  --space-20:  5rem;       /* 80px */
  --space-24:  6rem;       /* 96px */

  /* --- LAYOUT --- */
  --content-width:    800px;
  --content-narrow:   600px;
  --content-wide:     1000px;
  --nav-height:       60px;
  --section-padding:  calc(var(--nav-height) + var(--space-12)) var(--space-6) var(--space-12);


  /* ─── BORDES ─── */
  --radius-sm:   6px;
  --radius-md:   10px;
  --radius-lg:   16px;
  --radius-xl:   24px;
  --radius-full: 9999px;


  /* ─── SOMBRAS (tintadas cálidas, nunca negro puro) ─── */
  --shadow-sm:    0 1px 3px rgba(44, 42, 40, 0.06);
  --shadow-md:    0 4px 12px rgba(44, 42, 40, 0.08);
  --shadow-lg:    0 8px 30px rgba(44, 42, 40, 0.12);
  --shadow-xl:    0 16px 50px rgba(44, 42, 40, 0.16);
  --shadow-inner: inset 0 1px 3px rgba(44, 42, 40, 0.06);


  /* ─── ANIMACIONES ─── */
  --ease-out:      cubic-bezier(0.22, 1, 0.36, 1);
  --ease-in-out:   cubic-bezier(0.65, 0, 0.35, 1);
  --duration-fast:    150ms;
  --duration-normal:  250ms;
  --duration-slow:    400ms;
  --duration-slower:  500ms;
  --stagger-delay:    120ms;
}
```

---

## Resaltado de texto legal

Los bloques de texto legal usan fondo oscuro (`--color-bg-code`) con formateo de artículos en vez de sintaxis de código. Estos colores están inspirados en Catppuccin pero adaptados para estructura legal:

```css
/* Formateo de texto legal sobre fondo oscuro */
.legal-article-num   { color: #89B4FA; font-weight: 700; }    /* azul — número de artículo */
.legal-fraction       { color: #CBA6F7; }                      /* púrpura — marcadores de fracción (I, II, III) */
.legal-paragraph      { color: #F9E2AF; }                      /* amarillo — letras de inciso (a, b, c) */
.legal-defined-term   { color: #A6E3A1; font-style: italic; }  /* verde — términos definidos */
.legal-reference      { color: #94E2D5; }                      /* teal — referencias cruzadas a otros artículos/leyes */
.legal-emphasis       { color: #F38BA8; font-weight: 600; }    /* rosa — obligaciones/prohibiciones clave */
.legal-deadline       { color: #FAB387; font-weight: 600; }    /* durazno — fechas y períodos de tiempo */
.legal-text-base      { color: #CDD6F4; }                      /* gris claro — texto legal base */
```

**Reglas para bloques de texto legal:**
- `white-space: pre-wrap` — el texto DEBE ajustarse; barras de desplazamiento horizontal prohibidas
- `word-wrap: break-word` — respaldo para palabras largas
- `font-family: var(--font-body)` — usar fuente de cuerpo (el texto legal es prosa, no código)
- `font-size: var(--text-sm)` — ligeramente más pequeño que el texto de cuerpo
- `line-height: var(--leading-relaxed)` — espaciado generoso para legibilidad
- `padding: var(--space-6)` — padding cómodo
- `border-radius: var(--radius-md)` — esquinas redondeadas consistentes
- `overflow: visible` — NUNCA `overflow: hidden` (los tooltips necesitan escapar)

---

## Indicador de severidad de sanciones

Badge reutilizable para comunicar visualmente la severidad de sanciones. Se usa dentro de tarjetas de obligación, ítems del checklist y entradas del timeline.

```css
.sanction-severity {
  font-size: var(--text-xs);
  letter-spacing: 2px;
  font-weight: 700;
  display: inline-block;
  padding: var(--space-1) var(--space-2);
  border-radius: var(--radius-full);
  cursor: pointer;  /* tiene tooltip */
}
.severity-low {
  color: var(--color-sanction-low);
  background: var(--color-sanction-low-bg);
}
.severity-medium {
  color: var(--color-sanction-medium);
  background: var(--color-sanction-medium-bg);
}
.severity-high {
  color: var(--color-sanction-high);
  background: var(--color-sanction-high-bg);
}
```

**Tres niveles:**
- **Baja** (● ámbar): apercibimientos, medidas correctivas, multas menores
- **Media** (●● coral): multas significativas, suspensión temporal
- **Alta** (●●● rojo): multas mayores, clausura permanente, responsabilidad penal

---

## Módulos y navegación

```css
/* Scroll-snap para módulos */
.guide-container {
  scroll-snap-type: y proximity;  /* NUNCA mandatory */
  overflow-y: auto;
  height: 100vh;
}

.module {
  min-height: 100dvh;            /* fallback: 100vh */
  scroll-snap-align: start;
  display: flex;
  flex-direction: column;
  padding: var(--section-padding);
}

/* Fondos alternados para módulos */
.module:nth-child(odd)  { background: var(--color-bg); }
.module:nth-child(even) { background: var(--color-bg-warm); }
```

**Navegación:**
- Barra de progreso superior que se llena conforme el usuario avanza
- Indicadores de punto (visitado/actual) en el borde derecho
- Navegación con flechas del teclado (↑/↓ o ←/→)
- Soporte táctil para swipe vertical

```css
/* Barra de progreso */
.progress-bar {
  position: fixed;
  top: 0;
  left: 0;
  height: 3px;
  background: var(--color-accent);
  transition: width var(--duration-normal) var(--ease-out);
  z-index: 100;
}

/* Indicadores de punto */
.nav-dots {
  position: fixed;
  right: var(--space-4);
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
  z-index: 100;
}

.nav-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: var(--color-border);
  transition: all var(--duration-normal) var(--ease-out);
  cursor: pointer;
}

.nav-dot.visited { background: var(--color-accent-muted); }
.nav-dot.current {
  background: var(--color-accent);
  transform: scale(1.3);
}
```

---

## Animaciones de entrada

Usa Intersection Observer para activar animaciones cuando los elementos entran en viewport:

```css
/* Fade-in desde abajo */
.animate-in {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity var(--duration-slow) var(--ease-out),
              transform var(--duration-slow) var(--ease-out);
}

.animate-in.visible {
  opacity: 1;
  transform: translateY(0);
}

/* Escalonamiento para hijos */
.stagger-children > .animate-in:nth-child(1) { transition-delay: calc(var(--stagger-delay) * 0); }
.stagger-children > .animate-in:nth-child(2) { transition-delay: calc(var(--stagger-delay) * 1); }
.stagger-children > .animate-in:nth-child(3) { transition-delay: calc(var(--stagger-delay) * 2); }
.stagger-children > .animate-in:nth-child(4) { transition-delay: calc(var(--stagger-delay) * 3); }
.stagger-children > .animate-in:nth-child(5) { transition-delay: calc(var(--stagger-delay) * 4); }
.stagger-children > .animate-in:nth-child(6) { transition-delay: calc(var(--stagger-delay) * 5); }
```

```javascript
// Intersection Observer para animaciones
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
    }
  });
}, { threshold: 0.15 });

document.querySelectorAll('.animate-in').forEach(el => observer.observe(el));
```

---

## Responsive

```css
/* Tablet */
@media (max-width: 768px) {
  :root {
    --text-hero: 2.5rem;
    --text-4xl:  2rem;
    --text-3xl:  1.75rem;
    --section-padding: calc(var(--nav-height) + var(--space-8)) var(--space-4) var(--space-8);
  }
  .nav-dots { display: none; }
}

/* Móvil */
@media (max-width: 480px) {
  :root {
    --text-hero: 2rem;
    --text-4xl:  1.75rem;
    --text-3xl:  1.5rem;
    --text-2xl:  1.25rem;
    --section-padding: calc(var(--nav-height) + var(--space-6)) var(--space-3) var(--space-6);
  }
}
```

---

## Scrollbar personalizado

```css
::-webkit-scrollbar {
  width: 8px;
}
::-webkit-scrollbar-track {
  background: var(--color-bg);
}
::-webkit-scrollbar-thumb {
  background: var(--color-border);
  border-radius: var(--radius-full);
}
::-webkit-scrollbar-thumb:hover {
  background: var(--color-text-muted);
}
```

---

## Google Fonts — enlace CDN

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:wght@400;600;700;800&family=DM+Sans:ital,wght@0,400;0,500;0,600;0,700;1,400&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
```
