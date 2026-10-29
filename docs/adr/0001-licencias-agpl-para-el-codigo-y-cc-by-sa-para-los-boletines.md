# 1. Licencias: AGPL v3 para el código y CC BY-SA 4.0 para los boletines

Fecha: 2026-10-29 · Estado: aceptado

## Contexto

La web del boletín (`https://chatgpt-ia-edu.github.io/boletin/`) está en el
Repositorio de recursos educativos digitales de Vibe Coding Educativo, que solo admite
recursos con una licencia abierta que conste en el código. La revisión del 29-10-2026
la marcó como «sin licencia»: no había archivo LICENSE ni licencia en la web. Juanjo
pidió añadírsela.

## Decisión

- El código de la web (`index.html`, `script.js`, `style.css`) se publica bajo
  AGPL-3.0-or-later: archivo `LICENSE` y línea `SPDX-License-Identifier` al inicio de
  cada archivo.
- Los boletines y los textos de la web, bajo CC BY-SA 4.0 (`LICENSE-CONTENIDOS`), la
  misma licencia que declara el boletín de Vibe Coding Educativo.
- El pie dice la autoría, las dos licencias con su enlace, el código fuente, que los
  boletines los redacta una IA a partir de los mensajes del grupo, el nivel 4 del MIAE
  para la web y las bibliotecas que usa (Marked y Tailwind CSS, las dos MIT).

## Alternativas descartadas

- Una sola licencia CC BY-SA para todo, como en el boletín de VCE: la guía «Vibe coding
  responsable» recomienda AGPL v3 para el código.

## Consecuencias

- Los archivos de código nuevos llevan la línea SPDX desde el principio.
