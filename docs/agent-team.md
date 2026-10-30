# Agent team

The custom agent team for Mona's Project Pulse dashboard is:

- **Orchestrator** (Claude Opus 5.5): Breaks work into tasks, delegates to specialist agents, coordinates dependencies and file ownership, and checks the integrated result. Definition: `.github/agents/orchestrator.agent.md`.
- **Planner** (Claude Opus 5.5): Researches the codebase and dependencies, identifies risks and edge cases, and produces an implementation plan with file assignments and validation expectations. Definition: `.github/agents/planner.agent.md`.
- **Coder** (GPT-5.5): Implements code and fixes bugs within the assigned scope, follows repository patterns, and validates changes. Definition: `.github/agents/coder.agent.md`.
- **Designer** (Gemini 3.7 Flash): Shapes the dashboard's user experience, accessibility, information hierarchy, interaction flow, visual design, and responsive behavior. Definition: `.github/agents/designer.agent.md`.

## How the team works together

1. The Orchestrator asks the Planner to research Project Pulse and produce an implementation plan, including file ownership, dependencies, risks, and validation expectations.
2. The Orchestrator turns the plan into scoped tasks for the Designer and Coder. They can work in parallel when their file scopes are independent; dependent or overlapping work happens sequentially.
3. The Designer defines and implements the assigned experience and visual direction, while the Coder implements the assigned application behavior and supporting code, following the agreed scope.
4. The Orchestrator integrates the results, checks that the dashboard works as a whole, and reports the outcome and any remaining risks.

I am using GitHub Copilot CLI in a Codespace to orchestrate the work.
