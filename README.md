# MIDI Piano

A minimal two-octave on-screen MIDI keyboard in a single `index.html` — no
dependencies, no build step. It sends MIDI Note On/Off messages to a local
MIDI destination; it makes no sound of its own, so you'll need a synth or
DAW listening on the other end.

25 keys: C4 (MIDI note 60) through C6 (MIDI note 84).

## Requirements

- **macOS** (tested target; routing instructions below are mac-specific)
- **Chrome or Edge** — the page uses the [Web MIDI API](https://developer.mozilla.org/en-US/docs/Web/API/Web_MIDI_API),
  which Safari and Firefox don't support. The page shows a message instead of
  the keyboard if the API is missing.
- Something to make sound: a software synth/DAW listening to a MIDI input,
  or a hardware MIDI device.

## Setup (macOS)

1. **Create a virtual MIDI bus** (if you don't have a hardware destination):
   open **Audio MIDI Setup** → Window → *Show MIDI Studio* → double-click
   **IAC Driver** → check *Device is online*. This gives you "IAC Driver Bus 1".
2. **Point an instrument at it** — e.g. open GarageBand/Logic/Ableton with a
   software instrument track, or any synth that listens to MIDI input.
3. **Open `index.html`** in Chrome or Edge (double-click works; no server
   needed) and click **Allow** when the browser asks for MIDI permission.
4. Pick your output in the **Output** dropdown. A device with "IAC" in its
   name is auto-selected if present.

## Playing

- **Mouse/trackpad:** click and hold a key.
- **Computer keyboard** (FL Studio–style two-row layout, hints shown on the keys):

  | Octave | White keys | Black keys |
  |---|---|---|
  | C4–B4 | `Z X C V B N M` | `S D G H J` |
  | C5–C6 | `Q W E R T Y U I` | `2 3 5 6 7` |

  `Z` = C4, `Q` = C5, `I` = C6.

Notes are sent on channel 1 with velocity 100. Held notes are released
automatically if the window loses focus or the page closes, so nothing
should get stuck.

## Limitations

Deliberately bare-bones — no audio synthesis, no velocity or channel
controls, no octave shift, no sustain/pitch bend, no MIDI input. See
[SPEC.md](SPEC.md) for the full spec.
