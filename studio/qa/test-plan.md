# QA and Release Validation Plan

## Pre-runtime checks
- Confirm ledger files and source-of-truth design documents exist.
- Confirm Unity project imports and compiles cleanly.
- Confirm build scenes, input actions, UI documents, chapter data, and save schema references are non-null.
- Confirm APK target settings, landscape orientation, package id, and offline assumptions.

## Runtime smoke after consent
- Start from the title screen using the real entry path.
- Use touch/editor fallback to move, look, toggle flashlight, tune radio, complete a relay repair, and enter/exit hide.
- Verify threat state, exposure, feedback, pause, checkpoint restart, chapter transition, and one ending path.
- Read diagnostics after each interaction; capture only the necessary gameplay evidence.

## Asset/scene checks
- Validate grounding, orientation, scale, materials, colliders, and mobile readability in each chapter.
- No blocking graybox, default-gray UI, magenta material, missing reference, or T-pose remains.

## Android checks
- Build a debug APK.
- Inspect artifact existence, size, package identity, and build output.
- Install/launch on an available Android validation path when available; otherwise record the exact missing device/ADB limitation.

## Release gates
- Blocking matrix rows are green.
- `OPEN_TASKS.md` contains no blocking work.
- APK artifact is present and source tree is ready for GitHub publication.
