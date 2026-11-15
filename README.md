# agent-harness

I wanted one system that takes me from an idea to something ready for production, where everything is connected. The knowledge and the scope are shared, and the AI has guardrails that steer it where I want, with less room for hallucination.

Before this, I kept repeating myself. Every session I had to give the AI the right prompt, the right context and the right knowledge again. I used different tools, copied the output of one LLM and pasted it into another, and I had to be very careful, because getting things wrong was very likely.

This is what I use now. Claude Code is the orchestrator. I talk to it, it plans the work, delegates to specialist agents for research, marketing, design, outbound and engineering, and keeps the notes in an Obsidian vault up to date. The agents and I read the same notes, so I don't have to repeat the context every time.

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

## What it's good at

The searches. The researcher goes to the web for fresh data, with sources, and the evaluations start from that, not from what the model remembers.

The structure is the other thing. I can forget the process, lose focus or get stuck on a detail. The harness brings me back to the rules we agreed, the next step and the deadline. Every idea starts as a short brief with a decision date and what would make me continue or stop, and nothing gets built before someone is ready to pay for it.

It's also good at brainstorming with me. For the design of a holiday home website and a developer tool it proposed a couple of directions, we worked on them together, I got feedback from other people and we picked one. On my own it would have taken me much longer.

## It's not perfect

It isn't opinionated enough. It says A, I say B, and it moves to B. When I'm brainstorming that's the opposite of what I need. I want it to hold its position when it's right and let go when it isn't. I know an LLM predicts the next word, but I think there is a way to make it firmer, and I'm still looking for it.

It also plays safe. Even with rules against it, the designs, the copy and the choices tend to be the default ones.

If you've found something that works for either problem, I'd like to hear it. Open an issue.

## Get started

```bash
git clone https://github.com/deeseert/agent-harness.git
cd agent-harness
```

Fill in the `TODO` parts of `CLAUDE.md` (who you are, what you're working on, what the agents must never do), then start Claude Code in the folder and ask for something, for example "use the researcher to compare the price of this product in three shops". Opening `vault/` in Obsidian is nice but not needed.

It won't fit your setup out of the box. Expect to change the agents, the skills and the MCP servers.

## What's in it

- `CLAUDE.md` is the orchestrator's handbook. `AGENTS.md` points other coding agents to it.
- `.claude/agents/` has one short file per specialist. I keep them short and put the project facts in the vault, not in the agents.
- `.claude/skills/product-research/` is the one skill I wrote for this repo.
- `vault/` holds the notes: home page, board, briefs, playbooks, leads and templates.
- `docs/lessons.md` is where I log the rules I add when an agent gets something wrong.
- `n8n/` has exported n8n workflows. The one in there checks job boards every morning.

## MCP servers and skills

For search I connect [Firecrawl](https://docs.firecrawl.dev/mcp-server) and [Exa](https://docs.exa.ai/reference/exa-mcp) as MCP servers, and [Apollo](https://www.apollo.io) for finding companies and contacts. Add them with `claude mcp add`, then add their tools to the `tools` list of the agents that need them (`/mcp` shows the names). Without them the agents use Claude Code's own web search.

The engineer reads [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills):

```bash
git submodule add https://github.com/addyosmani/agent-skills.git .agents/agent-skills
```

The designer uses [design-taste-frontend](https://github.com/Leonxlnx/taste-skill), the style skills in [taste-skill-classics](https://github.com/Leonxlnx/taste-skill-classics) and [Superdesign](https://github.com/superdesigndev/superdesign-skill). Each repo explains how to install it.

## Credits

The experiment rules borrow from Alex Hormozi's *$100M Offers* and *$100M Leads*, and the customer interview playbook from *The Mom Test* by Rob Fitzpatrick and Bob Moesta's switch interview. The skills belong to their authors, linked above.

## License

MIT
