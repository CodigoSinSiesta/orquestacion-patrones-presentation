<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });

  const conclusions = [
    {
      num: '01',
      title: 'La escalera no se puede saltarse',
      body: 'Cada nivel de complejidad existe porque el anterior tiene un límite real. Saltar niveles por ambición arquitectónica produce deuda técnica disfrazada de sofisticación.',
      color: '#86efac',
      module: 'A'
    },
    {
      num: '02',
      title: 'El evaluador independiente es tu mejor inversión',
      body: 'Un agente que valida su propio trabajo tiene confirmation bias. Añadir un evaluador en contexto separado es la intervención con mejor ROI en calidad del sistema.',
      color: '#fcd34d',
      module: 'B'
    },
    {
      num: '03',
      title: 'Lógica en texto, estado fuera del contexto',
      body: 'La lógica de orquestación en prompts mejora con cada nuevo modelo sin tocar código. El estado en disco permite misiones de semanas. Estos dos principios juntos definen la anti-fragilidad.',
      color: '#60A5FA',
      module: 'B+C'
    },
    {
      num: '04',
      title: 'Anthropic, OpenAI, Factory y academia dicen lo mismo',
      body: 'Las 4 convergencias no son tendencias — son restricciones emergentes del campo. El harness explica más varianza que el modelo. Invertir en arquitectura antes que en benchmarks.',
      color: '#c4b5fd',
      module: 'C'
    }
  ];
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="slide-header">
      <h2 class="title">Lo que se lleva el que estuvo en la sala</h2>
    </div>

    <div class="conclusions-grid">
      {#each conclusions as c}
        <div class="conclusion-card" style="--cc-color: {c.color}">
          <div class="cc-header">
            <span class="cc-num">{c.num}</span>
            <span class="cc-module">Módulo {c.module}</span>
          </div>
          <h3 class="cc-title">{c.title}</h3>
          <p class="cc-body">{c.body}</p>
        </div>
      {/each}
    </div>

    <div class="meta-insight">
      <p class="mi-text">Estos no son patrones de moda. Son respuestas ingenieriles a problemas concretos que aparecen siempre que un agente trabaja en tareas no triviales. El contexto cambia; el problema no.</p>
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

  .title {
    font-size: clamp(1.8rem, 4.5vw, 3.2rem);
    font-weight: 900;
    color: var(--color-neutral-light);
    margin-bottom: 0;
  }

  .conclusions-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: var(--spacing-lg);
  }

  .conclusion-card {
    background: rgba(30, 58, 138, 0.1);
    border: 1px solid color-mix(in srgb, var(--cc-color) 25%, transparent);
    border-radius: var(--radius-md);
    padding: var(--spacing-xl);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-md);
    transition: border-color var(--transition-base), background var(--transition-base);
  }

  .conclusion-card:hover {
    border-color: color-mix(in srgb, var(--cc-color) 50%, transparent);
    background: color-mix(in srgb, var(--cc-color) 5%, transparent);
  }

  .cc-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .cc-num {
    font-family: var(--font-display);
    font-size: 2.5rem;
    font-weight: 900;
    color: var(--cc-color);
    opacity: 0.15;
    line-height: 1;
  }

  .cc-module {
    font-family: var(--font-mono);
    font-size: 0.68rem;
    font-weight: 700;
    color: var(--cc-color);
    opacity: 0.6;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    background: color-mix(in srgb, var(--cc-color) 12%, transparent);
    border: 1px solid color-mix(in srgb, var(--cc-color) 25%, transparent);
    padding: 2px 8px;
    border-radius: 999px;
  }

  .cc-title {
    font-size: 1.05rem;
    font-weight: 700;
    color: var(--color-neutral-light);
    margin-bottom: 0;
    line-height: 1.3;
  }

  .cc-body {
    font-size: 0.875rem;
    color: var(--color-neutral-light);
    opacity: 0.65;
    line-height: 1.65;
    margin-bottom: 0;
    flex: 1;
  }

  .meta-insight {
    background: rgba(96, 165, 250, 0.06);
    border: 1px solid rgba(96, 165, 250, 0.15);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg) var(--spacing-xl);
    border-left: 4px solid rgba(96, 165, 250, 0.4);
  }

  .mi-text {
    font-size: 0.95rem;
    color: var(--color-neutral-light);
    opacity: 0.6;
    line-height: 1.7;
    font-style: italic;
    margin-bottom: 0;
  }

  @media (max-width: 900px) {
    .conclusions-grid { grid-template-columns: 1fr; }
  }
</style>
