# Monster Grove - Roadmap

## Development Principle

Build the game as a vertical slice first.

Do not add large amounts of content until the core loop works.

The first success condition is:

> The player can walk, enter grass, encounter a monster, battle it, capture it, return to the map, and see the captured monster saved.

## Phase 1 - Vertical Slice MVP

### Goal

Create the smallest playable version.

### Features

- Vite + TypeScript + Phaser 3 project
- Title screen
- Continue game
- Delete save
- One small map
- Player movement
- Grass tiles
- Random encounters
- Three original monsters
- One move
- Turn-based battle
- Attack
- Capture
- Run
- Party save with localStorage
- Auto-save after important events
- README with setup instructions

### Acceptance Criteria

- `npm install` works
- `npm run dev` starts the game
- `npm run build` succeeds
- Player can move around the map
- Grass can trigger battles
- Battle can end by win, capture, or run
- Captured monsters are added to party
- Reloading the page preserves save data
- Delete save resets the game

## Phase 2 - Basic RPG Progression

### Goal

Make battles feel more like an RPG.

### Features

- Experience points
- Level up
- Stat growth
- Four move slots
- 6 to 8 total moves
- Heal party after battle for testing convenience
- Basic battle result screen

### Acceptance Criteria

- Monsters gain EXP after winning
- Monsters level up
- Stats increase
- No save corruption from new level/EXP fields

## Phase 3 - Collection Screen

### Goal

Add collection motivation.

### Features

- Collection screen
- Encountered / captured / unknown states
- Species descriptions
- Party list
- Basic monster detail view

### Acceptance Criteria

- Encountering a monster marks it as seen
- Capturing a monster marks it as captured
- Collection state persists after reload

## Phase 4 - 30 Monster Expansion

### Goal

Expand content without changing core systems too much.

### Features

- 30 original monster species
- Multiple encounter rarity tiers
- Different base stats
- Better placeholder sprites
- More moves

### Acceptance Criteria

- All 30 monsters can appear through encounter tables
- Data is clean and not hardcoded in scenes
- Build still succeeds

## Phase 5 - Evolution and Type Matchups

### Goal

Add deeper collection and battle systems.

### Features

- Evolution rules
- Type effectiveness
- More move types
- Better damage formula
- Evolution notification

### Acceptance Criteria

- Monsters can evolve based on level
- Type matchups affect damage
- Existing save data can be migrated or safely reset

## Phase 6 - World Expansion

### Goal

Make the game feel like an actual adventure.

### Features

- Multiple maps
- Map transitions
- Simple NPCs
- Signs
- Dialogue boxes
- Rest area / healing point
- Basic quest flags

### Acceptance Criteria

- Player can move between maps
- Save data remembers current map and position
- NPC dialogue works without breaking movement

## Phase 7 - Presentation Layer

### Goal

Improve look and feel.

### Features

- Original pixel art-style sprites
- Better battle UI
- Basic animations
- BGM and sound effects using original or generated assets only
- Settings menu

### Acceptance Criteria

- No copyrighted assets
- Game remains lightweight
- Controls remain responsive

## Phase 8 - Large Content Expansion

### Goal

Only after systems are stable, expand toward a larger monster roster.

### Features

- 100+ original monsters
- Larger maps
- More moves
- More encounter tables
- Optional story structure

### Acceptance Criteria

- Content is data-driven
- No massive hardcoded logic
- Save system remains stable