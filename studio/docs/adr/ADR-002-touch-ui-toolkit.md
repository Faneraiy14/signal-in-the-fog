# ADR-002 — Touch input and UI Toolkit

## Status
Accepted

## Decision
Use Unity Input System actions plus UI Toolkit touch controls. Touch controls and hardware/editor fallbacks emit the same normalized commands; gameplay does not read UI elements directly.

## Rationale
The Android target requires reliable touch input, while shared commands keep editor smoke tests and mobile runtime behavior aligned. UI Toolkit provides a single themed presentation layer for HUD, pause, settings, subtitles, and endings.

## Consequences
- Buttons must be at least 96 dp and remain visible over fog.
- Input focus and pointer ownership are validation targets.
- Desktop keyboard/mouse is a development fallback, not the shipped control contract.
