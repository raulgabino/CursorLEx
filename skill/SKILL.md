---
name: reglabot
description: "Convierte cualquier ley, reglamento o norma técnica en una guía interactiva de cumplimiento personalizada por rol profesional. Un archivo HTML autocontenido con navegación por scroll, traducciones texto-legal↔lenguaje-simple, quizzes de escenarios, checklists de cumplimiento y líneas de tiempo de plazos. Usa este skill cuando alguien quiera crear una guía de cumplimiento interactiva, un tutorial regulatorio, o una explicación visual de una norma. También se activa con: 'ReglaBot', 'guía de cumplimiento', 'explica esta ley', 'qué significa esta norma para mi puesto', 'hazme un curso de esta regulación', 'compliance guide for [role]', 'interactive legal tutorial', 'teach me this regulation', 'obligaciones de esta ley', 'convierte esta ley en guía'."
---

# ReglaBot

Transforma cualquier documento legal o normativo en una guía interactiva de cumplimiento en un solo archivo HTML, personalizada para un rol profesional específico. El resultado es un archivo HTML autocontenido (sin dependencias excepto Google Fonts) que enseña qué significa la regulación para el rol del usuario a través de módulos con scroll, simulaciones de escenarios, checklists de cumplimiento y traducciones de texto legal a lenguaje simple.

---

## Bienvenida (primera ejecución)

Cuando el usuario active el skill sin especificar documento o rol, muestra:

> **Puedo convertir cualquier ley o regulación en una guía interactiva de cumplimiento personalizada para tu rol — no necesitas formación jurídica.**
>
> Necesito dos cosas:
> - **La norma** — un PDF, una URL al texto oficial, o pega el texto directamente
> - **Tu rol** — por ejemplo: "director de RRHH en empresa de 200 empleados", "oficial de datos personales", "contador independiente", "director de clínica"
>
> Ejemplos:
> - "Hazme una guía de la Ley Federal de Protección de Datos Personales para un gerente de marketing"
> - "Convierte este PDF de la NOM-035 en guía para un director de RRHH"
> - "Explica el RGPD para el CTO de una startup"
>
> Leeré la norma, filtraré lo que aplica a tu rol, y generaré una guía visual en una sola página HTML con simulaciones de escenarios, explicaciones en lenguaje simple, checklists de cumplimiento y líneas de tiempo de plazos. Todo corre en tu navegador — sin instalación.

Si el usuario proporciona una URL, obtén el contenido. Si proporciona una ruta de PDF, léelo. Si dice "este documento" o similar, busca el archivo en el directorio de trabajo actual.

---

## Para quién es esto

El alumno objetivo es un **profesional en activo** — alguien que debe cumplir una ley o regulación como parte de su trabajo pero que NO es abogado y NO tiene formación jurídica formal. Puede ser un director de RRHH que debe cumplir regulaciones laborales, un dueño de negocio navegando obligaciones fiscales, un oficial de protección de datos implementando reglas de privacidad, o un director de escuela siguiendo normas educativas.

**Asume cero formación jurídica.** Todo concepto legal — desde prescripción hasta supletoriedad, de persona moral a recurso de revisión — necesita explicarse en lenguaje simple como si el alumno nunca lo hubiera visto. Sin jerga sin definición. Sin "como usted sabe". El tono debe ser como un colega conocedor explicando las cosas tomando un café, no un abogado leyendo un escrito.

**Sus metas son prácticas, no académicas:**
- Saber **exactamente qué debe hacer** para cumplir la regulación en su rol específico
- Entender **plazos** — cuándo se debe hacer cada cosa
- Saber **qué evidencia/documentos** debe mantener
- Entender **consecuencias** del incumplimiento (sanciones, multas, penalidades)
- Poder **explicar los requisitos de cumplimiento** a su equipo o superiores
- **Detectar cuándo necesita un abogado** versus cuándo puede manejarlo solo
- **Adquirir el vocabulario de la regulación** — aprender los términos legales precisos para comunicarse con asesores legales

**NO están tratando de ser abogados.** Quieren cumplimiento regulatorio como una habilidad práctica que los protege a ellos y a su organización.

---

## Por qué funciona este enfoque

Este skill invierte la educación legal tradicional. El modelo viejo es: leer toda la ley → memorizar artículos → interpretar doctrina → eventualmente descubrir qué te aplica (la mayoría se rinde y contrata un abogado para todo). Este modelo es: **empezar con tu trabajo diario → identificar dónde la regulación toca tu rol → entender tus obligaciones específicas → aprender cómo cumplir.**

El alumno ya tiene contexto que los estudiantes de derecho no tienen — viven las situaciones que la ley regula todos los días. La guía los encuentra donde están: "¿Esos datos de clientes que recopilas cada mañana? Aquí está lo que la ley dice que debes hacer con ellos."

Cada módulo responde "¿por qué me importa?" antes de "¿qué debo hacer?" La respuesta a "¿por qué me importa?" siempre es práctica: porque este conocimiento te protege de sanciones, mantiene a tu organización en cumplimiento, y te permite tomar decisiones informadas sin correr al abogado por cada pregunta.

La restricción de archivo único es intencional: un archivo HTML significa cero configuración, se comparte instantáneamente con colegas, funciona sin internet, y fuerza decisiones de diseño ajustadas.

---

## El proceso de 4 fases

### Fase 1: Análisis del Documento

Antes de escribir HTML de la guía, entiende profundamente la regulación. Lee el documento completo, identifica su estructura, extrae las disposiciones clave, y mapea qué partes aplican al rol especificado por el usuario. La minuciosidad aquí vale la pena — mientras más precisamente mapees la regulación al rol, más útil será la guía.

**Qué extraer:**
- La **estructura** del documento (títulos, capítulos, secciones, artículos, disposiciones transitorias)
- Sección de **definiciones** — cada término definido que usa la regulación (estos se convierten en tooltips)
- **Sujetos obligados** — quién debe cumplir y en qué capacidad
- **Obligaciones específicas** — qué debe hacer cada sujeto, mapeado por artículo
- **Plazos** — fechas de cumplimiento, períodos de presentación, períodos de transición de artículos transitorios
- **Sanciones** — qué pasa por cada tipo de incumplimiento, mapeado a la obligación específica
- **Excepciones y exenciones** — quién o qué situaciones están excluidas
- **Procedimientos** — pasos para cumplimiento, reportes, notificaciones
- **Autoridades competentes** — quién supervisa el cumplimiento, quién resuelve controversias
- **Referencias cruzadas** — otras leyes o regulaciones que ésta referencia (supletoriedad)

**El filtrado por rol es crítico.** Después de extraer el panorama regulatorio completo, filtra agresivamente a lo que aplica al rol especificado. Una regulación con 200 artículos puede tener solo 30-40 relevantes para un rol específico. La guía debe enfocarse en esos y mencionar el resto solo como contexto. Si un artículo es irrelevante para el rol, córtalo. Si es tangencialmente relevante, menciónalo brevemente. Si es directamente relevante, recibe tratamiento completo.

**Descubre el propósito de la regulación tú mismo** leyendo el preámbulo, los artículos de objeto/propósito (usualmente Artículos 1-3), y la sección de definiciones. No le pidas al usuario que explique la ley — puede que tampoco la entienda. La guía debe abrir explicando qué hace esta regulación y por qué existe en lenguaje simple antes de entrar en obligaciones.

---

### Fase 2: Diseño del Currículo

Estructura la guía en 5-7 módulos. El arco siempre comienza desde lo que el alumno ya conoce (su trabajo diario) y avanza hacia lo que no conoce (lo que la ley requiere). Piensa en hacer zoom progresivo: empieza amplio con contexto, luego capa obligaciones, procedimientos, plazos y consecuencias.

| # | Módulo | Valor práctico |
|---|--------|----------------|
| 1 | **¿Qué es esta norma y por qué existe?** | Contexto: qué problema resuelve, a quién protege, cuándo entró en vigor. Abre con una situación real que el alumno reconozca — "Imagina que un cliente te pide borrar todos sus datos. ¿Qué haces?" — luego revela que la ley aborda exactamente esto. |
| 2 | **Un día normal en tu trabajo — dónde te toca esta norma** | Fundamenta la regulación en la experiencia diaria. Recorre un día laboral realista y marca cada momento donde la regulación aplica. Esto hace concreto lo abstracto. |
| 3 | **Tus obligaciones específicas** | El módulo central. Qué requiere la regulación del rol del alumno, organizado por tipo de obligación (reportes, documentación, procedimientos, capacitación, etc.). Cada obligación enlaza a su artículo fuente. |
| 4 | **Cómo cumplir — procedimientos, documentos, evidencia** | Pasos accionables. Para cada obligación del Módulo 3, explica CÓMO cumplir: qué documentos crear, qué procedimientos seguir, qué evidencia mantener. |
| 5 | **Plazos y cronograma** | Vista cronológica: qué se debe hacer cuándo. Incluye plazos iniciales de cumplimiento (de artículos transitorios), plazos recurrentes (presentaciones anuales, reportes periódicos), y plazos activados por eventos (responder dentro de X días a una queja). |
| 6 | **Qué pasa si no cumples — sanciones y consecuencias** | Para cada obligación, ¿cuál es la consecuencia del incumplimiento? Mapea sanciones a obligaciones para que el alumno entienda la severidad. Incluye sanciones formales (multas, penalidades) y consecuencias prácticas (responsabilidad, reputación). |
| 7 | **Tu checklist de cumplimiento** | Un checklist completo e interactivo de todo lo que el alumno debe hacer, organizado por prioridad y cronograma. Este es el módulo al que regresarán. |

No toda regulación necesita los 7. Una norma simple puede necesitar solo 5 módulos. Una ley federal compleja puede necesitar 8 (dividiendo el Módulo 3 en sub-temas). Adapta el arco a la complejidad de la regulación.

**Principio clave:** Cada módulo debe conectar con una acción práctica — algo que el alumno debe hacer, un documento que debe crear, un plazo que debe cumplir, o un riesgo que debe entender. Si un módulo no ayuda al alumno a HACER algo o EVITAR algo, córtalo o replantéalo.

**Cada módulo debe contener:**
- 3-6 pantallas
- Al menos una traducción texto-legal↔lenguaje-simple
- Al menos un elemento interactivo (quiz de escenario, flujo de cumplimiento, ítem del checklist, segmento del cronograma)
- Una o dos cajas de "dato clave" con sabiduría práctica de cumplimiento
- Una metáfora que fundamente el concepto legal en situaciones laborales cotidianas — pero NUNCA reusar la misma metáfora entre módulos, y NUNCA usar metáforas genéricas. Elige metáforas del contexto profesional específico del alumno.

**NO presentes el currículo para aprobación — simplemente constrúyelo.**

---

### Fase 3: Construir la Guía

**Orden de construcción:**
1. Cimiento HTML + sistema CSS completo + navegación + scroll-snap
2. Un módulo a la vez (verifica cada uno antes del siguiente)
3. Pasada de pulido para transiciones/móvil/consistencia

**Reglas críticas de implementación:**
- Archivo autocontenido — solo Google Fonts como dependencia CDN externa
- `scroll-snap-type: y proximity` (NO obligatorio — no usar `mandatory`)
- Solo animar `transform` y `opacity` (animaciones amigables con GPU)
- `min-height: 100dvh` con fallback `100vh` para secciones
- Soporte táctil + navegación por teclado + atributos ARIA
- Envolver JS en IIFE; usar `passive: true` en scroll; throttle con `requestAnimationFrame`
- Construir el checklist de cumplimiento como componente funcional — debe persistir estado de checkboxes en localStorage para que el usuario pueda regresar
- Construir la línea de tiempo de plazos como componente visual mostrando hitos cronológicos de cumplimiento
- Breakpoints responsivos: tablet (768px) y móvil (480px)

---

### Fase 4: Revisión y apertura

Después de generar el archivo HTML de la guía, ábrelo en el navegador para que el usuario lo revise. Recorre lo que se construyó y pide retroalimentación sobre precisión del contenido, completitud y diseño.

---

## Filosofía de contenido

### Mostrar, no decir (agresivamente visual)

- Máximo 2-3 oraciones por bloque de texto
- Nunca más ancho que el ancho de contenido Y más alto que ~4 líneas
- Mínimo 50% visual por pantalla

**Convierte texto a elementos visuales:**

| Si tienes... | Conviértelo en... |
|---|---|
| Una lista de 3+ elementos | Tarjetas con íconos y badges |
| Una secuencia de pasos | Diagrama de flujo o tarjetas numeradas |
| Relaciones entre entidades regulatorias | Diagrama de ecosistema regulatorio animado |
| Responsabilidades de documentos | Árbol de documentos visual con anotaciones |
| Un artículo que crea obligaciones | **Tarjeta de obligación con badge de plazo e indicador de severidad** |
| Un proceso descrito en la regulación | **Diagrama de flujo de cumplimiento** (quién hace qué, en qué orden, con qué documentos) |
| Explicación de qué dice un artículo | **Bloque de traducción texto-legal↔lenguaje-simple** (NO un párrafo explicativo) |
| Comparación de dos enfoques | Columnas lado a lado |

**Espacio para respirar:** Espaciado generoso (`--space-8` a `--space-12`); alterna visuales de ancho completo con texto estrecho; mínimo un "visual héroe" por módulo.

---

### Traducciones: Texto Legal ↔ Lenguaje Simple

Cada artículo relevante recibe una traducción lado a lado. Panel izquierdo: el texto legal original con número de artículo y formato. Panel derecho: explicación en lenguaje simple de qué significa el artículo para el rol del alumno.

**Crítico: Usa el texto legal original EXACTO tal cual.** Nunca parafrasees, abrevies o "simplifiques" el texto legal del lado izquierdo. El alumno debe poder encontrar el mismo texto exacto en el documento oficial. El lado de lenguaje simple hace la simplificación.

**Crítico: Sin barras de desplazamiento horizontal en texto legal.** Usa `white-space: pre-wrap` y `word-wrap: break-word`.

**Elige artículos naturalmente concisos.** Cuando un artículo es muy largo, muestra las fracciones o párrafos más relevantes para el rol en lugar de recortar el artículo.

---

### Un concepto por pantalla

No amontones. Si hay demasiada información para una pantalla, agrega pantallas en vez de sobrecargar.

---

### Metáforas primero, luego realidad

Introduce cada concepto legal nuevo con una metáfora del contexto laboral del alumno. Luego fundamenta inmediatamente: "En la regulación, esto se ve en el Artículo 25..." La metáfora construye intuición; la cita del artículo la fundamenta en la realidad.

**Crítico: No reciclar metáforas.** NO uses "tribunal" o "juicio" para todo. Cada concepto merece su propia metáfora que se sienta natural para esa idea específica y para el contexto profesional del alumno:
- La prescripción es como la fecha de caducidad de una garantía
- La supletoriedad es como un número telefónico de respaldo
- Un fideicomiso es como una caja de seguridad administrada por un tercero neutral
- La portabilidad de datos es como transferir tu número telefónico a otra compañía
- El aviso de privacidad es como la etiqueta de ingredientes de un producto

Elige la metáfora que haga click para alguien en el rol específico del alumno.

---

### Aprender por escenario

Sigue lo que realmente pasa cuando ocurre una situación realista en el trabajo del alumno — traza el proceso regulatorio de principio a fin. "Un cliente llama y exige que borres todos sus datos personales. Aquí está lo que la regulación dice que debes hacer, paso a paso..." Esto funciona porque el alumno ya ha vivido situaciones así — ahora está viendo el marco legal detrás de sus decisiones diarias.

---

### Cajas de dato clave

Usa para insights universales de cumplimiento. Inyecta humor natural. Dale personalidad a las explicaciones. Tres variantes:
- `callout-accent`: Insight de cumplimiento ("Dato clave: Este artículo es el que más sanciones genera en la práctica")
- `callout-info`: Referencia útil ("Bueno saber: La autoridad publica una guía práctica en su sitio web")
- `callout-warning`: Error común de cumplimiento ("Ojo: Muchas empresas confunden 'consentimiento tácito' con 'no pedir consentimiento'")

---

### Tooltips de glosario (ningún término sin definir)

Cada término legal recibe un tooltip con subrayado punteado en su primer uso en cada módulo. El alumno nunca debe necesitar salir de la página para buscar un término en Google.

**Sé extremadamente agresivo con los tooltips.** Términos para tooltippear:
- **Términos legales:** prescripción, caducidad, supletoriedad, persona moral, persona física, sujeto obligado, acto jurídico, responsable, encargado, titular, tratamiento, etc.
- **Términos procesales:** recurso de revisión, amparo, medio de impugnación, notificación personal, requerimiento, etc.
- **Nombres de instituciones:** INAI, PROFECO, COFEPRIS, SAT, IMSS, etc. — con qué hacen realmente
- **Tipos de documentos:** aviso de privacidad, dictamen, constancia, acta constitutiva, póliza de fianza, etc.
- **Cualquier término** que no aparecería en una conversación cotidiana en el lugar de trabajo del alumno

**El vocabulario ES el aprendizaje.** Uno de los objetivos clave es que los alumnos adquieran el vocabulario legal preciso que necesitan para comunicarse con asesores legales, auditores y reguladores. Cada tooltip debe enseñar el término de forma que ayude al alumno a USARLO — por ejemplo: "**Prescripción** es la fecha de caducidad legal de una obligación o derecho — como una garantía que se vence. Después del período de prescripción, la autoridad ya no puede sancionarte por esa violación específica. Cuando hables con tu abogado, preguntarías '¿Esta obligación ya prescribió?'"

**Implementación de tooltips:**
- Subrayado punteado en primer uso por módulo
- Definición de 1-2 oraciones en lenguaje simple
- Usar `cursor: pointer` (no `cursor: help`)
- Usar `position: fixed` con append a `document.body` (previene recorte por contenedores con overflow)
- Calcular posición con `getBoundingClientRect()`

---

### Quizzes que prueban decisiones de cumplimiento

**Qué evaluar (en orden de valor):**
1. **Escenarios "¿Qué harías?"** — Presenta una situación realista que el alumno podría enfrentar y pide aplicar lo aprendido. Ej: "Un empleado te pide transferir sus datos personales a un competidor que lo está contratando. ¿Qué debes hacer según la regulación?"
2. **Identificación de violaciones** — "Tu empresa ha estado haciendo X durante el último año. Según lo que aprendiste, ¿es esto una violación? ¿Qué deberías hacer ahora?"
3. **Escenarios de plazos** — "Un titular de datos presenta una solicitud de acceso el 15 de marzo. ¿Cuál es la fecha límite para responder?"
4. **Escenarios de documentación** — "Un auditor pide prueba de cumplimiento del Artículo X. ¿Qué documentos deberías tener listos?"

**Qué NO evaluar:**
- Definiciones legales ("¿Qué significa persona moral?") — para eso están los tooltips
- Recordar números de artículos ("¿Qué artículo cubre sanciones?") — nadie memoriza números de artículos
- Doctrina o interpretación legal — esto no es la facultad de derecho
- Cualquier cosa que se pueda responder haciendo scroll hacia arriba

**Tono de quizzes:** Alentador. No punitivo. Respuesta incorrecta → explicación educativa. Respuesta correcta → refuerzo breve. Un quiz por módulo al final. 3-5 preguntas de escenario por quiz.

---

## Identidad de diseño

**Estética:** Cuaderno de cumplimiento — cálido, invitante, profesional, distintivo.

**Elementos requeridos:**
- Paleta cálida (off-white papel envejecido `#FAF7F2`, grises cálidos; SIN blancos fríos ni azules)
- Color de acento profesional (teal `#2A7B9B` por defecto; alternativas: vermillion, coral, ámbar, verde bosque; NUNCA degradados morados)
- Fuente display con personalidad (Bricolage Grotesque o geométrica bold; NUNCA Inter/Roboto/Arial/Space Grotesk)
- Sans-serif limpia para cuerpo (DM Sans)
- JetBrains Mono para texto legal en bloques oscuros
- Espaciado generoso; máximo 3-4 párrafos cortos por pantalla
- Fondos alternados (módulos pares/impares)
- Bloques de texto legal oscuros (estilo Catppuccin sobre `#1E1E2E`) con formateo de artículos
- Sombras cálidas sutiles (nunca negras)

**Lee `references/design-system.md` antes de escribir cualquier CSS.**
**Lee `references/interactive-elements.md` antes de construir cualquier elemento interactivo.**

---

## Errores comunes a evitar

### 1. Recorte de tooltips
Los tooltips con `position: fixed` deben agregarse a `document.body` y posicionarse con `getBoundingClientRect()`. NUNCA pongas tooltips dentro de contenedores con `overflow: hidden` — se recortarán.

### 2. Pocos tooltips
En caso de duda, agrega tooltip. Es mejor sobre-tooltippear que dejar términos sin definir. Si algo te haría pausar para Googlear, necesita tooltip.

### 3. Muros de texto
Cada pantalla debe ser mínimo 50% visual. Si tienes más de 3 oraciones seguidas, convierte a elemento visual. Usa la tabla de conversión texto→visual arriba.

### 4. Metáforas recicladas
Cada módulo necesita una metáfora única e inevitable. NUNCA uses "tribunal" como metáfora por defecto. Si no se te ocurre una buena metáfora, piensa en el trabajo diario del alumno — ¿qué proceso laboral se parece al concepto legal?

### 5. Texto legal modificado
NUNCA parafrasees, abrevies o "limpies" el texto legal en el panel izquierdo de los bloques de traducción. El alumno debe poder encontrar el mismo texto exacto en el documento oficial. El panel derecho hace la simplificación.

### 6. Quizzes de memoria
Preguntar "¿Qué significa prescripción?" o "¿Qué artículo cubre sanciones?" — eso evalúa memorización, no comprensión. Cada pregunta de quiz debe presentar un escenario laboral realista y pedir al alumno tomar una decisión de cumplimiento.

### 7. Scroll-snap obligatorio
Usar solo `proximity`. NUNCA `mandatory` — los usuarios pueden quedar atrapados.

### 8. Degradación de calidad por módulo
Construye un módulo a la vez. Verifica cada uno antes de empezar el siguiente. Construir todos simultáneamente degrada la calidad.

### 9. Falta de interactividad
Cada módulo necesita al menos un elemento interactivo — quiz, simulación, flujo animado, o componente del checklist.

### 10. Artículos irrelevantes al rol
El error más común específico de ReglaBot. Una ley federal puede tener 200 artículos pero solo 30-40 son relevantes para un director de RRHH. La guía debe filtrar agresivamente. Si un artículo solo aplica a la autoridad competente (no al sujeto regulado), córtalo. Si aplica a otro tipo de organización, córtalo. En caso de duda, menciónalo brevemente en una caja de dato clave en vez de darle una pantalla completa.

### 11. Falta de contextualización al rol
Cada obligación debe explicarse en términos del rol específico del alumno. No digas solo "el responsable debe mantener un registro de tratamientos." Di "Como oficial de datos personales en tu empresa, TÚ debes mantener un registro de cada tipo de dato personal que tu empresa procesa — aquí está cómo se ve ese documento y dónde guardarlo."

### 12. Ignorar artículos transitorios
Los artículos transitorios contienen plazos críticos de cumplimiento y reglas de transición. Determinan CUÁNDO entran en vigor las obligaciones, qué períodos de gracia existen, y qué pasa con regímenes regulatorios anteriores. Nunca los saltes — frecuentemente contienen la información más sensible al tiempo.

### 13. Sanciones sin contexto
Listar sanciones sin mapearlas a obligaciones específicas es inútil. Cada sanción debe vincularse a la obligación que la hace cumplir, para que el alumno entienda "si no hago X (obligación), entonces pasa Y (sanción)."

---

## Archivos de referencia

- **`references/design-system.md`** — Propiedades CSS personalizadas, paleta de colores, escala tipográfica, sistema de espaciado, sombras, animaciones, estilo de scrollbar, estilo de bloques de texto legal. Lee esto antes de escribir cualquier CSS.
- **`references/interactive-elements.md`** — Patrones de implementación para cada elemento interactivo: quizzes de escenario, traducciones legales, diagramas de flujo de cumplimiento, tarjetas de obligación, checklists de cumplimiento, líneas de tiempo de plazos, indicadores de severidad de sanciones, cajas de dato clave, árboles de documentos, tooltips. Lee esto antes de construir cualquier elemento interactivo.
