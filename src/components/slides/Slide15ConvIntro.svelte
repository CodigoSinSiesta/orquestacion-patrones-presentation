<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });

  const sources = [
    {
      name: 'Anthropic Engineering',
      role: 'Generator-Evaluator · 12-factor agents · Sprint Contracts',
      color: '#c4b5fd'
    },
    {
      name: 'OpenAI / Lopopolo',
      role: 'Harness Engineering · PNPM 750 packages · Persona-based reviewers',
      color: '#60A5FA'
    },
    {
      name: 'Factory (Missions)',
      role: 'Orchestrator-Workers-Validators · Validation Contracts · 16.5h Slack clone',
      color: '#86efac'
    },
    {
      name: 'Academia (Tsinghua / Stanford)',
      role: 'NLAH +16.8pts · Meta-Harness 6× variance · GRPO multi-agent',
      color: '#fcd34d'
    }
  ];
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="module-tag">
      <span class="tag-dot"></span>
      <span>Módulo C · Convergencias Industria</span>
    </div>

    <h2 class="title">4 fuentes independientes. <span class="hl">Las mismas conclusiones.</span></h2>

    <p class="lead">Cuando una empresa hace una afirmación sobre IA, es una opinión. Cuando 4 fuentes que no se coordinaron llegan a lo mismo, empieza a ser una ley del campo.</p>

    <div class="sources-grid">
      {#each sources as source}
        <div class="source-card" style="--src-color: {source.color}">
          <div class="src-header">
            <span class="src-dot"></span>
            <span class="src-name">{source.name}</span>
          </div>
          <p class="src-role">{source.role}</p>
        </div>
      {/each}
    </div>

    <div class="convergence-preview">
      <p class="cp-label">Las 4 convergencias que emergen:</p>
      <div class="convergences">
        {#each ['Harness > Modelo', 'Separar generación y evaluación', 'Lógica en prompts, no en estado', 'Estado externalizado y estructurado'] as c, i}
          <div class="c-item">
            <span class="c-num">{i + 1}</span>
            <span>{c}</span>
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
    color: #c4b5fd;
  }

  .tag-dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: #a78bfa;
    box-shadow: 0 0 6px rgba(167, 139, 250, 0.6);
  }

  .title {
    font-size: clamp(2rem, 5vw, 3.5rem);
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

  .lead {
    font-size: 1.1rem;
    color: var(--color-neutral-light);
    opacity: 0.7;
    line-height: 1.7;
    max-width: 750px;
    margin-bottom: 0;
  }

  .sources-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: var(--spacing-md);
  }

  .source-card {
    background: rgba(30, 58, 138, 0.1);
    border: 1px solid rgba(var(--src-color), 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
    border-color: color-mix(in srgb, var(--src-color) 30%, transparent);
    transition: background var(--transition-base);
  }

  .source-card:hover {
    background: rgba(30, 58, 138, 0.2);
  }

  .src-header {
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
    margin-bottom: var(--spacing-sm);
  }

  .src-dot {
    width: 8px; height: 8px;
    border-radius: 50%;
    background: var(--src-color);
    flex-shrink: 0;
  }

  .src-name {
    font-family: var(--font-display);
    font-size: 0.95rem;
    font-weight: 700;
    color: var(--color-neutral-light);
  }

  .src-role {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    color: var(--color-neutral-light);
    opacity: 0.5;
    line-height: 1.5;
    margin-bottom: 0;
  }

  .convergence-preview {
    background: rgba(167, 139, 250, 0.07);
    border: 1px solid rgba(167, 139, 250, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg) var(--spacing-xl);
  }

  .cp-label {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    font-weight: 700;
    color: #c4b5fd;
    margin-bottom: var(--spacing-md);
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  .convergences {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: var(--spacing-sm);
  }

  .c-item {
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
    font-size: 0.9rem;
    color: var(--color-neutral-light);
    opacity: 0.75;
  }

  .c-num {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    font-weight: 800;
    color: #a78bfa;
    min-width: 18px;
  }

  @media (max-width: 768px) {
    .sources-grid { grid-template-columns: 1fr; }
    .convergences { grid-template-columns: 1fr; }
  }
</style>
