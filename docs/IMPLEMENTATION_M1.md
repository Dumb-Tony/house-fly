# M1 implementation · rules v2 (second pass)

One offline HTML at `prototypes/m1/index.html`. No dependencies or asset requests. GitHub Pages publishes this folder only. Run the regression harness from the project root with `node tests/simulation.cjs` (Node 22 or newer).

## Tuning decisions

- Room 1100 × 680; velocity approaches directional target at exponential rate 18/s and brakes at 24/s; nominal speed cap 330; diagonal input normalized. Burst speed 720 for 0.16s; cooldown 1.4s, no invulnerability. Landed speed cap 55.
- Three tiers: relaxed below 20 anger (155 reach), annoyed below 40 (205), furious 40+ (255). Ear anger 24/s, sandwich +35. Only furious swats break the lamp. Lamp awards 400 once. No direct fly destruction.
- Tracking 0.4s, windup 0.7s, strike 0.15s, recovery 1s. **Deliberate fairness adjustment:** aim follows perception for the first 0.4s of windup, then freezes for its final 0.3s. Strike snapshots that displayed aim at windup end. This changes the original proposed live-position sample at the last instant, which made sideways baiting unreliable in the initial scripted route. The frozen sector becomes solid and says BURST NOW. The strike never homes.
- Sector half-angle 0.32 radians; swept fly collision samples its entire per-step segment at <=2-unit spacing, with a 7-unit fly radius. Cabinet blocks flight, perception and hit checks. Table is a low flyable surface. Decorative human/rug are traversable; no altitude layer implied.
- Ear scoring caps at three seconds per visit: 30, 15, then 0. A visit resets after 0.7s away. Sandwich requires E and a 0.6s exposed dwell: 100, 50, then 0. Anger still rises after score depletion. No meaningful encounter reset until a new run.
- A survived swat awards 150 only if the fly was inside its displayed danger sector during the locked windup. Mere proximity no longer awards a dodge. Exit unlocks at the first provoked strike; hold 0.75s, +25% on escape. Two-minute hard encounter clock prevents indefinite farming. Timeout and defeat retain banked events.
- 1/120s fixed simulation, maximum eight catch-up steps; excess backlog discarded. Focus loss pauses and clears held keys. Pausing freezes the current attack; resuming explicitly continues it. R creates fresh state.
- Separate v2 records prevent comparison with old scoring/physics. Versioned, try/catch localStorage stores only settings and best total; storage denial is tested. Audio defaults off, uses quiet generated event tones. Flight sensitivity, visible patterned telegraph and F3 developer overlay included. Full remapping and other broad GDD accessibility proposals remain outside this M1 implementation.

## Scope and next gate

M1 implementation is complete; the human comprehension/enjoyment gate is **not passed**. No M2 work authorized by automated success. Next experiment is five fresh players, up to five attempts each, following `PROTOTYPE_M1.md`. Capture intentional lamp baiting, explained hits and voluntary retries. Default sound is intentionally sparse; no voice recording, third-party artwork or production systems.

## Second-pass presentation and teaching

Responds to the user's report that movement, reactions, baiting and excitement all needed improvement. Remains one room/human/lamp, with no added milestone content.

- Cabinet collision resolves axes separately so diagonal motion slides along it. Landing within the valid perch radius gently snaps to the sandwich. Fly silhouette is larger, oriented to movement, with a short trail and nearby burst recharge ring.
- Human head turns toward visible fly; brows, shirt color, speech bubbles, windup arm and extended striking hand show attention and escalation. Speech is caption text, no voice assets.
- Sandwich dwell and ear visits show progress. Score callouts, a crash ring and a human reaction connect actions with outcomes. Effects are bounded (9 trail samples, 12 callouts) and non-colliding; no camera shake.
- HUD gives the current objective: irritate, bait lamp, escape. At furious tier, a bait position appears on the human–lamp line. A lined-up cue reflects the actual attack sector.
- Optional “Watch a lamp bait” plays a recorded normal-spawn input route through the same simulation at 65% presentation speed. It uses normal sensitivity regardless of the player's setting, is labeled DEMO, can be interrupted with R, and never writes a score. The source route regression can regenerate its input data with `node tests/simulation.cjs --record-demo` (create ignored `test-results` directory first). Demo input is embedded; no separate asset is needed offline.
- The normal-spawn lamp route initially failed when returning during the first active swat. Waiting through that swat before returning succeeded; attack fairness was not weakened to force the replay to pass.
