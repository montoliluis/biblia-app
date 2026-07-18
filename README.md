# Biblia de Estudio RVR1960

App web de estudio bíblico (Reina-Valera 1960) en una sola página. Dos funciones principales:

1. **Biblia a la vista + selector de libros y versículos**
   - Los 66 libros (Antiguo y Nuevo Testamento) en la barra lateral, con filtro de búsqueda.
   - Grilla de capítulos y navegación anterior/siguiente (también con las flechas ← →).
   - Búsqueda de texto en toda la Biblia (`Ctrl/Cmd + K`).
   - Tamaño de letra ajustable (A− / A+) y **temas de colores** (🎨): Original, Pergamino y Esmeralda.

2. **Traducción y explicación rica de las palabras originales** (requiere API key de Claude)
   - Clic en cualquier **palabra** → análisis del original hebreo/griego: morfología, número de Strong, léxico ampliado, aporte teológico y ocurrencias clave.
   - Clic en el **número de versículo** → referencias cruzadas y comentarios (Calvino, Matthew Henry, Spurgeon).

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

## Datos

`biblia.json` contiene el texto completo RVR1960 (66 libros → capítulos → versículos). El modelo usado por defecto es `claude-sonnet-4-5-20250929`.
