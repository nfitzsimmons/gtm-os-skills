# taste-check

A free skill that judges whether a draft **deserves to exist** before anyone polishes it. Part of [gtm-os-skills](../../README.md).

Every AI draft now lands clean, competent, and forgettable. Editing tools make it worse in a quiet way, because they smooth a hollow draft upward until it reads well and says nothing. `taste-check` runs before any of that. It asks whether there's a real idea in the draft that only you could have written, and when there isn't, it refuses to rewrite the words. It argues with you until you find the idea.

## What it does

1. **The Share Test.** Would a smart, busy reader forward this to a colleague? It names which of the five reasons people share the draft is going for, and whether it lands it.
2. **The Onlyness Test.** Delete your name. Could anyone tell you wrote it? Could a competitor republish it next week? Is it built on something only you have, or on the same public inputs every model has already seen?
3. **Spars instead of rewriting.** When the idea is hollow, it asks you for the belief, the story, or the number only you have. If you ask it to suggest angles, it offers them as provocations and pushes you to claim one as genuinely yours, never as a finished opinion.
4. **A verdict it means.** SHIP, REWORK, SPAR, or KILL. KILL is the point of the skill. It's allowed to tell you not to post.

## Install

**Claude Code.** Drop the folder into your skills directory:

```bash
git clone https://github.com/nfitzsimmons/gtm-os-skills.git
cp -r gtm-os-skills/skills/taste-check ~/.claude/skills/taste-check
```

It triggers on "taste-check this," "would anyone share this," "is there a real idea here," or "should I even post this."

**Claude.ai or ChatGPT Projects.** Open `SKILL.md`, copy everything below the frontmatter, and paste it into your project's custom instructions. Add three of your best past posts to the project so the Onlyness Test has a baseline to measure against.

## When to use it

Use it on anything with your name on it that you want to be remembered for, such as a LinkedIn post, a newsletter issue, an opinion piece, or a bylined argument. Skip it on scratch, status updates, and transactional copy. Run it first, before you edit, grade, or de-slop anything.

## Credit

The two gates, the sparring mechanic, and the KILL verdict are adapted from [Kieran Flanagan](https://www.linkedin.com/in/kieranjflanagan/)'s Content Taste Skill, which he gave away to his newsletter readers. This version keeps those pieces, leaves slop detection and polish to the tools that already do it, and adds a relay exception, a don't-re-ask rule, and locks on the lines that carry the idea.

## License

MIT. Take it, change it, ship it.
