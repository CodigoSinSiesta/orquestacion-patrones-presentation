<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="slide-header">
      <p class="label">El mapa del territorio</p>
      <h2 class="title">3 módulos. Una misma conversación.</h2>
      <p class="subtitle">Cada módulo es autosuficiente. Puedes usarlos juntos o por separado según la audiencia.</p>
    </div>

    <div class="modules-grid">
      <div class="module-card mod-a">
        <div class="mod-header">
          <span class="mod-badge">A</span>
          <span class="mod-name">Taxonomía Evolutiva</span>
        </div>
        <p class="mod-desc">El mapa mental completo: 10 patrones en escalera ascendente de complejidad. Cada patrón existe porque el anterior tiene un límite.</p>
        <div class="mod-meta">
          <span class="meta-chip">Desarrolladores</span>
          <span class="meta-chip">Arquitectos</span>
        </div>
        <div class="mod-tesis">
          <span class="tesis-label">Tesis</span>
          <span>La complejidad no es mala — tiene estructura.</span>
        </div>
      </div>

      <div class="module-card mod-b">
        <div class="mod-header">
          <span class="mod-badge">B</span>
          <span class="mod-name">Por Problema</span>
        </div>
        <p class="mod-desc">6 dolores reales → 6 patrones que los resuelven. No "qué es cada patrón" sino "cuándo te salva la vida cada uno".</p>
        <div class="mod-meta">
          <span class="meta-chip">Product Owners</span>
          <span class="meta-chip">Tech Leads</span>
          <span class="meta-chip">Audiencia mixta</span>
        </div>
        <div class="mod-tesis">
          <span class="tesis-label">Tesis</span>
          <span>Cada patrón nació de un pain real. El dolor es el punto de entrada.</span>
        </div>
      </div>

      <div class="module-card mod-c">
        <div class="mod-header">
          <span class="mod-badge">C</span>
          <span class="mod-name">Convergencias</span>
        </div>
        <p class="mod-desc">Anthropic, OpenAI, Factory y la academia llegaron independientemente a las mismas 4 conclusiones. Cuando 4 fuentes convergen, ya no es tendencia.</p>
        <div class="mod-meta">
          <span class="meta-chip">Arquitectos senior</span>
          <span class="meta-chip">Decisores técnicos</span>
        </div>
        <div class="mod-tesis">
          <span class="tesis-label">Tesis</span>
          <span>No son opiniones de una empresa — son leyes emergentes del campo.</span>
        </div>
      </div>
    </div>

    <p class="label label-bottom">Slides 3–22 ↓</p>
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
    max-width: 1200px;
    width: 100%;
    padding: var(--spacing-content);
    padding-top: 5rem;
    display: flex;
    flex-direction: column;
    gap: var(--spacing-2xl);
  }

  .slide-header {
    text-align: center;
  }

  .label {
    font-family: var(--font-mono);
    font-size: 0.8rem;
    font-weight: 600;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--color-electric);
    margin-bottom: var(--spacing-sm);
  }

  .label-bottom {
    text-align: center;
    opacity: 0.4;
    margin-top: 0;
  }

  .title {
    font-size: clamp(1.8rem, 4vw, 3rem);
    font-weight: 800;
    color: var(--color-neutral-light);
    margin-bottom: var(--spacing-md);
  }

  .subtitle {
    font-size: 1.1rem;
    color: var(--color-neutral-light);
    opacity: 0.65;
    margin-bottom: 0;
  }

  .modules-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: var(--spacing-xl);
  }

  .module-card {
    background: rgba(30, 58, 138, 0.1);
    border-radius: var(--radius-lg);
    padding: var(--spacing-xl);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-lg);
    border: 1px solid transparent;
    transition: border-color var(--transition-base), background var(--transition-base);
  }

  .mod-a { border-color: rgba(34, 197, 94, 0.25); }
  .mod-b { border-color: rgba(245, 158, 11, 0.25); }
  .mod-c { border-color: rgba(167, 139, 250, 0.25); }

  .mod-a:hover { background: rgba(34, 197, 94, 0.07); border-color: rgba(34, 197, 94, 0.5); }
  .mod-b:hover { background: rgba(245, 158, 11, 0.07); border-color: rgba(245, 158, 11, 0.5); }
  .mod-c:hover { background: rgba(167, 139, 250, 0.07); border-color: rgba(167, 139, 250, 0.5); }

  .mod-header {
    display: flex;
    align-items: center;
    gap: var(--spacing-md);
  }

  .mod-badge {
    width: 36px;
    height: 36px;
    border-radius: var(--radius-sm);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: var(--font-mono);
    font-size: 1rem;
    font-weight: 800;
    flex-shrink: 0;
  }

  .mod-a .mod-badge { background: rgba(34, 197, 94, 0.2); color: #86efac; }
  .mod-b .mod-badge { background: rgba(245, 158, 11, 0.2); color: #fcd34d; }
  .mod-c .mod-badge { background: rgba(167, 139, 250, 0.2); color: #c4b5fd; }

  .mod-name {
    font-family: var(--font-display);
    font-size: 1.1rem;
    font-weight: 700;
    color: var(--color-neutral-light);
  }

  .mod-desc {
    font-size: 0.95rem;
    color: var(--color-neutral-light);
    opacity: 0.7;
    line-height: 1.6;
    margin-bottom: 0;
    flex: 1;
  }

  .mod-meta {
    display: flex;
    flex-wrap: wrap;
    gap: var(--spacing-xs);
  }

  .meta-chip {
    font-family: var(--font-mono);
    font-size: 0.72rem;
    font-weight: 600;
    padding: 3px 10px;
    border-radius: 999px;
    background: rgba(96, 165, 250, 0.1);
    border: 1px solid rgba(96, 165, 250, 0.2);
    color: var(--color-electric);
    letter-spacing: 0.04em;
  }

  .mod-tesis {
    display: flex;
    gap: var(--spacing-sm);
    font-size: 0.875rem;
    color: var(--color-neutral-light);
    opacity: 0.6;
    font-style: italic;
    line-height: 1.4;
    padding-top: var(--spacing-sm);
    border-top: 1px solid rgba(96, 165, 250, 0.1);
  }

  .tesis-label {
    font-style: normal;
    font-family: var(--font-mono);
    font-size: 0.7rem;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--color-electric);
    opacity: 1;
    flex-shrink: 0;
    padding-top: 1px;
  }

  @media (max-width: 900px) {
    .modules-grid { grid-template-columns: 1fr; }
  }
</style>
