# DECISIONS — Signal in the Fog

## ADR seeds
- Full production selected over lite because the user explicitly requested a complete phone horror game and APK deliverable.
- Unity 3D selected for Android input, URP mobile lighting, and APK export.
- The game is finite and authored: three chapters, one non-combat threat, two endings.
- Battery uses float storage with rounded HUD display.
- Relay repair is the sole chapter-completion trigger; narrative beats after repair are presentation-only.
- Checkpoint restart restores exact serialized resource and collected-state values.
- Final UI is UI Toolkit-oriented and must provide visual equivalents for audio-only threats.

## Change rule
Any scope reduction that changes the release slice, content floor, platform, or authored ending contract must be recorded here before implementation continues.
