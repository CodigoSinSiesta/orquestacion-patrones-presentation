<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="problem-badge">
      <span class="badge-num">Problema 4</span>
      <span class="badge-emoji">🐛</span>
    </div>

    <h2 class="title">Los tests escritos por el mismo agente <span class="hl">no atrapan bugs reales</span></h2>

    <div class="two-col">
      <div class="col-problem">
        <h3 class="col-title col-title-prob">El dolor</h3>
        <p>Si el mismo agente que implementa también escribe los tests, ambos parten del mismo malentendido. El agente no tiene un spec externo — tiene su propia interpretación de lo que debería hacer el código. Los tests validan esa interpretación, no el comportamiento correcto.</p>
        <div class="stats-box">
          <div class="stat">
            <span class="stat-num">52%</span>
            <span class="stat-label">de los tests en la misión Slack clone los escribió el mismo worker que implementó</span>
          </div>
          <div class="stat highlight-stat">
            <span class="stat-num">89%</span>
            <span class="stat-label">coverage final — gracias al Validation Contract escrito antes de la implementación</span>
          </div>
        </div>
      </div>

      <div class="col-solution">
        <h3 class="col-title col-title-sol">El patrón: Validation Contract</h3>

        <div class="contract-flow">
          <div class="cf-step step-before">
            <span class="step-label">ANTES de implementar</span>
            <div class="contract-box">
              <p class="cb-title">Validation Contract</p>
              <p class="cb-item">✓ Criterios de aceptación funcional</p>
              <p class="cb-item">✓ Casos edge obligatorios</p>
              <p class="cb-item">✓ Performance thresholds</p>
              <p class="cb-item">✓ Constraints de seguridad</p>
            </div>
          </div>
          <div class="cf-arrow">↓ Worker implementa contra este contrato</div>
          <div class="cf-step step-after">
            <span class="step-label">DESPUÉS de implementar</span>
            <div class="validator-box">
              <p class="vb-title">Scrutiny Validator (pipeline)</p>
              <p class="cb-item">→ Tests contra el contrato</p>
              <p class="cb-item">→ Linter + type-check</p>
              <p class="cb-item">→ Code review agente independiente</p>
            </div>
          </div>
        </div>

        <p class="key-insight">El contrato lo escribe el Orchestrator, que tiene la visión de la tarea completa. El Worker no puede alterar los criterios de aceptación.</p>
      </div>
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
    max-width: 1100px;
    width: 100%;
    padding: var(--spacing-content);
    padding-top: 4rem;
    display: flex;
    flex-direction: column;
    gap: var(--spacing-xl);
  }

  .problem-badge { display: flex; align-items: center; gap: var(--spacing-md); }

  .badge-num {
    font-family: var(--font-mono);
    font-size: 0.78rem;
    font-weight: 700;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: #fcd34d;
    background: rgba(245, 158, 11, 0.12);
    border: 1px solid rgba(245, 158, 11, 0.3);
    padding: 4px 12px;
    border-radius: 999px;
  }

  .badge-emoji { font-size: 1.5rem; }

  .title {
    font-size: clamp(1.6rem, 3.5vw, 2.8rem);
    font-weight: 900;
    color: var(--color-neutral-light);
    margin-bottom: 0;
  }

  .hl {
    background: linear-gradient(135deg, #f59e0b, #fcd34d);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .two-col {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: var(--spacing-2xl);
    align-items: start;
  }

  .col-title {
    font-size: 0.85rem;
    font-weight: 700;
    margin-bottom: var(--spacing-md);
    font-family: var(--font-mono);
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  .col-title-prob { color: #f87171; }
  .col-title-sol { color: #86efac; }

  .col-problem, .col-solution { display: flex; flex-direction: column; gap: var(--spacing-lg); }

  .col-problem p {
    font-size: 0.875rem;
    color: var(--color-neutral-light);
    opacity: 0.7;
    line-height: 1.7;
    margin-bottom: 0;
  }

  .stats-box {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-md);
  }

  .stat {
    background: rgba(30, 58, 138, 0.2);
    border: 1px solid rgba(96, 165, 250, 0.15);
    border-radius: var(--radius-md);
    padding: var(--spacing-md) var(--spacing-lg);
    display: flex;
    gap: var(--spacing-md);
    align-items: center;
  }

  .highlight-stat {
    background: rgba(34, 197, 94, 0.08);
    border-color: rgba(34, 197, 94, 0.3);
  }

  .stat-num {
    font-family: var(--font-display);
    font-size: 2rem;
    font-weight: 900;
    color: var(--color-electric);
    flex-shrink: 0;
  }

  .highlight-stat .stat-num { color: #86efac; }

  .stat-label {
    font-size: 0.8rem;
    color: var(--color-neutral-light);
    opacity: 0.65;
    line-height: 1.4;
  }

  .contract-flow {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
  }

  .cf-step { display: flex; flex-direction: column; gap: var(--spacing-sm); }

  .step-label {
    font-family: var(--font-mono);
    font-size: 0.7rem;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }

  .step-before .step-label { color: var(--color-electric); }
  .step-after .step-label { color: #86efac; }

  .contract-box {
    background: rgba(59, 130, 246, 0.08);
    border: 1px solid rgba(59, 130, 246, 0.25);
    border-radius: var(--radius-sm);
    padding: var(--spacing-md) var(--spacing-lg);
  }

  .validator-box {
    background: rgba(34, 197, 94, 0.07);
    border: 1px solid rgba(34, 197, 94, 0.2);
    border-radius: var(--radius-sm);
    padding: var(--spacing-md) var(--spacing-lg);
  }

  .cb-title, .vb-title {
    font-family: var(--font-mono);
    font-size: 0.78rem;
    font-weight: 700;
    color: var(--color-electric);
    margin-bottom: var(--spacing-sm);
  }

  .vb-title { color: #86efac; }

  .cb-item {
    font-size: 0.8rem;
    color: var(--color-neutral-light);
    opacity: 0.65;
    line-height: 1.6;
    margin-bottom: 0;
  }

  .cf-arrow {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    color: rgba(34, 197, 94, 0.4);
    text-align: center;
    padding: 4px 0;
  }

  .key-insight {
    font-size: 0.875rem;
    color: var(--color-neutral-light);
    opacity: 0.6;
    line-height: 1.6;
    font-style: italic;
    margin-bottom: 0;
    background: rgba(34, 197, 94, 0.06);
    border-left: 3px solid rgba(34, 197, 94, 0.4);
    padding: var(--spacing-md) var(--spacing-lg);
    border-radius: 0 var(--radius-sm) var(--radius-sm) 0;
  }

  @media (max-width: 900px) { .two-col { grid-template-columns: 1fr; } }
</style>
