# TAKT custom firmware (based on v1.7.2)

[Back to README](README.md)

> **Warning:** Flame does not support this firmware. Back up your scenes before flashing. Use it at your own risk.

Existing scenes load and sound the same.

## Files

| File | Purpose |
| --- | --- |
| [`FlameTaktV1_7_2_custom.syx`](FlameTaktV1_7_2_custom.syx) | TAKT custom firmware |

## Features

### 1. Seeded VARIATION

VARIATION can be random and still repeat every loop, so a variation you like stays.

In the VARIATION menu, tap a track to cycle: off → on (stock random) → slow blink → fast blink → off.

- **Slow blink:** seeded VARIATION.
- **Fast blink:** seeded VARIATION plus seeded SHOTS random VELOCITY and random GATETIME.

Each track has its own 3-character seed, from 0–9 and the letters that read clearly on the display (`A b C c d E F G H h J L n o P q r t U u y`), about 30,000 seeds. Hold a track to see it.

While holding:

- Turn DATA to change the character with the dot.
- Push DATA to move to the next character.
- Press VARIATION for a random seed (applied at once).
- A track held for about half a second or more only shows its seed. When you let go the state does not step (a short tap does step it).
- Touching the seed during a hold does not change the on/off state. The state changes when you release the track button.

Details:

- The result is tied to the note's position: same seed, same velocities and same dropped notes on every loop.
- The VARIATION pot works as usual. Turning it right only adds dropped notes.
- "On" is exactly stock random.
- Seeds are saved with the scene and in the SysEx dump. Old scenes start at seed 000.

### 2. Performance mode on the function buttons

A short press still opens that menu and stays there.

Hold a function button for 400 ms or more, or tap a track while holding it, and releasing it returns you to where you were. That includes:

- the other function menus
- REC NOTE, REC MOD-CV, REC velocity (both REC buttons)
- TEMPO
- the LFO pages (including PHASE, SYNC and RANGE)
- SCENE load/save
- SETUP / MIDI on the page you were on

Example: while recording, hold MUTE, tap kick and hats, let go. You are back in REC, and the mutes land on the next bar.

**Keep a held track recording:** in REC NOTE, REC MOD-CV or REC velocity, keep holding a track and press any function button, as a tap or a hold. The held track goes on recording exactly as in REC (a SHOTS roll keeps rolling) until you let go of it, while the function menu works on the other tracks. The held track's own button stays with REC until you let go of it, so you can't mute that track in the same move. A track on HOLD is still only heard, not recorded.

Example for a build-up: in REC NOTE with SHOTS, hold the snare, hold MUTE, unmute kick and hats (they land on the next bar), let go of MUTE and then of the snare.

On stock, pressing a function button while holding a track in REC stopped its SHOTS, and the note was never finished: it wasn't recorded, and in some settings the track went on erasing its notes as they played until you pressed it again in REC.

In EDIT USER and EDIT EUCLID the function buttons are still step buttons.

**Staged MUTE and VARIATION:**

HOLD is not staged: taps in the HOLD menu act at once, as on stock. HOLD is still a momentary menu.

- While you hold the button, track taps do not change anything yet. The track LED flickers.
- On release, all of those changes land together on the first step of the next bar (or later, see Delay). With the sequencer stopped they apply right away.
- Tap a track twice to un-stage it. In VARIATION each tap steps off → on → slow blink → fast blink, so four taps bring it back.
- Pressing another function button while still holding drops what you staged.
- In a latched menu (short press), taps apply immediately, as on stock.
- Seed edits are staged too if you hold VARIATION first and then a track (see Staged seeds).

**Delay:**

- While you hold the button, the display shows how many bars to wait. Turn DATA to set it from `0` to `16`, or below `0` to wait for a pattern (see below). It starts at `1` each time.
- `1` is the first bar line after you release, `2` the one after that, and so on. `0` applies the changes right when you release, in the middle of a bar.
- After the release the number counts down at every bar line, and the changes land when it reaches 0.
- Hold the button again to see how many bars are left. Turn DATA to move it, up or down. `0` applies on release.
- Tracks you stage while changes are already waiting join them and keep the count that is left, unless you turn DATA.
- Each menu has its own count. MUTE and VARIATION can wait different numbers of bars.
- In VARIATION, DATA sets the delay only while no track is held. With a track held it edits the seed.

**Wait for the next pattern (`Ptn`, `Ptn.`):**

Below `0` there are two more values:

- `Ptn`: the changes land when the next pattern starts, even if it is the same one: when the pattern loops, at a chain step, or when a pattern you picked comes in.
- `Ptn.` (with the dot): the changes land only when a different pattern starts, from a pattern key, a chain step, or loading a scene. While the same pattern keeps looping they wait.

This works with or without a chain. A pattern picked with `PtC` = `FrE` switches mid-bar, and the changes land with it. Holding the button again shows `Ptn` or `Ptn.` while they wait, and DATA can change it.

**Global apply point:**

- Push DATA while a number from `1` to `16` is shown. That many bars from now is the global apply point, and this menu's waiting changes follow it. The display then alternates `stg` and the bars left, with a dot (for example `4.`).
- In another menu, scroll DATA down past `0`, `Ptn` and `Ptn.` to `stg` to follow the same point. That entry only exists while a global point is waiting. Stage as usual, then release.
- When the point arrives, everything that follows it lands together on the same bar. The point is then gone and `stg` can no longer be selected.
- Turning DATA on a menu that follows the point only changes that menu: scrolling up from `stg` leaves it with its own count. Pushing DATA again sets a new point for every menu that follows it.
- Menus that do not follow the point keep their own count.
- Pushing at `0`, `Ptn` or `Ptn.` does nothing, and a stopped sequencer still applies everything on release.

**Staged seeds:**

- Hold VARIATION first, then hold a track and turn DATA. The seed you edit is staged, while the seed that plays does not change. The display shows the staged seed.
- A short push of DATA moves the cursor (when you let go of it). Hold the push for about half a second to stage a random seed.
- The track flickers, and the staged seed lands with the other staged changes at the bar, after the same delay. A seed and a state change on the same track land together.
- Setting it back to the playing seed drops it. Tapping the flickering track in the VARIATION menu, or a short tap of VARIATION, cancels it.
- Hold a track first, then turn DATA or press VARIATION for a random seed: that is applied at once, as before, and DATA push moves the cursor at once. Order is the only difference.
- If you release VARIATION while still holding the track, edits after that are immediate.

**Cancel before the bar:**

- A short tap of the same function button drops everything still waiting for that menu.
- If you are already in that menu, tapping a flickering track cancels just that track.
- To look at what is waiting, hold the button: the waiting tracks flicker.

### 3. Random sample & hold LFO waves

After `rnd` in WAVE there are three new waves: `r-4`, `r-8` and `r16`.

- Each LFO has its own 16-step random pattern.
- `r-4` and `r-8` loop the first 4 or 8 steps, so you can shorten or lengthen the loop and keep the pattern.
- Press DATA on the WAVE page to roll a new pattern for the selected LFO. The step that is playing finishes with its old value.
- Patterns are saved with the scene.
- Old scenes have no seed stored, so all four LFOs start on the same pattern until you press DATA on each one.

### 4. REC fixes: velocity LEDs, NOTE / MOD-CV hold

A stock bug: entering velocity recording (NOTE + MOD-CV, either order) from another menu left the HOLD / MUTE / VARIATION LEDs lit, including forever on muted tracks. They now turn off, as they do for REC NOTE and REC MOD-CV, and then only flash on triggers.

Also a stock bug: holding NOTE or MOD-CV and pressing a track to clear it while in another menu (MUTE, for example) left that menu's LED lit but its tracks dead, so you had to press MUTE again before you could mute or unmute. When you let go of NOTE or MOD-CV now, the menu works right away.

### 5. Per-track SHUFFLE

Like QUANTIZE: press SHUFFLE, pick a track with the track buttons, and set its shuffle with DATA: `GLb`, then `000` to `127` (same scale as the stock shuffle).

- `GLb` (default) follows the global shuffle. A number replaces it for that track, it is not added. With the global at 65, `000` turns shuffle off for a track.
- Press SHUFFLE again for the global page, and a third time to go back.
- It also applies to the notes you hear while recording with SHOTS, but not to the note you play in single-note recording.
- Saved with the scene. Old scenes start on `GLb` and play as before.
- The global shuffle is now applied per note instead of delaying the whole tick, so the clock stays straight. Notes on ticks 7-11 get the full delay, where stock fades it out.

### 6. Record on a muted track

A muted track can now be recorded, with SHOTS or single notes. Its pattern stays silent, so you can prepare a fill, then unmute it (a staged unmute lands on the next bar). The SHOTS hits you play while recording on a muted track are silent too, but the track LED still flashes for each one. HOLD still blocks recording, as stock.

### 7. Auto BAR copy keeps the modulation

This is a stock bug. With `bCo` on, extending the pattern with BAR copied the notes, velocities and gate times but not the MOD-CV values. They are copied now. Which bars are copied and when is unchanged, and tracks on HOLD are still skipped.

### 8. HOLD lets you hear velocity and MOD-CV recording

On stock, a track on HOLD can't be recorded but you can still play over it live. That worked in REC NOTE but not in the other two recording modes. Now it works in all three:

- **REC velocity** (NOTE + MOD-CV): hold a HOLD track and its notes play at the VELOCITY setting, so you can try a new dynamic before you take HOLD off. Its recorded velocities don't change. Before, you heard the old velocities.
- **REC MOD-CV**: hold a HOLD track (VELO/MOD set to REC) and its CV output follows the VELOCITY control the same way it would while recording. Nothing is recorded, and the recorded modulation plays again when you let go. Before, the recorded modulation kept playing.

GATETIME isn't affected: it only acts in SHOTS note recording, which already lets you hear it on HOLD.

### 9. VELO/MOD `uEL.` and `rEC.`: keep the velocity and gate time of recorded notes

VELO/MOD has two more values, shown with a dot: the order with DATA is `uEL`, `uEL.`, `rEC`, `rEC.`, `001`... The CV output works exactly as `uEL` / `rEC`. The difference is in REC NOTE recording (single notes and SHOTS, with the track buttons or the sensors):

- A hit that lands on or near a note that's already recorded keeps that note's velocity and gate time instead of taking the VELOCITY setting and a new gate (the GATETIME control in SHOTS, how long you hold the button for single notes). "Near" means within half a step of the grid you record with (QUANTIZE, or the BEAT control).
- You hear the old velocity while you record, and in SHOTS the old gate time too. A single note sounds as long as you hold the button, and the old gate time is what gets written when you let go.
- A hit on an empty spot uses the VELOCITY setting and a new gate, as on stock. With GATETIME at `OFF`, SHOTS still records nothing, also on old notes.
- MIDI notes keep the velocity they arrive with, as on stock, but take the old gate time like the buttons.

So you can re-record the timing of a part without losing the dynamics and note lengths you've shaped. `rEC.` is the useful one with MOD-CV recording: the VELOCITY control drives the modulation, and re-recorded notes keep their velocities. REC velocity and REC MOD-CV work as before on dot tracks.

The old notes are remembered from the moment you press the track, so the notes the held track erases as it plays still count. If the pattern changes while you hold the track, new hits use the VELOCITY setting.

### 10. Pattern chain

Play the patterns in an order you choose, for example A A B A C, as a song.

**Making a chain:** hold PLAY and press pattern keys in the order they should play. Press a key again to repeat it. Press FILL to add a FILL step (see [Four FILL patterns](#11-four-fill-patterns)). The display counts the steps, up to 64 (`FuL` after that). Let go of PLAY to start the chain:

- While playing, the first step comes in the way a pattern key would: at the next bar with `PtC` = `bAr`, at once with `PtC` = `FrE` or while FILL is held. It plays to the end of the pattern (only the rest of it, if it came in mid-pattern). After that, each step plays a full pattern, and the next one starts when the pattern loops. After the last step the chain starts over.
- While stopped, the first pattern is selected and the chain starts with PLAY.

The chain is saved with the scene (save the scene to keep it).

**PLAY:**

- A short tap starts and stops, as before, but now when you let go of the button, not when you press it.
- Hold PLAY for about half a second or more without pressing anything else, and letting go does nothing.
- While a chain is on, holding PLAY shows where you are: the step that is playing, a short pause, the number of steps, a pause, and again (for example `002`, `005`, `002`...). It starts after a moment, so a quick tap doesn't change the display. Pressing a pattern key switches to counting the new chain.

**Leaving and resuming:**

- Press a pattern key while playing to leave the chain. That pattern comes in as usual (at the next bar, or at once with `PtC` = `FrE`), and stays.
- Hold PLAY and push DATA to start the stored chain again from step 1. While playing, step 1 comes in like a pattern key: at the next bar with `bAr`, at once with `FrE` or while FILL is held.
- Pattern keys while stopped (to edit a pattern), and CLEAR / COPY / SWAP with the pattern keys, keep the chain.
- To replace the chain, make a new one. A chain of one step just plays that pattern.

**Where it starts:**

- Start, and a reset at the RESET input, go back to step 1.
- Loading a scene that has a chain starts at its step 1. Loading one without a chain plays as before.
- FILL doesn't pause the chain: it keeps counting while you hold FILL, and after you let go you are in whatever step is playing.

### 11. Four FILL patterns

Each scene has four fills instead of one.

**Choosing a fill:**

- Hold FILL and turn DATA. The display shows `F-1` to `F-4`, blinking while the fill you chose isn't the one playing. What you hear doesn't change while you hold FILL; when you let go, the fill you chose is ready for the next press. To switch in the middle of a fill, let go and press FILL again right away: fills play at the running position, so the new one comes in at the same step.
- Hold PLAY and turn DATA to choose without hearing anything. The display shows `F-1` to `F-4` for a second. Letting go of PLAY then doesn't start or stop.
- While PLAY or FILL is held, DATA chooses the fill and doesn't change the value of the menu you are in.

**Playing:** FILL plays the chosen fill as before: hold it, the pattern keeps going underneath, and pattern keys switch at once while it's held. Recording, CLEAR and COPY into FILL work on the chosen fill.

**In a chain:** while holding PLAY to make a chain, press FILL to add a FILL step. It uses the fill you chose last (turn DATA first, still holding PLAY, to pick another one), and the display counts it like a pattern step. In the chain, a FILL step plays its fill for one full pattern with the FILL LED lit, then the chain goes on. A staged change set to `Ptn.` lands on it, and a pattern key leaves the chain as usual.

The chosen fill and all four fills are saved with the scene and sent in the SysEx dump. Scenes and dumps from before have fills 2–4 empty.

### 12. Scales on the CV outputs

A track's CV output can play notes in a key (1 V/octave) instead of a smooth voltage: the recorded modulation, a preset sequence or the velocity, whatever VELO/MOD sends. Patch the CV output into a VCO's pitch input. Each pattern has its own key, so a pattern chain becomes a chord progression.

**The scale page:** press VELO/MOD, then press it again (a third press goes back to the normal VELO/MOD page). On it, the track buttons show a track's settings and the pattern keys show a pattern's settings. Turn DATA to change the value on the display; push DATA for the next setting of the same track or pattern:

| Setting | Belongs to | Display | Values |
| --- | --- | --- | --- |
| Transpose | the pattern | `t 0` ... | moves every note of the pattern by -24 to +24 semitones: `t 5` is +5, `t12` is +12, `t-5` is -5, `-12` is -12 |
| Scale | the pattern | `CHr` ... | `CHr` chromatic, `ion` major, `AEo` natural minor, `Pn5` major pentatonic, `Pn5.` minor pentatonic, `dor` dorian, `PHr` phrygian, `Lyd` lydian, `nni` mixolydian, `HAr` harmonic minor, `uHt` whole tone. B, C and D also have `=A` (below the scales) |
| Root | the pattern | `r C` ... `r b` | the key's root, C to B, a dot means sharp (`r F.` = F#) |
| Range | the selected track | `oFF`, `1-1` ... | `oFF` (the track's CV output is as stock), or which octaves it plays in: `1-1`, `1-2`, `1-3`, `1-4`, `2-2`, `2-3`, `2-4`, `3-3`, `3-4`, `4-4` |
| Mode | the selected track | `FrE` / `5-H` | `FrE` follows the value all the time; `5-H` (sample & hold) takes the value when the track plays a note and keeps that note until its next one |

- **A track:** press a track button. The display shows its Range, and a push toggles Range / Mode. Only that track's LED is lit, as on the VELO/MOD page (it's the same selected track). Tracks on `oFF` (the default) are not touched, so drum tracks keep their velocity CV.
- **A pattern:** press its pattern key. The display shows its Transpose, and pushes go on to its Scale, its Root and back. Its LED blinks fast and the track's LED stays lit. Nothing switches: the playing pattern goes on, so you can set B's key while A plays. Press the same pattern key again (and let go without turning DATA), or any track button, to go back to the track.
- **Changes play at once, or on release:** after a tap on a pattern key, turning DATA changes that pattern's key right away. If you keep the pattern key held while you turn DATA (Transpose, Scale or Root), the display shows the new setting but the pattern keeps playing the old one until you let go. Use it to set up a key change or a transposition on the pattern that's playing and drop it in on a beat. Either way, a note that is already sounding is never retuned (see below).
- **On this page the pattern keys don't switch patterns.** Leave the page (VELO/MOD again, or any menu) to switch. PLAY + pattern keys (chain entry) and CLEAR / COPY / SWAP work as usual.
- **Remembered:** the page reopens on what you had selected last (the track, or a pattern), and on the setting you used last on that side (Range or Mode, Scale or Root).
- **`=A`:** B, C and D start on `=A`: they play in A's key and A's Transpose, and changing A changes them too. Change a pattern's Transpose, Scale or Root to give it its own key (the other two start as A's); turn its Scale down to `=A` to follow A again. A always has its own key.
- **Transpose:** every note of the pattern moves up or down by that many semitones after it's put in the key, like transposing on a keyboard: C major with `t 2` plays D major a tone higher. Root is different: it picks the key's notes but keeps the octaves where they are. A note moved past the top or the bottom of the 4 octaves comes back in an octave lower or higher.
- **When a change is heard:** a note keeps the key and range it started with until the track's next note. That goes for a pattern change (at the bar, `PtC` = `FrE`, chain steps) and for turning Transpose, Scale, Root or Range (and switching a track between `oFF` and a range): the change comes in on the track's next note, so the first note of a new pattern is already in its key and a long note or a `5-H` note is never retuned while it sounds. A track with no note sounding at a bar line takes the change there, so tracks without notes (pure modulation) follow within a bar. Mode (`FrE` / `5-H`) applies at once.
- **FILL** plays in the key of the pattern it interrupts.
- **COPY pattern** copies the key and Transpose with the notes (as the target's own key, not `=A`); **SWAP pattern** swaps them. Copying into or from FILL leaves the keys alone.

**How it plays:**

- The output covers four octaves, 0.1 V to 4.1 V: octave 1 starts at 0.1 V, octave 2 at 1.1 V, and so on. The track's value (0–127) is spread over the octaves of its range and goes to the nearest note of the key. A narrower range gives the VELOCITY control more travel per note when you record.
- The root picks the notes of the key and doesn't move the octaves: E major in `2-3` uses E F# G# A B C# D# between 1.1 V and 3.1 V, so its lowest note is the C# of octave 2. Tune each VCO so that 0.1 V is a C, and every pattern's root is right.
- `5-H` makes moving modulation (recorded movement, LFO-like presets) step once per note. A track with no notes never changes its pitch in `5-H`, so leave pure modulation tracks on `FrE`.
- MIDI isn't affected: tracks still send their own note number from the MIDI menu.
- Keys and track settings are saved with the scene and in the SysEx dump. Old scenes start with every track on `oFF` and play as before (A is `CHr` root C, B–D `=A`).
- Holding a function button on the scale page (performance mode) brings you back to the same page and setting.

**Example:** open the scale page, press pattern A, push to Scale and set `AEo`, push, `r A` (A minor, for every pattern). Press the bass track and set `1-1`; press the lead and set `2-3`, push, `5-H`. Press pattern B and turn to `r d` (it's still on Root): B is D minor. Chain A A B A and the melody and bass move to D minor on every B. Or leave B on `=A`, push to Transpose and set `t 5`: B plays the same A-minor lines a fourth up.

## Install

1. Back up your scenes first (SysEx dump).
2. Power on holding MOD-CV + TRACK 8. The display shows `UPd`.
3. Send [`FlameTaktV1_7_2_custom.syx`](FlameTaktV1_7_2_custom.syx) with a gap of 20 ms between messages. The file is 2,857 messages.

### Going back to stock

Send the original `FlameTaktV1_7_2.syx` the same way. The original file and the manual are on the [official Flame TAKT downloads page](https://www.flame-instruments.de/flame2/downloads.html#takt). They are not included here.

## Caveats

- Scenes saved here load on stock. Seeded tracks play there with VARIATION off. An LFO set to `r-4`, `r-8` or `r16` shows a garbage name on stock and sits at about 0 V.
- Stock ignores the per-track shuffle, so scenes saved here play with the global shuffle only on stock. It also shows `uEL.` / `rEC.` as `uEL` / `rEC`, and ignores the scales (the CV outputs play the plain values).
- COPY and SWAP track do not copy the seed, the track's shuffle, the VELO/MOD dot or the track's Range / Mode. Stock does not copy the VARIATION state either.
- On a fast-blink track, repeated SHOTS hits at the same position (for example with the sequencer stopped) still vary, but they follow the same sequence every time.
- "Stopped" is no clock for 200 ms, so below about 30 BPM staged changes apply when you release the button.
- While a function menu is showing, tracks you press there don't record, same as stock. A track you were already holding in REC keeps recording (see Performance mode). Recording continues when you are back in REC.
- Going back to VELO/MOD, QUANTIZE, SHUFFLE, TRACKSHIFT or LASTSTEP after a momentary hold may reset which track is selected there.
- The scales are tuned to the CV outputs as measured on one TAKT (all eight jacks within about 5 cents). The top notes of a range can drift by a few cents on another unit; check the octaves with a tuner if you play long melodies across 4 octaves.
- A short tap of a function button cancels that menu's waiting changes. Hold the button to look at them.
- PLAY starts and stops when you let go of it, so a start by hand is a moment later than on stock. Starting from a clock, MIDI or the RESET input is not affected.
- Stock ignores the chain: a scene saved here plays its current pattern on stock.
- Saving a scene takes about 3 seconds longer, because fills 2–4 are written after the scene. Wait about 5 seconds after saving before you switch off; if you switch off sooner, that scene's other fills can come back empty (the scene itself is saved). Scene loads, saves and settings changes during those seconds are ignored.
- Stock loads a scene saved here with the chosen fill as its FILL; the other three are not used there. A SysEx dump made here also loads on stock that way.
- The SysEx scene dump takes about 70 seconds instead of 40.
- During a FILL step of a chain, CLEAR and recording go to the fill, as they do while FILL is held.
