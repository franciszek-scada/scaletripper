## ScaleTripper

**ScaleTripper** is a zero-dependency Python CLI utility that generates 16-measure swinging jazz improvisation MIDI files from either 20 built-in musical scales or your own custom semitone interval definitions. 

The utility is designed to explore scales and incorporate the explorations into compositions. It is deliberately kept as simple as possible with the assumption that the composer will use their own MIDI development environment to impart different instrument profiles.

---

## Features

- **Zero External Dependencies:** Uses only Python's standard library (`argparse`, `random`, `struct`, `sys`) to build raw Standard MIDI Format 0 files.
- **20 Built-In Scales:** Includes pentatonic, bebop, symmetrical, and world/exotic scales accessible via one-word identifiers.
- **Custom Scale Support:** Pass any comma-separated list of semitone offsets from the root note (`0`).
- **Authentic Jazz Swing Feel:** Generates syncopated eighth-note phrasing with a 66% swing ratio, dynamic MIDI velocities, and Acoustic Grand Piano (GM Program 0) mapping across a two-octave range starting at Middle C (`C4`).

---

## Requirements

- Python **3.8+** (tested on Python 3.14)
- No third-party packages required

---

## Installation

1. Save the script as `ScaleTripper` (or `ScaleTripper.py`).
2. *(Optional on Linux/macOS)* Make the script executable:

```bash
chmod +x ScaleTripper
```

---

## Usage

Running `ScaleTripper` with no arguments or with `--help` (`-h`) prints the program header, description, and available options:

```bash
./ScaleTripper --help
```

### Command-Line Options

| Flag | Required | Default | Description |
| :--- | :---: | :--- | :--- |
| `--scale <NAME>` | Yes* | — | One-word identifier for one of the 20 preset scales. |
| `--custom <LIST>` | Yes* | — | Comma-separated semitone offsets from the root (e.g., `"0,2,4,6,8,10"`). |
| `--output <FILE>` | No | `output_improvisation.mid` | Destination path/filename for the generated MIDI file. |
| `--bpm <INT>` | No | `120` | Playback tempo in beats per minute. |
| `-h`, `--help` | No | — | Show the help message and exit. |

*\*Note: `--scale` and `--custom` are mutually exclusive; you must provide one or the other.*

---

## Examples

### 1. Generate from a Preset Scale
Generate a swinging improvisation in the **Major Bebop** scale at 140 BPM:

```bash
./ScaleTripper --scale MajorBebop --output bebop_solo.mid --bpm 140
```

### 2. Generate from Custom Intervals
Create a MIDI track using a custom Whole Tone scale (`0, 2, 4, 6, 8, 10`) at 110 BPM:

```bash
./ScaleTripper --custom "0,2,4,6,8,10" --output whole_tone.mid --bpm 110
```

### 3. Run via Python Interpreter
If you haven't set executable permissions (`chmod +x`):

```bash
python3 ScaleTripper --scale JapanesePentatonic --output in_sen.mid
```

---

## Supported Preset Scales

Each scale is defined by its semitone distance from the root note (`0` = C4 / MIDI note `60`):

| One-Word Identifier | Semitone Intervals | Notes (Root = C) |
| :--- | :--- | :--- |
| `MajorPentatonic` | `[0, 2, 4, 7, 9]` | C, D, E, G, A |
| `NewPentatonic` | `[0, 2, 4, 6, 9]` | C, D, E, F♯, A |
| `JapanesePentatonic` | `[0, 1, 5, 7, 8]` | C, D♭, F, G, A♭ |
| `BalinesePentatonic` | `[0, 1, 3, 7, 8]` | C, D♭, E♭, G, A♭ |
| `PelogPentatonic` | `[0, 1, 4, 7, 8]` | C, D♭, E, G, A♭ |
| `HemitonicPentatonic3` | `[0, 1, 5, 7, 10]` | C, D♭, F, G, B♭ |
| `HarmonicMinor` | `[0, 2, 3, 5, 7, 8, 11]` | C, D, E♭, F, G, A♭, B |
| `HarmonicMinorDom7th` | `[0, 1, 4, 5, 7, 8, 10]` | C, D♭, E, F, G, A♭, B♭ |
| `MelodicMinor` | `[0, 2, 3, 5, 7, 9, 11]` | C, D, E♭, F, G, A, B |
| `MelodicMinorDom7th` | `[0, 2, 4, 6, 7, 9, 10]` | C, D, E, F♯, G, A, B♭ |
| `Esoteric6th` | `[0, 1, 4, 7, 8, 11]` | C, D♭, E, G, A♭, B |
| `Augmented` | `[0, 3, 4, 7, 8, 11]` | C, E♭, E, G, A♭, B |
| `Diminished` | `[0, 2, 3, 5, 6, 8, 9, 11]` | C, D, E♭, F, F♯, A♭, A, B |
| `Enigmatic` | `[0, 1, 4, 6, 8, 10, 11]` | C, D♭, E, F♯, G♯, B♭, B |
| `GypsyByzantine` | `[0, 1, 4, 5, 7, 8, 11]` | C, D♭, E, F, G, A♭, B |
| `ArabianMajorLocrian` | `[0, 2, 4, 5, 6, 8, 10]` | C, D, E, F, F♯, A♭, B♭ |
| `Persian` | `[0, 1, 4, 5, 6, 8, 11]` | C, D♭, E, F, F♯, A♭, B |
| `Spanish8Tone` | `[0, 1, 3, 4, 5, 6, 8, 10]` | C, D♭, E♭, E, F, F♯, A♭, B♭ |
| `NativeAmerican` | `[0, 3, 5, 7, 10]` | C, E♭, F, G, B♭ |
| `MajorBebop` | `[0, 2, 4, 5, 7, 8, 9, 11]` | C, D, E, F, G, G♯, A, B |

---

## Output Specifications

- **Format:** Standard MIDI File (`.mid`), Format 0 (single track)
- **Resolution:** 480 ticks per quarter note (PPQ)
- **Length:** 16 measures in `4/4` time
- **Pitch Range:** Two octaves starting at Middle C (`MIDI 60`–`83`)
- **Instrument:** Acoustic Grand Piano (`Program 0` on `Channel 1`)