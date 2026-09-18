# PROJECT.md

## Project Overview
- Project Name: Signal in the Fog
- Goal: Complete mobile psychological horror game for Android APK.
- Current Stage: Phase 3 — Tech Architecture.

## Technology Stack
- Engine: Unity 6, 3D URP.
- Platform: Android, landscape, offline-first.
- Runtime: UI Toolkit, Unity Input System, versioned local JSON save.

## Running / Build Methods
- Project creation and editor operations use the Unity editor bridge workflow.
- Validate by opening the Bootstrap scene, compiling, and running the project-specific validation matrix.
- Build target is a debug APK for local validation; release signing depends on available credentials.

## Directory Structure
- `unity/`: Unity 6 engine project containing `Assets/`, `Packages/`, and `ProjectSettings/`; it is the editor-bridge workspace.
- `studio/`: durable design, architecture, QA, and release documents.
- `game/`: game-support assets and non-Unity working files.
- `agent/`: project handoff docs.
- `.seele-game/`: production ledger and validation gates.

## Core Modules
- Game State: chapter phases, transitions, pause, win/lose, endings.
- Signal Relay: tuning, repair, signal events.
- Battery: float resource and pickup state.
- Fog Listener: authored threat state machine, hiding, exposure.
- Narrative: clues, subtitles, ending eligibility.
- UI/Audio/Save: presentation, accessibility, and offline persistence.

## Critical Reference Relationships
- Registry → chapter data: shared IDs, frequencies, pickups, hide volumes.
- Game State → all systems: read-only phase and transition events.
- Save → serialized state only: no scene references.
- UI → public commands: no direct gameplay state mutation.

## Architectural Constraints
- No combat loop or network dependency.
- Android touch is the shipped input contract; desktop input is fallback only.
- Visible final assets must be integrated and validated in context.
- No hand-edited Unity YAML; author engine objects through the editor workflow.
