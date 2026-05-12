<script lang="ts">
  import { onMount } from 'svelte';
  import { animateSlideEntrance } from '@/utils/animations';
  let slideElement: HTMLElement;
  onMount(() => { animateSlideEntrance(slideElement); });
</script>

<div class="swiper-slide" bind:this={slideElement}>
  <div class="slide-content">
    <div class="slide-header">
      <div class="module-tag">
        <span class="tag-dot"></span>
        <span>Módulo A · Niveles 8–10 · Emergencia y autonomía</span>
      </div>
      <h2 class="title">Cuando los agentes se <span class="hl">auto-organizan</span></h2>
    </div>

    <div class="top-levels">
      <div class="level-card level-8">
        <div class="level-badge">8</div>
        <div class="level-content">
          <h3>Swarm / Mesh</h3>
          <p><strong>Swarm</strong>: topología emergente en runtime. Los agentes se conectan dinámicamente según la tarea, como hormigas que construyen rutas sin coordinador central. Alta flexibilidad, baja predecibilidad.</p>
          <p><strong>Mesh</strong>: conexiones peer-to-peer fijas en design time. Cada agente conoce a sus vecinos. Más predecible que Swarm, pero con overhead de todos hablar con todos.</p>
          <div class="level-meta">
            <span class="meta-item warning">⚠️ Factory evita Swarm en producción: el no-determinismo hace imposible el debugging.</span>
          </div>
        </div>
      </div>

      <div class="level-card level-9">
        <div class="level-badge">9</div>
        <div class="level-content">
          <h3>Missions (composición de 4 patrones)</h3>
          <p>El patrón de Factory para tareas de software de semanas de duración. Combina: <strong>Orchestrator-Workers</strong> (3 roles) + <strong>Creator-Verifier</strong> (Validation Contracts) + <strong>ejecución serial</strong> (sin merge conflicts) + <strong>Handoffs estructurados</strong> (5 campos). Dato de producción: Slack clone en 16.5h, 778M tokens, 89% test coverage.</p>
          <div class="level-meta">
            <span class="meta-item success">✓ Comprobado en producción. La anti-fragilidad viene de lógica en prompts, no en código.</span>
          </div>
        </div>
      </div>

      <div class="level-card level-10">
        <div class="level-badge">10</div>
        <div class="level-content">
          <h3>Puppeteer / RL Orchestration</h3>
          <p>Un orquestador entrenado con Reinforcement Learning que aprende qué secuencia de delegaciones produce mejores resultados. Las 5 sub-decisiones que aprende: cuándo spawnear, a quién delegar, cómo comunicar, cómo agregar, cuándo parar.</p>
          <div class="level-meta">
            <span class="meta-item frontier">🔬 Investigación de frontera. Mayo 2026: sin método publicado para la decisión de cuándo parar.</span>
          </div>
        </div>
      </div>

      <div class="level-card level-rec">
        <div class="level-badge rec-badge">★</div>
        <div class="level-content">
          <h3>RecursiveMAS — Comunicación en latent space <span class="rec-tag">arXiv:2604.25917</span></h3>
          <p>Los agentes se comunican directamente a través de hidden states entrenados, sin convertir a tokens entre rondas. El módulo <strong>RecursiveLink</strong> (Inner + Outer adapters, 0.31% de los parámetros) proyecta el estado latente de un agente al espacio de entrada del siguiente. Resultado: +8.3% accuracy, 2.4× speedup, −75.6% tokens vs. MAS text-based — Tsinghua University, mayo 2026.</p>
          <div class="level-meta">
            <span class="meta-item rec-meta">📡 Saltar el canal de texto entre agentes es la siguiente frontera del nivel 10. El texto ya no es el único protocolo de coordinación.</span>
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
    background: linear-gradient(135deg, #22c55e, #a78bfa);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .top-levels {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-lg);
  }

  .level-card {
    display: flex;
    gap: var(--spacing-lg);
    background: rgba(30, 58, 138, 0.1);
    border-radius: var(--radius-md);
    padding: var(--spacing-xl);
    border-left: 4px solid transparent;
  }

  .level-8 { border-left-color: rgba(34, 197, 94, 0.5); }
  .level-9 { border-left-color: rgba(59, 130, 246, 0.6); }
  .level-10 { border-left-color: rgba(167, 139, 250, 0.6); }
  .level-rec { border-left-color: rgba(251, 191, 36, 0.6); background: rgba(251, 191, 36, 0.04); }

  .level-badge {
    width: 36px;
    height: 36px;
    border-radius: var(--radius-sm);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: var(--font-mono);
    font-size: 0.9rem;
    font-weight: 800;
    color: #86efac;
    background: rgba(34, 197, 94, 0.15);
    flex-shrink: 0;
  }

  .level-9 .level-badge { background: rgba(59, 130, 246, 0.15); color: var(--color-electric); }
  .level-10 .level-badge { background: rgba(167, 139, 250, 0.15); color: #c4b5fd; }
  .rec-badge { background: rgba(251, 191, 36, 0.15); color: #fde68a; font-size: 1rem; }
  .rec-tag { font-family: var(--font-mono); font-size: 0.7rem; font-weight: 600; color: #fde68a; opacity: 0.7; margin-left: 8px; vertical-align: middle; }
  .rec-meta { background: rgba(251, 191, 36, 0.1); color: #fde68a; border: 1px solid rgba(251, 191, 36, 0.3); }

  .level-content {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: var(--spacing-sm);
  }

  .level-content h3 {
    font-size: 1.05rem;
    font-weight: 700;
    color: var(--color-neutral-light);
    margin-bottom: 0;
  }

  .level-content p {
    font-size: 0.875rem;
    color: var(--color-neutral-light);
    opacity: 0.7;
    line-height: 1.6;
    margin-bottom: 0;
  }

  .level-meta {
    margin-top: var(--spacing-xs);
  }

  .meta-item {
    font-family: var(--font-mono);
    font-size: 0.75rem;
    padding: 4px 10px;
    border-radius: var(--radius-sm);
    display: inline-block;
    line-height: 1.5;
  }

  .warning { background: rgba(245, 158, 11, 0.1); color: #fcd34d; border: 1px solid rgba(245, 158, 11, 0.3); }
  .success { background: rgba(34, 197, 94, 0.1); color: #86efac; border: 1px solid rgba(34, 197, 94, 0.3); }
  .frontier { background: rgba(167, 139, 250, 0.1); color: #c4b5fd; border: 1px solid rgba(167, 139, 250, 0.3); }
</style>
