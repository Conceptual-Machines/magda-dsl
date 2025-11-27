# MAGDA DSL

Domain Specific Language for MAGDA (Musical AI Digital Assistant) - a functional scripting language for DAW control.

## Overview

MAGDA DSL is a language specification and parser implementations for translating natural language commands into DAW operations. It provides a clean, chainable syntax for common DAW tasks.

## Quick Example

```dsl
track(instrument="Serum", name="Bass").newClip(bar=1, length_bars=4).addMidi(notes=[{pitch=60, velocity=100, start=0, duration=1}])
```

This creates a track with Serum, adds a 4-bar clip starting at bar 1, and adds a MIDI note.

## Repository Structure

```
magda-dsl/
├── spec/                    # Language specification
│   ├── grammar.md           # Formal grammar (Lark/BNF)
│   ├── examples.md          # Usage examples
│   └── semantics.md         # Language semantics
├── parsers/                 # Parser implementations
│   ├── go/                  # Go parser (reference)
│   ├── cpp/                 # C++ parser (for REAPER)
│   └── python/              # Python parser (future)
├── tests/                   # Test suite
│   └── test_cases.json      # Standard test cases
└── docs/                    # Documentation
    └── LANGUAGE_SPEC.md     # Full specification
```

## Installation

### Go

```bash
go get github.com/conceptual-machines/magda-dsl/parsers/go
```

### C++

```cpp
// Include as submodule or copy parsers/cpp/ to your project
#include "magda-dsl/parsers/cpp/parser.h"
```

## Usage

### Go

```go
import "github.com/conceptual-machines/magda-dsl/parsers/go"

parser := dsl.NewParser()
parser.SetState(state) // Optional: for track resolution
actions, err := parser.ParseDSL(`track(instrument="Serum").newClip(bar=1)`)
```

### C++

```cpp
#include "magda-dsl/parsers/cpp/parser.h"

MagdaDSLParser parser;
parser.SetState(state); // Optional
auto actions = parser.ParseDSL(R"(track(instrument="Serum").newClip(bar=1))");
```

## Language Features

- **Method chaining**: `track().newClip().addMidi()`
- **Track creation**: `track(instrument="Serum", name="Bass")`
- **Track references**: `track(id=1)` or `track(selected=true)`
- **Clip operations**: `.newClip(bar=1, length_bars=4)`
- **MIDI operations**: `.addMidi(notes=[...])`
- **FX operations**: `.addFX(fxname="ReaEQ")`
- **Track control**: `.setVolume(volume_db=-3.0)`

## Documentation

- [Language Specification](docs/LANGUAGE_SPEC.md)
- [Grammar Definition](spec/grammar.md)
- [Examples](spec/examples.md)
- [Parser Implementation Guide](docs/PARSER_GUIDE.md)

## Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

AGPL v3 - See [LICENSE](LICENSE) file for details.

