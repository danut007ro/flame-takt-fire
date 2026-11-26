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
- Stock kits load with their amounts on the mode they were in, and the other set centred.

### 2. Bits modulation

Bits is modulatable by velocity and CV on SD, FM, BD, RIM and TOM. It shows up in the CV menu as "bits". The reducer has 23 steps, so a slow sweep steps.

### 3. Randomize

Hold A (or B) and press SETUP. Every parameter of that part of the selected channel moves by up to ±15%. Press SETUP again for another nudge.

- Releasing A or B does not change the page.
- Level is never touched, and neither are the hihat's decay, hold and mute group.
- There is no undo. Reload the kit.

### 4. Four extra hihat samples

`mtSel` goes metal, smp1–4 (factory, unchanged), then smp5 to smp8, each one 1/9 of the knob.

- Stock kits keep the sample they had. The even spacing starts the first time you turn `mtSel`.
- Factory samples 1–4 cannot be overwritten.
- An empty slot is silent.
- Each slot is 24 KB of 8-bit audio (about 0.77 s at 32 kHz). Use `tune` to bring a sample back to its original pitch.

See [Uploading the samples](#uploading-the-samples).

### 5. Two new hihat knobs, at the end of page 2

- **ring**: fades the metal into Plaits' ring-modulated square and saw metal. Works on the synth metal and on samples.
- **swing**: fades the VCA into Plaits' swing VCA, softer and more saturated.

At 0 the hihat is the stock sound. Stock kits load with both at 0. Both follow velocity, CV, morph and randomize.

**Mute groups:** the HIHAT's mute knob (page 2, `mute`) is a group: `noMtG` or `MtG1`–`MtG8`, shown on the display. A hit on any HIHAT or CYMBAL in a group cuts every other HIHAT and CYMBAL in that group (on stock it means "muted by channel N": stock kits need it set again).

### 6. Two new algorithms, after the last stock one

- **MODAL**: Plaits' modal voice. A mallet into a 24-mode resonator (from Rings). Bars, bells, plates, glassy and wooden hits.
- **SHAKERS**: Perry Cook's shaker models (PhISEM, from STK) as in Lyle Mills' Plaits firmware. Many small objects colliding inside a container: 16 instruments.

| Page | Parameters |
| --- | --- |
| Page 1 MODAL | level, tune, struc, brght, attck, decay, posit, malet |
| Page 2 MODAL | type, cutof, reso, dust (keeps exciting while the gate is held), bits, scale |
| Page 1 SHAKERS | level, tune, inst, objs, shake, decay, vary, cutof |
| Page 2 SHAKERS | type, reso |

- Both have a filter (LP/BP/HP/notch, shown like the hihat). MODAL also has an attack (0 = off).
- Everything except `type` (and the SHAKERS `inst`) can be modulated.
- MIDI note transposes. `tune` at the default plays C4.
- MODAL `scale`: snaps `tune` (with its modulation) to a scale, with the MIDI note as the key, the same as on ACID (section 15). Random CV on `tune` then plays mallet lines in key.
- Randomize leaves level and type alone (and the SHAKERS `inst`).
- Selecting one loads a default sound (SHAKERS: maraca).

**SHAKERS:**

- `inst` picks the instrument and the display shows its name: maraca (`marac`), cabasa, sekere, tambourine, sleigh bells, bamboo chimes, angklung, coke can, sticks (`stix`), crunch, big rocks, little rocks, coins in a mug (`mug`), water drops, guiro and wrench.
- A trigger is one shake. While the gate is held, `shake` keeps shaking: 0 gives single shakes only, higher keeps it rattling. On guiro and wrench it sets the speed of the scrape.
- `objs`: how many beans, stones or coins. `decay`: how long a shake lasts. Both play the measured instrument in the middle.
- `tune` transposes all the resonances: a pitch on the tuned ones (angklung is a real scale), a size on the others. Below the default (0.375) it goes down by up to 3 octaves. Above it, each instrument goes up as far as it can still sound: the top of the knob puts its lowest resonance near 13 kHz (up to 5 octaves for the low ones like coke can, about half an octave for little rocks), so every instrument plays over the whole knob. The highest resonances fade out above 12 kHz, so the bright instruments get thinner toward the top.
- `vary`: how much the resonances jump on each collision. In the middle each instrument is as measured, at 0 nothing jumps, above the middle they jump more, also on the instruments that don't jump by themselves.
- Velocity sets how hard it is shaken.
- Water drops only come at random while shaking, so a single short trigger is often silent. Hold the gate with some `shake`.

### 7. CV matrix

Every instrument can be modulated by all eight CV jacks (CV1–CV8) at the same time. One CV can drive several instruments, and one instrument can take all eight CVs plus velocity and the eight macros (section 23).

On the CV page, turn DATA. The header goes VELO, CV1–CV8, then M1–M8 (the macros). The pots edit the set shown in the header. All of the sets are applied together.

- VELO and the instrument's own jack are the two sets of section 1.
- The other seven jacks are continuous CV only. Velocity still comes from the instrument's own jack at its own trigger, and a CV on another jack does not trigger.
- Level works from any jack.
- Morph still uses velocity and the own CV.
- With the matrix amounts centred, only the instrument's own jack and velocity modulate it.

**Route pool:** each amount set away from the centre on another instrument's jack or on a macro is a route. All instruments share 128 routes.

- When all 128 are in use, turning a new amount does nothing and the header shows `(full)` for a second. Amounts already set keep working and can still be changed.
- An amount left near the centre, where it has no audible effect, for a second gives its route back. PAGE + knob (section 19) gives it back at once.
- The MACROS screen (section 23) lists the routes of each jack and macro.

**Randomize on the CV page:** hold CV and press SETUP to nudge every amount of the input shown in the header by up to ±15%. The other inputs are left alone. On another instrument's jack or a macro, only the amounts already set are nudged. Level, and the hihat's decay, hold and mute group, are skipped.

**Storage:**

- The matrix and macro amounts and the macro values are saved with the kit and in the kit dump (the dump is 12 messages longer).
- Stock kits load with them centred.
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

**Recording:** on page A hold A (on page B hold B); the header shows `(rec)`. Every knob you turn while holding is recorded, and keeps writing until you let go. You hear it live. Only knobs moved more than about 6% after pressing count, so pot noise is ignored. The small jitter of a resting knob is also kept out of recordings and out of recorded knobs: a knob held still records one steady value, and turning a recorded knob later shifts its loop without the jitter (a slow turn follows a few steps behind; a fast one and the ends of the knob are exact).

**Ending with FIRE:** while still holding A (or B), press FIRE to end the recording right there. FIRE makes no sound while you hold the button, and knobs you turn after pressing it aren't recorded. With clock, a tap ends the loop on the nearest beat and a hold gives any length in 16ths (see below).

**With MIDI clock** (Clock, Start and Stop on the FIRE's MIDI input):

- TAKT setup: connect its MIDI OUT to the FIRE's MIDI IN. Press MIDI until `SCL` (send clock) shows and set it to `On` with DATA.
- Record while the sequencer runs. Pressing A (or B) marks the start of the recording. A knob writes the 16th that is playing as soon as you turn it, and every 16th after that until you let go.
- So you can press A at the start of a bar, wait, turn a knob near the end of the bar and let go at the bar line: the knob's loop is a whole bar that plays its old value until the point where you turned it, then the new value, and every bar after that sounds the same (gliding into the new value over that 16th, and back to the old one over the first 16th of the next bar; see playback below).
- A new recorded knob's loop is as long as the time from your A (or B) press to the end of the recording, rounded up to whole beats under a bar (1, 2 or 3 beats) or to 1, 2, 3 or 4 bars. A 16th over still rounds down under a bar, and up to an eighth over above it (a bar recorded slightly long stays one bar); the extra steps wrap onto the start. Steps before your first turn, and any you didn't record, keep the knob's previous value.
- **Playback glides:** a `(rec)` knob moves smoothly through each 16th, from where the knob was when the 16th started to where you left it when it ended, so a recorded sweep plays back as a sweep instead of in 16th steps, and a jump you recorded becomes a quick slide over one 16th. The glide follows the tempo. A trigger in the last third of a 16th gets the value at its end. `(rec lock)` and `(rec s&h)` still change only at hits, a muted knob plays its knob value, and without clock each trigger plays its step as before.
- Ended with FIRE, the loop length is counted from your A (or B) press to the moment you press FIRE:
  - **Tap FIRE:** whole beats, rounded to the nearest beat. You only have to tap close to the beat: a tap between 2½ and just under 3½ beats after the press gives 3 beats (12 steps). At least 1 beat, at most 16.
  - **Hold FIRE about ⅓ second:** exactly the 16ths up to the press (up to 64), not rounded. The recording ends when the ⅓ second is up, without waiting for you to let go. A 3-, 5- or 7-step loop against the 16-step bar gives a polyrhythm.
  - Clock steps and knob turns while FIRE is down change nothing.
- Loops stay on the bar grid, so a half-bar and a 2-bar knob stay in line. Bars are counted as 4/4, whatever the TAKT pattern length.
- Recording again overwrites a recorded knob where you turn it; its length stays.
- Stop holds the values, and the next Start plays from bar 1. Recording while stopped makes nothing.
- If a Start comes while you are recording (the TAKT restarted), the recording starts again from bar 1, as if you had pressed the button at the Start. Knobs that already had a loop keep what you recorded into them.
- Triggers don't move the steps. Without clock for one second, the FIRE goes back to one step per trigger.

**Recording on hits: `(rec lock)` and `(rec s&h)`.** While holding A (or B), push DATA to change how this recording works. Each push goes to the next mode, and the header shows which one. Each instrument remembers its last mode per part: the next time you hold A (or B) on it, the recording starts in that mode (forgotten when you load a kit or an instrument, change the algorithm or power off):

| Header | Records | On a hit without a recorded value |
| --- | --- | --- |
| `(rec)` | every 16th (with clock) or every hit (without), as above | — |
| `(rec lock)` | only at the instrument's hits | plays the knob |
| `(rec s&h)` | only at the instrument's hits | keeps the last recorded value |

- Hits are the instrument's gate jack or its MIDI note (as INP allows, section 18). FIRE hits don't count.
- Turning a knob only arms it. Each hit while you hold A writes the armed knob's value at that hit's 16th; 16ths without a hit stay empty. Only hits while A is held are recorded.
- The loop length is counted the same way: with clock, from your A press to the last hit, rounded; ended with FIRE, to the 16th playing when you press it (a tap: the nearest beat; a hold: exactly). Without clock, steps are hits, and the hits before you turned the knob are empty.
- **Playback:** the knob changes only at the instrument's hits, just before the hit plays, never in the middle of one. A recorded step plays its value. An empty step plays the knob in `lock` mode (only the recorded hits differ, like parameter locks) or keeps the last recorded value in `s&h` mode (the value steps on and holds until the next recorded hit).
- **Example:** clock running, hold A, push DATA (`(rec lock)`), turn decay up, let the next hit play, let go. Only that hit has the long decay, every loop.
- Turning a `lock` / `s&h` knob later moves its value bar but not the sound: the next hit plays with everything shifted by your turn (its recorded values and, in `lock`, the knob value on empty steps). Nothing changes between hits. While you hold A to record, you hear the knob as you turn it.
- Recording over a knob in another mode switches it to the new recording's mode. Recording `(rec lock)` or `(rec s&h)` over a `(rec)` knob keeps its movement and from then on plays it only at the hits (sampled where each hit lands). Recording `(rec)` over a `lock` or `s&h` knob makes it smooth again: the steps you didn't write hold the value before them. Recording in the knob's own mode just overwrites the steps you turn.
- The mode of a new recording is the one shown when you let go; push DATA before you turn knobs.
- The name of a recorded knob always shows the playback position, also on `lock` / `s&h` hits.
- Copy, clearing (PAGE held), randomize and the momentary edit work as for `(rec)`.

**Recording MORPH, PAN and VOLUME.** On the MORPH, PANNING and VOLUME (page 1) screens, hold A and turn knobs: each knob is one instrument, so you record the morph (the A↔B mix of the whole sound), the pan or the volume of any of the 8 instruments at once. The header shows `MORPH (rec)` and so on.

- Everything above works the same: DATA cycles `(rec)`, `(rec lock)` and `(rec s&h)` (each screen remembers its last mode), with clock the 16ths, without clock the hits; each knob steps with its own instrument's hits. FIRE ends a loop (tap: on the beat, hold: exact 16ths).
- Letting go of A keeps you on the screen. A short tap of A without turning anything still goes to page A, and A + B (copy) or A + SETUP (randomize) still work as long as no knob was turned.
- Ideas: morph `(rec lock)` for a different A↔B blend on chosen hits, pan `(rec s&h)` for hats that jump around the stereo field, volume `(rec)` for swells and fades.
- A recorded knob's value bar and pickup are at its knob; its name fills with the position. Turning it later shifts the movement (`(rec)`: heard at once; `lock` / `s&h`: at the next hit).
- **Clearing** works as on the edit pages: hold PAGE for 400 ms (header `MORPH (clr)`, `PAN (clr)` or `VOLUME (clr)`; until then the knobs work as usual).
  - Turn a recorded knob: its recording is cleared, back to its knob value (header `(clr 3)` for instrument 3).
  - Press A or DATA: every recording of that screen (`(clr all)`).
  - Let go of PAGE to close. On PANNING, an unrecorded knob turned while the menu is open goes to the centre (section 19). On VOLUME, a short PAGE tap still flips the page.
- Volume and pan recordings move the main mix only (as the knobs do). The momentary edit doesn't include them. A kit save stores the knob values.
- The macros record the same way on the MACROS screen (section 23).

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

**Muting:** hold PAGE and tap FIRE. The header shows `(mute)` at once, without the 400 ms wait. This works on pages A and B, MORPH, PANNING, VOLUME and the MACROS screen.

- Turn a recorded knob about 6% either way: a playing knob mutes, a muted one unmutes. Turning further the same way does nothing; turning back the other way toggles it again, as often as you like while PAGE is held.
- The header shows the last change: `(mute tuneM)` or `(unmute tuneM)` on the edit pages, `(mute 3)` or `(unmute 3)` for instrument 3 on the other screens.
- The turns don't change the sound. Knobs without a recording, A, B and DATA do nothing here. Tap FIRE again for sample & hold (`(hold)`, section 24), and once more to go back to clearing (`(clr)`). Let go of PAGE to close.
- A muted knob's loop keeps running in the background but is not applied: the parameter sits at the knob value, and turning the knob is heard at once. Velocity, CV and the macros still modulate it. Unmuted, the loop comes back at the step it has reached, so it stays on the bar.
- A muted knob's name fills only in its bottom half.
- Recording on a muted knob (hold A) writes the loop without being heard; only the value bar follows your hand. The knob stays muted, so unmute it to hear the take.
- Clearing a knob also unmutes it. A+B copy copies the mutes. Mutes are not saved; loading a kit or changing the algorithm drops them.

**Other:**

- Recorded knobs show their name inverted. The inverted part grows with the loop position.
- A and B have their own recordings, and A+B copy copies them.
- MORPH, velocity, CV, the matrix, the macros and randomize all work on top of a recording.
- Only the knobs of parameters the instrument has can be recorded; the others are ignored.
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

- `stock`: the original soft saturation. At this setting the instrument sounds exactly as on stock.
- `hard`: a hard clip. Push `drive` up and a kick turns into the square, buzzing gabber kick, tail included.
- `fold`: the wave folds back on itself instead of flattening. Metallic, and the harmonics move as the sound decays.
- `asym`: the negative half saturates at a quarter of the level. A buzzy, fat sound with strong even harmonics.
- `2stg`: the soft saturation pushed into a hard clip. Thick and loud.

`drive` sets how hard the sound hits the curve. The four new types also push harder the higher `drive` is (`hard` and `asym` up to 8× more than stock, `fold` 5×, `2stg` 4×), so they keep distorting through the tail, where stock has already cleaned up. At `drive` 0 they are as clean as stock.

- **dType blends.** The five types sit at the start, ¼, ½, ¾ and the end of the knob, and every position in between is a mix of the two neighbouring types. So as soon as you turn it away from `stock`, a little of `hard` comes in, and halfway between two types you hear half of each. The display shows the nearest type, so it can say `stock` while you already hear some `hard`. To hear one type alone, set the knob right on it.
- dType can be modulated by velocity and CV like any other knob (and by the CV matrix). A CV sweeps smoothly from one type to the next.
- Randomize moves it too. Stock kits and instruments load on `stock`.
- On xCLAP, `drive` (stock) only works through its velocity or CV amount, so dType needs that amount set to be heard.
- The new types sound denser and louder than `stock` at the same `drive` (a hard-clipped kick at full drive is about 3 times the average level), but never go past full level. Turn the instrument's level down if it stands out too much.

### 11. Momentary edit (hold MORPH)

On page A, page B or the CV menu, hold MORPH and turn knobs: the sound changes while you hold it, and when you let go every knob of the kit glides back (in about 30 ms) to where it was when you pressed MORPH. The screen stays where it was.

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
- The whole kit is restored: all 8 instruments, parts A and B, and everything the CV menu sets: the velocity and CV amounts, the matrix and macro amounts (CV1–CV8, M1–M8) and the morph amounts. One edit covers all of it, wherever you start: hold MORPH on page A, turn knobs, press CV, turn amounts, let go, and both come back. The latch (MORPH + MASTER) and keep (VOLUME) work the same on the CV menu.
- Volume, panning, the output and input settings are not part of it.
- Saving a kit while latched saves the sound from before the edit (or from the last MORPH + VOLUME), amounts and matrix included.
- An instrument whose algorithm you change during the edit is left as it is.
- In SELECT mode and fire mode, MORPH works as on stock.

### 12. Drive on FM-DRUM

Stock FM-DRUM has no `drive`. Here it has `drive` (page 2, pot 4) and `dType` (page 2, pot 5) inside its voice, like the other drums: the distortion follows its envelope and velocity (softer hits distort less), and the level comes after it.

- At `drive` 0 FM-DRUM sounds exactly as on stock. Stock kits load like that.
- The distortion comes in gradually over the first few percent of `drive`.
- Both can be modulated by velocity and CV; randomize moves them too.

### 13. Offset knob mode

A third knob mode next to `pick` and `jump`: on the SETUP screen (page 1, pot 5) the knob mode goes `pick`, `jump`, `offs`.

With `offs`, a knob never has to find its value. Whenever a page opens (A, B, CV, MORPH, VOLUME, PANNING, MASTER), you pick another instrument, load a kit, or the momentary edit, randomize or a knob recording take ends, every knob starts from where it is and works relative to the value:

- Turning right raises the value from where it was, turning left lowers it, by as much as you turn. Nothing jumps, and there's no dead travel.
- The screen shows the real value, as always.
- At 0 or the maximum the value stops, and the knob's starting point follows it. Turning back changes the value at once.
- Small knob jitter is ignored, so a value doesn't creep while you don't touch the knob.

**Clutch: hold PANNING.** While PANNING is held, turning knobs changes nothing (the PANNING LED stays lit). Let go and the knobs work from their new positions. Use it when a knob runs out of travel: hold PANNING, turn the knob back, let go and keep turning.

While PANNING is held you can also line knobs up with their values:

- Each value bar shows where the knob physically is, as a 2-pixel gap in the line. The dot is the value. Move the knob until the gap reaches the dot.
- When a knob reaches its value, its bar turns 2 pixels high for 400 ms (the pick marker, section 14). Knobs that are already lined up when you press PANNING don't flash.
- Let go of PANNING: a knob that is lined up takes exactly its position as the value. From then on it works like a normal knob, and its ends reach 0 and the maximum. The value moves by the small difference (at most about 1.5%) at that moment. Knobs that aren't lined up keep working relative to their value.

- A short tap of PANNING, without turning a knob, still opens the PANNING screen (when you let go).
- In `pick` and `jump` mode, PANNING works as on stock.
- Knob recording records the values that come out; knob moves while PANNING is held aren't recorded.
- The SETUP screen itself uses its knobs as on stock.

### 14. Pick marker

In `pick` mode each value bar also shows where the knob physically is, as a 2-pixel gap in the line. The dot is the value: turn the knob towards the dot. When the knob reaches its value and takes over, its value bar turns 2 pixels high (as high as the dot) for 400 ms, and from then on the knob is on the value, so the gap disappears into the dot.

- Only knobs you actually move onto their value show it. Knobs that already sit on their value when a page opens don't, so a page flip doesn't flash every bar at once.
- It works on every page with value bars: A, B (both pages), CV, MORPH, VOLUME and PANNING. MASTER shows numbers, not bars, so there's nothing to mark there.
- Keep turning: the bar stays 2 pixels high until the 400 ms are up.
- In `jump` mode there's no pickup, so no marker. In `offs` mode the marker shows while PANNING is held (section 13).

### 15. ACID: a 303-style bass

A new algorithm after SHAKERS for basslines from the TAKT (or any MIDI sequencer): an oscillator from sine through wavefold, saw and square to a thin pulse, with a sub, a resonant 4-pole filter with an envelope, accent and slide.

| Page | Parameters |
| --- | --- |
| Page 1 | level, tune, wave, envMd, accnt, decay, reso, cutof |
| Page 2 | type, slide, aDec, sub, track, drive, dType, scale |

- `wave`: one sweep through the oscillator's shapes, with no jumps:
  - at 0 a **sine**, for deep sub and 808-style basses;
  - then a **wavefold** that grows (growly, vocal) and eases back while the wave leans into a ramp;
  - the ramp brightens into the **saw** (a wide flat spot just before the middle): the classic 303 saw, where a new ACID starts;
  - the saw blends into the **square** (a flat spot at about three quarters), staying at an even level through the blend;
  - past the square the **pulse narrows** to a thin, buzzy 1/8 pulse at full (SH-101 style), getting quieter as it thins.

  The sine, saw, square and thinnest pulse have flat spots around them, so they're easy to hit. `sub`: a square an octave down.
- `cutof`, `reso` (up to self-oscillation), `envMd` (how far the filter envelope opens the filter), `decay` (filter envelope decay), `track` (how much the cutoff follows the note).
- `type`: the filter's response, shown on the display: `LP24` (round), `LP18` (closest to a 303, the default), `LP12` (brighter), `BP` (thin, nasal), `HP` (only the fizz and the resonance). The types are level-matched, so switching doesn't jump in volume.
- `accnt`: how strong the accent is. Velocity decides which notes are accented: below 64 none, from 64 up more and more, full at 127. An accented note is louder and brighter and has a shorter filter decay; accents in a row build up, like the 303. At 0 velocity does nothing.
- `slide`: the glide time (0 = the pitch jumps). A note glides into the next one when the notes overlap: the next note starts before the previous one ends, as a DAW or keyboard plays legato and as the TAKT sends a step recorded at GATETIME `tiE`. Notes that don't overlap start again.

  `slide` at the bottom of the knob turns sliding off. A slid-into note doesn't restart the envelope or take a new accent, as on a 303, but its velocity still counts for the velocity amounts: with velocity → `tune`, each slid-into note's velocity moves the pitch and it glides there. This works on ACID's own MIDI channel (1–8) and on channel 10, where the drum map plays ACID from its note.
- **Basslines from the TAKT:** on each step, velocity sets the accent (e.g. 127 accented, 40 not) and GATETIME sets the slide: a step recorded at GATETIME `tiE` (TAKT custom firmware) glides into the track's next note, every other step plays as a new note. A TAKT track always sends the same MIDI note, so the pitch comes from:
  - **velocity:** a velocity amount on `tune` (and a `scale` to snap the pitch to notes): each step's velocity sets its pitch (`octv` gives octave jumps, `5th` roots and fifths). Accent then follows velocity too (loud steps are high and accented), so turn `accnt` down if you don't want that,
  - **several tracks:** set several TAKT tracks to ACID's MIDI channel, each on its own note (one track per pitch), or
  - **CV:** a TAKT CV output (on its scale page) into this channel's CV jack, with a CV amount on `tune` and the same `scale`.
- `aDec`: the note sounds while the gate (the MIDI note) is held, then fades out over `aDec` (0 = cut at once, like a 303).
- `drive` and `dType`: the same drive curves as the drums (section 10), after the filter.
- `scale`: snaps `tune`, including its CV, velocity and matrix modulation, to the notes of a scale. The MIDI note is added afterwards, so it sets the key: with `major` and a held MIDI G, random CV on `tune` plays G major. Without MIDI the key is C. A pitch resting between two notes stays on one instead of flickering, and between two notes equally near it takes the lower one. Combined with `slide`, a stepped CV glides from note to note.
  The scales are the TAKT's (its scale page, in the same order), so a FIRE voice and a TAKT CV track can play in the same key:

  | FIRE | TAKT | Scale |
  | --- | --- | --- |
  | `off` | | no quantizing |
  | `chrom` | `CHr` | chromatic |
  | `major` | `ion` | major (ionian) |
  | `minor` | `AEo` | natural minor (aeolian) |
  | `pnMaj` | `Pn5` | major pentatonic |
  | `pnMin` | `Pn5.` | minor pentatonic |
  | `dorn` | `dor` | dorian |
  | `phryg` | `PHr` | phrygian |
  | `lydn` | `Lyd` | lydian |
  | `mixo` | `nni` | mixolydian |
  | `hMin` | `HAr` | harmonic minor |
  | `whole` | `uHt` | whole tone |
  | `octv` | `oCt` | the root only, in every octave |
  | `5th` | `5th` | root and fifth |

  The TAKT's Root is the MIDI note here: send the root note from the TAKT track that plays the FIRE channel.
- MIDI notes play as sent with `tune` at 0 (the default); `tune` transposes. A trigger on the gate jack plays the `tune` pitch (C1 at 0) and holds the note only as long as the gate.
- Everything except `type` can be modulated, `scale` too. Randomize leaves level, type and scale alone. Selecting it loads a default acid sound (saw, scale off).

### 16. CYMBAL: ride, crash and 808 cymbal

A new algorithm after ACID, for the long, shimmering cymbals the hihat doesn't do.

| Page | Parameters |
| --- | --- |
| Page 1 | level, tune, metal, sprd, attck, decay, wash, bell |
| Page 2 | type, cutof, reso, body, bDec, dust, mute, swing |

- `metal`: the 808's six square oscillators at 0, Plaits' ring-modulated metal at 1, blended in between. `sprd` spreads the 808 oscillators further apart (wider = more crash-like). `wash` mixes in white noise.
- The sound has two parts with their own decay: the body (`body` sets its pitch, `bDec` its decay) and the sizzle on top (`decay`, the main length, up to several seconds).
- `bell`: the ping of a ride's bell. `dust`: rivets rattling in the sizzle.
- `attck`: a slower start, for crash swells. `cutof`, `type`, `reso`: the filter, as on MODAL and SHAKERS.
- `mute` (`noMtG`, `MtG1`–`MtG8`): the mute group, shared with the HIHAT (section 5). A hit on any HIHAT or CYMBAL in a group cuts all the other HIHATs and CYMBALs in that group: open and closed hats, a ride cut by a closed hat, two crashes cutting each other. Other instruments don't take part. To "grab" a crash, put a HIHAT or CYMBAL at level 0 in its group and trigger that.
- `swing`: the HIHAT's swing VCA (section 5) on the cymbal, a lopsided, punchier decay. 0 = off.
- Velocity sets how hard it's hit. `tune` at the default plays the measured frequencies; the MIDI note transposes.
- Everything except `type` and `mute` can be modulated. Randomize leaves level, type and mute alone. Selecting it loads a ride (`noMtG`, swing 0).

### 17. xDRUM: an additive drum

A new algorithm after CYMBAL: a tuned drum built from six sine partials. One voice goes from a deep kick through toms, congas and wood blocks to marimba, bells, gongs and noisy hits, and every step in between can be modulated.

| Page | Parameters |
| --- | --- |
| Page 1 | level, tune, harmo, sprd, attck, decay, sweep, swDec |
| Page 2 | mode, morph, fold, tilt, drive, dType, scale, bits |

- `harmo`: where the partials sit. At 0 they are all on the fundamental (a pure sine, for 808-style kicks), at the middle they form the harmonic series, at 1 they take the ratios of `mode`.
- `mode` (`skin`, `liqd`, `metal`, shown on the display): `skin` is a drum head (toms, congas), `liqd` is half-harmonic (hollow and woody, watery with a sweep), `metal` is a bar or bell (marimba, bells, gongs, clangs).
- `sprd`: how loud the upper partials are (0 = the fundamental only). `tilt`: how much sooner the upper partials die (0 = all ring together, like a bell; 1 = only the fundamental is left after the hit, like a tom or a marimba).
- `decay`: 10 ms to about 4 s. `attck`: a slower start, up to 200 ms (0 = none).
- `sweep` and `swDec`: the pitch drop after the hit, up to 4 octaves, lasting 2 to 300 ms: a kick's punch, a tom's bend, a laser zap.
- `morph`: each partial modulates the next one (the first one modulates itself). Clean up to about the middle, then brighter and metallic, and noise-like near the top, for snare-like and crashy hits.
- `fold`: a wavefolder on the whole sound.
- `drive` and `dType`: the drive curves of section 10, as on ACID. `bits`: bit reduction.
- `scale`: as on ACID (section 15), with `tune` at 0.375 being C4 as on MODAL; the MIDI note transposes and sets the key.
- Velocity sets how hard it's hit.
- Everything except `mode` can be modulated. Randomize leaves level, mode and scale alone. Selecting it loads a kick (G1, `skin`).

### 18. Input assign: MIDI, CV, both or none (VOLUME page 3)

PAGE on the VOLUME menu goes through three pages: the levels, the outputs (section 8), and `INP ASSIGN`. On page 3 each knob sets what its instrument listens to. The cell shows the instrument and a letter:

| Cell | Setting | The instrument plays from |
| --- | --- | --- |
| `TOM:B` | both (the default) | MIDI and its jacks, as on stock |
| `TOM:M` | MIDI | MIDI notes only |
| `TOM:C` | CV | its gate and CV jacks only |
| `TOM:-` | none | neither: only the FIRE button plays it |

- **MIDI** means the notes on the instrument's MIDI channel, or its note on channel 10: the trigger, the velocity and the note (the pitch of MODAL, ACID, xDRUM and the other tuned instruments). MIDI CCs for volume, pan and morph keep working whatever the setting.
- **CV** means the instrument's gate jack (trigger and velocity) and the modulation from its own CV jack (its CV amounts and the morph CV).
- On the outputs page and on page 3 each knob starts from that page's own setting, not from the level: in `pick` mode it takes over when it reaches the current choice, in `offs` mode it moves on from it. Changing pages never changes an output or input on its own.
- **The jack stays useful:** with `M`, the instrument ignores its jacks, but its CV jack still modulates the other instruments through the CV matrix (section 7). So you can play an instrument from the TAKT over MIDI and use its CV jack as a free modulation source. It also stops double hits when a sequencer sends both MIDI and gates.
- Changing the setting ends a note the instrument is holding.
- Knob recording (section 9) only counts the triggers the instrument takes.
- Saved with the kit and in the kit dump (one message longer). Stock kits and dumps load with every instrument on `B`.

### 19. PAGE + knob: back to the centre

On the CV menu (all its pages: the velocity, CV, matrix and macro amounts and the morph amounts) and on PANNING, hold PAGE and turn a knob: its value jumps to the centre, which means no modulation (or the pan centre). On the CV menu this works at once; on PANNING after PAGE has been held 400 ms (the recording clear opens with it, section 9).

- Each knob resets once per hold. While it is active, the knobs do nothing else, so you can reset several in a row without changing anything by accident.
- When you let go of PAGE, the knobs are picked up again as after a page change: in `pick` mode a reset knob takes over when it passes the centre, in `jump` mode it jumps when you move it, in `offs` mode it goes on from the centre.
- A short tap of PAGE on the CV menu flips the page when you let go.
- A matrix or macro amount reset to the centre gives its route back at once (section 7).
- On the edit pages A and B, on PANNING, VOLUME and MORPH and on the MACROS screen's ALL view, holding PAGE 400 ms opens the knob-recording clear, and PAGE + FIRE the mute menu (section 9). On the MACROS screen's route views, PAGE + knob removes a route (section 23).

### 20. Edit the other part silently (hold B on page A)

On page A, hold B. After about a third of a second the display shows page B: its values, both of its pages and its value bars, with `(B)` at the end of the header. The knobs now edit B, but you keep hearing A, so nothing changes in the sound while you set B up. Let go of B and you are back on page A. You stay on A even if you turned nothing.

- It works both ways: on page B, hold A to edit A while you hear B (the header shows `(A)`).
- A short tap of B switches to page B, as on stock.
- Turning a knob before page B shows still edits A. Wait for the B page.
- While B is shown:
  - PAGE flips between B's two pages.
  - SETUP randomizes B (section 3), silently. Pressing SETUP before page B shows randomizes B too, then page B shows.
  - Pressing A copies B into A (the usual copy). You land on page A and hear the copy.
  - FIRE plays as usual.
  - Any other button first takes you back to page A, then does its usual job.
- Holding B on page A never starts a knob recording (section 9). Lanes already recorded on A keep playing while you look at B.

### 21. CHORD: chords and stabs

A new algorithm after xDRUM: five-note chords for stabs, keys and pads, played from a jack trigger, MIDI or the TAKT.

| Page | Parameters |
| --- | --- |
| Page 1 | level, tune, chord, invrt, wave, cutof, reso, spred |
| Page 2 | attck, aDec, sustn, slide, fAtk, fDec, envMd, pEnv |
| Page 3 | detun, sub, drive, dType, strum, drift, type, scale |

CHORD has three pages: PAGE goes 1 → 2 → 3 → 1. Page 1 is the chord and its tone, page 2 the envelopes (the sound on the top row, the filter on the bottom row, attack and decay in the same columns), page 3 colour and setup. On the CV menu PAGE goes through the amounts of pages 1, 2 and 3, then the morph page; the amounts sit where their knobs are.

- `tune`: the chord's root. At 0.25 it is C3. A MIDI note sets the key: only its name counts (C, G, A …, in any octave), so `tune` keeps the octave. Without MIDI the key is C.
- `chord`: the chord shape, shown on the display.
  - With `scale` at `off` or `chrom`, 24 fixed shapes, each next to its family: `5`, `maj`, `min`, `madd9`, `sus2`, `sus4`, `aug`, `dim`, `m7b5`, `7`, `7sus4`, `7#9`, `9`, `13`, `maj7`, `maj9`, `M7#11`, `m7`, `m9`, `m11`, `m6`, `6/9`, `add9`, `quart` (stacked fourths). `tune` moves the shape as it is.
  - With any other scale, 13 shapes built from the scale, from simple to rich: `5th`, `triad`, `sus2`, `sus4`, `add9`, `6th`, `6/9`, `7th`, `7sus4`, `9th`, `11th`, `13th`, `4ths`. `tune` picks the step of the scale, and the chord follows the key by itself: in C major the triads go C, Dm, Em, F, G, Am, Bdim. Any CV, velocity or random modulation on `tune` then plays chords that fit together.
  - Every shape has a bass note an octave under the root, like a left hand. The rich chords (9, maj9, m9, m11, 6/9, 13, 7#9, M7#11; 9th, 11th, 13th, 6/9 and 4ths with a scale) leave the root out of the notes above it, as a pianist voices them, so five notes are enough for the colour.
- **Chords from the TAKT:** send one note on CHORD's MIDI channel (it sets the key), set a `scale`, and put a velocity amount on `tune`: each step's velocity picks the chord, always in key. A TAKT CV track into the CV jack with a CV amount on `tune` does the same.
- `invrt` has two halves:
  - **Right half: the inversion.** From the middle, turning up moves the lowest notes up an octave one by one (higher, brighter). The display shows the inversion you hear: `root`, `1st`, `2nd`, `3rd` or `4th`, the inversion of the notes above the bass (the right hand), named by the chord tone at their bottom. With `slide` at 0, a note between two octaves plays at both, so a CV on `invrt` sweeps smoothly. With `slide` up, each note glides to its new octave at the slide's speed.
  - **Left half: voice leading** (the display shows `lead`). The knob is a register, from about F#4 next to the middle down to F#2 at the left end, and the notes above the bass are placed in the octave around it. When the chord changes (the `chord` knob, `tune`, a MIDI key, a step of the scale), each note moves to the nearest note of the new chord, as a keyboard player changes chords, instead of the whole shape jumping. The register follows `tune`'s octave: `tune` an octave up moves the whole voicing up. `spred` and `slide` work on top of it.
  - Just left of the middle is a small flat spot with the chord as listed.
- `wave`: one sweep through the oscillator's shapes, with no jumps:
  - at 0 a thin, buzzy **pulse** that widens into a **square** (a flat spot at about a fifth of the knob);
  - the square softens into a **sine** (a flat spot at about two fifths);
  - then a **wavefold** grows, glassy, vocal, then metallic, and eases back while the wave leans into a ramp;
  - the ramp brightens into a **saw** at full.

  The level stays even, and the corners are rounded, so high chords stay clean instead of turning harsh.
- `slide`: when the chord changes (the `chord` knob, `tune`, a new step of the scale, a MIDI note, a CV, `invrt`, the voicing), the notes glide to the new chord instead of jumping, each to the note in the same place (lowest to lowest, and so on up), like a pad changing chords. At 0 they jump; turning up makes the glide longer, up to about half a second. A new trigger doesn't stop a glide.
- `spred`: the voicing, shown on the display: `close` (tight, a keyboard stab), `open`, `wide`, `wider`, `huge`. It opens up the chord as `invrt` has inverted it: the bass stays in place and the upper notes move up by octaves, for open, orchestral chords, and every voicing has all the inversions.
- `detun`: each inner note gets a detuned twin, from clean to a wide supersaw-like stab. The lowest and highest notes stay clean.
- `strum` (page 3): the notes start one after another, from the lowest, up to 150 ms apart (a quick strum at small settings, an arpeggio at full). A short trigger still plays the whole roll, and each note plucks the filter.
- `type`: the filter, as on ACID (`LP24`, `LP18`, `LP12`, `BP`, `HP`) plus `NOTCH`, a hollow phaser-like cut that moves with the cutoff. `cutof`, `reso`, `envMd` (how far the filter envelope opens), `fAtk` (how long the filter takes to open, from at once to about 2 s) and `fDec` (how fast it closes again).
- `attck`: how long the sound takes to come in, from a click (2 ms) to a slow 2 s swell. A short trigger still swells all the way in before it fades.
- `sustn`: the level a held chord (a held MIDI note or gate) settles to after the attack, at the `aDec` speed. At full it stays at the peak.
- `aDec`: the fade after the gate. From a jack trigger CHORD plays a stab that fades with `aDec`; a held MIDI note holds the chord. The fade is exponential, from a click to a long tail. At the very top of the knob there is no fade: after one trigger the chord holds for ever (a drone); turn `aDec` down to let it fade.
- `sub`: a sine an octave below the lowest note you hear (after the inversion and the voicing), through the filter with the chord.
- `drive` and `dType`: ACID's drive and its five curves, on the whole chord. At 0 it is off.
- `pEnv`: a pitch blip on each note. In the middle it is off. Turned right, each note starts above its pitch and falls onto it; turned left, it starts below and rises. A little off the middle is a short, subtle blip; the ends are a zap from an octave away (about 150 ms). With `strum` each note gets its own blip as it starts.
- `drift`: each note wanders slowly and randomly around its pitch, on its own, like an old analog synth (up to about a third of a semitone at full). At 0 it is off.
- Velocity makes the chord louder and brighter.
- `tune`, `chord`, `invrt` and `spred` ignore the small jitter of a resting knob, so the pitch doesn't wobble and a chord on the edge between two shapes doesn't flicker. The name on the display changes exactly where the sound does.
- Everything except `type` can be modulated. Randomize leaves level, type and scale alone. Selecting it loads a minor-7th stab (C3, saw).

### 22. CPU warning dot

When the FIRE runs out of CPU (the audio misses its deadline, which you hear as a crackle), a tiny 2 × 2 dot lights in the top-right corner of the screen for one second. If it keeps happening, the dot stays on. Use it to find the moment a kit gets too heavy, then lighten it (see CPU under Caveats).

### 23. Macros

Eight macros, M1–M8. Each one moves any number of parameters, on any instruments, each by its own amount, so one knob can open a filter on the bass while it shortens the hats and adds drive to the snare.

**Assigning:** on an instrument's CV page, turn DATA to M1–M8 (after the CV jacks). Each pot sets how far that macro moves its parameter: the centre is not at all, either side moves it up or down. Set them on as many instruments as you like. Each amount set is a route from the shared pool (section 7).

**The MACROS screen:** hold MASTER for half a second (a short press opens MASTER as usual). Turn DATA to step through the views:

- **MACROS (all):** the 8 pots are M1–M8. Each cell shows the macro and how many routes it has (`M1  3`). At 0 a macro changes nothing; turned up, every parameter it reaches moves by up to its full amount.
- **M1–M8:** the routes of one macro, sorted by instrument. Each cell is the instrument number and the parameter (`2deca`: instrument 2's decay), its bar is the amount, and the pots edit the amounts. The header shows the number of routes (`M3 5 routes`). With more than 8, tap PAGE for the next 8 (the header shows `1-8`, `9-16` …).
- **CV1–CV8:** the same for a jack: every instrument and parameter it drives, and how much.
- In the M and CV views, hold PAGE and turn a knob to remove that route.
- A short MASTER press goes back to the MASTER screen. Any other button leaves the screen and does its usual job.

**Recording macros:** in the MACROS view, hold A and turn macros. They record like MORPH, PAN and VOLUME (section 9): the 16ths with clock or the hits without, `(rec lock)` and `(rec s&h)` with DATA, FIRE to end a loop, clearing with PAGE held (`MACROS (clr)`) and muting with PAGE + FIRE.

- The macro values and amounts are saved with the kit. A recorded macro saves its knob value.
- Macros cost no CPU until you move one (by hand or from a recording). Each CV route costs about 0.1 % of the CPU, so a pool filled with CV routes takes about a tenth.

### 24. Sample & hold

A held parameter changes only on its instrument's hits: whatever moves it in between (your hand on the knob, MIDI CC, MORPH, velocity, CV, the matrix, the macros, a knob recording, randomize, the momentary edit's glide) waits, and the next hit plays with the value it has reached by then. A hit is a trigger on the instrument's gate jack or a MIDI note for it. Each parameter of each instrument is held on its own, and so are each instrument's pan and volume.

**Holding:** on page A or B, hold PAGE and tap FIRE twice: `(mute)`, then `(hold)`.

- Turn a knob about 6% either way: its parameter is held (`(hold tuneM)`), turn back to free it (`(free tuneM)`). As with muting, turning further the same way does nothing, and you can toggle as often as you like while PAGE is held. Every knob of the instrument works here, recorded or not, on all its pages (CHORD's page 3 too).
- Press A: every parameter of the instrument is held (`(hold all)`). Press A again when they're all held to free them all; DATA frees them all too (`(free all)`). B does nothing here.
- Tap FIRE once more to go back to clearing (`(clr)`). Let go of PAGE to close.
- A hold is per parameter, not per part: it covers A, B and the morph between them.

**On the MORPH, PANNING and VOLUME screens** each knob is one instrument: hold PAGE, tap FIRE twice for `MORPH (hold)` (or `PAN`, `VOLUME`), and turn instrument 3's knob (`(hold 3)`, back again: `(free 3)`):

- MORPH: holds or frees every parameter of that instrument, the same as A on its own page.
- PANNING: its pan moves only on its hits.
- VOLUME (page 1): its volume moves only on its hits, a per-hit VCA.
- The MACROS screen has no hold: the macros reach parameters through their routes, which follow the holds of those parameters.

**What you see:** a held parameter's value bar is dashed (on its edit pages and its CV page; on MORPH, PANNING and VOLUME the instrument's bar). The bar, the name and the kit value still follow your hand at once: only the sound waits for the next hit, so turning a held knob on an instrument that isn't playing changes nothing you hear.

- Freeing a parameter plays its latest value at once, without waiting for a hit.
- The holds are saved with the kit. A kit load plays its values at once; its holds start at each instrument's first hit.
- Changing an instrument's algorithm frees all its parameters (they mean something else). The A+B copy leaves the holds alone.
- Knob recordings work on held parameters: a `(rec)` loop is heard at the step each hit lands on, and `(rec lock)` and `(rec s&h)` play on the hits as before.

## Install

1. Back up your kits (MIDI dump).
2. Power on holding SETUP + MASTER (firmware update mode, as in the [official manual](https://www.flame-instruments.de/flame2/downloads.html#fire)).
3. Send [`FlameFireV1_07_custom.syx`](FlameFireV1_07_custom.syx).
   - In your SysEx tool, set a **gap of 20 ms between messages**, as the official manual says. The file is 6,206 messages.
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
- On stock, the knob mode `offs` loads as `pick`.
- A kit that uses MODAL, SHAKERS, ACID, CYMBAL, xDRUM or CHORD needs this firmware; it will not load correctly on stock. Stock ignores ring and swing, the input assign (every instrument plays from both), dType and FM-DRUM's drive, and plays stock.
- On stock, an instrument set to M1–M6 plays on its direct out only, and a shared direct out plays only one of its instruments.
- Stock ignores the CV matrix amounts and the macros. Saving a kit on stock drops them.
- If you use CV on Level together with a negative velocity Level amount, soft hits play at the absolute value. Velocity-only Level behaves like stock.
- BASSDRUM and T-BRIDGE, page 2 pot 3: amounts above about +0.5 respond a bit differently from stock.
- Knob recording: saving a single instrument stores the step that is playing, not the knob value.
- CPU: every instrument stops using CPU a moment after it goes silent (its gate low and its sound faded out) and wakes on the next trigger, a knob change or a CV change, so a kit has much more room while only a few instruments play. FM-DRUM, COWBELL and CYMBAL then start their oscillators at another point in the cycle, like a free-running analog oscillator; the hit sounds the same. An instrument whose level is turned all the way down keeps running. The stock instruments do their math in single precision, which leaves a few percent more room while everything plays; they sound the same (CLAP's noise and FM-DRUM's feedback vary from hit to hit as they always did). A kit full of heavy instruments can still run out while everything plays at once: one CHORD channel costs about as much as xDRUM; `detun` adds a little, and so do `drive` (about as much as ACID's drive), `sub`, `pEnv`, `drift` and voice leading, while they are in use. If the sound crackles (the dot in the corner lights), lower `detun` or `drive` on CHORD, or use a lighter instrument on another channel.

## Credits

Plaits and Rings by Emilie Gillet (MIT). Plaits changes and the shakers engine by Lyle Mills (MIT). The shaker models by Perry Cook and Gary Scavone (STK, MIT).
