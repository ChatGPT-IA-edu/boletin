# Repository Guidelines

## Project Structure & Modules
- `index.html`: UI principal con Tailwind CDN, modales y layout.
- `script.js`: Lógica de carga (fetch de `config.json` y CSV), filtrado, modal, tema.
- `style.css`: Estilos complementarios a Tailwind (transiciones, prose, resaltados).
- `config.json`: Mapa año → URL CSV pública del boletín.
- `chatgptTelegram.jpeg`: Favicon/logo.  Documentación: `guia_estilo_boletinia.md`.

## Build, Test, and Development
- Servir localmente (evita problemas CORS): `python3 -m http.server 8000` y abre `http://localhost:8000`.
- Apertura rápida: doble clic en `index.html` (la carga remota puede fallar sin servidor).
- Comprobaciones manuales: selector de año, filtros, búsqueda, enlace compartible, modal (cuerpo/FAQ/índice), tema claro/oscuro, embeds de YouTube y audio. Revisa la consola sin errores.

## Coding Style & Naming
- General: indentación de 4 espacios; archivos y IDs en minúsculas con guiones (`kebab-case`).
- JavaScript: ES2020+, `const`/`let`, funciones y variables en `camelCase`, siempre con `;`. Evita dependencias nuevas.
- HTML/CSS: Utiliza utilidades Tailwind y clases existentes; no estilos inline. Mantén `darkMode: 'class'`.

## Testing Guidelines
- No hay framework de tests. Prioriza pruebas manuales end-to-end en navegador.
- Casos mínimos: carga `config.json`, parseo CSV, filtrado por mes/semana, navegación directa `?boletin=ID`, cierre de modal y control de audio único.

## Commit & Pull Requests
- Commits breves en imperativo (español). Ej.: `feat: filtro por semana`, `fix: scroll a titular`.
- Ramas: `feature/...`, `fix/...`, `chore/...`. Crear PR con descripción, pasos de prueba y capturas si afectan a UI.
- Flujo sugerido: `git checkout -b feature/x`; `git commit -m "feat: ..."`; `git push -u origin feature/x`; `gh pr create --fill`.

## Agent-Specific Notes
- Respeta `CONFIG_URL` y `CORS_PROXY` en `script.js`.
- No elimines `defer` de scripts ni el preload del tema.
- En depuración, ignora el aviso de Tailwind CDN sobre producción; este proyecto usa CDN.
- Para contenido del boletín, sigue `guia_estilo_boletinia.md`.

