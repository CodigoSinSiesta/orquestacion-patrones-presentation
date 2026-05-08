<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="problem-badge">
      <span class="badge-num">Problema 3</span>
      <span class="badge-emoji">⚔️</span>
    </div>

    <h2 class="title">Los agentes en paralelo <span class="hl">se pisan los cambios</span></h2>

    <div class="two-col">
      <div class="col-problem">
        <h3 class="col-title col-title-prob">El dolor</h3>
        <p>Correr 10 agentes en paralelo escribiendo código parece la solución obvia para acelerar. El resultado real: merge conflicts, estados inconsistentes, linter que pasa en aislamiento pero falla en integración.</p>
        <div class="conflict-viz">
          <div class="agents-parallel">
            <div class="agent-bad">Agente A escribe auth.ts</div>
            <div class="agent-bad">Agente B escribe auth.ts</div>
            <div class="agent-bad">Agente C escribe user.ts</div>
          </div>
          <div class="conflict-arrow">↓ integración</div>
          <div class="conflict-result">💥 conflicts · estado inconsistente · debugging imposible</div>
        </div>
        <p class="side-note">Factory midió esto: el overhead de coordinación de agentes paralelos sobre el mismo codebase supera el beneficio de velocidad en la mayoría de tareas de software.</p>
      </div>

      <div class="col-solution">
        <h3 class="col-title col-title-sol">El patrón: Serial con paralelismo interno read-only</h3>

        <div class="serial-viz">
          <div class="serial-step">
            <span class="ss-icon">📋</span>
            <div>
              <p class="ss-title">Orchestrator planifica</p>
              <p class="ss-desc">descompone en tareas seriales sin solapamiento</p>
            </div>
          </div>
          <div class="serial-arrow">↓</div>
          <div class="serial-step">
            <span class="ss-icon">⚙️</span>
            <div>
              <p class="ss-title">Worker 1 implementa módulo A</p>
              <p class="ss-desc">acceso exclusivo de escritura · paralelismo solo en lectura</p>
            </div>
          </div>
          <div class="serial-arrow">↓</div>
          <div class="serial-step">
            <span class="ss-icon">✅</span>
            <div>
              <p class="ss-title">Validator verifica</p>
              <p class="ss-desc">tests · lint · code review (pueden correr en paralelo)</p>
            </div>
          </div>
          <div class="serial-arrow">↓</div>
          <div class="serial-step">
            <span class="ss-icon">⚙️</span>
            <div>
              <p class="ss-title">Worker 2 implementa módulo B</p>
              <p class="ss-desc">parte del estado validado del worker 1</p>
            </div>
          </div>
        </div>

        <div class="insight-box">
          <p>El paralelismo es seguro cuando los agentes solo leen. Los validadores (tests, lint, reviews) pueden correr en paralelo porque no modifican el estado.</p>
        </div>
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
    font-size: clamp(1.8rem, 4vw, 3rem);
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

  .conflict-viz {
    background: rgba(248, 113, 113, 0.06);
    border: 1px solid rgba(248, 113, 113, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
    align-items: center;
  }

  .agents-parallel { display: flex; flex-direction: column; gap: 4px; width: 100%; }

  .agent-bad {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    color: #f87171;
    background: rgba(248, 113, 113, 0.1);
    border: 1px solid rgba(248, 113, 113, 0.2);
    border-radius: var(--radius-sm);
    padding: 6px 12px;
  }

  .conflict-arrow {
    font-family: var(--font-mono);
    font-size: 0.8rem;
    color: rgba(248, 113, 113, 0.5);
  }

  .conflict-result {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    color: #f87171;
    text-align: center;
    opacity: 0.8;
  }

  .side-note {
    font-size: 0.82rem !important;
    opacity: 0.5 !important;
    font-style: italic;
  }

  .serial-viz {
    background: rgba(34, 197, 94, 0.05);
    border: 1px solid rgba(34, 197, 94, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-xs);
  }

  .serial-step {
    display: flex;
    gap: var(--spacing-md);
    align-items: flex-start;
    background: rgba(30, 58, 138, 0.2);
    border-radius: var(--radius-sm);
    padding: var(--spacing-md);
  }

  .ss-icon { font-size: 1.1rem; flex-shrink: 0; line-height: 1.4; }

  .ss-title {
    font-size: 0.85rem;
    font-weight: 600;
    color: var(--color-neutral-light);
    margin-bottom: 2px;
  }

  .ss-desc {
    font-size: 0.75rem;
    color: var(--color-neutral-light);
    opacity: 0.5;
    margin-bottom: 0;
  }

  .serial-arrow {
    text-align: center;
    color: rgba(34, 197, 94, 0.4);
    font-size: 0.9rem;
    padding: 2px 0;
  }

  .insight-box {
    background: rgba(34, 197, 94, 0.07);
    border: 1px solid rgba(34, 197, 94, 0.25);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
  }

  .insight-box p {
    font-size: 0.875rem;
    color: var(--color-neutral-light);
    opacity: 0.65;
    line-height: 1.6;
    margin-bottom: 0;
  }

  @media (max-width: 900px) { .two-col { grid-template-columns: 1fr; } }
</style>
