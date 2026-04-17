# llm-setup-templates

> LLM agent-driven project setup templates. Go from empty directory to GitHub CI green with a single `SETUP.md`.

[![v1.0.0](https://img.shields.io/badge/release-v1.0.0-brightgreen)](https://github.com/llm-setup-templates/typescript-template/releases/tag/v1.0.0)
[![empirically verified](https://img.shields.io/badge/empirically%20verified-LLM%20agent%20no--intervention-blue)](#empirical-verification)

Each template is a **GitHub Template Repository** — click **Use this template** on any of the repos below to start a new project.

## Templates

| Template | Language / Stack | Primary Use Case | Release |
|---|---|---|---|
| [**typescript-template**](https://github.com/llm-setup-templates/typescript-template) | TypeScript 5 · Node 20 · FSD 5-layer · Dependency Cruiser | Next.js with strict FSD, Zod validation, infra isolation (DB driver boundary), Husky + commitlint | [v1.0.0](https://github.com/llm-setup-templates/typescript-template/releases/tag/v1.0.0) |
| [**spring-template**](https://github.com/llm-setup-templates/spring-template) | Java 17 (LTS) · Spring Boot 3 · Gradle KTS · ArchUnit 10 rules | Team-dodn package naming, ApiResponse\<T\> + @ControllerAdvice, multi-module migration ready | [v1.0.0](https://github.com/llm-setup-templates/spring-template/releases/tag/v1.0.0) |
| [**python-template**](https://github.com/llm-setup-templates/python-template) | Python 3.13 · uv · Ruff · basedpyright · Import Linter | FastAPI exception hierarchy, Loguru structured logging, 3 archetypes (FastAPI/CLI/Data-science) | [v1.0.0](https://github.com/llm-setup-templates/python-template/releases/tag/v1.0.0) |

## Empirical Verification (v1.0.0 · 2026-04-17)

All three templates reach **GitHub Actions CI green** from an empty
directory — driven by Claude Code following only `SETUP.md`, **without
human intervention mid-setup**.

| Template | CI run | Duration | Deviations |
|---|---|---|---|
| typescript | [run 24570457723](https://github.com/KWONSEOK02/llm-setup-e2e19-typescript/actions/runs/24570457723) | 9 min | 0 |
| spring | [run 24567854117](https://github.com/KWONSEOK02/llm-setup-e2e18-spring/actions/runs/24567854117) | 8.5 min (CI 2m39s) | 0 |
| python | [run 24571892389](https://github.com/KWONSEOK02/llm-setup-e2e20-python/actions/runs/24571892389) | 7 min | 0 |

**What "no intervention" means**:
- The agent reads only `SETUP.md` (and dotfile references it points to)
- Runs exact commands specified, no creative workarounds
- If a command fails, uses only the template's `Troubleshooting` section
- Does not modify template source files to make things pass
- The only "escape hatch" allowed is `windows-mcp FileSystem` for hook
  files (`.husky/pre-commit`) due to Claude Code permission sandbox —
  equivalent to running the same commands via a different shell.

See each template's README `Empirically verified` link for the
individual proof run.

## What's inside every template

- **`SETUP.md`** — 14 numbered phases that an LLM agent follows top-to-bottom to wire up a new project (deps, lint, format, type check, test, build, CI, PR review) until `ci.yml` is green on GitHub.
- **`CLAUDE.md`** — project overview + verification loop rules that Claude Code loads on every run.
- **`.claude/rules/`** — 4 authoritative rule files (code-style, architecture, git-workflow, verification-loop) loaded by the agent per task.
- **`.claude/skills/claude-md-reviewer/`** — embedded skill that audits CLAUDE.md against best practices.
- **`examples/`** — concrete config files (build scripts, CI workflow, commitlint, CodeRabbit, Dockerfile, archetypes) with `{{PLACEHOLDER}}` fields the agent fills in.
- **`validate.sh`** — placeholder-leak and required-file sanity check.

## Design principles

1. **Fail-fast verification loop** — format → typecheck → architecture boundary → lint → test → build. Agents may not declare a task complete until the full loop passes.
2. **Framework-native conventions** — Spring uses `ApiResponse<T>` wrapper, FastAPI uses `response_model=Schema` direct return, Next.js uses `NextResponse.json()` direct return. No cross-framework pattern forcing.
3. **Architecture boundary enforcement** — ArchUnit (Spring), Import Linter (Python), Dependency Cruiser (TypeScript) catch layer violations at build/CI time.
4. **AI Agent Hard Constraints** — each template's `architecture.md` contains `[CRITICAL]` rules that prevent agents from bypassing response standards, layer boundaries, and observability isolation.
5. **Git safety gate** — inline bash block in `SETUP.md` Phase 8.1 blocks pushes on `main`, non-conventional commits, or dirty working trees.
6. **Placeholder discipline** — Mustache `{{UPPERCASE_KEY}}` for every user-input value; `validate.sh` allowlist marks intentional runtime placeholders so leaks are caught.
7. **No migration lock-in** — every template is language-generic. Downstream-specific context has been stripped.

## License

MIT — see each template's `LICENSE` file.
