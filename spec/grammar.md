# MAGDA DSL Grammar

Formal grammar definition for the MAGDA DSL.

## Grammar Format

The grammar is defined in Lark format for use with CFG (Context-Free Grammar) parsing.

## Start Rule

```
start: statement+
```

A DSL program consists of one or more statements.

## Statements

```
statement: track_call chain?
```

A statement starts with a track call, optionally followed by a method chain.

## Track Operations

### Track Creation or Reference

```
track_call: "track" "(" track_params? ")"
track_params: track_param ("," SP track_param)*
           | NUMBER  // track(1) references existing track 1
track_param: "instrument" "=" STRING
           | "name" "=" STRING
           | "index" "=" NUMBER
           | "id" "=" NUMBER  // track(id=1) references existing track 1
           | "selected" "=" BOOLEAN  // track(selected=true) references currently selected track
```

**Examples:**
- `track()` - Create empty track
- `track(instrument="Serum")` - Create track with instrument
- `track(name="Bass", instrument="Serum")` - Create track with name and instrument
- `track(1)` - Reference existing track 1 (1-based)
- `track(id=1)` - Reference existing track 1 (explicit)
- `track(selected=true)` - Reference currently selected track

## Method Chaining

```
chain: clip_chain | midi_chain | fx_chain | volume_chain | pan_chain | mute_chain | solo_chain | name_chain
```

Methods can be chained together to perform multiple operations on a track.

## Clip Operations

```
clip_chain: ".newClip" "(" clip_params? ")" (midi_chain | fx_chain | volume_chain | pan_chain | mute_chain | solo_chain | name_chain)?
clip_params: clip_param ("," SP clip_param)*
clip_param: "bar" "=" NUMBER
          | "start" "=" NUMBER
          | "end" "=" NUMBER
          | "length_bars" "=" NUMBER
          | "length" "=" NUMBER
          | "position" "=" NUMBER
```

**Examples:**
- `.newClip(bar=1, length_bars=4)` - Create 4-bar clip at bar 1
- `.newClip(start=0, length=16)` - Create clip starting at beat 0, 16 beats long

## MIDI Operations

```
midi_chain: ".addMidi" "(" midi_params? ")"
midi_params: "notes" "=" array
           | "note" "=" midi_note
midi_note: "{" midi_note_fields "}"
midi_note_fields: midi_note_field ("," SP midi_note_field)*
midi_note_field: "pitch" "=" NUMBER
              | "velocity" "=" NUMBER
              | "start" "=" NUMBER
              | "duration" "=" NUMBER
```

**Examples:**
- `.addMidi(notes=[{pitch=60, velocity=100, start=0, duration=1}])` - Add MIDI note
- `.addMidi(note={pitch=60, velocity=100, start=0, duration=1})` - Add single MIDI note

## FX Operations

```
fx_chain: ".addFX" "(" fx_params? ")"
fx_params: "fxname" "=" STRING
         | "instrument" "=" STRING
```

**Examples:**
- `.addFX(fxname="ReaEQ")` - Add FX plugin
- `.addFX(instrument="Serum")` - Add instrument (alias for addInstrument)

## Track Control Operations

```
volume_chain: ".setVolume" "(" "volume_db" "=" NUMBER ")"
pan_chain: ".setPan" "(" "pan" "=" NUMBER ")"
mute_chain: ".setMute" "(" "mute" "=" BOOLEAN ")"
solo_chain: ".setSolo" "(" "solo" "=" BOOLEAN ")"
name_chain: ".setName" "(" "name" "=" STRING ")"
```

**Examples:**
- `.setVolume(volume_db=-3.0)` - Set track volume to -3 dB
- `.setPan(pan=0.5)` - Pan track 50% right
- `.setMute(mute=true)` - Mute track
- `.setSolo(solo=true)` - Solo track
- `.setName(name="Bass")` - Set track name

## Arrays

```
array: "[" (value ("," SP value)*)? "]"
value: STRING | NUMBER | BOOLEAN | midi_note | array
```

**Examples:**
- `[1, 2, 3]` - Array of numbers
- `["a", "b", "c"]` - Array of strings
- `[{pitch=60}, {pitch=64}]` - Array of MIDI notes

## Terminals

```
SP: " "
STRING: /"[^"]*"/
NUMBER: /-?\d+(\.\d+)?/
BOOLEAN: "true" | "false"
```

## Complete Grammar

See the Lark grammar definition in the Go implementation: `parsers/go/grammar.lark` (to be created)

