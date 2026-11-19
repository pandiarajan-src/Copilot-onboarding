# GitHub Copilot Onboarding Hub

Step-by-step guides and interactive simulators that teach professional developers **GitHub Copilot** in **VS Code** and the **Copilot CLI**.

It is a static site with no build step, published with GitHub Pages from the root of `main`.

## Pages

| # | Page | What it covers |
|---|------|----------------|
| – | `index.html` | Hub and recommended path |
| 1 | `Copilot_Intro.html` | What Copilot is, how it works, plans, models, benefits and limits |
| 2 | `Copilot_Feature_Tour.html` | Features in VS Code and the CLI, plus a cheat-sheet |
| 3 | `Copilot_Sim_Setup.html` | Install, sign in and verify on Windows, macOS and Linux |
| 4 | `Copilot_Sim_Customize.html` | Skills, custom agents, tools, hooks and MCP servers |
| 5 | `Copilot_Sim_Security.html` | Security, approvals, sandboxing and git worktrees |
| 6 | `Copilot_Sim_Greenfield.html` | New FastAPI service, from brief to PR |
| 7 | `Copilot_Sim_Brownfield.html` | Legacy Django codebase: understand, refactor, extend |
| 8 | `Copilot_Sim_Knowledge.html` | Instructions, prompt files, memory and the learning loop |
| 9 | `Copilot_VSCode_vs_CLI.html` | VS Code agents vs the Copilot CLI |
| 10 | `Copilot_FAQ.html` | Frequently asked questions |
| + | `Copilot_Training.html` | Training modules, labs and a knowledge check |
| + | `Copilot_Onboarding_Kit.html` | First-week checklist and prompt cheat-sheet |

## Run locally

```bash
python -m http.server 8000
# open http://localhost:8000
```

## Authoring a simulator page

Each step is a `<section class="step-panel" data-section="…" data-title="…" data-sub="…">`.
`assets/copilot-sim.js` builds the sidebar, progress bar, Back/Next buttons and `#step-N` deep links from these sections.
It also powers tabs (`data-tabs`), animated terminals (`.terminal.typer`) and step-through chats (`.chat.reveal`).
`assets/copilot-kit.js` adds quizzes (`.quiz`) and saved checklists (`.track`).

Structure and design are adapted from the [AIDLC Onboarding Hub](https://kaweween.github.io/AIDLC-onboarding/).
