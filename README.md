# supercomment

**Every GitHub thread now has two readers: the human skimming it, and the agent that will
grep it at 3am eight months from now. A supercomment feeds both without wasting either's time.**

The shape:

```
*Disclosure line (if agent-authored)*

**TL;DR:** verdict → the one load-bearing finding → what you want from the reader.
Self-sufficient. The skimming maintainer stops here and still acts correctly.

▸ <details> Confirmed: the empirical table, the MRE, exact SHAs, what was run
▸ <details> Refuted: the hypotheses that died, so nobody re-walks the dead end
▸ <details> Hedged: ideas marked untested, wearing their uncertainty visibly

Explicit ask: "three options we see — leave / cover / warn. Which do you prefer?"
```

Folded blocks cost the skimming human nothing. But agents don't skim — they grep, and they
resolve issues at rates that track how much evidence the thread carries: bug reports agents
can actually fix score **110–2700% higher on description quality** than ones they can't
([CodeScout](https://arxiv.org/pdf/2603.05744)); in SWE-bench, **~33% of "resolved" issues
had the solution sitting in the thread text** ([SWE-bench+](https://arxiv.org/pdf/2410.06992));
OpenAI had to hand-filter underspecified issues just to make the benchmark solvable
([SWE-bench Verified](https://openai.com/index/introducing-swe-bench-verified/)).

**The thread is the agent's working substrate. Starve it and you starve every future run.**

One honest caveat shapes the whole format: excess *evidence* helps agents; excess
*instructions* poisons them ([ETH Zurich on bloated AGENTS.md](https://www.marktechpost.com/2026/02/25/new-eth-zurich-study-proves-your-ai-coding-agents-are-failing-because-your-agents-md-files-are-too-detailed/)).
So the `<details>` carry facts, repros, and outcomes — never standing directives.

## Receipts

Distilled from one heavy maintainer day (NiceGUI, 2026-06-12: a request-changes with a
confirmed footgun, approvals with verification tables, a comment carrying a formal
dead-code proof) which earned, unprompted, from the receiving maintainer:

> I like your (agent's) review comments today. Rather short and to the point, with
> optional details to expand on demand 👍

That quote is the spec. The skill is just the spec written down.

## Status: brick (拋磚引玉)

Deliberately rough, thrown to attract refinement — see the
[chengyu-throw-brick-attract-jade skill](https://github.com/evnchn-agentic/chengyu-skills/tree/main/chengyu-throw-brick-attract-jade)
for why the roughness is the feature, not an apology. Intended to be shareable once polished.

## Known gaps (bait — refine me)

- Cutoff calibration: when is a comment too small to deserve the apparatus? (One-line +1s
  obviously exempt; where's the line?)
- No worked examples embedded yet; origin-day threads worth mining into references/: a
  request-changes with confirmed-footgun + refuted-mitigation, an approval with
  verification table, a comment-not-approval carrying a formal proof.
- When to use formal review states (Request Changes vs comment-only) is implied, not specified.
- Disclosure/changelog sections are one operator's policy; team-adoptable phrasing TBD.
