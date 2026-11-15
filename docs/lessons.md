# Lessons: rules added to the harness

When an agent gets something wrong, don't only fix the answer. Write down what happened and add a rule where the agent will read it next time. This file is the log of those rules.

## How to add a rule

1. Fix the output.
2. Write down what happened in one or two sentences, with the date.
3. Add the rule where the agent will read it: `CLAUDE.md` for everything, an agent file for one specialist, a skill for one kind of task, or Claude Code's memory for how you like to work.
4. Keep the reason next to the rule. An agent follows a rule better when it knows why it exists.
5. If the same mistake comes back, the rule is in the wrong place or too vague. Move it or make it more concrete.

## Template

```markdown
## [Number]. [Short name of the rule]

**Date.** [YYYY-MM-DD]

**What happened.** [What the agent did wrong, in one or two sentences.]

**Rule.** [What the agent must do from now on, written so it can't be misread.]

**Where.** [CLAUDE.md / .claude/agents/<agent>.md / .claude/skills/<skill>/SKILL.md / memory]
```

## Log

## 1. [Short name of the rule]

**Date.** [YYYY-MM-DD]

**What happened.** [What the agent did wrong.]

**Rule.** [The rule.]

**Where.** [Where the rule lives.]
