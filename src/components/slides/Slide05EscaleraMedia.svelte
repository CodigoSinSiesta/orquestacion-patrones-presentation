<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });

  const levels = [
    {
      num: 5,
      name: 'Orchestrator-Workers',
      desc: 'Un LLM central descompone la tarea, delega a workers especializados y sintetiza los resultados. La topología emerge en runtime según el input.',
      cuando_subir: 'Necesitas verificación independiente: el mismo agente no puede evaluar su propio trabajo de forma fiable.',
      tech: 'El patrón más adoptado en producción 2024-2025. Bottleneck: el orchestrator serializa todo.'
    },
    {
      num: 6,
      name: 'Creator-Verifier',
      desc: 'Dos agentes con roles opuestos: uno genera, otro evalúa en contexto separado. El evaluador no tiene acceso al razonamiento del generador — solo al output.',
      cuando_subir: 'La tarea requiere coordinación jerárquica: orquestadores que coordinan a otros orquestadores.',
      tech: 'Anthropic llama a esto "Generator-Evaluator". Factory lo llama "Worker-Validator". Misma idea.'
    },
    {
      num: 7,
      name: 'Hierarchical + Broadcast',
      desc: 'Árbol de agentes: un root-orchestrator coordina sub-orquestadores que a su vez coordinan workers. Broadcast permite notificar a múltiples ramas en paralelo.',
      cuando_subir: 'La coordinación centralizada se convierte en cuello de botella: el orchestrator no puede seguir el ritmo de los workers.',
      tech: 'LangGraph, CrewAI, AutoGen. Coste alto de coordinación — solo cuando lo justifica la escala.'
    }
  ];
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="slide-header">
      <div class="module-tag">
        <span class="tag-dot"></span>
        <span>Módulo A · Niveles 5–7 · Coordinación</span>
      </div>
      <h2 class="title">La coordinación se hace <span class="hl">explícita</span></h2>
    </div>

    <div class="levels-stack">
      {#each levels as level}
        <div class="level-card">
          <div class="level-left">
            <span class="level-num">{level.num}</span>
            <div class="connector"></div>
          </div>
          <div class="level-body">
            <h3 class="level-name">{level.name}</h3>
            <p class="level-desc">{level.desc}</p>
            <div class="level-footer">
              <div class="trigger">
                <span class="trigger-label">↑ Sube cuando</span>
                <span class="trigger-text">{level.cuando_subir}</span>
              </div>
              <div class="tech-tag">{level.tech}</div>
            </div>
          </div>
        </div>
      {/each}
    </div>

    <div class="key-insight">
      <span class="ki-icon">💡</span>
      <p>El Creator-Verifier es el patrón más subvalorado: añadir un evaluador independiente es la intervención con mejor ROI en calidad del output de cualquier sistema agéntico.</p>
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

  .levels-stack {
    display: flex;
    flex-direction: column;
    gap: 0;
  }

  .level-card {
    display: flex;
    gap: var(--spacing-lg);
    padding: var(--spacing-xl) 0;
    border-bottom: 1px solid rgba(96, 165, 250, 0.08);
  }

  .level-left {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: var(--spacing-sm);
    flex-shrink: 0;
  }

  .level-num {
    width: 36px;
    height: 36px;
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
  }

  .connector {
    width: 2px;
    flex: 1;
    background: linear-gradient(to bottom, rgba(34, 197, 94, 0.3), transparent);
    min-height: 20px;
  }

  .level-body {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
  }

  .level-name {
    font-size: 1.1rem;
    font-weight: 700;
    color: var(--color-neutral-light);
    margin-bottom: 0;
  }

  .level-desc {
    font-size: 0.9rem;
    color: var(--color-neutral-light);
    opacity: 0.7;
    line-height: 1.6;
    margin-bottom: 0;
  }

  .level-footer {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-xs);
  }

  .trigger {
    display: flex;
    gap: var(--spacing-sm);
    align-items: flex-start;
  }

  .trigger-label {
    font-family: var(--font-mono);
    font-size: 0.7rem;
    font-weight: 700;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: #f59e0b;
    flex-shrink: 0;
    padding-top: 1px;
  }

  .trigger-text {
    font-size: 0.82rem;
    color: var(--color-neutral-light);
    opacity: 0.55;
    line-height: 1.4;
    font-style: italic;
  }

  .tech-tag {
    font-family: var(--font-mono);
    font-size: 0.72rem;
    color: var(--color-electric);
    opacity: 0.5;
  }

  .key-insight {
    display: flex;
    gap: var(--spacing-md);
    background: rgba(34, 197, 94, 0.07);
    border: 1px solid rgba(34, 197, 94, 0.25);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
  }

  .ki-icon { font-size: 1.5rem; flex-shrink: 0; }

  .key-insight p {
    font-size: 0.95rem;
    color: var(--color-neutral-light);
    opacity: 0.75;
    line-height: 1.6;
    margin-bottom: 0;
  }
</style>
