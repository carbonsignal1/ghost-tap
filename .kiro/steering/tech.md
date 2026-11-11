---
inclusion: always
---

# Tech stack and conventions

## Stack
- **Vite + React + TypeScript** (strict mode), single-page app, deployable as static files.
- **Vitest** for unit tests, **fast-check** for property-based tests.
- **Playwright** for end-to-end and accessibility checks (with `@axe-core/playwright`).
- **MediaPipe Tasks Vision (Face Landmarker)** for blink detection, running fully in the browser.
- **Web Speech API** (`speechSynthesis`) for spoken output.
- No backend for the MVP. Persist settings and phrase history in `localStorage`
  behind a small storage module that tolerates storage being unavailable.

## Rules
- Core logic (`src/morse`, `src/prediction`) is **pure TypeScript**: no React, no DOM,
  no timers. Time is always passed in as a number (ms) so it can be tested deterministically.
- Every requirement in a spec that describes an invariant gets a **property-based test**.
  Name them `*.property.test.ts`.
- Never use `Date.now()` or `performance.now()` inside core logic; inject a clock.
- Input adapters convert device signals into `SignalEvent`s and nothing else.
- Prefer small modules with one export each over large utility files.
- Commands: `npm run dev`, `npm test`, `npm run test:e2e`, `npm run build`.
