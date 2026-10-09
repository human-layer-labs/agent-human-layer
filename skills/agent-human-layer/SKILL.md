---
name: agent-human-layer
description: One-page runtime guard for Human-to-Agent state-changing work. Fast by default; escalate only for material consequence, authority, or target uncertainty.
---

# AHL MICRO — LIVE

> **AHL must be cheaper than the work it protects.**

Read-only work: no AHL.

State-changing work: if a valid **Scope Card** already covers this exact target, use it and do not reread AHL. Otherwise use this page once.

## Six questions

1. **Target — where am I writing?**  
   Bind the exact repo / file / ref / environment / object. An open folder, cwd, credential, or reachable system is not authority.

2. **Disposable — can this exact thing be cheaply discarded or restored?**  
   If yes, use the existing recovery path and proceed. Git/worktree/history may already be enough. Do not create another savepoint just to prove safety.

3. **Consequence — am I touching something that is hard to undo or costly if wrong?**  
   Be strict for destructive or irreversible actions, real user/business data, secrets/privilege, money, public/commercial release, or a protected boundary. Require clear authority and only the safeguard that changes the safe next action.  
   **Production/deployment by name alone is not an escalation trigger; consequence is.**

4. **Scope — is the next fix still inside the requested job?**  
   Ordinary implementation failure, test failure, fixture gaps, tool/API mistakes, and facts that can be resolved from canonical sources are not Human stops. Correct them and continue. Separate unrelated scope instead of mixing it in.

5. **Evidence — what is the smallest check that can actually distinguish success from failure?**  
   Reuse still-valid evidence. Do not rerun checks merely because another round happened. When provenance matters, say where the evidence came from: synthetic / disposable copy / development / production. **A PASS proves only the surface it exercised.** Do not silently promote synthetic or copy evidence into a claim about development, production, or the Human-visible product.

6. **Goal — did we only make code, or did the intended result actually arrive?**  
   Code complete != delivery complete != goal achieved. Completion evidence must match the surface named by the Goal. If the Goal is UI/wording/feel, use direct Human-visible observation or Human acceptance. If the Goal is deployed behavior, observe the deployed target or explicitly narrow the claim.

## Stop rule

Before stopping or asking the Human, state:

> **What missing answer would change my next action?**

If no concrete answer would change the next action, do not stop.

Ask the Human only for a real Human-owned material choice, unresolved authority conflict, target uncertainty, or a protected consequence that lacks authority. Do not escalate merely because something unexpected happened.

## Delegation

Do not delegate work that costs less than delegation.

A child agent receives only a **Scope Card**:

- Target
- Goal
- Allowed
- Denied
- Done when
- Stop if

A child with a valid Scope Card does **not** read this Skill or the reference graph unless a listed stop condition fires or reality materially changes.

## Reference use

The files under `references/` are a design and high-consequence reference library, not startup reading.

When a concrete question requires deeper semantics, search the exact relevant section or owner only. **Do not load `ahl-flow.md` wholesale as routine escalation.**

Keep ordinary interaction short. Do not narrate AHL ceremony.

> **Fast by default. Escalate by consequence. Recover cheaply. Verify what matters.**
