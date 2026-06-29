# Chucks

**Generate 5E-compatible balanced, themed combat encounters for your party in seconds.**

Chucks is a plugin for Codex that helps Game Masters build combat encounters on the fly. Tell Codex your party's level, the setting, and the kind of fight you want. It picks monsters that fit, balances the XP, and hands you a short hook you can read straight to the table.

## Install

The plugin connects to the Chucks monster database automatically. No API keys, no configuration.

Install directly from GitHub:

```bash
codex plugin marketplace add https://github.com/chucks-ai/codex
codex plugin add chucks@chucks
```

For step-by-step setup instructions, visit [chucks.ai/docs](https://www.chucks.ai/docs).

## How to use

Just ask, in plain English:

> *Build me a moderate encounter for four level 5 characters. They're sneaking through a haunted lighthouse at night.*

You'll get back:

- **An Encounter Hook** - a couple of sentences describing who the creatures are, why they're there, and why they're hostile. Read it to your players.
- **A Roster** - the monsters involved, their counts, and the XP each. Total XP lands inside the budget for the difficulty you asked for.

You can then say things like *"swap the wraith for something less deadly"* or *"give me a tougher version"* and it'll iterate.

## What you get

The **Encounter Builder** skill. It knows how to:

- Match monsters to your party's level and chosen difficulty
- Respect the setting
- Generate random wilderness, travel, and dungeon encounters at the roll of a die
- Pick thematically coherent groups of enemies
- Keep encounters playable

It **won't** give you stat blocks, read-aloud text, or tactical advice. Those belong in your books and your head, not in an LLM.

## Coming soon

More skills are in the works:

- **Monster builder** - design and balance your own stat blocks
- **NPC generator** - flesh out NPCs with personality, motivation, and mechanics
- **Rules lookup** - search SRD 5.2.1 for specific rules and spells
- **Monster converter** - bring old-edition monsters up to the current ruleset

## Questions or feedback

Visit [chucks.ai](https://chucks.ai).

## Legal

This work includes material from the System Reference Document 5.2.1 ("SRD 5.2.1") by Wizards of the Coast LLC, available at https://www.dndbeyond.com/srd. The SRD 5.2.1 is licensed under the Creative Commons Attribution 4.0 International License, available at https://creativecommons.org/licenses/by/4.0/legalcode.

Chucks is an independent project and is not affiliated with, endorsed by, or sponsored by Wizards of the Coast.

## License

The contents of this repository - plugin configuration, skill instructions, and documentation - are released under the MIT License. See `LICENSE`.

The Chucks MCP server at `mcp.chucks.ai` is a hosted service and is not covered by this license.
