# Design: Morse decoder

## Overview
A pure, synchronous state machine in `src/morse/`. Callers feed it signal events and
regular `tick(t)` calls (for example from `requestAnimationFrame`); it returns outputs.
No timers, no DOM, no clock inside, so it is fully deterministic under test.

## Modules
| File | Responsibility |
|---|---|
| `alphabet.ts` | ITU table: A–Z, 0–9, `. , ? ' ! / ( ) & : ; = + - " @`, plus command codes (Req 5) |
| `encoder.ts` | `encode(text, unitMs) -> SignalEvent[]` used by tests and the "practice/preview" UI |
| `timing.ts` | `classifyPress`, `classifyGap`, `updateUnit` (pure functions, Req 1–3) |
| `decoder.ts` | `createDecoder(config)` returning `{ push(event), tick(t), state() }` |
| `types.ts` | shared types below |

## Types
```ts
type SignalEvent = { kind: "down" | "up"; t: number; source?: "single" | "dot" | "dash" };

type DecoderOutput =
  | { type: "symbol"; symbol: "." | "-" }
  | { type: "char"; char: string }
  | { type: "space" }
  | { type: "unknown"; symbols: string }
  | { type: "command"; command: "delete" | "send" };

type DecoderConfig = {
  unitMs: number;          // default 200
  adaptive: boolean;       // default true
  twoSwitch: boolean;      // default false
  debounceMs: number;      // default 30
  minUnitMs: number;       // 80
  maxUnitMs: number;       // 2000
};

type DecoderState = {
  unitMs: number;
  pending: string;         // symbols for the current letter
  pressedAt: number | null;
  lastReleaseAt: number | null;
  charCommittedSinceGap: boolean;
  spaceEmitted: boolean;
  history: Array<{ symbol: "." | "-"; durationMs: number }>; // last 20
};
```

## State machine
- `push(down)`: if already pressed, ignore (Req 6.3). Record `pressedAt`.
- `push(up)`: if not pressed, ignore. Duration = `t - pressedAt`.
  Below debounce → ignore. Otherwise classify (or use `source` in two-switch mode),
  append to `pending`, push to history, maybe update unit, emit `symbol`.
- `tick(t)`: while released, gap = `t - lastReleaseAt`.
  - gap ≥ 3 units and `pending` non-empty → look up code: command, char, or `unknown`; clear `pending`.
  - gap ≥ 7 units, a char was committed, and no space emitted yet → emit `space` once.

## Unit estimation (Req 3)
Estimate = mean over history of `duration / (symbol === "." ? 1 : 3)`.
New unit = clamp(estimate, unit × 0.75, unit × 1.25), then clamp to [min, max].
Only runs when adaptive, not two-switch, and history has ≥ 5 entries.

## Error handling
The decoder never throws on input. Invalid configs throw once, at creation.

## Testing strategy
- Unit tests: one per acceptance criterion in Req 1, 2, 4, 5.
- Property tests (fast-check) in `decoder.property.test.ts`:
  - P1 round trip (Req 6.1), P2 jitter round trip (Req 6.2),
  - P3 never throws on arbitrary event arrays (Req 6.3),
  - P4 unit bounds and max 25% step (Req 3.3, 3.4, 6.4).
