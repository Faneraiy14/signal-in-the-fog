# GAME_SPEC — Signal in the Fog

## One-screen brief
- **Genre / camera:** First-person psychological survival horror; landscape mobile 3D.
- **Player fantasy:** Mara Voss explores an abandoned mountain relay station where radio information is useful but dangerous.
- **Core loop:** Explore → use flashlight and radio → tune a relay → repair under exposure → hide/retreat → unlock the next chapter.
- **Primary verbs:** Move/look, interact/repair, tune signal, hide, manage flashlight/radio.
- **World layout:** Three connected authored chapters: Gatehouse, Service Tunnels, Summit Array.
- **Threat:** Fog Listener reacts to active broadcasts, pursues through authored corridors, and is survived through silence and hiding.
- **Progression:** Relay 01 teaches signal risk; Relay 02 adds pursuit and spatial distortion; Relay 03 enables two endings.
- **Win states:** Complete Relay 03 and choose Sever or eligible Answer ending.
- **Lose state:** Threat exposure reaches 100; reload exact checkpoint state.
- **Target run:** 25–45 minutes; 3-minute validation slice must show exploration, signal risk, and recovery.
- **Platform:** Android APK, offline-first, Unity URP, 30 FPS on mid-range devices.

## Prototype validation target
Before final asset passes, prove one compact relay room with touch movement/look, flashlight/radio state, frequency tuning, repair hold, threat response, hide, checkpoint reload, pause, and a reachable win/lose result.

## Content floor
- 5 meaningful player verbs/states: move/look, flashlight, tune, repair, hide.
- 3 authored relay/puzzle variants, one per chapter.
- 3 battery pickups plus 6 narrative clues.
- 3 encounter beats: first signal reveal, tunnel pursuit, summit confrontation.
- 1 progression/escalation: chapter rules and ending eligibility.
- Start, win, lose, restart checkpoint, pause, settings, subtitles, reduced-flash feedback.

## Asset replacement plan
- Player-critical: first-person hands/flashlight and rugged meter presentation.
- Level: relay station structural kit, tunnel pieces, summit array, fog volumes.
- Props: relay cabinets, fuses, tapes, lockers, doors, battery pickups, antenna console.
- Threat: Fog Listener silhouette and wet blue-green material/VFX.
- Audio/UI: radio static, adaptive threat beds, subtitle system, amber waveform theme.
- Greybox stand-ins are temporary only; every visible final slice gets a replacement or an explicit intentional procedural-geometry decision.
