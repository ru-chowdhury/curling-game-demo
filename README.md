# Curling Game SDLC Lab

This repository is a prompt-driven, hands-on lab for exploring the software development lifecycle (SDLC) by creating a browser-based curling game with GitHub Copilot. The initial repository contains workshop instructions, not an implemented game. You will use Copilot to generate the application during the lab, moving through planning, implementation, testing, review, and final delivery.

Start with the [SDLC Prompt Playbook](GitHub%20Copilot_%20Curling%20Game%20SDLC%20Prompt%20Playbook.md). Stages 1-3 produce planning documents; application scaffolding begins in **Stage 4**, and gameplay is implemented in later stages.

## What this lab covers

The goal is to experience the full SDLC in a simple, practical example:

- Define user requirements and scope
- Design a lightweight technical architecture
- Break the work into backlog tasks
- Build the game incrementally in code
- Validate behavior with automated tests
- Debug, review, and improve the solution
- Document onboarding steps and prepare a demonstration

The workshop's target product is a simplified, local two-player browser game. Participants will use HTML5 canvas, JavaScript, and CSS, with Vite for development/builds and Vitest for testing. These application technologies are not configured in the initial repository: Copilot will introduce Vite and Vitest during Stage 4 scaffolding and implement gameplay in Stages 5-8.

## Lab instructions

The full set of step-by-step instructions for the lab can be found in the Markdown file:

- [SDLC Prompt Playbook](GitHub%20Copilot_%20Curling%20Game%20SDLC%20Prompt%20Playbook.md)

Follow the numbered stages in that file one at a time in GitHub Copilot Chat. Each stage builds on the previous one so the lab reflects a realistic SDLC workflow from requirements through delivery.

## Getting started

**Prerequisites:** VS Code with GitHub Copilot Chat available and signed in to an account with Copilot access. For Stage 4 onward, you will also need Node.js (a version supported by the generated Vite project) and npm.

1. In VS Code, choose **File > Open Folder** and select your local copy of this repository.
2. Open **GitHub Copilot Chat** using the Chat icon in VS Code. If needed, use the Command Palette to search for **Chat: Open Chat**.
3. Open the [SDLC Prompt Playbook](GitHub%20Copilot_%20Curling%20Game%20SDLC%20Prompt%20Playbook.md) from this link or the VS Code Explorer.
4. Begin at **Stage 1**. Copy one numbered prompt at a time into Copilot Chat, use Plan or Agent mode as directed, and review each result before continuing through all 14 stages in order.
5. At **Stage 4**, use the scaffolding prompt to have Copilot create the project files, including `package.json` and the npm scripts. There is no application to run before this step; do not run npm commands in the initial repository.
6. Once Stage 4 scaffolding is complete, open **Terminal > New Terminal** in the generated project folder (the repository root by default). If Copilot has not already installed dependencies, run `npm install`. Run `npm run dev`, then open the local URL printed by Vite. At this point, expect a minimal landing page, not a playable game; continue with Stage 5 to begin gameplay implementation.

### Application commands (after Stage 4 scaffolding)

These commands require the generated `package.json` and its scripts. Stage 4 configures the test tooling; later stages add gameplay tests. Use another terminal for tests/builds while the development server is running.

```bash
npm install
npm run dev
npm test -- --run
npm run build
```

`npm test -- --run` runs the configured Vitest suite once. For watch-mode tests, use `npm test`. If the generated scripts differ, use the commands listed in `package.json`. The playbook also lists coverage and production-preview commands for use after scaffolding.

## Learning outcome

By the end of the lab, users will have built and validated a working curling game while exploring how the SDLC connects requirements, design, coding, testing, and documentation into a complete software project.
