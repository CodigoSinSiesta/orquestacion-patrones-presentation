<script lang="ts">
  import { onMount } from 'svelte';
  import gsap from 'gsap';
  import { animateSlideEntrance, addButtonHoverAnimation } from '../utils/animations';

  let currentSlide = $state(0);
  let slides = $state<HTMLElement[]>([]);
  let menuOpen = $state(false);

  let touchStartX = 0;
  let touchStartY = 0;
  let touchEndX = 0;
  let touchEndY = 0;
  let isSwiping = false;
  let lastSwipeTime = 0;

  const slideNames = [
    'hero',
    'mapa',
    'tax-intro',
    'escalera-base',
    'escalera-media',
    'escalera-top',
    'diagrama-capas',
    'prob-intro',
    'prob-bias',
    'prob-contexto',
    'prob-paralelo',
    'prob-tests',
    'prob-obsolescencia',
    'prob-supervision',
    'conv-intro',
    'conv-harness-modelo',
    'conv-gen-eval',
    'conv-logica-texto',
    'conv-estado',
    'conv-matriz',
    'conclusiones',
    'closing'
  ] as const;

  const slideTitles: Record<(typeof slideNames)[number], string> = {
    hero: 'Patrones de Orquestación',
    mapa: 'El mapa del territorio',
    'tax-intro': 'Módulo A · Taxonomía Evolutiva',
    'escalera-base': 'Niveles 1–4 · La base',
    'escalera-media': 'Niveles 5–7 · Coordinación',
    'escalera-top': 'Niveles 8–10 · Emergencia',
    'diagrama-capas': 'Las 4 capas de complejidad',
    'prob-intro': 'Módulo B · Por Problema',
    'prob-bias': 'El agente no detecta sus errores',
    'prob-contexto': 'El contexto se degrada',
    'prob-paralelo': 'Los agentes se pisan los cambios',
    'prob-tests': 'Los tests no atrapan bugs reales',
    'prob-obsolescencia': 'El sistema caduca con cada modelo',
    'prob-supervision': 'Supervisar sin microgestionar',
    'conv-intro': 'Módulo C · Convergencias',
    'conv-harness-modelo': 'Harness > Modelo',
    'conv-gen-eval': 'Separar generación y evaluación',
    'conv-logica-texto': 'Lógica en prompts, no en código',
    'conv-estado': 'Estado externalizado',
    'conv-matriz': 'La matriz de convergencias',
    conclusiones: 'Conclusiones',
    closing: 'Cierre'
  };

  const moduleColors: Record<(typeof slideNames)[number], string> = {
    hero: '',
    mapa: '',
    'tax-intro': '#22c55e',
    'escalera-base': '#22c55e',
    'escalera-media': '#22c55e',
    'escalera-top': '#22c55e',
    'diagrama-capas': '#22c55e',
    'prob-intro': '#f59e0b',
    'prob-bias': '#f59e0b',
    'prob-contexto': '#f59e0b',
    'prob-paralelo': '#f59e0b',
    'prob-tests': '#f59e0b',
    'prob-obsolescencia': '#f59e0b',
    'prob-supervision': '#f59e0b',
    'conv-intro': '#a78bfa',
    'conv-harness-modelo': '#a78bfa',
    'conv-gen-eval': '#a78bfa',
    'conv-logica-texto': '#a78bfa',
    'conv-estado': '#a78bfa',
    'conv-matriz': '#a78bfa',
    conclusiones: '',
    closing: ''
  };

  const totalSlides = slideNames.length;

  onMount(() => {
    slides = Array.from(document.querySelectorAll('.swiper-slide')) as HTMLElement[];

    if (slides.length > 0) {
      slides[0].classList.add('swiper-slide-active');
      animateSlideEntrance(slides[0]);
    }

    const buttons = document.querySelectorAll('.btn');
    buttons.forEach((btn) => {
      addButtonHoverAnimation(btn as HTMLElement);
    });

    const hash = window.location.hash.replace('#/', '');
    const slideIndex = slideNames.indexOf(hash as (typeof slideNames)[number]);
    if (slideIndex !== -1 && slideIndex !== currentSlide) {
      goToSlide(slideIndex);
    }

    const handleHashChange = () => {
      const nextHash = window.location.hash.replace('#/', '');
      const nextSlide = slideNames.indexOf(nextHash as (typeof slideNames)[number]);
      if (nextSlide !== -1 && nextSlide !== currentSlide) {
        goToSlide(nextSlide);
      }
    };

    window.addEventListener('hashchange', handleHashChange);
    return () => window.removeEventListener('hashchange', handleHashChange);
  });

  $effect(() => {
    const handleKeyDown = (e: KeyboardEvent) => {
      if (e.key === 'ArrowRight') nextSlide();
      else if (e.key === 'ArrowLeft') prevSlide();
      else if (e.key === 'Escape' && menuOpen) menuOpen = false;
    };
    window.addEventListener('keydown', handleKeyDown);
    return () => window.removeEventListener('keydown', handleKeyDown);
  });

  function updateHash(slideName: string) {
    window.location.hash = `#/${slideName}`;
  }

  function goToSlide(index: number) {
    if (index < 0 || index >= slides.length || index === currentSlide) return;
    const reduceMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
    if (menuOpen) menuOpen = false;

    const previousSlide = slides[currentSlide];
    if (previousSlide) {
      gsap.to(previousSlide, {
        opacity: 0,
        duration: reduceMotion ? 0 : 0.3,
        ease: 'power2.out',
        onComplete: () => previousSlide.classList.remove('swiper-slide-active')
      });
    }

    currentSlide = index;
    slides[currentSlide]?.classList.add('swiper-slide-active');
    animateSlideEntrance(slides[currentSlide]);
    updateHash(slideNames[currentSlide]);
  }

  function goToSlideFromMenu(index: number) {
    menuOpen = false;
    goToSlide(index);
  }

  function nextSlide() { goToSlide(currentSlide + 1); }
  function prevSlide() { goToSlide(currentSlide - 1); }

  const SWIPE_THRESHOLD = 50;
  const SWIPE_DEBOUNCE = 300;

  function handleTouchStart(event: TouchEvent) {
    const touch = event.touches[0];
    touchStartX = touch.clientX;
    touchStartY = touch.clientY;
    touchEndX = touch.clientX;
    touchEndY = touch.clientY;
    isSwiping = true;
  }

  function handleTouchMove(event: TouchEvent) {
    if (!isSwiping) return;
    const touch = event.touches[0];
    touchEndX = touch.clientX;
    touchEndY = touch.clientY;
  }

  function handleTouchEnd() {
    if (!isSwiping) return;
    isSwiping = false;
    const deltaX = touchEndX - touchStartX;
    const deltaY = touchEndY - touchStartY;
    const now = Date.now();
    if (now - lastSwipeTime < SWIPE_DEBOUNCE) return;
    if (Math.abs(deltaX) < SWIPE_THRESHOLD) return;
    if (Math.abs(deltaY) > Math.abs(deltaX)) return;
    lastSwipeTime = now;
    if (menuOpen) menuOpen = false;
    if (deltaX > 0) prevSlide();
    else nextSlide();
  }
</script>

<div
  class="presentation-container"
  ontouchstart={handleTouchStart}
  ontouchmove={handleTouchMove}
  ontouchend={handleTouchEnd}
>
  <div class="swiper">
    <div class="swiper-wrapper">
      <slot />
    </div>

    <button class="swiper-button-prev nav-btn nav-btn-prev" title="Anterior" aria-label="Anterior" onclick={prevSlide}>
      <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="15 18 9 12 15 6"></polyline></svg>
    </button>

    <button class="swiper-button-next nav-btn nav-btn-next" title="Siguiente" aria-label="Siguiente" onclick={nextSlide}>
      <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="9 18 15 12 9 6"></polyline></svg>
    </button>
  </div>

  <div class="slide-counter">
    <span class="counter-number">{currentSlide + 1}</span>
    <span class="counter-separator">/</span>
    <span class="counter-total">{totalSlides}</span>
  </div>

  {#if moduleColors[slideNames[currentSlide]]}
    <div class="module-indicator" style="--mod-color: {moduleColors[slideNames[currentSlide]]}">
      {currentSlide <= 6 ? 'Módulo A' : currentSlide <= 13 ? 'Módulo B' : currentSlide <= 19 ? 'Módulo C' : ''}
    </div>
  {/if}

  <button class="hamburger-btn" class:open={menuOpen} title="Navegación" aria-label="Abrir navegación" onclick={() => menuOpen = !menuOpen}>
    <span class="hamburger-line"></span>
    <span class="hamburger-line"></span>
    <span class="hamburger-line"></span>
  </button>

  {#if menuOpen}
    <div class="drawer-overlay" onclick={() => menuOpen = false}></div>
  {/if}

  <div class="slide-drawer" class:open={menuOpen}>
    <div class="drawer-header">
      <span class="drawer-title">Navegación</span>
      <button class="drawer-close" title="Cerrar" aria-label="Cerrar navegación" onclick={() => menuOpen = false}>
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
          <line x1="18" y1="6" x2="6" y2="18"></line>
          <line x1="6" y1="6" x2="18" y2="18"></line>
        </svg>
      </button>
    </div>
    <nav class="drawer-nav">
      <ul class="drawer-list">
        {#each slideNames as name, index}
          <li>
            <button
              class="drawer-item"
              class:active={index === currentSlide}
              style={moduleColors[name] ? `--item-color: ${moduleColors[name]}` : ''}
              onclick={() => goToSlideFromMenu(index)}
            >
              <span class="item-number">{index + 1}</span>
              <span class="item-title">{slideTitles[name]}</span>
            </button>
          </li>
        {/each}
      </ul>
    </nav>
  </div>
</div>

<style>
  .presentation-container {
    position: relative;
    width: 100%;
    height: 100vh;
    background-color: var(--color-base-dark);
    overflow: hidden;
  }

  .swiper {
    width: 100%;
    height: 100%;
  }

  :global(.swiper-wrapper) {
    width: 100%;
    height: 100%;
    overflow: hidden;
  }

  :global(.swiper-slide) {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: flex-start !important;
    justify-content: center;
    position: absolute !important;
    top: 0;
    left: 0;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.6s ease-out;
    visibility: hidden;
    overflow: auto;
  }

  :global(.swiper-slide-active) {
    opacity: 1;
    pointer-events: auto;
    visibility: visible;
    overflow-y: auto !important;
  }

  .nav-btn {
    position: fixed;
    top: 50%;
    transform: translateY(-50%);
    z-index: 100;
    width: 50px;
    height: 50px;
    background: rgba(30, 58, 138, 0.6);
    border: 2px solid var(--color-electric);
    border-radius: var(--radius-md);
    color: var(--color-neutral-light);
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: background-color var(--transition-base), border-color var(--transition-base), transform var(--transition-base);
    backdrop-filter: blur(8px);
  }

  .nav-btn:hover {
    background: rgba(30, 58, 138, 0.9);
    border-color: var(--color-accent-bright);
    transform: translateY(-50%) scale(1.1);
  }

  .nav-btn-prev { left: var(--spacing-2xl); }
  .nav-btn-next { right: var(--spacing-2xl); }

  .slide-counter {
    position: fixed;
    bottom: var(--spacing-xl);
    right: var(--spacing-2xl);
    z-index: 100;
    font-family: var(--font-mono);
    font-size: 1.25rem;
    color: var(--color-electric);
    display: flex;
    gap: var(--spacing-grid);
    align-items: center;
    background: rgba(30, 58, 138, 0.4);
    padding: var(--spacing-md) var(--spacing-lg);
    border-radius: var(--radius-md);
    border: 1px solid rgba(96, 165, 250, 0.2);
    backdrop-filter: blur(8px);
  }

  .counter-separator, .counter-total {
    color: var(--color-neutral-light);
    opacity: 0.7;
  }

  .module-indicator {
    position: fixed;
    bottom: var(--spacing-xl);
    left: var(--spacing-2xl);
    z-index: 100;
    font-family: var(--font-mono);
    font-size: 0.8rem;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--mod-color, var(--color-electric));
    background: rgba(30, 58, 138, 0.4);
    padding: var(--spacing-md) var(--spacing-lg);
    border-radius: var(--radius-md);
    border: 1px solid var(--mod-color, rgba(96, 165, 250, 0.2));
    backdrop-filter: blur(8px);
  }

  .hamburger-btn {
    display: none;
    position: fixed;
    top: var(--spacing-lg);
    right: var(--spacing-lg);
    z-index: var(--z-modal);
    width: 48px;
    height: 48px;
    background: rgba(30, 58, 138, 0.6);
    border: 2px solid var(--color-electric);
    border-radius: var(--radius-md);
    cursor: pointer;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 5px;
    transition: background-color var(--transition-base), border-color var(--transition-base);
    backdrop-filter: blur(8px);
  }

  .hamburger-line {
    display: block;
    width: 22px;
    height: 2px;
    background: var(--color-neutral-light);
    border-radius: 2px;
    transition: opacity var(--transition-fast), transform var(--transition-fast);
    transform-origin: center;
  }

  .hamburger-btn.open .hamburger-line:nth-child(1) { transform: translateY(7px) rotate(45deg); }
  .hamburger-btn.open .hamburger-line:nth-child(2) { opacity: 0; transform: scaleX(0); }
  .hamburger-btn.open .hamburger-line:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }

  .drawer-overlay {
    position: fixed;
    inset: 0;
    background: rgba(10, 22, 40, 0.7);
    z-index: var(--z-modal);
  }

  .slide-drawer {
    display: none;
    position: fixed;
    top: 0;
    right: 0;
    width: min(300px, 85vw);
    height: 100vh;
    background: linear-gradient(180deg, rgba(30, 58, 138, 0.95) 0%, rgba(10, 22, 40, 0.98) 100%);
    border-left: 2px solid var(--color-electric);
    z-index: var(--z-popover);
    transform: translateX(100%);
    transition: transform var(--transition-base) cubic-bezier(0.4, 0, 0.2, 1);
    overflow-y: auto;
    backdrop-filter: blur(12px);
  }

  .slide-drawer.open { transform: translateX(0); }

  .drawer-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: var(--spacing-lg);
    border-bottom: 1px solid rgba(96, 165, 250, 0.2);
  }

  .drawer-title {
    font-family: var(--font-display);
    font-size: 1.25rem;
    font-weight: 700;
    color: var(--color-neutral-light);
    letter-spacing: 0.05em;
    text-transform: uppercase;
  }

  .drawer-close {
    width: 48px;
    height: 48px;
    background: transparent;
    border: 2px solid var(--color-electric);
    border-radius: var(--radius-md);
    color: var(--color-neutral-light);
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .drawer-nav { padding: var(--spacing-md); }
  .drawer-list { list-style: none; padding: 0; margin: 0; }

  .drawer-item {
    width: 100%;
    min-height: 48px;
    padding: var(--spacing-sm) var(--spacing-lg);
    background: transparent;
    border: none;
    border-radius: var(--radius-md);
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: var(--spacing-md);
    text-align: left;
    margin-bottom: 2px;
    color: inherit;
    border-left: 3px solid transparent;
    transition: background var(--transition-fast), border-color var(--transition-fast);
  }

  .drawer-item:hover { background: rgba(96, 165, 250, 0.15); }

  .drawer-item.active {
    background: rgba(59, 130, 246, 0.2);
    border-left-color: var(--item-color, var(--color-accent-bright));
  }

  .item-number {
    font-family: var(--font-mono);
    font-size: 0.8rem;
    font-weight: 600;
    color: var(--color-electric);
    min-width: 24px;
    opacity: 0.7;
  }

  .item-title {
    font-family: var(--font-body);
    font-size: 0.9rem;
    font-weight: 500;
    color: var(--color-neutral-light);
    line-height: 1.3;
  }

  @media (max-width: 768px) {
    .nav-btn { width: 44px; height: 44px; }
    .nav-btn-prev { left: var(--spacing-lg); }
    .nav-btn-next { right: var(--spacing-lg); }
    .slide-counter { bottom: var(--spacing-lg); right: var(--spacing-lg); font-size: 1rem; }
    .module-indicator { display: none; }
    .hamburger-btn { display: flex; }
    .slide-drawer { display: block; }
    :global(.swiper-slide) { overflow-y: auto; padding-top: 80px; padding-bottom: 72px; }
  }
</style>
