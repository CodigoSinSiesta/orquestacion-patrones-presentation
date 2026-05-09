# Patrones de Orquestación

Presentación interactiva (22 slides) sobre **patrones de orquestación de agentes IA** — 10 patrones, 3 perspectivas, la misma conclusión: la arquitectura importa más que el modelo.

**Live**: [codigosinsiesta.github.io/orquestacion-patrones-presentation](https://codigosinsiesta.github.io/orquestacion-patrones-presentation)

## Tesis

> 10 patrones. 3 perspectivas. La misma conclusión:<br>
> **la arquitectura importa más que el modelo.**

## Stack

- **Astro 5** + **Svelte 5** + **TypeScript** estricto
- **Tailwind CSS 4** + tokens del sistema visual canónico de Código Sin Siesta
- **GSAP 3** para animaciones de entrada y stagger
- Diagramas SVG propios animados

## Módulos y slides (22)

### Módulo A — Taxonomía Evolutiva (slides 1–7)

1. **Hero** — título, tesis, autor.
2. **Mapa** — visión general de los tres módulos.
3. **Intro a la taxonomía** — por qué una escalera, no un menú.
4. **Escalera base** — herramienta directa, prompt chaining, routing.
5. **Escalera media** — paralelización, orchestrator-workers.
6. **Escalera top** — eval-optimizer, agentes autónomos.
7. **Diagrama de capas** — cómo se apilan los niveles en un sistema real.

### Módulo B — Por Problema (slides 8–14)

8. **Intro a los problemas** — por qué los problemas dictan el patrón.
9. **Bias de confirmación** — el agente que valida su propio trabajo.
10. **Desbordamiento de contexto** — ventana finita, misión infinita.
11. **Paralelismo sin coordinación** — fan-out sin fan-in fiable.
12. **Ausencia de tests** — cómo se evalúa lo que no tiene output determinista.
13. **Obsolescencia de instrucciones** — prompts que envejecen.
14. **Supervisión humana** — cuándo y cómo interrumpir al agente.

### Módulo C — Convergencias (slides 15–21)

15. **Intro a las convergencias** — lo que Anthropic, OpenAI, Factory y academia dicen a la vez.
16. **Harness como modelo mental** — el harness explica más varianza que el modelo.
17. **Gen / Eval** — separar la generación de la evaluación.
18. **Lógica en texto** — orquestación en prompts que mejora sola con cada nuevo modelo.
19. **Estado fuera del contexto** — persistencia en disco para misiones de semanas.
20. **Matriz de patrones** — tabla cruzada problema × patrón × nivel.
21. **Conclusiones** — 4 takeaways para llevarse de la sala.
22. **Cierre** — recursos y autor.

## Desarrollo

```bash
npm install
npm run dev      # → http://localhost:4328/orquestacion-patrones-presentation
npm run build    # type-check + build estático en dist/
```

## Despliegue

GitHub Pages desde `main`. La `base` está fijada a `/orquestacion-patrones-presentation` en `astro.config.mjs`.

## Autor

Alejandro de la Fuente · Tech Lead · NTT Data · GDNE  
[tellmealex.dev](https://tellmealex.dev) · [GitHub](https://github.com/TellMeAlex) · [LinkedIn](https://es.linkedin.com/in/alejandro-de-la-fuente)
