---
inclusion: always
---

# Project structure

```
src/
  morse/          pure decoder, encoder, alphabet, adaptive timing
  input/          adapters: keyboard/switch, two-switch, webcam blink -> SignalEvent
  prediction/     phrase bank, history learning, ranking (pure)
  output/         speech synthesis, clipboard/share, caregiver alert
  ui/             React components for the "spirit telegraph" interface
  storage/        settings and history persistence
  app/            wiring: App.tsx, state store
tests/e2e/        Playwright tests, including accessibility audits
docs/             plan, Kiro usage log, demo script
```

- Unit and property tests live next to the code they test (`foo.ts`, `foo.test.ts`,
  `foo.property.test.ts`).
- Dependencies flow one way: `ui -> app -> (input, morse, prediction, output, storage)`.
  Core modules never import from `ui` or `app`.
