# Monster Grove - Codex Tasks

## Important Rule

Do not implement future-phase features unless the task explicitly asks for them.

The priority is a stable, working vertical slice.

## Recommended File Structure

Use a clear structure similar to this:

```txt
src/
  main.ts
  game/
    config.ts
    constants.ts
  scenes/
    BootScene.ts
    TitleScene.ts
    WorldScene.ts
    BattleScene.ts
  data/
    monsters.ts
    moves.ts
    maps.ts
    encounters.ts
  systems/
    saveSystem.ts
    battleSystem.ts
    encounterSystem.ts
    monsterFactory.ts
  types/
    game.ts
    monster.ts
    battle.ts
    map.ts
  ui/
    Button.ts
    TextPanel.ts
```

This structure can be adjusted if there is a good reason, but do not place all logic inside one large file.

## Task 1 - Create Project and Phase 1 MVP

### Instruction

Implement Phase 1 only.

### Requirements

- Create a Vite + TypeScript + Phaser 3 project
- Implement BootScene
- Implement TitleScene
- Implement WorldScene
- Implement BattleScene
- Add one small map
- Add player movement
- Add grass encounter logic
- Add 3 original monsters
- Add one simple move
- Add turn-based battle
- Add attack, capture, and run actions
- Add localStorage save/load
- Add delete save button
- Add README

### Do Not Implement

- Evolution
- Full collection screen
- 151 monsters
- NPCs
- Shops
- Multiple maps
- Items
- BGM
- Sound effects
- Advanced battle mechanics

### Validation

After implementation:

```bash
npm install
npm run build
```

If there are errors, fix them before finishing.

## Task 2 - Review Phase 1 Before Expanding

After Phase 1 works, review the implementation.

Check:

- Is state management clean?
- Is save data isolated from Phaser scene logic?
- Are monster species and monster instances clearly separated?
- Are map tiles data-driven?
- Is encounter logic reusable?
- Is battle logic testable outside Phaser scenes?
- Are there obvious bugs around save/load?
- Does the game still build?

Fix structural problems before adding new features.

## Task 3 - Add Basic Progression

Only after Task 2 is complete:

- Add EXP
- Add level up
- Add stat growth
- Add 4 move slots
- Add 6 to 8 total moves
- Update save data carefully

Run build after changes.

## Task 4 - Add Collection Screen

Only after Task 3 is stable:

- Add collection screen
- Track seen/captured/unknown
- Show species description
- Show party list
- Persist collection state

Run build after changes.

## Task 5 - Expand to 30 Monsters

Only after Task 4 is stable:

- Add 30 original monsters
- Add rarity-weighted encounter tables
- Add more moves
- Keep content data-driven

Run build after changes.