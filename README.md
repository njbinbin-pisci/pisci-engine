# piscis-engine

OS / UI-neutral **agent runtime kernel**, extracted from
[`openpiscis`](../openpiscis) so it can be shared by multiple host products
(the `openpiscis` desktop app and the `codez` AI IDE).

This repo contains only the host-agnostic layers — it **never** depends on
Tauri, any GUI framework, or platform-specific tooling. Hosts inject all of
that through the trait contracts in `pisci-core`.

## Crates

| Crate | Role |
|---|---|
| `pisci-core` | Pure contracts: `HostRuntime` / `EventSink` / `Notifier` / `HostTools` / `SecretsStore` + shared schema types. Depends only on serde / chrono / anyhow / async-trait. |
| `pisci-kernel` | The agent runtime: agent loop + harnesses, LLM adapters (claude / openai / qwen / deepseek / kimi / minimax / zhipu), SQLite store + encrypted settings, memory + Dream consolidation, policy / approval, scheduler, security, and platform-neutral tools (file_*, shell, code_run, web_search, ssh, mcp, …). |
| `pisci-cli` | Headless host adapter + the `openpiscis-headless` binary (NDJSON streaming, env-var secrets). Cross-platform agent runner for CI / evals / IDE integrations. |

## Build & test

```bash
cargo build                                   # whole workspace
cargo test  -p pisci-core -p pisci-kernel -p pisci-cli --lib --bins
cargo clippy -p pisci-core -p pisci-kernel -p pisci-cli --all-targets -- -D warnings
cargo build -p pisci-cli --release --bin openpiscis-headless
```

## Consuming this engine from a host

Hosts depend on the crates as path (local dev) or git (CI / release)
dependencies. With both repos checked out as siblings:

```
Projects/
├── piscis-engine/      ← this repo
├── openpiscis/         ← desktop host
└── codez/             ← AI IDE host
```

a host's `Cargo.toml` references:

```toml
[dependencies]
pisci-core   = { path = "../../piscis-engine/pisci-core" }
pisci-kernel = { path = "../../piscis-engine/pisci-kernel" }
# Swap for a git source once this repo has a published remote:
# pisci-kernel = { git = "https://…/piscis-engine", package = "pisci-kernel" }
```

## Provenance

Extracted from `openpiscis` with `git filter-repo`, preserving the full commit
history of `pisci-core` / `pisci-kernel` / `pisci-cli`. The desktop-coupled
`pisci_compact_one` benchmark binary (which links `pisci-desktop`) was
intentionally left behind in `openpiscis`.
