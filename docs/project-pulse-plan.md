# Project Pulse Implementation Plan

## Summary

Build a lightweight static Project Pulse dashboard for contributors. The dashboard should make active projects, owners, status, recent activity, priority or risk, and contributor-friendly summaries easy to scan. The result should be a polished responsive UI served from the `app/` directory and opened directly at `index.html` through the `Run Project Pulse Dashboard` launch configuration.

## Implementation Phases

### Phase 1: Establish the project data contract

**Owner:** Coder

**File assignment:** `app/project-data.json`

- Create a top-level `projects` array.
- Give each project the fields `name`, `owner`, `status`, `recentActivity`, and `priority`.
- Use representative data that covers active work, different statuses, and multiple priority or risk levels.
- Keep the JSON valid and stable so the page can load it deterministically.

### Phase 2: Define the dashboard experience

**Owner:** Designer

**File assignment:** `app/styles.css`

- Establish the visual direction, typography, color variables, spacing, and responsive layout.
- Design a clear page header and project-card grid that supports quick comparison.
- Make status and priority easy to distinguish with readable badges and accessible contrast.
- Define responsive behavior for narrow screens and predictable CSS hooks for the dashboard and project cards.
- Account for focus states, reduced-motion preferences, and layouts that do not depend on hover.

### Phase 3: Implement the dashboard UI

**Owner:** Coder, using the Designer's decisions

**File assignment:** `app/index.html`

- Build the Project Pulse page structure with the exact title `Project Pulse`.
- Load `app/project-data.json` and render the project information into the dashboard.
- Show project names, owners, statuses, recent activity, priorities, and short contributor-friendly summaries.
- Use semantic HTML, meaningful labels, accessible status text, and a clear heading hierarchy.
- Keep the implementation static and avoid introducing a framework or unnecessary dependencies.

### Phase 4: Configure local launch

**Owner:** Coder

**File assignment:** `.vscode/launch.json`

- Add a launch configuration named `Run Project Pulse Dashboard`.
- Serve the `app/` directory as the web root.
- Open `index.html` when the configuration starts so the dashboard is shown instead of a directory listing.
- Use the repository's existing runnable-app conventions where applicable.

### Phase 5: Integrate and validate

**Owner:** Orchestrator

**File assignments:** All files above

- Review the Designer and Coder handoffs for consistency.
- Confirm that the data fields consumed by `app/index.html` match `app/project-data.json`.
- Confirm that the launch configuration serves the correct directory and opens the correct page.
- Run the available exercise validation and inspect the rendered dashboard at desktop and mobile sizes.

## File Dependencies

- `app/index.html` depends on the `projects` schema in `app/project-data.json`.
- `app/index.html` depends on selectors and visual states defined in `app/styles.css`.
- `.vscode/launch.json` depends on `app/index.html` and the `app/` directory being present.
- The launch configuration and browser validation depend on all three app files being integrated successfully.

## Parallel Work Decisions

- The Designer can work on the visual and responsive specification in `app/styles.css` while the Coder defines the independent data contract in `app/project-data.json`.
- The Coder can prepare the semantic HTML structure in `app/index.html` in parallel with those tasks, provided the final data field names remain aligned with the agreed contract.
- `.vscode/launch.json` can be prepared in parallel with the app files because it only requires the known `app/` root and entry point.
- Final integration and browser validation must happen after the parallel work is complete so selector, data, and launch mismatches can be caught together.

## Designer Responsibilities

- Establish the information hierarchy and visual language for a contributor-focused dashboard.
- Specify project-card layout, status and priority treatments, readable spacing, responsive breakpoints, and interaction states.
- Ensure keyboard focus, contrast, semantic relationships, and reduced-motion behavior are considered.
- Keep the design implementable with the static files in this repository.

## Coder Responsibilities

- Implement the data, semantic page structure, styling, and launch configuration assigned in the phases above.
- Preserve the agreed JSON contract and connect the page to the data without hardcoding a conflicting schema.
- Keep the app dependency-free unless an existing repository dependency is required.
- Verify that the dashboard renders useful content and remains usable on small screens.

## Validation Expectations

- `docs/project-pulse-plan.md` exists and records the goal, phases, ownership, dependencies, parallel work, and validation approach.
- `app/project-data.json` is valid JSON with a top-level `projects` array and all required project fields.
- `app/index.html` contains the exact `Project Pulse` title and renders the required project information.
- `app/styles.css` provides the dashboard and project-card presentation, readable contrast, responsive behavior, and focus states.
- `.vscode/launch.json` contains `Run Project Pulse Dashboard`, serves from `app/`, and opens `index.html`.
- The exercise validation script passes.
- A local preview opens the Project Pulse UI directly, with no directory listing, and remains legible at desktop and mobile viewport sizes.

## Edge Cases and Risks

- Invalid JSON or a changed field name can leave the dashboard empty; validate the data file and keep the schema explicit.
- Missing data should not produce confusing blank cards; the page should expose a clear empty or loading state if it cannot render projects.
- Long project names, owner names, and activity text must wrap without breaking the card layout.
- Status and priority should not be communicated by color alone.
- The launch configuration must point to the `app/` directory so the entry page is displayed directly.

## Open Questions

- The final project examples, branding details, and exact visual tokens can be chosen during implementation because the brief defines the required information and behavior but does not prescribe specific content.
