<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="problem-badge">
      <span class="badge-num">Problema 2</span>
      <span class="badge-emoji">💧</span>
    </div>

    <h2 class="title">El contexto se <span class="hl">degrada</span> en tareas largas</h2>

    <div class="two-col">
      <div class="col-problem">
        <h3 class="col-title col-title-prob">El dolor</h3>
        <p>Un agente que trabaja días en la misma sesión acumula ruido en su context window. Los resultados parciales de hace 50 pasos compiten con las instrucciones actuales. La calidad del razonamiento cae de forma no lineal a medida que el contexto crece.</p>
        <div class="degradation-viz">
          <div class="bar-row">
            <span class="bar-label">Turno 1</span>
            <div class="bar"><div class="bar-fill" style="width:95%"></div></div>
            <span class="bar-val">95%</span>
          </div>
          <div class="bar-row">
            <span class="bar-label">Turno 10</span>
            <div class="bar"><div class="bar-fill" style="width:80%"></div></div>
            <span class="bar-val">80%</span>
          </div>
          <div class="bar-row">
            <span class="bar-label">Turno 50</span>
            <div class="bar"><div class="bar-fill" style="width:55%"></div></div>
            <span class="bar-val">55%</span>
          </div>
          <div class="bar-row">
            <span class="bar-label">Turno 200</span>
            <div class="bar"><div class="bar-fill" style="width:30%; background: rgba(248,113,113,0.6)"></div></div>
            <span class="bar-val warn">30%</span>
          </div>
          <p class="viz-caption">Calidad de razonamiento estimada (degradación acumulativa)</p>
        </div>
      </div>

      <div class="col-solution">
        <h3 class="col-title col-title-sol">El patrón: Context Isolation + Structured Handoffs</h3>

        <div class="handoff-diagram">
          <div class="handoff-step">
            <span class="hs-label">Worker A</span>
            <span class="hs-desc">contexto propio · 0 ruido externo</span>
          </div>
          <div class="handoff-arrow">
            <svg width="60" height="24" viewBox="0 0 60 24">
              <line x1="0" y1="12" x2="52" y2="12" stroke="rgba(34,197,94,0.5)" stroke-width="2"/>
              <polyline points="46,6 54,12 46,18" fill="none" stroke="rgba(34,197,94,0.7)" stroke-width="2"/>
            </svg>
            <span class="ha-label">handoff estructurado</span>
          </div>
          <div class="handoff-step">
            <span class="hs-label">Worker B</span>
            <span class="hs-desc">recibe solo lo necesario · contexto fresco</span>
          </div>
        </div>

        <div class="handoff-fields">
          <h4 class="hf-title">Los 5 campos del handoff (Factory)</h4>
          {#each ['objetivo_completado', 'estado_actual_sistema', 'decisiones_tecnicas_tomadas', 'proximos_pasos', 'contexto_critico'] as field}
            <div class="hf-field">
              <span class="hf-dot"></span>
              <code class="hf-name">{field}</code>
            </div>
          {/each}
        </div>

        <p class="solution-note">El handoff no es un resumen informal — es un contrato. El worker siguiente puede arrancar desde 0 con solo esos 5 campos. La misión puede durar semanas.</p>
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

  .problem-badge {
    display: flex;
    align-items: center;
    gap: var(--spacing-md);
  }

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

  .col-problem, .col-solution {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-lg);
  }

  .col-problem p {
    font-size: 0.875rem;
    color: var(--color-neutral-light);
    opacity: 0.7;
    line-height: 1.7;
    margin-bottom: 0;
  }

  .degradation-viz {
    background: rgba(248, 113, 113, 0.05);
    border: 1px solid rgba(248, 113, 113, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
  }

  .bar-row {
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
  }

  .bar-label {
    font-family: var(--font-mono);
    font-size: 0.72rem;
    color: var(--color-neutral-light);
    opacity: 0.5;
    min-width: 65px;
  }

  .bar {
    flex: 1;
    height: 8px;
    background: rgba(30, 58, 138, 0.4);
    border-radius: 4px;
    overflow: hidden;
  }

  .bar-fill {
    height: 100%;
    background: rgba(34, 197, 94, 0.5);
    border-radius: 4px;
    transition: width 0.5s ease;
  }

  .bar-val {
    font-family: var(--font-mono);
    font-size: 0.72rem;
    color: var(--color-electric);
    min-width: 35px;
    text-align: right;
  }

  .bar-val.warn { color: #f87171; }

  .viz-caption {
    font-size: 0.7rem !important;
    color: var(--color-neutral-light) !important;
    opacity: 0.3 !important;
    font-style: italic;
    text-align: center;
    margin-top: var(--spacing-xs);
    margin-bottom: 0 !important;
  }

  .handoff-diagram {
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
    background: rgba(34, 197, 94, 0.05);
    border: 1px solid rgba(34, 197, 94, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
  }

  .handoff-step {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 4px;
    background: rgba(30, 58, 138, 0.3);
    border-radius: var(--radius-sm);
    padding: var(--spacing-md);
    text-align: center;
  }

  .hs-label {
    font-family: var(--font-mono);
    font-size: 0.8rem;
    font-weight: 700;
    color: #86efac;
  }

  .hs-desc {
    font-size: 0.72rem;
    color: var(--color-neutral-light);
    opacity: 0.5;
    line-height: 1.3;
  }

  .handoff-arrow {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2px;
    flex-shrink: 0;
  }

  .ha-label {
    font-size: 0.65rem;
    color: rgba(34, 197, 94, 0.5);
    font-family: var(--font-mono);
    white-space: nowrap;
  }

  .handoff-fields {
    background: rgba(30, 58, 138, 0.1);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
  }

  .hf-title {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    font-weight: 700;
    color: #86efac;
    margin-bottom: var(--spacing-sm);
    letter-spacing: 0.05em;
  }

  .hf-field {
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
  }

  .hf-dot {
    width: 5px;
    height: 5px;
    border-radius: 50%;
    background: rgba(34, 197, 94, 0.5);
    flex-shrink: 0;
  }

  .hf-name {
    font-family: var(--font-mono);
    font-size: 0.8rem;
    color: var(--color-electric);
    opacity: 0.8;
  }

  .solution-note {
    font-size: 0.875rem;
    color: var(--color-neutral-light);
    opacity: 0.6;
    line-height: 1.6;
    font-style: italic;
    margin-bottom: 0;
  }

  @media (max-width: 900px) {
    .two-col { grid-template-columns: 1fr; }
  }
</style>
