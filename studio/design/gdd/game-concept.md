# Game Concept: Signal in the Fog

*Created: 2026-04-29*
*Status: Approved*

## Elevator Pitch

**Signal in the Fog** is a first-person mobile horror exploration game set in an abandoned mountain relay station. You investigate a distress transmission, restore three signal relays, and descend into the fog while managing a flashlight, limited batteries, and a creature that only becomes visible when the signal is active. The goal is to survive long enough to discover who is transmitting—and decide whether to answer.

## Core Identity

| Aspect | Detail |
|---|---|
| Genre | First-person psychological survival horror / exploration |
| Platform | Android APK, landscape |
| Target Audience | Players who want a tense 20–40 minute horror session with readable touch controls |
| Player Count | Single-player |
| Session Length | 25–45 minutes per complete run |
| Monetization | None for the prototype/release candidate |
| Estimated Scope | Full vertical-slice production: 3 connected chapters, 1 central antagonist, 10 coordinated systems |
| Comparable Titles | Stories Untold (signal-driven unease), Alien: Isolation (threat discipline), Oxenfree (radio as narrative interface) |

## Core Fantasy

You are a lone emergency technician entering a place where the radio is the only thing that still answers. Every time you repair the station, you make the unseen presence more real—and every time you turn the signal off, you lose the one tool that can guide you.

## Unique Hook

It is like a first-person exploration horror game, **and also** the supernatural threat can only be tracked through the radio signal: tuning the frequency reveals clues and the creature’s position, but broadcasts your location and drains the battery.

## MDA Analysis

### Target Aesthetics

| Aesthetic | Priority | How We Deliver It |
|---|---:|---|
| Sensation | 1 | Fog, low-frequency radio noise, touch flashlight, sudden loss of orientation |
| Discovery | 2 | Signal fragments, hidden relay rooms, environmental contradictions |
| Narrative | 3 | Three chapters, radio logs, the unresolved identity of the caller |
| Challenge | 4 | Battery pressure, route decisions, hiding, timing relay repairs |
| Fantasy | 5 | Being the last technician in a dead mountain station |
| Fellowship | N/A | Single-player loneliness is intentional |
| Expression | N/A | No character build; expression is through route and ending choice |
| Submission | N/A | Sustained tension, not relaxation |

**Lead aesthetic:** Sensation — the player should feel that the phone itself has become a fragile instrument inside the horror.

### Key Dynamics

- Players switch between signal-on for information and signal-off for safety.
- Players create short safe windows by hiding, powering doors, and planning battery use.
- Players read environmental inconsistencies before the game confirms supernatural events.
- Players choose whether to investigate optional transmissions or rush toward the exit.

### Core Mechanics

1. First-person touch locomotion and camera look.
2. Diegetic flashlight with battery drain and recharge pickups.
3. Radio frequency tuning that reveals objectives, clues, and threat proximity.
4. Contextual interactions: repair relay, collect tape, unlock gate, hide.
5. Threat state: the Fog Listener patrols, reacts to signal use, and forces hiding or retreat.
6. Chapter progression with win, loss, restart, and two ending variants.

## Player Motivation

| Need | Delivery | Strength |
|---|---|---|
| Autonomy | Choose signal routes, optional tapes, and final answer/escape decision | Core |
| Competence | Learn the creature’s audio/visual rules and manage scarce batteries | Core |
| Relatedness | The caller’s voice creates a bond that becomes morally uncertain | Supporting |

### Player Types

- **Explorers:** hidden relay rooms, contradictory logs, frequency secrets.
- **Achievers:** collect all six tapes and unlock the true ending.
- **Immersion-focused players:** atmosphere, environmental storytelling, and audio cues.
- Not aimed at competitive players or combat-first audiences.

### Flow Plan

- Onboarding: Chapter 1 teaches movement, flashlight, interaction, and one safe radio scan without explaining the creature.
- Difficulty curve: each chapter adds one new rule, then gives a recovery beat before the next escalation.
- Feedback clarity: every interaction has a sound, UI pulse, light change, or world-state change within 0.5 seconds.
- Failure recovery: restart returns to the current chapter checkpoint, preserving the checkpoint's exact battery value and collected state; it does not reset the whole game.

## Core Loop

### 30-second loop
Move through fog → use flashlight to read the space → tap to inspect or tune the radio → hear/see a clue → choose whether to stay exposed or retreat.

### 5–15 minute loop
Locate a relay room → gather a fuse and battery → tune the correct signal → repair the relay → survive the creature’s response → unlock the next path.

### Full-session loop
Arrive at the station → restore Relay 01 and learn the rules → restore Relay 02 while the creature becomes active → descend to Relay 03 and confront the caller → choose to answer or sever the signal.

### Long-term hook
Optional tape collection, two endings, and a New Signal mode that randomizes clue order and battery placement without changing the authored story.

## Game Pillars

### Pillar 1: Information Is Dangerous
The best clue is also a beacon. If a mechanic gives the player knowledge, it must carry exposure risk.
*Design test:* if choosing to use the radio has no downside, add threat pressure or battery cost.

### Pillar 2: The World Is the Puzzle
The player solves space, sound, and contradictions—not abstract lock-and-key menus.
*Design test:* every key item must be foreshadowed by a spatial or audio clue.

### Pillar 3: Fear Needs Recovery
Every major scare is followed by a quiet, readable beat so tension can rebuild rather than flatten.
*Design test:* do not chain high-intensity events without a safe landmark or battery opportunity.

### Anti-Pillars

- **Not a combat shooter:** the creature is avoided, not killed.
- **Not an inventory simulator:** maximum carried items are three; context handles use.
- **Not a jumpscare reel:** scares change the player’s understanding of the space.
- **Not an endless runner:** the story has three authored chapters and a final choice.

## Visual Identity Anchor

**The Amber Static Mountain** — every safe human-made signal uses a warm amber source, while every supernatural distortion uses a desaturated blue-green haze. The world is made from damp painted metal, salt-stained concrete, and old analog equipment. The radio waveform is the only repeating graphic motif across world, HUD, and chapter transitions.

## Story and Level Summary

1. **Chapter 1 — The Gatehouse:** arrive during a storm, restore the first relay, find the first tape, and hear the caller say your name.
2. **Chapter 2 — The Service Tunnels:** descend through maintenance corridors, restore the second relay, learn the Fog Listener follows the signal rather than the player.
3. **Chapter 3 — The Summit Array:** reach the antenna chamber, decide whether to transmit the final response, then escape or remain connected for the alternate ending.

## Technical Considerations

| Consideration | Assessment |
|---|---|
| Recommended Engine | Unity for Android input, URP lighting, APK export, and mobile performance tooling |
| Key Technical Challenges | Touch-first FPS controls, stable fog/lighting on mobile, threat state clarity, Android audio focus |
| Art Style | Stylized grounded 3D: low-poly silhouettes with selective high-contrast materials |
| Art Pipeline Complexity | Medium; procedural structural geometry plus a small authored prop set |
| Audio Needs | High; ambience, radio voice, directional threat cues, and accessibility fallback indicators |
| Networking | None |
| Content Volume | 3 chapters, 6 tapes, 3 relay puzzles, 1 threat, 2 endings |
| Procedural Systems | Optional battery/clue placement variation only after authored route validation |

## Risks and Open Questions

- Mobile fog and post-processing may vary across GPUs; use layered fog volumes and a reduced-flash fallback.
- Touch camera control can make precise inspection tiring; add generous interaction cones and a sensitivity slider.
- The threat must feel present without requiring expensive AI; use authored patrol anchors with a simple state machine.

## Full-production Release Slice

The first complete release slice includes the three chapters, the authored story, the threat loop, the two ending states, the settings panel, pause/restart flow, and an Android APK. Future expansions may add a fourth chapter, more signal anomalies, and a challenge mode.

## Next Steps

- [x] `setup-engine` — lock Unity 3D Android target
- [x] `art-bible` — author the visual identity
- [x] `narrative-design` — author world, characters, and story beats
- [x] `audio-direction` — define radio and threat audio rules
- [x] `map-systems` — map implementation systems and dependencies
- [ ] Phase 2 — write and approve each system GDD
- [ ] Phase 3 — write architecture and accessibility requirements
- [ ] Phase 4 — author UX, asset specification, greybox, epics, and stories
