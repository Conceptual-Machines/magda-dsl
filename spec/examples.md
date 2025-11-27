# MAGDA DSL Examples

Usage examples for the MAGDA DSL.

## Basic Track Creation

```dsl
track()
```

Creates an empty track.

## Track with Instrument

```dsl
track(instrument="Serum")
```

Creates a track with Serum instrument.

## Track with Name and Instrument

```dsl
track(name="Bass", instrument="Serum")
```

Creates a track named "Bass" with Serum instrument.

## Track with Clip

```dsl
track(instrument="Serum").newClip(bar=1, length_bars=4)
```

Creates a track with Serum, then adds a 4-bar clip starting at bar 1.

## Track with MIDI

```dsl
track(instrument="Serum").newClip(bar=1, length_bars=4).addMidi(notes=[{pitch=60, velocity=100, start=0, duration=1}])
```

Creates a track, adds a clip, and adds a MIDI note (C4, velocity 100, starting at beat 0, 1 beat duration).

## Multiple MIDI Notes

```dsl
track(instrument="Serum").newClip(bar=1, length_bars=4).addMidi(notes=[
  {pitch=60, velocity=100, start=0, duration=1},
  {pitch=64, velocity=100, start=1, duration=1},
  {pitch=67, velocity=100, start=2, duration=2}
])
```

Creates a track with a clip containing multiple MIDI notes.

## Track with FX

```dsl
track().addFX(fxname="ReaEQ")
```

Creates a track and adds ReaEQ plugin.

## Track Control

```dsl
track(name="Bass").setVolume(volume_db=-3.0).setPan(pan=0.5)
```

Creates a track named "Bass", sets volume to -3 dB, and pans 50% right.

## Reference Existing Track

```dsl
track(id=1).newClip(bar=5, length_bars=8)
```

References existing track 1 (1-based) and adds a clip.

## Reference Selected Track

```dsl
track(selected=true).newClip(bar=1, length_bars=4)
```

References the currently selected track and adds a clip.

## Complex Chain

```dsl
track(instrument="Serum", name="Lead")
  .newClip(bar=1, length_bars=8)
  .addMidi(notes=[{pitch=60, velocity=100, start=0, duration=1}])
  .setVolume(volume_db=-2.0)
  .setPan(pan=-0.3)
```

Creates a complete track setup with instrument, clip, MIDI, volume, and pan in one chain.

## Multiple Statements

```dsl
track(instrument="Serum", name="Bass").newClip(bar=1, length_bars=4)
track(instrument="Massive", name="Lead").newClip(bar=5, length_bars=8)
```

Creates two tracks with different instruments and clips.

