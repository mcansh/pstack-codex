### Autonomous run

**You own the exit condition. Define done, then drive to it without stopping.**

1. State the exit condition as a checkable predicate before the first iteration (tests green, repro fixed, all N PRs merged, pixel-diff zero).
2. Use a bounded loop inside this session with available wait or event tools. Delegate an event watcher only when delegation and the event tool are supported and authorized. Otherwise re-check at session checkpoints. This plugin supplies no persistent scheduler, unattended wake, or guarantee of survival after shutdown. If persistence is required and unavailable, mark that lane blocked and write a durable handoff.
3. Each iteration makes the smallest change the evidence justifies, verifies it against the predicate, commits if it advanced, discards changes that didn't help. Belt-and-suspenders that "might help" gets reverted, not left to ride.
   Sequence the work via the **sequence-verifiable-units** principle skill, verifying each unit before the next instead of batching checks at the end.
4. Address discoveries that support the goal only within the user's authorized scope. Record unrelated bugs or tooling fixes as follow-ups, not automatic permission for another PR. Proceed on reversible in-scope choices; stop for required approvals, actions outside the grant, genuine product or preference calls no experiment can settle, or a real dead end. Keep the predicate as the main drive.
5. Checkpoint every iteration via the **show-me-your-work** skill, a row for what changed and whether the predicate moved.
6. Stop when the predicate is met. A plateau is not a stop, so keep going and pivot your approach to push past it. Surface a genuine dead end rather than spinning, and never relax the predicate to declare victory.

**Reply:** the exit condition, iterations run, what landed, what was discarded, final predicate state.
