# Contributing to MAGDA DSL

Thank you for your interest in contributing to MAGDA DSL!

## How to Contribute

### Reporting Issues

- Use GitHub Issues to report bugs or suggest features
- Include clear descriptions and reproduction steps
- For parser bugs, include the DSL code that fails

### Contributing Code

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/your-feature-name`
3. **Make your changes**
4. **Add tests** for new functionality
5. **Ensure tests pass**: `go test ./...` (for Go parser)
6. **Commit your changes**: `git commit -m "Add feature: description"`
7. **Push to your fork**: `git push origin feature/your-feature-name`
8. **Create a Pull Request**

### Parser Implementations

We welcome parser implementations in new languages! When contributing a parser:

1. Create it in `parsers/{language}/`
2. Follow the existing Go parser as a reference
3. Add tests that match the standard test suite
4. Update the main README.md with usage instructions
5. Document any language-specific considerations

### Code Style

- **Go**: Follow standard Go conventions, use `gofmt`
- **C++**: Follow C++20 standards, use consistent formatting
- **Python**: Follow PEP 8, use type hints

### Testing

All parsers must pass the standard test suite in `tests/test_cases.json`. Add new test cases there if you're adding language features.

## Questions?

Open an issue or discussion on GitHub!

