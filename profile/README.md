# llm-setup-templates

> LLM agent-driven project setup templates. Go from empty directory to GitHub CI green with a single `SETUP.md`.

Each template is a **GitHub Template Repository** — click **Use this template** on any of the repos below to start a new project.

## Templates

| Template | Language / Stack | Primary Use Case |
|---|---|---|
| [**typescript-template**](https://github.com/llm-setup-templates/typescript-template) | TypeScript 5 · Node 20 · FSD 5-layer | Next.js / Node services with strict FSD architecture, Husky + commitlint + lint-staged |
| [**spring-template**](https://github.com/llm-setup-templates/spring-template) | Java 17 (LTS) · Spring Boot 3 · Gradle KTS (Foojay toolchain auto-provision) | 3-layer Spring apps (Controller → Service → Repository), ArchUnit-enforced, Docker + ECS Fargate ready |
| [**python-template**](https://github.com/llm-setup-templates/python-template) | Python 3.13 · uv · Ruff · basedpyright | 3 archetypes: FastAPI service, CLI library, data-science pipeline — all with strict typing and pre-commit |

## What's inside every template

- **`SETUP.md`** — 14 numbered phases that an LLM agent follows top-to-bottom to wire up a new project (deps, lint, format, type check, test, build, CI, PR review) until `ci.yml` is green on GitHub.
- **`CLAUDE.md`** — project overview + verification loop rules that Claude Code loads on every run.
- **`.claude/rules/`** — 4 authoritative rule files (code-style, architecture, git-workflow, verification-loop) loaded by the agent per task.
- **`.claude/skills/claude-md-reviewer/`** — embedded skill that audits CLAUDE.md against best practices.
- **`examples/`** — concrete config files (build scripts, CI workflow, commitlint, CodeRabbit, Dockerfile, archetypes) with `{{PLACEHOLDER}}` fields the agent fills in.
- **`validate.sh`** — placeholder-leak and required-file sanity check.

## Design principles

1. **Fail-fast verification loop** — format → typecheck → static-analysis → lint → test → build. Agents may not declare a task complete until the full loop passes.
2. **Git safety gate** — inline bash block in `SETUP.md` Phase 8.1 blocks pushes on `main`, non-conventional commits, or dirty working trees.
3. **Placeholder discipline** — Mustache `{{UPPERCASE_KEY}}` for every user-input value; `validate.sh` allowlist marks intentional runtime placeholders so leaks are caught.
4. **No migration lock-in** — every template is language-generic. Mind Signal / CheckMate / downstream-specific context has been stripped.

## License

MIT — see each template's `LICENSE` file.
