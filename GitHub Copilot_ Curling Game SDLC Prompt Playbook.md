# Build a Curling Game with GitHub Copilot: SDLC Prompt Playbook

**Workshop outcome:** A playable, tested browser-based curling game running locally.

**Starting state:** This repository contains the workshop instructions, not an implemented curling game or an npm project. Stages 1-3 produce planning documents. Application scaffolding begins in **Stage 4**, when Copilot creates `package.json`, project files, and npm scripts; gameplay follows in Stages 5-8. Do not run npm commands before scaffolding.

**How to use:** Open this repository folder in VS Code, then open GitHub Copilot Chat. See the [README Getting started section](README.md#getting-started) for setup steps and prerequisites. Start at Stage 1 and copy and paste **one prompt at a time** into Copilot Chat, following all 14 stages in order. Use **Plan mode** for planning stages when available and **Agent mode** for file creation, code changes, and running commands. Stages 10-11 use **Copilot Code Review or Ask mode** for review before any optional, human-approved implementation. Review each result before proceeding. If your IDE has different modes, use the equivalent planning, read-only review, and editing capabilities.

**Original customer requirements:** HTML5 canvas, score tracking, sound effects, mobile support, and unit tests.

**Workshop defaults (target application, not preinstalled tooling):** Vanilla JavaScript (ES modules), HTML, CSS, Vite, Vitest, no backend, no cloud dependency. Copilot will configure Vite and Vitest in Stage 4 and implement the game incrementally afterward. Use simple two-player local play, simplified physics, two teams, four stones per team per end, three ends per game. Scoring: only the team with the closest stone inside the house scores, one point for each of its stones closer to the button than the opponent's closest stone, subject to being inside the house. These are *demo rules*, not a full simulation of official curling rules.

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

This is the first application setup stage. The prompt below creates the files and scripts needed for npm commands. Its minimal landing page is not yet a playable game.

**Paste into Copilot:**

> Implement only the project scaffolding approved in `docs/02-architecture.md` and `docs/03-backlog.md`. Create a Vite vanilla JavaScript project in the current repository, with `package.json`, `index.html`, `src/` modules, `public/` assets if needed, `tests/`, `.gitignore`, `README.md`, and npm scripts named `dev`, `build`, `preview`, `test`, `test:watch`, and `test:coverage`. Configure Vitest and coverage tooling. Keep the landing page minimal. Install dependencies, run the initial tests and production build, and show the exact commands and outputs. Do not build gameplay yet. Preserve the existing docs, README workshop starting instructions and playbook link, and this prompt file.

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

> Improve the existing game for workshop-quality usability, targeting WCAG 2.2 Level AA where applicable. Add short sound effects for release, collision, and scoring using Web Audio API or locally stored assets, with a persistent-in-session mute toggle. Handle browser audio autoplay restrictions gracefully. Add touch/pointer controls for aiming and power, prevent accidental page scrolling over the active game surface where appropriate, and make layout responsive for mobile, tablet, and desktop. Preserve the approved gameplay rules and architecture; choose accessible interaction techniques appropriate to the existing game.
>
> Implement these accessibility requirements, extending existing controls and status feedback rather than duplicating them:
> - Keyboard: players can navigate and operate essential controls, including aim, power, release, mute, and restart/new game, without a mouse. Provide clear control instructions, accessible labels, logical focus order, no keyboard traps, and predictable focus after restart. Keep keyboard focus visibly indicated; focused controls must not be entirely obscured by author-created content such as overlays or sticky panels.
> - Game information: expose the current turn/team, scores, selected power, and relevant state (such as stones moving, ready to throw, end changes, and game over) as readable text available to assistive technologies. Provide text alternatives for important canvas information needed to understand play, including relevant stone positions/results; a canvas label alone is insufficient. Do not rely exclusively on canvas graphics, team color, sound, or animation for essential information. Keep readable contrast and non-color cues. Announce meaningful status changes through an appropriate live region or equivalent accessible status mechanism without moving focus or flooding users with per-frame announcements.
> - Pointer: if aiming or power selection uses dragging, also provide a single-pointer way to perform the same action without dragging (for example, click/tap selection or adjustment controls). Keyboard support alone is not this pointer alternative. Interactive pointer targets must be at least 24 by 24 CSS pixels or meet an applicable WCAG 2.2 SC 2.5.8 exception; document and verify any exception used, including the spacing rule where relevant.
> - Motion: respect reduced-motion preferences for nonessential effects where applicable, while preserving gameplay and access to essential information without animation alone.
>
> Add tests for testable input mappings and mute-state logic. Run tests and build; identify which UX/accessibility checks still require manual verification. Carry these expectations into the existing requirement IDs and test plan, adding IDs only for requirements not already represented.

**Check:** Complete aim/power/release and restart with keyboard only and with a pointer without dragging; verify visible, non-obscured focus, readable game state and meaningful announcements, target sizes or justified exceptions, responsive layout, contrast, and reduced-motion behavior. Muting must not break gameplay. Record manual checks not performed as unverified.

## Stage 9. Test quality and coverage verification

**Copilot mode:** Agent

**Learning objective:** Review existing tests against approved requirements, identify missing or weak coverage, add targeted tests only where necessary, and evaluate the quality of Copilot-generated assertions.

Stages 5-8 already add tests alongside implementation: aim/power and motion, collisions and turns, scoring and the game loop, and input/mute logic. This stage evaluates that evidence rather than generating those suites again.

**Paste into Copilot:**

> Act as a QA engineer reviewing test quality and coverage, not generating a new test suite. Read `docs/01-requirements.md` (including approved updates from Stage 8), `docs/02-architecture.md`, `docs/03-backlog.md`, the current implementation, existing tests, and configured test scripts. Reuse the existing Vitest framework and coverage tooling from Stage 4; do not add frameworks or dependencies.
>
> Create or update `docs/04-test-plan.md` with a concise requirements-to-test evidence table: requirement ID and acceptance criterion, relevant existing test file/name and behavior asserted, coverage assessment (adequate, partial/weak, or missing), appropriate manual/integration checks, and execution evidence/status (passed, failed, or not run). Map tests to multiple requirements where appropriate; a requirement may need multiple checks, and not every requirement needs a separate test. Mark requirements without executed evidence as unverified, even if a test exists. Distinguish expected behavior derived from approved requirements from implemented behavior observed in code or execution. Flag ambiguities or mismatches rather than treating current implementation as the specification or inventing game rules.
>
> Review existing assertions for meaningful gaps and prioritize the smallest useful set of improvements. Use the actual requirements and implementation to decide whether scoring, turn transitions, valid/invalid actions, game-state changes, restart behavior, or relevant edge cases need additional coverage; these are examples, not a mandatory test-generation checklist. Add tests only for genuine gaps, or strengthen weak assertions without discarding existing checks. If existing coverage is adequate, report that and add no tests. Preserve passing tests rather than rewriting them for style, do not duplicate coverage, and do not weaken assertions to make tests pass. Do not modify application logic; report suspected defects and request separate approval for any application fix.
>
> For each proposed new or strengthened test, identify the requirement/acceptance criterion, concrete expected values or state transitions derived from it, and the incorrect behavior the test should detect. Assert meaningful outcomes, not merely that a result exists or is truthy. Do not calculate expected values by calling or copying the implementation under test. Explain how each test would fail for a plausible incorrect result where practical. Show these assertions and their rationale for participant review before editing tests; stop for approval. If an expectation is ambiguous, ask for clarification instead of encoding a guessed rule.
>
> After approval, apply only the targeted test changes. Run the relevant focused tests, then the full existing suite and configured coverage command in non-watch mode (for example, `npm test -- --run` and `npm run test:coverage -- --run`, after checking the actual scripts). Record exact commands and observed results, including passed/failed/skipped counts and coverage where available. Treat coverage metrics as supporting evidence, not proof that requirements or assertions are correct; do not chase a percentage by adding redundant tests. Report failures, blocked commands, and checks not run honestly; do not claim tests passed without execution or browser/mobile/manual checks occurred unless performed. Update the evidence table with final results, tests added or strengthened and why, and remaining unverified requirements or acceptance criteria.

**Participant review:** Before approving test edits, inspect Copilot's proposed assertions. Explain where the expected values come from in the approved requirements, which observable behavior they verify, and one plausible incorrect outcome they would reject. Reject implementation-derived expectations, existence-only checks, and duplicate cases.

**Verification checkpoint:** Use `docs/04-test-plan.md` and actual output to explain:

- Which requirements and acceptance criteria have adequate test evidence, and which remain partial, weak, or unverified (including manual checks not performed).
- Which tests were added or strengthened, why they fill meaningful gaps, and how their assertions detect incorrect behavior; adding none is valid when no meaningful gap exists.
- Which exact commands were executed and their actual results, including failures, skipped tests, unavailable coverage, and commands not run. Do not label failed or unexecuted checks as passed.
- That existing tests and application logic were preserved, apart from approved assertion improvements, and no unnecessary testing dependencies were introduced.

## Stage 10. Debugging and code review

**Copilot mode:** Copilot Code Review (preferred where available); Ask for chat-based review and evaluation; Agent only for optional approved remediation.

### 1. Review the current implementation

Use **GitHub Copilot Code Review** in VS Code where available:

1. Save your files and open **Source Control** from the Activity Bar. Inspect the diffs to understand the current changes.
2. Hover over **CHANGES** and select **Copilot Code Review - Uncommitted Changes**. Review comments appear inline and in the **Problems** panel.
3. If all work is already committed, select relevant implementation code in the editor, right-click, and choose **Review** where available. Selection reviews appear inline and in **Comments**. Record that this is a limited scope, not a whole-application review.
4. Read the comments without applying suggestions. Do not select **Apply and Go To Next** or request a fix yet.

Availability and labels can vary by VS Code version, account, and organization policy. See [GitHub's VS Code code review instructions](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/use-code-review?tool=vscode). If the feature is unavailable, use the chat prompt below to review the implementation instead. No pull request or remote repository is required.

### 2. Generate evidence-backed findings without edits

Use the following review criteria for either method. For dedicated review comments, use this prompt in Ask mode to evaluate the comments and fill evidence gaps; attach the comments and affected code as context. Otherwise, use it as the standalone review prompt.

**Paste into Copilot (Ask):**

> Act as a senior reviewer and debugging partner. Review the current curling-game implementation against `docs/01-requirements.md`, `docs/02-architecture.md`, and `docs/04-test-plan.md`. If I supply Copilot Code Review comments, evaluate those first and state the scope you actually inspected. Focus on correctness, unintended behavior, potential defects, error handling, requirements compliance, and relevant regression risks. Examine scoring, deterministic physics, animation timing, input edge cases, resizing, restart state leaks, coupling, and duplication where they affect behavior. Identify browser console checks that require runtime verification.
>
> For each actionable finding provide an ID, severity, actual source file and line/function, supporting code or test evidence, expected versus actual behavior, triggering conditions, realistic impact, related requirement ID(s), and a minimal recommended correction. Separate source-based reasoning from observed runtime results; give reproduction or verification steps and mark unperformed checks as unverified. Distinguish confirmed defects from potential concerns and explain uncertainty. Do not invent findings or test outcomes; if none are supported, say so. Return the findings in chat for `docs/05-review-findings.md`. Do not modify files, apply fixes, or rewrite code. Stop for human evaluation.

### 3. Evaluate one finding

Select one finding, open its referenced source location, and read the surrounding code and relevant requirement/test. Explain the issue in your own words. Examine the evidence and triggering conditions; reproduce it or run an existing focused test where practical. Decide whether the issue is genuine, rather than accepting the AI's severity or suggested fix at face value.

### 4. Make an explicit decision

Record a human classification and a separate action, with rationale:

- **Confirmed:** Evidence establishes the issue in this implementation.
- **Potential concern:** Plausible, but evidence or runtime verification is missing.
- **Not applicable:** The assumptions do not hold; explain the counterevidence.

Choose **Accept** (approve the proposed correction), **Modify** (approve a revised correction with explicit scope), **Reject** (no correction), or **Investigate** (collect more evidence before approval). Accepting a finding does not automatically apply a suggestion.

Save the findings and your decision in `docs/05-review-findings.md`, retaining requirement IDs, evidence, severity, proposed correction, approval scope, and verification status. Unselected findings may remain unevaluated; do not imply they are approved. If no finding is supported, record that result and the review scope without manufacturing a defect.

### 5. Optional: implement one approved correction

To preserve workshop timing, stop after evaluation if needed. Only after explicit human approval, switch to Agent mode and replace the placeholders below.

**Paste into Copilot (Agent, optional):**

> I approve only finding [ID] in `docs/05-review-findings.md`, with this correction scope: [approved correction]. Implement that one targeted correction, preserving the curling demo rules, requirement IDs, architecture, and existing behavior outside this scope. Add a focused regression test where appropriate, run relevant tests and the production build, and inspect the resulting diff against the approved scope. Report exact commands and observed results, update the finding's fix and verification status, and leave anything not run marked unverified. Do not address other findings, add unnecessary dependencies, or perform broad rewrites. Stop if the correction requires a wider scope and request approval.

**Check:** Review precedes implementation; findings have evidence; one finding has a recorded human classification and action (or no supported findings is documented). Any optional fix is explicitly approved and verified, preferably with a focused regression test.

## Stage 11. Security, dependencies, and accessibility audit

**Copilot mode:** Ask for reviews and evaluation; Agent only for optional approved remediation.

### 1. Security and reliability review

**Paste into Copilot (Ask):**

> Review the generated curling game for relevant security and reliability concerns. Read `docs/01-requirements.md`, `docs/02-architecture.md`, `docs/04-test-plan.md`, actual source files, and dependency manifests/lockfiles. Respect the local-only browser game context: vanilla JavaScript, HTML5 canvas, Vite/Vitest, no backend or cloud dependency. Examine unsafe DOM insertion, input validation, exposed secrets (report locations, not secret values), remote assets, unnecessary dependencies, package vulnerabilities, and error handling that could break gameplay.
>
> For each supported finding provide an ID, severity, actual source file and line/function (or manifest/lockfile entry), evidence, triggering conditions or exploit prerequisites, realistic impact, related requirement ID(s), and minimal remediation. Distinguish confirmed findings from potential concerns; an audit advisory alone does not establish exploitability in this game. Identify a suitable read-only package-manager audit command for me to run, then interpret its actual output if supplied. Do not install packages, run automatic audit fixes, or change dependency files. State review limits and checks not performed. Return a security section in chat for `docs/06-quality-audit.md`; say if no findings are supported. Do not modify any files or automatically implement recommendations. Stop for human evaluation.

If dependency audit evidence is needed, run the suggested read-only command (for example, `npm audit`) in the generated project and supply its output. Record command failures or unavailable network access as verification gaps, not a clean audit.

### 2. Accessibility review

**Paste into Copilot (Ask):**

> Review the generated curling game's accessibility against its approved requirements, the Stage 8 expectations, and applicable WCAG 2.2 Level A and AA criteria. Read the actual implementation files for rendering, input, UI, styles, and audio, plus relevant tests; state the files and scope inspected. Examine keyboard-only aiming/power/release, mute, restart/new game and navigation; keyboard traps; focus visibility/order, obscuration by overlays/panels, and restart behavior; accessible control labels; readable text for turn, score, selected power and relevant game state; text alternatives for important canvas information such as stone positions/results; meaningful status announcements without focus changes or per-frame noise; contrast and non-color cues; pointer target sizes/exceptions; a single-pointer non-drag alternative for any dragging interaction; responsive layout; and reduced-motion behavior. Do not treat keyboard support as evidence of a non-drag pointer alternative.
>
> For each finding give an ID, severity/impact on players, actual source file and line/function, supporting evidence, related requirement ID(s), applicable WCAG success criterion number, name and level, and a minimal recommended correction. Consider Level A criteria 1.1.1 Non-text Content, 1.4.1 Use of Color, 2.1.1 Keyboard, 2.1.2 No Keyboard Trap, 2.4.3 Focus Order, and 4.1.2 Name, Role, Value; and Level AA criteria 1.4.3 Contrast (Minimum), 1.4.11 Non-text Contrast, 2.4.7 Focus Visible, 2.4.11 Focus Not Obscured (Minimum), 2.5.7 Dragging Movements, 2.5.8 Target Size (Minimum), and 4.1.3 Status Messages only where applicable. Explain applicability, exceptions, and uncertainty rather than assuming a game or canvas is exempt. For target size, check 24 by 24 CSS pixels or substantiate an applicable exception, not a blanket 44-pixel AA requirement. Keep reduced-motion preference support as a workshop expectation; do not mislabel 2.3.3 Animation from Interactions (Level AAA) as an AA requirement.
>
> Distinguish confirmed issues supported by source or observed runtime evidence from potential concerns needing verification. Separate code evidence from browser observations; never claim keyboard, screen-reader, contrast, touch, or mobile tests were performed unless observed. Provide a focused manual checklist with steps and expected results for keyboard-only gameplay and focus after restart; visible focus and controls not entirely hidden by author-created content at relevant viewport sizes; screen-reader access to text game state, canvas alternatives and meaningful announcements; pointer-only aiming/power without dragging; rendered target measurements or verified exceptions; contrast, non-color cues and mobile layout; and reduced-motion settings with essential information still available. State which checks require a browser, assistive technology or human judgment, and mark unperformed checks unverified. Source inspection and automated tests cannot establish the usability of these interactions or complete accessibility conformance.
>
> Return an accessibility section in chat for `docs/06-quality-audit.md`, including scope, evidence, confirmed issues, potential concerns, and manual verification gaps. Do not modify files, add tooling/dependencies, or implement fixes. Do not claim full WCAG compliance or complete accessibility conformance from this workshop review, even if no issues are found. Stop for human evaluation.

Use the [WCAG 2.2 Quick Reference](https://www.w3.org/WAI/WCAG22/quickref/) to check criterion applicability; a source review is not an accessibility conformance audit.

### 3. Evaluate findings before deciding

Select **one finding across the two reviews**, not every reported issue. Locate the referenced code, review its evidence and relevant requirement, and check whether its assumptions apply to this local game. Perform the relevant manual check if feasible, or retain the uncertainty.

Use the Stage 10 classifications (**Confirmed**, **Potential concern**, **Not applicable**) and actions (**Accept**, **Modify**, **Reject**, **Investigate**). Record your rationale, whether remediation is necessary, and the exact approved scope, if any. Save both review sections and the decision in `docs/06-quality-audit.md`, including evidence, severity, requirement/WCAG references, minimal remediation, and manual/verification status. Leave unselected findings unevaluated and unresolved checks explicit. If neither review supports a finding, document the scope and limitations instead of inventing one.

### 4. Optional: implement one approved correction

Only if time permits and a human explicitly approves a correction, switch to Agent mode.

**Paste into Copilot (Agent, optional):**

> I approve only finding [ID] in `docs/06-quality-audit.md`, with this correction scope: [approved correction]. Implement one minimal correction without broad rewrites, unnecessary dependencies, or changes to unrelated behavior. Preserve the local curling game constraints and requirement traceability. Add a focused regression test where appropriate, run relevant tests and the production build, and verify the affected interaction using the review's manual steps where feasible. Report exact commands and actual results; mark any unperformed manual checks unverified. Update only this finding's remediation and verification status. Do not fix every reported issue. Stop and request approval if a wider scope is needed.

**Check:** Both reviews precede any code changes; findings cite evidence and distinguish confirmed issues from potential concerns. One finding has a human decision (or no supported findings is documented). Remediation is optional, scoped, and approved; there is no unsupported claim that the game is fully secure or accessible.

## Stage 12. Documentation and onboarding

**Copilot mode:** Agent

**Paste into Copilot:**

> Act as a technical writer. Update `README.md` for someone receiving this repository in a customer workshop. Preserve the workshop starting instructions and playbook link, and distinguish them from instructions for running the now-generated application. Include purpose, feature list, simplified game rules, prerequisites, setup, commands to develop/test/build/preview locally, mouse/keyboard/touch controls, screenshots placeholders only if screenshots are not available, architecture overview, test strategy, accessibility notes, known limitations, and troubleshooting. Add a short `CONTRIBUTING.md` with branching, test, and pull-request expectations. Verify every documented npm command against `package.json` and correct inconsistencies.

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
