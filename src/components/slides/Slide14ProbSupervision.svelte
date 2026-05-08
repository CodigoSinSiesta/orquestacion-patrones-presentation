<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="problem-badge">
      <span class="badge-num">Problema 6</span>
      <span class="badge-emoji">🔭</span>
    </div>

    <h2 class="title">Supervisar a los agentes <span class="hl">sin microgestionar</span></h2>

    <div class="two-col">
      <div class="col-problem">
        <h3 class="col-title col-title-prob">El dolor</h3>
        <p>El pendulo oscila entre dos extremos igual de malos: aprobar cada acción (el agente pierde todo su valor) o no supervisar nada (el agente causa daños antes de que alguien los vea).</p>

        <div class="spectrum-viz">
          <div class="spectrum-bar">
            <div class="spec-label left">Sin supervisión</div>
            <div class="spec-track">
              <div class="spec-dot bad-left"></div>
              <div class="spec-dot bad-right"></div>
            </div>
            <div class="spec-label right">Micro-gestión</div>
          </div>
          <div class="spec-problems">
            <span class="sp bad">Daños antes de detectar</span>
            <span class="sp bad">Agente inútil</span>
          </div>
        </div>

        <p>La solución no es un punto fijo en el espectro — es supervisión dinámica orientada a riesgo.</p>
      </div>

      <div class="col-solution">
        <h3 class="col-title col-title-sol">El patrón: HITL/HOTL + Mission Control</h3>

        <div class="tiers">
          <div class="tier tier-auto">
            <div class="tier-header">
              <span class="tier-label">Automatización completa</span>
              <span class="tier-badge">Bajo riesgo</span>
            </div>
            <p class="tier-example">tests, lint, formatting, operaciones de lectura</p>
          </div>
          <div class="tier tier-hotl">
            <div class="tier-header">
              <span class="tier-label">Human-on-the-Loop</span>
              <span class="tier-badge tier-badge-mid">Riesgo medio</span>
            </div>
            <p class="tier-example">commits, PRs, mensajes a usuarios, deploys a staging</p>
          </div>
          <div class="tier tier-hitl">
            <div class="tier-header">
              <span class="tier-label">Human-in-the-Loop</span>
              <span class="tier-badge tier-badge-high">Alto riesgo</span>
            </div>
            <p class="tier-example">producción, datos sensibles, acciones irreversibles</p>
          </div>
        </div>

        <div class="decision-rule">
          <p class="dr-title">Marco de decisión rápida</p>
          <div class="dr-item">
            <span class="dr-q">¿Es irreversible?</span>
            <span class="dr-a">→ HITL obligatorio</span>
          </div>
          <div class="dr-item">
            <span class="dr-q">¿Afecta a terceros?</span>
            <span class="dr-a">→ HITL o HOTL según regulación</span>
          </div>
          <div class="dr-item">
            <span class="dr-q">¿Cuánto daño si se equivoca?</span>
            <span class="dr-a">→ proporcional al nivel de supervisión</span>
          </div>
        </div>

        <p class="footnote">EU AI Act, Art. 14: supervisión humana obligatoria para sistemas IA de alto riesgo.</p>
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

  .spectrum-viz {
    background: rgba(248, 113, 113, 0.05);
    border: 1px solid rgba(248, 113, 113, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
  }

  .spectrum-bar {
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
  }

  .spec-label {
    font-family: var(--font-mono);
    font-size: 0.7rem;
    color: #f87171;
    opacity: 0.7;
    min-width: 80px;
  }

  .spec-label.right { text-align: right; }

  .spec-track {
    flex: 1;
    height: 6px;
    background: linear-gradient(to right, rgba(248,113,113,0.5), rgba(251,191,36,0.3), rgba(248,113,113,0.5));
    border-radius: 3px;
    position: relative;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 4px;
  }

  .spec-dot {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background: #f87171;
    border: 2px solid rgba(248, 113, 113, 0.5);
  }

  .spec-problems {
    display: flex;
    justify-content: space-between;
  }

  .sp {
    font-family: var(--font-mono);
    font-size: 0.72rem;
    padding: 3px 8px;
    border-radius: 999px;
  }

  .sp.bad {
    background: rgba(248, 113, 113, 0.1);
    color: #f87171;
    border: 1px solid rgba(248, 113, 113, 0.2);
  }

  .tiers {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
  }

  .tier {
    border-radius: var(--radius-sm);
    padding: var(--spacing-md) var(--spacing-lg);
    border-left: 4px solid transparent;
  }

  .tier-auto { background: rgba(34, 197, 94, 0.07); border-left-color: #22c55e; }
  .tier-hotl { background: rgba(245, 158, 11, 0.07); border-left-color: #f59e0b; }
  .tier-hitl { background: rgba(248, 113, 113, 0.07); border-left-color: #f87171; }

  .tier-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 4px;
  }

  .tier-label {
    font-family: var(--font-mono);
    font-size: 0.8rem;
    font-weight: 700;
    color: var(--color-neutral-light);
  }

  .tier-badge {
    font-family: var(--font-mono);
    font-size: 0.65rem;
    font-weight: 600;
    padding: 2px 8px;
    border-radius: 999px;
    background: rgba(34, 197, 94, 0.15);
    color: #86efac;
    border: 1px solid rgba(34, 197, 94, 0.3);
  }

  .tier-badge-mid { background: rgba(245, 158, 11, 0.15); color: #fcd34d; border-color: rgba(245, 158, 11, 0.3); }
  .tier-badge-high { background: rgba(248, 113, 113, 0.15); color: #fca5a5; border-color: rgba(248, 113, 113, 0.3); }

  .tier-example {
    font-size: 0.78rem;
    color: var(--color-neutral-light);
    opacity: 0.5;
    font-style: italic;
    margin-bottom: 0;
  }

  .decision-rule {
    background: rgba(96, 165, 250, 0.07);
    border: 1px solid rgba(96, 165, 250, 0.2);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
  }

  .dr-title {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    font-weight: 700;
    color: var(--color-electric);
    margin-bottom: var(--spacing-xs);
  }

  .dr-item {
    display: flex;
    gap: var(--spacing-md);
    font-size: 0.82rem;
    line-height: 1.4;
  }

  .dr-q {
    color: var(--color-neutral-light);
    opacity: 0.7;
    min-width: 160px;
  }

  .dr-a {
    color: var(--color-electric);
    opacity: 0.8;
  }

  .footnote {
    font-family: var(--font-mono);
    font-size: 0.72rem;
    color: var(--color-neutral-light);
    opacity: 0.35;
    margin-bottom: 0;
  }

  @media (max-width: 900px) { .two-col { grid-template-columns: 1fr; } }
</style>
