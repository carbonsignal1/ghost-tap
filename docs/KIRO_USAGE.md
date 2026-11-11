# How Kiro was used to build Ghost Tap

Fill this in as you go. Judges score "Technological Implementation" from this write-up,
so record real moments: what you asked, what Kiro did, what changed. Screenshots help.

## Kiro apps used
_Which of IDE, CLI, Web and Crew did you use, for what, and how did they differ?_

## Spec-driven development
_How the specs were structured (requirements in EARS format → design → tasks), and how it
compared with vibe coding._

- 2026-11-11: Started `morse-decoder` spec with 6 requirements, including 4 robustness properties.

## Steering docs
- `product.md`: user, principles ("never lose input"), non-goals.
- `tech.md`: stack, pure core logic with injected time, every invariant gets a property test.
- `structure.md`: folders and dependency direction.
- `accessibility.md`: loaded only for `src/ui/**`, enforces WCAG 2.2 AA and no flashing.

_What difference did they make to Kiro's output?_

## Agent hooks
- Run related tests on save (core modules)
- Accessibility review on UI change
- Keep README and this log in sync when specs change
- Manual pre-commit check

_Which hook saved the most time? Any surprises?_

## MCP
- Playwright MCP for driving the app and running accessibility checks.

_What did it make possible?_

## Property-based testing
_Which properties did you write, and what bugs did they catch that unit tests missed?
Include the shrunk counterexample if one surprised you._

## Custom agents and Kiro Crew
_Agents you created, how work was split, what went well or badly._

## Kiro powers
_Which powers you used and what they added._
