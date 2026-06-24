# trust-check

A free skill that makes an AI answer **auditable** instead of just plausible. Part of [gtm-os-skills](../../README.md).

When you ask AI to pull a number from a document, synthesize research, or answer something you're about to act on, the failure isn't usually a hallucinated fact. It's a confident answer built on a word the model guessed at, a stale source, or an inference dressed up as a finding. `trust-check` bundles three behaviors that close those gaps, adapted from how Anthropic's own team keeps AI honest when nearly every internal data question runs through it.

## What it does

1. **Disambiguate before executing.** Surfaces the words in your request whose interpretation would change the answer, and states the reading it's using, before it runs.
2. **Receipts on every claim.** Cites the file and section each claim came from, flags anything it inferred rather than found, and names the one thing most worth double-checking.
3. **Second opinion for high-stakes work.** For money, legal, brand, or anything you're about to automate, gets the output judged in fresh context or by a different model, adversarially.

Plus a method for building an "answer key" before you automate a task end to end.

## Install

**Claude Code.** Drop the folder into your skills directory:

```bash
git clone https://github.com/nfitzsimmons/gtm-os-skills.git
cp -r gtm-os-skills/skills/trust-check ~/.claude/skills/trust-check
```

It triggers on "verify this," "can I trust this," "give me receipts," "double-check this," or before you act on an extracted figure or claim.

**Claude.ai or ChatGPT Projects.** Open `SKILL.md`, copy everything below the frontmatter, and paste it into your project's custom instructions. The three behaviors work the same in any chat — they're a discipline, not a dependency.

## When to use it

Use it when a wrong answer would cost something: a figure going into a board deck, a number you're forwarding to a customer, a research synthesis you'll make a decision on. Skip it for low-stakes chat where being wrong costs nothing. The overhead only pays off against real stakes.

## Credit

The three tactics are adapted from Anthropic's published account of how their team improves AI data-retrieval accuracy internally. This skill is one person's clean-room implementation of that approach, free to use and modify.

## License

MIT. Take it, change it, ship it.
