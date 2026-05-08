<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="conv-badge">
      <span class="badge-num">Convergencia 3</span>
    </div>

    <h2 class="title"><span class="hl">Lógica en prompts,</span> no en estado</h2>
    <p class="subtitle">Un sistema frágil requiere reescritura con cada nuevo modelo. Un sistema anti-frágil mejora solo.</p>

    <div class="comparison">
      <div class="col col-fragile">
        <h3 class="col-title">Sistema frágil</h3>
        <div class="code-block">
          <p class="code-comment">// Orchestrator hardcodeado</p>
          <p class="code-line">if (confidence &lt; 0.75) &#123;</p>
          <p class="code-line indent">retry(3);</p>
          <p class="code-line">&#125; else if (error_type == 'auth') &#123;</p>
          <p class="code-line indent">escalate('human');</p>
          <p class="code-line">&#125;</p>
        </div>
        <div class="fragile-problems">
          <p class="prob-item">❌ Claude 5 sube baseline → thresholds son incorrectos</p>
          <p class="prob-item">❌ Nueva categoría de error → reescribir código</p>
          <p class="prob-item">❌ Cada release de modelo requiere QA completo</p>
        </div>
      </div>

      <div class="col-arrow">→</div>

      <div class="col col-antifragile">
        <h3 class="col-title">Sistema anti-frágil</h3>
        <div class="prompt-block">
          <p>"Si el resultado no cumple los criterios del Validation Contract, genera una descripción específica de por qué falló y reintenta con ese contexto. Si tras 3 intentos no converge, escala al orchestrator con un análisis de la causa raíz."</p>
        </div>
        <div class="antifragile-benefits">
          <p class="benefit-item">✓ Claude 5 entiende mejor estas instrucciones → mejora gratis</p>
          <p class="benefit-item">✓ Nueva situación → el modelo la maneja con razonamiento</p>
          <p class="benefit-item">✓ Sin código que actualizar con cada release</p>
        </div>
      </div>
    </div>

    <div class="evidence-row">
      <div class="ev-item">
        <span class="ev-src">Factory Missions</span>
        <span class="ev-fact">~700 líneas de texto de lógica de orquestador</span>
      </div>
      <div class="ev-item">
        <span class="ev-src">12-factor agents (Factor 8)</span>
        <span class="ev-fact">"El modelo es el intérprete, no el estado"</span>
      </div>
      <div class="ev-item">
        <span class="ev-src">NLAH (Tsinghua)</span>
        <span class="ev-fact">Execution contracts en lenguaje natural → +16.8pts</span>
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

  .comparison {
    display: grid;
    grid-template-columns: 1fr auto 1fr;
    gap: var(--spacing-lg);
    align-items: start;
  }

  .col { display: flex; flex-direction: column; gap: var(--spacing-md); }

  .col-title {
    font-family: var(--font-mono);
    font-size: 0.85rem;
    font-weight: 700;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    margin-bottom: 0;
  }

  .col-fragile .col-title { color: #f87171; }
  .col-antifragile .col-title { color: #86efac; }

  .col-arrow {
    font-size: 1.5rem;
    color: rgba(167, 139, 250, 0.4);
    display: flex;
    align-items: center;
    padding-top: 3rem;
  }

  .code-block {
    background: rgba(248, 113, 113, 0.07);
    border: 1px solid rgba(248, 113, 113, 0.2);
    border-radius: var(--radius-sm);
    padding: var(--spacing-lg);
  }

  .code-comment {
    font-family: var(--font-mono);
    font-size: 0.78rem;
    color: rgba(96, 165, 250, 0.4);
    margin-bottom: 4px;
  }

  .code-line {
    font-family: var(--font-mono);
    font-size: 0.78rem;
    color: var(--color-neutral-light);
    opacity: 0.65;
    line-height: 1.7;
    margin-bottom: 0;
  }

  .code-line.indent { padding-left: 16px; }

  .fragile-problems {
    display: flex;
    flex-direction: column;
    gap: 4px;
  }

  .prob-item {
    font-size: 0.8rem;
    color: #f87171;
    opacity: 0.75;
    margin-bottom: 0;
    line-height: 1.5;
  }

  .prompt-block {
    background: rgba(34, 197, 94, 0.07);
    border: 1px solid rgba(34, 197, 94, 0.2);
    border-left: 3px solid rgba(34, 197, 94, 0.5);
    border-radius: 0 var(--radius-sm) var(--radius-sm) 0;
    padding: var(--spacing-lg);
  }

  .prompt-block p {
    font-size: 0.85rem;
    color: var(--color-neutral-light);
    opacity: 0.75;
    line-height: 1.7;
    font-style: italic;
    margin-bottom: 0;
  }

  .antifragile-benefits {
    display: flex;
    flex-direction: column;
    gap: 4px;
  }

  .benefit-item {
    font-size: 0.8rem;
    color: #86efac;
    opacity: 0.75;
    margin-bottom: 0;
    line-height: 1.5;
  }

  .evidence-row {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: var(--spacing-md);
    padding-top: var(--spacing-sm);
    border-top: 1px solid rgba(167, 139, 250, 0.1);
  }

  .ev-item {
    display: flex;
    flex-direction: column;
    gap: 4px;
  }

  .ev-src {
    font-family: var(--font-mono);
    font-size: 0.7rem;
    font-weight: 700;
    color: #c4b5fd;
    opacity: 0.7;
    letter-spacing: 0.06em;
  }

  .ev-fact {
    font-size: 0.82rem;
    color: var(--color-neutral-light);
    opacity: 0.55;
    line-height: 1.4;
  }

  @media (max-width: 900px) {
    .comparison { grid-template-columns: 1fr; }
    .col-arrow { display: none; }
    .evidence-row { grid-template-columns: 1fr; }
  }
</style>
