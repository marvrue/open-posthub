# Browse / Chat navigation baseline

This fork preserves the two project navigation modes as the starting point for Posthub adaptation. This change restores navigation only; it does not deploy a new application, migrate data or enable provider calls.

## Provenance

- Fork baseline: `d7ea7852480601af9bc8870942af8311a410e567`.
- Historical source with Browse / Chat tabs: `e0a58757902cf214db8517fe5e1111436f96312a`.
- Upstream removal: `db8bde17e245d01f9ca4ab06acaf37fe22aac361`, “Hide SAM from the UI and fix vite dev on fresh checkouts”. The backend agent and chat routes remained present.
- The historical source is a reproducible upstream reference, **not** a verified byte-for-byte snapshot of an existing self-host deployment.

Git tags `baseline/openseo-fork-2026-10-17` and `baseline/openseo-split-navigation-original` preserve both unmodified references. Work continues on `codex/open-posthub-migration-baseline` with the later upstream fixes retained.

## Restoration

`src/client/components/Sidebar.tsx` restores Browse / Chat below the project switcher. The active tab follows the route, including direct links and browser history. Chat opens the current project's existing SAM route; Browse returns from chat to the same project's overview. While the project is loading, placeholder tabs are disabled. Mobile navigation closes after switching.

The change deliberately does not replace the complete Sidebar with the historical file: that would discard later active-project cleanup and prompt-history navigation fixes. The agent's beta/setup gates, authorization, model configuration and persistence remain unchanged. Opening Chat with no OpenRouter configuration still shows setup; restoring a tab does not create provider credentials.

## Migration boundary

Posthub's detailed migration inventory and acceptance plan are maintained with its existing private application sources. This public baseline contains no copied private application code, customer material, screenshots of private projects, credentials or infrastructure exports. Future reuse must preserve source licenses and explicitly select material suitable for publication.

The target product includes web browsing/editing, the built-in agent, remote MCP and an installable CLI backed by common domain actions. The current OpenSEO plugins are MCP clients; the developer `scripts/cli-auth.ts` is not that future product CLI.

## Validation, 2026-10-17

Frozen-lockfile dependency installation, TypeScript, targeted Sidebar lint and the production build passed. Five existing MCP/agent test files passed (21 tests), covering project/API-key authorization, output contracts, skills and tool adaptation. The build retains upstream bundler warnings.

The local production build was exercised against an isolated local D1 database: Browse → Chat → Browse kept the same project, route selection matched the selected tab, and the mobile drawer closed after switching. At a 390 × 844 viewport, document width was 390 pixels. Browser Back returned to Browse. Desktop and mobile screenshots were retained with the private migration evidence.

No provider credentials were configured. The expected SAM beta/setup gates remain; no model inference, publishing, payment or production database action was tested. The initial development-server run failed loading the worker entry; the production-build preview was used successfully for the checks above. This is a navigation baseline, not a complete agent or SaaS acceptance.
