### Feature

**You own the design. Plan, review, verify.** Delegate implementation. Stay in the lead.

1. Trace the affected subsystem.
2. `architect` for the shape.
3. Write the throughput checkpoint as four todo items. A dimension that genuinely does not apply (single file, no fan-out) keeps its item with `n/a: <reason>` rather than being dropped:
   - **Blocking first steps.** Gates run before fan-out.
   - **Independent workstreams.** Disjoint files, services, or layers parallelize. Shared writes serialize.
   - **Shared mutable state.** Default to splitting the target (the **separate-before-serializing-shared-state** principle skill). Serialize only for real invariants.
   - **Smallest safe decomposition.** If one worker is best, name why.
4. Delegate code-writing using your configured feature role (default `inherit-parent`) with a specific scope: file paths, the data shape and organizing structure per **principle-model-the-domain**, and success criteria. Use only supported spawn arguments and explicitly isolate writers. When several valid shapes remain, use **arena** to surface alternatives. If delegation is prohibited or unavailable, own the diff directly, disclose reduced independence, and leave independent-verification gates blocked. Do not wait on an unsupported nested agent. Make surgical edits and re-ground upstream-derived files against their source. Port shared improvements to authorized consumers and verify each; report out-of-scope consumers as follow-ups. Commit only when authorized.
5. Verify on the matching surface. "Inconclusive" or wrong-surface is not a pass. Flag it.
6. Rebase into small, ordered commits. Stack follow-ups.
   Use the **sequence-verifiable-units** principle skill, building, verifying, and committing each small unit before the next.
7. If the design is contested, `interrogate` before shipping.
8. Run **Opening a PR**.

Code-coupled work (one feature, one migration) goes to a single owner with the checkpoint inline. That owner fans out internally after the blocking phase. Parent-level fan-out is for slices that produce independent artifacts (audits, cross-subsystem investigations, competing experiments). Rewrite the checkpoint at phase boundaries. Spawn a fresh owner rather than chaining interrupts.

**Reply:** what you built, what you chose and why, the throughput checkpoint, open decisions. Tables for design alternatives.
