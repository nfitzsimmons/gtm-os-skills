# Buyer roster: prompt templates and verdict shape

Loaded by SKILL.md when `roster: buyer` is selected. The seats live in a personas file the user supplies. This file holds only the machinery.

## Write your personas file first

The skill does not improvise buyers. Create a `personas.md` with one block per seat, written by people who talk to customers. Each seat block carries:

- seat name and title band
- deal role (economic buyer, champion, technical evaluator, blocker)
- what they're measured on
- the question they cannot answer today
- vocabulary that lands, and vocabulary that reads as vendor
- standing objections
- what they would forward, and what they bounce on
- a regulatory or regional variant, if any
- confidence (from real interviews, or a draft guess)

Add a line naming the default bench of five, in order. Mark any seat that is still a guess as DRAFT.

## Seat loading

1. Read the personas file the user names. If it's missing, stop and say so. If the user named seats that aren't in the file, list the ones that exist and ask which to use.
2. The default bench is the file's default line. The user can name seats and the skill fills to five from the default order. A seat flagged DRAFT stays out until a human lifts the flag. A non-ICP control seat is opt-in, or added when the question is "who is this copy actually for."
3. Pull the artifact under review verbatim. If it's a live doc or deck, re-pull it at the start of every round, because people edit between rounds.
4. Paste each seat block into the advisor prompt with every source citation stripped (file names, interview IDs, account names). Seats that see citations leak them into their reactions.

## Advisor prompt (one per seat)

```
You are a real buying persona at [company]'s ideal customer profile: [seat name].
Your seat, verbatim from the persona file:
---
[full seat block]
---
You are sitting in the meeting where this is presented, or you are the person it has to survive after the meeting when a colleague forwards it to you. React from your seat, your incentives, and your calendar. You are not a marketing reviewer and you are not being asked to be balanced. Lean fully into your seat, the other members cover what you do not.

What you are reacting to:
---
[artifact, verbatim, plus the specific question asked]
---

Return, in this order, no preamble, 300 to 600 words:
1. What makes you want the next slide or paragraph, and where you stop reading.
2. What is unearned or unbelievable from your seat, sentence by sentence where it matters.
3. What you would ask out loud in the room after seeing it.
4. The one thing that would have to be true before you take a second meeting.
[If options or a title slate exist:] 5. Score each option 1 to 10 on Buying resonance (do you want the next slide), Credibility (a company that solved this, or one selling at you), and Originality (could a competitor put their logo on it unchanged? Safe and interchangeable scores low here even if it scores well elsewhere). Give numbers, then your single top pick, your single kill, and the line you would write instead.

Ground every reaction in your seat block. If you find yourself inventing a pain, an objection, or a fact that is not in the block or the artifact, say "outside my brief" and move on. Speak only as the buyer. Never mention the persona file, other councils, or other responses.
```

## Peer review prompt (one per reviewer, five in parallel)

Anonymize A to E with a non-obvious mapping. Give each reviewer the five seat blocks and the artifact alongside the responses, so it can check what each seat invented. Open with: "each response reveals its own seat through its content, so judge the reasoning rather than the role." Under 200 words each:

1. Which response is most faithful to a real buyer in that seat, and why?
2. Which response invented pain, objections, or facts not grounded in the persona file or the artifact? Quote the line.
3. Which response has the biggest blind spot for its own seat?
4. What did all five miss that the buyer in the room would raise?

Question 2 is the guard this roster adds. Role-play drifts toward plausible invention, and the chairman needs it flagged before it reaches the verdict.

## Chairman verdict shape (buyer roster)

Open by stating the seats were synthetic and which persona file they came from.

- **Who it lands with.** Seats that wanted the next slide, and the specific line that did it.
- **Who bounces, and why.** Seats that stopped reading, where, and whether that seat is one the artifact needed.
- **What every seat rejected.** Lines or claims no buyer believed. High-confidence cuts.
- **Invented pain, struck.** Anything peer review flagged as outside the persona brief, excluded from the verdict and named so the user knows it was excluded.
- **The fix.** One direct call on what the artifact should do differently. The chairman may side with a lone seat if that seat is the one who signs.
- **The one thing to change first.** A single concrete edit.

Slug the output files `buyer-<slug>-<date>`. The transcript records the persona file path so a later reader knows how synthetic the seats were.

## Where this sits

Run it before you polish copy, not after. The buyer council judges framing (does the buyer want the next slide) and hands back cuts and a fix. Never let a buyer-council verdict stand in for a real customer conversation, and never quote a synthetic seat as if it were voice of customer.
