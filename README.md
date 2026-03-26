# ReglaBot

**Convierte cualquier ley, reglamento o norma en una guia interactiva de cumplimiento personalizada por rol profesional.**

ReglaBot es un skill para [Claude Code](https://claude.ai/claude-code) que transforma documentos legales en archivos HTML autocontenidos e interactivos. El usuario proporciona un documento normativo y su rol profesional, y ReglaBot genera una guia visual con traducciones legal-a-lenguaje-simple, quizzes de escenarios, checklists de cumplimiento y lineas de tiempo de plazos.

---

## Como funciona

```
Documento legal + Rol profesional = Guia HTML interactiva
(PDF, URL o texto)   (ej: "analista      (archivo unico,
                      en movilidad")      sin dependencias)
```

### Las 4 fases

1. **Analisis del documento** — Lee la norma completa, extrae estructura, definiciones, obligaciones, plazos, sanciones. Filtra agresivamente por rol.
2. **Diseno del curriculo** — Estructura 5-7 modulos con arco narrativo: contexto -> dia normal -> obligaciones -> como cumplir -> plazos -> sanciones -> checklist.
3. **Construccion** — Genera un HTML autocontenido con scroll-snap, componentes interactivos, tooltips legales y checklist con persistencia en localStorage.
4. **Revision** — Abre en navegador para revision y feedback del usuario.

---

## Componentes interactivos (20)

| # | Componente | Descripcion |
|---|-----------|-------------|
| 1 | Traduccion Legal <-> Simple | Texto legal exacto a la izquierda, explicacion simple a la derecha |
| 2 | Quiz de Escenarios | Preguntas con situaciones laborales realistas |
| 3 | Emparejar Obligaciones | Drag-and-drop para asociar obligaciones con responsables |
| 4 | Simulacion de Escenario | Conversacion tipo chat entre actores regulatorios |
| 5 | Flujo de Cumplimiento | Animacion paso a paso de procedimientos |
| 6 | Diagrama del Ecosistema | Mapa interactivo de actores regulatorios |
| 7 | Capas de Cumplimiento | Tabs: "Que dice la ley" / "Que significa" / "Como cumplir" |
| 8 | Detecta la Violacion | Click en la linea que viola la regulacion |
| 9 | Quiz de Decision | Escenarios de cumplimiento con razonamiento detallado |
| 10 | Cajas de Dato Clave | Callouts: insight, referencia util, error comun |
| 11 | Tarjetas de Obligacion | Cards con plazo, articulo fuente e indicador de severidad |
| 12 | Diagramas de Procedimiento | Flujos horizontales con pasos numerados |
| 13 | Badges de Requisitos | Tokens anotados para tipos de documentos |
| 14 | Tooltips Legales | Definiciones en lenguaje simple con posicion fija |
| 15 | Arbol de Documentos | Jerarquia visual de documentos requeridos |
| 16 | Filas de Icono + Label | Listados con iconos circulares y descripcion |
| 17 | Tarjetas de Pasos | Cards secuenciales para procedimientos |
| **18** | **Checklist Interactivo** | **Checkboxes con persistencia en localStorage** |
| **19** | **Linea de Tiempo** | **Timeline vertical de plazos cronologicos** |
| **20** | **Indicador de Severidad** | **Badge: baja/media/alta con colores semanticos** |

Los componentes 18-20 son nuevos, creados especificamente para ReglaBot.

---

## Estructura del repositorio

```
CursorLEx/
├── README.md                              # Este archivo
├── skill/
│   ├── SKILL.md                           # Skill principal (instrucciones completas)
│   └── references/
│       ├── design-system.md               # Tokens CSS, paleta, tipografia, animaciones
│       └── interactive-elements.md        # 20 componentes con HTML/CSS/JS
└── examples/                              # Guias generadas (despues de usar el skill)
    └── .gitkeep
```

---

## Requisitos previos

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) instalado y funcionando
- Una suscripcion activa a Claude (Pro, Team o Enterprise)
- Terminal con acceso a bash/zsh

### Instalar Claude Code

Si aun no tienes Claude Code:

```bash
# macOS / Linux
npm install -g @anthropic-ai/claude-code

# Verificar instalacion
claude --version
```

> Para mas detalles, consulta la [documentacion oficial de Claude Code](https://docs.anthropic.com/en/docs/claude-code).

---

## Instalacion de ReglaBot

### Paso 1: Clona el repositorio

```bash
git clone https://github.com/tu-usuario/CursorLEx.git
cd CursorLEx
```

### Paso 2: Instala el skill (elige una opcion)

#### Opcion A: Skill local (solo en este proyecto)

Instala el skill para que funcione solo dentro de este directorio:

```bash
mkdir -p .claude/skills/reglabot/references

cp skill/SKILL.md .claude/skills/reglabot/SKILL.md
cp skill/references/design-system.md .claude/skills/reglabot/references/design-system.md
cp skill/references/interactive-elements.md .claude/skills/reglabot/references/interactive-elements.md
```

#### Opcion B: Skill global (disponible en cualquier proyecto)

Instala el skill para que funcione desde cualquier directorio:

```bash
mkdir -p ~/.claude/skills/reglabot/references

cp skill/SKILL.md ~/.claude/skills/reglabot/SKILL.md
cp skill/references/design-system.md ~/.claude/skills/reglabot/references/design-system.md
cp skill/references/interactive-elements.md ~/.claude/skills/reglabot/references/interactive-elements.md
```

### Paso 3: Verifica la instalacion

Abre Claude Code en el directorio donde instalaste el skill:

```bash
claude
```

Escribe `ReglaBot` y deberia activarse mostrando el mensaje de bienvenida.

---

## Uso

### Inicio rapido

Abre Claude Code y escribe:

```
ReglaBot
```

El skill te pedira dos cosas:
1. **La norma** — un PDF, una URL al texto oficial, o pega el texto directamente
2. **Tu rol** — descripcion de tu puesto profesional

### Ejemplos de prompts

```
Hazme una guia de cumplimiento de la Ley Federal de Proteccion de Datos
Personales para un gerente de marketing
```

```
Convierte este PDF de la NOM-035 en guia para un director de RRHH
```

```
Explica el RGPD para el CTO de una startup
```

```
Guia de cumplimiento del Reglamento de Movilidad de Nuevo Leon
para un analista en movilidad
```

### Tambien puedes pasar un archivo directamente

```bash
# Si tienes un PDF de la norma en tu directorio:
claude "ReglaBot: hazme una guia de cumplimiento de este PDF para un contador independiente" --file mi-norma.pdf
```

### Resultado

ReglaBot genera un **archivo HTML unico** (sin dependencias excepto Google Fonts) que puedes:

- Abrir en cualquier navegador
- Compartir por correo o chat (es un solo archivo)
- Usar sin internet (despues de la primera carga)
- El checklist de cumplimiento guarda tu progreso en el navegador (localStorage)

---

## Ejemplo: flujo completo paso a paso

```bash
# 1. Clona e instala
git clone https://github.com/tu-usuario/CursorLEx.git
cd CursorLEx
mkdir -p .claude/skills/reglabot/references
cp skill/SKILL.md .claude/skills/reglabot/SKILL.md
cp skill/references/*.md .claude/skills/reglabot/references/

# 2. Abre Claude Code
claude

# 3. Dentro de Claude Code, escribe:
#    "Hazme una guia de la NOM-035 para un director de RRHH"

# 4. ReglaBot analiza la norma, genera el HTML y lo abre en tu navegador

# 5. El archivo generado queda en tu directorio de trabajo
#    (ejemplo: guia-nom035-rrhh.html)
```

---

## Sistema de diseno

- **Paleta calida:** off-white papel envejecido (#FAF7F2), sin blancos frios
- **Acento teal institucional:** #2A7B9B (confianza profesional)
- **Tipografia:** Bricolage Grotesque (display) + DM Sans (cuerpo) + JetBrains Mono (texto legal)
- **Severidad de sanciones:** ambar (baja) / coral (media) / rojo (alta)
- **Responsive:** tablet (768px) y movil (480px)

---

## Inspiracion

Este proyecto esta basado en [codebase-to-course](https://github.com/nichochar/codebase-to-course) de Nicholas Charriere, que convierte repositorios de codigo en cursos interactivos. ReglaBot adapta el mismo concepto al dominio legal: en vez de codigo, lee normas; en vez de traducciones codigo-ingles, hace traducciones legal-simple; en vez de quizzes de arquitectura, hace quizzes de cumplimiento.

---

## Licencia

MIT
