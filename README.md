# Engineering Discipline — LLM Coding Guidelines

A single `CLAUDE.md` file with 10 engineering discipline rules, distilled from [Andrej Karpathy's internal CLAUDE.md](https://x.com/karpathy) used at Anthropic (June 2026). Tool-agnostic — works across **Claude Code**, **Codex**, **Cursor**, **WorkBuddy**, and any LLM coding assistant.

English | [简体中文](./README.zh.md)

## Why This Exists

The community knows the 4-rule version (Think Before Coding, Simplicity First, Surgical Changes, Goal-Driven Execution). This is the **full 10-rule internal version** — the one that also teaches the model how to **verify itself**, debug systematically, manage dependencies, communicate clearly, and self-audit before declaring done.

> *"These are not suggestions. These are rules. Follow them and you'll produce code that doesn't need to be rewritten."*
> — Andrej Karpathy

## The 10 Rules at a Glance

| # | Rule | What It Prevents |
|---|------|-----------------|
| 1 | **Read Before You Write** | Alien code that doesn't match the codebase |
| 2 | **Think Before You Code** | Silent assumptions, hidden tradeoffs |
| 3 | **Simplicity** | Over-engineering, premature abstraction |
| 4 | **Surgical Changes** | Unnecessary diff noise, style drift |
| 5 | **Verification** | Code that *seems* to work but doesn't |
| 6 | **Goal-Driven Execution** | Vague tasks, unclear success criteria |
| 7 | **Debugging** | Guessing instead of investigating |
| 8 | **Dependencies** | Bloated package manifests, unnecessary deps |
| 9 | **Communication** | Unclear commit messages, unflagged concerns |
| 10 | **Common Failure Modes** | Kitchen Sink, Wrong Abstraction, Runaway Refactor, etc. |

## The Four Phases

```
┌─────────────────────────────────────────────┐
│  Pre-flight    →  Surface assumptions       │
│                   State the plan             │
│                  (Rule 2, Rule 6)            │
├─────────────────────────────────────────────┤
│  In-flight     →  Rules 1-4 for writing     │
│                   Rule 8 for dependencies   │
├─────────────────────────────────────────────┤
│  Post-flight   →  Rule 5 (verification)     │
│                   Rule 7 (if debugging)      │
│                   Rule 9 (communication)     │
├─────────────────────────────────────────────┤
│  Self-audit    →  Rule 10 failure modes     │
│                   before declaring done      │
└─────────────────────────────────────────────┘
```

## Install

### Option A: Claude Code Plugin (recommended)

From within Claude Code, first add the marketplace:

```
/plugin marketplace add murphycheng-24/coding-guidelines
```

Then install the plugin:

```
/plugin install engineering-discipline@coding-guidelines
```

This installs the guidelines as a Claude Code plugin, making the skill available across all your projects.

### Option B: CLAUDE.md (per-project)

New project:

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/murphycheng-24/coding-guidelines/main/CLAUDE.md
```

Existing project (append):

```bash
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/murphycheng-24/coding-guidelines/main/CLAUDE.md >> CLAUDE.md
```

### Option C: Cursor

Copy [`.cursor/rules/engineering-discipline.mdc`](.cursor/rules/engineering-discipline.mdc) into your project's `.cursor/rules/` directory. See **[CURSOR.md](CURSOR.md)** for details.

## Using with Other Tools

These rules are **tool-agnostic**:

| Tool | How to Use |
|------|-----------|
| **Claude Code** | Place `CLAUDE.md` in project root |
| **Cursor** | Use `.cursor/rules/engineering-discipline.mdc` |
| **Codex (OpenAI)** | Include in system prompt or project instructions |
| **WorkBuddy** | The skill loads rules into context automatically |

The rules work because they constrain **universal LLM failure modes** — silent assumptions, over-engineering, style drift, scope creep — which are not tool-specific.

## How to Know It's Working

These guidelines are working if you see:

- **Fewer unnecessary changes in diffs** — Only requested changes appear
- **Fewer rewrites due to overcomplication** — Code is simple the first time
- **Clarifying questions come before implementation** — Not after mistakes
- **Bug fixes verified by reproducing tests** — Not hopeful guessing
- **Clean, minimal PRs** — No drive-by refactoring or "improvements"
- **Specific commit messages** — "Fix null pointer in user lookup" not "Fix bug"

## Customization

These guidelines are designed to be merged with project-specific instructions. Add them to your existing `CLAUDE.md` or create a new one.

For project-specific rules, add sections like:

```markdown
## Project-Specific Guidelines

- Use TypeScript strict mode
- All API endpoints must have tests
- Follow the existing error handling patterns in `src/utils/errors.ts`
```

## Repository Structure

```
.
├── .claude-plugin/
│   └── plugin.json                     # Claude Code plugin config
├── .cursor/
│   └── rules/
│       └── engineering-discipline.mdc  # Cursor IDE rule
├── skills/
│   └── engineering-discipline/
│       └── SKILL.md                    # Reusable skill definition
├── CLAUDE.md                           # Core guidelines (the 10 rules)
├── CURSOR.md                           # Cursor setup guide
├── README.md                           # This file
├── README.zh.md                        # Chinese README
├── LICENSE                             # MIT
└── .gitignore
```

## Tradeoff Note

These guidelines bias toward **caution over speed**. For trivial tasks (simple typo fixes, obvious one-liners), use judgment — not every change needs the full rigor.

The goal is reducing costly mistakes on non-trivial work, not slowing down simple tasks.

## License

MIT © [murphycheng-24](https://github.com/murphycheng-24)
