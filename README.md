# devkeep-workflows

Public host for [Devkeep](https://github.com/BubbaF377/devkeep)'s reusable GitHub Actions workflows. Copied from [devlore-workflows](https://github.com/BubbaF377/devlore-workflows) on 2026-08-24 (full history preserved) when Devkeep got its own caller-workflow-facing repo, distinct from standalone Devlore's.

Devkeep itself is private, and GitHub only allows a public repository's workflow to call a reusable workflow (`uses: owner/repo/path@ref`) that's *also* hosted in a public repository — a public caller can never reach a private one, regardless of any repository access settings. Splitting these thin orchestration files out here lets Devkeep work with both public and private linked project repos, without making the actual application source public.

Every file here is pure orchestration — checkout, install, run one script — with zero business logic, prompts, or proprietary code. Two different execution models currently coexist, tracked in `docs/PRODUCT.md` (Devlore module doc) as real, ongoing porting work:

- **`draft-log-entry.yml`, `consolidate-release.yml`, `sync-user-manual.yml`** — check out the real (private) `BubbaF377/devkeep` repo at runtime using the caller-supplied `devkeep-github-token`, build `modules/core` + `modules/devlore` fresh, and run the compiled action from there. These three have real Devkeep-native logic ported (module-aware doc sync, the monorepo-shaped core loop).
- **Every other workflow** (`sync-test-plan.yml`, `sync-visualizer.yml`, `sync-onboarding.yml`, `draft-release-notes.yml`, `analyze-codebase.yml`, `capture-baseline-draft.yml`, `capture-baseline-seed.yml`) — still install and run the published `@starterculture/devlore` npm package, standalone Devlore's own compiled output. Devkeep has no native replacement for these yet; they're carried over as-is from `devlore-workflows` so linking still works end-to-end, but they're oblivious to a Devkeep-shaped monorepo (`docs/MODULES.md`, `modules/*`) since that npm package predates it.

Not meant to be used standalone — these are called by Devkeep's own "Link a project" flow when it links a project repo.
