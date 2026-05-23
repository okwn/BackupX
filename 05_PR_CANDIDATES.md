# 05_PR_CANDIDATES.md — BackupX

## Open Issues (3 total)
| # | Title | Labels | Difficulty | Focus Area |
|---|-------|--------|------------|------------|
| 62 | [Bug] 建议作者自己测试一下能不能跑起来,本地WSL/真实服务器都无法跑起来 | bug | medium | Dev experience, docs |
| 59 | build(deps): bump npm_and_yarn group across 2 directories with 7 updates | dependencies, javascript | low | Dependency updates |
| 36 | build(deps): bump golang.org/x/image from 0.32.0 to 0.38.0 in /server | dependencies, go | low | Dependency updates |

## Open PRs (2 total)
- None visible from upstream (these are dependabot PRs)

## Candidate PR Ideas (from code analysis)

### Documentation Candidates
1. **Improve README with troubleshooting section** — Issue #62 suggests users can't start the app; a troubleshooting section in README covering common startup issues (WSL, port conflicts, permissions) would help
2. **Contributing guide improvements** — README says "commit messages and PRs on this project are written in Chinese" but no CONTRIBUTING.md exists; could create one with Chinese contribution guidelines
3. **Expand API documentation** — docs-site/docs/reference/api.md likely needs more endpoints documented
4. **Clarify multi-node setup docs** — The cluster/agent architecture is complex; step-by-step diagrams would help

### CI/CD Improvements
5. **Add test coverage reporting to ci.yml** — Backend runs `go test ./...` but no coverage. Could add `-coverprofile` and upload to codecov/coveralls
6. **Add frontend visual regression testing** — web/src/test/ has unit tests but no visual/e2e tests; could add Playwright
7. **Add go vet / staticcheck to ci.yml** — Currently only builds and runs tests; could add linter step
8. **Dependabot is slow/manual** — Issue #36 and #59 are open dependabot PRs; could help by adding `go-consistent` or other auto-fixes

### Test Infrastructure
9. **Increase backend test coverage** — 56 test files exist but many packages likely have low coverage; could add tests for storage, scheduler, notification services
10. **Add integration tests for rclone storage backends** — Storage package tests likely minimal; real rclone backend testing would improve confidence
11. **Frontend component test improvements** — 11 test files in web; could expand coverage for forms, API services

### Error Handling / User Messages
12. **Improve error messages in httpapi handlers** — API error responses could include more context for debugging
13. **Add structured logging to key operations** — app.go shows zap logging is well-established; could audit key paths for missing log statements

### Configuration / Observability
14. **Document metrics endpoint** — Prometheus /metrics endpoint exists but not prominently documented
15. **Add Grafana dashboard JSON to deploy/grafana** — release.yml packages grafana/ but it may be empty; check and populate

## High-Value, Low-Risk Candidates (Focus Areas)
Based on task brief (docs, CI, error messages, test infrastructure):

### Top 5 for BackupX
1. **Docs: Add troubleshooting section to README** (addresses Issue #62)
2. **CI: Add Go test coverage reporting to ci.yml**
3. **CI: Add go vet linting step to ci.yml**
4. **Test: Add backend tests for httpapi handlers**
5. **Docs: Create CONTRIBUTING.md**