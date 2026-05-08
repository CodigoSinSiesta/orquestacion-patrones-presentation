<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="module-tag">
      <span class="tag-dot mod-a-dot"></span>
      <span>Módulo A · Taxonomía Evolutiva</span>
    </div>

    <h2 class="title">La escalera de <span class="hl-green">complejidad</span></h2>

    <p class="lead">
      Cada patrón existe porque el anterior tiene un límite. No son opciones paralelas — son niveles de una escalera. Subir no siempre es mejor; subir cuando lo necesitas es obligatorio.
    </p>

    <div class="insight-grid">
      <div class="insight-card">
        <span class="insight-icon">🎯</span>
        <div>
          <p class="insight-title">La pregunta correcta</p>
          <p class="insight-desc">No "¿qué patrón uso?" sino "¿cuál es el límite del que tengo ahora y cuándo lo voy a golpear?"</p>
        </div>
      </div>
      <div class="insight-card">
        <span class="insight-icon">📐</span>
        <div>
          <p class="insight-title">10 niveles, 4 capas</p>
          <p class="insight-desc">Desde un único agente con ReAct hasta un orquestador entrenado con RL. Cada capa añade coordinación, y coordinación tiene coste.</p>
        </div>
      </div>
      <div class="insight-card">
        <span class="insight-icon">⚠️</span>
        <div>
          <p class="insight-title">El error más común</p>
          <p class="insight-desc">Saltarse niveles por "ambición arquitectónica". Un Orchestrator-Workers para un problema de Routing es deuda técnica disfrazada de sofisticación.</p>
        </div>
      </div>
    </div>

    <div class="preview-ladder">
      <div class="ladder-mini">
        {#each ['Single Agent ReAct', 'Reflexion', 'Pipeline', 'Routing', 'Orchestrator-Workers', 'Creator-Verifier', 'Hierarchical', 'Swarm / Mesh', 'Missions', 'Puppeteer RL'] as step, i}
          <div class="step" style="opacity: {0.3 + i * 0.07}; transform: translateX({i * 4}px)">
            <span class="step-num">{i + 1}</span>
            <span class="step-name">{step}</span>
          </div>
        {/each}
      </div>
    </div>
  </div>
</div>

<style>
  .swiper-slide {
    width: 100%;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background: var(--color-base-dark);
  }

  .slide-content {
    max-width: 1100px;
    width: 100%;
    padding: var(--spacing-content);
    padding-top: 5rem;
    display: flex;
    flex-direction: column;
    gap: var(--spacing-xl);
  }

  .module-tag {
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
    font-family: var(--font-mono);
    font-size: 0.8rem;
    font-weight: 700;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: #86efac;
  }

  .tag-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
  }

  .mod-a-dot { background: #22c55e; box-shadow: 0 0 8px rgba(34, 197, 94, 0.6); }

  .title {
    font-size: clamp(2rem, 5vw, 3.5rem);
    font-weight: 900;
    color: var(--color-neutral-light);
    margin-bottom: 0;
  }

  .hl-green {
    background: linear-gradient(135deg, #22c55e, #86efac);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .lead {
    font-size: 1.2rem;
    color: var(--color-neutral-light);
    opacity: 0.75;
    line-height: 1.7;
    max-width: 750px;
    margin-bottom: 0;
  }

  .insight-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: var(--spacing-lg);
  }

  .insight-card {
    display: flex;
    gap: var(--spacing-md);
    background: rgba(34, 197, 94, 0.06);
    border: 1px solid rgba(34, 197, 94, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
  }

  .insight-icon {
    font-size: 1.5rem;
    flex-shrink: 0;
    line-height: 1;
    margin-top: 2px;
  }

  .insight-title {
    font-family: var(--font-display);
    font-size: 0.95rem;
    font-weight: 700;
    color: #86efac;
    margin-bottom: var(--spacing-xs);
  }

  .insight-desc {
    font-size: 0.875rem;
    color: var(--color-neutral-light);
    opacity: 0.65;
    line-height: 1.5;
    margin-bottom: 0;
  }

  .preview-ladder {
    background: rgba(30, 58, 138, 0.15);
    border: 1px solid rgba(34, 197, 94, 0.15);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg) var(--spacing-xl);
  }

  .ladder-mini {
    display: flex;
    flex-direction: column;
    gap: 4px;
  }

  .step {
    display: flex;
    align-items: center;
    gap: var(--spacing-md);
    padding: 4px 0;
  }

  .step-num {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    font-weight: 700;
    color: #22c55e;
    min-width: 20px;
  }

  .step-name {
    font-family: var(--font-body);
    font-size: 0.875rem;
    color: var(--color-neutral-light);
  }

  @media (max-width: 768px) {
    .insight-grid { grid-template-columns: 1fr; }
  }
</style>
