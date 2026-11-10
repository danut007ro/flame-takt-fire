# FIRE custom firmware (based on v1.07)

[Back to README](README.md)

> **Warning:** Flame does not support this firmware. Back up your kits before flashing. Use it at your own risk.

The 12 stock algorithms sound the same as stock when the new amounts are left centred.

## Files

| File | Purpose |
| --- | --- |
| [`FlameFireV1_07_custom.syx`](FlameFireV1_07_custom.syx) | FIRE custom firmware |
| [`smp5_42k_sample5.syx`](smp5_42k_sample5.syx) | Hihat sample 5 |
| [`smp6_37k_sample6.syx`](smp6_37k_sample6.syx) | Hihat sample 6 |
| [`smp7_32k_sample7.syx`](smp7_32k_sample7.syx) | Hihat sample 7 |
| [`smp8_25k_sample8.syx`](smp8_25k_sample8.syx) | Hihat sample 8 |

## Features

### 1. Velocity and CV at the same time

Every parameter, and MORPH, has two amounts: one for velocity and one for CV. Both stay active. The VELO/CV switch only chooses which set you edit.

- Velocity comes from MIDI, or from the CV jack sampled at the trigger.
- The same jack also works continuously through the CV amounts. A voice can have velocity dynamics and an LFO or sequence on its jack.
- Old kits load with their current amounts on the mode they were in, and the other set centred.

### 2. Bits modulation

Bits is modulatable by velocity and CV on SD, FM, BD, RIM and TOM. It shows up in the CV menu as "bits". The reducer has 23 steps, so a slow sweep steps.

### 3. Randomize

Hold A (or B) and press SETUP. Every parameter of that part of the selected channel moves by up to ±15%. Press SETUP again for another nudge.

- Releasing A or B does not change the page.
- Level is never touched, and neither are the hihat's decay, hold and mute group.
- There is no undo. Reload the kit.

### 4. Four extra hihat samples

`mtSel` goes metal, smp1–4 (factory, unchanged), then smp5 to smp8, each one 1/9 of the knob.

- Kits saved before keep the sample they had. The even spacing starts the first time you turn `mtSel`.
- Factory samples 1–4 cannot be overwritten.
- An empty slot is silent.
- Each slot is 24 KB of 8-bit audio (about 0.77 s at 32 kHz). Use `tune` to bring a sample back to its original pitch.

See [Uploading the samples](#uploading-the-samples).

### 5. Two new hihat knobs, at the end of page 2

- **ring**: fades the metal into Plaits' ring-modulated square and saw metal. Works on the synth metal and on samples.
- **swing**: fades the VCA into Plaits' swing VCA, softer and more saturated.

At 0 the hihat is the stock sound. Old kits load with both at 0. Both follow velocity, CV, morph and randomize.

### 6. Two new algorithms, after the last stock one

- **MODAL**: Plaits' modal voice. A mallet into a 24-mode resonator (from Rings). Bars, bells, plates, glassy and wooden hits.
- **STRING**: Plaits' string voice. A noise burst into a plucked string, with dispersion for harder, inharmonic tones.

| Page | Parameters |
| --- | --- |
| Page 1 (both) | level, tune, struc, brght, attck, decay, dust (keeps exciting while the gate is held), cutof |
| Page 2 MODAL | type, reso, posit, malet, drive, bits |
| Page 2 STRING | type, reso, burst, drive, bits |

- Both have an attack (0 = off) and a filter (LP/BP/HP/notch, shown like the hihat).
- Everything except `type` can be modulated.
- MIDI note transposes. `tune` at the default plays C4.
- Randomize leaves level and type alone.
- Selecting one loads a default sound.

### 7. CV matrix

Instruments 1–4 can be modulated by CV1–CV4 at the same time, and instruments 5–8 by CV5–CV8. One CV can drive several instruments, and one instrument can take four CVs plus velocity.

On the CV page, turn DATA. The header goes VELO, CV1, CV2, CV3, CV4 (CV5–CV8 on instruments 5–8). The pots edit the set shown in the header. All of the sets are applied together.

- VELO and the instrument's own jack are the same two sets as before.
- The other three jacks are continuous CV only. Velocity still comes from the instrument's own jack at its own trigger, and a CV on another jack does not trigger.
- Level works from any jack.
- Morph still uses velocity and the own CV.
- With the new amounts centred, it sounds as before.

**Randomize on the CV page:** hold CV and press SETUP to nudge every amount of the input shown in the header by up to ±15%. The other inputs are left alone. Level, and the hihat's decay, hold and mute group, are skipped.

**Storage:**

- The extra amounts are saved with the kit and in the kit dump (the dump is 12 messages longer).
- Kits from earlier builds load with them centred.
- Single instruments do not store them, only kits do.
- Changing the algorithm resets them like the other amounts.
- A dump from this build still loads on stock. Stock ignores the extra messages.

### 8. Outputs: main and a direct out together, and shared outs

On VOLUME page 2 the pot goes 1–6, M, M1–M6.

- M1–M6 play on the main mix and on that direct out at the same time (the display shows e.g. "TOM:M3").
- Several instruments can share one direct out and are mixed there as a plain sum. Loud hits together can clip. Lower the levels if they do.
- The settings are saved with the kit and in the kit dump.

### 9. Knob recording

Record knob movements as steps on the A and B pages of the selected instrument. With MIDI clock (for example from the TAKT) the steps are 16th notes locked to the bars, like recording knobs on the TAKT. Without clock, each trigger is one step.

**Recording:** on page A hold A (on page B hold B); the header shows `(rec)`. Every knob you turn while holding is recorded, and keeps writing until you let go. You hear it live. Only knobs moved more than about 6% after pressing count, so pot noise is ignored.

**With MIDI clock** (Clock, Start and Stop on the FIRE's MIDI input):

- TAKT setup: connect its MIDI OUT to the FIRE's MIDI IN. Press MIDI until `SCL` (send clock) shows and set it to `On` with DATA.
- Record while the sequencer runs. A knob writes the 16th that is playing as soon as you turn it, and every 16th after that.
- A new recorded knob's loop is as long as you recorded it, rounded up to a quarter bar, half a bar, or 1, 2, 3 or 4 bars. Up to an eighth over still rounds down (a bar recorded slightly long stays one bar); the extra steps wrap onto the start. Steps you didn't record keep the knob's previous value.
- Loops stay on the bar grid, so a half-bar and a 2-bar knob stay in line. Bars are counted as 4/4, whatever the TAKT pattern length.
- Recording again overwrites a recorded knob where you turn it; its length stays.
- Stop holds the values, and the next Start plays from bar 1. Recording while stopped makes nothing.
- Triggers don't move the steps. Without clock for one second, the FIRE goes back to one step per trigger.

**Without clock** (one step per trigger):

- Each trigger from the instrument's gate jack or a MIDI note is one step (FIRE hits are not). Each trigger sets the next step of every recorded knob before the sound starts.
- A new loop is as long as the triggers while you held the button, up to 64, counting from the press: steps before the knob moved keep its previous value. A recording with no triggers or no turned knob makes nothing.
- Playback starts on the next trigger after you let go. Loops of different lengths drift against each other (a 3-step knob over a 4-step knob).
- Recording again: a recorded knob keeps its length and position and is written from its current step. For a new length, clear it and record it again.

**Turning a recorded knob** afterwards shifts its whole movement up or down. Its value bar shows that knob value, not the steps. If your pots pick up at the stored value, a recorded knob is picked up at the bar, without a jump.

**Clearing:** hold PAGE for 400 ms on page A or B (header `(clr A)` / `(clr B)`).

- Twist a knob: its recording is cleared, back to its knob value (the twist doesn't change the sound).
- Press A or B: all recordings of that part. Press DATA: all recordings of the page's part.
- Let go of PAGE to close. A short tap of PAGE still flips the page, on release.

**Other:**

- Recorded knobs show their name inverted. The inverted part grows with the loop position.
- A and B have their own recordings, and A+B copy copies them.
- MORPH, velocity, CV, the matrix and randomize all work on top of a recording.
- Recordings are not saved. Loading a kit, powering off, loading an instrument or changing the algorithm clears them (the last two for that instrument only). Saving a kit stores each recorded knob at its knob value.

## Install

1. Back up your kits (MIDI dump).
2. Power on holding SETUP + MASTER (firmware update mode, as in the [official manual](https://www.flame-instruments.de/flame2/downloads.html#fire)).
3. Send [`FlameFireV1_07_custom.syx`](FlameFireV1_07_custom.syx).
   - In your SysEx tool, set a **gap of 20 ms between messages**, as the official manual says. The file is 7,528 messages.
4. Upload the four samples (below).

### Uploading the samples

Upload with the new firmware running normally (**not** in update mode).

1. Send [`smp5_42k_sample5.syx`](smp5_42k_sample5.syx) with a 150 ms gap between messages (503 messages).
2. Pause for a few seconds after it finishes. The FIRE writes the sample to flash after the last message and ignores a new upload while that write is still running. Nothing on the display tells you when the write is done, so wait before sending the next file.
3. Send [`smp6_37k_sample6.syx`](smp6_37k_sample6.syx), [`smp7_32k_sample7.syx`](smp7_32k_sample7.syx) and [`smp8_25k_sample8.syx`](smp8_25k_sample8.syx) the same way: 150 ms between messages, then a pause after each file.

**To check:** select a HIHAT, turn `mtSel` to smp5–smp8 and play, with `nsMix` fully on metal and the filter open. There is no confirmation on the display.

### Going back to stock

Flash the original `FlameFireV1_07.syx` the same way. Stock ignores samples 5–8, and the factory samples are not touched. The original file and the manual are on the [official Flame FIRE downloads page](https://www.flame-instruments.de/flame2/downloads.html#fire). They are not included here.

## Caveats

- Kits saved with this firmware will not load correctly on stock.
- A kit that uses MODAL or STRING will not load correctly on stock or on the earlier builds. Ring and swing are ignored there.
- On stock and older builds, an instrument set to M1–M6 plays on its direct out only, and a shared direct out plays only one of its instruments.
- Older builds and stock ignore the CV matrix amounts. Saving a kit on an older build drops them.
- If you use CV on Level together with a negative velocity Level amount, soft hits play at the absolute value. Velocity-only Level behaves like stock.
- BASSDRUM and T-BRIDGE, page 2 pot 3: amounts above about +0.5 respond a bit differently from stock.
- Knob recording: saving a single instrument stores the step that is playing, not the knob value.
- Knob recording with MIDI clock is new and not yet tried on the device.
- Ring on hihat samples is the least tested part. Please say if its level jumps against your samples.
- CPU: with every matrix amount set, all CV inputs moving, and the heaviest stock algorithm on every channel, audio uses about half the CPU time (stock's heaviest kit is about 46%). Please say if you hear glitches with a big matrix anyway.

## Credits

Plaits and Rings by Emilie Gillet (MIT). Plaits changes by Lyle Mills (MIT).
