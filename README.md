# Biblia de Estudio RVR1960

App web de estudio bíblico (Reina-Valera 1960) en una sola página. Dos funciones principales:

1. **Biblia a la vista + selector de libros y versículos**
   - Los 66 libros (Antiguo y Nuevo Testamento) en la barra lateral, con filtro de búsqueda.
   - Grilla de capítulos y navegación anterior/siguiente (también con las flechas ← →).
   - Búsqueda de texto en toda la Biblia (`Ctrl/Cmd + K`).
   - Tamaño de letra ajustable (A− / A+) y **temas de colores** (🎨): Original, Pergamino y Esmeralda.

2. **Léxico Strong hebreo y griego** — *sin API key*
   - Pestaña **Strong**: diccionario completo (8.674 entradas hebreas, 5.523 griegas) buscable por número (`H430`, `G26`), por palabra original (`אלהים`, `ἀγάπη`) o en castellano (`amor`, `pacto`, `gracia`).
   - Dato real y verificable, no generado por IA.

3. **Referencias cruzadas reales** — *sin API key*
   - Clic en el **número de versículo** → hasta 12 referencias cruzadas clásicas, con su texto RVR, ordenadas por relevancia. Clic en cualquiera para saltar allí.

4. **Capa de IA** (requiere API key de Claude)
   - Clic en cualquier **palabra** → la IA identifica qué término original hay detrás y explica su peso teológico; el número de Strong que devuelve se **contrasta contra el diccionario real** y se muestra ese dato, no el que la IA recuerde.
   - Botón de **síntesis teológica** sobre las referencias cruzadas.
   - Comentarios en el estilo de Calvino, Matthew Henry y Spurgeon.

## El enfoque: híbrido

La estructura sale de **datos abiertos reales** (instantáneos, offline, verificables) y la **IA** se usa encima para explicar y sintetizar — nunca para inventar el dato. Cada bloque de la interfaz está marcado como `dato real` o `generado por IA`, así siempre sabés qué estás leyendo.

Sin API key la app ya sirve para estudiar: lectura, búsqueda, léxico Strong completo y referencias cruzadas.

## Seguridad: app blindada, sin servidor 🔒

Esta app es un **sitio 100% estático**. **No hay servidor ni clave compartida.**

- La IA se llama **directo a Anthropic desde tu navegador**, usando **tu propia API key**.
- Tu clave se guarda **solo en tu navegador** (`localStorage`) y se envía **únicamente a Anthropic**. No pasa por ningún servidor intermedio ni queda en el código.
- Como no hay clave en el servidor, **nadie de afuera puede gastar tus créditos**: cada persona que use la IA debe poner su propia clave. Un visitante sin clave solo puede leer y buscar.

> Recomendado: en `console.anthropic.com` podés fijar un **límite de gasto mensual** por las dudas.

## Desplegar en Netlify (o cualquier hosting estático)

No necesita funciones ni variables de entorno. Solo servir los archivos:

1. Conectá el repositorio en Netlify (o `netlify deploy`). `netlify.toml` publica la raíz.
2. **No definas `ANTHROPIC_API_KEY` en Netlify** — no se usa y no hace falta.
3. Abrí el sitio, tocá ⚙, pegá tu API key y listo.

Sirve igual en GitHub Pages, Vercel, o cualquier hosting de archivos estáticos.

## Uso local

```bash
python3 -m http.server 8899
# abrir http://localhost:8899/index.html
```

Todo funciona en local, incluida la IA (el navegador habla directo con Anthropic).

## Datos y licencias

| Archivo | Contenido | Fuente | Licencia |
|---|---|---|---|
| `biblia.json` | Texto RVR1960 completo (66 libros) | — | — |
| `data/strong-h.json` | 8.674 entradas del léxico hebreo | *A Concise Dictionary of the Words in the Hebrew Bible*, James Strong (1894) — edición digital de [OpenScriptures](https://github.com/openscriptures/strongs) | CC BY-SA |
| `data/strong-g.json` | 5.523 entradas del léxico griego | *Dictionary of Greek Words*, James Strong (1890) — edición digital de [OpenScriptures](https://github.com/openscriptures/strongs) | CC BY-SA |
| `data/xrefs.json` | Referencias cruzadas de 29.335 versículos | [OpenBible.info](https://www.openbible.info/labs/cross-references/) | CC BY |

Los tres archivos de `data/` se cargan **en diferido**: solo se descargan la primera vez que abrís la pestaña que los usa. El modelo de IA por defecto es `claude-sonnet-4-5-20250929`.
