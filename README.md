# Vocal emotion feedback

Live sad / happy / afraid voice effect for plugdata (iOS). Based on Rachman et al. 2018 (DAVID) and Aucouturier et al. 2016. Independent re-implementation, not endorsed by the authors. Live effect, requires wired headphones, preferably closed-back or noise-cancelling.

## Files
- `vocal-emotion-feedback.pd` - the patch
- `LICENSE` - MIT

## Use
1. Put `vocal-emotion-feedback.pd` in plugdata's folder and open it.
2. DSP on, run mode.
3. Tick USE_MIC.

Requires: ELSE `knob` (bundled with plugdata, not in vanilla Pd), `sigmund~` `expr` `expr~` `fexpr~` `samphold~` `rzero~` `vline~`. If `sigmund~` is missing, turn SMOOTH off.

## Controls
| Control | Function |
|---|---|
| EMOTION | left sad, centre neutral, right happy |
| FEAR | afraid vibrato, 8.5 Hz, up to +-40 cents |
| INFLECT | pitch swoop at phrase start, 0 = off (default) |
| Presets | NEUTRAL, HAPPY / SAD / AFRAID at low / mid / high |
| MIC GAIN | 25 = unity |
| VOL | fader, default 50, output limited to +-0.95 |
| GATE 0=off | 0 = off, 1-100 = -69.5 to -20 dBFS |
| GLIDE ms | 0 = jump |
| USE_MIC | mic on |
| SMOOTH | on (default): shifter window follows the pitch period (about 20 ms). off: fixed 10 ms |
| NEUTRAL_reset | button, resets to no effect |
| MORE | RECORD_(may_fail), SHELF_2nd-order, FEMALE_VOICE, SMALLER_PITCH, PAPER_LEVELS, AFRAID_SWOOP_150ms, AFRAID_SWOOP_SIZE |

## Parameters
| | Pitch (cents) | High band above 8 kHz | Other |
|---|---|---|---|
| Happy low / mid / high | +29.5 / +40.9 / +50 | up to +9.5 dB/oct | inflection -200..+140 cents, 500 ms |
| Sad low / mid / high | -39.8 / -56.2 / -70 | down to -12 dB/oct | |
| Afraid | | | vibrato 8.5 Hz, 30% rate spread |

The high band is approximated by a 5th-order Butterworth shelf.

## Latency (44.1 kHz)
| Setting | Delay |
|---|---|
| SMOOTH off | 291 samples (6.6 ms) |
| SMOOTH on | 512 samples (11.6 ms) |

Only the shifter delay line adds delay. plugdata's audio buffers are additional.

## Console
Printed once a second: `mic_in_dB`, `src_dB`, `out_dB` (100 = full scale), `f0_Hz`, `window_ms`.

## Tested
Desktop Pd 0.54.1 on a test build with sliders in place of the five ELSE knobs (test tones: pitch, shelf gain, inflection, latency, gate, limiter, presets). Live on iPad with a USB headset.

## Known issues
- GLIDE deviates for about 0.5 s with a 2000 ms ramp.
- RECORD fails on iOS outside plugdata's folder.
- plugdata on iOS has no input chooser.

## Credits
- Rachman, Liuni, Arias, Lind, Johansson, Hall, Richardson, Watanabe, Dubal, Aucouturier. DAVID. Behavior Research Methods 50:323-343 (2018). DOI 10.3758/s13428-017-0873-y. CC BY 4.0.
- DAVID software, github.com/neuro-team-femto/david. MIT, Copyright (c) 2015 CNRS UMR 9912 STMS / IRCAM.
- Aucouturier, Johansson, Hall, Segnini, Mercadie, Watanabe. PNAS 113(4):948-953 (2016). DOI 10.1073/pnas.1506552113.
- Pure Data, plugdata, ELSE, Cyclone.

## Licence
MIT.
