# 00_STATE.md — BackupX

## Repository Identity
- **Full name**: Awuqing/BackupX
- **Fork**: okwn/BackupX (cloned to /root/oss-pr-campaign/repos/backupx)
- **License**: Apache-2.0
- **Archived**: No
- **Language**: Go (backend), React/TypeScript (frontend), SQLite (embedded DB)
- **Default branch**: main
- **Topics**: backupx

## Key Numbers
| Metric | Value |
|--------|-------|
| Stars | 97 |
| Watchers | 97 |
| Forks (upstream) | 15 |
| Open Issues | 3 |
| Open PRs | 2 |
| Go version | 1.25 (go.mod declares 1.25.0) |
| Node version | 20 |

## Phase 1 Status: COMPLETE
- [x] Fork created at okwn/BackupX
- [x] Cloned to /root/oss-pr-campaign/repos/backupx
- [x] Upstream remote added (Awuqing/BackupX)
- [x] Default branch: main (confirmed from git and API)
- [x] Archived: false, License: Apache-2.0

## Phase 2-6 Status: IN PROGRESS

## Critical Focus Areas (per task brief)
- **Docs**: Documentation site (docs-site/), README, contributing guide, API docs
- **CI**: GitHub Actions workflows (.github/workflows/)
- **Error messages**: Logging, error handling, user-facing messages
- **Test infrastructure**: Test files in server/ and web/src/ (vitest + go test)

## DO NOT TOUCH (per task brief)
- Deletion code
- Restore code
- Encryption code (file_cipher.go, crypto package)

## Environment Notes
- Go is NOT installed in the execution environment — cannot run `go test` locally
- Node.js/npm not verified available
- GitHub CLI (`gh`) is available and used for API queries