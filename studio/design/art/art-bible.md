# Signal in the Fog — Art Bible

## Document Status
- **Version**: 1.0
- **Last Updated**: 2026-04-29
- **Status**: Approved

## 1. Visual Identity Statement

**The Amber Static Mountain:** a damp, low-poly industrial mountain station where warm human signal light is surrounded by cold blue-green fog. Human spaces are legible and geometric; supernatural spaces are subtly misaligned, stretched, or repeated. The player should recognize the game from amber equipment glow, wet charcoal surfaces, radio waveform accents, and the yellow storm jacket.

Supporting principles:
- Human objects are warm, worn, and rectangular; supernatural distortion is smooth, vertical, and slightly too tall. Pillar: The World Is the Puzzle. Test: a clue prop must read from silhouette before close inspection.
- Darkness hides information but never hides basic navigation. Pillar: Fear Needs Recovery. Test: every danger beat retains a readable amber landmark or UI cue.
- The radio waveform is the only repeated graphic motif. Pillar: Information Is Dangerous. Test: waveform use must imply either knowledge or exposure.

## 2. Mood by Game State

| State | Emotion | Lighting | Keywords | Energy |
|---|---|---|---|---|
| Exploration | wary curiosity | cool ambient fill, isolated amber practicals, high negative space | damp, patient, distant, listening | low |
| Signal scan | focused exposure | amber waveform pulse against blue-green fog, slight vignette | revealed, vulnerable, narrow, alert | medium |
| Threat pursuit | panic with readable choices | cold contrast, moving shadow bands, reduced saturation, no constant strobe | wet, close, wrong, breathless | high |
| Safe room | temporary relief | stable amber pool, visible floor contact, warmer midtones | procedural, grounded, shelter, memory | low-medium |
| Ending | grief or surrender | Sever: pale dawn gray; Answer: blue-green signal bloom | final, quiet, unresolved, open | low |
| Menu/pause | control | flat charcoal background with amber waveform line | archival, restrained, legible | low |

## 3. Shape Language

- Player silhouette: compact, grounded, yellow shoulder/sleeve accent and rugged meter silhouette.
- Threat silhouette: narrow waist, overlong limbs, head motion that resembles a tuning needle.
- Environment geometry: modular 2.5m industrial bays, 90-degree service corridors, rounded cable bundles, bent antenna elements.
- UI: hard rectangular panels with one waveform notch; no glossy sci-fi glass.

## 4. Color System

| Name | Hex | Meaning / Use |
|---|---|---|
| Wet Charcoal | #12161A | primary world surfaces and UI background |
| Iron Gray | #39434A | readable structural planes |
| Signal Amber | #E6A34A | safe interaction, human equipment, objective confirmation |
| Fog Teal | #3D7275 | supernatural distortion and threat proximity |
| Warning Ivory | #F0E6D1 | subtitles and high-contrast instructions |
| Emergency Red | #C8544B | damage, low battery, irreversible warning; always paired with icon/shape |
| Dawn Gray | #A9B0AE | escape ending and release state |

UI palette uses luminance contrast rather than hue alone: amber objective tags include a square icon; red warnings include a pulse and triangle; teal threat cues include a waveform and audio-direction indicator.

## 5. Character Direction

- Player: no visible face; hands/forearm only for flashlight and meter. Use a simple, animated hand rig or silhouette proxy at first, then a low-poly glove/forearm asset.
- Fog Listener: never show a detailed face; preserve a strong silhouette and surface reflection. Near-camera detail is reserved for one authored reveal.
- LOD: threat keeps silhouette shape at distance; small surface details are dropped before the torso/head silhouette.

## 6. Environment Direction

The station is late-1990s emergency infrastructure: galvanized panels, concrete, orange cable, wet glass, analog meters, faded safety paint. Art shows weathering where it explains history: water streaks, salt lines, frost, hand marks, and emergency labels. Density is high in inhabited workspaces and low in the fog-facing relay chambers.

Texture philosophy: stylized PBR with restrained roughness variation; no photoreal 4K. Use trim sheets and vertex color grime where possible. Story is placed in objects: a chair facing the wrong way, a logged frequency repeated by hand, a broken emergency lamp that still warms one wall.

## 7. UI/HUD Direction

- Use UI Toolkit with a charcoal panel, thin amber waveform rule, and plain high-contrast sans-serif body text.
- Diegetic meter overlay carries frequency, battery, and threat direction; screen-space prompts are reserved for touch affordances and subtitles.
- Buttons are large enough for thumb targets, with pressed-state inversion and vibration option.
- Motion is restrained: waveform scan, 120ms panel fade, no constant shake. Reduced-flash mode removes flicker and replaces it with brightness breathing.
- Body text must maintain at least 4.5:1 contrast and never rely on red/green alone.

## 8. Asset Standards

Naming: `[category]_[name]_[variant]_[size].[ext]`.

| Category | Max | Format | Notes |
|---|---:|---|---|
| Characters | 1K textures | FBX/GLB + PNG | low-poly, 1–2 materials, LOD near/far |
| Environment | 1K textures | FBX/GLB/PNG | modular, grounded pivots, simple colliders |
| UI | 512px | SVG/PNG/UXML/USS | theme elements only, no default gray |
| VFX | 512px | Particle/VFX Graph | additive fog wisps, signal distortion, reduced-flash fallback |
| Audio | 44.1kHz mono/stereo | WAV/OGG | short mobile-friendly loops and one-shots |

Target 30 FPS on mid-range Android; prioritize silhouette, lighting, and readable placement over mesh density.

## 9. Reference Directions

| Reference | Medium | Take | Avoid / Transform |
|---|---|---|---|
| Stories Untold | Game | analog terminals as narrative objects and readable text fragments | avoid copying interface layouts; use the waveform as our own motif |
| Alien: Isolation | Game | threat anticipation, sound-led navigation, recovery beats | avoid combat and industrial scale; keep the station compact and authored |
| Stalker-like abandoned infrastructure | Film/game mood | damp materials, distant lights, weathered utility spaces | avoid post-apocalyptic sprawl; the station remains a functioning technical place |
| Early emergency broadcast rooms | Real-world | practical amber indicators, labels, cable density | avoid retro fetishism; keep objects tied to gameplay clues |

## Production Gate

A scene passes visual review when the player silhouette reads, the UI has the amber/waveform theme, the environment has depth and grounded contact, the lighting carries mood without hiding navigation, and all visible direction agrees with the Amber Static Mountain identity.
