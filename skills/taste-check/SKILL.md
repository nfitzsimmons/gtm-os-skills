---
name: taste-check
description: A pre-publish taste gate that JUDGES whether a draft deserves to exist and, when it doesn't, spars with the author to fix the idea instead of rewriting the words. Runs two gates, the Share Test (would anyone forward this) and the Onlyness Test (delete the byline, can you still tell who wrote it), then returns a SHIP / SPAR / REWORK / KILL verdict. Use before publishing anything bylined, such as LinkedIn posts, newsletters, opinion pieces, thought leadership, or a bylined marketing argument, and before any polish or editing pass. Triggers on "taste-check this," "would anyone share this," "is this differentiated," "does this sound like me or like anyone," "is there a real idea here," "should I even post this." This skill does NOT rewrite.
---

# Taste Check

A pre-publish judge, not a writer. Editing tools, graders, and AI-tell strippers all improve the words on the page, and every one of them assumes the draft is worth improving. This skill asks the question upstream of all of them. Is there a real, non-copyable idea here at all? When the answer is no, it does not polish. It spars.

The failure it exists to catch is a draft that is clean, competent, on-voice, and completely forgettable. "Competent and clean" is where every AI draft now lands, and a review process that only polishes will smooth a hollow draft *upward* and ship it. Taste-check is the stop-the-line gate that can say "there is no idea here, don't publish."

Use it on anything bylined and worth being remembered for. Skip it on scratch, internal status, transactional copy, and pure announcements (note if one could be stronger, but don't gate it).

## Load context

Before judging, find out whose byline this is. The Onlyness Test is meaningless without knowing whose voice and stance to measure against.

1. **The author.** Who is publishing this, what do they do, and what do they stand for? Use whatever the user has given you: a bio, a voice guide, a positioning doc.
2. **A baseline.** If the user has 3 to 5 of their best past pieces, or a short list of writing they admire with the reason each one works, read them. "Could only they have written this" is much sharper against real work. Judge the Share Test against those reasons, not your own sense of good writing, and name the one a failing draft breaks.
3. If neither exists, run the gates anyway and say the voice read is limited. Better: ask the author for three posts they're proud of before the next run.

## Gate 1: The Share Test

Would a smart, busy reader forward this to a colleague with a note that says "you need to read this"? People share for five reasons. Name which one the piece is going for, then judge whether it lands it.

1. **It made them look smart.** Sharing it signals taste.
2. **It named something they felt but couldn't articulate.** The "yes, exactly" reaction.
3. **It gave them an unfair advantage.** A framework, number, or model they can use now.
4. **It surprised them.** It broke a pattern they didn't know they were in.
5. **It told a story that lingers** after the tab closes.

A piece aimed at none of these gets a like, not a share. "Maybe" is a fail. Within a niche, shareability *within that niche* is what counts. A post fifty security engineers would send each other passes even if the public wouldn't care.

## Gate 2: The Onlyness Test

Could *only this author* have written this? This is the differentiation gate, and it's the reason the skill exists. AI models are shared infrastructure. Everyone prompting the same model on the same topic converges on the same competent answer. The only defense is something the model doesn't have. Test three ways.

- **The byline test.** Delete the author's name. Can you still tell who wrote it? If any competent person in the niche could have produced it, it fails.
- **The steal test.** Could a competitor reverse-engineer and republish this next week? If the substance is public knowledge rearranged, there's no moat.
- **The source test.** Is it built on something only this author has (a first-hand story, their own data, a belief they'll defend), or on the same public inputs every model has already seen?

Generic-but-good still fails Gate 2. A draft that passes Share and fails Onlyness is the exact case this skill was built for. **Do not send it to polish. Go to the sparring step.**

**Relays are the one exception.** If the piece's job is relaying or promoting someone else's work (a company launch, a colleague's research, a teammate's post), Onlyness is advisory. Surface the strengthener once, marked optional, and never invent a first-person detail to satisfy it. The verdict rests on the Share Test and craft, so it is SHIP or REWORK, never SPAR or KILL on Onlyness alone. Not every post has to be uniquely yours. It's the aspiration, not an absolute.

## The sparring step (fix the idea, not the words)

When the core is weak (it passes Share but fails Onlyness, or it has no real insight at all), the answer is never better word choice. Polishing a hollow draft is lipstick on slop. Interrogate the author for the non-copyable input. Ask questions like these.

- What do you believe about this that your smartest peers would argue with?
- What did you personally watch happen that contradicts the consensus?
- What's the number, the result, or the specific story that only you have?
- Who is this for, and who are you willing to be wrong in front of?

Give the author two doors at each prompt.

- **"I'll answer."** They supply the real opinion, story, or data. This is the best path, because genuine differentiation only comes from here.
- **"Suggest for me."** You propose candidate angles and contrarian-but-defensible takes drawn from the topic and their voice.

**The guardrail on "suggest for me" is the whole game.** An AI-suggested opinion comes from the same model everyone else uses, so handing over a finished take is generating slop with extra steps. Never deliver a suggested opinion as if it's theirs. Present suggestions as provocations, then push back. "Here are three angles. Which is actually true for *you*? What would you add from your own experience that I can't know?" The suggestion is a prompt for the author's conviction, not a replacement for it. If they can't claim any of it as genuinely theirs, the piece isn't ready. Say so.

## The verdict

Close every run with one call, and mean it.

- **SHIP.** Passes both gates. Send it on to editing, or straight out.
- **REWORK.** Passes Onlyness but misses on execution (weak hook, buried lede, vague where it should be specific). The idea is real. Hand it to editing with the specific miss named.
- **SPAR.** Clean but hollow, with a salvageable core. Run the sparring step. Do not polish first.
- **KILL.** No idea, no angle, nothing only this author could say, and sparring surfaced nothing. Say so directly. Don't pretend a rewrite of the words will save it. This verdict is the point of the skill, so use it when it's true.

**Don't re-ask what's been answered.** This applies when Onlyness is borderline, meaning there's a real idea but it could be more personal. If the author was already asked for the non-copyable input and has none to add, decide on the Share Test and craft as in the relay exception. That means SHIP, or REWORK with the miss named. SPAR only when the questions were never asked. A draft with no idea at all is still a KILL, asked or not.

**Name the locks.** When the gate passes, list the sentences any later editing pass must keep word for word (copied exactly from the draft). These are usually the lines that carry the onlyness. Editors and AI polish passes love to smooth exactly those lines into something generic, so check the final against them.

## Output format

```
## Taste Check

**Share Test:** PASS / FAIL / BORDERLINE. Which of the 5 triggers, and does it land?
**Onlyness Test:** PASS / FAIL / BORDERLINE. Could only this author have written it? What's missing?

**What's working:** the real strengths, cited to specific lines.

**Verdict:** SHIP / REWORK / SPAR / KILL, in one or two sentences.
**Locks:** the lines later edits must keep verbatim (on SHIP or REWORK).
**Next move:** the specific hand-off (sparring questions, or "edit the hook," or "ship it").
```

## Where it sits

- **First gate, before any polish.** Run it before you edit, grade, fact-check the wording, or de-slop a draft. A KILL or SPAR here stops the process before it wastes a polish pass smoothing a hollow draft.
- **It judges the idea and hands off.** AI-tell detection, rubric scoring, and line editing belong to your other tools. This skill is deliberately thin on everything an editor already does well.

## Hard rules

- **Never rewrite the draft.** The moment you hand back rewritten prose you've become an editor and skipped the idea problem. Judge, spar, hand off.
- **Never deliver a suggested opinion as the author's.** Suggestions are provocations to draw out their conviction, not a stance to adopt.
- **Don't soften a KILL to be agreeable.** The skill's only value is an honest verdict. A hollow draft called "pretty good" is worse than useless.

## Credit

The two-gate shape, the Onlyness Test, the sparring mechanic, and the KILL verdict are adapted from Kieran Flanagan's Content Taste Skill, which he gave away to his newsletter readers. This version keeps those pieces, drops the slop detection and polish that other tools already cover, and adds the relay exception, the don't-re-ask rule, and the locks.
