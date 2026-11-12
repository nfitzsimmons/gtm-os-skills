---
name: copy-grader
description: Score a piece of marketing copy against a weighted rubric of master-copywriter principles, with a quoted line as evidence for every score, then rewrite it toward 100 without flattening the voice. The copy version of a design critique. Use when the ask is to grade, score, rate, or systematically improve copy against a standard, such as "grade this copy," "score this against Ogilvy," "how good is this landing page copy," "score my LinkedIn post," "build a rubric from Halbert," or "rewrite this to a 95." Grades and lifts existing copy. It does not write from scratch.
---

# Copy Grader

A rubric engine for marketing copy. Design has critique tools that score a page against named principles. This skill does the same for words: score a draft against weighted principles, quote the evidence for every score, then rewrite toward a perfect score. Run the same draft through the same rubric and you get the same number, which is the point. A number you can repeat is a number you can argue with.

Use it on copy worth grading, such as a hero section, a key email, an ad, a pricing page, a cold-outreach opener, or a post you want remembered. Skip it on scratch and quick replies.

## Load context

Before grading, gather only what the scoring needs:
1. **The voice the copy is for.** A brand voice guide, a style guide, or three to five pieces the author is proud of. The rubric scores against that voice, never against a generic ideal. If none is on hand, ask for one or grade voice fidelity as "no baseline" and say so.
2. **The audience and the goal.** Who reads this and what it should make them do. A pricing page and a thought post fail in different ways.
3. **The rubric.** `references/default-rubric.md` unless the format or the user calls for another (see Mode A step 1 and Mode B).

## Three modes

**Mode A, Grade (default).** Score a draft against the rubric and report.
**Mode B, Build a rubric.** Generate a weighted rubric from a named master or domain, save it, then grade with it.
**Mode C, Rewrite toward 100.** Grade, rewrite against the lowest-scoring principles, re-grade, and repeat until the score plateaus or the user stops.

Most requests are A then C: grade, then fix.

## Mode A: Grade a draft

1. **Pick the rubric.** The default is `references/default-rubric.md`, 12 weighted direct-response principles distilled from Ogilvy, Halbert, Sugarman, Hopkins, and Caples. For a **LinkedIn thought or educational post** (or any social post that argues a point without selling), use `references/linkedin-post-rubric.md`. It drops the hard offer and sales CTA principles a thought post can't earn and moves that weight to the hook, the idea, and the proof. For other formats (cold email, pricing page), apply the format weighting notes at the bottom of the default rubric, or build a dedicated rubric (Mode B).
2. **Score each principle 0 to 100.** Every score gets *evidence*: quote the line that earns or loses it. A score with no quoted evidence is a guess, so don't report it. Grade hard. 100 means a master would publish it as is, 70 means competent but unremarkable, and below 50 means the line is working against the goal.
3. **Compute the weighted total.** Weights sum to 100. Weighted total = Σ(score × weight) / 100. Show each principle's points (score × weight / 100) in the Points column and report the total as that column's sum, so anyone can audit the arithmetic.
4. **Output the scorecard:**

```
## Copy Grade: <weighted total>/100

| Principle (weight) | Score | Points | Evidence / why |
|---|---|---|---|
| Hook earns the read (15) | 60 | 9.0 | "We help teams..." opens on the company, not the reader's stake |
| ... | | | |
| **Total** | | **<sum of Points>** | |

### Top 3 fixes (ranked by points recoverable)
1. <principle>: <the specific change that moves it most>
2. ...
3. ...
```

5. **Rank fixes by points recoverable**, which is score gap × weight, so effort goes where it moves the number most. A 40-point miss on a 15-weight principle beats a 10-point miss on a 5-weight one.

## Mode B: Build a rubric from a master or domain

When the user names a copywriter ("score this like Halbert"), a domain ("grade this as a SaaS pricing page"), or wants a custom standard:

1. **Generate 10 to 15 principles** that master or domain is known for. Each gets a one-line name, what it means, a **good example**, a **bad example**, and a **weight**. Weights sum to 100. Weight by how much each principle actually moves outcomes in that domain. The hook and the offer almost always outweigh grammar.
2. **Show the rubric before grading.** A rubric is a judgment call, and the user should get one look at it before it produces numbers.
3. **Save it** as `references/<master-or-domain>-rubric.md`, in the same structure as `default-rubric.md`, so it's reusable, and add it to the rubric list in Mode A step 1.
4. Then grade with it (Mode A).

## Mode C: Rewrite toward 100

1. Grade (Mode A).
2. Rewrite the draft, attacking the principles with the most points recoverable first. Keep the voice. This raises the score *within* the author's voice, never toward generic high-scoring sludge.
3. Re-grade the rewrite. Show before and after scores per principle so the lift is visible.
4. Repeat until the score plateaus (two rounds with under 3 points of gain) or the user is satisfied. Stop chasing 100 past the point of diminishing returns. A 92 in voice beats a 98 that sounds like a machine tuned it.

## Where it fits

- **It grades, it doesn't write.** Bring a draft. If there's no draft yet, write one first.
- **Run it after a judgment pass, not instead of one.** A grader assumes the draft deserves to exist. If you aren't sure there's a real idea in it, check that first (the [taste-check](../taste-check) skill in this pack does exactly that). Polishing a hollow draft to a 90 is still a hollow draft.
- **A high score doesn't mean it reads human.** The rubric scores persuasion. After a Mode C rewrite, do one pass for AI-writing tells (stock phrases, rule-of-three lists, tidy aphorism endings) before it ships.
- **Check the grader against reality.** A model grading a model's copy can learn to please itself. Once you have a dozen graded pieces live, put each score beside how the piece actually performed. If the score doesn't track results, fix the rubric weights before trusting the next number.

## Hard rules

- Never report a score without quoted evidence for it.
- Score against the loaded voice, not a generic ideal. A brand that is deliberately plain doesn't lose points for lacking flair.
- Never add a statistic, customer name, or claim in a rewrite that the original didn't support. A rewrite can sharpen proof, never invent it.
- A rewrite that raises the score by flattening the voice has failed. The voice is the constraint, and the score is the objective.
