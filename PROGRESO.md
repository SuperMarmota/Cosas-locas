# Progreso – Generador de códigos para Calendario de Adviento

## Contexto
Generador de códigos QR y de barras para tarjetas de un calendario de adviento.
Por ahora funciona con **códigos ficticios**; también permite cargar una lista de códigos reales.

## Cómo correrlo
```
npm install
npm run dev
```
Abrir http://localhost:5173 (si se ve en blanco tras instalar librerías: `npm run dev -- --force`).

## Funcionalidades
- Genera N códigos ficticios únicos `ADV26-XXXX-XXXX` (sin caracteres confusos 0/O, 1/I/L).
- Selector arriba: **Código QR** (guarda la URL `?codigo=`) o **Código de barras** CODE128 (solo el código).
- Cada **PNG** lleva el código escrito debajo, por si la cámara falla y hay que teclearlo.
- Descargar PNG individual, **ZIP** con todos los PNG + `codigos.csv`, CSV suelto, imprimir.
- Cargar códigos reales: pegarlos o subir un CSV/TXT (uno por línea).
- La casilla **Cantidad** acepta cualquier número entero desde 1, sin máximo (con muchos miles el navegador puede ponerse lento por la memoria de las imágenes). Si el número no es válido, sale un aviso y el botón se desactiva. Con Enter también se genera.
- **Barra de progreso** con porcentaje y tiempo restante mientras se generan las imágenes (también al cambiar QR/barras, cargar códigos reales y armar el ZIP).
- Las imágenes se generan todas juntas en `src/App.jsx`, así el ZIP las reutiliza y sale más rápido.

## Diseño
- Fondo aguamarina con ondas y título en pastilla gris verdosa.
- Apartados como tarjetas de color: Simulación (naranja), Códigos reales (verde azulado), Exportar (azul).
- Barra de progreso amarilla con relleno naranja; cada tarjeta lleva un marcador amarillo con su número.
- Tipografía Signika (Google Fonts). Colores definidos como variables en `src/index.css` (`--aqua`, `--pizarra`, `--naranja`, `--verde`, `--azul`, `--amarillo`).

## Archivos clave
| Archivo | Qué hace |
|---|---|
| `src/config.js` | URL del QR, prefijo, cantidad inicial |
| `src/utils/codigos.js` | Generar/parsear códigos, CSV, descargas |
| `src/utils/imagenes.js` | Arma el PNG (símbolo + texto) |
| `src/components/TarjetaQR.jsx` | Tarjeta de cada código (recibe la imagen ya hecha) |
| `src/components/BarraProgreso.jsx` | Barra con %, conteo y tiempo restante |
| `src/utils/progreso.js` | Genera todos los PNG avisando el avance |
| `src/App.jsx` | Pantalla principal, selector, exportar |

## Posibles mejoras
- [ ] Configurar `URL_BASE` en `src/config.js` con la URL real.
- [ ] Diseño de tarjeta imprimible con logo.
- [ ] Página destino + backend que valide el código y lo marque como usado.
