# Ghost Tap: build plan (Nov 11 – Dec 4, 2026)

Deadline: **Friday Dec 4, 2:00 PM Pacific**. Aim to submit by **Dec 3** to leave buffer.

## Week 1 (Nov 11–17): core that works
- [ ] Request the 4,000 free Kiro credits now (Resources tab; deadline Dec 1, 12:00 PM PT)
- [ ] Create the public GitHub repo, push this scaffold (with `.kiro/`), confirm the MIT license shows in the About section
- [ ] In Kiro: open the `morse-decoder` spec and run its tasks (decoder + property tests)
- [ ] Ask Kiro to create the next specs: `input-adapters`, `phrase-prediction`, `speech-output`, `telegraph-ui`
- [ ] Post on social starting with `#KiroweenHackathon26` (Social Blitz bonus)

## Week 2 (Nov 18–24): make it useful
- [ ] Keyboard/switch adapter and two-switch mode
- [ ] Webcam blink adapter (MediaPipe Face Landmarker, blink = "press")
- [ ] Phrase bank and history-based ranking
- [ ] Speech output and "send to caregiver" (share sheet or copy link)
- [ ] Try Kiro Crew: parallel agents for input, prediction and UI (Best Kiro Crew App bonus)
- [ ] Reach out to a speech therapist or AAC user for 10 minutes of feedback

## Week 3 (Nov 25–Dec 3): polish and present
- [ ] "Spirit telegraph" interface, high-contrast and reduced-motion modes
- [ ] Playwright + axe accessibility tests passing
- [ ] Deploy (e.g. AWS Amplify, Netlify or GitHub Pages) and test on a second device
- [ ] Record the demo video (under 3 min), upload public to YouTube, no copyrighted music
- [ ] Finish `docs/KIRO_USAGE.md` and paste it into the submission
- [ ] Publish the blog post mentioning Kiroween 2026 (Bonus Blog Prize)

## Submission checklist
- [ ] Category: Resurrection (+ bonuses: Kiro Crew, Blog, Social; Student if eligible)
- [ ] Working app URL
- [ ] Public GitHub repo, open-source license visible, `.kiro/` at root and not ignored
- [ ] Text description of features
- [ ] YouTube demo link
- [ ] Kiro usage write-up
- [ ] Disclose any pre-existing code or templates used

## Demo video outline (2:45)
1. 0:00 Hook: someone who can't speak or type blinks, the telegraph flickers, the app says "I'm thirsty."
2. 0:20 The problem and who it is for (cost of communication devices, one reliable movement).
3. 0:45 Live walkthrough: tap input, adaptive timing, prediction, speech, blink mode.
4. 1:50 How Kiro built it: specs, property test catching a real bug, hooks, Crew.
5. 2:30 Impact and close.
