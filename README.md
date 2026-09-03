# Chucks

**Teach your AI how to play 5e. Right rules, sound mechanics, and ideas that surprise you.**

Chucks gives Codex reliable 5e capabilities for preparing and running a game. It can search the current SRD, look up monsters and stat blocks, build and validate balanced encounters, or roll a random encounter when the party goes off the beaten path.

## Install

The plugin connects to the Chucks monster database automatically. No API keys, no configuration.

Install directly from GitHub:

```bash
codex plugin marketplace add https://github.com/chucks-ai/codex
codex plugin add chucks@chucks
```

For step-by-step setup instructions, visit [chucks.ai/docs](https://www.chucks.ai/docs).

## What you can do with Chucks

Just ask Codex in plain English:

- **Check a rule.** Ask *“What are the current rules for hiding?”* Chucks searches the current SRD instead of relying on Codex's memory of older editions.
- **Look up a monster.** Ask *“Show me the fire elemental stat block.”* Chucks returns the verified current name, description, and SRD stat block.
- **Build a balanced encounter.** Ask *“Build a moderate encounter for four level 5 characters. They're sneaking through a haunted lighthouse at night.”* Chucks uses real monsters, calculates the XP budget with the 2024 rules, and checks the completed roster.
- **Roll a random encounter.** Tell Codex where the party is and how difficult the fight should be. Chucks chooses the opponents, and Codex sets the scene and gives them a reason to be there.

You can follow up naturally: ask for a harder version, replace a monster, request the broader chapter behind a rule, or adjust the encounter for your table.

## What the plugin includes

Chucks combines two pieces:

- A connector to Chucks' hosted rules and monster data, encounter calculations, validation, and random encounter generator.
- An encounter-building skill that teaches Codex how to combine those capabilities into a useful result.

The individual capabilities can also be combined in your own skills. Chucks supplies reliable building blocks without deciding how you have to play.

## What's covered

Rules, character options, spells, items, and monsters are limited to material published in the current SRD. Material from other sourcebooks is not available through Chucks. Codex may still answer from memory, but that answer did not come from Chucks and may be incomplete or blend different editions.

The bundled encounter builder keeps its default output focused on a short encounter hook and a checked roster. It leaves out read-aloud text and tactical advice unless you ask for them because those details are easier for an AI to get wrong.

## Coming soon

More skills are in the works:

- **Monster builder** - design and balance your own stat blocks
- **NPC generator** - flesh out NPCs with personality, motivation, and mechanics

## Questions or feedback

Visit [chucks.ai](https://chucks.ai).

## Legal

This work includes material from the System Reference Document 5.2.1 ("SRD 5.2.1") by Wizards of the Coast LLC, available at https://www.dndbeyond.com/srd. The SRD 5.2.1 is licensed under the Creative Commons Attribution 4.0 International License, available at https://creativecommons.org/licenses/by/4.0/legalcode.

Chucks is an independent project and is not affiliated with, endorsed by, or sponsored by Wizards of the Coast.

## License

The contents of this repository - plugin configuration, skill instructions, and documentation - are released under the MIT License. See `LICENSE`.

The Chucks MCP server at `mcp.chucks.ai` is a hosted service and is not covered by this license.
