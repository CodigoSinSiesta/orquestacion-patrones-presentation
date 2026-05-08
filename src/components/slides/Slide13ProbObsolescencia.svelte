<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="problem-badge">
      <span class="badge-num">Problema 5</span>
      <span class="badge-emoji">🦕</span>
    </div>

    <h2 class="title">El sistema queda obsoleto con <span class="hl">cada nuevo modelo</span></h2>

    <div class="two-col">
      <div class="col-problem">
        <h3 class="col-title col-title-prob">El dolor</h3>
        <p>Si tu lógica de orquestación está hardcodeada en una state machine — "si output contiene X, haz Y, sino Z" — tienes que reescribirla cada vez que cambias de modelo. El modelo mejora sus capacidades y tu código no sabe aprovecharlo.</p>
        <div class="brittle-box">
          <p class="bb-title">Orquestación frágil (state machine)</p>
          <pre class="code-block">if (output.includes('error')) &#123;
  retryStrategy = 'exponential';
&#125; else if (confidence &lt; 0.7) &#123;
  escalate('human');  // hardcoded threshold
&#125;</pre>
          <p class="bb-note">Cuando GPT-5 / Claude 5 salgan, estos thresholds son basura.</p>
        </div>
      </div>

      <div class="col-solution">
        <h3 class="col-title col-title-sol">El patrón: lógica en prompts (Factor 8)</h3>

        <div class="prompts-box">
          <p class="pb-title">Orquestación anti-frágil (lógica en texto)</p>
          <div class="prompt-example">
            <p>"Si detectas que la implementación tiene baja cobertura de edge cases, genera tests adicionales antes de marcar la tarea como completa. Si encuentras un error de compilación, intenta corregirlo hasta 3 veces antes de escalar al orchestrator."</p>
          </div>
          <p class="pb-note">Un modelo mejor entiende mejor estas instrucciones. No hay código que actualizar.</p>
        </div>

        <div class="principles">
          <div class="principle">
            <span class="p-icon">📝</span>
            <div>
              <p class="p-title">Las Missions de Factory: ~700 líneas de texto</p>
              <p class="p-desc">La lógica del orquestador está en prompts, no en código. Cada release de modelo la mejora gratis.</p>
            </div>
          </div>
          <div class="principle">
            <span class="p-icon">🔧</span>
            <div>
              <p class="p-title">12-factor agents, Factor 8</p>
              <p class="p-desc">"Codifica la lógica de negocio en prompts, no en state machines. El modelo es el intérprete."</p>
            </div>
          </div>
        </div>
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

  .problem-badge { display: flex; align-items: center; gap: var(--spacing-md); }

  .badge-num {
    font-family: var(--font-mono);
    font-size: 0.78rem;
    font-weight: 700;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: #fcd34d;
    background: rgba(245, 158, 11, 0.12);
    border: 1px solid rgba(245, 158, 11, 0.3);
    padding: 4px 12px;
    border-radius: 999px;
  }

  .badge-emoji { font-size: 1.5rem; }

  .title {
    font-size: clamp(1.8rem, 4vw, 3rem);
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

  .two-col {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: var(--spacing-2xl);
    align-items: start;
  }

  .col-title {
    font-size: 0.85rem;
    font-weight: 700;
    margin-bottom: var(--spacing-md);
    font-family: var(--font-mono);
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  .col-title-prob { color: #f87171; }
  .col-title-sol { color: #86efac; }

  .col-problem, .col-solution { display: flex; flex-direction: column; gap: var(--spacing-lg); }

  .col-problem p {
    font-size: 0.875rem;
    color: var(--color-neutral-light);
    opacity: 0.7;
    line-height: 1.7;
    margin-bottom: 0;
  }

  .brittle-box {
    background: rgba(248, 113, 113, 0.06);
    border: 1px solid rgba(248, 113, 113, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
  }

  .bb-title, .pb-title {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    font-weight: 700;
    margin-bottom: var(--spacing-xs);
  }

  .bb-title { color: #f87171; }
  .pb-title { color: #86efac; }

  .code-block {
    font-family: var(--font-mono);
    font-size: 0.78rem;
    color: var(--color-neutral-light);
    opacity: 0.65;
    background: rgba(10, 22, 40, 0.5);
    border-radius: var(--radius-sm);
    padding: var(--spacing-md);
    overflow-x: auto;
    white-space: pre;
    line-height: 1.6;
  }

  .bb-note, .pb-note {
    font-size: 0.78rem;
    color: var(--color-neutral-light);
    opacity: 0.45;
    font-style: italic;
    margin-bottom: 0;
  }

  .prompts-box {
    background: rgba(34, 197, 94, 0.06);
    border: 1px solid rgba(34, 197, 94, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
  }

  .prompt-example {
    background: rgba(10, 22, 40, 0.5);
    border-radius: var(--radius-sm);
    padding: var(--spacing-md);
    border-left: 3px solid rgba(34, 197, 94, 0.4);
  }

  .prompt-example p {
    font-size: 0.85rem !important;
    color: var(--color-neutral-light) !important;
    opacity: 0.75 !important;
    line-height: 1.6 !important;
    font-style: italic;
    margin-bottom: 0 !important;
  }

  .principles {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-md);
  }

  .principle {
    display: flex;
    gap: var(--spacing-md);
    background: rgba(30, 58, 138, 0.15);
    border-radius: var(--radius-sm);
    padding: var(--spacing-md) var(--spacing-lg);
  }

  .p-icon { font-size: 1.2rem; flex-shrink: 0; }

  .p-title {
    font-size: 0.85rem;
    font-weight: 600;
    color: var(--color-neutral-light);
    margin-bottom: 2px;
  }

  .p-desc {
    font-size: 0.78rem;
    color: var(--color-neutral-light);
    opacity: 0.5;
    line-height: 1.4;
    margin-bottom: 0;
  }

  @media (max-width: 900px) { .two-col { grid-template-columns: 1fr; } }
</style>
