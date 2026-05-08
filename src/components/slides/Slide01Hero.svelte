<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-background"></div>
  <div class="animated-grid"></div>

  <div class="slide-content">
    <div class="eyebrow">
      <span class="eyebrow-dot"></span>
      <span>Patrones de Orquestación · Codigo Sin Siesta · 2026</span>
    </div>

    <h1 class="title">
      Patrones de<br />
      <span class="highlight">Orquestación</span>
    </h1>

    <p class="subtitle">
      10 patrones. 3 perspectivas. La misma conclusión:<br />
      la arquitectura importa más que el modelo.
    </p>

    <div class="modules-preview">
      <div class="module-chip mod-a">
        <span class="mod-letter">A</span>
        <span>Taxonomía Evolutiva</span>
      </div>
      <div class="module-chip mod-b">
        <span class="mod-letter">B</span>
        <span>Por Problema</span>
      </div>
      <div class="module-chip mod-c">
        <span class="mod-letter">C</span>
        <span>Convergencias</span>
      </div>
    </div>

    <div class="author-card card-glass">
      <img
        src="https://www.gravatar.com/avatar/8461e0b8674185c1df153079e820504b?s=120"
        alt="Alejandro de la Fuente"
        class="author-avatar"
      />
      <div class="author-info">
        <p class="author-name">Alejandro de la Fuente</p>
        <p class="author-role">Tech Lead · NTT Data · GDNE</p>
        <div class="author-links">
          <a href="https://tellmealex.dev" target="_blank" rel="noopener noreferrer" class="author-link" aria-label="Sitio web">🌐</a>
          <a href="https://github.com/TellMeAlex" target="_blank" rel="noopener noreferrer" class="author-link" aria-label="GitHub">🐙</a>
          <a href="https://es.linkedin.com/in/alejandro-de-la-fuente" target="_blank" rel="noopener noreferrer" class="author-link" aria-label="LinkedIn">💼</a>
        </div>
      </div>
    </div>
  </div>

  <div class="orb orb-1"></div>
  <div class="orb orb-2"></div>
  <div class="orb orb-3"></div>
</div>

<style>
  .swiper-slide {
    position: relative;
    width: 100%;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  .slide-background {
    position: absolute;
    inset: 0;
    background:
      radial-gradient(ellipse at 15% 60%, rgba(59, 130, 246, 0.12) 0%, transparent 55%),
      radial-gradient(ellipse at 85% 30%, rgba(30, 58, 138, 0.18) 0%, transparent 55%);
    z-index: 1;
  }

  .animated-grid {
    position: absolute;
    inset: 0;
    background-image:
      linear-gradient(rgba(96, 165, 250, 0.07) 1px, transparent 1px),
      linear-gradient(90deg, rgba(96, 165, 250, 0.07) 1px, transparent 1px);
    background-size: 60px 60px;
    z-index: 0;
    animation: moveGrid 25s linear infinite;
  }

  .slide-content {
    position: relative;
    z-index: 2;
    max-width: 1100px;
    width: 100%;
    padding: var(--spacing-content);
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: var(--spacing-xl);
  }

  .eyebrow {
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
    font-family: var(--font-mono);
    font-size: 0.85rem;
    color: var(--color-electric);
    letter-spacing: 0.12em;
    text-transform: uppercase;
    animation: fadeUp 0.6s ease-out backwards;
  }

  .eyebrow-dot {
    width: 8px;
    height: 8px;
    background: var(--color-accent-bright);
    border-radius: 50%;
    animation: pulse 2s ease-in-out infinite;
    box-shadow: 0 0 8px rgba(59, 130, 246, 0.8);
  }

  .title {
    font-size: clamp(3.5rem, 9vw, 7.5rem);
    font-weight: 900;
    line-height: 1.0;
    margin-bottom: 0;
    color: var(--color-neutral-light);
    animation: fadeUp 0.7s ease-out 0.1s backwards;
  }

  .highlight {
    background: linear-gradient(135deg, #22c55e 0%, #60A5FA 50%, #a78bfa 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .subtitle {
    font-size: clamp(1.1rem, 2.2vw, 1.5rem);
    color: var(--color-neutral-light);
    opacity: 0.78;
    font-family: var(--font-body);
    font-weight: 400;
    line-height: 1.6;
    margin-bottom: 0;
    animation: fadeUp 0.7s ease-out 0.2s backwards;
  }

  .modules-preview {
    display: flex;
    flex-wrap: wrap;
    gap: var(--spacing-sm);
    animation: fadeUp 0.7s ease-out 0.3s backwards;
  }

  .module-chip {
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
    padding: var(--spacing-sm) var(--spacing-lg);
    border-radius: 999px;
    font-family: var(--font-body);
    font-size: 0.9rem;
    font-weight: 600;
    backdrop-filter: blur(4px);
  }

  .mod-letter {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    font-weight: 800;
    letter-spacing: 0.05em;
  }

  .mod-a {
    background: rgba(34, 197, 94, 0.12);
    border: 1px solid rgba(34, 197, 94, 0.4);
    color: #86efac;
  }

  .mod-b {
    background: rgba(245, 158, 11, 0.12);
    border: 1px solid rgba(245, 158, 11, 0.4);
    color: #fcd34d;
  }

  .mod-c {
    background: rgba(167, 139, 250, 0.12);
    border: 1px solid rgba(167, 139, 250, 0.4);
    color: #c4b5fd;
  }

  .author-card {
    display: flex;
    align-items: center;
    gap: var(--spacing-lg);
    padding: var(--spacing-lg) var(--spacing-xl);
    animation: fadeUp 0.7s ease-out 0.4s backwards;
  }

  .author-avatar {
    width: 52px;
    height: 52px;
    border-radius: 50%;
    flex-shrink: 0;
    object-fit: cover;
  }

  .author-name {
    font-size: 1.1rem;
    font-weight: 700;
    color: var(--color-neutral-light);
    margin-bottom: var(--spacing-xs);
  }

  .author-role {
    font-size: 0.9rem;
    color: var(--color-electric);
    opacity: 0.85;
    font-family: var(--font-mono);
  }

  .author-links {
    display: flex;
    gap: var(--spacing-sm);
    margin-top: var(--spacing-xs);
  }

  .author-link {
    font-size: 1rem;
    text-decoration: none;
    opacity: 0.7;
    transition: opacity var(--transition-fast);
  }

  .author-link:hover { opacity: 1; }

  .orb {
    position: absolute;
    border-radius: 50%;
    filter: blur(80px);
    pointer-events: none;
    z-index: 0;
  }

  .orb-1 { width: 500px; height: 500px; background: rgba(59, 130, 246, 0.08); top: -100px; right: -100px; animation: floatOrb 12s ease-in-out infinite; }
  .orb-2 { width: 300px; height: 300px; background: rgba(34, 197, 94, 0.06); bottom: 50px; right: 200px; animation: floatOrb 9s ease-in-out infinite reverse; }
  .orb-3 { width: 200px; height: 200px; background: rgba(167, 139, 250, 0.05); bottom: -50px; left: 100px; animation: floatOrb 15s ease-in-out infinite; }

  @keyframes fadeUp { from { opacity: 0; transform: translateY(28px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes moveGrid { 0% { transform: translate(0, 0); } 100% { transform: translate(60px, 60px); } }
  @keyframes pulse { 0%, 100% { opacity: 1; transform: scale(1); } 50% { opacity: 0.6; transform: scale(0.85); } }
  @keyframes floatOrb { 0%, 100% { transform: translateY(0) scale(1); } 50% { transform: translateY(-30px) scale(1.05); } }

  @media (max-width: 768px) {
    .slide-content { align-items: center; }
    .title { font-size: clamp(3rem, 13vw, 5rem); text-align: center; width: 100%; }
    .subtitle { text-align: center; }
    .modules-preview { justify-content: center; }
    .eyebrow { justify-content: center; }
  }
</style>
