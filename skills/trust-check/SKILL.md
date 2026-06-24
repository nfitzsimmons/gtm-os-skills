---
name: trust-check
description: Make an AI answer auditable instead of just plausible. Use on any task where a wrong answer carries cost — extracting figures from a document, pulling data across files, synthesizing research, answering a question you'll act on or forward. Triggers on "can I trust this," "verify this," "give me receipts," "double-check this," "is this right," "make this auditable," or before you act on an extracted number, quote, or claim. Bundles three behaviors from how Anthropic's own team keeps AI honest: disambiguate the ask before running it, cite a source for every claim, and get a fresh second opinion on high-stakes output. Skip it for low-stakes chat where being wrong costs nothing.
trigger: User asks to verify, trust, double-check, or get receipts on an AI answer, or is extracting/synthesizing information they will act on or forward.
---

# Skill: Trust Check

## The shift

The wrong question is "is the AI right?" You can't answer that by staring at a fluent paragraph. The right question is "how much can I trust this, and what would make it auditable?" Trust is something you engineer into the process, not a property you hope the model has.

Wrong answers come from three places: the model guessed what an ambiguous word meant, it pulled stale or wrong-source information, or it inferred something and presented the guess as fact. The three behaviors below close each gap. Apply them when a wrong answer would actually cost something. For low-stakes chat, skip this entirely — overhead with no payoff.

## Behavior 1: Disambiguate before you execute

Before running a request that involves judgment words, find the terms whose interpretation would change the result, and state the reading you're using. "Top customers" could mean highest spend, most recent, most orders, or biggest brand. If the model silently picks one, a confident wrong answer follows.

Run this check before producing the answer:

> Before you answer, scan my request for any word or phrase that could be interpreted more than one way and would change the result. List each one, state how you're interpreting it, and ask me to confirm only the ones where the wrong reading would meaningfully change the output.

When the right interpretation is settled, write it into the project instructions or the skill so you never re-litigate it. "Top means highest revenue in the last 12 months" belongs in the system prompt, not in your head.

## Behavior 2: Receipts on every claim

Any time the answer extracts or synthesizes information, make it cite where each piece came from and flag what it didn't actually find. The format:

> For every claim you give me, tell me which file and which part of it (page, section, sheet, or tab) the claim came from. If a claim is your own inference rather than something stated in the source, mark it INFERRED. End with the single thing most worth double-checking, and where to check it.

Two things make this work. The model often self-corrects mid-stream once it has to attribute a claim, so the answer gets better before you even read it. And the INFERRED flags plus the one-thing-to-check line tell you exactly where to spend your audit time, instead of re-reading everything.

A receipt looks like:

```
Claim: Q3 revenue was $4.2M
Source: 2025-q3-financials.pdf, page 3, "Summary" table

Claim: growth was driven mostly by the enterprise segment
Source: INFERRED — the deck shows enterprise up 40% but doesn't
        attribute total growth to it

Double-check first: the enterprise-growth attribution. Confirm
against the segment breakdown on slide 11.
```

## Behavior 3: Second opinion for high-stakes

When the stakes are real — money, legal or compliance exposure, brand or reputation, or a task you're about to automate end to end — don't trust a single pass. Get the work judged.

- **Fresh context, same model.** Start a clean chat or session and paste only the output. Ask: "Challenge this. Tell me what's wrong, what's weak, and what's missing." In the original chat the model defends its own work; with no memory of having written it, it critiques honestly.
- **Different model.** Hand the output to a second model and ask it to review. If both agree, your confidence goes up. If they disagree, they've handed you the exact spot that needs your human judgment.

Make the judge adversarial, not agreeable. "Is this good?" gets you a yes. "What's the strongest case that this is wrong?" gets you the failure mode.

## Before you automate something end to end

If you're removing yourself from the loop, build an answer key first. Take ten real cases you've already done by hand, where you know the right output. Run the AI on the same ten and score it. Ten out of ten, automate with confidence. Seven to nine, fix the input first — the prompt, the context you're feeding it, the model tier — before giving up. Below seven, set the case aside with its ten samples and re-run the test when a stronger model ships. Capability arrives on a schedule, and the answer key is how you notice.

## What this is and isn't

This is a discipline you apply to a normal chat, not a tool you install and forget. It costs a little overhead per task and earns it back the first time it catches a confident wrong answer before you forwarded it to your board. Use judgment about when the stakes justify it.

The approach is adapted from Anthropic's published account of how their own team keeps AI honest when nearly every internal data question runs through it. Original write-up: search "Anthropic" for their post on improving data-retrieval accuracy.
