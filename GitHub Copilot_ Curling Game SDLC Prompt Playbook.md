# Build a Curling Game with GitHub Copilot: SDLC Prompt Playbook

**Workshop outcome:** A playable, tested browser-based curling game running locally.

**How to use:** Open an empty folder in VS Code with GitHub Copilot Chat. Save this playbook in the repository. Copy and paste **one numbered prompt at a time** into Copilot Chat. Use **Plan mode** for planning stages when available and **Agent mode** for file creation, code changes, and running commands. Review each result before proceeding. If your IDE has different modes, use the equivalent planning and editing capabilities.

**Original customer requirements:** HTML5 canvas, score tracking, sound effects, mobile support, and unit tests.

**Workshop defaults:** Vanilla JavaScript (ES modules), HTML, CSS, Vite, Vitest, no backend, no cloud dependency. Use simple two-player local play, simplified physics, two teams, four stones per team per end, three ends per game. Scoring: only the team with the closest stone inside the house scores, one point for each of its stones closer to the button than the opponent's closest stone, subject to being inside the house. These are *demo rules*, not a full simulation of official curling rules.

**Important:** Do not paste every prompt at once. Each stage consumes the files and decisions produced by the previous stage. Ask Copilot to show evidence of commands run, not just say they passed. Approve destructive changes before execution.

---

## Stage 1. Requirements and user stories

**Copilot mode:** Plan

**Paste into Copilot:**

> We are building a browser-based curling game as a workshop project. Requirements: HTML5 canvas, score tracking, sound effects, mobile support, and unit tests. Use a simple local two-player game, two teams, four stones per team per end, three ends, simplified friction/collision physics, and a visible house and button. Support mouse, touch, and keyboard controls. No backend or cloud dependencies.
>
> Act as a product owner and business analyst. Create `docs/01-requirements.md` with the product goal, MVP boundaries, assumptions, functional and nonfunctional requirements, accessibility requirements, user stories, Given/When/Then acceptance criteria, and a prioritized MVP backlog. Assign stable requirement IDs such as REQ-01. Flag ambiguous game rules and propose simple workshop-friendly defaults. Do not write application code. Summarize decisions and ask me to approve the requirements before continuing.

**Check:** Every original requirement has an ID and testable acceptance criteria.

## Stage 2. Architecture and technical design

**Copilot mode:** Plan

**Paste into Copilot:**

> Read `docs/01-requirements.md`. Act as a solution architect. Design a maintainable but lightweight browser game using vanilla JavaScript ES modules, HTML5 canvas, CSS, Vite, and Vitest. Separate pure game rules, scoring, physics, and state transitions from rendering, input, audio, and UI. Define the coordinate system, animation loop, fixed-time-step or delta-time strategy, collision model, scoring algorithm, touch/mouse/keyboard controls, responsive canvas scaling, and accessible game status. Create `docs/02-architecture.md` with a module diagram in Mermaid, proposed file tree, data structures, key functions/interfaces, design tradeoffs, and technical risks. Do not implement yet. Explicitly map each requirement ID to the proposed module.

**Check:** Scoring and physics can be tested without the browser.

## Stage 3. Sprint planning and task breakdown

**Copilot mode:** Plan

**Paste into Copilot:**

> Read `docs/01-requirements.md` and `docs/02-architecture.md`. Act as a scrum team. Create `docs/03-backlog.md` with a sequenced implementation backlog broken into small tasks. For each task include an ID, user-story/requirement link, dependency, acceptance criteria, test expectation, and definition of done. Organize work into playable increments: canvas and rink, aiming/release, motion/collisions, turns/scoring, sound, responsive controls, and polish. Mark the critical path to a locally deployable MVP. Do not write code. Identify the first smallest vertical slice.

**Check:** Each task has an observable outcome and a verification method.

## Stage 4. Repository and project scaffolding

**Copilot mode:** Agent

**Paste into Copilot:**

> Implement only the project scaffolding approved in `docs/02-architecture.md` and `docs/03-backlog.md`. Create a Vite vanilla JavaScript project in the current repository, with `index.html`, `src/` modules, `public/` assets if needed, `tests/`, `.gitignore`, `README.md`, and npm scripts named `dev`, `build`, `preview`, `test`, `test:watch`, and `test:coverage`. Configure Vitest and coverage tooling. Keep the landing page minimal. Install dependencies, run the initial tests and production build, and show the exact commands and outputs. Do not build gameplay yet. Preserve the existing docs and this prompt file.

**Check:** `npm install`, `npm run dev`, `npm test -- --run` (or the configured equivalent), and `npm run build` work. Record the actual local URL printed by Vite.

## Stage 5. First playable slice: rink and aiming

**Copilot mode:** Agent

**Paste into Copilot:**

> Read the approved requirements, architecture, and backlog. Implement the first playable vertical slice: render a curling rink and house on HTML5 canvas; display one stone; let a user aim and choose release power with mouse and keyboard; release the stone and animate it moving and slowing to a stop. Keep physics as pure testable functions, separate from canvas drawing. Scale the canvas correctly for different viewport sizes and device pixel ratios. Add clear instructions and a text status area. Add focused unit tests for aim/power validation and motion/friction. Run tests and build. Stop after this slice and report changed files and any limitations.

**Check:** A stone can be launched and stops predictably.

## Stage 6. Collision physics and game state

**Copilot mode:** Agent

**Paste into Copilot:**

> Extend the existing playable slice without rewriting working modules. Implement deterministic, simplified stone-to-stone collision behavior, boundaries, turn state, team colors, and alternating throws. Use two teams with four stones each per end. Prevent throwing while stones are moving. Maintain an explicit game-state model that can be reset. Write unit tests for collision cases, stopping thresholds, out-of-bounds behavior, turn transitions, and invalid actions. Run tests and build, then explain the chosen physics simplifications.

**Check:** Stones interact, turns alternate, and no new throw begins during motion.

## Stage 7. Scoring and complete game loop

**Copilot mode:** Agent

**Paste into Copilot:**

> Implement score tracking and the complete three-end game loop according to `docs/01-requirements.md`. After both teams have thrown four stones, determine which team has the closest stone to the button inside the house; award one point for each of that team's stones inside the house that is closer than the opponent's closest eligible stone. If no stones qualify, score zero. Handle ties with a documented deterministic rule suitable for the demo. Display end number, active team, stones remaining, end score, and total scores. Add new-game and restart controls. Write table-driven unit tests for empty house, one scoring stone, multiple scoring stones, opponent closer, equal distances, end transition, and game over. Run tests and build.

**Check:** A full three-end game finishes and produces consistent scores.

## Stage 8. Sound, mobile, and accessibility

**Copilot mode:** Agent

**Paste into Copilot:**

> Improve the existing game for workshop-quality usability. Add short sound effects for release, collision, and scoring using Web Audio API or locally stored assets, with a persistent-in-session mute toggle. Handle browser audio autoplay restrictions gracefully. Add touch/pointer controls for aiming and power, prevent accidental page scrolling over the active game surface where appropriate, and preserve keyboard controls. Make layout responsive for mobile, tablet, and desktop. Ensure labeled controls, visible focus, readable contrast, a text status/live region for scores and turns, and reduced-motion considerations. Add tests for testable input mappings and mute-state logic. Run tests and build; identify which UX checks still require manual verification.

**Check:** Play with touch and keyboard; muting does not break gameplay.

## Stage 9. Test strategy and automated test suite

**Copilot mode:** Agent

**Paste into Copilot:**

> Act as a QA engineer. Read the requirement IDs and current code/tests. Create `docs/04-test-plan.md` mapping each requirement to unit tests, integration-level checks, and manual browser checks. Identify missing cases, then add automated Vitest tests for pure scoring, game state, physics, collisions, boundaries, and controls. Include normal, edge, and invalid cases. Run the entire test suite and coverage report. Fix actual failures without weakening assertions merely to make tests pass. Report passed/failed counts, coverage where available, remaining gaps, and commands run. Do not claim browser or mobile testing occurred unless actually performed.

**Check:** Critical rules have meaningful assertions and all automated tests pass.

## Stage 10. Debugging and code review

**Copilot mode:** Agent

**Paste into Copilot:**

> Act as a senior reviewer and debugging partner. Review the entire curling-game implementation against `docs/01-requirements.md` and `docs/02-architecture.md`. Look for incorrect scoring, non-deterministic physics, animation timing problems, input edge cases, resize bugs, state leaks on restart, excessive coupling, duplicate code, and browser console errors. Reproduce each issue where possible, prioritize findings, fix high-severity defects in small changes, and add regression tests. Run tests and build again. Create `docs/05-review-findings.md` with issue, severity, evidence, fix, and verification status. Do not invent test outcomes.

**Check:** Each fixed defect has evidence and preferably a regression test.

## Stage 11. Security, dependencies, and accessibility audit

**Copilot mode:** Agent

**Paste into Copilot:**

> Audit this local browser game for common web risks and quality issues: unsafe DOM insertion, input handling, exposed secrets, remote assets, unnecessary dependencies, and package vulnerabilities. Run the package manager's available audit command and distinguish reported findings from confirmed exploitable issues. Also review keyboard navigation, focus states, screen-reader status text, color contrast, touch targets, and mobile layout. Fix actionable high-priority issues without adding unnecessary packages. Create `docs/06-quality-audit.md` with findings, severity, remediation, and items requiring manual testing. Rerun tests and build.

**Check:** Findings are documented, with no unsupported claim that the app is fully secure or accessible.

## Stage 12. Documentation and onboarding

**Copilot mode:** Agent

**Paste into Copilot:**

> Act as a technical writer. Update `README.md` for someone receiving this repository in a customer workshop. Include purpose, feature list, simplified game rules, prerequisites, setup, commands to develop/test/build/preview locally, mouse/keyboard/touch controls, screenshots placeholders only if screenshots are not available, architecture overview, test strategy, accessibility notes, known limitations, and troubleshooting. Add a short `CONTRIBUTING.md` with branching, test, and pull-request expectations. Verify every documented npm command against `package.json` and correct inconsistencies.

**Check:** Another participant can follow the README without asking for missing commands.

## Stage 13. Production build and local deployment

**Copilot mode:** Agent

**Paste into Copilot:**

> Prepare the curling game for local deployment only. Run all unit tests, run `npm run build`, and launch the production build with `npm run preview` using the project's configured host/port. Report the exact URL from the server output. If a browser automation tool is available, smoke-test the deployed build; otherwise provide manual steps and clearly mark them unverified. Validate starting a game, throwing a stone, collisions, score updates, mute, restart, keyboard controls, and responsive/mobile emulation. Create `docs/07-local-deployment.md` with exact commands, expected results, troubleshooting, and a checked/unchecked deployment checklist based only on actual verification. Do not deploy to a cloud provider.

**Check:** The production build is served locally and verified to the extent tooling permits.

## Stage 14. Final demo and requirements traceability

**Copilot mode:** Agent or Ask

**Paste into Copilot:**

> Act as a workshop facilitator. Read the original requirements and all project docs. Create `docs/08-demo-and-traceability.md` containing: (1) a concise live demo script showing gameplay, score tracking, sound, mobile controls, tests, and local deployment; (2) a requirements traceability matrix with requirement ID, implementation file(s), test(s), and status (Complete/Partial/Not done); (3) exact demo commands; (4) a short explanation of how GitHub Copilot supported each SDLC phase; (5) known limitations and next-iteration backlog. Use only verified results and do not mark requirements complete without evidence. Do not modify gameplay code in this phase.

**Check:** The facilitator can demonstrate the complete SDLC and a working local game.

---

## Facilitator quick runbook

1. **Start:** Open the folder in VS Code and keep this Markdown file visible.
2. **Plan:** Paste Stages 1–3 in Plan mode, review the generated docs, and approve.
3. **Build:** Paste Stages 4–8 in Agent mode, pausing to run the game after each playable increment.
4. **Validate:** Paste Stages 9–11, inspect test output, review and correct findings.
5. **Ship locally:** Paste Stages 12–14, then demo the production preview and traceability matrix.
6. **Show Git workflow (optional):** Commit after each approved increment; open a pull request if a remote repository is available, but no remote is required for this workshop.

### Standard local commands (after scaffolding)

```bash
npm install
npm run dev
npm run test
npm run test:coverage
npm run build
npm run preview
```

Use the actual scripts in `package.json` if they differ. The development and preview URLs are printed by the running server.

### Final definition of done

- [ ] HTML5 canvas rink and stones are playable
- [ ] Aiming, power, movement, and collisions work
- [ ] Turns, ends, and score tracking work
- [ ] Sound effects and mute work
- [ ] Mouse, keyboard, and mobile/touch controls work
- [ ] Unit tests run and pass
- [ ] Responsive and accessibility checks are documented
- [ ] Production build succeeds and is served locally
- [ ] README explains how to run and test
- [ ] Requirement IDs map to code and verification evidence
