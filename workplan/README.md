# workplan

A Claude Code skill that structures research tasks using hypothesis-driven methodology from MBB (McKinsey, BCG, Bain) strategy consulting.

## What it does

When an AI agent receives a research or evaluation task, this skill prevents it from jumping straight into execution. Instead, it enforces a structured discipline:

1. **Decompose** the problem into a MECE issue tree before touching a single source
2. **Formulate** a Day One Hypothesis — a falsifiable best guess at the answer
3. **Prioritize** sub-hypotheses by risk (the question that kills the idea fastest goes first)
4. **Execute** iterative research cycles, updating hypothesis status as evidence accumulates
5. **Review** through a three-tier quality chain before surfacing to a human

The output is a structured workplan file that persists across sessions, giving the human operator full visibility into the agent's reasoning at every step.

## When it triggers

Any research or evaluation prompt:
- "Should we build or buy X?"
- "Evaluate whether Y adds enough value to justify the cost"
- "Research whether Z can replace our current tool"
- "How should we respond to [competitor move]?"
- "Is there a viable market for [product concept]?"

## Methodology

### Core principles

**Structure precedes analysis.** Map the problem space before touching a single source. A well-structured MECE (Mutually Exclusive, Collectively Exhaustive) issue tree is worth more than hours of unfocused research.

**Day One Hypothesis.** Formulate a best guess immediately — even with almost no information. Optimize for falsifiability and specificity, not correctness. A wrong-but-specific hypothesis creates a concrete target for research.

**Risk-first prioritization.** Order sub-hypotheses by: which one, if wrong, kills the whole idea fastest? That goes first. The 80/20 principle applies — don't boil the ocean.

**"So what? Who cares? What next?"** Every finding must survive this three-part test before it goes into the workplan.

### Three-tier quality chain

| Tier | Role | Responsibility |
|------|------|----------------|
| 1 | Associate (the agent) | Runs iterative research cycles, maintains workplan |
| 2 | Engagement Manager (adversarial LLM) | Blocking quality gate every 4 cycles — checks MECE integrity, hypothesis falsifiability, priority alignment |
| 3 | Managing Director (human) | Reviews EM-approved workplan — judgment calls only a human can make |

### Workplan output format

Each cycle produces a structured workplan with:
1. Research Task (preserved verbatim)
2. Governing Hypothesis (falsifiable, updated as evidence accumulates)
3. Sub-Hypotheses Table (status, priority, research question, test method, findings)
4. Assumptions (explicit, not buried)
5. Cycle Log (audit trail of what changed and why)
6. Next Steps (specific hypothesis + test method)
7. Blockers for Human Review

## Files

```
workplan/
├── SKILL.md                    — skill instructions (loaded by Claude Code)
├── references/
│   ├── workplan-template.md    — exact output format
│   └── em-review-guide.md      — adversarial EM review checklist
└── learnings.md                — auto-research self-improvement log
```

## Installation

### Claude Code

Copy the `workplan/` directory into your skills directory:

```bash
cp -r workplan/ ~/.claude/skills/workplan/
```

Claude Code will automatically pick up the skill on next session start.

### Claude Cowork / other agents

Load `SKILL.md` into the agent's context and reference the `references/` files as needed. The skill is platform-agnostic — it uses no provider-specific APIs or infrastructure.

## Self-improvement

The skill ships with `learnings.md` — a structured log for accumulating patterns across sessions. After each human (Tier 3) review, feedback is logged here. Every 5 sessions, the accumulated patterns are analyzed and proposed as mutations to `SKILL.md`.

This implements the autoresearch self-improvement pattern: experiment → measure → keep/discard → repeat.

## License

MIT
