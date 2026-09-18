# Systems Index: Signal in the Fog

> **Status**: Approved
> **Created**: 2026-04-29
> **Last Updated**: 2026-04-29
> **Source Concept**: design/gdd/game-concept.md

## Overview

The game is a finite first-person mobile horror exploration experience. The implementation must support one authored session across three connected chapters, a signal-risk loop, an avoidable threat, a small set of contextual interactions, two endings, and touch-first presentation. No system may add combat, crafting, or online dependencies that weaken the information-is-dangerous pillar.

## System Inventory

| # | System | Category | Priority | Status | Design Document | Depends On |
|---|---|---|---|---|---|---|
| 1 | Input and Touch Controls | Core | MVP | Approved | systems/input-touch-controls.md | Unity Input System |
| 2 | Player Locomotion and Camera | Core | MVP | Approved | systems/player-locomotion-camera.md | Input and Touch Controls |
| 3 | Chapter and Game State | Core | MVP | Approved | systems/chapter-game-state.md | Player Locomotion |
| 4 | Signal Tuning and Relay Interaction | Gameplay | MVP | Approved | systems/signal-tuning-relay.md | Input, Chapter State, Battery |
| 5 | Fog Listener Threat | Gameplay | MVP | Approved | systems/fog-listener-threat.md | Chapter State, Signal Relay |
| 6 | Battery and Resource Pressure | Progression | Vertical Slice | Approved | systems/battery-resource-pressure.md | Signal Relay |
| 7 | Narrative Clues and Endings | Narrative | Vertical Slice | Approved | systems/narrative-clues-endings.md | Chapter State, Signal Relay |
| 8 | Touch HUD, Settings, and Subtitles | UI | MVP | Approved | systems/touch-hud-settings.md | All gameplay read-only |
| 9 | Audio and Feedback | Audio | MVP | Approved | systems/audio-feedback.md | Signal Relay, Threat, UI |
| 10 | Local Save and Resume | Persistence | Vertical Slice | Approved | systems/local-save-resume.md | Chapter State, Settings |

## Categories

- **Core:** input, movement, camera, scene/state flow.
- **Gameplay:** signal, relay, threat, resource pressure.
- **Narrative:** clue delivery and ending choice.
- **UI:** touch affordances, HUD, settings, subtitles.
- **Audio:** state-aware ambience and readable feedback.
- **Persistence:** local settings and chapter resume.

## Priority Tiers

- **MVP:** systems required to test the central signal-risk loop and reach a win/lose result.
- **Vertical Slice:** systems required to make the three-chapter story feel complete.
- **Alpha:** reserved for randomized clue/battery placement and replay variants.
- **Full Vision:** future challenge mode, additional anomaly types, and expanded endings.

## Dependency Order

### Foundation
1. Input and Touch Controls — owns touch actions and device sensitivity.
2. Chapter and Game State — owns active chapter, pause, restart, win, lose, and ending state.

### Core
3. Player Locomotion and Camera — consumes touch input and publishes player pose.
4. Signal Tuning and Relay Interaction — consumes touch interaction and owns relay progress.

### Feature
5. Battery and Resource Pressure — owns battery state and exposes read-only availability.
6. Fog Listener Threat — consumes signal and chapter events; never writes battery directly.
7. Narrative Clues and Endings — consumes relay and tape events; owns story flags.

### Presentation
8. Touch HUD, Settings, and Subtitles — reads state and emits UI commands only.
9. Audio and Feedback — listens to events and reads state; owns no gameplay state.
10. Local Save and Resume — serializes state from the state owner; never mutates gameplay during play.

## Cross-System Contracts

- Input owns touch actions; all other systems consume normalized commands.
- Chapter State owns `activeChapter`, `gamePhase`, `endingChoice`, and restart transitions.
- Signal Relay owns `signalMode`, `currentFrequency`, `relayProgress`, and emits `SignalStarted`, `SignalLost`, `RelayRepaired`.
- Battery Resource owns `batteryPercent`, `batteryCharges`, and emits `BatteryLow`, `BatteryEmpty`; it reads signal drain intent but does not let the threat mutate battery.
- Fog Listener owns threat state, target selection, patrol anchor, and damage/failure requests; Chapter State owns the final lose transition.
- Narrative owns `tapeFlags`, `trueMemoryCount`, and ending eligibility; it reads relay completion and tape collection.
- HUD reads all public state and emits commands to Input/Chapter/Settings. HUD never writes gameplay state directly.
- Audio/VFX listens to named events and presents feedback; it cannot gate progress.

## Recommended Design Order

| Order | System | Priority | Layer | Workload |
|---:|---|---|---|---|
| 1 | Input and Touch Controls | MVP | Foundation | M |
| 2 | Chapter and Game State | MVP | Foundation | M |
| 3 | Player Locomotion and Camera | MVP | Core | M |
| 4 | Signal Tuning and Relay Interaction | MVP | Core | L |
| 5 | Battery and Resource Pressure | Vertical Slice | Feature | S |
| 6 | Fog Listener Threat | MVP | Feature | L |
| 7 | Narrative Clues and Endings | Vertical Slice | Feature | M |
| 8 | Touch HUD, Settings, and Subtitles | MVP | Presentation | M |
| 9 | Audio and Feedback | MVP | Presentation | M |
| 10 | Local Save and Resume | Vertical Slice | Presentation | S |

## Cyclic Dependencies

The signal system and threat system form a behavioral loop: signal reveals threat information, and signal use attracts threat pressure. Architecturally, the dependency is one-way through events: Signal Relay emits signal state/events; Fog Listener consumes them and emits threat events; HUD/Audio consume both. The threat never calls Relay methods directly.

## High-risk Systems

| System | Risk | Mitigation |
|---|---|---|
| Touch Controls | Camera movement may feel imprecise on phones | Sensitivity slider, dead zone, generous interaction cones, editor touch simulation |
| Signal Relay | Radio puzzle may become opaque | Always show frequency band, audio/visual confirmation, and one nearby clue |
| Fog Listener | AI may feel random or unfair | Authored patrol anchors, telegraphed proximity cues, safe-room recovery beats |
| Mobile Lighting | Fog and shadows may exceed budget | URP, baked lights, capped real-time lights, reduced-flash mode |

## Progress Tracking

| Metric | Count |
|---|---:|
| Systems identified | 10 |
| MVP systems | 8 |
| Vertical Slice systems | 2 |
| System GDDs started | 10 |
| System GDDs approved | 10 |
| Cross-system review | Complete |
