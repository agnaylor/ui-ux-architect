# Tech Stack Canon — Language Routing

> When the requirements imply the wrong language, push back before writing code.

## TypeScript — UI & Web Applications

**Use when:**
- Building any state-heavy front-end (React, Next.js, React Native).
- Live data sync, optimistic UI, multi-step workflows.
- Production reliability matters (TS strict mode catches what JS hides).

**Pair with:** React 18+, Tailwind (with custom tokens), shadcn/ui, Zustand or React Query for state.

**Do not use for:** Pure backend logic (use Python). System-level performance work (use Rust).

---

## Python — Backend, APIs, Data, Scripting

**Use when:**
- REST/GraphQL API layer.
- Data pipelines, ML inference, batch processing.
- Glue code, automation scripts, log sweeps.

**Pair with:** FastAPI (preferred), Pydantic, SQLAlchemy, Polars over Pandas for performance.

**Do not use for:** Highly concurrent network servers (use Go). GPU compute kernels (use Rust). Native AEC plugins (use C#).

---

## Rust — Hardware, Performance, Memory Safety

**Use when:**
- Wringing performance from dual-GPU setups (Intel Arc, NVIDIA).
- Building daemons, long-running nodes on bare-metal Ubuntu.
- Replacing a slow Python hot path (call from Python via PyO3 FFI — don't rewrite the whole app).

**Pair with:** Tokio for async, Axum for HTTP, candle or burn for ML compute.

**Do not use for:** Quick prototypes. Surface-level UI (TypeScript is faster to ship).

---

## Go — Server Orchestration & Concurrency

**Use when:**
- Orchestrating multi-node server clusters.
- Heartbeat monitoring, load balancing, gateway proxies.
- 10k+ concurrent connections (IoT streams, websocket fan-out).

**Pair with:** Standard library where possible. `chi` or `gin` for HTTP. `nats` for messaging.

**Strength:** Statically compiled single binaries deploy without dependency hell.

**Do not use for:** Complex business logic (Python expresses it better). UI (TypeScript).

---

## C# / .NET — AEC Integration & Compiled Desktop Plugins

**Use when:**
- Building plugins for ArchiCAD, Bluebeam, Revit, AutoCAD.
- Tapping deep APIs that .NET languages access exclusively (GDL script logic, native object models).
- Native Windows desktop add-ons that must match host-app UI conventions.

**Pair with:** WPF for plugin UI shells. .NET 8+. Roslyn for source generation if needed.

**Do not use for:** Cross-platform desktop (use Electron + TS or Tauri + Rust). Web backends.

---

## Routing Cheat Sheet

| Problem | Language |
|---|---|
| "I need a dashboard" | TypeScript + React |
| "Sync 50k IoT streams" | Go |
| "Plugin for ArchiCAD that extracts geometry" | C# |
| "Sweep nightly logs, write CSV" | Python |
| "Train a model on dual GPUs" | Python orchestration → Rust compute |
| "Mobile app to manage recipes" | TypeScript (React Native) + Python API |
| "Knowledge base with markdown editing" | TypeScript (Next.js) + Python API |
| "Real-time control panel for a server cluster" | TypeScript front + Go backend + Rust agents |

---

## Cross-Language Patterns

### Python ↔ Rust (FFI)
Compile the hot path in Rust, expose via PyO3, call from Python like any module. Don't rewrite the whole codebase to gain 100x on one function.

### TypeScript ↔ Go (HTTP/gRPC)
Standard REST or gRPC contract. Generate TS types from Go structs via OpenAPI codegen — never hand-sync.

### TypeScript ↔ C# (No direct bridge)
For AEC plugins with a web UI, run a local HTTP server inside the C# plugin and serve a TypeScript SPA against it.
