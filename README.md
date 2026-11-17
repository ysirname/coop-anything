# Uncharted 3: Drake's Deception (2011)

| | |
|---|---|
| Engine | Naughty Dog proprietary (PS3) |
| Versions tested | none yet — user owns PS3 disc, version/build unknown |
| Projects | none found (gap) |
| QA level | none |
| Last updated | 2026-11-15 |

## Where things stand

Nobody has built campaign co-op for Uncharted 3. The game is PS3-only with no PC port, no decompilation, and no scripting layer. The campaign is single-player only; the game ships a separate competitive multiplayer mode. This project is at Phase 0 (triage) only — no code has been written.

## Existing work

None found. Searched `DIRECTORY.md` and `games/` in cranebeaker/coop-anything, plus general web search. No co-op project exists for the Uncharted 3 campaign.

## How the game works (for co-op)

- **Engine:** Naughty Dog proprietary in-house engine, PS3 Cell architecture. Closed binary, no symbols, no source.
- **Scripting layer:** none available to modders.
- **Netcode:** competitive multiplayer mode exists but is separate from the campaign; no campaign replication, server, or client netcode.
- **Save system:** unknown — needs investigation on PS3 save format and where campaign progress is stored.
- **Level loading:** unknown — needs reverse engineering.
- **Client-side vs server-side:** N/A for single-player campaign; everything is local.
- **Tools:** RPCS3 (PS3 emulator), RPCS3 debugger, Ghidra (headless decompilation), PINE protocol (PCSX2-style IPC — unknown if RPCS3 supports it).

## What we changed

Nothing yet. No code written.

## QA

No tests exist yet. Per AGENTS.md, QA must use bots, not human playtests. Planned:
1. Boot test: two RPCS3 instances load the same save state.
2. Memory census: find player struct, verify addresses stable across loads.
3. Bridge test: write player A's pose into a mailbox, assert player B sees remote avatar.
4. Full-state catch-up test after a peer restart.

## How to play

Not playable yet. This is a research/Reverse-engineering phase project.

## Known issues

- No PC port exists; must use RPCS3 PS3 emulation.
- No prior co-op work to build on.
- PS3 RAM-sync via memory bridge is untested territory (no verified project).
- Player struct offsets unknown in proprietary engine.
- Cutscenes and loading screens need gating so both clients stay in step.

## Next steps

1. Fork cranebeaker/coop-anything, branch `game/uncharted-3`, add these files.
2. Open a "claim a game" issue.
3. Add `data/directory.yaml` entry with `kind: gap`.
4. Dump own PS3 disc; verify RPCS3 runs the campaign.
5. Reverse-engineer player struct with RPCS3 debugger + Ghidra.
6. Build memory-sync bridge between two RPCS3 instances.
