# Changelog

## [0.8.47] - 2026-06-07

### Added
- **`SceneKind::KoiPersona`**: main-chat persona mode with a dedicated tool registry profile and `koi_persona_*` prompt protocol.
- **`build_koi_persona_system_prompt`**: assembles Koi identity, instructions, and project context for direct user conversation (no pool collaboration tools).

### Changed
- **Vision delegation**: `delegate_vision_analysis` runs per attachment image instead of batching multiple images in one call.

## [0.8.38] - 2026-06-05

### Added
- **Pluggable loop strategies** (`LoopStrategy` trait) and runtime **contrib registry** for host-supplied loop/compaction strategies.
- Built-in compaction modes: `sliding_window`, `vector_retrieval`.
- `HarnessConfig` slots: `loop_strategy`, `memory_retrieval_prompt`.

### Changed
- Crate versions aligned to the **0.8.x** release line (supersedes the mistaken `v0.7.38` tag).
- Consumers should pin `rev = "v0.8.38"` (not `v0.7.38`).

## [0.8.25] - 2026-05-31

- Stricter heartbeat / org_spec convergence (consumed by openpiscis 0.8.25).
