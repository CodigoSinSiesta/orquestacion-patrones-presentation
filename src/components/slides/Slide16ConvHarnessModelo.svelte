<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });

  const evidence = [
    {
      source: 'NLAH · Tsinghua 2026',
      finding: '+16.8 puntos de accuracy',
      detail: 'Solo cambiando la representación del harness (código → lenguaje natural). Mismo modelo, misma tarea.',
      color: '#fcd34d'
    },
    {
      source: 'Meta-Harness · Stanford 2026',
      finding: '6× más varianza explicada',
      detail: 'La arquitectura del harness explica 6 veces más la variación en rendimiento que la elección del modelo.',
      color: '#c4b5fd'
    },
    {
      source: 'Factory Missions 2025',
      finding: '16 días → 16.5 horas',
      detail: 'Slack clone completo. 778M tokens, 89% test coverage. El harness define el patrón de éxito.',
      color: '#86efac'
    },
    {
      source: 'Lopopolo · OpenAI 2026',
      finding: '"Toda interacción es fallo del harness"',
      detail: 'Si el agente necesita clarificación humana, el harness no dio suficiente contexto. El problema es siempre la estructura.',
      color: '#60A5FA'
    }
  ];
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="conv-badge">
      <span class="badge-num">Convergencia 1</span>
    </div>

    <h2 class="title"><span class="hl">Harness > Modelo</span></h2>
    <p class="subtitle">La arquitectura que envuelve al LLM determina más el rendimiento que el modelo en sí.</p>

    <div class="evidence-grid">
      {#each evidence as e}
        <div class="evidence-card" style="--ev-color: {e.color}">
          <div class="ev-header">
            <span class="ev-source">{e.source}</span>
          </div>
          <div class="ev-finding">{e.finding}</div>
          <p class="ev-detail">{e.detail}</p>
        </div>
      {/each}
    </div>

    <div class="implication">
      <span class="impl-icon">→</span>
      <p>Implicación práctica: la decisión de <strong>qué modelo usar</strong> es secundaria a la decisión de <strong>cómo estructurar el harness</strong>. Invierte más tiempo en la arquitectura que en el benchmark.</p>
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

  .conv-badge {
    display: inline-flex;
  }

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
    font-size: clamp(2rem, 6vw, 4rem);
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
    font-size: 1.1rem;
    color: var(--color-neutral-light);
    opacity: 0.65;
    line-height: 1.6;
    margin-bottom: 0;
  }

  .evidence-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: var(--spacing-lg);
  }

  .evidence-card {
    background: rgba(30, 58, 138, 0.1);
    border: 1px solid color-mix(in srgb, var(--ev-color) 25%, transparent);
    border-radius: var(--radius-md);
    padding: var(--spacing-xl);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
  }

  .ev-header {
    margin-bottom: 4px;
  }

  .ev-source {
    font-family: var(--font-mono);
    font-size: 0.72rem;
    font-weight: 600;
    color: var(--ev-color);
    letter-spacing: 0.06em;
    opacity: 0.8;
  }

  .ev-finding {
    font-family: var(--font-display);
    font-size: clamp(1.4rem, 2.5vw, 2rem);
    font-weight: 800;
    color: var(--ev-color);
    line-height: 1.2;
  }

  .ev-detail {
    font-size: 0.85rem;
    color: var(--color-neutral-light);
    opacity: 0.6;
    line-height: 1.6;
    margin-bottom: 0;
    flex: 1;
  }

  .implication {
    display: flex;
    gap: var(--spacing-md);
    background: rgba(167, 139, 250, 0.08);
    border: 1px solid rgba(167, 139, 250, 0.25);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg) var(--spacing-xl);
    align-items: flex-start;
  }

  .impl-icon {
    font-size: 1.5rem;
    color: #a78bfa;
    flex-shrink: 0;
    line-height: 1.5;
  }

  .implication p {
    font-size: 0.95rem;
    color: var(--color-neutral-light);
    opacity: 0.7;
    line-height: 1.6;
    margin-bottom: 0;
  }

  @media (max-width: 900px) {
    .evidence-grid { grid-template-columns: 1fr; }
  }
</style>
