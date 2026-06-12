---
name: supercomment
description: Use when writing any substantive GitHub comment, issue reply, PR body, or thread post — for humans AND for the agents that will read the thread later. Enough at a glimpse for a skimming human; structured excess underneath, because agents thrive on abundance of evidence, not scarcity.
---

# Supercomment

A supercomment serves two readers at once:

1. **The human at a glimpse.** A self-sufficient TL;DR — verdict, the one load-bearing
   finding, what you want from them. If they read nothing else, they still act correctly.
2. **People and agents who come later.** Collapsible excess: MREs, exact SHAs, command
   output, empirical tables, refuted hypotheses, links to prior context. Costs the skimming
   human nothing (it's folded); feeds every future reader who needs depth — especially
   agents, who grep threads instead of skimming them.

**The core argument: agents thrive in excess of information, not lack.**
- Bug reports that agents can actually resolve score 110%–2700% higher on description
  quality than unresolvable ones; low-quality inputs correlate with rejected agent output
  ([CodeScout, arXiv 2603.05744](https://arxiv.org/pdf/2603.05744)).
- What's written in the thread IS the agent's working substrate: in SWE-bench, ~33% of
  "resolved" issues contained the solution in the issue text itself
  ([SWE-bench+, arXiv 2410.06992](https://arxiv.org/pdf/2410.06992)) — and OpenAI had to
  human-filter underspecified issues as unsolvable to build
  [SWE-bench Verified](https://openai.com/index/introducing-swe-bench-verified/).
- The honest caveat that shapes the format: excess **instructions** hurt (agents
  over-obey irrelevant directives — [ETH Zurich on bloated AGENTS.md](https://www.marktechpost.com/2026/02/25/new-eth-zurich-study-proves-your-ai-coding-agents-are-failing-because-your-agents-md-files-are-too-detailed/));
  excess **evidence** helps. A supercomment's `<details>` carry facts, repros, and
  outcomes — never standing instructions. Same shape as progressive disclosure in
  [SWE-Bench Pro](https://arxiv.org/pdf/2509.16941)'s problem-statement + requirements split.

**Origin:** distilled from operator memory files + one heavy maintainer day (NiceGUI,
2026-06-12) that earned, unprompted: *"Rather short and to the point, with optional details
to expand on demand."*

## Structure (top to bottom)

1. **Disclosure line** (if agent-authored, policy-dependent): top-line italic, e.g.
   *"Posted by Claude Code on \<operator\>'s behalf."* Never a buried footer.
2. **TL;DR block.** Bold-prefixed (`**TL;DR:**`). Verdict first, then the ONE
   load-bearing finding, then the ask — self-sufficient. Optimise it to be *scanned*,
   not read: put the bold verdict label on its own line, then break the rest across short
   paragraphs separated by blank lines. When the reasoning has 2+ discrete parts, render
   them as a real markdown list (`1.` / `-`), never inline `(1)… (2)…` — inline enumeration
   buried in a long sentence is the wall-of-text that defeats the glimpse reader. A skimming
   human should catch the verdict and the shape of the argument without reading one full
   sentence.
3. **`<details>` blocks, one per topic**, each `<summary><b>…</b></summary>` standing
   alone. The evidence layer: empirical tables, MRE code, file:line refs, exact commit
   SHAs, what-was-run. Order: confirmed findings → refuted hypotheses → nits → hedged ideas.
   Refuted hypotheses are first-class content — ruling things out is signal, and it saves
   the next reader (or agent) from re-walking the dead end.
4. **Explicit ask or enumerated options** ("three options we see: leave / cover / warn"),
   not "thoughts?".

## Claim discipline (what earns the trust)

- **Verified vs. hedged, visibly separated.** "Confirmed (ran it): …" vs "untested unless
  noted". Never let an unverified claim wear a verified claim's clothes.
- **Evidence is empirical, not rhetorical.** Before/after tables from running both branches
  beat prose. Include SHAs and commands — that's what makes the comment replayable by an
  agent later.
- **Process transparency:** if a finding came from another tool/conversation, link it and
  say what was independently re-verified (and what got refuted on the way).
- **Correct yourself in public**, in-thread, plainly — the audit trail is part of the excess.
- **Credit the counterpart** specifically when they catch your miss or improve your sketch.

## Stock shapes (pick the closest; the structure flexes per shape)

- **Review verdict** (approve / request changes): TL;DR = verdict + load-bearing finding +
  merge-or-fix ask; details = verification evidence, refuted hypotheses, nits.
- **Status note / hold:** 2–3 sentences, no details blocks — say what's pending and when
  the follow-up lands ("MRE in progress; please hold merging").
- **Proposal to a counterpart:** TL;DR = the direction + the one correction or trade-off
  they must see; details = implementation, empirical table; end with "does this match your
  intent?" or enumerated options.
- **Answering questions in-thread:** one details block per question, each independently
  citable (file:line); TL;DR says which questions are settled vs open.

## Editing posted comments

Append a `Changelog` footer: date + one line per edit. Silent edits break the thread's
value as a record.

## Anti-patterns

- Verdict in paragraph four; `<details>` hiding the verdict itself.
- Instructions smuggled into the evidence layer ("future agents should always …") — that's
  the bloat failure mode, not the abundance virtue.
- Hedging everything (no spine) or nothing (bluffing).
- "Great PR! Just a few nits…" padding. Start at the TL;DR.
- Trimming the MRE/SHAs "for brevity" — brevity belongs to the TL;DR layer only.
- **A TL;DR that's one dense block.** Verdict label glued to the front of a 6-sentence
  run-on, multi-part reasoning crammed inline as `(1)… (2)…`. It's all *there*, but the
  glimpse reader can't skim it — the verdict and the argument's shape must survive a
  half-second scan. Label on its own line; discrete reasons as a list.
