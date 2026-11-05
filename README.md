# gtm-os-skills

The skills behind the operating system I use to run go-to-market.

I'm a marketer who builds. Across demand gen, content, and marketing leadership at Kolide, 1Password, and Origin, I stopped treating AI as a chat box and built a personal operating system that runs the work with me. Context, voice, and workflows, all version-controlled, all firing through skills like the ones in this repo.

Hopefully my posts and this repo will help you build your own AI OS. The individual skills inside mine are useful on their own, so I'm giving them away here, one at a time. Star the repo and you'll catch each new one as it lands.

## What a skill is

A skill is a self-contained instruction set that makes a capable model do one job well, the same way every time. It's not a prompt you paste once and lose. It's a reusable unit you install and trigger.

Each folder under `skills/` is one skill, standalone. Take the one you want or clone the whole thing.

## The promise

Every skill in here is one I actually use in real work. No filler, no content-marketing demos. If it's in the pack, it earned its place. And when I sharpen a skill in my own system, the public version gets the upgrade too.

## Skills

| # | Skill | What it does |
| --- | --- | --- |
| 01 | [trust-check](skills/trust-check) | Make an AI answer auditable instead of just plausible. Disambiguate before it runs, get a receipt for every claim, and a second opinion when the stakes are real. |
| 02 | [advisory-council](skills/advisory-council) | Run a high-stakes decision through 5 advisors with clashing angles, anonymized peer review, and a chairman verdict, plus a decision record you can score later. |
| 03 | [taste-check](skills/taste-check) | Judge whether a draft deserves to exist before anyone polishes it. Two gates, a sparring step instead of a rewrite, and a verdict that can say KILL. |

More landing over time.

## Install

**Claude Code.** Copy the skill folders you want into your skills directory:

```bash
git clone https://github.com/nfitzsimmons/gtm-os-skills.git
cp -r gtm-os-skills/skills/taste-check ~/.claude/skills/
# or all of them
cp -r gtm-os-skills/skills/* ~/.claude/skills/
```

advisory-council also ships a `/council` slash command. Its README has the one extra copy step.

**Claude.ai or ChatGPT projects.** Open the skill's `SKILL.md`, copy everything below the frontmatter, and paste it into your project's custom instructions. If a skill has a `references/` folder, upload those files to the project's knowledge too. The skills are disciplines, not dependencies, so they work in any capable chat.

## Changelog

**2026-11-02**
- **taste-check** added as skill 03.
- **trust-check** now tags every claim SOURCED, INFERRED, or UNVERIFIED, treats a claim about a live page as unproven until the page itself is fetched, runs a denominator test on market-size numbers, and holds second-opinion reviewers to an output contract (a verdict that contradicts its own findings is a failed review).
- **advisory-council** now writes a decision record (success criteria, kill criteria, a review date, and the strongest dissent quoted verbatim), adds a retro mode that scores the call against what actually happened, and adds three rosters: buyer personas, practitioner schools of thought, and an interview panel.

**2026-08-05.** advisory-council added as skill 02.

**2026-06-24.** trust-check added as skill 01.

## License

MIT. Take them, change them, ship them.

## Who built this

Nick Fitzsimmons. Full-funnel marketer, former engineer. I write about building and running an AI GTM operating system on [LinkedIn](https://www.linkedin.com/in/nickfitzsimmons/).
