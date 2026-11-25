# AGENTS.md — Sumi development instructions

Read [the design index](docs/windows-live-ime/README.md), [implementation plan](docs/windows-live-ime/implementation-plan.md), [macOS input compatibility](docs/windows-live-ime/macos-input-compatibility.md), [WinUI 3 settings](docs/windows-live-ime/winui3-settings.md), [performance/Rust](docs/windows-live-ime/performance-and-rust.md), [licensing](docs/windows-live-ime/licensing.md) and [roadmap](docs/windows-live-ime/roadmap.md) before implementing.

## Non-negotiable requirements

- Sumi is independent of IME Guard; use Mozkey as the upstream. Preserve original licenses, notices, authors and attribution.
- This is the **public fork**. Do not commit or push proprietary Sumi implementation, private test traces, private build artifacts, credentials or signing material here. Use an independently created Private repository for proprietary implementation; verify its visibility and remotes first. If it does not exist, stop before writing proprietary code to this public repository and report the blocker. Do not treat a branch in a public fork as private.
- First reproduce observed macOS Japanese IME behavior (not a guessed keymap). Reference: Japanese romaji input, live conversion on, Windows-style keys off, predictive suggestions off. Record actual Mac version/layout/settings and test state transitions; don't claim parity until verified. Different engine dictionaries and rankings are a separate quality metric.
- Keep existing C++ conversion and TSF as the baseline. Initial release must include a real separate WinUI 3 settings application, preferably C++/WinRT, with input, appearance, keys, dictionaries, AI and learning management. No permanently resident settings UI and no Qt UI in the ordinary user path. Remove Qt runtime from shipping artifacts where possible.
- Measure ARM64/x64 memory, latency and CPU before optimizing. Adopt Rust only if matched-condition measurements or demonstrable safety/maintenance improvements justify it without regression. Do not claim unmeasured savings.
- Test input integrity, focus changes, candidate state, composition, accessibility, high DPI, interoperability, secure fields and local-only inference. No collection of real user input or secret context in diagnostics.
- Separate product GUIDs, paths, IPC, profile data and installer upgrade IDs from Mozkey. Ensure install/update/uninstall coexistence.
- For distribution, audit actual bundled dependencies, dictionaries and models; maintain third-party rights. Do not redistribute unclear materials. Verify Store policy, service dependency, signing and offline installation.
- Never treat unimplemented plans or untested cases as done; document evidence and remaining gaps. Do not publish releases, submit to the Store or enable CI workflows without a separate request.

## Current state

Planning documents only. Upstream code remains unmodified. Start with the reference Mac observations and unmodified Windows baseline; use the roadmap's dependencies and acceptance criteria.
