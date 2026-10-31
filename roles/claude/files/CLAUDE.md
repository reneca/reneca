# Personal Claude Code Instructions

## About Me

Senior developer (Rust, C++, Puppet/Hiera, Terraform, Grafana). Prioritize correctness, performance, and simplicity.
No need to explain low-level concepts (memory, concurrency, ownership, lifetimes).

## Workflow

- "Explain / review / analyse / tell me / what do you propose" → answer only. Change code only when asked
- Review findings: numbered list with severity and file:line. I pick which to fix — fix only those
- Never commit, amend, or push unless I explicitly ask. I commit myself after checking. Rebase when asked is fine
- If I say I rewrote code myself, it is final: adapt tests/docs around it, suggest fixes as hints only
- "Revert" means restore fully. "Stop" means stop now
- Ask on ambiguous requirements and non-obvious design trade-offs, with a recommendation
- When available, fetch context yourself through MCP (GitLab jobs/MRs, Jira, Confluence, Grafana) rather than asking me to paste it

## Code

- Before coding, identify constraints, edge cases, and failure modes
- Simplest correct solution. If a fix needs a workaround, the design is wrong — propose the design fix before applying it
- No speculative abstractions, no generalization for one use case
- If multiple approaches exist, reason about trade-offs before picking one
- Reuse first: framework methods, crate re-exports, existing helpers. Search before adding a helper or dependency
- Replacing an API: replace it fully. No deprecated aliases or compat shims
- Rust errors (when error handling is in scope): typed (`thiserror`), no `unwrap`/panic on runtime paths, never catch panics to hide them.
  Error messages must identify their origin
- Don't add features, comments, abstractions, or error handling beyond what was asked
- Only touch code directly related to the request. No reformatting, renaming, or reorganizing outside the edited scope
- Run the project formatter/linter on touched files (rustfmt, cargo clippy, clang-format, pdk validate).
  Revert formatter changes to untouched files
- Trust internal code and framework guarantees — only validate at boundaries

## Docs

- Describe current behavior only: no "previously", "no longer", "instead of". History belongs in commits/release notes
- Never mention internal tools, hostnames, or company systems in public/OSS docs
- Jira/MR write-ups: concise, two parts — Analysis (the problem), Solution (what changed). Only kept changes

## Security

- Never hardcode secrets, tokens, or API keys — always use environment variables
- Validate all input at system boundaries (user input, external APIs, file reads)
- Check for common vulnerabilities: injection, XSS, CSRF, path traversal
- Memory safety is a first-class concern (especially in C++ and unsafe Rust)

## Style

- Be terse. No filler, no trailing summaries, no restating what was just done
- For destructive or irreversible actions, always confirm before proceeding
