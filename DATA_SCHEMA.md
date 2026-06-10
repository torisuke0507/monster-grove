# Monster Grove - Data Schema

This document defines the core TypeScript data structures for the project.

The goal is to keep Phase 1 simple while allowing later expansion into levels, moves, evolution, type matchups, a collection screen, and more monsters.

## 1. Basic Types

```ts
export type MonsterType =
  | "nature"
  | "ember"
  | "stone"
  | "water"
  | "wind"
  | "spark"
  | "shade"
  | "neutral";

export type TileType = "path" | "grass" | "wall";

export type Direction = "up" | "down" | "left" | "right";
```

## 2. Stats

```ts
export interface Stats {
  hp: number;
  attack: number;
  defense: number;
  speed: number;
}
```

## 3. Monster Species

`MonsterSpecies` represents the fixed species-level data.

```ts
export interface MonsterSpecies {
  id: string;
  name: string;
  type: MonsterType;
  description: string;
  baseStats: Stats;
  baseCaptureRate: number;
  startingMoveIds: string[];
  placeholderColor: string;
}
```

Example Phase 1 species:

```ts
export const MONSTER_SPECIES: MonsterSpecies[] = [
  {
    id: "mossbun",
    name: "Mossbun",
    type: "nature",
    description: "A small grove-dweller with soft moss around its ears.",
    baseStats: {
      hp: 24,
      attack: 7,
      defense: 6,
      speed: 5
    },
    baseCaptureRate: 0.45,
    startingMoveIds: ["quick_strike"],
    placeholderColor: "#5fa36a"
  },
  {
    id: "cindermite",
    name: "Cindermite",
    type: "ember",
    description: "A tiny ember creature that leaves warm sparks behind.",
    baseStats: {
      hp: 20,
      attack: 9,
      defense: 4,
      speed: 7
    },
    baseCaptureRate: 0.38,
    startingMoveIds: ["quick_strike"],
    placeholderColor: "#c65b3a"
  },
  {
    id: "pebloon",
    name: "Pebloon",
    type: "stone",
    description: "A round stone-like creature that rolls through tall grass.",
    baseStats: {
      hp: 28,
      attack: 6,
      defense: 9,
      speed: 3
    },
    baseCaptureRate: 0.42,
    startingMoveIds: ["quick_strike"],
    placeholderColor: "#8a8d91"
  }
];
```

## 4. Monster Instance

`MonsterInstance` represents an owned or wild individual monster.

```ts
export interface MonsterInstance {
  instanceId: string;
  speciesId: string;
  nickname?: string;
  level: number;
  exp: number;
  currentHp: number;
  stats: Stats;
  moveIds: string[];
}
```

## 5. Move

Phase 1 only needs one simple move, but the schema should support expansion.

```ts
export interface Move {
  id: string;
  name: string;
  type: MonsterType;
  power: number;
  accuracy: number;
}
```

Example:

```ts
export const MOVES: Move[] = [
  {
    id: "quick_strike",
    name: "Quick Strike",
    type: "neutral",
    power: 8,
    accuracy: 1.0
  }
];
```

## 6. Map Data

```ts
export interface Position {
  x: number;
  y: number;
}

export interface GameMap {
  id: string;
  name: string;
  width: number;
  height: number;
  tileSize: number;
  tiles: TileType[][];
  startPosition: Position;
  encounterTableId?: string;
}
```

## 7. Encounter Table

```ts
export interface EncounterEntry {
  speciesId: string;
  minLevel: number;
  maxLevel: number;
  weight: number;
}

export interface EncounterTable {
  id: string;
  mapId: string;
  entries: EncounterEntry[];
}
```

Example:

```ts
export const ENCOUNTER_TABLES: EncounterTable[] = [
  {
    id: "starter_grove_grass",
    mapId: "starter_grove",
    entries: [
      {
        speciesId: "mossbun",
        minLevel: 3,
        maxLevel: 5,
        weight: 45
      },
      {
        speciesId: "cindermite",
        minLevel: 3,
        maxLevel: 5,
        weight: 30
      },
      {
        speciesId: "pebloon",
        minLevel: 3,
        maxLevel: 5,
        weight: 25
      }
    ]
  }
];
```

## 8. Save Data

```ts
export interface PlayerSaveData {
  version: 1;
  currentMapId: string;
  playerPosition: Position;
  party: MonsterInstance[];
  encounteredSpeciesIds: string[];
  capturedSpeciesIds: string[];
  createdAt: string;
  updatedAt: string;
}
```

Default new save:

```ts
export const createNewSave = (): PlayerSaveData => {
  const now = new Date().toISOString();

  return {
    version: 1,
    currentMapId: "starter_grove",
    playerPosition: {
      x: 2,
      y: 2
    },
    party: [
      {
        instanceId: crypto.randomUUID(),
        speciesId: "mossbun",
        level: 5,
        exp: 0,
        currentHp: 24,
        stats: {
          hp: 24,
          attack: 7,
          defense: 6,
          speed: 5
        },
        moveIds: ["quick_strike"]
      }
    ],
    encounteredSpeciesIds: ["mossbun"],
    capturedSpeciesIds: ["mossbun"],
    createdAt: now,
    updatedAt: now
  };
};
```

## 9. Battle State

```ts
export type BattlePhase =
  | "intro"
  | "player_turn"
  | "enemy_turn"
  | "capture_attempt"
  | "won"
  | "captured"
  | "ran"
  | "lost";

export interface BattleState {
  phase: BattlePhase;
  activePlayerMonster: MonsterInstance;
  wildMonster: MonsterInstance;
  turn: number;
  log: string[];
}
```

## 10. Utility Functions Needed

Implement these utility functions outside Phaser scenes:

```ts
export function getSpeciesById(speciesId: string): MonsterSpecies;

export function getMoveById(moveId: string): Move;

export function createMonsterInstance(
  speciesId: string,
  level: number
): MonsterInstance;

export function calculateDamage(
  attacker: MonsterInstance,
  defender: MonsterInstance,
  move: Move
): number;

export function calculateCaptureChance(
  wildMonster: MonsterInstance,
  species: MonsterSpecies
): number;

export function chooseWildEncounter(
  encounterTable: EncounterTable
): MonsterInstance;
```