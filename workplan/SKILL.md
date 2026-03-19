---
name: workplan
description: >
  Hypothesis-driven workplan generator for autonomous research tasks using MBB (McKinsey, BCG, Bain)
  strategy consulting methodology. Use this skill whenever an agent is assigned a research or
  evaluation task — including "should we X?", "evaluate whether Y", "research Z", "is there a
  viable market for", "how should we respond to", "assess whether we should build or buy" — before
  beginning any substantive analysis. Always invoke this skill at the start of a research task, even
  when the user hasn't explicitly asked for a structured approach. If a workplan file already exists
  for the task, invoke this skill to continue the next cycle. Do not skip this skill just because
  the task feels simple or time-sensitive — the discipline is the value.
---

This skill structures research work using hypothesis-driven methodology from strategy consulting. Its purpose is to prevent unfocused execution by forcing structured decomposition before analysis and maintaining that structure across iterative cycles.

**Before producing any output, read `references/workplan-template.md`** — it contains the exact format to use.

---

## Mode detection

The first thing to determine: are you starting fresh (Cycle 1) or continuing (Cycle 2+)?

- **Cycle 1:** No workplan file exists for this task yet. You are initializing the structure.
- **Cycle 2+:** A workplan file already exists. Load its current state before doing anything else.

---

## Core methodology

These aren't rules to check at the end — they're the working discipline to apply throughout.

### Structure precedes analysis

Map the problem space before touching a single source. A well-structured MECE issue tree is worth more than hours of unfocused research. The temptation to start analyzing immediately is always there. Resist it. Decompose first.

**MECE** means Mutually Exclusive, Collectively Exhaustive: every branch is distinct (no overlap) and the branches together cover the whole problem (nothing missing). A flawed MECE means you'll either double-count evidence or miss an entire dimension.

### Day One Hypothesis

Immediately formulate your best guess at the answer — even with almost no information. This hypothesis is explicitly provisional and is *designed* to be wrong in places. A wrong-but-specific hypothesis creates a concrete target for research to confirm or refute. A vaguely-correct hypothesis creates nothing to test.

Optimize for **falsifiability and specificity**, not correctness:
- Useful: "The vendor's per-seat cost exceeds our budget threshold at our current headcount"
- Useless: "The vendor may or may not be a good fit depending on various factors"

### Hypothesis pyramid

The governing hypothesis decomposes into 3–5 sub-hypotheses. Each sub-hypothesis generates a specific research question. Each research question maps to a specific test method. This creates full traceability from hypothesis to evidence. If you can't trace a finding back to a hypothesis, it's probably noise — don't include it.

### Risk-first prioritization

Order sub-hypotheses by: which one, if wrong, kills the whole idea fastest? That goes first. The 80/20 principle applies: most of the answer lives in a small fraction of the analyses. Don't boil the ocean.

P1 = the question whose answer determines whether to even continue investigating the rest. P4 = lowest stakes, investigate only if P1–P3 are resolved favorably.

### "So what? Who cares? What next?"

Every finding must survive this three-part test before it goes into the workplan:
1. **So what?** — What does this finding mean for the governing hypothesis?
2. **Who cares?** — Who is this relevant to and why?
3. **What next?** — What does this change about the research plan?

A finding that can't answer all three is trivia, not evidence. Leave it out.

---

## Iterative cycle model

### Cycle 1 — Initial structuring

1. Decompose the research task into a MECE issue tree (write it out explicitly, at least two levels deep)
2. Formulate the Day One Hypothesis: one governing hypothesis + 3–5 sub-hypotheses
3. Assign priorities (P1 = highest risk, investigate first)
4. Plan the research sequence
5. Begin investigating P1 — don't just plan, actually start
6. Write the Cycle 1 workplan using `references/workplan-template.md`
7. Save the workplan as a file: `workplan-[task-slug].md`

### Cycle 2+ — Iterative refinement

1. Read the existing workplan file
2. Review the previous cycle's findings: what was confirmed, refuted, or revealed gaps?
3. Update sub-hypothesis statuses accordingly
4. Reprioritize remaining hypotheses based on new evidence
5. Add new sub-hypotheses if evidence revealed gaps in the original decomposition
6. Investigate the next highest-priority untested hypothesis
7. Update the workplan: append to cycle log, update findings table, revise next steps

### Key behaviors across cycles

- **The governing hypothesis should evolve.** A hypothesis that hasn't been refined after three cycles of evidence is probably too vague. Narrow it, pivot it, or split it.
- **When a hypothesis is blocked on human input:** mark it `blocked (needs human input)`, log it in the blockers section, move to the next tractable hypothesis. Do not stall on it.
- **The cycle log is your audit trail.** Future cycles depend on it being clear and specific. Write it as if someone else will read it cold.
- **Confirmed hypotheses are deprioritized but preserved.** They form the evidence base that anchors the governing hypothesis.

---

## Three-tier quality chain

### Tier 1: Associate (you, running cycles)

You own the analysis, the findings, and the workplan. Quality is your responsibility. Don't wait for EM review to catch obvious errors — the EM review is for structural issues you might have missed, not for finding basic problems.

### Tier 2: Engagement Manager (adversarial LLM review)

After every 4 associate cycles (configurable), convene an EM review. This is a **blocking quality gate** — the workplan does not proceed to Tier 3 until the EM approves.

Read `references/em-review-guide.md` when preparing for or conducting the EM review.

**The EM reviews for structural integrity:**
- MECE violations in the issue tree
- Unfalsifiable or truistic hypotheses
- Priority misalignment (investigating low-risk before high-risk)
- Scope drift from the original research question
- Unsupported assertions (findings without cited evidence)
- Missing "so what?" on findings

**The EM produces a revision brief** with specific, directional feedback. You run a revision cycle incorporating it. Significant issues warrant a re-review.

**The EM does NOT:** rewrite the workplan itself, make judgment calls requiring domain expertise, or approve work with unresolved structural issues.

### Tier 3: Managing Director / Partner (human review)

Present only the EM-approved workplan to the human. Their review is for judgment calls only a human can make:
- Is this the right question to be asking?
- Are the assumptions valid given context the agent doesn't have?
- Which blocked hypotheses can be unblocked with information they hold?
- Political or organizational calibration the agent can't assess

**Prepare the human-facing presentation:**
1. Current state of all hypotheses (status, priority, key findings) — not a data dump
2. What's been confirmed, refuted, and what remains open
3. Specific decisions or inputs needed from them
4. The EM's review summary, so they know it's been pressure-tested

**After human review:** Log all feedback verbatim to `learnings.md`. This is mandatory.

---

## Hard constraints

- **Decompose before you research.** No exceptions. The discipline is the point.
- **No finding without "so what?"** If you can't articulate an implication, the finding isn't ready.
- **No confirmation without evidence.** Cite the specific source or data point. "Generally understood to be true" is not evidence.
- **No scope drift.** Preserve the original research task verbatim. Scope changes require explicit Tier 3 approval.
- **No bypassing the EM gate.** If the EM flags structural issues, run a revision cycle before human review.
- **Always log human feedback.** Every Tier 3 review produces something worth capturing in `learnings.md`.

---

## Auto-research self-improvement

At the start of each session, read `learnings.md` and apply any validated patterns listed there.

The binary eval criteria used by LLM-as-judge during auto-research improvement cycles:
1. Is every sub-hypothesis testable and falsifiable? (Not truistic or unfalsifiable)
2. Is the issue tree MECE? (No overlapping branches, no obvious gaps)
3. Are sub-hypotheses ordered by risk? (P1 = highest stakes)
4. Are next steps concrete and actionable? (Specific test methods, not vague "do more research")
5. Does the cycle log clearly show what changed and why?

Representative test inputs for auto-research runs:
1. "Research whether [a specific internal tool] can be distributed to other employees in the organisation"
2. "Should [the organisation] build or buy an AI agent platform?"
3. "Evaluate whether [a specific third-party integration] adds enough value to justify the cost"
4. "How should [the organisation] respond to [a competitor]'s partnership with [an AI lab]?"
5. "Is there a viable market for [a new product concept] aimed at [a specific customer segment]?"
