# Biblia de Estudio RVR1960

App web de estudio bíblico (Reina-Valera 1960) en una sola página. Dos funciones principales:

1. **Biblia a la vista + selector de libros y versículos**
   - Los 66 libros (Antiguo y Nuevo Testamento) en la barra lateral, con filtro de búsqueda.
   - Grilla de capítulos y navegación anterior/siguiente (también con las flechas ← →).
   - Búsqueda de texto en toda la Biblia (`Ctrl/Cmd + K`).
   - Tamaño de letra ajustable (A− / A+).

2. **Traducción y explicación rica de las palabras originales** (requiere API key de Claude)
   - Clic en cualquier **palabra** → análisis del original hebreo/griego: morfología, número de Strong, léxico ampliado, aporte teológico y ocurrencias clave.
   - Clic en el **número de versículo** → referencias cruzadas y comentarios (Calvino, Matthew Henry, Spurgeon).

## Cómo funciona la IA

Las llamadas al modelo pasan por una **Netlify Function** (`netlify/functions/claude.js`) para no exponer la clave en el navegador. La clave se resuelve así:

- **Clave del usuario**: la que se ingresa en la app (⚙) se guarda en `localStorage` y se envía a la función en el header `x-user-key`. Útil para uso personal.
- **Clave del servidor**: si no se envía clave de usuario, la función usa la variable de entorno `ANTHROPIC_API_KEY` configurada en Netlify. Útil para compartir la app sin pedir clave a cada persona.

Sin ninguna clave, la lectura, los selectores y la búsqueda funcionan igual; solo se desactiva el análisis con IA.

## Desplegar en Netlify

1. Conectá este repositorio en Netlify (o `netlify deploy`).
2. La configuración ya está en `netlify.toml` (publica la raíz y sirve las funciones desde `netlify/functions`).
3. (Opcional) En *Site settings → Environment variables* definí `ANTHROPIC_API_KEY` con tu clave de [console.anthropic.com](https://console.anthropic.com).

## Uso local

Servir la carpeta con cualquier servidor estático, por ejemplo:

```bash
python3 -m http.server 8899
# abrir http://localhost:8899/index.html
```

> Las funciones de IA necesitan la Netlify Function; en modo estático local funcionan la lectura, los selectores y la búsqueda. Para probar la IA localmente usá `netlify dev`.

## Datos

`biblia.json` contiene el texto completo RVR1960 (66 libros → capítulos → versículos). El modelo usado por defecto es `claude-sonnet-4-5-20250929`.
