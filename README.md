# Nodus Loop Compare EQ

**Nodus Loop Compare EQ** is a JSFX effect for REAPER that compares the tonal balance of two passages:

- a **reference** passage whose tonal character you want to preserve; and
- a **target** passage you want to make more similar to the reference.

The effect measures seven broad frequency bands, proposes a restrained EQ curve, and provides level-matched listening so that louder is not mistaken for better.

## Status

Prototype verified in REAPER on Windows on **November 21, 2026**. Installation, loop capture, curve generation, and the Dry, EQ level-matched, EQ actual-level, and Delta listening modes were tested successfully.

The first evaluation should always use copied audio. Do not render over original recordings until you have listened critically and saved a backup.

## Files

- `Nodus-Loop-Compare-EQ.jsfx` — the REAPER effect
- `README.md` — installation, use, and troubleshooting
- `LICENSE` — MIT License

## Installation

JSFX effects do not use an installer. REAPER loads them from its own `Effects` directory.

1. Download `Nodus-Loop-Compare-EQ.jsfx`.
2. Open REAPER.
3. Choose **Options → Show REAPER resource path in explorer/finder**.
4. Open the `Effects` folder inside the resource directory.
5. Optionally create a subfolder named `Nodus`.
6. Copy `Nodus-Loop-Compare-EQ.jsfx` into `Effects` or `Effects/Nodus`.
7. Restart REAPER. Alternatively, reopen or refresh the FX browser.
8. Click the **FX** button on a track.
9. Select **All Plugins** or **JS**, then search for `Nodus`.
10. Double-click **JS: Nodus Loop Compare EQ**.

### Windows filename warning

If the effect does not appear, enable **File name extensions** in Windows Explorer and confirm that the filename is exactly:

```text
Nodus-Loop-Compare-EQ.jsfx
```

It must not be `Nodus-Loop-Compare-EQ.jsfx.txt`.

## Safe first test

For the clearest evaluation, use passages that contain similar material but have noticeably different tonal balance—for example, two recordings of the same voice or instrument made at different distances.

1. Work in a copy of the REAPER project.
2. Put copies of the reference and target passages sequentially on one temporary test track.
3. Add **Nodus Loop Compare EQ** to that track.
4. Set **Strength** to `35%`.
5. Set **Maximum change per band** to `2.0 dB`.
6. Leave **Listen** set to **Dry** while capturing.

### Capture the reference

1. In REAPER's timeline ruler, drag a time selection around **3–5 seconds** of the desired reference passage.
2. Turn on the transport's **Repeat** control.
3. In the effect's **Capture** menu, choose **Arm reference loop**.
4. The Capture menu returns to **Idle** immediately. This is intentional: it is a command menu, not a persistent mode.
5. Start playback and allow the selection to return to its beginning twice.
6. The display progresses from **Armed for the next loop restart (reference)** to **Capturing reference**, then **Reference ready**.

The first return begins capture; the second return completes it.

### Capture the target

1. Stop playback.
2. Make a new 3–5 second time selection around the target passage.
3. Keep **Repeat** on.
4. Choose **Capture → Arm target loop**.
5. Start playback and allow two returns to the beginning.
6. Confirm that the display says **Reference ready     Target ready**.

Once both captures are ready, the seven displayed band gains show the proposed correction.

## Listening and adjustment

Loop the target passage and use the **Listen** menu:

| Mode | Purpose |
|---|---|
| **Dry** | Original, unprocessed signal |
| **EQ level matched** | Corrected signal with automatic loudness matching; recommended for fair comparison |
| **EQ actual level** | Corrected signal without loudness compensation |
| **Delta (dry minus actual EQ)** | Only the difference introduced by the EQ; useful for diagnosis |

Toggle between **Dry** and **EQ level matched** while listening to the target. Begin with `35%` Strength and a `2 dB` limit. Increase them only for diagnosis or after careful listening.

### Controls

| Control | Meaning |
|---|---|
| **Strength (%)** | Scales the proposed correction from none (`0%`) to the complete measured curve (`100%`) |
| **Maximum change per band (dB)** | Limits the largest boost or cut that any individual band may receive |
| **Capture** | Arms or controls reference and target measurement |
| **Listen** | Selects the monitoring comparison |

The analyzed bands are centered at **80, 180, 400, 900, 2000, 4500, and 10000 Hz**.

`A/B trim` shows the current automatic level compensation used by **EQ level matched**.

## Manual capture

Manual capture is available for a passage that does not loop:

1. Start playback first.
2. Choose **Start manual reference** or **Start manual target**.
3. Before playback stops, seeks, or loops, choose **Finish manual capture**.

Use **Cancel capture** to abandon the current attempt without deleting previous successful captures. Use **Clear all** to remove both saved measurements.

## Interpreting subtle results

An inaudible result is not automatically a failure. If the displayed gains remain close to `0.0 dB`, the passages have similar tonal balance and the effect correctly has little to change.

- A quiet **Delta** signal indicates a small correction.
- A difference that is primarily overall loudness will produce little EQ change because the analysis intentionally normalizes level.
- Very short or dissimilar musical content can give a less representative comparison. Prefer 3–5 second passages containing comparable material.

For an obvious diagnostic test, temporarily try `100%` Strength and a `6 dB` limit, then return to conservative values before real use.

## Troubleshooting

### The effect does not appear in REAPER

- Confirm that the file is inside the `Effects` directory shown by REAPER itself.
- Confirm that the filename does not end in `.txt`.
- Restart REAPER.
- Search under **All Plugins** or **JS** for `Nodus`.

### Reference or target remains empty

- Confirm that **Repeat** is on.
- Watch the playhead: it must visibly jump back to the start of the time selection.
- Confirm that the track's audio meter moves during playback; the effect cannot capture silence.
- Use a selection of approximately 3–5 seconds.
- Allow two complete loop returns after arming capture.

### Dry and EQ sound identical

- Confirm that both statuses say **ready**.
- Select **EQ level matched**, not Dry.
- Inspect the seven band gains. Values near zero indicate a genuinely small tonal difference.
- Briefly use **Delta** or stronger diagnostic settings to confirm operation.
- Confirm that the reference and target were not accidentally captured from the same passage.

## What it does not do

Nodus Loop Compare EQ does not repair clipping, remove background noise, correct timing, remove reverberation, or replace critical listening. It proposes a broad tonal correction based on the two captured passages.

Because track FX process the entire track, place material requiring a different correction on its own track before rendering. A practical workflow is to place a temporary copy of the reference passage on the target track for capture, then mute or remove that temporary copy after the curve has been created.

## Authors and license

Created by **Nodus** with **Ankairos** as steward, listener, and first REAPER operator.

Released under the [MIT License](LICENSE).
