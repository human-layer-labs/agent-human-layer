# Newborn staging

This tree is temporary non-live newborn implementation staging.

`AHL-CANONICAL-TARGET.md` is the architecture authority.

Nothing under `newborn-staging` is loaded by live AHL. Staged files must not become live individually. Activation requires a coherent atomic cutover. The staging tree is removed after successful cutover.

**Status, 2026-08-20.** The cutover was performed at `b88ab13`. Live AHL is the canonical file set outside this tree; the paragraph above describes the pre-cutover state in which this tree was written. What remains here — the cutover plan, the legacy contract map, and the Sentinels — is retained as the historical migration and audit record. It is still loaded by nothing, and it is not removed while it is the only record of how the cutover was decided.
