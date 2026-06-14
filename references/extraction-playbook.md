# GitHub Solution Extraction Playbook

Use this playbook after GitHub evidence or repository candidates have been found. The goal is to turn projects, issues, PRs, code, examples, releases, and docs into a local solution for the user's specific problem.

## Read in This Order

Use GitHub CLI (`gh`) as the default inspection entrypoint before browser scraping or custom scripts. Start from `gh search repos`, `gh search issues`, `gh search prs`, `gh search code`, `gh repo view`, `gh issue view`, `gh pr view`, and `gh api`, then deep-read the strongest evidence.

1. Repository README/docs for candidate projects to identify what the project does, its public workflow/API, setup path, stated limitations, and license.
2. Examples, templates, source code, tests, and fixtures that show the correct implementation or configuration shape.
3. Matching issues, PRs, or discussions to identify known edge cases, affected versions, maintainer stance, and fixes or workarounds.
4. Merged PR diff, release notes, changelog, or commit messages to see whether a fix shipped and how behavior changed.
5. Repository-level architecture only when a complete project is the solution source or the problem is an implementation blocker rather than a narrow error.

## Extract What Matters

For each strong evidence item, identify:

- project basics: repo, URL, Stars, forks, language, license, activity, and what the project actually provides;
- root cause: what actually fails and under which versions, inputs, environments, or configuration;
- reusable surface: CLI command, package/API, service, example, architecture, config, test pattern, data model, or operational workflow worth using;
- solution pattern: patch, dependency upgrade/downgrade, config change, API usage, migration, retry/fallback, data model, or workflow;
- applicability: exact conditions needed for the solution to match the user's local problem;
- verification: tests, reproduction command, fixture, build, real request, browser check, or operational signal that proves the fix;
- risk: stale workaround, breaking change, hidden dependency, security/privacy issue, license obligation, deployment mismatch, or maintainer warning;
- adaptation boundary: which parts can be reused directly, which local interfaces/config/data/auth/deployment details must change, and what must not be copied blindly.

## Translate to Local Work

The local recommendation should say:

- reuse: the existing GitHub project's workflow, API, config, example, or operational pattern that should remain intact;
- adapt: only the version, framework, runtime, deployment, data, auth, interface, or scale differences required by the user's local problem;
- avoid: adjacent fixes, old workarounds, unsafe patches, large architecture copies, heavy rewrites of the upstream solution, or unverified suggestions;
- verify: the exact command, request, test, or check required before claiming the problem is solved.

When a repository itself is a candidate solution, include a compact table in the answer with repo, Stars, forks, language, license, activity, basic content, fit, and local adaptation. When the strongest evidence is an issue/PR/code example rather than a reusable project, the project table is optional.

## Subagent Evidence Handling

Subagents are conditional research aids, not a default requirement. If they are used, the controller must merge and deduplicate their findings, then directly verify the strongest claims with `gh`, source reads, tests, logs, real requests, or official docs before finalizing.

The final answer should include a subagent trace with each subagent's scope, evidence surfaces, key findings, rejected candidates, deduplication results, and controller verified claims.

## Avoid These Failure Modes

- Searching only high-star repositories when the problem is an error or regression.
- Treating Stars as proof of applicability instead of a maturity and tie-break signal.
- Treating a similar keyword as a match without checking version, API, and environment.
- Ignoring unresolved state, maintainer warnings, or release availability.
- Copying a patch without license and compatibility awareness.
- Rewriting a mature solution instead of adapting its public workflow to the local codebase.
- Recommending a workaround when a released fix exists.
- Claiming GitHub evidence exists without direct links to the relevant issue, PR, code, example, or release.
- Passing tokens, cookies, private repository contents, sensitive logs, secrets, production data, or credentials to subagents.

## Evidence Standard

When an evidence item materially affects the recommendation, include a direct link to the relevant issue, PR, source file, example, release, or docs page. Keep quotes short and summarize the solution in your own words.
