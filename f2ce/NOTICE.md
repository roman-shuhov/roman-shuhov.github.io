# Notice

This folder contains a **modified version** of Fallout 2 Community Edition
(fallout2-ce) by Alexander Batalov and contributors,
<https://github.com/alexbatalov/fallout2-ce>. It is distributed free of charge
for non-commercial use under the Sustainable Use License; the full terms are in
[LICENSE.md](LICENSE.md).

## What was modified

These changes were made in October 2026 for the termit.dev web port, so the
engine runs in a web browser:

- **Build:** compiled to WebAssembly with Emscripten 3.1.52 and SDL 2.24.2
  (`CMakeLists.txt`).
- **Browser file layer** (`os/web/library_f2web.js`): the visitor supplies the
  game files. They are read lazily from browser storage, and the engine is
  suspended with Asyncify while data loads.
- **Responsiveness:** the engine hands control back to the browser during long
  input-polling loops (`src/platform/web/`, `src/input.cc`, `src/svga.cc`,
  `src/delay.cc`, `src/fps_limiter.cc`).
- **Input:** the game cursor follows the browser pointer directly instead of
  using relative mode or pointer lock (`src/dinput.cc`, `src/mouse.cc`). Touch
  hints are set as on mobile builds (`src/win32.cc`).
- **Audio:** a larger audio buffer is used in browsers (`src/audio_engine.cc`).
- **Saves:** the page is told when saves and the config are written, so it can
  store them in the browser (`src/loadsave.cc`, `src/game_config.cc`).
- **Loader page:** `index.html` is new.

The complete source changes are in [web-port.patch](web-port.patch), made
against upstream commit `e97087b`.

No game data is included. Fallout is a trademark of Bethesda Softworks LLC.
This project is not affiliated with or endorsed by Bethesda Softworks,
Interplay, or the fallout2-ce project.
