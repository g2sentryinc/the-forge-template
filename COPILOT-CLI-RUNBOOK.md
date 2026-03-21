# Copilot CLI Runbook

## 1. Start the CLI

```bash
copilot login
copilot --version
copilot
```

## 2. Set the default model

Use `GPT-5 Mini` for normal work.

```text
/model GPT-5 Mini
```

Use a premium model only for:

- greenfield framing
- brownfield analysis
- large architecture analysis
- explicit user request

After analysis, switch back:

```text
/model GPT-5 Mini
```

## 3. Load repo context

```text
Read @.github/instructions/copilot-instructions.md and follow it for this repository.
/skills reload
/skills list
/agent
```

## 4. Greenfield flow

```text
Read @.github/prompts/project/greenfield-init.prompt.md and run that flow with me. Ask clarifying questions first.
```

Then continue phase by phase:

```text
Read @.github/prompts/forge/01-frame.prompt.md and continue from the current repo state.
Read @.github/prompts/forge/02-obstruct.prompt.md and continue from the current repo state.
Read @.github/prompts/forge/03-reconstruct.prompt.md and continue from the current repo state.
```

Switch back to `GPT-5 Mini` before implementation.

```text
/model GPT-5 Mini
Read @.github/prompts/backlog/story-breakdown.prompt.md and break the approved specs into stories.
Read @.github/prompts/backlog/backlog-grooming.prompt.md and groom the current backlog.
Read @.github/prompts/backlog/iteration-planning.prompt.md and create the next iteration plan.
```

## 5. Brownfield flow

Put the existing code in `solution/`, then run:

```text
Read @.github/prompts/project/brownfield-analysis.prompt.md and analyze @solution. Produce technical specs under @spec/technical.
```

After the analysis is done, switch back to `GPT-5 Mini` and continue with backlog and implementation work.

## 6. Single-story implementation flow

```text
/model GPT-5 Mini
Read @spec/iterations/iteration-1/stories/STORY-001.md and implement it in @solution following @.github/instructions/copilot-instructions.md.
```

If needed, pick a role first:

```text
/agent
```

## 7. Dark Factory /fleet flow

Use this after the iteration plan is approved.

```text
/model GPT-5 Mini
Read @spec/iterations/iteration-1/plan.md and summarize the implementation plan.
```

If you want plan mode first, press `Shift+Tab` and refine the plan.

Then run:

```text
/fleet implement the approved iteration plan using the relevant custom agents, keep status documents updated, and stop on blocking issues.
```

Track work:

```text
/tasks
/usage
```

Assess the result:

```text
Read @.github/prompts/dark-factory/assess-iteration.prompt.md and assess the completed iteration.
```

## 8. Useful session commands

```text
/help
/session
/agent
/skills list
/skills reload
/model
/usage
/tasks
```

## 9. Simple non-interactive usage

```bash
copilot -s -p "Read @.github/instructions/copilot-instructions.md and summarize the next FORGE step for this repo."
```

Use `--agent` when you want a specific custom agent:

```bash
copilot -s --agent devops-engineer -p "Review @solution/infra and suggest the next safe deployment change."
```