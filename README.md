# BytesBricks · SimPlant — Pitch Deck

Pitch deck de **BytesBricks / SimPlant** publicado con GitHub Pages.

**Ver online:** https://bytesbricksai.github.io/bytesbricks.github.io/

## Qué es

Presentación de una sola página, **100 % autocontenida**: HTML + CSS + JS en línea, sin
dependencias locales. Las tipografías se cargan desde Google Fonts (HTTPS). Incluye toggle
de idioma **ES/EN** y navegación por teclado (`↑ ↓ ← →` · `Espacio` · `Home/End`).

## Estructura

| Archivo | Rol |
|---|---|
| `index.html` | El deck completo — es lo que sirve GitHub Pages. |
| `.nojekyll` | Desactiva el procesamiento Jekyll; el HTML se sirve tal cual. |

## Desarrollo local

Abrí `index.html` en cualquier navegador. No requiere build ni servidor.

## Publicación (GitHub Pages)

Settings → Pages → **Deploy from a branch** · Branch `main` · Folder `/ (root)`.
Cada push a `main` republica el sitio automáticamente.
