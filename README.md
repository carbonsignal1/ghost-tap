# 👻 Ghost Tap

**Talk with a single tap.** Ghost Tap brings the telegraph back from the dead as a
communication aid for people who can make only one small movement: a key press, an
accessibility switch, a sip-and-puff, or an eye blink seen by the webcam.

> Built for **Kiroween 2026**, Resurrection category, using [Kiro](https://kiro.dev).
> Ghost Tap is a communication aid, not a medical device.

## The problem
People living with ALS, cerebral palsy, spinal cord injury or locked-in syndrome often
keep only one reliable movement. Dedicated communication devices can cost thousands.
Ghost Tap runs free in any modern browser.

## Features
- **One input is enough:** keyboard, accessibility switch, two-switch mode, or webcam blink.
- **Learns your rhythm:** Morse timing adapts to each user's speed, including slow or uneven tapping.
- **Phrase prediction:** common needs ("I'm thirsty", "Please call…") ranked by your history.
- **Speaks for you:** text-to-speech, plus a quick "send to caregiver" action.
- **Spirit telegraph interface:** every tap glows as a ghostly signal, so you always see what was registered. High-contrast and reduced-motion modes included.
- **Private:** camera frames and text never leave your device.

## Try it
- Live app: _link coming soon_
- Demo video: _link coming soon_

## Run locally
```bash
npm install
npm run dev
```
Tests: `npm test` (unit + property-based) and `npm run test:e2e` (Playwright + accessibility).

## How Kiro was used
See [docs/KIRO_USAGE.md](docs/KIRO_USAGE.md). Specs, steering docs and hooks live in [`.kiro/`](.kiro).

## License
[MIT](LICENSE)
