<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });

  const matrix = [
    {
      convergence: 'Harness > Modelo',
      anthropic: { check: true, note: 'Generator-Evaluator, Sprint Contracts' },
      openai: { check: true, note: 'Harness Engineering keynote, "toda interacción es fallo del harness"' },
      factory: { check: true, note: 'Missions: 16.5h Slack clone, droid whispering' },
      academia: { check: true, note: 'NLAH +16.8pts, Meta-Harness 6×' }
    },
    {
      convergence: 'Separar Gen/Eval',
      anthropic: { check: true, note: 'Generator + Evaluator en contextos separados' },
      openai: { check: true, note: 'Persona-based reviewer agents, code review en CI' },
      factory: { check: true, note: 'Worker + Validator + Scrutiny Validator' },
      academia: { check: true, note: 'Multi-agent GRPO: roles separados en entrenamiento' }
    },
    {
      convergence: 'Lógica en prompts',
      anthropic: { check: true, note: 'Factor 8 de 12-factor agents' },
      openai: { check: true, note: 'Skills ricas sobre proliferación de código' },
      factory: { check: true, note: '~700 líneas de texto de orquestador, anti-fragilidad' },
      academia: { check: true, note: 'NLAH: execution contracts en lenguaje natural' }
    },
    {
      convergence: 'Estado externalizado',
      anthropic: { check: true, note: 'Checkpointing, handoffs estructurados' },
      openai: { check: true, note: 'Git como memoria, 750 packages PNPM como contexto' },
      factory: { check: true, note: 'Structured Handoffs 5 campos, misiones de semanas' },
      academia: { check: true, note: 'File-backed state (NLAH), progress/ compartida' }
    }
  ];

  const sources = ['Anthropic', 'OpenAI / Lopopolo', 'Factory', 'Academia'];
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="slide-header">
      <div class="module-tag">
        <span class="tag-dot"></span>
        <span>Módulo C · Matriz de convergencias</span>
      </div>
      <h2 class="title">La misma conclusión, 4 veces</h2>
    </div>

    <div class="matrix-table">
      <div class="matrix-header">
        <div class="mh-cell convergence-col">Convergencia</div>
        {#each sources as src}
          <div class="mh-cell">{src}</div>
        {/each}
      </div>

      {#each matrix as row}
        <div class="matrix-row">
          <div class="mr-cell convergence-cell">
            <span class="conv-name">{row.convergence}</span>
          </div>
          {#each [row.anthropic, row.openai, row.factory, row.academia] as cell}
            <div class="mr-cell source-cell">
              <span class="check-mark">✓</span>
              <span class="cell-note">{cell.note}</span>
            </div>
          {/each}
        </div>
      {/each}
    </div>

    <div class="bottom-insight">
      <span class="bi-icon">🎯</span>
      <p>Cuando Anthropic, OpenAI, Factory y la academia llegan independientemente a las mismas 4 conclusiones, dejan de ser recomendaciones y se convierten en restricciones del dominio. No seguirlas no es heterodoxia — es ignorancia.</p>
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
    color: #c4b5fd;
  }

  .tag-dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: #a78bfa;
    box-shadow: 0 0 6px rgba(167, 139, 250, 0.6);
  }

  .title {
    font-size: clamp(1.8rem, 4vw, 2.8rem);
    font-weight: 900;
    color: var(--color-neutral-light);
    margin-bottom: 0;
  }

  .matrix-table {
    display: grid;
    grid-template-rows: auto;
    border: 1px solid rgba(167, 139, 250, 0.2);
    border-radius: var(--radius-md);
    overflow: hidden;
  }

  .matrix-header {
    display: grid;
    grid-template-columns: 200px repeat(4, 1fr);
    background: rgba(167, 139, 250, 0.1);
    border-bottom: 1px solid rgba(167, 139, 250, 0.2);
  }

  .mh-cell {
    padding: var(--spacing-md) var(--spacing-lg);
    font-family: var(--font-mono);
    font-size: 0.72rem;
    font-weight: 700;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: #c4b5fd;
    border-right: 1px solid rgba(167, 139, 250, 0.1);
  }

  .mh-cell:last-child { border-right: none; }

  .convergence-col { color: rgba(250, 249, 246, 0.5); }

  .matrix-row {
    display: grid;
    grid-template-columns: 200px repeat(4, 1fr);
    border-bottom: 1px solid rgba(96, 165, 250, 0.06);
    transition: background var(--transition-fast);
  }

  .matrix-row:last-child { border-bottom: none; }
  .matrix-row:hover { background: rgba(167, 139, 250, 0.04); }

  .mr-cell {
    padding: var(--spacing-md) var(--spacing-lg);
    border-right: 1px solid rgba(96, 165, 250, 0.06);
    display: flex;
    flex-direction: column;
    gap: 4px;
  }

  .mr-cell:last-child { border-right: none; }

  .convergence-cell { justify-content: center; }

  .conv-name {
    font-family: var(--font-body);
    font-size: 0.875rem;
    font-weight: 600;
    color: var(--color-neutral-light);
    line-height: 1.3;
  }

  .source-cell {
    flex-direction: row;
    align-items: flex-start;
    gap: var(--spacing-sm);
  }

  .check-mark {
    font-size: 0.9rem;
    color: #86efac;
    flex-shrink: 0;
    line-height: 1.4;
  }

  .cell-note {
    font-size: 0.72rem;
    color: var(--color-neutral-light);
    opacity: 0.45;
    line-height: 1.4;
  }

  .bottom-insight {
    display: flex;
    gap: var(--spacing-md);
    background: rgba(167, 139, 250, 0.07);
    border: 1px solid rgba(167, 139, 250, 0.25);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg) var(--spacing-xl);
  }

  .bi-icon { font-size: 1.5rem; flex-shrink: 0; }

  .bottom-insight p {
    font-size: 0.9rem;
    color: var(--color-neutral-light);
    opacity: 0.65;
    line-height: 1.6;
    margin-bottom: 0;
  }

  @media (max-width: 900px) {
    .matrix-header, .matrix-row {
      grid-template-columns: 1fr;
    }
    .mh-cell, .mr-cell { border-right: none; }
  }
</style>
