# Problem and Project Evidence Rubric

Use this rubric when ranking GitHub evidence for a concrete engineering problem or a repository-level solution. The score is a decision aid, not a replacement for judgment.

## Default Score: 100 points

| Category | Points | What to Check |
| --- | ---: | --- |
| Problem match | 35 | Same error, symptom, API, dependency, framework, version class, runtime, config, workflow, capability, or failure mode. |
| Evidence strength | 20 | Maintainer confirmation, merged PR, released fix, official example, test fixture, repeated independent reports, clear reproduction, or mature project implementation. |
| Local applicability | 20 | Fits the user's repo constraints, versions, deployment target, data/auth model, dependency policy, and risk tolerance. |
| Actionability and adaptation cost | 15 | Provides a concrete patch, config change, version pin/upgrade, API usage, reusable workflow, test, reproduction, or operational step with minimal local adaptation. |
| Project maturity signals | 10 | Stars, forks, recent activity, non-archived status, clear license, docs/examples, maintainer responsiveness, and production use signals. |

## Evidence Priority

- Highest: merged PRs, release notes, maintainer-confirmed issues, official examples, and source/tests showing the exact behavior.
- Strong: resolved issues with matching versions, code examples in active projects, reproducible fixes confirmed by multiple users.
- Strong for repository-level solutions: high-fit, high-Star, active repositories with clear license, real examples, and an implementation that maps cleanly to the user's problem.
- Useful but weaker: similar issues on nearby versions, unmerged PRs, user-discovered workarounds, old but still relevant source examples, or lower-Star projects that demonstrate the exact workflow.
- Weak: speculative comments, stale unresolved issues, archived repos, unrelated high-Star projects, tutorials that do not hit the same failure mode, and "awesome" lists without a usable implementation.

High Stars can put a repository near the top of the inspection list and break ties among similarly fitting projects. Stars must not override a clearly better problem match, official maintainer guidance, or exact same-version evidence.

## Search Surface Handling

- Use GitHub CLI first. Prefer `gh search repos`, `gh search issues`, `gh search prs`, `gh search code`, `gh repo view`, `gh issue view`, `gh pr view`, and `gh api` before browser scraping or custom scripts.
- Search issues and PRs first for errors, regressions, dependency upgrades, framework behavior, and integration failures.
- Search code/examples first for API usage, config shape, feature implementation, or unclear integration patterns.
- Search repositories when the problem is an implementation blocker, tool/capability need, or reusable project search where a complete project can reveal architecture or workflow.
- For repository candidates, start with high-Star active projects, then lower the Star threshold when high-Star projects are too broad or miss the exact need.
- Use Stars and forks as maturity context and tie-breakers. They should not outweigh exact problem evidence.

## Subagent Handling

Subagents are conditional. Use them when the problem spans independent ecosystems, query families, repositories, versions, or evidence surfaces. Skip them when the task has one obvious repository or API surface, when local context must be understood first, or when authorization, private repositories, secrets, sensitive logs, or production data would make delegation risky.

When subagents are used, rank only after merging and deduplicating repeated reports of the same repo, issue, PR, discussion, code path, or release. The controller must directly verify the strongest claims before presenting them as evidence.

## Output Fields

For each shortlisted repository candidate, capture:

- repo name and URL;
- Stars, forks, primary language, license, last push/activity, archived status;
- basic content: what the project does and the primary workflow/API it provides;
- problem fit: why it matches the user's concrete problem;
- reusable parts: API, CLI, workflow, architecture, config, examples, tests, or operational pattern;
- adaptation cost: what must change for the user's local code, data, auth, deployment, or runtime;
- key risk or mismatch.

For each issue/PR/code/release evidence item, capture:

- source type: issue, PR, discussion, code, example, release, docs, or repository;
- title/name and URL;
- repository and project status when available;
- relevant version/environment signal;
- problem match summary;
- proposed solution or pattern;
- key risk or mismatch;
- rank or score rationale.

If subagents were used, also capture:

- subagent scope and assigned query family;
- evidence surfaces searched;
- key findings and direct links;
- rejected candidates and rejection reasons;
- deduplication results;
- controller verified claims.

Use exact metadata only when verified in the current run. If metadata may be stale, label it as such.
