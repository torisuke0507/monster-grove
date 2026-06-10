# Monster Grove - Game Spec

## 1. Project Overview

Monster Grove is a local, personal-use, retro handheld-style monster collecting RPG.

The goal is not to recreate any existing IP. Do not use copyrighted names, sprites, music, sound effects, characters, maps, text, UI assets, or monster designs from existing games.

The game should feel like a simple top-down 2D monster collecting RPG, but all content must be original.

## 2. Tech Stack

- TypeScript
- Phaser 3
- Vite
- localStorage for save/load
- No backend
- No external art assets in Phase 1
- Placeholder graphics should be drawn with Phaser primitives or simple generated shapes

## 3. Core MVP Goal

Phase 1 must prove that the following loop works:

1. Player starts the game
2. Player moves around a small map
3. Player steps into grass
4. Random encounter begins
5. Turn-based battle starts
6. Player can attack, capture, or run
7. Captured monster is added to party
8. Game returns to the map
9. Player position and party are saved with localStorage

If this loop works, the project can be expanded safely.

## 4. Phase 1 Scope

### Screens / Scenes

Implement these scenes:

1. BootScene
   - Load or initialize basic data
   - Then move to TitleScene

2. TitleScene
   - Show game title
   - Start Game button
   - Continue button if save exists
   - Delete Save button if save exists

3. WorldScene
   - Small top-down map
   - Player movement with arrow keys or WASD
   - Grass tiles
   - Random encounters while walking on grass
   - Save player position automatically

4. BattleScene
   - Player active monster vs wild monster
   - Turn-based battle
   - Actions:
     - Attack
     - Capture
     - Run
   - Battle log text
   - Return to WorldScene after win, capture, or run

## 5. Initial Map

Use one small map only.

Recommended settings:

- Canvas size: 640 x 576
- Tile size: 32px
- Map size: 20 columns x 15 rows
- Tiles:
  - `path`
  - `grass`
  - `wall`

The map should include:
- A walkable path area
- A grass area where encounters can occur
- Simple wall boundaries

No NPCs, buildings, signs, doors, shops, caves, or multiple maps in Phase 1.

## 6. Player Movement

Movement should be grid-based or tile-snapped if possible.

Minimum requirements:
- Move up/down/left/right
- Cannot walk through wall tiles
- Can walk on path and grass tiles
- Encounter check occurs only after stepping onto a grass tile
- Prevent repeated encounter checks while holding a key on the same tile

Recommended encounter chance:
- 12% per valid grass step

## 7. Battle System

Phase 1 battle should be deliberately simple.

### Player starts with one starter monster

Initial starter:
- Species: `mossbun`
- Level: 5
- Full HP

### Wild monsters

Use only 3 original species in Phase 1:

1. Mossbun
2. Cindermite
3. Pebloon

### Battle actions

#### Attack
- Player monster attacks wild monster
- Wild monster attacks back if still alive
- Damage formula can be simple:

```ts
damage = Math.max(1, attacker.attack - Math.floor(defender.defense / 2))
```

#### Capture
- Try to capture the wild monster
- If successful:
  - Add wild monster to player's party
  - Mark species as encountered and captured
  - Return to WorldScene
- If failed:
  - Wild monster attacks back

Recommended capture formula:

```ts
hpRatio = currentHp / maxHp
captureChance = clamp(baseCaptureRate * (1.2 - hpRatio) + 0.05, 0.05, 0.95)
```

#### Run
- End battle and return to WorldScene
- No monster is added

## 8. Save System

Use localStorage.

Save key:

```ts
monster_grove_save_v1
```

Save automatically when:
- Game starts for the first time
- Player moves to a new tile
- A monster is captured
- Battle ends

Save data should include:
- Save version
- Current map ID
- Player position
- Party monsters
- Encountered species IDs
- Captured species IDs

## 9. Phase 1 Non-Goals

Do not implement these yet:

- 151 monsters
- Full Pokédex-style collection screen
- Evolution
- Type effectiveness
- Multiple moves
- Items
- Shops
- NPCs
- Dialogue
- Quests
- Multiple maps
- BGM
- Sound effects
- Real pixel art
- Online functionality
- Mobile optimization
- Complex animations
- Advanced balancing

## 10. Quality Requirements

The Phase 1 implementation must:

- Build successfully with `npm run build`
- Run with `npm run dev`
- Avoid TypeScript errors
- Keep data definitions separate from scene logic
- Avoid hardcoding too much inside Phaser scenes
- Use clear file structure
- Be easy to extend in later phases