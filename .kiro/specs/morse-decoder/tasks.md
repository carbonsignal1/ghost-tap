# Implementation plan: Morse decoder

- [ ] 1. Set up the project
  - Scaffold Vite + React + TypeScript (strict), add Vitest and fast-check, add `npm test`.
  - _Requirements: none (setup)_

- [ ] 2. Define types and the alphabet
  - [ ] 2.1 Create `src/morse/types.ts` with the types from the design.
  - [ ] 2.2 Create `src/morse/alphabet.ts` with the ITU table and the two command codes, plus a reverse lookup.
  - [ ] 2.3 Unit test: every code is unique and every character maps back to itself.
  - _Requirements: 5.1, 5.2_

- [ ] 3. Implement timing functions
  - [ ] 3.1 `classifyPress` and `classifyGap` in `src/morse/timing.ts`.
  - [ ] 3.2 `updateUnit` with the 25% step limit and min/max clamping.
  - [ ] 3.3 Unit tests for the boundaries (exactly 2 units, exactly 3 units, exactly 7 units).
  - [ ] 3.4 Property test: unit stays in bounds and never moves more than 25% per update.
  - _Requirements: 1.1, 1.2, 2.1, 2.2, 3.1–3.5, 6.4_

- [ ] 4. Implement the encoder
  - [ ] 4.1 `encode(text, unitMs)` producing signal events with correct gaps.
  - [ ] 4.2 Unit test with "SOS" and "HI THERE".
  - _Requirements: 6.1 (test support)_

- [ ] 5. Implement the decoder state machine
  - [ ] 5.1 `createDecoder` with `push`, `tick`, `state`.
  - [ ] 5.2 Debounce and duplicate-event handling.
  - [ ] 5.3 Letter and word commit on `tick`; `unknown` output for unmatched codes.
  - [ ] 5.4 Two-switch mode.
  - [ ] 5.5 Command outputs for delete and send.
  - [ ] 5.6 Unit tests for each acceptance criterion in Requirements 1, 2, 4, 5.
  - _Requirements: 1.1–1.4, 2.1–2.4, 4.1, 4.2, 5.1, 5.2_

- [ ] 6. Property-based tests
  - [ ] 6.1 P1 round trip for any supported string.
  - [ ] 6.2 P2 round trip with ±30% jitter.
  - [ ] 6.3 P3 decoder never throws on arbitrary event arrays.
  - _Requirements: 6.1, 6.2, 6.3_

- [ ] 7. Developer preview
  - [ ] 7.1 Minimal page: hold Space to tap, show symbols, decoded text and current unit.
  - _Requirements: 1.4_
