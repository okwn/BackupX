# 01_REPO_MAP.md — BackupX

## Repository Structure
```
BackupX/
├── .github/
│   ├── ISSUE_TEMPLATE/
│   └── workflows/
│       ├── ci.yml          # Go + React CI
│       ├── docs.yml        # GitHub Pages deployment
│       └── release.yml     # Multi-arch release + Docker Hub
├── LICENSE                 # Apache-2.0
├── README.md               # English
├── README.zh-CN.md         # Chinese
├── Makefile                # build, dev-server, dev-web, test, docker, clean
├── docker-compose.yml      # Docker one-click setup
├── screenshots/            # UI screenshots
├── deploy/                 # install.sh, grafana/, docker/, nginx.conf
├── server/                 # Go backend (module: backupx/server)
│   ├── cmd/backupx/         # main.go, agent.go, backint.go
│   ├── internal/
│   │   ├── agent/          # Agent communication
│   │   ├── app/             # App initialization
│   │   ├── apperror/        # Error types
│   │   ├── backup/          # Backup execution engine
│   │   ├── backint/         # SAP HANA Backint protocol
│   │   ├── config/          # Viper configuration
│   │   ├── database/        # GORM/SQLite setup
│   │   ├── http/            # Gin middleware/router
│   │   ├── httpapi/         # REST API handlers
│   │   ├── installscript/   # Agent install scripts
│   │   ├── logger/          # Zap + Lumberjack logging
│   │   ├── metrics/         # Prometheus metrics
│   │   ├── model/           # GORM models
│   │   ├── notify/          # Email/webhook/Telegram notifications
│   │   ├── repository/      # Data access layer
│   │   ├── scheduler/       # Cron scheduling (robfig/cron)
│   │   ├── security/        # JWT, bcrypt, AES-256-GCM
│   │   ├── service/        # Business logic services
│   │   └── storage/         # rclone storage backends
│   └── pkg/
│       ├── compress/        # Gzip compression
│       ├── crypto/          # File encryption (AES-256-GCM)
│       └── response/        # API response helpers
├── web/                    # React/TypeScript frontend
│   ├── src/
│   │   ├── components/      # UI components (storage-targets, backup-tasks, notifications, auth-guard, etc.)
│   │   ├── pages/          # Page components (nodes/, etc.)
│   │   ├── stores/         # Zustand state stores
│   │   ├── services/       # API client (axios)
│   │   ├── hooks/          # Custom React hooks
│   │   ├── router/         # React Router (ProtectedRoute)
│   │   ├── locales/        # i18n (English + Chinese)
│   │   ├── types/          # TypeScript types
│   │   ├── utils/          # Utility functions
│   │   └── styles/         # CSS/styles
│   ├── package.json        # Vitest for tests
│   ├── vite.config.ts      # Vite bundler config
│   └── tsconfig.json       # TypeScript config
├── docs-site/              # Docusaurus documentation site
│   ├── docs/              # English docs
│   ├── i18n/zh-CN/        # Chinese docs
│   └── package.json        # Docusaurus build
└── server/config.example.yaml  # Example configuration
```

## Technology Stack
| Layer | Technology |
|-------|------------|
| Backend language | Go 1.25 |
| Web framework | Gin v1.10.1 |
| Database | SQLite via GORM v1.25 + glebarez/sqlite |
| Auth | JWT (golang-jwt/jwt) + bcrypt |
| Encryption | AES-256-GCM (golang.org/x/crypto) |
| Storage | rclone v1.73 (70+ backends) |
| Scheduling | robfig/cron v3 |
| Logging | Zap + Lumberjack |
| Metrics | Prometheus client_golang |
| Frontend | React 18 + TypeScript |
| UI framework | Arco Design |
| State management | Zustand |
| Bundler | Vite |
| Testing (backend) | go test |
| Testing (frontend) | Vitest + Testing Library |
| Documentation | Docusaurus |

## CI/CD Pipeline
```
ci.yml:
  - backend: go build + go test (Go 1.25, ubuntu-latest)
  - frontend: npm ci + tsc --noEmit + npm test + npm run build (Node 20)

docs.yml:
  - Build Docusaurus site → GitHub Pages

release.yml:
  - build-web: npm ci + npm run build
  - build-release: Go cross-compile (linux/amd64 + linux/arm64) → GitHub Release
  - build-docker: Multi-arch Docker (linux/amd64 + linux/arm64) → Docker Hub
```

## Key Go Dependencies (direct imports)
- `github.com/gin-gonic/gin` — HTTP framework
- `github.com/golang-jwt/jwt/v5` — JWT auth
- `github.com/robfig/cron/v3` — Cron scheduling
- `github.com/rclone/rclone` — Storage backends
- `gorm.io/gorm` + `github.com/glebarez/sqlite` — ORM + SQLite
- `github.com/spf13/viper` — Config management
- `go.uber.org/zap` — Structured logging
- `github.com/prometheus/client_golang` — Metrics
- `golang.org/x/crypto` — AES-256-GCM encryption

## Key REST API Areas (httpapi handlers)
- Auth: login, register, OTP (TOTP)
- Nodes: agent management, commands, labels
- Storage targets: CRUD for 70+ backends
- Backup tasks: scheduling, retention
- Backup records: history, restore points
- Audit logs: compliance logging

## Known Issues
- Issue #62 (open, bug): "建议作者自己测试一下能不能跑起来,本地WSL/真实服务器都无法跑起来" — App doesn't start on WSL/real servers
- Issue #59 (open, dependencies): npm_and_yarn group bump across 2 directories (7 updates)
- Issue #36 (open, dependencies): golang.org/x/image bump in /server

## Focus Areas for PRs
1. **Documentation**: docs-site content, README improvements, API docs
2. **CI/CD**: Workflow improvements, test coverage
3. **Test infrastructure**: More backend tests, frontend component tests
4. **Error handling**: User-facing error messages, logging improvements