# Uncharted 3: Drake's Deception — Campaign Co-op Notes

*Private state for this session. Not committed to the fork. See AGENTS.md ground rule 1.*

## Game identity (Phase 0: Triage — complete)

| Field | Value | Source |
|---|---|---|
| Exact game | Uncharted 3: Drake's Deception (2011) | user |
| Store / platform | PS3 disc (user owns); no PC version exists | user |
| Version / build | unknown — need to check disc serial / update version | unknown |
| Engine | Naughty Dog proprietary in-house engine (PS3 Cell) | known |
| OS | Windows 11 (host PC) running RPCS3 PS3 emulator | user hardware |
| CPU | AMD Ryzen 5 5600G (3.90 GHz) | user |
| GPU | NVIDIA GeForce RTX 3060 (12 GB) + Radeon Graphics | user |

## Triage answers

1. **Which exact game?** Uncharted 3: Drake's Deception (2011), PS3 exclusive. Campaign is single-player only. The game ships a separate competitive multiplayer mode, but that is not campaign co-op.
2. **Is it already done?** No. Checked `DIRECTORY.md` and `games/` in cranebeaker/coop-anything — no Uncharted 3 entry, no `games/uncharted-3/` folder, no prior work found. Web search also found no co-op project for the campaign.
3. **Which engine?** Naughty Dog proprietary in-house engine. No source code, no decompilation, no scripting layer available. Closed binary only.
4. **How much source is there?** Nothing. Heavy reverse engineering required. Per the triage difficulty table: "Closed binary, no MP [in campaign], no scripting → Very hard."
5. **Does the engine have any multiplayer?** Yes — competitive multiplayer exists as a separate mode. Campaign has no netcode, no replication, no server.
6. **Shipping check?** Cannot ship changes without shipping game files (no source, no port). Must distribute as a patch/tool the player applies to their own dump. Stay away from online services per ground rule 10.

## Applicable route (console-emulators playbook)

**Route B: memory-sync co-op** — two RPCS3 instances running the same single-player game; a bridge reads each player's state from emulated RAM and writes remote players into spare actor slots or overlays. PS3 RAM-sync is marked untested territory in the playbook — no verified project exists.

## Workspace plan

- Dump your own PS3 disc (you own it; I will not help locate ISOs/ROMs per AGENTS.md ground rule 7).
- Run two RPCS3 instances with identical dumps/settings on your PC.
- Reverse-engineer player structs (position, health, animation, weapon) in the proprietary engine.
- Build a PINE-style or custom bridge between instances at 10–20 Hz with interpolation.
- Sync world flags/progress as events; enemies as host-authority or per-player copies.
- Gate cutscenes and loading so both clients wait.

## Next steps

1. Fork cranebeaker/coop-anything and branch `game/uncharted-3`.
2. Add `games/uncharted-3/NOTES.md` and `games/uncharted-3/README.md`.
3. Open a "claim a game" issue so others can find you (AGENTS.md).
4. Add a directory entry in `data/directory.yaml` with `kind: gap`.
5. Begin reverse engineering: RPCS3 debugger + Ghidra headless on the EBOOT.BIN.

## Claims & unknowns

- **unknown**: disc serial, update/build version, SHA-256 of EBOOT.BIN
- **unknown**: whether two RPCS3 instances can run simultaneously with separate PINE slots
- **unknown**: player struct offsets in U3's proprietary engine
- **unknown**: whether campaign data is deterministic enough for memory-sync
