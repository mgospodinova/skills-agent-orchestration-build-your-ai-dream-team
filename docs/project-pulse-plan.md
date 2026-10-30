# Project Pulse Implementation Plan

## Summary

Build a lightweight static dashboard that helps contributors scan project names, owners, status, recent activity, priority or risk, and a short summary. Use `app/project-data.json` as the data source, `app/index.html` to render it, `app/styles.css` for the responsive accessible presentation, and `.vscode/launch.json` to run a local preview that opens the dashboard rather than a directory listing.

## Responsibilities

- **Orchestrator:** Assign the file scopes below, confirm the shared HTML/CSS and data contracts before parallel implementation, sequence integration, and report validation results.
- **Designer:** Define the dashboard hierarchy, project-card layout, status and priority treatment, accessibility, and responsive behavior. Own `app/styles.css`; coordinate the class and markup contract with Coder before implementation.
- **Coder:** Own `app/project-data.json`, `app/index.html`, and `.vscode/launch.json`. Implement data-driven project cards and the runnable preview within those assigned files. Use strict JSON with no comments for the launch configuration.

## Ordered Implementation

1. **Agree on contracts.** Orchestrator confirms the required project fields (`name`, `owner`, `status`, `recentActivity`, `priority`), includes a short contributor-friendly `summary`, and agrees with Designer and Coder on the `.dashboard` and `.project-card` hooks and status/priority labels.
2. **Prepare independent foundations in parallel.** Designer implements the agreed responsive design in `app/styles.css`. Coder creates representative project records in `app/project-data.json`, using a top-level `projects` array and the agreed fields. These tasks have separate file ownership and can run in parallel after the contracts are set.
3. **Build the page and preview configuration.** After the data and markup/style contracts are settled, Coder implements `app/index.html` to reference the CSS and JSON and render each project’s required information. Coder creates `.vscode/launch.json` with the name **Run Project Pulse Dashboard**, serving from `${workspaceFolder}/app` and opening `index.html`. The page and launch configuration have separate scopes and may be implemented in parallel once their paths and requirements are fixed.
4. **Integrate and validate sequentially.** Orchestrator checks that the page, data, styles, and launch configuration agree; resolve integration issues before reporting completion.

## File Assignments and Dependencies

- `app/styles.css` — Designer. Depends on the agreed card markup and class contract; must include `.dashboard`, `.project-card`, `border-radius`, and `box-shadow`.
- `app/project-data.json` — Coder. Independent after the data contract; must contain a top-level `projects` array and required fields for each project.
- `app/index.html` — Coder. Depends on the JSON schema and Designer’s agreed markup/style hooks; must show **Project Pulse**, reference `styles.css` and `project-data.json`, and render visible cards with status, recent activity, and priority.
- `.vscode/launch.json` — Coder. Independent of visual styling; configure Python’s HTTP server on port 5500 with `cwd` set to `${workspaceFolder}/app`, and open `http://localhost:%s/index.html` through `serverReadyAction`.

## Parallel and Sequential Work

- **Parallel:** Once the shared contracts are agreed, Designer can implement `app/styles.css` while Coder prepares `app/project-data.json`. After the page and launch requirements are fixed, Coder’s `app/index.html` and `.vscode/launch.json` work can proceed independently if separately scoped.
- **Sequential:** Agree on data and markup contracts before implementation; finish the JSON and CSS contract before integrating the page; validate the integrated app after all four files are complete. Any changes to shared markup or selectors require coordination before either specialist edits that contract.

## Assumptions and Risks

- The app is static and needs no framework or package setup; the HTTP server is needed so the page can fetch JSON.
- No project dataset or visual brand specification is provided. Use clearly illustrative sample projects and a readable, contributor-focused design; avoid implying sample data is live.
- Status and priority must remain understandable without color alone. Handle empty or failed data loading, unknown labels, narrow screens, and long project names or activity text without overlap.
- Port 5500 may already be occupied; report the launch failure clearly and use the prescribed configuration unless the Orchestrator approves a port change.

## Validation Expectations

- Confirm all four assigned files exist and inspect the integrated result.
- Parse `app/project-data.json` and `.vscode/launch.json` with `python3 -m json.tool`.
- Check the required fields, page references, visible card content, `.dashboard` and `.project-card` selectors, and required card styling.
- Run **Run Project Pulse Dashboard** and verify the browser opens `index.html` and displays project cards rather than a directory listing.
- Check keyboard access, readable status/priority labels, responsive layout, and empty/error behavior. The repository’s Step 2 workflow checks plan terms and assignments; Step 3 checks app files and required phrases/JSON syntax. Those automated checks do not replace the runtime preview check.

## Open Questions

- Which real projects and summaries should replace the illustrative sample records? This does not block implementation; confirm with Mona before treating sample data as authoritative.