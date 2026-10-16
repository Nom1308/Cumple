# Página de cumpleaños de Sara

Regalo de Brandon para Sara (su novia), que cumple **19 años el lunes 19 de octubre de 2026**.
Brandon escribe en español, sin términos técnicos: responde en español, sencillo y cálido.
Le importa mucho que todo se vea "increíble", elegante y nostálgico, no infantil ni de "cantina".

## Dónde vive

- Todo es **un solo archivo: `index.html`** (HTML + CSS + JS, sin build).
- Repo: `github.com/Nom1308/Cumple`, rama `main`. Se publica con GitHub Pages al hacer push.
- Arriba del archivo está el objeto de configuración `C` ("LO EDITABLE"), que termina en
  `/* ===== FIN DE LO EDITABLE ===== */`. Textos, fechas, fotos, vinilos, deseos y créditos se cambian ahí.

## Carpetas

- `audios/`: los mensajes de voz de los vinilos, en mp3.
- `audios familia/`: los originales `.ogg` de WhatsApp. **No están en git** (se copian a mano entre computadores).
- `fotos/` (y `fotos/mini/` en miniatura), `fotos/ninez/` (canales de la tele), `musica/`, `videos/`.
- `vhs/`: `poscreditos.mp4` (escena poscréditos, ya está) y `secreto.mp4` (**pendiente**: mientras no
  exista, el canal 15 usa `videos/juntos.mp4`).

## Cómo está armada la experiencia

1. **Antes del cumpleaños: el cuarto.** Se va decorando solo entre `C.cuarto.desde` (jue 15 oct 12:00 m.)
   y `C.fechaCumple`; las cosas de `C.cuarto.cosas` aparecen repartidas en ese tiempo.
   - Tele "Saravisión": canal 19 bloqueado hasta el cumpleaños; los canales 1–14 son fotos de niñez.
   - VHS bajo la tele: se desbloquea al encontrar los 5 corazones escondidos (`C.secretos`). Una cinta
     entra en la ranura y el video secreto sale en el **canal 15**.
   - Caja de vinilos junto al tocadiscos (se elige de lomo en una caja de madera).
   - Regalos con vales: se abren desde `C.regalos.abren` (sáb 17 oct).
   - **Modo prueba:** tocar la pantalla de la tele 70 veces seguidas, con menos de 1 segundo entre toques.
2. **El día del cumpleaños** (o en modo prueba) se entra por el canal 19 y sigue la página:
   portada → dedicatoria → **álbum antiguo** (se abre, se vuelve luz y salen las fotos una a una) →
   **frasco** de papelitos (moño, etiqueta, luciérnagas) → **camino de estrellas** (título ⭐) →
   **cajita musical** (Sara le da cuerda manteniéndola presionada; la cuerda se gasta mientras suena) →
   **pastel** (momento del deseo, soplar con micrófono) → **carta** (sobre con lacre, se desdobla en tres) →
   medalla → **faroles de deseos** → **créditos estilo VHS** → escena poscréditos.

## Vinilos

- Lista en `C.vinilos`. Llegan **repartidos parejo** entre `cuarto.desde` y el cumpleaños, en el orden
  de la lista: agregar uno corre los horarios de los que faltan. Brandon cuida el orden (ej. pidió cambiar
  al papá con Deissi).
- Para agregar uno nuevo desde WhatsApp:
  `ffmpeg -i "audios familia/Nombre.ogg" -ac 1 -ar 44100 -b:a 96k audios/nombre.mp3`
  y agregar `{ de: "tu …", audio: "audios/nombre.mp3", dibujo: …, color: … }` a la lista.
- Videos nuevos: si no son mp4 H.264, convertir; siempre `-movflags +faststart` para que carguen rápido.

## Decisiones ya tomadas (no deshacer)

- **Ninguna polaroid lleva texto**, en ningún lado (mesa, vista en grande, carta, créditos).
- Gaby es **la prima** ("tu tía Anyie y tu prima Gaby").
- La carta firma **"Te amo muchísimo, Brandon"**; se desdobla ya escrita (sin escritura palabra por palabra).
- La polaroid de la carta es `fotos/09-premios.jpg` y el texto la rodea (flota).
- Los créditos terminan en "Feliz cumpleaños, amor mío" (usa `C.apodo`).

## Estilo visual

Noche morada oscura, dorado `#f5c97a`, rosa `#ee8fae`, lila, papel `#fbf5ec`.
Fuentes: Caveat (`--mano`), Fraunces (`--serif`), VT323 (pantallas/VHS).
Antes de crear una clase o id nuevo, **buscar que no exista** (ya pasó con `.sobre` y `.palabra`).

## Cómo trabajamos

- Mostrar el resultado y **preguntar antes de subir**; Brandon responde "súbelo".
- Commits en español describiendo el cambio, terminando con
  `Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com>`. Escribir el mensaje en un archivo y usar
  `git commit -F` (en PowerShell las comillas del mensaje rompen el comando). Luego `git push origin main`.

## Probar sin el celular

Chrome headless con la página en un iframe de 375×812, inyectando un script que activa el modo prueba
(`sessionStorage.setItem("cumple-prueba","1")`) y hace clics. Cuidado con el tiempo virtual:
- Las animaciones CSS se quedan atrasadas: usar `document.getAnimations().forEach(a => a.finish())`
  antes de la captura.
- Los `setTimeout` se adelantan hasta el final del tiempo: para congelar un momento, reemplazar
  `window.setTimeout` por una función vacía justo después.
- `scroll-behavior: smooth` no avanza: forzar `behavior: "instant"` en `scrollIntoView`/`scrollTo`.
