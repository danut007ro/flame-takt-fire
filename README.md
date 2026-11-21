# Flame FIRE and TAKT: unofficial custom firmware

Unofficial firmware for two Flame modules:

| Module | Based on | Details |
| --- | --- | --- |
| **FIRE** | stock v1.07 | [FIRE.md](FIRE.md) |
| **TAKT** | stock v1.7.2 | [TAKT.md](TAKT.md) |

> **Warning:** Flame does not support this firmware. Back up your kits and scenes before flashing. Use it at your own risk.

Both builds are tested on hardware. Feedback and bug reports are welcome (open an issue).

## Files

| File | Purpose |
| --- | --- |
| `FlameFireV1_07_custom.syx` | FIRE custom firmware |
| `smp5_42k_sample5.syx` | FIRE hihat sample 5 |
| `smp6_37k_sample6.syx` | FIRE hihat sample 6 |
| `smp7_32k_sample7.syx` | FIRE hihat sample 7 |
| `smp8_25k_sample8.syx` | FIRE hihat sample 8 |
| `FlameTaktV1_7_2_custom.syx` | TAKT custom firmware |

## Highlights

**FIRE** (details in [FIRE.md](FIRE.md)):

- **Velocity and CV at the same time:** every parameter has one amount for velocity and one for CV, and both stay active. A voice can have velocity dynamics and an LFO on the same jack.
- **CV matrix:** CV1–CV4 can modulate instruments 1–4 together (CV5–CV8 for instruments 5–8). One CV can drive several instruments, and one instrument can take four CVs plus velocity.
- **Randomize:** hold A or B and press SETUP to nudge every parameter of that part by up to ±15%. Hold CV and press SETUP to do the same for the CV amounts of one input.
- **Four extra hihat samples:** upload your own samples to slots smp5–smp8 and pick them with `mtSel`. The factory samples are untouched.
- **New MODAL and SHAKERS algorithms:** Plaits' modal voice (bars, bells, plates) and Lyle Mills' shakers (16 shaken, scraped and dripping instruments from Perry Cook's models), added after the last stock algorithm.
- **Drive types:** a `dType` knob next to `drive` (snare, kick, T-BRIDGE, rimshot, tom, xCLAP): stock, hard clip, wavefolder, asymmetric and two-stage, blended in between and modulatable by velocity and CV.
- **FM-DRUM drive:** FM-DRUM gets `drive` and `dType`.
- **Momentary edit:** hold MORPH on page A, B or the CV menu, twist knobs, let go and the whole kit (parameters and CV / matrix / morph amounts) glides back. MORPH + MASTER latches it (A, B and other instruments), MORPH + VOLUME keeps the tweak. While latched, MORPH leaves the latch at once, VOLUME + MORPH keeps the tweak and MASTER + MORPH opens the MORPH screen.
- **Offset knob mode:** a third knob mode, `offs`, next to `pick` and `jump`. Knobs work relative to the value from wherever they are: no jumps and no hunting for the value. Hold PANNING as a clutch to reposition knobs without changing anything; while it's held, each bar shows where the knob is, so you can line knobs up with their values.
- **Pick marker:** in `pick` mode each value bar shows where the knob is (a gap in the line), and turns 2 pixels high for 400 ms the moment the knob reaches its value and takes over.
- **Main plus direct outs together:** the M1–M6 settings play an instrument on the main mix and on a direct out at the same time. Several instruments can share one direct out.
- **Knob recording:** hold A (or B) and turn knobs. With MIDI clock (for example from the TAKT) the movement is recorded in 16ths counted from your A / B press (press at the start of a bar, turn late in the bar, and the loop keeps the old value until then), looping on the bar grid, a quarter bar up to 4 bars, following Start and Stop. Tap FIRE while holding to end a loop at any length, for polyrhythms. Without clock, each trigger records one step, up to 64, and the movement loops on the following triggers. Each knob has its own loop length, and the inverted knob name fills up with the loop position. A recorded knob's value bar shows where to pick it up. Overdub by holding again, and clear by holding PAGE and twisting a knob (or pressing A or B for the whole part). Recordings stay in RAM only. Push DATA while recording for `(rec lock)` or `(rec s&h)`: the knob is recorded and played only on the instrument's hits, as per-hit locks or as sample & hold. Morph, pan and volume can be recorded the same way on their screens, all 8 instruments at once.
- **ACID bass:** a 303-style voice for basslines: saw / square with a sub, a resonant 4-pole filter with five types (LP24, LP18, LP12, BP, HP), accent, slide from overlapping MIDI notes or a TAKT step at GATETIME `tiE`, drive with the dType curves, and a scale quantizer for CV-driven lines with the TAKT's 13 scales (MODAL and xDRUM have it too).
- **CYMBAL:** ride, crash and 808 cymbal: 808 squares blended with ring-mod metal and noise, body and sizzle with their own decays, a bell ping, rivets, the HIHAT's swing, and mute groups shared with the HIHAT (MtG1–MtG8: hihats and cymbals cut each other).
- **xDRUM:** an additive drum from six sine partials: kicks, toms, congas, wood blocks, marimba, bells and gongs from one voice, with skin / liquid / metal ratios, a pitch sweep, a morph from clean to noisy, a wavefolder, drive with the dType curves and the scale quantizer.
- **CHORD:** five-note chords and stabs: 20 chord shapes, or 11 built from a scale so that one CV or velocity plays progressions in key. With inversion, voicing spread, strum, slide between chords, a drone hold, detune, a square–triangle–saw morph, and ACID's filter plus a notch.
- **More CPU room:** every instrument stops using CPU while it is silent and wakes on the next trigger; the mixer and the stock algorithms' pitch math are lighter too. A tiny dot in the screen's corner lights for a second when the CPU runs out.
- **Input assign:** a third VOLUME page sets per instrument whether it plays from MIDI, its jacks, both or neither. A MIDI-played instrument leaves its CV jack free for the matrix, and double hits from MIDI plus gates are gone.
- **PAGE + knob to the centre:** on the CV and PANNING pages, hold PAGE and turn a knob to reset it to the centre (no modulation, pan centre).
- **Edit the other part silently:** on page A, hold B to see and edit part B while you keep hearing A. Let go and you are back on A. On page B, hold A for the reverse.

**TAKT** (details in [TAKT.md](TAKT.md)):

- **Seeded VARIATION:** a variation that is random but repeats the same way every loop, so one you like stays. Each track has its own seed, and you can also seed random velocity and gate time for SHOTS.
- **Performance mode on the function buttons:** hold a function button (or tap a track while holding it) and let go to return to where you were. MUTE and VARIATION changes are staged and land together on the next bar, up to 16 bars later, or when the next pattern (or the next different pattern) starts (set with DATA while you hold the button). A global apply point lets several menus land on the same bar, and seed edits can be staged too. A track you hold in REC keeps recording while you use a function menu, for build-ups.
- **Random sample & hold LFO waves:** three new waves, `r-4`, `r-8` and `r16`, with a saved random pattern per LFO that you can reroll with DATA.
- **Per-track SHUFFLE:** each track can follow the global shuffle or have its own value from 000 to 127. It also applies to the notes you hear while recording with SHOTS.
- **Recording on muted tracks:** record into a muted track while it stays silent, then unmute it on the next bar. HOLD still blocks recording, as on stock.
- **REC fixes:** entering velocity recording no longer leaves the HOLD, MUTE or VARIATION LEDs lit on muted tracks, and after holding NOTE or MOD-CV to clear a track the menu you were in (MUTE, for example) works again right away.
- **Auto BAR copy keeps the modulation:** extending the pattern with BAR now copies the MOD-CV values along with the notes.
- **Record settings:** per track, choose whether the VELOCITY and GATETIME knobs record (on, off, or auto: once you turn the knob), in REC NOTE, REC velocity and REC MOD-CV. Re-record a groove keeping its velocities and gate times, or add ties to a finished line with REC gate (REC velocity + DATA push: only GATETIME is written), without moving notes. Capture what VARIATION plays into the steps you hold: a snapshot in REC NOTE (gaps and velocities), or only the velocities in REC velocity.
- **HOLD lets you hear velocity and MOD-CV recording:** on a track on HOLD, REC velocity and REC MOD-CV now play what you set without recording it, as REC NOTE already did.
- **Pattern chain:** hold PLAY and press pattern keys to play them in order, up to 64 steps, each one for a full pattern. Saved with the scene. FILL steps can be part of it. A pattern key leaves the chain, PLAY + DATA starts it again.
- **Four FILL patterns:** each scene has four fills. Hold FILL (or PLAY, silently) and turn DATA to choose one. Saved with the scene and in the SysEx dump.
- **Scales on the CV outputs:** a track's CV output plays notes (1 V/octave) in the key of the pattern: 13 scales (including root-only octaves and root + fifth), a root and a transpose (±24 semitones) per pattern (B–D follow A until you change them), octave range and sample & hold per track, so modulation and presets play melodies on a VCO and a pattern chain becomes a chord progression. On the VELO/MOD page (press it twice): a track button shows the track, a pattern key the pattern (without switching to it). Saved with the scene.
- **GATETIME `tiE`:** a new GATETIME position after 100% that ties a note into the track's next one, so a synth with legato or slide (like the FIRE's ACID) glides into it. `tiE`, descending, ascending and RND share the top of the knob equally, and the display names the zone you turn into (`100` for the stretch before them).

## Installing and going back to stock

Each module has its own install steps and caveats. Read them before flashing.

- FIRE: [FIRE.md](FIRE.md#install)
- TAKT: [TAKT.md](TAKT.md#install)

To go back, flash the original Flame firmware file the same way. The originals and the manuals are on the official Flame downloads pages. They are not included here.

- FIRE: [official downloads](https://www.flame-instruments.de/flame2/downloads.html#fire)
- TAKT: [official downloads](https://www.flame-instruments.de/flame2/downloads.html#takt)

## Credits

Plaits and Rings by Emilie Gillet (MIT). Plaits changes and the shakers engine by Lyle Mills (MIT). The shaker models by Perry Cook and Gary Scavone (STK, MIT).

## License

[MIT](LICENSE), covering only the modifications in this repository. The original Flame firmware belongs to Flame.

## Disclaimer

This is unofficial, third-party firmware and is not affiliated with or endorsed by Flame. Flashing it is at your own risk.
