# Your Claude Code Agent Team

## What this is

A 4-role team built on Claude Code's **subagents** feature:

- **Lead Agent** — this isn't a separate file you invoke; it's *the main Claude Code session
  itself*, shaped by `CLAUDE.md`. Claude Code can't have a subagent that calls other
  subagents, so the main session is the natural place for a "manager/report writer" role.
- **Project Manager**, **Researcher/Analyst**, **Marketing Strategist** — real subagents in
  `.claude/agents/`, each with its own system prompt, tool access, and trigger conditions.

## How to install it

1. Copy this whole folder's contents into the root of your project (wherever you run
   `claude` from). You should end up with:
   ```
   your-project/
     CLAUDE.md
     marketing-plan.md
     budget-tracker.md
     .claude/
       agents/
         project-manager.md
         researcher-analyst.md
         marketing-strategist.md
   ```
2. Run `claude` in that directory. Claude Code auto-loads `CLAUDE.md` and the subagent
   definitions — no separate registration step needed.
3. Run `/agents` inside Claude Code any time to see the three subagents listed, tweak their
   tools/model, or add more.

## How it behaves day to day

- Just talk to the main session normally — it's your Lead Agent. It decides when to delegate.
- You can also invoke a subagent directly by name if you want to skip the routing logic, e.g.
  "have researcher-analyst look into X."
- The Researcher/Analyst has **no write/edit tools on purpose** — that's what enforces its
  neutrality, not just the prompt. Don't add `Write` or `Edit` to its tool list unless you
  intentionally want to loosen that constraint.
- `marketing-plan.md` and `budget-tracker.md` are plain files for now. If you want the
  Project Manager working against your actual Google Sheet instead of `budget-tracker.md`,
  connect a Google Sheets MCP server (or point it at a local `.xlsx` — Claude Code has a
  built-in `xlsx` skill for that) and tell it in your prompt; update its tool list if the
  connector needs to be explicitly enabled.

## Things worth knowing before you rely on this

- Subagent behavior (available tools, whether `WebSearch` is on by default, how `/agents`
  works) is an active area of Claude Code development — if anything here doesn't match what
  you see, check `https://docs.claude.com/en/docs/claude-code/sub-agents` for the current
  behavior, since my knowledge of this feature could be out of date.
- These prompts are a starting point, not a finished product — the neutrality rules for
  Researcher/Analyst and the report format for the Lead Agent are the parts most worth
  reading closely and adjusting to how your team actually talks.
