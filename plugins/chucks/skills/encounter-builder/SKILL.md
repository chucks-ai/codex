---
name: encounter-builder
description: Build balanced 5E-compatible combat encounters. Use this when the user wants to create, design, or plan a combat encounter for their fifth edition party.
---

# 5E Encounter Builder

Build valid 5E-compatible combat encounters (SRD 5.2.1) with random_encounter_generator, encounter_planner, monster_search, encounter_validator, and monster_lookup.

Do not force an encounter when the user's constraints cannot produce a valid roster. If required monsters do not exist, cannot fit the XP budget, or cannot satisfy explicit scene constraints, explain what blocks the encounter and ask which constraint to relax.

## Read the request

Before calling any tool, read the party, the scene, and the encounter constraints.

### Party Composition

`party_composition` is required: the number of characters and their levels. Ask for it if missing.

`difficulty` is optional. If the user does not specify it, use `"unknown"`. Map the user's wording to `low`, `moderate`, or `high`: easy is `low`, medium is `moderate`, and hard or deadly is `high`.

Only include `xp_bump_percent` if the user explicitly asks for an encounter that diverges from the baseline XP budget for the party's levels.

### Scene

Map scene fields once and pass the same values to any tool that accepts them.

`habitat`: the environment the user described, plus any habitat that directly borders it. Examples: village in farmland -> `["Urban", "Grassland"]`; shallow cavern in woods -> `["Caverns", "Forest"]`; forest river -> `["Forest", "Inland Water"]`.

Map scene words to habitat values:
- Urban: city, town, village, hamlet, castle, tower, street, alley, inn
- Grassland: plains, prairie, steppe, farmland, savanna, open fields
- Inland Water: river, lake, stream, canal, riverbank, lake shore
- Forest: forest, jungle, rainforest, dense woods
- Hill: hills, moorland, foothills
- Mountain: mountains, peaks, high pass, alpine cliff
- Coastal: beach, shoreline, seaside cliff, cove, lagoon
- Sea: ocean, high seas, reef, seabed, abyss
- Swamp: swamp, marsh, bog, fen, bayou, mangrove
- Caverns: caves, tunnels, mines, grottos
- Dungeon: crypts, catacombs, sewers, vaults, prison, tomb
- Ruins: ruined temple, keep, abandoned town, ancient ruins
- Arctic, Desert, Underdark, Planar: use the matching value only when explicitly named

`pc_situation`: what the PCs are doing. Use `on_waterborne_vessel`, `flying`, `surface_swimming`, or `underwater_swimming`. Omit it for an ordinary land scene.

### Encounter constraints

Encounter constraints are what the user says about the opponents or about what they must overcome. Look for them in:
- **Creatures.** Monsters or groups the user includes or excludes, including unnamed groups such as "companions". A single creature ("a troll") means one. A plural or group ("kobolds", "companions", "a pack of wolves") means two or more. "A pair" means two. Companions are in addition to the creatures they accompany.
- **Theme or faction.** For example, a horror encounter or a thieves' guild.
- **Monster descriptions.** What the user says the monsters look like, carry, or do.
- **Scene obstacles.** Terrain that keeps the creatures from reaching the PCs, such as a wide river between them or PCs on top of a tower. Infer the capability the creatures need to reach the PCs.
- **Hazards.** A hazard the fight happens inside. Infer what the creatures need to survive it or attack from outside it. Inside a freezing blizzard: cold resistance or immunity.

A description is mechanical only if most creatures could not do it, such as casting fire spells, carrying crossbows, or burrowing up from underground. Capabilities inferred from scene obstacles and hazards are mechanical too. Check mechanical constraints with the tools.

Everything else is flavor, such as charging, surrounding the PCs, taunting them, or sizes: "a huge beast" is any very big beast, not the Huge size. Do not verify flavor with tools. When in doubt, treat a description as flavor.

`pc_situation` is never an encounter constraint. The tools already restrict creatures to what the PCs' situation requires, so do not add constraints for it: PCs riding griffons do not need a flying constraint.

## Choose your approach

First decide whether the request has any encounter constraints.

The following fields do not count as encounter constraints:
- `party_composition`
- `difficulty`
- `xp_bump_percent`
- `habitat`
- `pc_situation`

Scene context such as forest, ocean, countryside, dungeon, city street, sailing on a ship, swimming, or flying is only `habitat` and/or `pc_situation`. It does not require plan → search → validate.

Do not invent themes such as pirates, sea creatures, naval threats, ambushers, or factions before choosing the workflow.

A hazard is a constraint even when it names a habitat: "fighting in a mountain blizzard" is a `Mountain` habitat plus a cold hazard.

Use **plan → search → validate** only when the request has at least one encounter constraint, even a flavor-only one: the random generator cannot match any description. In all other cases, use **random_encounter_generator**.

Both approaches produce a balanced 5E roster to present to the user.

## Random encounter generator

Never use the **encounter_planner** with the random encounter generator.

Call only **random_encounter_generator** with `party_composition`, `difficulty`, `xp_bump_percent`, `habitat`, and `pc_situation`. Do not call encounter_planner, monster_search, or encounter_validator before or after it.

Use the returned roster as-is. Do not swap creatures or adjust counts after calling the tool. If the tool returns an error, fall back to the plan → search → validate workflow.

## Plan -> Search -> Validate

### 1. Plan XP

Call **encounter_planner** with `party_composition`, `difficulty`, and `xp_bump_percent`. Reuse its exact `xp_budget` and `number_of_pcs`.

### 2. Find candidates

Call **monster_search** once, in the same response as encounter_planner: the search does not need the planner's results. Pass `party_composition`, `difficulty`, `xp_bump_percent`, `habitat`, `pc_situation`, and `queries` for every creature group and constraint.

Search returns a summary of each candidate. When a mechanical constraint needs details the summary does not show, such as gear or damage defenses, call **monster_lookup** (when available) with the shortlist in one call, and look up more candidates if none qualify. Keep only creatures whose stat block confirms the detail; creatures of the same species often carry different gear. If **monster_lookup** is unavailable, tell the user which details are unverified.

The tools know what creatures can do, not what fits a theme. Use your own knowledge to pick creatures that fit the theme, faction, and flavor, such as undead and cultists for a horror encounter.

### 3. Assemble

Include exactly the creatures and counts from the encounter constraints.

Default to single-species encounters. Go multi-species only when the theme calls for it.

Useful patterns: war band, swarm, solo boss, captain + squad, boss + minions, elite pair.

Hard rules, unless the user asks otherwise:
- **Max 2 species.** Pets, mounts, summoned creatures, constructs, and template-variant flavor species do not count.
- **Faction coherence.** All creatures must plausibly fight on the same side. When in doubt, use one species.
- **Monster count.** Stay at or below 2x number_of_pcs.

The Hook may add factions, motives, settings, and props, but do not invent gear, abilities, damage types, or mechanical effects. If a detail is mechanically important, verify it with **monster_lookup** or keep it vague.

### 4. Validate

Call **encounter_validator** with the finalized roster and planner budget. If invalid, adjust counts or swaps and validate again before presenting.

## Present

Present only:

**Encounter Hook**: 2-3 sentences explaining who the creatures are, why they are here, and why they are hostile. Use the roster's exact creature names and counts.

If the roster includes creatures that do not naturally fit the scene, explain how they are present and able to engage the PCs. For example, humanoids in aerial or naval encounters usually need their own vessel, mount, platform, or other scene explanation.

**Roster**: table with name, count, and XP each. Then show total XP and budget range.

Do not use tactical-role labels such as "frontline tank", "ranged sniper", "melee brute", or "spellcaster support". If behavior matters, describe it in fiction.

Do not include stat summaries, damage numbers, read-aloud text, tactical advice, DCs, skill checks, ability scores, or other mechanics unless the user asks. If asked, keep it brief and include only information provided by the tools.

End by asking whether the user wants to adjust the roster or generate another encounter.
