<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });

  const problems = [
    { emoji: '🪞', text: 'El agente no detecta sus propios errores' },
    { emoji: '💧', text: 'El contexto se degrada en tareas largas' },
    { emoji: '⚔️', text: 'Los agentes en paralelo se pisan los cambios' },
    { emoji: '🐛', text: 'Los tests no atrapan bugs reales' },
    { emoji: '🦕', text: 'El sistema queda obsoleto con cada modelo' },
    { emoji: '🔭', text: 'Supervisar sin microgestionar' }
  ];
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="module-tag">
      <span class="tag-dot"></span>
      <span>Módulo B · Por Problema que Resuelven</span>
    </div>

    <h2 class="title">Cada patrón nació de un <span class="hl">dolor real</span></h2>

    <p class="lead">
      En lugar de preguntar "¿qué es este patrón?", pregunta "¿cuándo te salva la vida?". El pain es el punto de entrada más honesto a la arquitectura.
    </p>

    <div class="problems-grid">
      {#each problems as p, i}
        <div class="problem-card">
          <span class="problem-emoji">{p.emoji}</span>
          <span class="problem-num">{i + 1}</span>
          <span class="problem-text">{p.text}</span>
          <span class="arrow">→</span>
        </div>
      {/each}
    </div>

    <p class="footer-hint">Los próximos 6 slides cubren cada problema con el patrón que lo resuelve y por qué funciona.</p>
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
    max-width: 1000px;
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
    font-size: 0.78rem;
    font-weight: 700;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: #fcd34d;
  }

  .tag-dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: #f59e0b;
    box-shadow: 0 0 6px rgba(245, 158, 11, 0.6);
  }

  .title {
    font-size: clamp(2rem, 5vw, 3.5rem);
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

  .lead {
    font-size: 1.1rem;
    color: var(--color-neutral-light);
    opacity: 0.7;
    line-height: 1.7;
    max-width: 700px;
    margin-bottom: 0;
  }

  .problems-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: var(--spacing-md);
  }

  .problem-card {
    display: flex;
    align-items: center;
    gap: var(--spacing-md);
    background: rgba(245, 158, 11, 0.06);
    border: 1px solid rgba(245, 158, 11, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
    transition: border-color var(--transition-base), background var(--transition-base);
  }

  .problem-card:hover {
    border-color: rgba(245, 158, 11, 0.5);
    background: rgba(245, 158, 11, 0.1);
  }

  .problem-emoji {
    font-size: 1.5rem;
    flex-shrink: 0;
  }

  .problem-num {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    font-weight: 800;
    color: #f59e0b;
    flex-shrink: 0;
  }

  .problem-text {
    font-size: 0.9rem;
    color: var(--color-neutral-light);
    opacity: 0.8;
    line-height: 1.4;
    flex: 1;
  }

  .arrow {
    color: rgba(245, 158, 11, 0.4);
    font-size: 1.1rem;
    flex-shrink: 0;
  }

  .footer-hint {
    font-family: var(--font-mono);
    font-size: 0.78rem;
    color: var(--color-neutral-light);
    opacity: 0.35;
    letter-spacing: 0.05em;
    text-align: center;
    margin-bottom: 0;
  }

  @media (max-width: 768px) {
    .problems-grid { grid-template-columns: 1fr; }
  }
</style>
