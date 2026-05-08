<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });

  const examples = [
    {
      source: 'Factory Missions',
      mechanism: 'Structured Handoffs',
      how: '5 campos JSON en el handoff. El estado del sistema en un formato que cualquier worker puede consumir sin el contexto histórico.',
      duration: 'Semanas de ejecución'
    },
    {
      source: 'NLAH (Tsinghua)',
      mechanism: 'File-backed State',
      how: 'El estado de la misión se persiste en archivos. Si el agente se reinicia, recupera exactamente donde estaba. Sin perder progreso.',
      duration: 'Días de ejecución'
    },
    {
      source: 'BettaTech Harness',
      mechanism: 'Carpeta progress/ compartida',
      how: 'Los agentes leen y escriben en progress/ como memoria externalizada. El contexto window del agente es efímero; el estado no.',
      duration: 'Proyectos largos'
    },
    {
      source: 'Lopopolo / OpenAI',
      mechanism: 'Git como memoria',
      how: 'El historial de git es el estado externalizado. El agente puede "recordar" decisiones pasadas leyendo commits, sin que ese contexto esté en su ventana.',
      duration: 'Proyectos multi-semana'
    }
  ];
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="conv-badge">
      <span class="badge-num">Convergencia 4</span>
    </div>

    <h2 class="title"><span class="hl">Estado externalizado</span> y estructurado</h2>
    <p class="subtitle">Si el estado vive solo en el context window, el agente no puede trabajar más de unas horas. Si vive fuera, puede trabajar semanas.</p>

    <div class="examples-grid">
      {#each examples as ex}
        <div class="example-card">
          <div class="ex-header">
            <span class="ex-source">{ex.source}</span>
            <span class="ex-duration">{ex.duration}</span>
          </div>
          <div class="ex-mechanism">{ex.mechanism}</div>
          <p class="ex-how">{ex.how}</p>
        </div>
      {/each}
    </div>

    <div class="principle">
      <div class="pr-left">
        <span class="pr-icon">📦</span>
      </div>
      <div>
        <p class="pr-title">El principio</p>
        <p class="pr-text">El context window es RAM — efímero y limitado. El estado externalizado es disco — persistente y sin límite de tamaño. Los sistemas agénticos de larga duración usan el context window como buffer de trabajo, no como almacén de estado.</p>
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

  .conv-badge { display: inline-flex; }

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
    font-size: clamp(1.8rem, 4.5vw, 3.2rem);
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
    font-size: 1rem;
    color: var(--color-neutral-light);
    opacity: 0.6;
    margin-bottom: 0;
  }

  .examples-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: var(--spacing-lg);
  }

  .example-card {
    background: rgba(30, 58, 138, 0.1);
    border: 1px solid rgba(167, 139, 250, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-xl);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
    transition: border-color var(--transition-base), background var(--transition-base);
  }

  .example-card:hover {
    border-color: rgba(167, 139, 250, 0.45);
    background: rgba(167, 139, 250, 0.06);
  }

  .ex-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .ex-source {
    font-family: var(--font-mono);
    font-size: 0.72rem;
    font-weight: 600;
    color: #c4b5fd;
    opacity: 0.7;
    letter-spacing: 0.06em;
  }

  .ex-duration {
    font-family: var(--font-mono);
    font-size: 0.68rem;
    color: var(--color-electric);
    opacity: 0.5;
    background: rgba(96, 165, 250, 0.1);
    padding: 2px 8px;
    border-radius: 999px;
  }

  .ex-mechanism {
    font-family: var(--font-display);
    font-size: 1rem;
    font-weight: 700;
    color: var(--color-neutral-light);
  }

  .ex-how {
    font-size: 0.85rem;
    color: var(--color-neutral-light);
    opacity: 0.6;
    line-height: 1.6;
    margin-bottom: 0;
  }

  .principle {
    display: flex;
    gap: var(--spacing-lg);
    background: rgba(167, 139, 250, 0.07);
    border: 1px solid rgba(167, 139, 250, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg) var(--spacing-xl);
    align-items: flex-start;
  }

  .pr-left { flex-shrink: 0; }
  .pr-icon { font-size: 2rem; line-height: 1; }

  .pr-title {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    font-weight: 700;
    color: #c4b5fd;
    margin-bottom: var(--spacing-xs);
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  .pr-text {
    font-size: 0.9rem;
    color: var(--color-neutral-light);
    opacity: 0.65;
    line-height: 1.7;
    margin-bottom: 0;
  }

  @media (max-width: 900px) {
    .examples-grid { grid-template-columns: 1fr; }
  }
</style>
