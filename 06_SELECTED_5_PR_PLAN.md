# 06_SELECTED_5_PR_PLAN.md — BackupX

## Selected PRs (5)

### PR 1: Add troubleshooting section to README
**Problem**: Issue #62 reports users can't start the app on WSL or real servers
**Solution**: Add a troubleshooting section to README covering common startup problems
**Files to modify**: `README.md`, optionally `README.zh-CN.md`
**Effort**: Low | **Risk**: Very low | **Impact**: High (user experience)

**Changes**:
- Add "Troubleshooting" section after Quick Start
- Cover: port 8340 already in use, WSL-specific notes, permission issues, database path problems
- Keep entries brief with links to full docs

---

### PR 2: Add Go test coverage reporting to ci.yml
**Problem**: CI runs `go test ./...` but doesn't track or upload coverage
**Solution**: Add `-coverprofile` to test step and upload coverage artifact
**Files to modify**: `.github/workflows/ci.yml`
**Effort**: Low | **Risk**: Very low | **Impact**: Medium (quality visibility)

**Changes**:
- Install `coverallsapp/github-action@v2` or use `codecov/codecov-action@v4`
- Add `-coverprofile=coverage.out` to test step
- Upload coverage to coveralls/codecov

---

### PR 3: Add go vet linting to ci.yml
**Problem**: CI doesn't run static analysis on Go code
**Solution**: Add `go vet ./...` as a separate CI step
**Files to modify**: `.github/workflows/ci.yml`
**Effort**: Very low | **Risk**: Very low | **Impact**: Medium (code quality)

**Changes**:
- Add step after Build: `go vet ./...`
- Optional: add `golangci-lint` for more comprehensive checks

---

### PR 4: Add tests for httpapi handlers
**Problem**: HTTP API layer (httpapi) likely has low test coverage
**Solution**: Add handler tests for key endpoints (auth, backup tasks, storage targets)
**Files to modify**: Create new `server/internal/httpapi/*_test.go` files
**Effort**: Medium | **Risk**: Low | **Impact**: Medium (confidence in API)

**Changes**:
- Use `httptest` to test handler endpoints
- Test auth endpoints (login, register, 2FA)
- Test CRUD for storage targets and backup tasks
- Use table-driven test patterns

---

### PR 5: Create CONTRIBUTING.md
**Problem**: No CONTRIBUTING.md exists; README mentions Chinese commit messages but doesn't explain process
**Solution**: Create a contributing guide explaining development setup, commit conventions, PR process
**Files to modify**: Create `CONTRIBUTING.md` (and `CONTRIBUTING.zh-CN.md`)
**Effort**: Low | **Risk**: Very low | **Impact**: Medium (community engagement)

**Changes**:
- Development setup instructions (make dev-server, make dev-web)
- Commit message format (conventional commits in Chinese)
- PR submission process
- Testing requirements
- Links to full development docs

---

## Execution Plan

| PR | Order | Estimated Time | Notes |
|----|-------|----------------|-------|
| 1: README troubleshooting | 1st | ~30 min | Quick win, addresses user complaint |
| 5: CONTRIBUTING.md | 2nd | ~45 min | Low effort, high value for community |
| 3: go vet in CI | 3rd | ~20 min | Simple CI addition |
| 2: Coverage reporting | 4th | ~30 min | Depends on understanding test setup |
| 4: httpapi handler tests | 5th | ~2-3 hrs | Most effort, requires understanding API layer |

## DO NOT TOUCH (per task brief)
- `server/pkg/crypto/` — encryption code
- `server/internal/backup/` — deletion/restore logic
- `server/internal/service/restore_service.go` — restore code