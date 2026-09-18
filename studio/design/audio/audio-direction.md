# Signal in the Fog — Audio Direction

> Last Updated: 2026-04-29

## 1. Audio Identity Statement

All important sound should feel like a real emergency station heard through weather, wire, and distance. The radio is not a music player; it is the game’s second camera. Human audio is dry, close, and procedural. The Listener is wet, phase-shifted, and slightly delayed.

Supporting principles:
- Gameplay-critical information always has a visual partner; audio creates urgency, not hidden mandatory knowledge.
- Silence is an authored state, not an empty mix. When the signal cuts out, leave a deliberate noise floor.
- Touch actions receive short, tactile audio feedback within 0.5 seconds.

## 2. State Emotion

| State | Music Energy | Rhythm | Sound Palette | Visual Alignment |
|---|---:|---|---|---|
| Exploration | 0.1–0.2 | sparse, irregular | wind, cable hum, distant metal, low radio hiss | cool fog and amber pools |
| Signal scan | 0.3–0.5 | pulsed interference | filtered voice, tuning clicks, waveform pings | amber scan pulse |
| Threat pursuit | 0.6–0.9 | unstable low throb | reversed footsteps, wet resonance, clipped voice tails | teal distortion and readable directional cue |
| Safe room | 0.2 | steady transformer hum | close room tone, warm relay ticks | stable amber light |
| Sever ending | 0.0 | no beat | breath, wind, final relay click | dawn gray |
| Answer ending | 0.4 | slow repeating pulse | layered voices, widening stereo field | blue-green bloom |

## 3. Music Direction

Use adaptive stems rather than a long melodic score: weather bed, relay hum, low pulse, signal shimmer, and ending pad. Exploration loops should crossfade into scan and threat states without hard cuts. No music is used during the first radio revelation; the voice and station ambience must carry the moment.

Reference palette: bowed metal, prepared piano harmonics, granular radio noise, low modular pulse. Avoid heroic strings, jump-scare cymbal hits, and genre clichés.

## 4. SFX Philosophy

- Interactions: mechanical click + amber confirmation tick.
- Battery pickup: short ascending two-note pulse with a tactile vibration.
- Relay repair: layered switch, motor, and distant station-wide power bloom.
- Threat proximity: directional wet scrape, always paired with a subtle teal edge cue.
- Damage/failure: low heartbeat, screen vignette, and explicit UI label.
- UI: dry, quiet, no glossy sci-fi bleeps.

## 5. Mix Priority

Gameplay-critical directional cues > subtitles/voice > interaction confirmation > music stems > ambient weather. Duck music by 6dB during radio voice and by 10dB during threat proximity. Never duck the threat cue so far that it becomes inaudible on mobile speakers.

## 6. Accessibility Hooks

- Separate Music, SFX, Voice, and UI volume sliders.
- 100% of story voice has subtitles.
- Threat direction is represented by a waveform edge indicator and a proximity icon.
- Reduced-flash mode removes rapid flicker and replaces it with a low-frequency brightness pulse.
- The player can finish the game without sound by using subtitles, UI direction cues, and visible waveform state.
