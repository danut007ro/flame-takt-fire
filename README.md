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

**FIRE:** velocity and CV active at the same time, a CV matrix, randomize, four extra hihat samples, new MODAL and STRING algorithms, and main plus direct outs together. See [FIRE.md](FIRE.md).

**TAKT:** seeded VARIATION, performance mode on the function buttons, random sample & hold LFO waves, per-track SHUFFLE, and a fix for the REC velocity LED bug. See [TAKT.md](TAKT.md).

## Installing and going back to stock

Each module has its own install steps and caveats. Read them before flashing.

- FIRE: [FIRE.md](FIRE.md#install)
- TAKT: [TAKT.md](TAKT.md#install)

To go back, flash the original Flame firmware file the same way. The originals and the manuals are on the official Flame downloads pages. They are not included here.

- FIRE: [official downloads](https://www.flame-instruments.de/flame2/downloads.html#fire)
- TAKT: [official downloads](https://www.flame-instruments.de/flame2/downloads.html#takt)

## Credits

Plaits and Rings by Emilie Gillet (MIT). Plaits changes by Lyle Mills (MIT).

## License

[MIT](LICENSE), covering only the modifications in this repository. The original Flame firmware belongs to Flame.

## Disclaimer

This is unofficial, third-party firmware and is not affiliated with or endorsed by Flame. Flashing it is at your own risk.
