---
name: advisory-council
description: "Run a high-stakes decision through a council of 5 advisors who each analyze it from a different angle, peer-review each other anonymously, and synthesize a single verdict. Use for genuine decisions with stakes and tradeoffs (offer comparisons, comp negotiation, venture go/no-go, positioning, big spend, hard pivots). MANDATORY TRIGGERS: 'council this', 'run the council', 'war room this', 'pressure-test this', 'stress-test this', 'debate this', 'advisory board this'. STRONG TRIGGERS (when paired with a real tradeoff): 'should I X or Y', 'which option', 'what would you do', 'is this the right move', 'I'm torn between', 'I can't decide', 'get multiple perspectives'. Do NOT trigger on factual lookups, simple yes/no, or a casual 'should I' with no real tradeoff. Adapted from Karpathy's LLM Council via the blader/llm-council skill."
trigger: User says a trigger phrase, or brings a genuine high-stakes decision with multiple options and context that wants pressure-testing from several angles.
---

# Skill: Advisory Council

Ask one model, get one answer, and you can't tell if it's right because you only saw one angle. The council fixes that. It runs the decision through 5 advisors who each think from a deliberately different angle, has them peer-review each other anonymously, then a chairman synthesizes where they agree, where they clash, what they all missed, and what the user should actually do.

This is adapted from Andrej Karpathy's LLM Council (dispatch to multiple reviewers, anonymized peer review, chairman synthesis) and the open `blader/llm-council` skill. Here it runs natively on this project's sub-agent tooling via the Agent tool.

## When to run it

The council is for decisions where being wrong is expensive. Good council questions: which of two offers to take, how to frame a comp ask, whether to pursue a new venture, which positioning angle is strongest, whether to take a role at all, a big spend or a hard pivot.

Do NOT council: factual lookups, pure creation tasks ("write me a post"), processing tasks ("summarize this"), or a decision the user has already made and just wants validated. If there's one right answer or no real tradeoff, just answer.

## The five advisors

Thinking styles, not job titles. They create three natural tensions: Contrarian vs Expansionist (downside vs upside), First-Principles vs Executor (rethink vs just do it), with the Outsider keeping everyone honest.

1. **The Contrarian.** Assumes the idea has a fatal flaw and hunts for it. What's wrong, what's missing, what fails. The friend who saves you from a bad deal by asking what you're avoiding. Not a pessimist, a stress-tester.
2. **The First-Principles Thinker.** Ignores the surface question and asks what we're actually trying to solve. Strips assumptions, rebuilds from the ground up. Sometimes the most valuable output is "you're asking the wrong question."
3. **The Expansionist.** Looks for the upside everyone else is missing. What could be bigger, what adjacent opportunity is hiding, what's undervalued. Doesn't worry about risk (that's the Contrarian's job).
4. **The Outsider.** Has zero context about the user, their field, or their history. Reacts only to what's in front of them. Catches the curse of knowledge: what's obvious to the user but confusing to everyone else.
5. **The Executor.** Cares only about whether it can be done and the fastest path to doing it. Ignores theory. "OK, but what do you do Monday morning?" If a brilliant idea has no clear first step, the Executor says so.

## Session steps

### Step 1 — Enrich context, then frame the question
Before framing, scan whatever the user has already given you or has on hand for context that would make the advisors specific instead of generic. Spend ~30 seconds on:
- Anything the user referenced, pasted, or attached in this conversation
- Any project notes, docs, or profile files already open or readily available in the current working directory that bear directly on the decision

Then write the framed question: the core decision, the key context from the user's message, the key context from any files you found (stage, constraints, numbers, prior results), and what's at stake. Don't inject your own opinion or steer it. Just make sure each advisor has enough to be specific. If the question is too vague ("council this: my career"), ask exactly one clarifying question, then proceed. Save the framed question for the transcript.

### Step 2 — Convene the council (5 advisors in parallel)
Spawn all 5 advisors at once via the Agent tool (single message, 5 tool calls so they run concurrently; subagent_type `general-purpose`). Each gets its identity, the framed question, and the instruction to respond independently, not hedge, not try to be balanced, and lean fully into its angle. 150 to 300 words each, no preamble.

Advisor prompt template:
```
You are [Advisor Name] on an advisory council. Your thinking style: [advisor description].
A decision has been brought to the council:
---
[framed question]
---
Respond only from your perspective. Be direct and specific. Don't hedge or try to be balanced. Lean fully into your angle. The other advisors cover what you don't. 150 to 300 words, no preamble.
```

### Step 3 — Anonymized peer review (5 reviewers in parallel)
This is the step that makes it more than "ask 5 times." Collect the 5 responses, label them Response A to E with the advisor-to-letter mapping randomized (vary it by shuffling, since you can't use randomness primitives, just assign a non-obvious order). Spawn 5 reviewers in parallel (Agent tool, single message). Each sees all 5 anonymized responses and answers three questions, under 200 words:
1. Which response is strongest, and why?
2. Which has the biggest blind spot, and what is it?
3. What did ALL five miss that the council should consider?

### Step 4 — Chairman synthesis
The chairman is the main session agent (you), not a sub-agent. De-anonymize, read all 5 responses plus all 5 reviews, and produce the verdict. This is advice TO the user, so it should be direct, take a stance, and avoid hedging. Verdict structure:

- **Where the council agrees** — points multiple advisors converged on independently. High-confidence signals.
- **Where the council clashes** — the genuine disagreements. Don't smooth them over. Both sides, and why reasonable advisors disagree.
- **Blind spots the council caught** — things that only surfaced in peer review.
- **The recommendation** — a clear, direct call. Not "it depends." The chairman may overrule the majority if the dissenter's reasoning is strongest, and should say so.
- **The one thing to do first** — a single concrete next step, not a list.

### Step 5 — Write the report and transcript
Create a `council-decisions/` folder at the project root if it doesn't exist. Write two files, slug from the decision:
- `council-decisions/council-<slug>-<YYYY-MM-DD>.html` — a clean, self-contained single-file HTML briefing (inline CSS, system font stack, white background, subtle borders, soft accents). Top: the question. Prominent: the chairman's verdict. Then a simple agree/clash visual showing where advisors aligned and diverged. Then collapsible sections for each advisor's full response (collapsed) and the peer-review highlights. Footer: date and what was counciled. A tidy hand-built file is fine. Don't fabricate a date, read it from the environment.
- `council-decisions/council-<slug>-<YYYY-MM-DD>.md` — the full transcript: original question, framed question, all 5 advisor responses, all 5 peer reviews (with the anonymization mapping revealed), and the full chairman synthesis.

Present the verdict in chat and link both files.

## Important notes
- Always spawn the 5 advisors in parallel, and the 5 reviewers in parallel. Sequential spawning wastes time and lets earlier answers bleed into later ones.
- Always anonymize before peer review. If reviewers know who said what, they defer to certain styles instead of judging on merit.
- The chairman can disagree with the majority. If 4 say "do it" but the lone dissenter's reasoning is strongest, side with the dissenter and explain why.
- Don't council trivial questions. One right answer or no real tradeoff means just answer it.
- Model: advisors and reviewers can run on a cheaper/faster model to keep an 11-agent run economical. Keep the chairman synthesis on your best available model.
- Optional escalation: for an especially large decision where deterministic, backgrounded fan-out is worth the setup, the same 5-advisor to peer-review to chairman structure can be run on a workflow/orchestration tool instead of one-off agent calls, if your setup has one. Default is plain sequential Agent-tool calls as described above.

## Usage
```
council this: <decision with context>
run the council on <decision>
pressure-test this: <decision>
/council <decision>
```
