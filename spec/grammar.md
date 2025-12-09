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
chain: clip_chain | midi_chain | fx_chain | volume_chain | pan_chain | mute_chain | solo_chain | name_chain | selected_chain | delete_chain | delete_clip_chain
```

Methods can be chained together to perform multiple operations on a track.

## Deletion Operations

```
delete_chain: ".delete" "(" ")"
delete_clip_chain: ".delete_clip" "(" delete_clip_params? ")"
delete_clip_params: delete_clip_param ("," SP delete_clip_param)*
delete_clip_param: "clip" "=" NUMBER
                 | "position" "=" NUMBER
                 | "bar" "=" NUMBER
```

**Examples:**
- `.delete()` - Delete the current track
- `.delete_clip(bar=2)` - Delete clip at bar 2
- `.delete_clip(clip=0)` - Delete clip at index 0

## Clip Operations

```
clip_chain: ".new_clip" "(" clip_params? ")"
clip_params: clip_param ("," SP clip_param)*
clip_param: "bar" "=" NUMBER
          | "start" "=" NUMBER
          | "length_bars" "=" NUMBER
          | "length" "=" NUMBER
          | "position" "=" NUMBER
```

**Examples:**
- `.new_clip(bar=1, length_bars=4)` - Create 4-bar clip at bar 1
- `.new_clip(start=0, length=16)` - Create clip starting at beat 0, 16 beats long

## MIDI Operations

```
midi_chain: ".add_midi" "(" midi_params? ")"
midi_params: "notes" "=" array
```

**Examples:**
- `.add_midi(notes=[{pitch=60, velocity=100, start=0, duration=1}])` - Add MIDI note

## FX Operations

```
fx_chain: ".add_fx" "(" fx_params? ")"
fx_params: "fxname" "=" STRING
         | "instrument" "=" STRING
```

**Examples:**
- `.add_fx(fxname="ReaEQ")` - Add FX plugin
- `.add_fx(instrument="Serum")` - Add instrument

## Track Control Operations

```
volume_chain: ".set_volume" "(" "volume_db" "=" NUMBER ")"
pan_chain: ".set_pan" "(" "pan" "=" NUMBER ")"
mute_chain: ".set_mute" "(" "mute" "=" BOOLEAN ")"
solo_chain: ".set_solo" "(" "solo" "=" BOOLEAN ")"
name_chain: ".set_name" "(" "name" "=" STRING ")"
selected_chain: ".set_selected" "(" "selected" "=" BOOLEAN ")"
```

**Examples:**
- `.set_volume(volume_db=-3.0)` - Set track volume to -3 dB
- `.set_pan(pan=0.5)` - Pan track 50% right
- `.set_mute(mute=true)` - Mute track
- `.set_solo(solo=true)` - Solo track
- `.set_name(name="Bass")` - Set track name
- `.set_selected(selected=true)` - Select track

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

