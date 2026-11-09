# copy-grader

A free skill that scores marketing copy against a weighted rubric, quotes the line behind every score, and rewrites toward 100 without flattening your voice. Part of [gtm-os-skills](../../README.md).

"Make this better" is the worst instruction you can give a model. It has no standard, so every pass moves the copy somewhere different, and you can't tell whether the new version is better or just different. `copy-grader` gives the model a standard. Twelve weighted principles from the direct-response masters, a score for each one with the quoted line that earned it, and a ranked list of the fixes that recover the most points. Same draft, same rubric, same number.

## What it does

1. **Grades.** Scores each principle 0 to 100, quotes the evidence, and computes a weighted total you can audit line by line.
2. **Ranks the fixes.** Orders them by points recoverable (score gap × weight), so you fix the hook before you fix the comma.
3. **Rewrites toward 100.** Attacks the biggest gaps, re-grades, shows the before and after per principle, and stops when the gains flatten. A rewrite that raises the score by flattening your voice counts as a failure.
4. **Builds new rubrics.** Name a master ("score this like Halbert") or a domain ("SaaS pricing page") and it drafts 10 to 15 weighted principles with good and bad examples, shows them to you, and saves the rubric for reuse.

It ships with two rubrics: a default direct-response rubric (Ogilvy, Halbert, Sugarman, Hopkins, Caples) and a LinkedIn thought-post rubric that drops the offer and CTA principles a thought post can't earn.

## Install

**Claude Code.** Drop the folder into your skills directory:

```bash
git clone https://github.com/nfitzsimmons/gtm-os-skills.git
cp -r gtm-os-skills/skills/copy-grader ~/.claude/skills/copy-grader
```

It triggers on "grade this copy," "score this against Ogilvy," "how good is this landing page," or "rewrite this to a 95."

**Claude.ai or ChatGPT Projects.** Open `SKILL.md`, copy everything below the frontmatter, and paste it into your project's custom instructions. Upload both files in `references/` to the project's knowledge, plus three to five pieces in your voice so voice fidelity has something to score against.

## When to use it

Use it on copy that has to perform, such as a hero section, a launch email, an ad, a pricing page, a cold opener, or a post you want remembered. Skip it on scratch.

Run [taste-check](../taste-check) first when you're not sure the draft has a real idea. A grader assumes the draft deserves to exist, and polishing a hollow draft to a 90 still leaves it hollow.

## Credit

The rubric-engine idea (pick a master, generate weighted principles with good and bad examples, score the work, rewrite toward 100) comes from [Kieran Flanagan](https://www.linkedin.com/in/kieranjflanagan/)'s newsletter piece on turning an expert's best thinking into an AI skill. The default rubric's principles are distilled from David Ogilvy, Gary Halbert, Joseph Sugarman, Claude Hopkins, and John Caples.

## License

MIT. Take it, change it, ship it.
