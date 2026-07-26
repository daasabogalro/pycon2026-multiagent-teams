Review the pull request that adds "discovery, sharing, and messaging" to Stable Match
  (the diff of branch `feat/discovery-messaging` against `main`). Produce ONE reconciled
  review that ends in a single verdict: MERGE or DON'T MERGE.

  Split the work across your team — one agent per review lens, working in parallel. Use
  your shared task list to track each lens as its own task, and let teammates message each
  other directly to work out disagreements before the synthesis step (see CONFLICTS
  RESOLVED below) — that direct peer negotiation is the point of running this on Claude Code.
  - SECURITY — injection, broken authentication/authorization, data exposure, unsafe input
    handling, secrets.
  - CORRECTNESS — does the code do what the PR description claims? Logic errors, inverted
    conditionals, boundary/edge cases, error handling.
  - PERFORMANCE — N+1 queries, work done inside loops that shouldn't be, needless round-trips.
  - TESTS — do the new/changed tests actually exercise the new behavior, or could a bug slip
    through while the suite still passes?

  Scope and rigor:
  - Review the DIFF. You may read surrounding code for context, but only report issues the
    diff introduces or makes worse — not pre-existing issues in untouched code.
  - For every finding: cite file:line, state its category, explain why it's a real problem
    (not a style preference), and give a concrete fix.
  - Do not invent problems. If a line looks suspicious but is actually fine, say so — a clean
    bill on a scary-looking line is a valid finding.

  Then SYNTHESIZE — this is the point of the exercise, do not skip it:
  - Merge duplicate findings that more than one reviewer raised into a single item.
  - Where two lenses conflict (e.g. a performance fix that would weaken security), resolve it
    explicitly: state the tradeoff and recommend a resolution. Do not just list both sides.
  - Rank the real issues by severity: blocking vs non-blocking.
  - Emit ONE verdict for the whole PR, not four separate reviews.

  Write the final reconciled review to a file named REVIEW.md in the repo root — exactly the
  shape below — then STOP. The review is complete once the file is written; do not wait for or
  request further work.

  # Stable Match — PR Review
  1. VERDICT — MERGE / DON'T MERGE, one line why.
  2. BLOCKING ISSUES (ranked) — [category] file:line — problem — fix.
  3. NON-BLOCKING NITS — brief.
  4. CONFLICTS RESOLVED — where two reviewers disagreed and how the team reconciled it.
  5. CONFIDENCE — one line on what you're least sure about.

  Appendix: each lens's raw findings *before* synthesis.
