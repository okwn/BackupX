# Contributing to BackupX

Thank you for your interest in contributing to BackupX! This guide covers everything you need to know to set up your development environment and submit contributions.

## Development Setup

### Prerequisites

- **Go** 1.25+
- **Node.js** 18+
- **npm** 9+

### Quick Start

```bash
# Clone the repository
git clone https://github.com/Awuqing/BackupX.git && cd BackupX

# Terminal 1 — Start the backend server
make dev-server

# Terminal 2 — Start the frontend with hot module replacement
make dev-web
```

The backend runs at `http://localhost:8340` and the frontend supports Vite HMR for fast iteration.

### Building for Production

```bash
# Build both server and web frontend
make build

# Build server only (produces server/bin/backupx)
make build-server

# Build web only (produces web/dist)
make build-web
```

## Testing

Run all tests before submitting a PR:

```bash
# Run all tests (server + web)
make test

# Run server tests only
make test-server

# Run web tests only
make test-web
```

## Commit Message Format

This project uses **Conventional Commits** (中文撰写). Format:

```
<type>(<scope>): <subject>

<body>
```

### Type Prefixes

| Type | Description |
|------|-------------|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `style` | Code style changes (formatting, semicolons, etc.) |
| `refactor` | Code refactoring |
| `perf` | Performance improvements |
| `test` | Adding or updating tests |
| `chore` | Build process, auxiliary tools, dependencies |

### Examples

```
feat(storage): add support for Wasabi S3 backend

fix(schedule): correct cron expression parsing for monthly jobs

docs: add CONTRIBUTING.md
```

## Pull Request Process

1. **Fork** the repository and create a feature branch from `main`
2. **Develop** your feature or fix — write tests if applicable
3. **Test** ensure `make test` passes
4. **Commit** using conventional commit format (Chinese commit messages)
5. **Push** and create a PR against `main`

### PR Description Guidelines

- Provide a clear summary of what the PR does
- Explain the motivation if it's a new feature or bug fix
- Link any related issues
- For documentation PRs, testing is not required

## More Information

For detailed development documentation, see the full guide at:

- [Development Setup](https://awuqing.github.io/BackupX/docs/development/setup)
- [Contributing Guide](https://awuqing.github.io/BackupX/docs/development/contributing)

## License

By contributing to BackupX, you agree that your contributions will be licensed under the [Apache License 2.0](LICENSE).