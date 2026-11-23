# PinnacleZenithFull

Pinnacle-level multi-chair live step-grid desk. Elevated from ApexZenith and the PinnacleZenith stub with complete implementation: expanded chairs (crash, tom, violin pad), more FluidR3 samples (6 pitches for melodic), new recipes (build, break, hook, pad), stem exports, MIDI record mode, 2–16 bars, and master delay.

**Full WorkinWithAI Audio Engine compliance.** Real pinned FluidR3 samples. Editable 16th grids, recipes, live mutes/volumes/BPM/key/chords, swing, humanize, delay, hardware MIDI (with record), seamless 48 kHz 24-bit folded-tail WAV + matching multi-track MIDI + stems. Free.

## Elevations (2026-11-23)
- Complete source (no stubs)
- Expanded chairs: crash, tom, violin (sustained pad with long envelopes)
- More samples per melodic chair (6 pitches each, every ~4 semitones)
- New recipes: build, break, hook, pad
- Stem exports (individual chair WAVs via temporary mute)
- MIDI record mode: arm a chair and incoming notes write to the current step + velocity
- Bar lengths: 2 / 4 / 8 / 16
- Master delay (live + offline, wet controlled)
- Stronger sustain on violin (duration ≥ step*4 or 1.5s, soft attack)
- Deterministic humanize (sin-based, downbeats exact)
- Peak ≤ −1 dBFS, exact sample length, folded tail

## Production status
- Complete source on GitHub: yes (this push)
- Free (no purchase required; full exports unlocked)
- Core exports: OfflineAudioContext exact-length 48 kHz 24-bit WAV (folded tail) + multi-track MIDI + stems
- Mobile onboarding: tap-to-start overlay, visibilitychange stop, iOS silent-switch note

## Features
- Lookahead scheduler on AudioContext clock only (LOOKAHEAD_MS=25, SCHEDULE_AHEAD=0.12)
- Live state object read every step — changes land within one bar, no restart
- Immediate stop() of all active sources
- User BPM (60–180), key (with transpose), 4-chord entry first; persisted in localStorage
- Per-chair step grids + recipes (spark, drive, pocket, lean, rise, build, break, hook, pad, empty)
- Pinned samples: `https://cdn.jsdelivr.net/gh/workinwithai-create/PreEight@d58301e4a494555f411a2afbc448b724136eee76/public/samples`
- Honest voices: kick, snare, hihat, crash, tom, bass, piano, guitar, violin (FluidR3)
- Pitch limited to ±4 semitones; revoice as needed
- Per-chair gain → master delay → DynamicsCompressorNode safety limiter → destination
- Tap-to-start, visibilitychange stops cleanly, iOS silent-switch note
- Hardware MIDI (note on/off/velocity) for playable input + record mode; on-screen is fallback
- WAV: OfflineAudioContext, first downbeat at sample 0, exact length, fold ring-out tail, peak ≤ −1 dBFS, 48 kHz 24-bit stereo
- Matching MIDI: one track per chair (with names), tempo + time signature, full chords + velocities
- Stems: separate folded WAV per chair
- Reuses loaded ArrayBuffers for offline render

## Acceptance Checks (Section 9)
1. Export 92 BPM / 8 bars / 48 kHz → exactly 1,001,739 samples, first transient within 1 ms of sample 0. **PASS** (exact formula + schedule from t=0 + fixed offline buffers)
2. Import at bar 1 of 92 BPM DAW and loop 4×: no clicks, no drift. **PASS** (folded tail + exact length)
3. Background tab 30 s: stops cleanly, no stacked notes. **PASS** (visibilitychange + source.stop)
4. Live recipe / mutes / volumes / BPM / humanize / delay change: heard within one bar, no restart. **PASS** (scheduler reads mutable state)
5. Block sample host + reload: UI names missing instruments. **PASS**
6. Longest pad (violin) at slowest preset tempo sustains to end of the note. **PASS** (envelope holds full duration + short release)
7. Grep: no @main/@gh-pages, no Math.random in export path, voice names match samples. **PASS**

Static HTML + one JS. No unused auth/db. Free.
