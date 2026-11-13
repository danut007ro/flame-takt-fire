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

### 6. Three new algorithms, after the last stock one

- **MODAL**: Plaits' modal voice. A mallet into a 24-mode resonator (from Rings). Bars, bells, plates, glassy and wooden hits.
- **STRING**: Plaits' string voice. A noise burst into a plucked string, with dispersion for harder, inharmonic tones.
- **SHAKERS**: Perry Cook's shaker models (PhISEM, from STK) as in Lyle Mills' Plaits firmware. Many small objects colliding inside a container: 16 instruments.

| Page | Parameters |
| --- | --- |
| Page 1 MODAL, STRING | level, tune, struc, brght, attck, decay, dust (keeps exciting while the gate is held), cutof |
| Page 2 MODAL | type, reso, posit, malet, bits |
| Page 2 STRING | type, reso, burst, bits |
| Page 1 SHAKERS | level, tune, inst, objs, shake, decay, vary, cutof |
| Page 2 SHAKERS | type, reso |

- All three have a filter (LP/BP/HP/notch, shown like the hihat). MODAL and STRING also have an attack (0 = off).
- Everything except `type` (and the SHAKERS `inst`) can be modulated.
- MIDI note transposes. `tune` at the default plays C4.
- Randomize leaves level and type alone (and the SHAKERS `inst`).
- Selecting one loads a default sound (SHAKERS: maraca).

**SHAKERS:**

- `inst` picks the instrument and the display shows its name: maraca (`marac`), cabasa, sekere, tambourine, sleigh bells, bamboo chimes, angklung, coke can, sticks (`stix`), crunch, big rocks, little rocks, coins in a mug (`mug`), water drops, guiro and wrench.
- A trigger is one shake. While the gate is held, `shake` keeps shaking: 0 gives single shakes only, higher keeps it rattling. On guiro and wrench it sets the speed of the scrape.
- `objs`: how many beans, stones or coins. `decay`: how long a shake lasts. Both play the measured instrument in the middle.
- `tune` transposes all the resonances: a pitch on the tuned ones (angklung is a real scale), a size on the others.
- `vary`: how much the resonances jump on each collision. In the middle each instrument is as measured, at 0 nothing jumps, above the middle they jump more, also on the instruments that don't jump by themselves.
- Velocity sets how hard it is shaken.
- Water drops only come at random while shaking, so a single short trigger is often silent. Hold the gate with some `shake`.

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

**Ending with FIRE:** while still holding A (or B), tap FIRE to end the recording right there. FIRE makes no sound while you hold the button, and knobs you turn after the tap aren't recorded. With clock this gives a loop of any length (see below).

**With MIDI clock** (Clock, Start and Stop on the FIRE's MIDI input):

- TAKT setup: connect its MIDI OUT to the FIRE's MIDI IN. Press MIDI until `SCL` (send clock) shows and set it to `On` with DATA.
- Record while the sequencer runs. Pressing A (or B) marks the start of the recording. A knob writes the 16th that is playing as soon as you turn it, and every 16th after that until you let go.
- So you can press A at the start of a bar, wait, turn a knob near the end of the bar and let go at the bar line: the knob's loop is a whole bar that plays its old value until the point where you turned it, then the new value, and every bar after that sounds the same.
- A new recorded knob's loop is as long as the time from your A (or B) press to the end of the recording, rounded up to a quarter bar, half a bar, or 1, 2, 3 or 4 bars. Up to an eighth over still rounds down (a bar recorded slightly long stays one bar); the extra steps wrap onto the start. Steps before your first turn, and any you didn't record, keep the knob's previous value.
- Ended with a FIRE tap, the loop is exactly the 16ths from your A (or B) press to the tap (up to 64), not rounded. A 3- or 5-step loop against the 16-step bar gives a polyrhythm.
- Loops stay on the bar grid, so a half-bar and a 2-bar knob stay in line. Bars are counted as 4/4, whatever the TAKT pattern length.
- Recording again overwrites a recorded knob where you turn it; its length stays.
- Stop holds the values, and the next Start plays from bar 1. Recording while stopped makes nothing.
- Triggers don't move the steps. Without clock for one second, the FIRE goes back to one step per trigger.

**Without clock** (one step per trigger):

- Each trigger from the instrument's gate jack or a MIDI note is one step (FIRE hits are not). Each trigger sets the next step of every recorded knob before the sound starts.
- A new loop is as long as the triggers while you held the button (or until the FIRE tap), up to 64, counting from the press: steps before the knob moved keep its previous value. A recording with no triggers or no turned knob makes nothing.
- Playback starts on the next trigger after you let go. Loops of different lengths drift against each other (a 3-step knob over a 4-step knob).
- Recording again: a recorded knob keeps its length and position and is written from its current step. For a new length, clear it and record it again.

**Turning a recorded knob** afterwards shifts its whole movement up or down. Its value bar shows that knob value, not the steps. If your pots pick up at the stored value, a recorded knob is picked up at the bar, without a jump.

**Clearing:** hold PAGE for 400 ms on page A or B (header `(clr)`).

- Twist a knob: its recording is cleared, back to its knob value (the twist doesn't change the sound).
- Press A or B: all recordings of that part. Press DATA: all recordings of both parts.
- Let go of PAGE to close. A short tap of PAGE still flips the page, on release.

**Other:**

- Recorded knobs show their name inverted. The inverted part grows with the loop position.
- A and B have their own recordings, and A+B copy copies them.
- MORPH, velocity, CV, the matrix and randomize all work on top of a recording.
- Recordings are not saved. Loading a kit, powering off, loading an instrument or changing the algorithm clears them (the last two for that instrument only). Saving a kit stores each recorded knob at its knob value.

### 10. Drive types (dType)

Every instrument with a `drive` knob gets a `dType` knob that picks how the drive distorts:

| Instrument | dType |
| --- | --- |
| SNAREDRUM, BASSDRUM | page 2, pot 8 |
| T-BRIDGE | page 2, pot 5 |
| RIMSHOT, xCLAP | page 2, pot 3 |
| TOM | page 2, pot 4 |
| FM-DRUM | page 2, pot 5 (after its new `drive`, see section 12) |

The display shows the type:

- `stock`: the original soft saturation. At this setting the instrument sounds exactly as before.
- `hard`: a hard clip. Push `drive` up and a kick turns into the square, buzzing gabber kick, tail included.
- `fold`: the wave folds back on itself instead of flattening. Metallic, and the harmonics move as the sound decays.
- `asym`: the negative half saturates at a quarter of the level. A buzzy, fat sound with strong even harmonics.
- `2stg`: the soft saturation pushed into a hard clip. Thick and loud.

`drive` sets how hard the sound hits the curve. The four new types also push harder the higher `drive` is (`hard` and `asym` up to 8× more than stock, `fold` 5×, `2stg` 4×), so they keep distorting through the tail, where stock has already cleaned up. At `drive` 0 they are as clean as stock.

- **dType blends.** The five types sit at the start, ¼, ½, ¾ and the end of the knob, and every position in between is a mix of the two neighbouring types. So as soon as you turn it away from `stock`, a little of `hard` comes in, and halfway between two types you hear half of each. The display shows the nearest type, so it can say `stock` while you already hear some `hard`. To hear one type alone, set the knob right on it.
- dType can be modulated by velocity and CV like any other knob (and by the CV matrix). A CV sweeps smoothly from one type to the next.
- Randomize moves it too. Old kits and instruments load on `stock`.
- On xCLAP, `drive` (stock) only works through its velocity or CV amount, so dType needs that amount set to be heard.
- The new types sound denser and louder than `stock` at the same `drive` (a hard-clipped kick at full drive is about 3 times the average level), but never go past full level. Turn the instrument's level down if it stands out too much.

### 11. Momentary edit (hold MORPH)

On page A or B, hold MORPH and turn knobs: the sound changes while you hold it, and when you let go every knob of the kit glides back (in about 30 ms) to where it was when you pressed MORPH. The screen stays on A or B.

| Gesture | Not latched | Latched |
| --- | --- | --- |
| Hold MORPH, turn knobs, let go | Temporary tweak, glides back | — |
| Press MORPH | A short tap opens the MORPH screen (on release) | Leave the latch at once: everything goes back to where it was before you latched |
| MORPH held, then MASTER | Latch | — |
| MORPH held, then VOLUME | Keep the tweaks | — |
| VOLUME held, then MORPH | — | Keep the tweaks, still latched: the current sound becomes the new starting point |
| MASTER held, then MORPH | — | Open the MORPH screen, still latched |
| VOLUME, MASTER on their own | As usual | As usual, but the screen opens when you let go |
| SETUP, A, B on their own | As usual | As usual |

- The MORPH LED is lit while you hold MORPH, and while the edit is latched.
- Latched, you can switch between A and B, pick other instruments, open other screens and turn knobs. Leaving with MORPH works from any screen.
- When you latch, the tweaks you made before pressing MASTER stay; the latch remembers the sound from before you pressed MORPH. To keep the tweaks and leave, do VOLUME + MORPH, then MORPH.
- While latched the order matters: hold VOLUME or MASTER first. A MORPH press on its own always leaves the latch, so a stray press drops the tweaks.
- While holding MORPH you can tap A or B to switch pages and tweak both parts; letting go of MORPH brings back both. Just tap them: holding A (or B) on its own page while turning a knob is the knob recording gesture, and it records here too (the recording stays after the edit).
- Randomize (hold A or B, press SETUP) works inside the edit, while holding MORPH or latched, and is brought back with the rest.
- Recorded knobs follow the tweak like a turned knob (the whole movement shifts) and come back to their knob value.
- The whole kit is restored: all 8 instruments, parts A and B. Volume, panning, CV amounts and the output settings are not part of it.
- Saving a kit while latched saves the sound from before the edit (or from the last MORPH + VOLUME).
- An instrument whose algorithm you change during the edit is left as it is.
- In SELECT mode and fire mode, MORPH works as before.

### 12. Drive on FM-DRUM

FM-DRUM had no `drive`. It now has `drive` (page 2, pot 4) and `dType` (page 2, pot 5) inside its voice, like the other drums: the distortion follows its envelope and velocity (softer hits distort less), and the level comes after it.

- At `drive` 0 FM-DRUM sounds exactly as before. Old kits load like that.
- The distortion comes in gradually over the first few percent of `drive`.
- Both can be modulated by velocity and CV; randomize moves them too.

## Install

1. Back up your kits (MIDI dump).
2. Power on holding SETUP + MASTER (firmware update mode, as in the [official manual](https://www.flame-instruments.de/flame2/downloads.html#fire)).
3. Send [`FlameFireV1_07_custom.syx`](FlameFireV1_07_custom.syx).
   - In your SysEx tool, set a **gap of 20 ms between messages**, as the official manual says. The file is 7,754 messages.
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
- MODAL and STRING no longer have `drive`; `bits` moved into its place. A kit saved with MODAL or STRING on an earlier build reads its old `drive` value as `bits` here: set `bits` again.
- A kit that uses MODAL or STRING will not load correctly on stock or on the earlier builds. Ring and swing are ignored there. A kit that uses SHAKERS also needs this build. Stock and older builds ignore dType and FM-DRUM's drive and play stock.
- On stock and older builds, an instrument set to M1–M6 plays on its direct out only, and a shared direct out plays only one of its instruments.
- Older builds and stock ignore the CV matrix amounts. Saving a kit on an older build drops them.
- If you use CV on Level together with a negative velocity Level amount, soft hits play at the absolute value. Velocity-only Level behaves like stock.
- BASSDRUM and T-BRIDGE, page 2 pot 3: amounts above about +0.5 respond a bit differently from stock.
- Knob recording: saving a single instrument stores the step that is playing, not the knob value.
- Knob recording with MIDI clock (loops counted from the A / B press) and the FIRE tap ending are new and not yet tried on the device.
- Ring on hihat samples is the least tested part. Please say if its level jumps against your samples.
- SHAKERS, dType, the momentary edit and FM-DRUM's drive (section 12) are new and not yet tried on the device.
- CPU: with every matrix amount set, all CV inputs moving, and the heaviest stock algorithm on every channel, audio uses about half the CPU time (stock's heaviest kit is about 46%). Please say if you hear glitches with a big matrix anyway.

## Credits

Plaits and Rings by Emilie Gillet (MIT). Plaits changes and the shakers engine by Lyle Mills (MIT). The shaker models by Perry Cook and Gary Scavone (STK, MIT).
