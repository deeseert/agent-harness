# The AI harness: how to use it

The main Claude Code session is the **orchestrator**, and specialist agents handle each rail. You talk to the orchestrator: it plans, delegates, reviews the specialists' work and keeps the vault current.

## The team

| Rail | Specialist | Use it for |
| --- | --- | --- |
| Harness | orchestrator (main session) | Planning, decisions, automations you start yourself |
| Research | `researcher` | Markets, competitors, prices, regulations, always with sources |
| Ops brain | orchestrator + this vault | Notes, boards, briefs, reviews |
| Outbound | `outbound` | Prospect lists, lead notes, first-message drafts (never sends) |
| Content | `marketer` | Offers, copy, posts and campaigns |
| Design | `designer` | Landing pages and UI |
| Build | `engineer` | Code and small tools |

The definitions live in `.claude/agents/`. Run `/agents` in Claude Code to see and edit them.

## How to delegate

- Let the orchestrator choose: "Find 20 bakeries in my city that sell online" goes to `outbound`.
- Or name the specialist: "Use the researcher to check flour wholesale prices", or "Ask the marketer for the offer in Spanish".
- Chain them, with the orchestrator reviewing between steps: researcher, then marketer, then designer, then engineer.

## Guardrails (all specialists)

- Nothing is sent, published, bought or charged without your explicit OK.
- Facts come with sources, and estimates are labelled.
- No invented results, clients, testimonials or scarcity.

## Learning routine

- Delegate one task per working session, and read the specialist's output critically.
- When a specialist gets something wrong twice, edit its file in `.claude/agents/`, or add the rule to `CLAUDE.md` if it applies to everyone. See `docs/lessons.md` in the repo root.
- Keep agent instructions short. Project facts belong in the vault, not in the agent files.
