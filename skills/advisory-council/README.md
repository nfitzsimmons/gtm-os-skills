# advisory-council

A free skill that turns one model's opinion into a **council's** verdict. Part of [gtm-os-skills](../../README.md).

Ask an AI one question and you get one answer, and you have no way to tell if it's right because you only ever saw one angle. `advisory-council` fixes that. It runs a genuinely high-stakes decision through 5 advisors who each think from a deliberately different angle, has them peer-review each other anonymously, then a chairman synthesizes where they agree, where they clash, what they all missed, and what you should actually do. Adapted from Andrej Karpathy's LLM Council (dispatch to multiple reviewers, anonymized peer review, chairman synthesis) and the open `blader/llm-council` skill.

## What it does

1. **Frames the question.** Pulls in whatever context makes the decision specific instead of generic, then writes a neutral framing so every advisor starts from the same facts.
2. **Convenes 5 advisors, in parallel.** Contrarian (hunts for the fatal flaw), First-Principles Thinker (asks what you're actually trying to solve), Expansionist (finds the upside everyone's missing), Outsider (zero context, catches the curse of knowledge), Executor (only cares what you do Monday morning). Three built-in tensions, not five people trying to agree.
3. **Anonymized peer review, in parallel.** Each advisor's response gets relabeled and shown to 5 reviewers blind to who said what. They rank the strongest response, name the biggest blind spot, and flag what all five missed. This is the step that makes it more than "ask 5 times" — reviewers judge on merit, not by deferring to a favorite persona.
4. **Chairman synthesis.** De-anonymized, direct, and willing to overrule the majority if the lone dissenter's reasoning is strongest. Structured as: where the council agrees, where it clashes, blind spots peer review caught, the recommendation, and the one thing to do first.
5. **Writes the record.** A self-contained HTML briefing plus a full markdown transcript (every advisor response, every peer review, the anonymization mapping revealed) to `council-decisions/`.

## Install

**Claude Code.** This skill ships with a slash command, so there are two files to copy:

```bash
git clone https://github.com/nfitzsimmons/gtm-os-skills.git
cp -r gtm-os-skills/skills/advisory-council ~/.claude/skills/advisory-council
cp gtm-os-skills/skills/advisory-council/council.md ~/.claude/commands/council.md
```

It triggers on "council this," "run the council," "pressure-test this," "stress-test this," or "I'm torn between," or invoke it directly with `/council <decision>`.

**Claude.ai or ChatGPT Projects.** Open `SKILL.md`, copy everything below the frontmatter, and paste it into your project's custom instructions. Trigger it by asking for the council by name — the 5-advisor structure works the same in any chat, it just runs sequentially instead of through parallel sub-agents.

## When to use it

The council is for decisions where being wrong is expensive: which of two offers to take, how to frame a comp ask, whether to pursue a new venture, which positioning angle is strongest, whether to take a role at all, a big spend or a hard pivot. Skip it for factual lookups, pure creation tasks, or a decision you've already made and just want validated. One right answer or no real tradeoff means just answer it.

## Credit

The council structure is adapted from Andrej Karpathy's LLM Council and the open `blader/llm-council` skill. This version is a clean-room implementation rewritten to run on parallel sub-agent tooling.

## License

MIT. Take it, change it, ship it.
