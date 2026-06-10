# MIDI Piano — Spec

A minimal two-octave on-screen MIDI keyboard that sends MIDI messages to a
selectable local MIDI destination. No built-in sound — an external MIDI
instrument (listening on "IAC Driver Bus 1") produces the audio.

## Form

- A single self-contained `index.html` (HTML + CSS + JS, no dependencies, no
  build step). Opened directly from disk in Chrome or Edge.
- Uses the Web MIDI API. If the API is unavailable (e.g. Firefox, Safari),
  the page shows a clear message instead of the keyboard.

## Keyboard

- 25 keys: C4 (MIDI note 60) through C6 (MIDI note 84). 15 white, 10 black.
- Keys highlight while held (mouse or computer keyboard).
- Each key is labeled with its computer-keyboard letter; C keys also show
  their note name (C4, C5, C6).

## MIDI behavior

- Output device dropdown listing all available MIDI destinations.
  - Auto-selects the first device whose name contains "IAC" if present,
    otherwise the first device.
  - Refreshes automatically when devices are added/removed (statechange).
- Note On (0x90) with velocity 100 on press; Note Off (0x80) on release.
- Channel 1, fixed. No velocity control, no octave shift (bare bones).
- Stuck-note safety: all held notes get Note Off on window blur, on pointer
  leaving a key while held, and on page unload.
- The target instrument is monophonic; the app does not need chord handling
  beyond sending correct per-key on/off pairs.

## Input

- Mouse/trackpad: pointer down on a key = Note On, pointer up/leave = Note Off.
- Computer keyboard, two-row mapping (FL Studio style):
  - Lower octave C4–B4: `Z S X D C V G B H N J M`
    (Z=C4, S=C#4, X=D4, D=D#4, C=E4, V=F4, G=F#4, B=G4, H=G#4, N=A4, J=A#4, M=B4)
  - Upper octave C5–C6: `Q 2 W 3 E R 5 T 6 Y 7 U I`
    (Q=C5, 2=C#5, W=D5, 3=D#5, E=E5, R=F5, 5=F#5, T=G5, 6=G#5, Y=A5, 7=A#5, U=B5, I=C6)
  - Key auto-repeat is ignored; a held key sends one Note On.

## Out of scope

- Audio synthesis, velocity/channel controls, octave shifting, MIDI input,
  sustain pedal, pitch bend, persistence of settings.
