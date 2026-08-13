---
name: policy
description: >-
  Operate a repository through its pinned Code Policy checkout: inspect policy health, clean up concrete findings, display the configured testing levels, choose and run authorized verification, synchronize managed agent guidance, or start the plan implementation loop. Use when the user invokes /policy or $policy, asks what tests or verification level to run, asks whether a repository is policy-ready, requests a Code Policy cleanup or gate, or wants to run a checked-in implementation plan. Triggers on code policy, policy check, cleanup, test levels, test plan, recommended tests, full tests, supplemental tests, gate, doctor, AGENTS sync, and plan implementation loop.
---

# Operate Code Policy

Use the target repository's pinned policy checkout as the source of truth. Keep
inspection read-only until the user asks for a change or explicitly selects a
verification run.

## Core Workflow

### 1. Establish the Local Contract

Read the target `AGENTS.md`, `.code-policy.json`, Git status, and the checked-in
`check_policy.sh` wrapper before acting. Prefer `./check_policy.sh` for every
engine command. In the Code Policy repository itself, follow its local
instructions for `./bin/code-policy` and the pinned Go toolchain.

Never substitute a global binary or a neighboring checkout for the target's
pinned revision. If the wrapper, config, or pinned checkout is missing, report
that the repository is not fully adopted. Do not install or upgrade Code Policy
unless the user asked for adoption or an upgrade.

Preserve unrelated user changes. Treat project-specific providers, builds, and
tests declared in `.code-policy.json` as part of the policy contract rather
than generic code to delete.

### 2. Display Testing Levels Before Choosing

Resolve the merge target in this order: an explicit user value, checked-in
repository guidance, the symbolic `origin/HEAD`, then an existing
`origin/main` or `origin/master`. If none resolves, omit `--base` and state that
the plan covers current uncommitted changes only.

Run the read-only planner:

```sh
./check_policy.sh test-levels --base <merge-target>
```

Use the ASCII table exactly as emitted in the terminal; do not recreate it as a
Markdown table. The table is calculated from the target's declared suites and
marks the planner's ordinary recommendation. Follow it with the planner's
suite names and reason.

If `test-levels` is unavailable, the target pins an older Code Policy revision.
Run `test-plan` only for compatibility, say that the tabular command requires a
policy upgrade, and do not invent authoritative suite counts.

### 3. Keep the Verification Boundaries Distinct

- Treat focused (`test --changed`, `--module`, or exact `--suite`) as routine
  implementation feedback when repository guidance permits it.
- Treat recommended and full as the two ordinary pre-merge choices. Run either
  only after the user or checked-in lifecycle guidance authorizes it. A direct
  request to run one is authorization for that invocation.
- Treat supplemental mutation and risk suites as a separate decision after
  ordinary verification. They are not a higher ordinary tier and are excluded
  from `test --all`, `verify`, and `gate`.
- Prefer the planner's impact-relevant exact supplemental suite names over
  `test --supplemental`, which runs every declared supplemental suite.
- Treat `verify` as full ordinary tests plus builds, and `gate` as the complete
  policy, ordinary verification, build, and online supply-chain workflow. Do
  not describe either as merely another test level.

When the user has not chosen between recommended and full, present those two
choices with the emitted costs, identify the suggestion, and wait. Do not turn
an ambiguous request such as "test it" into broad verification.

### 4. Run the Selected Scope

Use the selector shown by `test-levels`, preserving the same `--base` for
focused or recommended runs. On failure, diagnose and rerun the exact failing
suite or narrow package first. Do not repeatedly restart a broad run while its
known failure remains.

Report the exact commands, pass/fail result, and anything not run. Never claim
that a skipped or unavailable check passed.

### 5. Clean Up Concrete Policy Findings

Only mutate code when the user asks for cleanup or fixes. Start with:

```sh
./check_policy.sh doctor --strict
./check_policy.sh check --git-changes
```

Use `check --all` only for a requested repository-wide cleanup. Fix confirmed
findings at their owning boundary, then run formatting and focused tests in the
smallest affected scope. Investigate non-blocking warnings when they match the
request, but do not silently convert warnings into failures or add exceptions.

Never create a broad, ownerless, or non-expiring exception to make a run green.
If a deliberate exception is necessary, explain its exact subject, owner,
reason, and expiry before adding it.

### 6. Run a Checked-In Plan Loop

For a plan implementation request, inspect the pinned loop's help and use the
target-owned path:

```sh
./.code-policy/bin/code-plan-loop <plan-path> --repo-root . --verification <level>
```

Require a clean worktree, an existing checked-in plan, and an explicit
verification level. Map focused, recommended, full, and supplemental directly
from the testing-level table; use `none` only when the user authorizes no
automated verification. Do not add `--unattended-permission-bypass` unless the
user explicitly requests that separate execution authority and the environment
is appropriately isolated.

### 7. Maintain Managed Guidance

After an intentional Code Policy pin upgrade, run `agents check`, then
`agents sync` when stale. Preserve the project-owned section of `AGENTS.md`
byte-for-byte and review the resulting managed-policy change.

## Common Mistakes

| Mistake | Correction |
| --- | --- |
| Running a sibling or global policy checkout | Use the target's checked-in wrapper and pinned revision |
| Reformatting planner output by hand | Show the emitted ASCII table unchanged |
| Treating supplemental as part of full | Request a separate decision and run relevant exact suites |
| Running `gate` after permission to run tests | Ask separately unless gate was explicitly authorized |
| Repeating an entire failed broad run | Isolate and rerun the failing suite first |
| Adding an exception to silence cleanup | Fix the owner or make any necessary exception exact, owned, and expiring |
| Starting the plan loop with an inferred scope | Obtain an explicit verification level first |

## Output Format

For a level-selection request, show the terminal table, state the planner's
reason in one sentence, and ask one concise recommended-versus-full question
when authorization is still needed. For execution or cleanup, lead with the
outcome, list exact commands and observed results, distinguish warnings from
findings, and name every required check that remains unrun.
