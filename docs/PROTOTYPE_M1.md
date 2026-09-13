# Milestone 1 — Standalone HTML vertical prototype

**Status: implemented 2026-09-13; fresh-player gates pending.** See IMPLEMENTATION_M1.md for actual timing and the justified final-windup aim-lock adjustment. The sole purpose of this milestone is proving the core mechanic/verb before expanding content. Follow the offline, fixed-step, restart, storage, and measurement contract in GDD.md. All thresholds are initial acceptance targets to validate, not completed test results.

## Question and hypothesis
Can a player intentionally annoy a human, dodge their response, and cause a funny object-breaking mistake? Flight and causal readability must both pass.

## Exact playable slice
One top-down living room; human near a table and lamp; fly, ear zone, sandwich perch, lamp and exit. A two-minute session limit compresses the eventual longer encounter. Three anger tiers change tracking and swat reach without adding tools. Buzz, land, provoke, burst away; a swat can break the lamp. Exit unlocks after one provoked swat. Touching the open exit for 0.75 seconds finishes; a strike defeats the fly.

## Implementation specification
Fly has acceleration, velocity cap and drag; burst has a two-second cooldown and grants speed rather than invulnerability. Start with 0.7-second swat anticipation, 0.15-second active hit and one-second recovery. Snapshot attack target when windup ends. A visible sector previews reach; collision uses swept motion during the active window. Human target tracking honors room obstacles. Lamp destruction awards once and only from the human strike. Expose anger, state, perception and attack target in a toggleable debug view.

## Deliberate exclusions
No tool retrieval, spray, furniture pathfinding, pets, flight traits, 3D ceiling movement or complex destruction. One lamp breaking is enough to demonstrate the joke.

## Test procedure and exit gate
Five fresh players get up to five attempts. Four must understand how to irritate and escape by attempt three. Three must intentionally bait the lamp break and explain that the human caused it. At least three ask to retry. Record whether each hit was understood; at least 80% of observed hits should be explainable from the telegraph, without relying on debug overlays.

Check zero score from idle hiding, one award per prop, target diminishing returns, no strike after pause, no attack through blockers and no unavoidable spawn hit. Test rapid restarts and ten minutes of repeated encounters.

## Decision rule and deliverables
Deliver one offline HTML, recorded attack timings and playtest notes. If players dodge but do not understand baiting, change staging and causal effects before adding attacks. If flight is unpleasant, pause AI work and tune movement in the same room. Escalation passes only if it creates intentional risk, not merely faster death.


