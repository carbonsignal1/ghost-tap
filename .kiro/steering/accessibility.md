---
inclusion: fileMatch
fileMatchPattern: "src/ui/**/*"
---

# Accessibility rules for UI work

Ghost Tap's users depend on it to communicate. Treat these as hard requirements.

- Meet **WCAG 2.2 AA**: text contrast at least 4.5:1, UI component contrast at least 3:1,
  including in the dark "spooky" theme.
- Provide a **high-contrast mode** and honour `prefers-reduced-motion`: flicker, glow and
  ghost animations become static when reduced motion is on.
- **No flashing** more than 3 times per second anywhere (seizure risk).
- Every state change the user must notice (dot registered, letter committed, phrase
  spoken, input lost) has **both** a visual and a non-visual cue (sound or ARIA live region).
- All controls are reachable with a **single switch** via scanning, and with keyboard alone.
- Use semantic HTML and ARIA live regions (`aria-live="polite"` for decoded text,
  `"assertive"` only for errors like camera loss).
- Minimum touch target 44×44 px. Minimum body text 18 px; decoded text at least 32 px.
- Spooky visuals must never hide the current input state. If in doubt, show more clearly.
