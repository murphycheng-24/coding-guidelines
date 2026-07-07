# Contributing to Coding Guidelines

Thanks for your interest in improving these guidelines! 🎉

## Ways to Contribute

### 1. Report Issues

Found a rule that's unclear, missing, or counterproductive? Open an [issue](https://github.com/murphycheng-24/coding-guidelines/issues) with:

- **What rule** you're referring to (rule number or name)
- **What happened** — describe the scenario where the rule didn't help
- **What you expected** — what would have been more useful

### 2. Suggest Rule Improvements

Rules evolve with practice. If you have a suggestion:

1. Open an issue with the prefix `[Rule Improvement]`
2. Quote the current rule text
3. Explain what's missing or could be better
4. Propose your revised wording

### 3. Add Examples

Real-world Before/After examples are the most valuable contribution. To add one:

1. Fork the repo
2. Add your example to a new section in `EXAMPLES.md` (create if it doesn't exist)
3. Include:
   - **Task description** — what was the user asking for?
   - **Without rules (Before)** — what did the LLM do wrong?
   - **With rules (After)** — how did the guidelines help?
   - **Which rules applied** — reference by number
4. Submit a PR

### 4. Translate

If you'd like to translate the guidelines into another language:

1. Create a `README.<lang>.md` file
2. Translate `CLAUDE.md` content as `CLAUDE.<lang>.md`
3. Submit a PR

## Style Guide

- **Be concise.** Rules should be one sentence when possible.
- **Use imperative voice.** "Read before you write." not "You should read before you write."
- **Explain the why.** Every rule should say what failure mode it prevents.
- **No tool-specific assumptions.** Rules must work across Claude Code, Cursor, Codex, and any LLM coding assistant.

## Pull Request Process

1. Fork the repository
2. Create a branch: `git checkout -b improve-rule-5`
3. Make your changes
4. Commit with a clear message: `git commit -m "Clarify Rule 5: add test-reproduction requirement"`
5. Push: `git push origin improve-rule-5`
6. Open a PR with a description of what and why

## Code of Conduct

Be respectful. Disagree on ideas, not people. Focus on making the guidelines better for everyone.

## License

By contributing, you agree that your contributions will be licensed under the MIT license.
