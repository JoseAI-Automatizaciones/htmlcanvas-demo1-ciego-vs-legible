# Demo 1 — Canvas ciego vs. legible

Demostración mínima de la API **HTML-in-Canvas**. Dos columnas idénticas en
pantalla: la izquierda es un `<canvas>` tradicional (solo píxeles, invisible
para una IA o un buscador); la derecha usa `drawElementImage()` para dibujar
HTML **real** dentro del canvas, que sigue siendo legible, seleccionable e
indexable.

## Cómo verlo funcionando

La API es experimental (Origin Trial, Chrome 148+). Tienes dos caminos:

### Opción A — Local, con flag (para probar tú mismo)
1. Abre **Chrome Canary 149+** o **Brave**.
2. Ve a `chrome://flags/#canvas-draw-element` y ponlo en **Enabled**. Reinicia.
3. Abre `index.html`.

Si el navegador no soporta la API, la página lo detecta y muestra un banner +
una versión degradada (no se rompe).

### Opción B — Público, con Origin Trial (para que funcione en Vercel sin flag)
1. Despliega este repo en Vercel y copia tu URL final (`https://TU-DEMO.vercel.app`).
2. Registra ese origin exacto en el Origin Trial:
   https://developer.chrome.com/origintrials#/view_trial/3478467762190286849
3. Copia el token que te da y pégalo en `index.html`, descomentando:
   ```html
   <meta http-equiv="origin-trial" content="PEGA_TU_TOKEN_AQUI" />
   ```
4. Redespliega. Ahora cualquier visitante en Chrome lo ve sin tocar flags.

> El token es **por origin**: cada demo (cada subdominio de Vercel) necesita su
> propio token.

## API usada
- `<canvas layoutsubtree>` — opta a los hijos del canvas a participar en layout/hit-testing.
- `ctx.drawElementImage(element, x, y)` — dibuja el elemento y devuelve un `DOMMatrix`.
- `element.style.transform = transform.toString()` — alinea el DOM con lo dibujado (clic/hover/selección nativos).
- `canvas.onpaint` — se redispara cuando el HTML hijo cambia.

## Estado
Experimental. Solo Chromium (Chrome/Brave). No funciona con iframes cross-origin.
