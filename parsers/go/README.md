# MAGDA DSL - Go Parser

Go implementation of the MAGDA DSL parser.

## Status

✅ **Reference Implementation** - This is the canonical Go parser for MAGDA DSL.

## Installation

```bash
go get github.com/conceptual-machines/magda-dsl/parsers/go
```

## Usage

```go
package main

import (
    "fmt"
    "github.com/conceptual-machines/magda-dsl/parsers/go"
)

func main() {
    parser := dsl.NewParser()
    
    // Optional: Set state for track resolution
    state := map[string]interface{}{
        "tracks": []map[string]interface{}{
            {"name": "Track 1", "selected": true},
        },
    }
    parser.SetState(state)
    
    // Parse DSL code
    dslCode := `track(instrument="Serum").newClip(bar=1, length_bars=4)`
    actions, err := parser.ParseDSL(dslCode)
    if err != nil {
        panic(err)
    }
    
    fmt.Printf("Parsed %d actions\n", len(actions))
    for _, action := range actions {
        fmt.Printf("Action: %v\n", action)
    }
}
```

## API

### NewParser()

Creates a new DSL parser instance.

### SetState(state map[string]interface{})

Sets the current DAW state for track resolution. Used to resolve track references like `track(selected=true)`.

### ParseDSL(dslCode string) ([]map[string]interface{}, error)

Parses DSL code and returns an array of action objects. Each action is a map with:
- `action`: Action type (e.g., "create_track", "create_clip_at_bar")
- Additional fields specific to the action type

## Output Format

The parser converts DSL to action objects. For example:

**Input:**
```dsl
track(instrument="Serum", name="Bass").newClip(bar=1, length_bars=4)
```

**Output:**
```json
[
  {
    "action": "create_track",
    "instrument": "Serum",
    "name": "Bass"
  },
  {
    "action": "create_clip_at_bar",
    "track": 0,
    "bar": 1,
    "length_bars": 4
  }
]
```

## Testing

```bash
go test ./...
```

## Contributing

See the main [MAGDA DSL repository](../../README.md) for contribution guidelines.

