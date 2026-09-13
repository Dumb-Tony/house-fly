# House Fly — Playtest log

## 2026-09-13 · M1 rules/physics v1

- Agent-run engineering tests, not human feel testing. No fresh testers recruited and no subjective gates passed.
- PC: AMD Ryzen 9 9950X, Radeon RX 9070 XT (also integrated Radeon graphics), desktop 2560 × 1440. Browser/performance observations to be added after deployment inspection.
- Official Node 22.16.0 used after the bundled Node 24 runtime crashed with Windows access violation. Downloaded runtime and diagnostics are ignored and not published.
- `node tests/simulation.cjs`: 12/12 passing. Safe spawn, idle hiding zero score, capped/diminishing ear and sandwich rewards, pause/focus loss, cabinet occlusion, swept collision and burst vulnerability, non-homing strike, human-only one-time lamp award, staged bait/dodge/break/escape/restart, FPS equivalence, reset stress and ten simulated minutes.
- FPS replay: identical final x=700.8280834687641, y=535, score=0 after 2 simulated seconds at 30/60/120 presentation FPS. This is deterministic harness evidence, not measured real presentation performance.
- Bait route sets initial anger/location, then uses simulated directional input and burst; exit is positioned by the harness. It verifies causal mechanics but does not prove a complete human-played traversal. Five 120-second idle encounters test ten minutes of simulation; this is not ten wall-clock minutes of manual play. 100 rapid resets tested.
- Initial route failed: tracking through windup made sideways baiting unreliable. Tuning round 1 freezes aim for final 0.30s of the 0.70s windup, labels that window, and retains 0.15s active hit/1s recovery. Regression route now survives, breaks the lamp once and escapes. See IMPLEMENTATION_M1.md for all values and spec adjustment.
- Storage-unavailable path tested with getItem/setItem throwing. Runtime remains functional and records in memory.
- Decision: **iterate through fresh-player validation**, no M2. Pending: five fresh players, 4/5 irritate and escape by attempt three, 3/5 intentional lamp baits with causal explanation, 3/5 voluntary retry, and 80% understood hits. No claims of these outcomes.
- Browser file URL is blocked by the in-app browser URL policy; offline real-browser verification is not claimed. Standalone source has no fetch, external fonts, scripts or media. Public browser checks follow separately.
