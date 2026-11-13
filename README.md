# Curling Game SDLC Lab

This repository is a hands-on lab for exploring the software development lifecycle (SDLC) from end to end by creating a browser-based curling game. Participants use the included [GitHub Copilot Curling Game SDLC Prompt Playbook](<GitHub Copilot_ Curling Game SDLC Prompt Playbook.md>) to guide the work through planning, implementation, testing, review, and a final demo.

## What you’ll explore

The lab walks through the major stages of building a small software product:

1. Define requirements and user stories.
2. Design the architecture and break the work into a backlog.
3. Scaffold the project and build the game incrementally.
4. Add game rules, scoring, sound, mobile support, and accessibility considerations.
5. Create and run tests, debug issues, and review the implementation.
6. Audit dependencies and security, document the project, build and preview it locally, and prepare a final demo.

The example game is a simplified, local two-player curling game. The playbook’s workshop defaults use vanilla JavaScript, HTML, CSS, Vite, and Vitest, with no backend or cloud dependency.

## Getting started

1. Open this repository in VS Code with GitHub Copilot Chat available.
2. Open the prompt playbook linked above.
3. Follow its stages in order, copying and pasting one prompt at a time into Copilot Chat. Review each stage’s output before moving on; later stages build on earlier decisions and files.
4. Create and run the game locally as directed by the playbook. Once the project is scaffolded, the usual commands are:

   ```bash
   npm install
   npm run dev
   npm run test
   npm run build
   ```

   Use the scripts in `package.json` if they differ. The development server prints the local URL to open in your browser.

## Learning approach

This is a guided lab, not just a finished-game download: the goal is to experience how requirements, design, implementation, verification, and documentation connect across the SDLC. The playbook includes checks for each stage and a final definition of done to help participants verify their work.
