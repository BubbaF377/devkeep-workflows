# devlore-workflows

Public host for [Devlore](https://github.com/BubbaF377/devlore)'s reusable GitHub Actions workflows.

Devlore itself is private, and GitHub only allows a public repository's workflow to call a reusable workflow (`uses: owner/repo/path@ref`) that's *also* hosted in a public repository — a public caller can never reach a private one, regardless of any repository access settings. Splitting these thin orchestration files out here lets Devlore work with both public and private linked project repos, without making the actual application source public.

Every file here is pure orchestration — checkout, install, run one script — with zero business logic, prompts, or proprietary code. Each workflow checks out the real (private) `BubbaF377/devlore` repo at runtime using a caller-supplied token to fetch the actual implementation before running it, so the logic these workflows invoke stays exactly as private as it's always been.

Not meant to be used standalone — these are called by Devlore's own setup wizard when it links a project repo.
