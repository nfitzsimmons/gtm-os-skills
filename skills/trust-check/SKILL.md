---
name: trust-check
description: Make an AI answer auditable instead of just plausible. Use on any task where a wrong answer carries cost, such as extracting figures from a document, pulling data across files, synthesizing research, or answering a question you'll act on or forward. Triggers on "can I trust this," "verify this," "give me receipts," "double-check this," "is this right," "make this auditable," or before you act on an extracted number, quote, or claim. Bundles three behaviors from how Anthropic's own team keeps AI honest. Disambiguate the ask before running it, cite a source for every claim, and get a fresh second opinion on high-stakes output. Skip it for low-stakes chat where being wrong costs nothing.
trigger: User asks to verify, trust, double-check, or get receipts on an AI answer, or is extracting/synthesizing information they will act on or forward.
---

# Skill: Trust Check

## The shift

The wrong question is "is the AI right?" You can't answer that by staring at a fluent paragraph. The right question is "how much can I trust this, and what would make it auditable?" Trust is something you engineer into the process, not a property you hope the model has.

Wrong answers come from three places. The model guessed what an ambiguous word meant, it pulled stale or wrong-source information, or it inferred something and presented the guess as fact. The three behaviors below close each gap. Apply them when a wrong answer would actually cost something. For low-stakes chat, skip this entirely, because it's overhead with no payoff.

## Behavior 1: Disambiguate before you execute

Before running a request that involves judgment words, find the terms whose interpretation would change the result, and state the reading you're using. "Top customers" could mean highest spend, most recent, most orders, or biggest brand. If the model silently picks one, a confident wrong answer follows.

Run this check before producing the answer:

> Before you answer, scan my request for any word or phrase that could be interpreted more than one way and would change the result. List each one, state how you're interpreting it, and ask me to confirm only the ones where the wrong reading would meaningfully change the output.

When the right interpretation is settled, write it into the project instructions or the skill so you never re-litigate it. "Top means highest revenue in the last 12 months" belongs in the system prompt, not in your head.

## Behavior 2: Receipts on every claim

Any time the answer extracts or synthesizes information, make it cite where each piece came from and flag what it didn't actually find. The format:

> For every claim you give me, tell me which file and which part of it (page, section, sheet, or tab) the claim came from. Tag each claim SOURCED, INFERRED, or UNVERIFIED. End with the single thing most worth double-checking, and where to check it.

Two things make this work. The model often self-corrects mid-stream once it has to attribute a claim, so the answer gets better before you even read it. And the status tags plus the one-thing-to-check line tell you exactly where to spend your audit time, instead of re-reading everything.

A receipt looks like:

```
Claim: Q3 revenue was $4.2M
Status: SOURCED
Source: 2025-q3-financials.pdf, page 3, "Summary" table

Claim: growth was driven mostly by the enterprise segment
Status: INFERRED. The deck shows enterprise up 40% but doesn't
        attribute total growth to it

Double-check first: the enterprise-growth attribution. Confirm
against the segment breakdown on slide 11.
```

### The three statuses

- **SOURCED.** A source you can name states it.
- **INFERRED.** It's the model's own reasoning, not a stated fact.
- **UNVERIFIED.** It's a factual assertion that no reachable source supports.

Tag coverage too. `checked` means a source was available to test the claim against. `no-source-available` means none was. An UNVERIFIED claim with no source available is a different problem from one a source contradicts.

### Two traps that pass for receipts

**A description of a live thing is not the live thing.** A claim about the present state of a web page, a shipped feature, a dashboard, or a CRM record is receipted only by that surface, fetched in this run. An internal doc that describes the page does not cover it. Until the surface itself is checked, the claim is INFERRED at best.

**A source existing is not the same as the claim being sound.** For any market-sizing or share claim ("X million companies," "Y% of buyers"), run the denominator test before tagging it SOURCED. Divide the claim by the total population it is drawn from, using the definition the claim states. If the implied share is implausible for that definition, the claim is unsound even though a source states it. Tag it UNVERIFIED, note "fails denominator test," and replace it with a claim the base supports, or cut it. Example: "two-thirds of US households hold $100k+ in investable assets" only holds if "investable" quietly includes home equity and retirement accounts. The source exists. The claim as worded is still wrong. *(The denominator test is adapted from matteotitta/genesys-skills, MIT.)*

## Behavior 3: Second opinion for high-stakes

When the stakes are real (money, legal or compliance exposure, brand or reputation, or a task you're about to automate end to end), don't trust a single pass. Get the work judged.

- **Fresh context, same model.** Start a clean chat or session and paste only the output. Ask: "Challenge this. Tell me what's wrong, what's weak, and what's missing." In the original chat the model defends its own work. With no memory of having written it, it critiques honestly.
- **Different model.** Hand the output to a second model and ask it to review. If both agree, your confidence goes up. If they disagree, they've handed you the exact spot that needs your human judgment.

Make the judge adversarial, not agreeable. "Is this good?" gets you a yes. "What's the strongest case that this is wrong?" gets you the failure mode.

### The reviewer's output contract

Whichever judge you use, ask it to return a verdict in this shape, then check the verdict against its own findings before trusting it.

- **Verdict** is one of APPROVED, REVISE, or BLOCKED.
- **Findings** each carry a severity (high, medium, low), the exact spot, and why it's wrong.
- **Coverage** lists what the reviewer actually checked (claims, figures, sections, files).
- **Consistency rules.** APPROVED cannot carry a high or medium finding. REVISE must name at least one concrete finding. Every verdict lists its coverage. There is no finding quota, so a clean APPROVED with real coverage is a valid answer.

A verdict that breaks a consistency rule is a failed review, not a pass. Re-run it or escalate. An APPROVED with no coverage list, or one that waves through its own medium finding, is a check that computed a result and then printed a verdict that ignores it. *(The contract is adapted from the review validator in chaseai-yt/claudex-loop, MIT.)*

## Before you automate something end to end

If you're removing yourself from the loop, build an answer key first. Take ten real cases you've already done by hand, where you know the right output. Run the AI on the same ten and score it. Ten out of ten, automate with confidence. Seven to nine, fix the input first (the prompt, the context you're feeding it, the model tier) before giving up. Below seven, set the case aside with its ten samples and re-run the test when a stronger model ships. Capability arrives on a schedule, and the answer key is how you notice.

## What this is and isn't

This is a discipline you apply to a normal chat, not a tool you install and forget. It costs a little overhead per task and earns it back the first time it catches a confident wrong answer before you forward it to your board. Use judgment about when the stakes justify it.

The approach is adapted from Anthropic's published account of how their own team keeps AI honest when nearly every internal data question runs through it: https://claude.com/blog/how-anthropic-enables-self-service-data-analytics-with-claude
