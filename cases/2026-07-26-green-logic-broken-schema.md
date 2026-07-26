# 2026-07-26 — The suite was green; the schema was broken

## Context

A payroll plugin was moving its wage-condition templates onto a new axis.
The change added two database tables and dropped three old ones — a schema migration,
one of the few operations a folder snapshot alone cannot undo.

The work had already survived several rounds of verification. The test suite was green.
An independent reviewer had run mutation checks on the resolution logic, the version engine,
and the read/write paths, and every planted break was caught. It looked ready.

## What happened

The build was deployed to the test environment. The migration ran and reported success.
Then the reviewer checked the actual database — not the report — and found the migration
half-done:

* the three old tables were correctly dropped
* one of the two new tables was created
* **the other new table was silently absent**

The site returned 200. No fatal error. The migration had said "done."

## What caught it

Checking the real database after the migration, instead of trusting the "success" message.

The missing table's `CREATE` statement had two columns with the same name. The framework's
schema helper, given a duplicate column, does not raise — the real database rejects the
statement, and the helper swallows the rejection and moves on. The table simply never exists.
Its twin table had no such collision, so it was created, which is why the failure looked
partial and quiet rather than total and loud.

## Why the green suite could not see it

Every test ran against an in-memory stand-in for the database. That stand-in accepts a
`CREATE` the way a filing cabinet accepts paper — it never parses the SQL, never enforces
uniqueness, never rejects anything. So the duplicate column was invisible to every test.

The logic was verified. The schema was never executed. Those are different layers, and a
green result in one says nothing about the other. A stand-in that answers through a different
path than production will agree with you right up until production disagrees.

## What made recovery cheap

The deploy took a file snapshot and a database dump before touching anything. Restoring the
environment to its previous known-good version — both code and schema — was two commands and
under a minute. The broken migration cost a redeploy, not a recovery scramble.

The rollback path existed before it was needed. That is the only time it can.

## What changed

1. **A static schema guard.** A test now reads the generated `CREATE` statements and fails on
   any duplicate column name — across every table, in pairs. This catches this entire class of
   defect without a real database, cheaply, on every run.
2. **The real-database gate is now explicit.** Schema changes are not considered done when the
   suite is green. They are considered done when the migration has run against a real database
   and the expected tables and columns are confirmed to exist. Logic green is not schema green.

## For other teams

* A green suite means the design agrees with itself. It does not mean the schema is valid.
  If your tests use an in-memory database stand-in, your `CREATE` statements may never have
  been executed by anything that enforces the rules a real database enforces.
* After a migration, verify the real tables and columns exist. Never accept the migration's
  own "success" as proof — a framework that swallows errors will report success over a table
  it failed to create.
* You can still catch most of this cheaply: parse your generated DDL for structural mistakes
  (duplicate columns, missing keys) in a plain unit test. Keep the real-database run as the
  final gate, not the first alarm.
* Keep a pre-migration database dump beside the file snapshot. Code rolls back by folder;
  schema and data only roll back if you took the dump first.

Related: [Cheap Enough to Die](../CHEAP-DEATH.md) — the floor's job moved up from *restoring
broken code* to *discarding a wrong build cheaply*. This is that, one layer down: the dump
made a bad migration cheap to abandon.
