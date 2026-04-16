# llm-setup-templates

> LLM agent-driven project setup templates. Go from empty directory to GitHub CI green with a single `SETUP.md`.

Each template is a **GitHub Template Repository** — click **Use this template** on any of the repos below to start a new project.

## Templates

| Template | Language / Stack | Primary Use Case |
|---|---|---|
| [**typescript-template**](https://github.com/llm-setup-templates/typescript-template) | TypeScript 5 · Node 20 · FSD 5-layer · Dependency Cruiser | Next.js with strict FSD, Zod validation, infra isolation (DB driver boundary), Husky + commitlint |
| [**spring-template**](https://github.com/llm-setup-templates/spring-template) | Java 17 (LTS) · Spring Boot 3 · Gradle KTS · ArchUnit 10 rules | Team-dodn package naming, ApiResponse\<T\> + @ControllerAdvice, multi-module migration ready |
| [**python-template**](https://github.com/llm-setup-templates/python-template) | Python 3.13 · uv · Ruff · basedpyright · Import Linter | FastAPI exception hierarchy, Loguru structured logging, 3 archetypes (FastAPI/CLI/Data-science) |

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
