---
name: advisory-council
description: "Run a high-stakes decision through 5 advisors who each take a different angle, peer-review each other anonymously, and produce one verdict plus a decision record you can score later. Use for real decisions with stakes and tradeoffs (offers, comp, venture go/no-go, positioning, big spend, hard pivots). Alternate rosters: buyer (your own personas, does an artifact land), practitioners (five marketing schools of thought), interviewer (rehearse against an interview panel), and retro mode (score a past council against what happened). MANDATORY TRIGGERS: council this, run the council, war room this, pressure-test this, stress-test this, retro this decision. STRONG TRIGGERS with a real tradeoff: should I X or Y, which option, I am torn between, I cannot decide. Not for factual lookups, simple yes/no, or a casual should-I with no tradeoff. Adapted from Karpathy's LLM Council via blader/llm-council."
trigger: User says a trigger phrase, or brings a genuine high-stakes decision with multiple options and context that wants pressure-testing from several angles.
---

# Skill: Advisory Council

Ask one model, get one answer, and you can't tell if it's right because you only saw one angle. The council fixes that. It runs the decision through 5 advisors who each think from a deliberately different angle, has them peer-review each other anonymously, then a chairman synthesizes where they agree, where they clash, what they all missed, and what the user should actually do. It also writes down what success and failure would look like before the decision is made, so you can score the call later instead of grading it with hindsight.

This is adapted from Andrej Karpathy's LLM Council (dispatch to multiple reviewers, anonymized peer review, chairman synthesis) and the open `blader/llm-council` skill. Here it runs natively on sub-agent tooling via the Agent tool.

## When to run it

The council is for decisions where being wrong is expensive. Good council questions: which of two offers to take, how to frame a comp ask, whether to pursue a new venture, which positioning angle is strongest, whether to take a role at all, a big spend or a hard pivot.

Do NOT council: factual lookups, pure creation tasks ("write me a post"), processing tasks ("summarize this"), or a decision the user has already made and just wants validated. If there's one right answer or no real tradeoff, just answer.

## The five advisors

Thinking styles, not job titles. They create three natural tensions. Contrarian vs Expansionist (downside vs upside), First-Principles vs Executor (rethink vs just do it), with the Outsider keeping everyone honest.

1. **The Contrarian.** Assumes the idea has a fatal flaw and hunts for it. What's wrong, what's missing, what fails. The friend who saves you from a bad deal by asking what you're avoiding. Not a pessimist, a stress-tester.
2. **The First-Principles Thinker.** Ignores the surface question and asks what we're actually trying to solve. Strips assumptions, rebuilds from the ground up. Sometimes the most valuable output is "you're asking the wrong question."
3. **The Expansionist.** Looks for the upside everyone else is missing. What could be bigger, what adjacent opportunity is hiding, what's undervalued. Doesn't worry about risk (that's the Contrarian's job).
4. **The Outsider.** Has zero context about the user, their field, or their history. Reacts only to what's in front of them. Catches the curse of knowledge, meaning what's obvious to the user but confusing to everyone else. Weight its findings heavily when they are internal contradictions. The four context-rich advisors are structurally unable to see those, because they silently fill the gap with what they already know.
5. **The Executor.** Cares only about whether it can be done and the fastest path to doing it. Ignores theory. "OK, but what do you do Monday morning?" If a brilliant idea has no clear first step, the Executor says so.

## Rosters

Four benches share the same peer-review and chairman machinery. Pick by what is under review.

- **`advisors` (default).** The five thinking styles above. For a decision the user owns, such as an offer, a spend, a pivot, or a positioning call.
- **`buyer`.** Five buyer-persona seats loaded from a personas file the user supplies. For an artifact aimed at a buyer where the question is "will this land," such as a deck, a post, a page, an email, or a title slate. Load `references/buyer-roster.md` and follow it in place of the advisor template, review questions, and verdict below.
- **`practitioners`.** Five marketing schools of thought (positioning, brand science, behavioral economics, direct response, writing craft), always with one designated dissenter. For a marketing-leadership call where a named lens adds something. Load `references/practitioner-roster.md`.
- **`interviewer`.** Up to five seats simulating the people in an interview loop, built from public material the user points at. Use it to rehearse a 90-day plan, a take-home readout, or a hard answer before the round. Load `references/interviewer-roster.md`.

The user can force any roster or name seats ("CISO, CFO, and CTO only"). The skill never invents a seat. If the personas file is missing or a named seat isn't in it, stop and say so. The tool cannot define your buyers. Humans have to.

## Session steps

### Step 1: Enrich context, then frame the question
Before framing, scan whatever the user has already given you or has on hand for context that would make the advisors specific instead of generic. Spend about 30 seconds on:
- Anything the user referenced, pasted, or attached in this conversation
- Any project notes, docs, or profile files already open or readily available in the current working directory that bear directly on the decision

**Adjacent artifacts are mandatory context when the decision is one piece of a multi-piece launch.** If the thing being counciled ships alongside, or days from, another public artifact (a companion blog post, a same-day announcement, a sibling landing page, a colleague's post on the same news), pull that artifact's actual text into the framed question. Advisors reasoning without it will manufacture a clash that the other document already settled.

Then write the framed question. Include the core decision, the key context from the user's message and files (stage, constraints, numbers, prior results), any adjacent artifacts shipping near it, and what's at stake. Always list the options explicitly, with **do nothing** (or "wait") as one of them, since every decision needs a counterfactual. Also call the **door type**. A one-way door is hard to reverse (signing an offer, a public launch). A two-way door is cheap to undo (a test, a draft). Don't inject your own opinion or steer it. If the question is too vague ("council this: my career"), ask exactly one clarifying question, then proceed. Save the framed question for the transcript.

### Step 2: Convene the council (5 advisors in parallel)
Spawn all 5 advisors at once via the Agent tool (single message, 5 tool calls so they run concurrently, subagent_type `general-purpose`). Each gets its identity, the framed question, and the instruction to respond independently, not hedge, not try to be balanced, and lean fully into its angle. 150 to 300 words each, no preamble.

Advisor prompt template:
```
You are [Advisor Name] on an advisory council. Your thinking style: [advisor description].
A decision has been brought to the council:
---
[framed question]
---
Respond only from your perspective. Be direct and specific. Don't hedge or try to be balanced. Lean fully into your angle. The other advisors cover what you don't. 150 to 300 words, no preamble.
```

### Step 3: Anonymized peer review (5 reviewers in parallel)
This is the step that makes it more than "ask 5 times." Collect the 5 responses and label them Response A to E with the advisor-to-letter mapping shuffled into a non-obvious order. Spawn 5 reviewers in parallel (Agent tool, single message). Each sees all 5 anonymized responses and answers three questions, under 200 words:
1. Which response is strongest, and why?
2. Which has the biggest blind spot, and what is it?
3. What did ALL five miss that the council should consider?

### Step 4: Chairman synthesis
The chairman is the main session agent (you), not a sub-agent. De-anonymize, read all 5 responses plus all 5 reviews, and produce the verdict. This is advice TO the user, so it should be direct, take a stance, and avoid hedging. Verdict structure:

- **Where the council agrees.** Points multiple advisors converged on independently. High-confidence signals.
- **Where the council clashes.** The genuine disagreements. Don't smooth them over. Both sides, and why reasonable advisors disagree.
- **Blind spots the council caught.** Things that only surfaced in peer review.
- **The recommendation.** A clear, direct call. Not "it depends." The chairman may overrule the majority if the dissenter's reasoning is strongest, and should say so.
- **The one thing to do first.** A single concrete next step, not a list.
- **Decision record.** Written now, before the user decides, so a later retro scores against what was expected and not against hindsight.
  - **Chosen option:** `pending` until the user decides. Update it when they do.
  - **Success criteria:** each with a threshold and a date ("written milestone definitions in hand before signing").
  - **Kill criteria:** the signal that means it was the wrong call, with its threshold, its date, and the action to take.
  - **Review checkpoint:** a date, 90 days by default, or the decision's natural horizon (end of probation, the next funding event).
  - **Preserved dissent:** the strongest dissenting advisor's concern, quoted verbatim from their response, never summarized. If the council was unanimous, write that.

### Step 5: Write the report and transcript
Create a `council-decisions/` folder at the project root if it doesn't exist. Write two files, slug from the decision (roster runs prefix the slug with the roster name, such as `buyer-<slug>-<date>`):
- `council-decisions/council-<slug>-<YYYY-MM-DD>.html` is a clean, self-contained single-file HTML briefing (inline CSS, system font stack, white background, subtle borders, soft accents). Put the question at the top and the chairman's verdict prominently. Then add a simple agree/clash visual showing where advisors aligned and diverged, collapsible sections for each advisor's full response (collapsed) and the peer-review highlights, and the decision record. Footer: date and what was counciled. Don't fabricate a date, read it from the environment.
- `council-decisions/council-<slug>-<YYYY-MM-DD>.md` is the full transcript. It holds the original question, framed question, all 5 advisor responses, all 5 peer reviews (with the anonymization mapping revealed), and the full chairman synthesis with the decision record.

Present the verdict in chat and link both files. Offer to put the review checkpoint on the user's calendar or task list as "Retro: <decision>."

## Retro mode

Run it when a decision reaches its review checkpoint, when a kill criterion fires, or when the user asks to score a past call ("retro this decision," "score the council," "post-mortem the decision"). No sub-agents. A retro scores facts, and debate would only add noise. The chairman runs it.

1. **Load** the council's `.md` transcript from `council-decisions/`. If it predates the decision record and has no criteria, say so up front. The retro then scores the dissent, the assumptions, and the recommendation, and labels itself `no pre-committed criteria`, so nobody reads hindsight criteria as if they were set in advance.
2. **Ask the user for the facts**, in one batch, each tied to a criterion, a dissent, or an assumption. What actually happened is theirs to supply. Never infer an outcome from files that might be stale. Where notes on hand disagree with their answers, their answers win.
3. **Score** each item against what actually happened:
   - every success and kill criterion: met, missed, or triggered
   - every advisor's core concern: materialized, partially, or not, with its cost if it did
   - each load-bearing assumption in the framed question: held, partially, or not
   - the recommendation: followed or not, and how it played out
4. **Overall.** Give a WIN, PARTIAL, LOSS, or MIXED rating, then the lessons. The first lesson is which advisor's lens proved right, which tells you whose warnings to weight next time. Then propose any change to a standing playbook, without writing it silently.
5. **Write** `council-decisions/retro-<slug>-<YYYY-MM-DD>.md`.

## Important notes
- Always spawn the 5 advisors in parallel, and the 5 reviewers in parallel. Sequential spawning wastes time and lets earlier answers bleed into later ones.
- Always anonymize before peer review. If reviewers know who said what, they defer to certain styles instead of judging on merit.
- The chairman can disagree with the majority. If 4 say "do it" but the lone dissenter's reasoning is strongest, side with the dissenter and explain why.
- A synthetic seat (buyer, practitioner, or interviewer) is rehearsal material. Never quote it as voice of customer, and never present it as something a real person said.
- Don't council trivial questions. One right answer or no real tradeoff means just answer it.
- Model: advisors and reviewers can run on a cheaper, faster model to keep an 11-agent run economical. Keep the chairman synthesis on your best available model.
- Optional escalation: for an especially large decision where deterministic, backgrounded fan-out is worth the setup, the same structure can run on a workflow or orchestration tool instead of one-off agent calls, if your setup has one.

## Usage
```
council this: <decision with context>
run the council on <decision>
pressure-test this: <decision>
/council <decision>
buyer council this deck, personas in <file>       (roster: buyer)
practitioner council: <decision>                  (roster: practitioners)
rehearse my 90-day plan against the <company> panel (roster: interviewer)
retro this decision: council-decisions/council-...md  (retro mode)
```

The decision record and retro mode are adapted from the c-level-agents brief, decide, and post-mortem pattern in alirezarezvani/claude-skills (MIT). The practitioner seating table with a designated dissenter is adapted from coreyhaines31/marketingskills marketing-council (MIT). The interviewer roster is adapted from Kieran Flanagan's Exec Panel idea.
