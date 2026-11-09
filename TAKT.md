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
- Press VARIATION for a random seed.
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

In EDIT USER and EDIT EUCLID the function buttons are still step buttons.

**Staged HOLD, MUTE and VARIATION:**

- While you hold the button, track taps do not change anything yet. The track LED flickers.
- On release, all of those changes land together on the first step of the next bar. With the sequencer stopped they apply right away.
- Tap a track twice to un-stage it. In VARIATION each tap steps off → on → slow blink → fast blink, so four taps bring it back.
- Pressing another function button while still holding drops what you staged.
- In a latched menu (short press), taps apply immediately, as on stock. Seed editing is always immediate.

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

### 4. REC velocity LED fix

This is a stock bug. Entering velocity recording (NOTE + MOD-CV, either order) from another menu left the HOLD / MUTE / VARIATION LEDs lit, including forever on muted tracks. They now turn off, as they do for REC NOTE and REC MOD-CV, and then only flash on triggers.

### 5. Per-track SHUFFLE

Like QUANTIZE: press SHUFFLE, pick a track with the track buttons, and set its shuffle with DATA: `GLb`, then `000` to `127` (same scale as the stock shuffle).

- `GLb` (default) follows the global shuffle. A number replaces it for that track, it is not added. With the global at 65, `000` turns shuffle off for a track.
- Press SHUFFLE again for the global page, and a third time to go back.
- It also applies to the notes you hear while recording with SHOTS, but not to the note you play in single-note recording.
- Saved with the scene. Old scenes start on `GLb` and play as before.
- The global shuffle is now applied per note instead of delaying the whole tick, so the clock stays straight. Notes on ticks 7-11 get the full delay, where stock fades it out.

## Install

1. Back up your scenes first (SysEx dump).
2. Power on holding MOD-CV + TRACK 8. The display shows `UPd`.
3. Send [`FlameTaktV1_7_2_custom.syx`](FlameTaktV1_7_2_custom.syx).

### Going back to stock

Send the original `FlameTaktV1_7_2.syx` the same way. The original file and the manual are on the [official Flame TAKT downloads page](https://www.flame-instruments.de/flame2/downloads.html#takt). They are not included here.

## Caveats

- Scenes saved here load on stock. Seeded tracks play there with VARIATION off. An LFO set to `r-4`, `r-8` or `r16` shows a garbage name on stock and sits at about 0 V.
- Stock ignores the per-track shuffle, so scenes saved here play with the global shuffle only on stock.
- COPY and SWAP track do not copy the seed or the track's shuffle. Stock does not copy the VARIATION state either.
- On a fast-blink track, repeated SHOTS hits at the same position (for example with the sequencer stopped) still vary, but they follow the same sequence every time.
- "Stopped" is no clock for 200 ms, so below about 30 BPM staged changes apply when you release the button.
- While a function menu is showing you are not recording, same as stock. Recording continues when you are back in REC.
- Going back to VELO/MOD, QUANTIZE, SHUFFLE, TRACKSHIFT or LASTSTEP after a momentary hold may reset which track is selected there.
- A short tap of a function button cancels that menu's waiting changes. Hold the button to look at them.
