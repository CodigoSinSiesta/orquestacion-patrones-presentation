<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });

  const levels = [
    {
      num: 1,
      name: 'Single Agent · ReAct',
      desc: 'Un LLM en bucle Thought → Action → Observation. La unidad mínima de agente. Razona sobre su propia acción antes de ejecutarla.',
      cuando_subir: 'El agente no reconoce sus propios errores y no aprende entre intentos.',
      tech: 'Yao et al. 2022 · HotPotQA +20% vs CoT'
    },
    {
      num: 2,
      name: 'Reflexion',
      desc: 'El agente genera una crítica verbal de su propio intento antes del siguiente. Sin cambiar los pesos — solo razonando sobre qué falló.',
      cuando_subir: 'La tarea requiere descomposición en etapas con responsabilidades distintas.',
      tech: 'Shinn et al. 2023 · HumanEval 91% pass@1'
    },
    {
      num: 3,
      name: 'Pipeline Agéntico',
      desc: 'Secuencia fija de agentes especializados: A → B → C. Topología definida antes de la ejecución. El output de cada etapa es el input de la siguiente.',
      cuando_subir: 'El input llega de múltiples tipos y cada tipo necesita un agente distinto.',
      tech: 'ETL agéntico · CI/CD agéntico · procesamiento de documentos'
    },
    {
      num: 4,
      name: 'Routing',
      desc: 'Un clasificador inicial decide a qué agente especializado dirigir el input. Sin coordinador dinámico — la decisión es puntual y unidireccional.',
      cuando_subir: 'Un coordinador necesita adaptar el plan en función de los resultados parciales.',
      tech: 'Embedding similarity 50ms · LLM-based 1-2s · cascading'
    }
  ];
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="slide-header">
      <div class="module-tag">
        <span class="tag-dot"></span>
        <span>Módulo A · Niveles 1–4 · La base</span>
      </div>
      <h2 class="title">El agente aprende a trabajar <span class="hl">con otros</span></h2>
    </div>

    <div class="levels-grid">
      {#each levels as level}
        <div class="level-card">
          <div class="level-header">
            <span class="level-num">{level.num}</span>
            <span class="level-name">{level.name}</span>
          </div>
          <p class="level-desc">{level.desc}</p>
          <div class="level-footer">
            <div class="trigger">
              <span class="trigger-label">↑ Sube cuando</span>
              <span class="trigger-text">{level.cuando_subir}</span>
            </div>
            <div class="tech-tag">{level.tech}</div>
          </div>
        </div>
      {/each}
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
    color: #86efac;
  }

  .tag-dot {
    width: 7px;
    height: 7px;
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

  .hl {
    background: linear-gradient(135deg, #22c55e, #60A5FA);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .levels-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: var(--spacing-lg);
  }

  .level-card {
    background: rgba(30, 58, 138, 0.1);
    border: 1px solid rgba(34, 197, 94, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-xl);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-md);
    transition: border-color var(--transition-base), background var(--transition-base);
  }

  .level-card:hover {
    border-color: rgba(34, 197, 94, 0.5);
    background: rgba(34, 197, 94, 0.05);
  }

  .level-header {
    display: flex;
    align-items: center;
    gap: var(--spacing-md);
  }

  .level-num {
    width: 32px;
    height: 32px;
    border-radius: var(--radius-sm);
    background: rgba(34, 197, 94, 0.2);
    border: 1px solid rgba(34, 197, 94, 0.4);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: var(--font-mono);
    font-size: 0.9rem;
    font-weight: 800;
    color: #86efac;
    flex-shrink: 0;
  }

  .level-name {
    font-family: var(--font-display);
    font-size: 1.05rem;
    font-weight: 700;
    color: var(--color-neutral-light);
  }

  .level-desc {
    font-size: 0.9rem;
    color: var(--color-neutral-light);
    opacity: 0.7;
    line-height: 1.6;
    margin-bottom: 0;
    flex: 1;
  }

  .level-footer {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
    padding-top: var(--spacing-sm);
    border-top: 1px solid rgba(96, 165, 250, 0.1);
  }

  .trigger {
    display: flex;
    flex-direction: column;
    gap: 2px;
  }

  .trigger-label {
    font-family: var(--font-mono);
    font-size: 0.7rem;
    font-weight: 700;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: #f59e0b;
    opacity: 0.9;
  }

  .trigger-text {
    font-size: 0.82rem;
    color: var(--color-neutral-light);
    opacity: 0.6;
    line-height: 1.4;
    font-style: italic;
  }

  .tech-tag {
    font-family: var(--font-mono);
    font-size: 0.72rem;
    color: var(--color-electric);
    opacity: 0.55;
  }

  @media (max-width: 900px) {
    .levels-grid { grid-template-columns: 1fr; }
  }
</style>
