# agent-harness

This is the setup I use to work with AI agents every day. Claude Code is the orchestrator: I talk to it, it plans the work, hands parts of it to specialist agents and keeps my notes up to date. The notes live in an Obsidian vault in the same repo, so the agents and I read the same context.

## How it works

```text
                         you
                          |
        orchestrator (main Claude Code session, reads CLAUDE.md)
                          |
   +-----------+----------+----------+-----------+
   |           |          |          |           |
researcher  marketer   designer   outbound   engineer
   |           |          |          |           |
   +-----------+-----  vault/  ------+-----------+
          (briefs, playbooks, leads, notes)
```

- The orchestrator reads `CLAUDE.md` first. It says who you are, what you're focused on, how to delegate and what never to do.
- Each specialist is a short file in `.claude/agents/`. It says what the agent is for, what to read before starting, its rules and what it has to return.
- Project facts live in the vault, not in the agent files. A specialist reads the project's brief before it starts.
- The orchestrator reviews what a specialist returns before acting on it, and then updates the vault itself.

## What's inside

| Path | What |
| --- | --- |
| `CLAUDE.md` | The orchestrator's handbook. Fill in the parts marked `TODO` |
| `AGENTS.md` | Points Codex, Cursor and other agents to `CLAUDE.md` |
| `.claude/agents/` | The specialists: researcher, marketer, designer, outbound, engineer |
| `.claude/skills/` | Skills the agents load when a task needs them |
| `.claude/settings.json` | Claude Code project settings and permissions |
| `vault/` | The Obsidian vault: home page, board, projects, playbooks, leads, templates, notes |
| `docs/lessons.md` | A log of the rules added to the harness, and why |
| `n8n/` | Exported n8n workflows |

## Getting started

1. Clone the repo:

   ```bash
   git clone https://github.com/deeseert/agent-harness.git
   cd agent-harness
   ```

2. Open `CLAUDE.md` and fill in the parts marked `TODO`: who you are, your current focus and anything you want the agents to always or never do.
3. Open `vault/` in Obsidian. This is optional, the agents only need the markdown files. I use the Dataview, Kanban and Templater plugins.
4. Add the MCP servers and skills you need (see below).
5. Start Claude Code in the repo root and say what you want to do, for example: "Use the researcher to compare the price of this product in three shops".

It may need some adjusting before it fits your setup. The agents, skills and MCP servers are the parts you'll most likely change.

## MCP servers

MCP servers give the agents tools they don't have by default. I use them mostly for search:

| Server | What I use it for | Used by |
| --- | --- | --- |
| [Firecrawl](https://docs.firecrawl.dev/mcp-server) | Web search and reading full pages, including pages that need JavaScript | researcher, outbound |
| [Exa](https://docs.exa.ai/reference/exa-mcp) | Search by meaning, and finding companies and people | researcher, outbound |
| [Apollo](https://www.apollo.io) | Finding companies and contacts for outreach | outbound |

None of them is required. Without them, the agents fall back on Claude Code's own web search and fetch tools.

To add one:

1. Add the server to Claude Code with `claude mcp add`, following the server's own docs. Most of them need an API key. Keep it in your environment, never in the repo. See [Connect Claude Code to tools via MCP](https://docs.anthropic.com/en/docs/claude-code/mcp).
2. Give the agents access. The researcher, marketer and outbound agents have a `tools` list in their frontmatter, so add the server's tools there, for example `mcp__firecrawl__firecrawl_search`. The exact names depend on the name you gave the server: run `/mcp` in Claude Code to see them. An agent without a `tools` list can use every tool, MCP included.

## Skills

A skill is a folder with a `SKILL.md` file: instructions for one kind of task, which the agent loads only when the task needs it. That keeps the agent files short.

Only `product-research` is in this repo. The others are open source (MIT) and stay in their own repos, so you install them and get their updates.

### Research

`.claude/skills/product-research/` is a method for researching products, prices and competitors. The researcher loads it through the `skills` list in its frontmatter.

### Coding

The engineer agent reads [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) when they fit: planning and task breakdown, incremental changes, code review, debugging, simplification, security, and more. Add them as a submodule:

```bash
git submodule add https://github.com/addyosmani/agent-skills.git .agents/agent-skills
```

### Design

The designer agent uses these when they fit:

| Skill | What it does | Install |
| --- | --- | --- |
| [design-taste-frontend](https://github.com/Leonxlnx/taste-skill) | Art direction for frontend pages, and checks the result in a real browser. Also audits an existing page before redesigning it | `npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"` |
| [high-end-visual-design, minimalist-ui, industrial-brutalist-ui, stitch-design-taste](https://github.com/Leonxlnx/taste-skill-classics) | One visual style each | `npx skills add https://github.com/Leonxlnx/taste-skill-classics --skill "minimalist-ui"` (one command per skill) |
| [Superdesign](https://github.com/superdesigndev/superdesign-skill) | Generates and iterates UI designs on a canvas, with its own CLI and account | In Claude Code: `/plugin marketplace add superdesigndev/superdesign-skill`, then `/plugin install superdesign@superdesign` |

`npx skills` is the [open skills CLI](https://github.com/vercel-labs/skills). It asks which agent to install for, so pick Claude Code. `design-taste-frontend` needs Node 22+ and Chrome, Edge or Chromium installed.

### Your own

Create `.claude/skills/<name>/SKILL.md` with a `name` and a `description` in the frontmatter. The description decides when the skill gets used, so say clearly what kind of task it's for. `npx skills find` searches for skills other people have published.

## Agents

Each agent is a markdown file in `.claude/agents/` with a short frontmatter (`name`, `description`, and optionally `tools` and `skills`) and its instructions. The description tells the orchestrator when to delegate to it. Run `/agents` in Claude Code to see and edit them.

Keep them short and general. When an agent gets the same thing wrong twice, add a rule to its file, or to `CLAUDE.md` if it applies to everyone, and log it in `docs/lessons.md`.

## Automations (n8n)

`n8n/` holds workflows exported from [n8n](https://n8n.io) as JSON. Import one from the n8n editor. The example included reads public job boards on a schedule and filters the roles. n8n doesn't need to be always on for this kind of batch job: anything that has to be always on, like forms or payments, belongs in the app itself.

## How I use it

- I start every session from `vault/HOME.md`.
- Before building anything for a new idea, I write a short brief with a decision date and the criteria to continue or stop. The only signal I count is money: payments, pre-orders, signed pilots.
- I delegate one task per session and read the output critically.
- Nothing is sent, published or bought without my OK. The agents draft, I send.
- When an agent gets something wrong, I add a rule where it will read it next time. That is how the harness gets better.

## Credits

- Engineering skills: [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills).
- Design skills: [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill), [Leonxlnx/taste-skill-classics](https://github.com/Leonxlnx/taste-skill-classics) and [superdesigndev/superdesign-skill](https://github.com/superdesigndev/superdesign-skill).
- The experiment rules borrow from Alex Hormozi's *$100M Offers* and *$100M Leads*.
- The customer interview playbook follows *The Mom Test* by Rob Fitzpatrick and the Jobs To Be Done switch interview by Bob Moesta.

## License

MIT
