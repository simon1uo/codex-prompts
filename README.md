# 📂 Codex Prompts

A curated collection of reusable prompt templates that help you prototype and ship Codex-powered workflows faster.

## Overview

This repository centralizes prompt building blocks aligned with the latest OpenAI Codex prompting guidance. Each template illustrates a specific interaction pattern so you can rapidly adapt it to your own product or experiment.

## Template Directory

- [`prompts/compliance.md`](prompts/compliance.md): Reuse-first implementation workflow that enforces compliance checks, code audits, and validation steps for strict architecture adherence. Source: [Suspicious-Prune-442/My Best Workflow for Working with Claude Code](https://www.reddit.com/r/ClaudeAI/comments/1m3pol4/my_best_workflow_for_working_with_claude_code/)
- [`prompts/kiro.md`](prompts/kiro.md): KIRO workflow that produces requirements, design, and implementation planning artifacts with explicit user approvals at each stage. Source: [kingkongshot
/KIRO](https://github.com/kingkongshot/prompts/blob/main/prompts/kiro/spec.md)
- [`prompts/riper.md`](prompts/riper.md): RIPER workflow (Research → Innovate → Plan → Execute → Review). Source: [robotlovehuman/RIPER-5 Mode](https://forum.cursor.com/t/i-created-an-amazing-mode-called-riper-5-mode-fixes-claude-3-7-drastically/65516).

## Getting Started

- Clone or fork this repository.
- Explore the `prompts/` directory, which groups sample prompts by task or interaction style.
- Copy any prompt template into your project or Codex working folder, and update the problem statement, input/output schema, or tool instructions to match your scenario.

## Installing Templates in Codex

Follow the official Codex prompting guide to register these templates as reusable slash commands:

1. **Pick a destination.** Codex loads prompts from `$CODEX_HOME/prompts/` (defaults to `~/.codex/prompts/`). Create the folder if it does not exist or override the location by exporting `CODEX_HOME`.
2. **Copy the template.** Save the Markdown file as `<name>.md` inside the prompts folder. The filename (minus `.md`) becomes the slash command, so `riper.md` registers `/prompts:riper`.
3. **Restart Codex.** Prompts are scanned when a session starts. Restart the Codex app (or open a new session) after adding or editing files to refresh the catalog.
4. **Invoke the prompt.** In the Codex composer, type `/` to open the slash popup, choose `/prompts:<name>`, supply any required arguments, and press Enter. Named placeholders such as `$FILE` must be provided via `KEY=value` pairs (e.g., `/prompts:lint FILE=src/app.ts`), while positional placeholders map to `$1`–`$9`.

Codex ignores non-Markdown files and hides prompts that collide with built-in command names, though you can still run them explicitly via `/prompts:<name>`.

## Using the Templates Safely

To achieve reliable Codex responses, keep these guardrails in mind:

1. **Set clear intent.** Introduce the assistant's role, user persona, and success criteria before you provide data or code.
2. **Ground Codex.** Feed structured examples (I/O pairs, tests, checks) so the model learns the target format.
3. **Constrain actions.** List allowed tools or commands explicitly and call out anything that must never be attempted.
4. **Iterate with feedback.** Capture failure cases in follow-up prompts or regression suites to tighten alignment.
5. **Protect secrets.** Never include production credentials, proprietary code, or customer data in shared templates.

These guidelines are distilled from the official prompt design recommendations linked in the References section.

## Template Structure

While each prompt varies, most follow a repeatable skeleton:

```text
System Role          → Frame capabilities, boundaries, and tone.
User Task            → Describe the current request or problem context.
Constraints & Rules  → Specify syntax, safety requirements, or tooling limits.
Examples (Optional)  → Provide I/O demonstrations or edge cases.
Checklist            → Summarize success criteria and failure modes.
```

Feel free to tailor these sections or add domain-specific instructions as needed.

## Designing Prompt Files

Summarized from the GPT-5 Codex prompting guide:

- **Start minimal.** Mirror the lean Codex CLI developer message and add only task-critical rules to avoid oversteering the model.
- **State non-negotiables up front.** Capture repo conventions, safety boundaries, or required tools in short, explicit bullet lists.
- **Limit tool exposure.** Declare only the shell and `apply_patch` unless your workflow genuinely requires more; trim verbose tool blurbs.
- **Skip preambles.** GPT-5 Codex will not emit summaries when forced; rely on Codex CLI's built-in summarizer instead of prompting for one.
- **Prefer concrete checks.** Encode acceptance tests, lint commands, or validation steps the agent can execute instead of lengthy prose.
- **Document arguments clearly.** Explain expected `KEY=value` pairs or positional inputs when you introduce placeholders.
- **Review and prune regularly.** Remove obsolete guidance to keep prompts aligned with evolving repositories or tooling.

## Contributing

1. Review the existing prompt categories to avoid duplication.
2. Add new templates under `prompts/<category>/` with a concise filename.
3. Include a short `README` or inline comments describing expected inputs, outputs, and evaluation criteria.
4. Run any relevant automated checks or linting tools before opening a pull request.
5. Submit a pull request that explains the motivation, testing strategy, and links to any demo artifacts.

## References

- [OpenAI Codex Prompting Guide](https://github.com/openai/codex/blob/main/docs/prompts.md)
- [GPT-5 Codex Prompting Cookbook](https://cookbook.openai.com/examples/gpt-5-codex_prompting_guide)
- [OpenAI Codex Developer Prompts](https://developers.openai.com/codex/prompting)

## License

This project is released under the [MIT License](./LICENSE). By contributing, you agree that your contributions will be licensed under the same terms.
