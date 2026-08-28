# Agent team

The Mona's Project Pulse dashboard team is orchestrated through GitHub Copilot CLI in a Codespace:

- **Orchestrator** - Uses **Claude Opus 4.7 (copilot)** to coordinate the specialist agents, split work into phases, manage file ownership and dependencies, run independent work in parallel when possible, and verify the integrated result. Definition: [.github/agents/orchestrator.agent.md](../.github/agents/orchestrator.agent.md)
- **Planner** - Uses **Claude Opus 4.7 (copilot)** to research the repository, documentation, dependencies, edge cases, risks, and validation needs, then produce an implementation plan for the Orchestrator. The Planner does not write code. Definition: [.github/agents/planner.agent.md](../.github/agents/planner.agent.md)
- **Designer** - Uses **Gemini 3.1 Pro (copilot)** to shape the dashboard's UI/UX, accessibility, information hierarchy, interaction flow, responsive behavior, and visual design. For Project Pulse, this includes polished project cards, status badges, priority treatment, responsive layout, and deterministic CSS hooks such as `.dashboard` and `.project-card`. Definition: [.github/agents/designer.agent.md](../.github/agents/designer.agent.md)
- **Coder** - Uses **GPT-5.5 (copilot)** to implement the assigned application code and supporting runnable-app configuration, with clear structure, deterministic behavior, explicit errors, and validation. For Project Pulse, the Coder can create `.vscode/launch.json` with the app working directory and open `index.html` for the dashboard preview when assigned. Definition: [.github/agents/coder.agent.md](../.github/agents/coder.agent.md)

The Orchestrator uses the Planner's research first, delegates design and implementation with explicit file scopes, sequences dependent work, and reports the final outcome. All agents leave Git staging, commits, and pushes to the learner.
