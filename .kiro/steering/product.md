---
inclusion: always
---

# Product: Ghost Tap

Ghost Tap is a browser-based communication aid that lets people with severe motor or
speech impairments talk using a **single input**: one key, one accessibility switch,
a sip-and-puff device, or an eye blink seen by the webcam. Input is Morse code,
"resurrected" from the telegraph era, with modern help: timing that adapts to the user,
AI phrase prediction, and spoken output.

Hackathon: Kiroween 2026, **Resurrection** category (dead tech: the telegraph and Morse code).

## Who it is for
- Primary: people with ALS, cerebral palsy, spinal cord injury, locked-in syndrome or
  post-stroke conditions who can reliably make one small movement.
- Secondary: caregivers and speech-language therapists who set it up.

## Product principles (in priority order)
1. **Never lose or block the user's input.** A missed or misread tap is the worst failure.
2. **Forgiving over fast.** Adapt to the user's rhythm; never demand a fixed speed.
3. **One input is enough.** Every feature must be reachable with a single switch.
4. **Private by default.** Camera frames and typed text stay on the device unless the user sends them.
5. **Spooky design serves function.** The "spirit telegraph" visuals must make input
   state *more* visible (what was registered, what is pending), never less.

## Non-goals
- Not a medical device; never make medical claims in UI or docs.
- Not a general Morse-learning game.

## Core features (MVP)
- Morse decoder with adaptive timing (spec: `morse-decoder`)
- Input adapters: keyboard/switch, two-switch mode, webcam blink
- Phrase prediction from a local phrase bank plus learned history
- Text-to-speech output and quick "send to caregiver" action
- "Spirit telegraph" UI with high-contrast and reduced-motion modes
