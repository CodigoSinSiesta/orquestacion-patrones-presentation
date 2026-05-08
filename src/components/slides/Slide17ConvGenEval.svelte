<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="conv-badge">
      <span class="badge-num">Convergencia 2</span>
    </div>

    <h2 class="title"><span class="hl">Separar generación y evaluación</span></h2>
    <p class="subtitle">Tres empresas con tres nombres distintos para el mismo principio — señal de convergencia real.</p>

    <div class="three-cols">
      <div class="company-card">
        <div class="cc-header">
          <span class="cc-logo anthro">A</span>
          <span class="cc-name">Anthropic</span>
        </div>
        <div class="cc-pattern">Generator + Evaluator</div>
        <p class="cc-desc">El evaluador opera en contexto separado. No ve el razonamiento del generador — solo su output. Sesgo independiente es el objetivo.</p>
        <div class="cc-detail">Sprint Contracts definen los criterios de evaluación antes de que el generador empiece.</div>
      </div>

      <div class="company-card">
        <div class="cc-header">
          <span class="cc-logo openai">O</span>
          <span class="cc-name">OpenAI / Lopopolo</span>
        </div>
        <div class="cc-pattern">Persona-based Reviewer Agents</div>
        <p class="cc-desc">Agentes reviewer con personalidades distintas (el escéptico, el optimizador de rendimiento, el de seguridad). Diferentes ángulos de ataque.</p>
        <div class="cc-detail">Code review en CI: no opcional, parte del harness. Cada revisión es autónoma.</div>
      </div>

      <div class="company-card">
        <div class="cc-header">
          <span class="cc-logo factory">F</span>
          <span class="cc-name">Factory</span>
        </div>
        <div class="cc-pattern">Worker + Validator + Scrutiny Validator</div>
        <p class="cc-desc">Dos tipos de validación: el Validator evalúa contra el Validation Contract; el Scrutiny Validator ejecuta el pipeline (tests → lint → type-check → review).</p>
        <div class="cc-detail">El Orchestrator decide si el output pasa a la siguiente tarea o se reprocesa.</div>
      </div>
    </div>

    <div class="why-works">
      <span class="ww-icon">🧠</span>
      <p>Por qué funciona: los LLMs tienen confirmation bias. Un modelo que genera también tiene el sesgo de "esto parece correcto porque yo lo generé". El evaluador independiente rompe ese ciclo.</p>
    </div>
  </div>
</div>

<style>
  .swiper-slide {
    width: 100%;
    min-height: 100vh;
    display: flex;
    align-items: flex-start;
    justify-content: center;
    background: var(--color-base-dark);
  }

  .slide-content {
    max-width: 1200px;
    width: 100%;
    padding: var(--spacing-content);
    padding-top: 4rem;
    display: flex;
    flex-direction: column;
    gap: var(--spacing-xl);
  }

  .conv-badge { display: inline-flex; }

  .badge-num {
    font-family: var(--font-mono);
    font-size: 0.78rem;
    font-weight: 700;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: #c4b5fd;
    background: rgba(167, 139, 250, 0.12);
    border: 1px solid rgba(167, 139, 250, 0.3);
    padding: 4px 12px;
    border-radius: 999px;
  }

  .title {
    font-size: clamp(1.8rem, 4.5vw, 3.2rem);
    font-weight: 900;
    color: var(--color-neutral-light);
    margin-bottom: 0;
  }

  .hl {
    background: linear-gradient(135deg, #a78bfa, #c4b5fd);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .subtitle {
    font-size: 1rem;
    color: var(--color-neutral-light);
    opacity: 0.6;
    margin-bottom: 0;
  }

  .three-cols {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: var(--spacing-lg);
  }

  .company-card {
    background: rgba(30, 58, 138, 0.1);
    border: 1px solid rgba(167, 139, 250, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-xl);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-md);
  }

  .cc-header {
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
  }

  .cc-logo {
    width: 32px; height: 32px;
    border-radius: var(--radius-sm);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: var(--font-mono);
    font-size: 0.85rem;
    font-weight: 800;
    flex-shrink: 0;
  }

  .anthro { background: rgba(167, 139, 250, 0.2); color: #c4b5fd; }
  .openai { background: rgba(96, 165, 250, 0.2); color: #93c5fd; }
  .factory { background: rgba(34, 197, 94, 0.2); color: #86efac; }

  .cc-name {
    font-family: var(--font-display);
    font-size: 0.9rem;
    font-weight: 700;
    color: var(--color-neutral-light);
  }

  .cc-pattern {
    font-family: var(--font-mono);
    font-size: 0.82rem;
    font-weight: 700;
    color: #c4b5fd;
    background: rgba(167, 139, 250, 0.1);
    border: 1px solid rgba(167, 139, 250, 0.2);
    border-radius: var(--radius-sm);
    padding: 6px 10px;
  }

  .cc-desc {
    font-size: 0.85rem;
    color: var(--color-neutral-light);
    opacity: 0.7;
    line-height: 1.6;
    margin-bottom: 0;
    flex: 1;
  }

  .cc-detail {
    font-size: 0.78rem;
    color: var(--color-neutral-light);
    opacity: 0.45;
    font-style: italic;
    line-height: 1.4;
    padding-top: var(--spacing-sm);
    border-top: 1px solid rgba(96, 165, 250, 0.08);
  }

  .why-works {
    display: flex;
    gap: var(--spacing-md);
    background: rgba(167, 139, 250, 0.07);
    border: 1px solid rgba(167, 139, 250, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg) var(--spacing-xl);
  }

  .ww-icon { font-size: 1.5rem; flex-shrink: 0; }

  .why-works p {
    font-size: 0.9rem;
    color: var(--color-neutral-light);
    opacity: 0.65;
    line-height: 1.6;
    margin-bottom: 0;
  }

  @media (max-width: 900px) {
    .three-cols { grid-template-columns: 1fr; }
  }
</style>
