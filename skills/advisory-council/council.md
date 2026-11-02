Invoke the `advisory-council` skill to run a high-stakes decision through 5 advisors, anonymized peer review, and a chairman synthesis with a decision record.

The argument is the decision to council (with whatever context the user gives). If no argument is provided, ask for the decision and any relevant context, then proceed. If the user names a roster (buyer, practitioners, interviewer) or asks to retro a past decision, follow that section of the skill.

Run the skill end to end:
1. Enrich context from whatever the user has already shared plus any directly relevant files on hand, then frame the question neutrally, with "do nothing" as an option and the door type called.
2. Spawn 5 advisors in parallel (Agent tool), then 5 anonymized peer reviewers in parallel.
3. Synthesize the chairman verdict in a direct, no-hedging voice (agree / clash / blind spots / recommendation / one thing to do first / decision record).
4. Write the HTML briefing and the markdown transcript to `council-decisions/`, and present the verdict.

Don't council trivial questions, factual lookups, or decisions already made. If there's no real tradeoff, just answer.
