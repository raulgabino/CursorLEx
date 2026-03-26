# Elementos Interactivos — ReglaBot

Patrones de implementación para los 20 componentes interactivos de la guía de cumplimiento. Cada sección incluye estructura HTML, estilos CSS clave y comportamiento JavaScript. Consulta `design-system.md` para tokens y propiedades CSS.

---

## 1. Bloques de Traducción: Texto Legal ↔ Lenguaje Simple

El componente estrella de ReglaBot. Muestra el texto legal original exacto a la izquierda y una explicación en lenguaje simple a la derecha.

```html
<div class="translation-block">
  <div class="translation-panel translation-legal">
    <div class="translation-label">TEXTO LEGAL</div>
    <div class="legal-content">
      <span class="legal-article-num">Artículo 16.</span>
      <span class="legal-text-base">El aviso de privacidad deberá contener, al menos, la siguiente información:</span>
      <br>
      <span class="legal-fraction">I.</span>
      <span class="legal-text-base">La identidad y domicilio del </span>
      <span class="legal-defined-term">responsable</span>
      <span class="legal-text-base"> que los recaba;</span>
    </div>
  </div>
  <div class="translation-panel translation-simple">
    <div class="translation-label">EN PALABRAS SIMPLES</div>
    <div class="simple-content">
      <div class="simple-line">
        <span class="simple-marker">→</span>
        <span>Tu aviso de privacidad DEBE incluir como mínimo estos datos:</span>
      </div>
      <div class="simple-line">
        <span class="simple-marker">→</span>
        <span>Primero: el nombre de tu empresa y su dirección física — para que la gente sepa quién tiene sus datos</span>
      </div>
    </div>
  </div>
</div>
```

```css
.translation-block {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--space-1);
  border-radius: var(--radius-lg);
  overflow: visible;  /* NUNCA hidden — los tooltips necesitan escapar */
  margin: var(--space-6) 0;
}

.translation-panel {
  padding: var(--space-6);
}

.translation-legal {
  background: var(--color-bg-code);
  color: var(--legal-text-base, #CDD6F4);
  font-family: var(--font-body);  /* prosa, no monoespaciada */
  font-size: var(--text-sm);
  line-height: var(--leading-relaxed);
  white-space: pre-wrap;
  word-wrap: break-word;
  border-radius: var(--radius-lg) 0 0 var(--radius-lg);
}

.translation-simple {
  background: var(--color-bg-card);
  border: 1px solid var(--color-border-light);
  font-family: var(--font-body);
  font-size: var(--text-base);
  line-height: var(--leading-normal);
  border-radius: 0 var(--radius-lg) var(--radius-lg) 0;
}

.translation-label {
  font-family: var(--font-display);
  font-size: var(--text-xs);
  font-weight: var(--font-bold);
  letter-spacing: 0.1em;
  text-transform: uppercase;
  margin-bottom: var(--space-4);
  opacity: 0.6;
}

.translation-legal .translation-label { color: var(--color-text-inverse); }
.translation-simple .translation-label { color: var(--color-text-secondary); }

.simple-line {
  display: flex;
  gap: var(--space-2);
  margin-bottom: var(--space-3);
}

.simple-marker {
  color: var(--color-accent);
  font-weight: var(--font-bold);
  flex-shrink: 0;
}

/* Responsive: apilar en móvil */
@media (max-width: 768px) {
  .translation-block { grid-template-columns: 1fr; }
  .translation-legal { border-radius: var(--radius-lg) var(--radius-lg) 0 0; }
  .translation-simple { border-radius: 0 0 var(--radius-lg) var(--radius-lg); }
}
```

**Reglas:**
- El texto legal del panel izquierdo debe ser EXACTO — nunca parafrasear
- Elige artículos naturalmente concisos (5-15 líneas)
- La explicación del lado derecho debe dirigirse al alumno directamente ("tu empresa", "tú debes")

---

## 2. Quiz de Cumplimiento por Escenarios

Quiz de opción múltiple con retroalimentación inmediata. Las preguntas siempre presentan un escenario laboral realista.

```html
<div class="quiz-container" data-quiz="mod3">
  <div class="quiz-header">
    <h3 class="quiz-title">Ponte a prueba</h3>
    <div class="quiz-progress">Pregunta <span class="quiz-current">1</span> de <span class="quiz-total">4</span></div>
  </div>

  <div class="quiz-question active" data-question="1">
    <div class="quiz-scenario">
      <p class="quiz-scenario-context">Eres el director de RRHH. Un ex-empleado te envía un correo exigiendo que elimines todos sus datos personales de los sistemas de la empresa.</p>
      <p class="quiz-scenario-question">Según lo que aprendiste sobre las obligaciones de cancelación, ¿qué debes hacer?</p>
    </div>

    <div class="quiz-options">
      <button class="quiz-option" data-correct="false">
        <span class="quiz-option-letter">A</span>
        <span class="quiz-option-text">Eliminar todos los datos inmediatamente para cumplir con la solicitud</span>
      </button>
      <button class="quiz-option" data-correct="true">
        <span class="quiz-option-letter">B</span>
        <span class="quiz-option-text">Acusar recibo en 5 días, evaluar si hay obligación legal de conservación, y responder en 20 días</span>
      </button>
      <button class="quiz-option" data-correct="false">
        <span class="quiz-option-letter">C</span>
        <span class="quiz-option-text">Ignorar la solicitud porque ya no es empleado</span>
      </button>
      <button class="quiz-option" data-correct="false">
        <span class="quiz-option-letter">D</span>
        <span class="quiz-option-text">Remitirlo al abogado sin responder directamente</span>
      </button>
    </div>

    <div class="quiz-feedback" hidden>
      <div class="quiz-feedback-correct">
        <span class="quiz-feedback-icon">✓</span>
        <p><strong>¡Exacto!</strong> Debes acusar recibo dentro de los primeros 5 días y resolver la solicitud en máximo 20 días. Pero ojo: hay datos que estás OBLIGADO a conservar (como registros fiscales y laborales), así que no puedes borrar todo.</p>
      </div>
      <div class="quiz-feedback-incorrect">
        <span class="quiz-feedback-icon">✕</span>
        <p><strong>No exactamente.</strong> La ley establece un procedimiento específico: acusar recibo en 5 días, evaluar la procedencia (algunos datos DEBEN conservarse por obligación legal), y responder en 20 días. Eliminar todo sin evaluar o ignorar la solicitud son ambos incumplimientos.</p>
      </div>
    </div>
  </div>
  <!-- más preguntas... -->
</div>
```

```css
.quiz-container {
  background: var(--color-bg-card);
  border-radius: var(--radius-lg);
  padding: var(--space-8);
  box-shadow: var(--shadow-md);
  margin: var(--space-8) 0;
}

.quiz-scenario {
  background: var(--color-accent-light);
  border-left: 4px solid var(--color-accent);
  padding: var(--space-4) var(--space-5);
  border-radius: 0 var(--radius-md) var(--radius-md) 0;
  margin-bottom: var(--space-6);
}

.quiz-scenario-context {
  color: var(--color-text-secondary);
  font-size: var(--text-sm);
  margin-bottom: var(--space-2);
}

.quiz-scenario-question {
  color: var(--color-text);
  font-weight: var(--font-semibold);
}

.quiz-option {
  display: flex;
  align-items: flex-start;
  gap: var(--space-3);
  width: 100%;
  padding: var(--space-4);
  margin-bottom: var(--space-2);
  border: 2px solid var(--color-border);
  border-radius: var(--radius-md);
  background: transparent;
  cursor: pointer;
  text-align: left;
  font-family: var(--font-body);
  font-size: var(--text-base);
  transition: border-color var(--duration-fast) var(--ease-out),
              background var(--duration-fast) var(--ease-out);
}

.quiz-option:hover { border-color: var(--color-accent); }
.quiz-option.selected-correct {
  border-color: var(--color-success);
  background: var(--color-success-light);
}
.quiz-option.selected-incorrect {
  border-color: var(--color-error);
  background: var(--color-error-light);
}

.quiz-option-letter {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 28px;
  height: 28px;
  border-radius: 50%;
  background: var(--color-accent-light);
  color: var(--color-accent);
  font-weight: var(--font-bold);
  font-size: var(--text-sm);
  flex-shrink: 0;
}

.quiz-feedback {
  margin-top: var(--space-4);
  padding: var(--space-4);
  border-radius: var(--radius-md);
}

.quiz-feedback-correct { background: var(--color-success-light); color: var(--color-success); }
.quiz-feedback-incorrect { background: var(--color-error-light); color: var(--color-error); }
```

```javascript
// Lógica de quiz
document.querySelectorAll('.quiz-option').forEach(btn => {
  btn.addEventListener('click', function() {
    const question = this.closest('.quiz-question');
    if (question.classList.contains('answered')) return;
    question.classList.add('answered');

    const isCorrect = this.dataset.correct === 'true';
    this.classList.add(isCorrect ? 'selected-correct' : 'selected-incorrect');

    // Mostrar la correcta si eligió mal
    if (!isCorrect) {
      question.querySelector('[data-correct="true"]').classList.add('selected-correct');
    }

    // Mostrar feedback
    const feedback = question.querySelector('.quiz-feedback');
    feedback.hidden = false;
    const correctDiv = feedback.querySelector('.quiz-feedback-correct');
    const incorrectDiv = feedback.querySelector('.quiz-feedback-incorrect');
    correctDiv.hidden = !isCorrect;
    incorrectDiv.hidden = isCorrect;
  });
});
```

---

## 3. Emparejar Obligaciones (Drag-and-Drop)

Ejercicio de arrastrar y soltar para emparejar obligaciones con responsables, o sanciones con violaciones.

```html
<div class="match-container">
  <div class="match-items" role="list" aria-label="Obligaciones para emparejar">
    <div class="match-item" draggable="true" data-match="a" role="listitem">
      Mantener registro de tratamiento de datos
    </div>
    <div class="match-item" draggable="true" data-match="b" role="listitem">
      Publicar aviso de privacidad
    </div>
    <div class="match-item" draggable="true" data-match="c" role="listitem">
      Responder solicitudes ARCO
    </div>
  </div>

  <div class="match-targets" role="list" aria-label="Áreas responsables">
    <div class="match-target" data-accept="a" role="listitem">
      <span class="match-target-label">Oficial de Datos Personales</span>
      <div class="match-dropzone" aria-dropeffect="move">Arrastra aquí</div>
    </div>
    <div class="match-target" data-accept="b" role="listitem">
      <span class="match-target-label">Área de Comunicación</span>
      <div class="match-dropzone" aria-dropeffect="move">Arrastra aquí</div>
    </div>
    <div class="match-target" data-accept="c" role="listitem">
      <span class="match-target-label">RRHH + Legal</span>
      <div class="match-dropzone" aria-dropeffect="move">Arrastra aquí</div>
    </div>
  </div>
</div>
```

```css
.match-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--space-8);
  margin: var(--space-6) 0;
}

.match-item {
  padding: var(--space-3) var(--space-4);
  background: var(--color-accent-light);
  border: 2px solid var(--color-accent);
  border-radius: var(--radius-md);
  cursor: grab;
  font-size: var(--text-sm);
  font-weight: var(--font-medium);
  transition: transform var(--duration-fast) var(--ease-out),
              box-shadow var(--duration-fast) var(--ease-out);
  margin-bottom: var(--space-2);
}

.match-item:active { cursor: grabbing; }
.match-item.dragging { opacity: 0.5; transform: scale(0.95); }

.match-target {
  margin-bottom: var(--space-3);
}

.match-target-label {
  font-weight: var(--font-semibold);
  font-size: var(--text-sm);
  margin-bottom: var(--space-2);
  display: block;
}

.match-dropzone {
  min-height: 48px;
  border: 2px dashed var(--color-border);
  border-radius: var(--radius-md);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-text-muted);
  font-size: var(--text-sm);
  transition: border-color var(--duration-fast), background var(--duration-fast);
}

.match-dropzone.drag-over {
  border-color: var(--color-accent);
  background: var(--color-accent-light);
}

.match-dropzone.correct {
  border-color: var(--color-success);
  background: var(--color-success-light);
  border-style: solid;
}

.match-dropzone.incorrect {
  border-color: var(--color-error);
  background: var(--color-error-light);
}

@media (max-width: 768px) {
  .match-container { grid-template-columns: 1fr; }
}
```

**JS:** Implementar HTML5 Drag API para mouse + eventos touch personalizados para móvil. Al soltar, verificar `data-match` contra `data-accept`. Feedback visual inmediato.

---

## 4. Simulación de Escenario (Formato Chat)

Simula una conversación entre actores regulatorios (empleado, autoridad, titular de datos, etc.) en formato tipo iMessage.

```html
<div class="chat-simulation" aria-label="Simulación de escenario regulatorio">
  <div class="chat-message entity-learner" data-delay="0">
    <div class="chat-avatar">👤</div>
    <div class="chat-bubble">
      <div class="chat-name">Tú (Director de RRHH)</div>
      <div class="chat-text">Recibí una solicitud de acceso a datos personales de un ex-empleado. ¿Qué hago?</div>
    </div>
  </div>

  <div class="chat-message entity-authority" data-delay="1500">
    <div class="chat-avatar">⚖️</div>
    <div class="chat-bubble">
      <div class="chat-name">La Ley dice (Art. 29)</div>
      <div class="chat-text">Tienes 20 días hábiles para responder la solicitud a partir de que la recibiste.</div>
    </div>
  </div>

  <div class="chat-message entity-learner" data-delay="3000">
    <div class="chat-avatar">👤</div>
    <div class="chat-bubble">
      <div class="chat-name">Tú (Director de RRHH)</div>
      <div class="chat-text">¿Y si necesito más tiempo?</div>
    </div>
  </div>

  <div class="chat-message entity-authority" data-delay="4500">
    <div class="chat-avatar">⚖️</div>
    <div class="chat-bubble">
      <div class="chat-name">La Ley dice (Art. 32)</div>
      <div class="chat-text">Puedes ampliar el plazo otros 20 días, pero debes notificar al titular y explicar las razones.</div>
    </div>
  </div>
</div>
```

```css
.chat-simulation {
  max-width: 600px;
  margin: var(--space-6) auto;
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
}

.chat-message {
  display: flex;
  gap: var(--space-3);
  align-items: flex-start;
  opacity: 0;
  transform: translateY(10px);
  transition: opacity var(--duration-normal) var(--ease-out),
              transform var(--duration-normal) var(--ease-out);
}

.chat-message.visible {
  opacity: 1;
  transform: translateY(0);
}

.chat-avatar {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  flex-shrink: 0;
}

.entity-learner .chat-avatar { background: var(--color-entity-1); color: white; }
.entity-authority .chat-avatar { background: var(--color-entity-2); color: white; }
.entity-subject .chat-avatar { background: var(--color-entity-4); color: white; }
.entity-third .chat-avatar { background: var(--color-entity-3); color: white; }

.chat-bubble {
  background: var(--color-bg-card);
  border: 1px solid var(--color-border-light);
  border-radius: var(--radius-lg);
  padding: var(--space-3) var(--space-4);
  max-width: 80%;
  box-shadow: var(--shadow-sm);
}

.chat-name {
  font-size: var(--text-xs);
  font-weight: var(--font-semibold);
  color: var(--color-text-secondary);
  margin-bottom: var(--space-1);
}

.chat-text {
  font-size: var(--text-base);
  line-height: var(--leading-normal);
}
```

```javascript
// Revelar mensajes secuencialmente con Intersection Observer
function initChatSimulation(container) {
  const messages = container.querySelectorAll('.chat-message');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        messages.forEach((msg, i) => {
          setTimeout(() => msg.classList.add('visible'), i * 800);
        });
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.3 });
  observer.observe(container);
}
```

---

## 5. Animación de Flujo de Cumplimiento

Visualización paso a paso de un procedimiento regulatorio. El usuario avanza por los pasos.

```html
<div class="flow-animation">
  <div class="flow-controls">
    <button class="flow-btn flow-prev" disabled>← Anterior</button>
    <span class="flow-step-indicator">Paso 1 de 5</span>
    <button class="flow-btn flow-next">Siguiente →</button>
  </div>

  <div class="flow-diagram">
    <div class="flow-step active" data-step="1">
      <div class="flow-node entity-subject">
        <span class="flow-icon">📨</span>
        <span class="flow-label">Titular presenta solicitud</span>
      </div>
      <div class="flow-arrow">→</div>
      <div class="flow-node entity-learner">
        <span class="flow-icon">📥</span>
        <span class="flow-label">Tú recibes la solicitud</span>
      </div>
    </div>

    <div class="flow-step" data-step="2">
      <div class="flow-node entity-learner highlighted">
        <span class="flow-icon">✅</span>
        <span class="flow-label">Acusas recibo (5 días)</span>
      </div>
      <div class="flow-arrow">→</div>
      <div class="flow-node entity-subject">
        <span class="flow-icon">📧</span>
        <span class="flow-label">Titular recibe confirmación</span>
      </div>
    </div>
    <!-- más pasos... -->
  </div>

  <div class="flow-detail">
    <p class="flow-detail-text">El titular de los datos presenta una solicitud de acceso, rectificación, cancelación u oposición (solicitud ARCO). Puede hacerlo por cualquier medio que hayas establecido en tu aviso de privacidad.</p>
    <span class="flow-detail-article">Art. 28, fracción I</span>
  </div>
</div>
```

```css
.flow-animation {
  background: var(--color-bg-card);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
  box-shadow: var(--shadow-md);
  margin: var(--space-6) 0;
}

.flow-controls {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: var(--space-6);
}

.flow-btn {
  padding: var(--space-2) var(--space-4);
  border: 2px solid var(--color-accent);
  border-radius: var(--radius-md);
  background: transparent;
  color: var(--color-accent);
  font-weight: var(--font-semibold);
  cursor: pointer;
  transition: all var(--duration-fast);
}

.flow-btn:hover:not(:disabled) { background: var(--color-accent); color: white; }
.flow-btn:disabled { opacity: 0.3; cursor: not-allowed; }

.flow-step {
  display: none;
  align-items: center;
  justify-content: center;
  gap: var(--space-4);
  min-height: 120px;
}

.flow-step.active { display: flex; }

.flow-node {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--space-2);
  padding: var(--space-4);
  border-radius: var(--radius-lg);
  min-width: 140px;
  text-align: center;
  transition: all var(--duration-normal) var(--ease-out);
}

.flow-node.entity-learner { background: rgba(42, 123, 155, 0.1); border: 2px solid var(--color-entity-1); }
.flow-node.entity-authority { background: rgba(217, 79, 48, 0.1); border: 2px solid var(--color-entity-2); }
.flow-node.entity-subject { background: rgba(212, 168, 67, 0.1); border: 2px solid var(--color-entity-4); }
.flow-node.highlighted { box-shadow: 0 0 0 4px rgba(42, 123, 155, 0.2); }

.flow-icon { font-size: 1.5rem; }
.flow-label { font-size: var(--text-sm); font-weight: var(--font-medium); }
.flow-arrow { font-size: var(--text-xl); color: var(--color-text-muted); }

.flow-detail {
  margin-top: var(--space-4);
  padding: var(--space-4);
  background: var(--color-accent-light);
  border-radius: var(--radius-md);
}

.flow-detail-article {
  font-size: var(--text-xs);
  color: var(--color-accent);
  font-weight: var(--font-semibold);
}

@media (max-width: 480px) {
  .flow-step { flex-direction: column; }
  .flow-arrow { transform: rotate(90deg); }
}
```

---

## 6. Diagrama del Ecosistema Regulatorio

Diagrama interactivo con zonas clickeables que representan los actores del ecosistema regulatorio.

```html
<div class="ecosystem-diagram">
  <div class="ecosystem-zone zone-learner" data-entity="learner">
    <h4>Tu Organización</h4>
    <div class="ecosystem-components">
      <button class="ecosystem-component" data-info="Responsable de implementar todas las medidas de cumplimiento">
        Oficial de Datos
      </button>
      <button class="ecosystem-component" data-info="Documenta y publica el aviso de privacidad">
        Comunicación
      </button>
    </div>
  </div>

  <div class="ecosystem-zone zone-authority" data-entity="authority">
    <h4>Autoridad Competente</h4>
    <div class="ecosystem-components">
      <button class="ecosystem-component" data-info="Recibe quejas, investiga violaciones, impone sanciones">
        INAI
      </button>
    </div>
  </div>

  <div class="ecosystem-zone zone-subjects" data-entity="subjects">
    <h4>Titulares de Datos</h4>
    <div class="ecosystem-components">
      <button class="ecosystem-component" data-info="Pueden ejercer sus derechos ARCO en cualquier momento">
        Clientes / Empleados
      </button>
    </div>
  </div>

  <div class="ecosystem-connections">
    <!-- Flechas SVG o CSS que conectan las zonas -->
  </div>
</div>
```

```css
.ecosystem-diagram {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: var(--space-4);
  margin: var(--space-6) 0;
  position: relative;
}

.ecosystem-zone {
  padding: var(--space-5);
  border-radius: var(--radius-lg);
  border: 2px solid;
  text-align: center;
}

.zone-learner   { border-color: var(--color-entity-1); background: rgba(42, 123, 155, 0.05); }
.zone-authority { border-color: var(--color-entity-2); background: rgba(217, 79, 48, 0.05); }
.zone-subjects  { border-color: var(--color-entity-4); background: rgba(212, 168, 67, 0.05); }

.ecosystem-component {
  display: block;
  width: 100%;
  padding: var(--space-2) var(--space-3);
  margin: var(--space-2) 0;
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
  background: var(--color-bg-card);
  cursor: pointer;
  font-size: var(--text-sm);
  transition: all var(--duration-fast);
}

.ecosystem-component:hover {
  box-shadow: var(--shadow-md);
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .ecosystem-diagram { grid-template-columns: 1fr; }
}
```

**JS:** Al hacer click en un componente, mostrar tooltip con `data-info`. Usar `position: fixed` + `getBoundingClientRect()`.

---

## 7. Capas de Cumplimiento (Toggle)

Interfaz de tres pestañas que muestra niveles progresivos de profundidad.

```html
<div class="layer-toggle">
  <div class="layer-tabs">
    <button class="layer-tab active" data-layer="law">Qué dice la ley</button>
    <button class="layer-tab" data-layer="meaning">Qué significa para ti</button>
    <button class="layer-tab" data-layer="comply">Cómo cumplir</button>
  </div>

  <div class="layer-content active" data-layer="law">
    <!-- Texto legal formateado -->
  </div>
  <div class="layer-content" data-layer="meaning">
    <!-- Explicación en lenguaje simple -->
  </div>
  <div class="layer-content" data-layer="comply">
    <!-- Pasos concretos de cumplimiento -->
  </div>
</div>
```

```css
.layer-tabs {
  display: flex;
  gap: var(--space-1);
  margin-bottom: var(--space-4);
}

.layer-tab {
  flex: 1;
  padding: var(--space-3);
  border: none;
  background: var(--color-bg-warm);
  font-family: var(--font-display);
  font-weight: var(--font-semibold);
  font-size: var(--text-sm);
  cursor: pointer;
  border-radius: var(--radius-md) var(--radius-md) 0 0;
  transition: all var(--duration-fast);
}

.layer-tab.active {
  background: var(--color-accent);
  color: white;
}

.layer-content {
  display: none;
  padding: var(--space-5);
  background: var(--color-bg-card);
  border-radius: 0 0 var(--radius-md) var(--radius-md);
  border: 1px solid var(--color-border-light);
}

.layer-content.active { display: block; }
```

---

## 8. Detecta la Violación

El alumno hace click en la línea de un procedimiento empresarial que contiene una violación regulatoria.

```html
<div class="spot-violation">
  <h4>¿Puedes detectar la violación?</h4>
  <p class="spot-instruction">Lee este procedimiento de tu empresa. Haz click en la línea que viola la regulación.</p>

  <div class="spot-lines">
    <div class="spot-line" data-violation="false">
      <span class="spot-num">1</span>
      <span>Cuando un cliente nuevo se registra, recopilamos su nombre y correo electrónico.</span>
    </div>
    <div class="spot-line" data-violation="true">
      <span class="spot-num">2</span>
      <span>También guardamos su historial de navegación sin informarle.</span>
    </div>
    <div class="spot-line" data-violation="false">
      <span class="spot-num">3</span>
      <span>Los datos se almacenan en nuestro servidor seguro con encriptación.</span>
    </div>
  </div>

  <div class="spot-feedback" hidden>
    <p class="spot-explanation"></p>
  </div>
</div>
```

```css
.spot-lines {
  background: var(--color-bg-code);
  border-radius: var(--radius-md);
  padding: var(--space-4);
  margin: var(--space-4) 0;
}

.spot-line {
  display: flex;
  gap: var(--space-3);
  padding: var(--space-2) var(--space-3);
  border-radius: var(--radius-sm);
  cursor: pointer;
  color: var(--color-text-inverse);
  font-size: var(--text-sm);
  line-height: var(--leading-relaxed);
  transition: background var(--duration-fast);
}

.spot-line:hover { background: rgba(255, 255, 255, 0.05); }
.spot-num { color: var(--color-text-muted); min-width: 24px; }

.spot-line.found-violation {
  background: rgba(201, 59, 59, 0.2);
  border-left: 3px solid var(--color-error);
}

.spot-line.safe {
  background: rgba(45, 139, 85, 0.1);
}
```

---

## 9. Quiz de Decisión de Cumplimiento

Variante del quiz (componente 2) con marco contextual más rico. Misma estructura HTML/CSS/JS del componente 2 pero con escenarios más detallados y explicaciones más largas.

---

## 10. Cajas de Dato Clave (Callouts)

Tres variantes para resaltar información importante.

```html
<!-- Insight de cumplimiento -->
<div class="callout callout-accent">
  <div class="callout-icon">💡</div>
  <div class="callout-content">
    <strong>Dato clave:</strong> Este artículo es el que más sanciones genera en la práctica. La mayoría de las multas del INAI en 2024 fueron por incumplimiento de este requisito.
  </div>
</div>

<!-- Referencia útil -->
<div class="callout callout-info">
  <div class="callout-icon">📌</div>
  <div class="callout-content">
    <strong>Bueno saber:</strong> La autoridad publica una guía práctica de implementación en su sitio web que puedes usar como plantilla.
  </div>
</div>

<!-- Error común -->
<div class="callout callout-warning">
  <div class="callout-icon">⚠️</div>
  <div class="callout-content">
    <strong>Ojo:</strong> Muchas empresas confunden "consentimiento tácito" con "no pedir consentimiento". Son cosas muy diferentes — el consentimiento tácito sí requiere que informes al titular.
  </div>
</div>
```

```css
.callout {
  display: flex;
  gap: var(--space-3);
  padding: var(--space-4) var(--space-5);
  border-radius: var(--radius-md);
  margin: var(--space-4) 0;
  border-left: 4px solid;
}

.callout-accent  { background: var(--color-accent-light); border-color: var(--color-accent); }
.callout-info    { background: #F0F4FF; border-color: #6B8AE0; }
.callout-warning { background: var(--color-sanction-low-bg); border-color: var(--color-sanction-low); }

.callout-icon { font-size: 1.2rem; flex-shrink: 0; }
.callout-content { font-size: var(--text-base); line-height: var(--leading-normal); }
```

---

## 11. Tarjetas de Obligación

Grid de tarjetas mostrando obligaciones con badges de plazo e indicadores de severidad.

```html
<div class="obligation-cards">
  <div class="obligation-card" style="border-top-color: var(--color-entity-1)">
    <div class="obligation-header">
      <h4 class="obligation-title">Publicar aviso de privacidad</h4>
      <span class="sanction-severity severity-high" title="Multa alta: 100-320,000 UMAs">●●●</span>
    </div>
    <p class="obligation-desc">Informar a los titulares sobre el tratamiento de sus datos personales antes de recopilarlos.</p>
    <div class="obligation-meta">
      <span class="obligation-article">Art. 15-18</span>
      <span class="obligation-deadline">📅 Antes de cualquier recopilación</span>
    </div>
  </div>
  <!-- más tarjetas... -->
</div>
```

```css
.obligation-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: var(--space-4);
  margin: var(--space-6) 0;
}

.obligation-card {
  background: var(--color-bg-card);
  border-radius: var(--radius-md);
  padding: var(--space-5);
  border-top: 4px solid var(--color-accent);
  box-shadow: var(--shadow-sm);
  transition: transform var(--duration-fast), box-shadow var(--duration-fast);
}

.obligation-card:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-md);
}

.obligation-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: var(--space-3);
}

.obligation-title {
  font-family: var(--font-display);
  font-size: var(--text-lg);
  font-weight: var(--font-bold);
}

.obligation-desc {
  color: var(--color-text-secondary);
  font-size: var(--text-sm);
  line-height: var(--leading-normal);
  margin-bottom: var(--space-3);
}

.obligation-meta {
  display: flex;
  gap: var(--space-3);
  flex-wrap: wrap;
}

.obligation-article {
  font-size: var(--text-xs);
  color: var(--color-accent);
  font-weight: var(--font-semibold);
  background: var(--color-accent-light);
  padding: var(--space-1) var(--space-2);
  border-radius: var(--radius-full);
}

.obligation-deadline {
  font-size: var(--text-xs);
  color: var(--color-text-secondary);
}
```

---

## 12. Diagramas de Flujo de Procedimiento

Pasos horizontales con flechas para procedimientos de cumplimiento.

```html
<div class="procedure-flow">
  <div class="procedure-step">
    <div class="procedure-number">1</div>
    <div class="procedure-content">
      <h5>Recibir solicitud</h5>
      <p>El titular presenta solicitud ARCO</p>
    </div>
  </div>
  <div class="procedure-arrow">→</div>
  <div class="procedure-step">
    <div class="procedure-number">2</div>
    <div class="procedure-content">
      <h5>Acusar recibo</h5>
      <p>Dentro de 5 días hábiles</p>
    </div>
  </div>
  <div class="procedure-arrow">→</div>
  <div class="procedure-step">
    <div class="procedure-number">3</div>
    <div class="procedure-content">
      <h5>Evaluar y resolver</h5>
      <p>Dentro de 20 días hábiles</p>
    </div>
  </div>
</div>
```

```css
.procedure-flow {
  display: flex;
  align-items: flex-start;
  gap: var(--space-2);
  margin: var(--space-6) 0;
  overflow-x: auto;
}

.procedure-step {
  flex: 1;
  min-width: 140px;
  text-align: center;
}

.procedure-number {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background: var(--color-accent);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: var(--font-bold);
  margin: 0 auto var(--space-2);
}

.procedure-content h5 {
  font-size: var(--text-sm);
  font-weight: var(--font-semibold);
  margin-bottom: var(--space-1);
}

.procedure-content p {
  font-size: var(--text-xs);
  color: var(--color-text-secondary);
}

.procedure-arrow {
  color: var(--color-text-muted);
  font-size: var(--text-xl);
  padding-top: var(--space-2);
}

@media (max-width: 480px) {
  .procedure-flow { flex-direction: column; align-items: stretch; }
  .procedure-arrow { transform: rotate(90deg); text-align: center; }
}
```

---

## 13. Badges de Requisitos/Documentos

Tokens anotados para tipos de documentos o requisitos.

```html
<div class="requirement-badges">
  <div class="requirement-badge">
    <span class="badge-code">📄 Aviso de Privacidad</span>
    <span class="badge-desc">Documento público que informa a los titulares sobre el tratamiento de sus datos</span>
  </div>
  <div class="requirement-badge">
    <span class="badge-code">📋 Registro de Tratamientos</span>
    <span class="badge-desc">Inventario interno de todas las bases de datos y tipos de datos que manejas</span>
  </div>
</div>
```

```css
.requirement-badges {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-3);
  margin: var(--space-4) 0;
}

.requirement-badge {
  background: var(--color-bg-card);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
  padding: var(--space-3) var(--space-4);
  max-width: 300px;
}

.badge-code {
  display: block;
  font-weight: var(--font-semibold);
  font-size: var(--text-sm);
  margin-bottom: var(--space-1);
}

.badge-desc {
  font-size: var(--text-xs);
  color: var(--color-text-secondary);
  line-height: var(--leading-normal);
}
```

---

## 14. Tooltips de Términos Legales

Tooltips en lenguaje simple para términos jurídicos. Se activan con click o hover.

```html
<span class="legal-tooltip" data-term="prescripción">
  prescripción
  <span class="tooltip-content">
    La fecha de caducidad legal de una obligación o derecho — como una garantía que se vence. Después del período de prescripción, la autoridad ya no puede sancionarte por esa violación. Cuando hables con tu abogado, preguntarías "¿Esto ya prescribió?"
  </span>
</span>
```

```css
.legal-tooltip {
  border-bottom: 2px dashed var(--color-accent-muted);
  cursor: pointer;
  position: relative;
}

/* El tooltip real se posiciona con JS usando position: fixed */
.tooltip-popup {
  position: fixed;
  background: var(--color-bg-code);
  color: var(--color-text-inverse);
  padding: var(--space-3) var(--space-4);
  border-radius: var(--radius-md);
  font-size: var(--text-sm);
  line-height: var(--leading-relaxed);
  max-width: 320px;
  box-shadow: var(--shadow-lg);
  z-index: 1000;
  pointer-events: none;
  opacity: 0;
  transform: translateY(4px);
  transition: opacity var(--duration-fast), transform var(--duration-fast);
}

.tooltip-popup.visible {
  opacity: 1;
  transform: translateY(0);
}
```

```javascript
// CRÍTICO: Tooltips con position: fixed para evitar recorte
(function() {
  const tooltip = document.createElement('div');
  tooltip.className = 'tooltip-popup';
  document.body.appendChild(tooltip);

  document.querySelectorAll('.legal-tooltip').forEach(el => {
    el.addEventListener('mouseenter', function(e) {
      const content = this.querySelector('.tooltip-content');
      if (!content) return;

      tooltip.textContent = content.textContent;
      tooltip.classList.add('visible');

      const rect = this.getBoundingClientRect();
      const tooltipRect = tooltip.getBoundingClientRect();

      let top = rect.bottom + 8;
      let left = rect.left + (rect.width / 2) - (tooltipRect.width / 2);

      // Mantener dentro del viewport
      if (left < 8) left = 8;
      if (left + tooltipRect.width > window.innerWidth - 8) {
        left = window.innerWidth - tooltipRect.width - 8;
      }
      if (top + tooltipRect.height > window.innerHeight - 8) {
        top = rect.top - tooltipRect.height - 8;
      }

      tooltip.style.top = top + 'px';
      tooltip.style.left = left + 'px';
    });

    el.addEventListener('mouseleave', () => {
      tooltip.classList.remove('visible');
    });
  });
})();
```

**REGLA CRÍTICA:** Siempre usar `position: fixed` + append a `document.body`. NUNCA poner tooltips dentro de contenedores con `overflow: hidden`.

---

## 15. Árbol de Documentos

Estructura visual de los documentos que el rol debe mantener para cumplimiento.

```html
<div class="doc-tree">
  <div class="doc-folder">
    <span class="doc-folder-icon">📁</span>
    <span class="doc-folder-name">Documentos de Cumplimiento</span>
  </div>
  <div class="doc-children">
    <div class="doc-folder">
      <span class="doc-folder-icon">📁</span>
      <span class="doc-folder-name">Avisos de Privacidad</span>
    </div>
    <div class="doc-children">
      <div class="doc-file">
        <span class="doc-file-icon">📄</span>
        <span class="doc-file-name">Aviso integral (clientes)</span>
        <span class="doc-file-desc">— Versión completa para recopilación directa</span>
      </div>
      <div class="doc-file">
        <span class="doc-file-icon">📄</span>
        <span class="doc-file-name">Aviso simplificado (web)</span>
        <span class="doc-file-desc">— Versión corta para formularios en línea</span>
      </div>
    </div>
    <div class="doc-file">
      <span class="doc-file-icon">📋</span>
      <span class="doc-file-name">Registro de tratamientos</span>
      <span class="doc-file-desc">— Inventario de todas las bases de datos</span>
    </div>
  </div>
</div>
```

```css
.doc-tree {
  font-family: var(--font-body);
  font-size: var(--text-sm);
  margin: var(--space-4) 0;
}

.doc-children { padding-left: var(--space-6); }

.doc-folder, .doc-file {
  display: flex;
  align-items: baseline;
  gap: var(--space-2);
  padding: var(--space-1) 0;
}

.doc-folder-name { font-weight: var(--font-semibold); }
.doc-file-desc { color: var(--color-text-muted); font-size: var(--text-xs); }
```

---

## 16. Filas de Ícono + Label

Filas flexbox con íconos circulares y texto explicativo.

```html
<div class="icon-rows">
  <div class="icon-row">
    <div class="icon-circle" style="background: var(--color-entity-1)">📊</div>
    <div class="icon-text">
      <h5>Obligaciones de documentación</h5>
      <p>Registros, avisos y políticas que debes mantener actualizados</p>
    </div>
  </div>
  <div class="icon-row">
    <div class="icon-circle" style="background: var(--color-entity-2)">⏰</div>
    <div class="icon-text">
      <h5>Obligaciones periódicas</h5>
      <p>Reportes y renovaciones que se deben hacer en fechas específicas</p>
    </div>
  </div>
</div>
```

```css
.icon-rows { margin: var(--space-4) 0; }

.icon-row {
  display: flex;
  gap: var(--space-4);
  align-items: flex-start;
  margin-bottom: var(--space-4);
}

.icon-circle {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.3rem;
  flex-shrink: 0;
}

.icon-text h5 {
  font-size: var(--text-base);
  font-weight: var(--font-semibold);
  margin-bottom: var(--space-1);
}

.icon-text p {
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
  line-height: var(--leading-normal);
}
```

---

## 17. Tarjetas de Pasos Numerados

Tarjetas secuenciales para procedimientos de cumplimiento.

```html
<div class="step-cards">
  <div class="step-card">
    <div class="step-number">01</div>
    <h4 class="step-title">Designa un responsable</h4>
    <p class="step-desc">Nombra a una persona o departamento encargado de atender solicitudes de datos personales.</p>
  </div>
  <div class="step-card">
    <div class="step-number">02</div>
    <h4 class="step-title">Elabora tu aviso de privacidad</h4>
    <p class="step-desc">Redacta el documento que informará a los titulares sobre el tratamiento de sus datos.</p>
  </div>
  <div class="step-card">
    <div class="step-number">03</div>
    <h4 class="step-title">Implementa medidas de seguridad</h4>
    <p class="step-desc">Establece controles técnicos y organizacionales para proteger los datos personales.</p>
  </div>
</div>
```

```css
.step-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: var(--space-4);
  margin: var(--space-6) 0;
}

.step-card {
  background: var(--color-bg-card);
  border-radius: var(--radius-lg);
  padding: var(--space-5);
  box-shadow: var(--shadow-sm);
}

.step-number {
  font-family: var(--font-display);
  font-size: var(--text-3xl);
  font-weight: var(--font-black);
  color: var(--color-accent);
  opacity: 0.3;
  line-height: 1;
  margin-bottom: var(--space-2);
}

.step-title {
  font-size: var(--text-lg);
  font-weight: var(--font-bold);
  margin-bottom: var(--space-2);
}

.step-desc {
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
  line-height: var(--leading-normal);
}
```

---

## 18. Checklist Interactivo de Cumplimiento (NUEVO)

Componente funcional con persistencia en localStorage. El alumno marca lo que ya cumplió.

```html
<div class="checklist-container" id="compliance-checklist">
  <div class="checklist-header">
    <h3>Tu Checklist de Cumplimiento</h3>
    <div class="checklist-progress">
      <span class="checklist-count">0 / 12 completados</span>
      <div class="checklist-bar"><div class="checklist-bar-fill"></div></div>
    </div>
  </div>

  <div class="checklist-section">
    <h4 class="checklist-section-title">🔴 Inmediato (primeros 30 días)</h4>

    <label class="checklist-item" data-id="item-1">
      <input type="checkbox" class="checklist-check">
      <div class="checklist-content">
        <span class="checklist-obligation">Designar un oficial de datos personales</span>
        <div class="checklist-meta">
          <span class="checklist-article">Art. 30</span>
          <span class="checklist-deadline">Antes de iniciar tratamiento</span>
          <span class="sanction-severity severity-high" title="Multa alta">●●●</span>
        </div>
      </div>
    </label>

    <label class="checklist-item" data-id="item-2">
      <input type="checkbox" class="checklist-check">
      <div class="checklist-content">
        <span class="checklist-obligation">Elaborar y publicar aviso de privacidad</span>
        <div class="checklist-meta">
          <span class="checklist-article">Art. 15-18</span>
          <span class="checklist-deadline">Antes de recopilar datos</span>
          <span class="sanction-severity severity-high" title="Multa alta">●●●</span>
        </div>
      </div>
    </label>
  </div>

  <div class="checklist-section">
    <h4 class="checklist-section-title">🟡 Corto plazo (primeros 90 días)</h4>
    <!-- más ítems... -->
  </div>

  <div class="checklist-section">
    <h4 class="checklist-section-title">🔵 Recurrente (anual)</h4>
    <!-- más ítems... -->
  </div>
</div>
```

```css
.checklist-container {
  background: var(--color-bg-card);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
  box-shadow: var(--shadow-md);
  margin: var(--space-8) 0;
}

.checklist-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--space-6);
  flex-wrap: wrap;
  gap: var(--space-3);
}

.checklist-progress { text-align: right; }

.checklist-count {
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
  display: block;
  margin-bottom: var(--space-1);
}

.checklist-bar {
  width: 200px;
  height: 6px;
  background: var(--color-border-light);
  border-radius: var(--radius-full);
  overflow: hidden;
}

.checklist-bar-fill {
  height: 100%;
  background: var(--color-success);
  border-radius: var(--radius-full);
  transition: width var(--duration-normal) var(--ease-out);
  width: 0%;
}

.checklist-section { margin-bottom: var(--space-6); }

.checklist-section-title {
  font-family: var(--font-display);
  font-size: var(--text-lg);
  font-weight: var(--font-bold);
  margin-bottom: var(--space-3);
}

.checklist-item {
  display: flex;
  align-items: flex-start;
  gap: var(--space-3);
  padding: var(--space-3) var(--space-4);
  border: 1px solid var(--color-border-light);
  border-radius: var(--radius-md);
  margin-bottom: var(--space-2);
  cursor: pointer;
  transition: all var(--duration-fast);
}

.checklist-item:hover { background: var(--color-accent-light); }

.checklist-item.checked {
  opacity: 0.6;
  background: var(--color-success-light);
}

.checklist-item.checked .checklist-obligation {
  text-decoration: line-through;
}

.checklist-check {
  width: 20px;
  height: 20px;
  margin-top: 2px;
  accent-color: var(--color-success);
  flex-shrink: 0;
}

.checklist-obligation {
  font-weight: var(--font-medium);
  font-size: var(--text-base);
  display: block;
  margin-bottom: var(--space-1);
}

.checklist-meta {
  display: flex;
  gap: var(--space-3);
  flex-wrap: wrap;
  align-items: center;
}

.checklist-article {
  font-size: var(--text-xs);
  color: var(--color-accent);
  font-weight: var(--font-semibold);
}

.checklist-deadline {
  font-size: var(--text-xs);
  color: var(--color-text-muted);
}
```

```javascript
// Persistencia en localStorage
(function() {
  const STORAGE_KEY = 'reglabot-checklist'; // Agregar hash del nombre de regulación

  function loadState() {
    try {
      return JSON.parse(localStorage.getItem(STORAGE_KEY)) || {};
    } catch { return {}; }
  }

  function saveState(state) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
  }

  function updateProgress() {
    const total = document.querySelectorAll('.checklist-check').length;
    const checked = document.querySelectorAll('.checklist-check:checked').length;
    const count = document.querySelector('.checklist-count');
    const fill = document.querySelector('.checklist-bar-fill');

    if (count) count.textContent = `${checked} / ${total} completados`;
    if (fill) fill.style.width = `${(checked / total) * 100}%`;
  }

  // Restaurar estado guardado
  const state = loadState();
  document.querySelectorAll('.checklist-item').forEach(item => {
    const id = item.dataset.id;
    const checkbox = item.querySelector('.checklist-check');

    if (state[id]) {
      checkbox.checked = true;
      item.classList.add('checked');
    }

    checkbox.addEventListener('change', function() {
      const currentState = loadState();
      currentState[id] = this.checked;
      saveState(currentState);
      item.classList.toggle('checked', this.checked);
      updateProgress();
    });
  });

  updateProgress();
})();
```

---

## 19. Línea de Tiempo de Plazos (NUEVO)

Timeline vertical mostrando plazos de cumplimiento en orden cronológico.

```html
<div class="timeline-container">
  <div class="timeline-line"></div>

  <div class="timeline-item animate-in">
    <div class="timeline-date">
      <span class="timeline-day">Día 1</span>
      <span class="timeline-label">Entrada en vigor</span>
    </div>
    <div class="timeline-node"></div>
    <div class="timeline-card">
      <h4>La regulación entra en vigor</h4>
      <p>Todas las disposiciones son exigibles a partir de esta fecha.</p>
      <div class="timeline-card-meta">
        <span class="timeline-article">Transitorio Primero</span>
      </div>
    </div>
  </div>

  <div class="timeline-item animate-in">
    <div class="timeline-date">
      <span class="timeline-day">30 días</span>
      <span class="timeline-label">Primer plazo</span>
    </div>
    <div class="timeline-node"></div>
    <div class="timeline-card">
      <h4>Designar oficial de datos</h4>
      <p>Nombrar a la persona responsable de cumplimiento dentro de tu organización.</p>
      <div class="timeline-card-meta">
        <span class="timeline-article">Art. 30</span>
        <span class="sanction-severity severity-medium" title="Multa media">●●</span>
      </div>
    </div>
  </div>

  <div class="timeline-item recurring animate-in">
    <div class="timeline-date">
      <span class="timeline-day">Cada 31 de marzo</span>
      <span class="timeline-label">Recurrente 🔄</span>
    </div>
    <div class="timeline-node recurring-node"></div>
    <div class="timeline-card">
      <h4>Actualizar registro de tratamientos</h4>
      <p>Revisar y actualizar el inventario de datos personales y bases de datos.</p>
      <div class="timeline-card-meta">
        <span class="timeline-article">Art. 43</span>
        <span class="sanction-severity severity-low" title="Multa baja">●</span>
      </div>
    </div>
  </div>
</div>
```

```css
.timeline-container {
  position: relative;
  padding: var(--space-6) 0 var(--space-6) var(--space-16);
  margin: var(--space-8) 0;
}

.timeline-line {
  position: absolute;
  left: 20px;
  top: 0;
  bottom: 0;
  width: 3px;
  background: var(--color-border);
}

.timeline-item {
  position: relative;
  margin-bottom: var(--space-8);
  display: grid;
  grid-template-columns: 80px 1fr;
  gap: var(--space-4);
  align-items: start;
}

.timeline-node {
  position: absolute;
  left: calc(-1 * var(--space-16) + 12px);
  top: var(--space-1);
  width: 18px;
  height: 18px;
  border-radius: 50%;
  background: var(--color-accent);
  border: 3px solid var(--color-bg);
  z-index: 1;
}

.recurring-node {
  background: var(--color-sanction-low);
  box-shadow: 0 0 0 4px var(--color-sanction-low-bg);
}

.timeline-date {
  text-align: right;
}

.timeline-day {
  display: block;
  font-family: var(--font-display);
  font-weight: var(--font-bold);
  font-size: var(--text-sm);
  color: var(--color-text);
}

.timeline-label {
  display: block;
  font-size: var(--text-xs);
  color: var(--color-text-muted);
}

.timeline-card {
  background: var(--color-bg-card);
  border: 1px solid var(--color-border-light);
  border-radius: var(--radius-md);
  padding: var(--space-4);
  box-shadow: var(--shadow-sm);
}

.timeline-card h4 {
  font-size: var(--text-base);
  font-weight: var(--font-semibold);
  margin-bottom: var(--space-2);
}

.timeline-card p {
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
  line-height: var(--leading-normal);
  margin-bottom: var(--space-2);
}

.timeline-card-meta {
  display: flex;
  gap: var(--space-3);
  align-items: center;
}

.timeline-article {
  font-size: var(--text-xs);
  color: var(--color-accent);
  font-weight: var(--font-semibold);
}

.recurring .timeline-card {
  border-style: dashed;
  border-color: var(--color-sanction-low);
}

/* Responsive */
@media (max-width: 480px) {
  .timeline-container { padding-left: var(--space-10); }
  .timeline-item { grid-template-columns: 1fr; }
  .timeline-date { text-align: left; }
  .timeline-node { left: calc(-1 * var(--space-10) + 8px); }
}
```

---

## 20. Indicador de Severidad de Sanciones (NUEVO)

Badge reutilizable. Ver `design-system.md` para los estilos CSS completos.

```html
<!-- Uso inline en cualquier componente -->
<span class="sanction-severity severity-low" title="Baja: Apercibimiento o multa menor">●</span>
<span class="sanction-severity severity-medium" title="Media: Multa significativa o suspensión">●●</span>
<span class="sanction-severity severity-high" title="Alta: Multa mayor, clausura o responsabilidad penal">●●●</span>
```

**Uso:** Se inserta dentro de tarjetas de obligación (comp. 11), ítems del checklist (comp. 18), entradas del timeline (comp. 19), y cualquier lugar donde se mencione una sanción.

**Tooltip:** Cada badge debe tener un `title` o tooltip con JS que explique la severidad en lenguaje simple.
