# Signal in the Fog

First-person psychological survival horror for Android.

You play as emergency technician Mara Voss, investigating an abandoned mountain relay station after a distress call that uses her missing brother's call sign. The radio is the most useful tool in the game and the most dangerous one: it reveals clues and relay frequencies, but it also drains the battery and attracts the Fog Listener.

## Current contents

This repository currently contains:

- Game concept, story, art, audio, and system design documents in `studio/`
- Unity 6 project scaffold in `unity/`
- Production ledger in `.seele-game/`
- Project handoff notes in `agent/`

Custom gameplay scenes, audio, 3D assets, and an APK have not been authored yet. The next implementation step is the Gatehouse greybox: touch movement, flashlight, radio tuning, relay repair, hiding, and checkpoint restart.

## Planned game

- Platform: Android APK, landscape, offline
- Engine: Unity 6, URP, 3D
- Chapters: Gatehouse, Service Tunnels, Summit Array
- Endings: Sever the Signal, Answer the Call
- No combat. Survival comes from listening, hiding, and deciding when to broadcast.

## Repository layout

```text
studio/          design, architecture, QA
unity/           Unity project
.seele-game/     production ledger
agent/           project status and changelog
```

## Status

The design package is complete. Unity editor startup in the original production environment was blocked by a missing license activation path. This snapshot preserves all current source so later sessions can continue from the same tree.
