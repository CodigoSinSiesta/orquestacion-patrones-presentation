<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });

  const layers = [
    {
      label: 'CAPA 4 · AUTONOMÍA APRENDIDA',
      color: '#a78bfa',
      bg: 'rgba(167,139,250,0.08)',
      border: 'rgba(167,139,250,0.3)',
      patterns: [{ num: 10, name: 'Puppeteer / RL' }],
      note: 'El orquestador aprende de la historia de ejecución'
    },
    {
      label: 'CAPA 3 · COORDINACIÓN COMPLEJA',
      color: '#60A5FA',
      bg: 'rgba(96,165,250,0.08)',
      border: 'rgba(96,165,250,0.25)',
      patterns: [
        { num: 7, name: 'Hierarchical' },
        { num: 8, name: 'Swarm' },
        { num: 8, name: 'Mesh' },
        { num: 9, name: 'Missions' }
      ],
      note: 'Multi-nivel · topología flexible o fija'
    },
    {
      label: 'CAPA 2 · COORDINACIÓN BÁSICA',
      color: '#22c55e',
      bg: 'rgba(34,197,94,0.06)',
      border: 'rgba(34,197,94,0.25)',
      patterns: [
        { num: 5, name: 'Orchestrator-Workers' },
        { num: 6, name: 'Creator-Verifier' }
      ],
      note: 'Un coordinador, múltiples workers o evaluadores'
    },
    {
      label: 'CAPA 1 · AGENTE SIMPLE',
      color: '#fbbf24',
      bg: 'rgba(251,191,36,0.06)',
      border: 'rgba(251,191,36,0.25)',
      patterns: [
        { num: 1, name: 'ReAct' },
        { num: 2, name: 'Reflexion' },
        { num: 3, name: 'Pipeline' },
        { num: 4, name: 'Routing' }
      ],
      note: 'Topología fija · sin coordinador dinámico'
    }
  ];
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="slide-header">
      <div class="module-tag">
        <span class="tag-dot"></span>
        <span>Módulo A · Las 4 capas de complejidad</span>
      </div>
      <h2 class="title">El mapa completo</h2>
    </div>

    <div class="diagram">
      {#each layers as layer}
        <div class="layer" style="--layer-color: {layer.color}; --layer-bg: {layer.bg}; --layer-border: {layer.border}">
          <div class="layer-label">{layer.label}</div>
          <div class="layer-patterns">
            {#each layer.patterns as p}
              <div class="pattern-chip">
                <span class="p-num">{p.num}</span>
                <span class="p-name">{p.name}</span>
              </div>
            {/each}
          </div>
          <div class="layer-note">{layer.note}</div>
        </div>
      {/each}

      <div class="arrow-up">
        <svg width="24" height="120" viewBox="0 0 24 120">
          <line x1="12" y1="110" x2="12" y2="10" stroke="rgba(96,165,250,0.4)" stroke-width="2" stroke-dasharray="4 4"/>
          <polyline points="6,14 12,4 18,14" fill="none" stroke="rgba(96,165,250,0.6)" stroke-width="2"/>
        </svg>
        <span class="arrow-label">Complejidad · Coordinación · Coste</span>
      </div>
    </div>

    <div class="bottom-rule">
      <span class="rule-icon">⚡</span>
      <p>Regla de oro: usa la capa más baja que resuelve tu problema. Cada capa añade overhead de coordinación que no se recupera si no lo necesitas.</p>
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
    max-width: 1000px;
    width: 100%;
    padding: var(--spacing-content);
    padding-top: 4rem;
    display: flex;
    flex-direction: column;
    gap: var(--spacing-xl);
  }

  .slide-header { display: flex; flex-direction: column; gap: var(--spacing-md); }

  .module-tag {
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
    font-family: var(--font-mono);
    font-size: 0.78rem;
    font-weight: 700;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: #86efac;
  }

  .tag-dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: #22c55e;
    box-shadow: 0 0 6px rgba(34, 197, 94, 0.6);
  }

  .title {
    font-size: clamp(1.8rem, 4vw, 2.8rem);
    font-weight: 900;
    color: var(--color-neutral-light);
    margin-bottom: 0;
  }

  .diagram {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
    position: relative;
  }

  .layer {
    background: var(--layer-bg);
    border: 1px solid var(--layer-border);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg) var(--spacing-xl);
    display: grid;
    grid-template-columns: auto 1fr auto;
    gap: var(--spacing-lg);
    align-items: center;
  }

  .layer-label {
    font-family: var(--font-mono);
    font-size: 0.72rem;
    font-weight: 700;
    letter-spacing: 0.1em;
    color: var(--layer-color);
    min-width: 200px;
  }

  .layer-patterns {
    display: flex;
    flex-wrap: wrap;
    gap: var(--spacing-sm);
  }

  .pattern-chip {
    display: flex;
    align-items: center;
    gap: 6px;
    background: rgba(30, 58, 138, 0.3);
    border: 1px solid rgba(96, 165, 250, 0.15);
    border-radius: 999px;
    padding: 4px 12px;
  }

  .p-num {
    font-family: var(--font-mono);
    font-size: 0.7rem;
    font-weight: 800;
    color: var(--layer-color);
  }

  .p-name {
    font-size: 0.82rem;
    color: var(--color-neutral-light);
    opacity: 0.8;
  }

  .layer-note {
    font-size: 0.78rem;
    color: var(--color-neutral-light);
    opacity: 0.45;
    font-style: italic;
    text-align: right;
    min-width: 200px;
  }

  .arrow-up {
    position: absolute;
    right: -40px;
    top: 0;
    bottom: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: var(--spacing-sm);
  }

  .arrow-label {
    font-family: var(--font-mono);
    font-size: 0.65rem;
    font-weight: 600;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: rgba(96, 165, 250, 0.5);
    writing-mode: vertical-rl;
    text-orientation: mixed;
    transform: rotate(180deg);
  }

  .bottom-rule {
    display: flex;
    gap: var(--spacing-md);
    background: rgba(251, 191, 36, 0.07);
    border: 1px solid rgba(251, 191, 36, 0.25);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
  }

  .rule-icon { font-size: 1.25rem; flex-shrink: 0; }

  .bottom-rule p {
    font-size: 0.9rem;
    color: var(--color-neutral-light);
    opacity: 0.7;
    line-height: 1.5;
    margin-bottom: 0;
  }

  @media (max-width: 768px) {
    .layer { grid-template-columns: 1fr; }
    .layer-note { text-align: left; }
    .arrow-up { display: none; }
  }
</style>
