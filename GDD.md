# House Fly — Game Design Document

## Elevator pitch
Be an infuriating fly in a room with one increasingly furious human. Buzz ears, touch food and bait swats until the person wrecks their own surroundings. Escape with a score or push too far and get flattened. Target full runs: 3–8 minutes, bounded by escalating danger.

## Design pillars
- Flying is nimble, expressive and immediately enjoyable.
- Irritation creates danger and comedy through understandable reactions.
- The human causes the biggest mess; the fly creates the opportunity.
- Risk beats passive survival and repetitive farming.

## Player fantasy
Outmaneuver a giant who takes a tiny nuisance personally. A last-second dodge should let the player watch an angry swat smash the lamp behind them and recognize their own setup.

## Core gameplay loop
Enter → read human attention and tempting targets → perform an invasive action → provoke retaliation → dodge and bait collateral damage → decide whether to attempt another scoring interaction or escape → see breakdown → retry. Death still records banked achievements; a deliberate escape earns a finish bonus.

## Controls
M1 top-down keyboard: WASD/arrows accelerate in the room plane, Space burst, E land/take off at a highlighted perch, R restart, Escape pause. Landed movement uses the same direction keys. Proposed gamepad: left stick flight, face buttons burst and perch. Flight uses fast acceleration and strong direction changes while preserving a short readable drift. A later altitude layer is conditional; do not assume full six-axis flight or mouse aiming.

## Moment-to-moment mechanics
Approach an ear zone, hover long enough to irritate, spot the windup and burst across the human’s reach. Landing on a sandwich commits to a brief exposed state but earns more than nearby buzzing. Swatting targets the fly's sampled position at commitment; it cannot home throughout the strike. Dive momentum and wall/ceiling traversal are later movement experiments. The fly can tip only small precarious items; it cannot directly demolish heavy furniture.

## Physics and human AI
Use a finite-state controller for activity, noticing, tracking, windup, strike, recovery and tool retrieval. An anger tier selects available attacks and cadence, while each attack still follows its readable sequence. Proposed tiers: relaxed 0–19, annoyed 20–39, angry 40–64, furious 65–84, unhinged 85–100. Thresholds are tuning hypotheses.

Human perception uses range and line-of-sight plus audible buzzing; last-known position persists briefly. Do not grant omniscience when the fly hides. Anger increases through interactions and cools slowly only outside an active attack; a separate encounter pressure clock prevents permanent safe farming. Each escalation has a visible transition. M1 tests lazy swat, active tracking and a stronger object-breaking swat. Later tiers add swatter, bounded spray zones and thrown props. Schedule only one lethal attack at a time initially.

Props use simple bodies and authored break responses. Credit collateral damage only when caused by a provoked attack within a short attribution window. Cap simultaneous debris; decorative shards do not damage the fly.

## Scoring
Proposed banked events: ear buzz 10/second for at most three seconds per visit, food landing 100, face landing 200, close swat dodge 150, human-broken prop 100–500 by category. Same target awards full value once, half on second visit and zero thereafter until a meaningful encounter reset. No survival points for hiding. Escape bonus adds 25% to banked score; death removes only that prospective bonus. Property-damage figures are comic abstractions, not an economy. Score screen separates irritation, dodges, collateral and escape.

## Level and environment design
One room is an arena with a loop around the human, exposed valuable perches, protected recovery pockets and destructibles behind bait positions. A clear exit opens after the initial irritation objective. Escape requires a short exposed hold, making cash-out a decision. Conditional release: kitchen, living room and office, each with one distinct human behavior profile. Source ideas such as wedding reception, restaurants and a cat owner stay in the backlog.

## Progression and unlocks
Unlock rooms with achievable encounter goals, not hours of survival. Traits are later sidegrades: fast/loud, small/low impact, heavier/slower. Cosmetic fly colors cannot compromise contrast. Player flight and knowledge of reactions supply the main improvement; no health or evasion upgrades that trivialize attacks.

## Replayability
Different bait positions, route sequences, local score medals and personality timing produce repeated decisions. Hold authored human rules stable within each scenario. Seeded activity variations can arrive later, but random unavoidable attacks cannot create variety. Challenge goals encourage intact-room escapes or specific collateral chains.

## Art direction
Exaggerated household scale, chunky human hands, readable fly outline/shadow, and an increasingly disheveled room. The human’s posture communicates mood before UI does. Use playful slapstick and non-graphic fly defeat. Camera favors awareness over cinematic closeups.

## Animation and VFX
Anticipation is gameplay: human gaze, shoulder windup, strike trail and recovery are distinct. Fly wing animation is decorative and must not hide its collision marker. Anger transitions use posture and short effects. Broken objects produce brief coarse fragments; spray zones have patterned boundaries and fade cues.

## Audio
Wing pitch reacts to burst and proximity; a comfortable reduced-buzz mix is essential. Human mutters and tool sounds signal tiers without required spoken comprehension. A sharp swat cue accompanies visual windup. Impacts sell escalating absurdity. Captions or icons convey offscreen threats.

## UI/UX
Show score, anger tier, burst readiness and exit status around a clear playfield. Highlight one nearby landing target, displaying its action and diminished value. Announce new attack types with concise cues. Death/result UI explains the strike that hit and offers immediate retry. Do not interrupt active flight with modal tutorials.

## Accessibility and options
Remap inputs; adjustable flight sensitivity, hold/toggle landing, reduced wing audio, reduced motion, high-contrast fly, patterned danger areas, captions and larger telegraphs. Optional practice mode slows attack cadence and records separately. No camera shake needed to understand impacts. Pause freezes AI and pressure clock.

## Technical approach
M1 is a top-down Canvas room with simple circle/box collision, explicit attack timelines and debug perception overlays. It proves flight, provocation and causal collateral; it does not prove 3D wall or ceiling traversal. M2 must separately decide whether depth adds enough to justify occlusion and controls. Store AI and interaction definitions as data; keep score attribution separate from visual break effects.

## Risks and mitigations
Flight may feel disconnected: tune acceleration, stopping distance and silhouette before adding targets. Anger may feel like punishment for playing: stronger attacks also expose greater scoring opportunities. AI may seem unfair: show commitment and prevent post-commit tracking. Comedy may be obscure: stage a destructible behind a safe dodge direction. Repetition may dominate: diminishing target values and a bounded encounter force movement.

## Scope boundaries
M1 has one fly, human, room and three interactions; no insecticide, pets, traits or full 3D locomotion. Conditional release caps at three rooms and three behavior profiles sharing a robust controller. No crowd simulation, life simulator, campaign narrative, multiplayer or general-purpose destructible house.

## Milestone roadmap
1. **Standalone HTML vertical prototype:** prove satisfying flight and the provoke–dodge–collateral loop in one room.
2. **Fairness and camera:** validate human attack readability, escape timing and any proposed altitude layer; add one new attack only after the original is fair.
3. **Small game:** three rooms/profiles, goals, local scores and limited sidegrades. Each profile must alter tactics rather than only attack speed.
4. **Polish:** feedback, audio comfort, accessibility, AI edge cases and bounded debris performance.
5. **Later possibilities:** cat encounters, larger social spaces or multiplayer only after a separate scope decision.

## Development policy and evidence

Design basis v0.1 (2026-09-12), with M1 authorized and implemented 2026-09-13. See docs/IMPLEMENTATION_M1.md for actual tuning. It is not a production commitment. The source is a private concept-development conversation, preserved locally in excluded source-basis notes. The user's current brief takes precedence over older multiplayer brainstorming. Mechanical formulas, key bindings, content budgets, and test thresholds below are proposed hypotheses, not previously approved requirements or measured results.

Single-player first. No accounts, servers, matchmaking, replication, rollback, network authority, or multiplayer-driven entity architecture. A later multiplayer proposal requires its own feasibility and scope decision. Ordinary modular separation of input, simulation, presentation, and save data is sufficient now.

Milestone 1 is a standalone HTML vertical prototype whose sole purpose is proving the core mechanic/verb before expanding content. “Vertical” means a complete tiny start–play–result–restart loop, not production polish. An M1 prototype is now included; this is not a full production build.

## Shared implementation and validation contract

Deliver the future M1 as one index.html with embedded CSS, JavaScript, geometry, and generated sound. It must open from file:// offline with no installation, build command, CDN, remote fonts, fetch, or external asset requirement. Use Canvas 2D for initial rendering, including projected geometry where specified. No engine decision for the full game is implied.

Use requestAnimationFrame for presentation and a fixed 1/120-second simulation accumulator, capped at eight catch-up steps. Discard excessive backlog after suspending a tab; pause on lost focus and clear held input. Tune to a stable 60 rendered frames/second on the actual test PC, whose CPU, GPU, browser, and resolution must be recorded. Compare repeated scripted input at 30, 60, and 120 rendered FPS; traversal/score differences above 2% need investigation. This is local repeatability, not a promise of cross-browser bitwise determinism.

Persist only settings and appropriate local records through a versioned localStorage adapter wrapped in try/catch. The game must remain playable in memory when storage is unavailable, especially under file://. Provide an explicit local reset action. Later ghost recordings must carry course, rules, and physics version identifiers. Never silently compare incompatible records.

Developer-only overlays report frame cost, simulation time, relevant physical variables, and reset state. M1 tests cover the normal loop, boundary cases, focus loss, rapid restart, and prolonged use. Do not invest in a general framework before a mechanic passes.

## Milestone governance

Milestones are exit gates, not promised calendar dates. At each gate, record observations, parameter changes, unresolved issues, and a proceed / iterate / park decision in docs/PLAYTEST_LOG.md. Recruit five fresh players where possible; an internal solo test can identify problems but cannot count as the fresh-player comprehension gate. Small samples are directional evidence.

M1 includes only the bespoke prototype specification in docs/PROTOTYPE_M1.md. Do not begin M2 merely because M1 runs without crashing. If the mechanic misses its enjoyment or readability gate, run up to two focused tuning rounds before deciding whether to revise the premise or park it. Adding levels, upgrades, story, or polished assets is not the remedy for an unproven verb.


