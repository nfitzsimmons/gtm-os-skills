# gtm-os-skills

The skills behind the operating system I use to run go-to-market.

I'm a marketer who builds. Across demand gen and product marketing at Kolide, 1Password, and Keychain, I stopped treating AI as a chat box and built a personal operating system that runs the work with me. Context, voice, and workflows, all version-controlled, all firing through skills like the ones in this repo.

Hopefully my posts and this repo will help you build your own AI OS. The individual skills inside mine are useful on their own, so I'm giving them away here, one at a time. Star the repo and you'll catch each new one as it lands. The value isn't this first skill. It's what this becomes as it grows.

## What a skill is

A skill is a self-contained instruction set that makes a capable model do one job well, the same way every time. It's not a prompt you paste once and lose. It's a reusable unit you install and trigger.

Each folder under `skills/` is one skill, standalone. Take the one you want or clone the whole thing.

## The promise

Every skill in here is one I actually use in real work. No filler, no content-marketing demos. If it's in the pack, it earned its place.

## Skills

| Skill | What it does |
| --- | --- |
| [trust-check](skills/trust-check) | Make an AI answer auditable instead of just plausible. Disambiguate before it runs, get a receipt for every claim, and a second opinion when the stakes are real. |
| [advisory-council](skills/advisory-council) | Run a high-stakes decision through 5 advisors with clashing angles, anonymized peer review, and a chairman synthesis, instead of trusting one model's one answer. |

More landing over time.

## Install

**Claude Code.** Copy the skill folder you want into your skills directory:

```bash
git clone https://github.com/nfitzsimmons/gtm-os-skills.git
cp -r gtm-os-skills/skills/<skill-name> ~/.claude/skills/<skill-name>
```

Some skills also ship a slash command (check the skill's own README) — those need one more file copied into `~/.claude/commands/`.

**Claude.ai or ChatGPT projects.** Open the skill's `SKILL.md`, copy everything below the frontmatter, and paste it into your project's custom instructions. The skills are disciplines, not dependencies, so they work in any capable chat.

## License

MIT. Take them, change them, ship them.

## Who built this

Nick Fitzsimmons. Full-funnel marketer, former engineer. I write about building and running an AI GTM operating system on [LinkedIn](https://www.linkedin.com/in/nickfitzsimmons/).
