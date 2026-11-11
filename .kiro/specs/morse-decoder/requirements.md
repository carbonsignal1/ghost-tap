# Requirements: Morse decoder

## Introduction
The decoder turns a stream of timed press/release signals from any single input into
text. It is the heart of Ghost Tap and must be forgiving of irregular timing, because
users may have tremors, fatigue or slow movement.

## Glossary
- **Signal event**: `{ kind: "down" | "up", t: number }`, a press or release at time `t` (ms).
- **Unit**: the length of one dot, in ms. Dash = 3 units, gap between letters = 3 units,
  gap between words = 7 units.
- **Symbol**: a dot (`.`) or dash (`-`).

## Requirement 1: Classify presses into dots and dashes
**User story:** As a user with one switch, I want short presses read as dots and long
presses as dashes, so that I can enter Morse with a single input.

### Acceptance criteria
1. WHEN a press lasts less than 2 units THE SYSTEM SHALL register a dot.
2. WHEN a press lasts 2 units or more THE SYSTEM SHALL register a dash.
3. WHEN a press is shorter than the debounce threshold (default 30 ms) THE SYSTEM SHALL ignore it.
4. WHEN a symbol is registered THE SYSTEM SHALL emit a `symbol` output immediately, so the UI can confirm it.

## Requirement 2: Commit letters and words from gaps
**User story:** As a user, I want pauses to end letters and words, so I don't need extra controls.

### Acceptance criteria
1. WHEN the input stays released for 3 units or more after a symbol THE SYSTEM SHALL commit the pending symbols as one character.
2. WHEN the input stays released for 7 units or more after a character THE SYSTEM SHALL emit a word break (space) once.
3. WHEN pending symbols do not match any known code THE SYSTEM SHALL emit an `unknown` output with those symbols and clear them, without throwing.
4. THE SYSTEM SHALL decide gaps from a `tick(t)` call so the caller controls time.

## Requirement 3: Adapt to the user's rhythm
**User story:** As a user who taps slowly or unevenly, I want the decoder to learn my speed, so I am not forced to match a fixed tempo.

### Acceptance criteria
1. THE SYSTEM SHALL start from a configurable unit (default 200 ms).
2. WHEN at least 5 symbols have been registered THE SYSTEM SHALL re-estimate the unit from the most recent 20 symbols (dots count as 1 unit, dashes as 3).
3. THE SYSTEM SHALL never change the unit by more than 25% in a single update.
4. THE SYSTEM SHALL keep the unit within 80 ms and 2000 ms.
5. WHERE adaptive timing is turned off THE SYSTEM SHALL keep the configured unit fixed.

## Requirement 4: Two-switch mode
**User story:** As a user with severe tremor, I want one switch for dot and another for dash, so timing doesn't matter for symbols.

### Acceptance criteria
1. WHERE two-switch mode is on THE SYSTEM SHALL map each signal's `source` (`"dot"` or `"dash"`) directly to a symbol, ignoring press length.
2. WHERE two-switch mode is on THE SYSTEM SHALL still use gaps to commit letters and words.

## Requirement 5: Editing commands
**User story:** As a user, I want to fix mistakes and finish messages using Morse alone.

### Acceptance criteria
1. WHEN the pending symbols are 8 dots (`........`, the telegraph "error" signal) THE SYSTEM SHALL emit a `delete` command instead of a character.
2. WHEN the pending symbols are `.-.-.` (prosign AR, "end of message") THE SYSTEM SHALL emit a `send` command.

## Requirement 6: Robustness (properties)
**User story:** As a user, I need the decoder to never crash or lose text, whatever I do.

### Acceptance criteria
1. FOR ANY string made of supported characters, encoding it to timed signals and decoding them SHALL return the same string (round trip).
2. FOR ANY timing jitter of up to ±30% of a unit on each press and gap, the round trip SHALL still hold.
3. FOR ANY sequence of signal events, including out-of-order or repeated `down`/`up`, the decoder SHALL not throw.
4. FOR ANY sequence of updates, the unit SHALL stay within the bounds of Requirement 3.4.
