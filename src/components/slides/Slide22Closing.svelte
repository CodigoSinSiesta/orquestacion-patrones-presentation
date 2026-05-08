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
    <div class="top-row">
      <div class="proof-card card-glass">
        <p class="proof-label">Dato de producción · Factory · 2025</p>
        <div class="metrics-row">
          <div class="metric">
            <span class="metric-num">16.5h</span>
            <span class="metric-label">Slack clone completo</span>
          </div>
          <div class="metric-divider"></div>
          <div class="metric">
            <span class="metric-num">778M</span>
            <span class="metric-label">tokens · 3 roles · 4 patrones</span>
          </div>
          <div class="metric-divider"></div>
          <div class="metric">
            <span class="metric-num">89%</span>
            <span class="metric-label">test coverage</span>
          </div>
        </div>
        <p class="proof-footnote">Sin los patrones de orquestación, este resultado no existe. La arquitectura no es accesoria — es el producto.</p>
      </div>

      <h1 class="closing-title">
        No es el modelo<br />
        que eliges.<br />
        Es cómo lo<br />
        <span class="hl">envuelves.</span>
      </h1>
    </div>

    <div class="links-section">
      <div class="links-col">
        <p class="links-heading">
          <span class="links-icon">▶</span> Vídeos
        </p>
        <ul class="links-list">
          <li>
            <a href="https://www.youtube.com/watch?v=ow1we5PzK-o" target="_blank" rel="noopener noreferrer" class="link-item">
              <span class="link-tag tag-green">Factory</span>
              <span class="link-text">The Multi-Agent Architecture That Actually Ships — Luke Alvoeiro</span>
            </a>
          </li>
          <li>
            <a href="https://www.youtube.com/watch?v=am_oeAoUhew" target="_blank" rel="noopener noreferrer" class="link-item">
              <span class="link-tag tag-green">OpenAI</span>
              <span class="link-text">Harness Engineering — Ryan Lopopolo (AI Engineer London)</span>
            </a>
          </li>
          <li>
            <a href="https://www.youtube.com/watch?v=Xxuxg8PcBvc" target="_blank" rel="noopener noreferrer" class="link-item">
              <span class="link-tag tag-green">Research</span>
              <span class="link-text">The Rise of Harness Engineering — PY (NLAH + Meta-Harness)</span>
            </a>
          </li>
          <li>
            <a href="https://www.youtube.com/watch?v=8kMaTybvDUw" target="_blank" rel="noopener noreferrer" class="link-item">
              <span class="link-tag tag-green">Talk</span>
              <span class="link-text">12-Factor Agents — Dexter Horthy (AI Engineer World's Fair)</span>
            </a>
          </li>
        </ul>
      </div>

      <div class="links-col">
        <p class="links-heading">
          <span class="links-icon">◎</span> Papers & Docs
        </p>
        <ul class="links-list">
          <li>
            <a href="https://www.anthropic.com/research/building-effective-agents" target="_blank" rel="noopener noreferrer" class="link-item">
              <span class="link-tag tag-amber">Anthropic</span>
              <span class="link-text">Building Effective Agents — Erik S. & Barry Zhang (5 patrones canónicos)</span>
            </a>
          </li>
          <li>
            <a href="https://arxiv.org/abs/2603.25723" target="_blank" rel="noopener noreferrer" class="link-item">
              <span class="link-tag tag-amber">Paper</span>
              <span class="link-text">Natural-Language Agent Harnesses — Tsinghua 2026 (+16.8 pts arXiv:2603.25723)</span>
            </a>
          </li>
          <li>
            <a href="https://arxiv.org/abs/2603.28052" target="_blank" rel="noopener noreferrer" class="link-item">
              <span class="link-tag tag-amber">Paper</span>
              <span class="link-text">Meta-Harness — Stanford/MIT 2026 (Haiku #1 TerminalBench arXiv:2603.28052)</span>
            </a>
          </li>
          <li>
            <a href="https://lilianweng.github.io/posts/2023-06-23-agent/" target="_blank" rel="noopener noreferrer" class="link-item">
              <span class="link-tag tag-amber">Referencia</span>
              <span class="link-text">LLM Powered Autonomous Agents — Lilian Weng (OpenAI, el post fundacional)</span>
            </a>
          </li>
        </ul>
      </div>

      <div class="links-col">
        <p class="links-heading">
          <span class="links-icon">▷</span> Pruébalo
        </p>
        <ul class="links-list">
          <li>
            <a href="https://factory.ai" target="_blank" rel="noopener noreferrer" class="link-item">
              <span class="link-tag tag-violet">Tool</span>
              <span class="link-text">Factory — plataforma Missions en producción</span>
            </a>
          </li>
          <li>
            <a href="https://claude.ai/code" target="_blank" rel="noopener noreferrer" class="link-item">
              <span class="link-tag tag-violet">Tool</span>
              <span class="link-text">Claude Code — agente CLI con herramientas reales</span>
            </a>
          </li>
          <li>
            <a href="https://agents.md" target="_blank" rel="noopener noreferrer" class="link-item">
              <span class="link-tag tag-violet">Estándar</span>
              <span class="link-text">AGENTS.md — estándar abierto para instruir agentes</span>
            </a>
          </li>
          <li>
            <a href="https://github.com/humanlayer/12-factor-agents" target="_blank" rel="noopener noreferrer" class="link-item">
              <span class="link-tag tag-violet">GitHub</span>
              <span class="link-text">12-Factor Agents — principios de producción (Dexter Horthy)</span>
            </a>
          </li>
        </ul>
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
          <a href="https://tellmealex.dev" target="_blank" rel="noopener noreferrer" class="author-link">tellmealex.dev</a>
          <span class="author-sep">·</span>
          <a href="https://github.com/TellMeAlex" target="_blank" rel="noopener noreferrer" class="author-link">@TellMeAlex</a>
        </div>
      </div>
    </div>
  </div>

  <div class="orb orb-1"></div>
  <div class="orb orb-2"></div>
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
      radial-gradient(ellipse at 20% 70%, rgba(167, 139, 250, 0.1) 0%, transparent 55%),
      radial-gradient(ellipse at 80% 25%, rgba(34, 197, 94, 0.07) 0%, transparent 55%);
    z-index: 1;
  }

  .animated-grid {
    position: absolute;
    inset: 0;
    background-image:
      linear-gradient(rgba(167, 139, 250, 0.05) 1px, transparent 1px),
      linear-gradient(90deg, rgba(167, 139, 250, 0.05) 1px, transparent 1px);
    background-size: 60px 60px;
    z-index: 0;
    animation: moveGrid 30s linear infinite;
  }

  .slide-content {
    position: relative;
    z-index: 2;
    max-width: 1100px;
    width: 100%;
    padding: var(--spacing-content);
    padding-top: 4rem;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: var(--spacing-xl);
  }

  .top-row {
    width: 100%;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: var(--spacing-xl);
    align-items: start;
  }

  .proof-card {
    width: 100%;
    animation: fadeUp 0.6s ease-out backwards;
  }

  .proof-label {
    font-family: var(--font-mono);
    font-size: 0.72rem;
    font-weight: 600;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--color-electric);
    margin-bottom: var(--spacing-lg);
    opacity: 0.6;
  }

  .metrics-row {
    display: flex;
    align-items: center;
    gap: var(--spacing-xl);
    margin-bottom: var(--spacing-lg);
    flex-wrap: wrap;
  }

  .metric { display: flex; flex-direction: column; gap: 4px; }

  .metric-num {
    font-family: var(--font-display);
    font-size: clamp(1.8rem, 3.5vw, 2.8rem);
    font-weight: 900;
    background: linear-gradient(135deg, #a78bfa, #c4b5fd);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1;
  }

  .metric-label {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    color: var(--color-neutral-light);
    opacity: 0.5;
  }

  .metric-divider {
    width: 1px;
    height: 48px;
    background: rgba(96, 165, 250, 0.15);
    flex-shrink: 0;
  }

  .proof-footnote {
    font-size: 0.875rem;
    color: var(--color-neutral-light);
    opacity: 0.5;
    font-style: italic;
    line-height: 1.5;
    margin-bottom: 0;
  }

  .closing-title {
    font-size: clamp(2rem, 4.5vw, 4rem);
    font-weight: 900;
    line-height: 1.1;
    color: var(--color-neutral-light);
    animation: fadeUp 0.7s ease-out 0.1s backwards;
    margin-bottom: 0;
    align-self: center;
  }

  .links-section {
    width: 100%;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: var(--spacing-lg);
    animation: fadeUp 0.7s ease-out 0.15s backwards;
  }

  .links-col {
    background: rgba(15, 23, 42, 0.5);
    border: 1px solid rgba(148, 163, 184, 0.1);
    border-radius: var(--radius-md);
    padding: var(--spacing-lg) var(--spacing-xl);
    display: flex;
    flex-direction: column;
    gap: var(--spacing-md);
  }

  .links-heading {
    font-family: var(--font-mono);
    font-size: 0.72rem;
    font-weight: 700;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--color-neutral-light);
    opacity: 0.4;
    margin-bottom: 0;
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
  }

  .links-icon {
    opacity: 0.5;
  }

  .links-list {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
  }

  .link-item {
    display: flex;
    align-items: flex-start;
    gap: var(--spacing-sm);
    text-decoration: none;
    padding: 6px 0;
    border-bottom: 1px solid rgba(148, 163, 184, 0.06);
    transition: opacity var(--transition-fast);
  }

  .link-item:last-child { border-bottom: none; }

  .link-item:hover { opacity: 0.8; }

  .link-tag {
    font-family: var(--font-mono);
    font-size: 0.6rem;
    font-weight: 700;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 2px 6px;
    border-radius: 999px;
    flex-shrink: 0;
    margin-top: 1px;
  }

  .tag-green {
    color: #86efac;
    background: rgba(134, 239, 172, 0.12);
    border: 1px solid rgba(134, 239, 172, 0.25);
  }

  .tag-amber {
    color: #fcd34d;
    background: rgba(252, 211, 77, 0.1);
    border: 1px solid rgba(252, 211, 77, 0.2);
  }

  .tag-violet {
    color: #c4b5fd;
    background: rgba(196, 181, 253, 0.1);
    border: 1px solid rgba(196, 181, 253, 0.2);
  }

  .link-text {
    font-size: 0.8rem;
    color: var(--color-neutral-light);
    opacity: 0.65;
    line-height: 1.4;
  }

  .hl {
    background: linear-gradient(135deg, #a78bfa 0%, #c4b5fd 50%, #86efac 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .author-card {
    display: flex;
    align-items: center;
    gap: var(--spacing-lg);
    padding: var(--spacing-lg) var(--spacing-xl);
    animation: fadeUp 0.7s ease-out 0.2s backwards;
  }

  .author-avatar {
    width: 48px;
    height: 48px;
    border-radius: 50%;
    object-fit: cover;
    flex-shrink: 0;
  }

  .author-name {
    font-size: 1rem;
    font-weight: 700;
    color: var(--color-neutral-light);
    margin-bottom: 2px;
  }

  .author-role {
    font-size: 0.82rem;
    color: var(--color-electric);
    font-family: var(--font-mono);
    opacity: 0.7;
    margin-bottom: 4px;
  }

  .author-links {
    display: flex;
    gap: var(--spacing-sm);
    align-items: center;
  }

  .author-link {
    font-family: var(--font-mono);
    font-size: 0.8rem;
    color: var(--color-electric);
    text-decoration: none;
    opacity: 0.6;
    transition: opacity var(--transition-fast);
  }

  .author-link:hover { opacity: 1; }

  .author-sep { color: var(--color-electric); opacity: 0.3; }

  .orb {
    position: absolute;
    border-radius: 50%;
    filter: blur(80px);
    pointer-events: none;
    z-index: 0;
  }

  .orb-1 { width: 400px; height: 400px; background: rgba(167, 139, 250, 0.07); top: -50px; right: -100px; animation: floatOrb 14s ease-in-out infinite; }
  .orb-2 { width: 300px; height: 300px; background: rgba(34, 197, 94, 0.05); bottom: 0; left: -50px; animation: floatOrb 10s ease-in-out infinite reverse; }

  @keyframes fadeUp { from { opacity: 0; transform: translateY(28px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes moveGrid { 0% { transform: translate(0, 0); } 100% { transform: translate(60px, 60px); } }
  @keyframes floatOrb { 0%, 100% { transform: translateY(0) scale(1); } 50% { transform: translateY(-25px) scale(1.04); } }

  @media (max-width: 1100px) {
    .links-section { grid-template-columns: 1fr 1fr; }
  }

  @media (max-width: 900px) {
    .top-row { grid-template-columns: 1fr; }
    .closing-title { font-size: clamp(2.5rem, 11vw, 4rem); }
    .links-section { grid-template-columns: 1fr; }
    .metrics-row { gap: var(--spacing-lg); }
    .metric-divider { display: none; }
  }
</style>
