# Copilot / AI Agent Instructions for KAGSZO Automation Demo

This repo contains a Vite + React demo that simulates business automation workflows. Keep suggestions and code changes focused, small, and aligned with existing patterns.

Architecture (big picture)
- **App root:** `automation-simulator/Automation simulator/src/main.jsx` → `App.jsx`.
- **Presentation:** Reusable UI in `src/components/` (e.g. `AutomationStep.jsx`, `AutomationTimeline.jsx`, `WorkflowSimulation.jsx`).
- **State & flow:** `src/context/AutomationContext.jsx` provides central state and actions used across components.
- **Business logic / simulation:** `src/utils/apiSimulator.js` emulates remote APIs (delays, failures, retries). `src/utils/configProcessor.js` and `ConfigProcessor.jsx` handle XLSX-based config-driven runs.

Developer workflows (exact commands)
- Install: `npm install` in `automation-simulator/Automation simulator`.
- Dev server: `npm run dev` (Vite, default `http://localhost:5173`).
- Build: `npm run build` → output in `dist`.
- Preview production build: `npm run preview`.

Project-specific conventions and patterns
- Component naming: Many components are prefixed with `Automation` (e.g. `AutomationStep.jsx`) — follow this convention for new UI parts.
- Simulation-first logic: Prefer using `apiSimulator.js` for new integrations/mocks rather than adding new real network calls.
- Single source of truth: Use `AutomationContext.jsx` for cross-component state (avoid local ad-hoc event buses).
- Config-driven flows: XLSX parsing and row-by-row processing lives in `src/utils` and is orchestrated by components under `src/components` (see `ConfigFileUpload.jsx`, `ConfigProcessor.jsx`, `BatchProcessing.jsx`).
- Toasts & logs: Use existing `Toast` / `ToastContainer` and `TechnicalLogs.jsx` to surface runtime events and API payloads.

Integration points & external files
- `public/sample-automation-config.json` — example config used by UI.
- `public/admin_password.txt` — local demo credential (do not commit secrets elsewhere).
- Tailwind config: `tailwind.config.js`, PostCSS in `postcss.config.js`.
- Vite config: `vite.config.js` — modify only if you need custom dev server behavior.

Code patterns to follow (examples)
- Retry logic: see `apiSimulator.js` for how retries and backoff are implemented; mirror its approach when adding simulated failures.
- Sequential processing: Config rows are processed sequentially (not parallel) to maintain visible timeline ordering — preserve this unless intentionally changing UX.
- Component props: UI components accept plain JS objects/arrays; keep prop shapes consistent with existing components (inspect `WorkflowSimulation.jsx` and `AutomationTransactionsTable.jsx`).

What to avoid
- Adding external network calls or new backend integrations directly — prefer using `apiSimulator.js` to keep the demo self-contained.
- Large refactors without incremental PRs — this demo is used to teach UX and behavior; keep changes small and reviewable.

Where to look for more context
- Main README: `automation-simulator/Automation simulator/README.md` (contains usage, XLSX template, and run commands).
- Key files:
  - `automation-simulator/Automation simulator/src/utils/apiSimulator.js`
  - `automation-simulator/Automation simulator/src/context/AutomationContext.jsx`
  - `automation-simulator/Automation simulator/src/components/WorkflowSimulation.jsx`
  - `automation-simulator/Automation simulator/src/components/ConfigProcessor.jsx`

If any instruction is unclear or you want additional examples (tests, lint rules, or contributor workflow), tell me what to expand and I'll iterate.
