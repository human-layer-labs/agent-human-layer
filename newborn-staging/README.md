# Newborn staging

This tree is temporary non-live newborn implementation staging.

`AHL-CANONICAL-TARGET.md` is the architecture authority.

Nothing under `newborn-staging` is loaded by live AHL. Staged files must not become live individually. Activation requires a coherent atomic cutover. The staging tree is removed after successful cutover.
