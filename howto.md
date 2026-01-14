# HOWTO - Agent Failover Template (Step-by-step)

This is a short usage guide for the template. Keep it updated so any AI agent
or developer can continue without losing context.

## 1) Initial setup (once per repo)
1) Copy this template into your project repo root.
2) Update `agent/context.md` with:
   - Repo purpose
   - Tech stack
   - Important folders
3) Update `agent/models.md` with the actual model routing you use.
4) Update `agent/commands.ps1` with real commands for build/test/lint.
5) Review `agent/rules.md` and keep the rules small and actionable.
6) Optionally add notes in `docs/architecture.md` and `docs/runbook.md`.

## 2) Daily workflow
1) Read `agent/handoff.md` first to understand current state.
2) Read `agent/plan.md` to see the current steps and done criteria.
3) Execute the next step with minimal changes.
4) Update `agent/plan.md` and `agent/handoff.md` as you finish work.

## 3) Handoff to another agent/tool
1) Update `agent/handoff.md`:
   - What is done
   - What is not done
   - Any blockers
   - Next actions
2) Keep the handoff short and specific. No broad refactors.
3) If a decision was made, record it in `docs/decisions.md`.

## 4) Using prompts (optional)
The prompt files in `agent/prompts/` are tool-agnostic. You can paste them into
your agent UI to keep behavior consistent:
- `takeover_prompt.txt` for a new agent takeover
- `implement_step_prompt.txt` for step execution
- `bugfix_prompt.txt` for small fixes

## 5) Quick checklist
- [ ] `agent/context.md` filled
- [ ] `agent/models.md` set to real models
- [ ] `agent/commands.ps1` has real commands
- [ ] `agent/plan.md` current
- [ ] `agent/handoff.md` current
