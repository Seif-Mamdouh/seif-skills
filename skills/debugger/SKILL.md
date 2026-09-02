---
name: debugger
description: Debug investigation workflow for hypothesis-driven debugging with read-only investigation scripts.
disable-model-invocation: true
---

# Debug Investigation

Systematically reduce uncertainty through hypothesis-driven investigation using read-only database scripts.

## Workflow

### 1. Read Code First

Before any scripts: understand the relevant code paths, data flow (API -> controller -> service -> DB), key entities/relationships, and assumptions the code makes.

### 2. Generate Hypotheses

Generate at least three hypotheses before writing investigation scripts.

```text
H1: Appointments have wrong status -> would show in DB but filtered out
H2: Customer FK is broken -> joins return empty
H3: Timezone issue -> "upcoming" filter excludes valid appointments
H4: Sync never happened -> data missing entirely
```

For each hypothesis, state what it would explain and what it would not explain.

### 3. Design Discriminating Tests

The best scripts either confirm one hypothesis or eliminate one hypothesis. Ask: "What data distinguishes H1 from H2?"

Maximize information per script:

- Binary search over possibilities.
- Compare working and broken cases side-by-side.
- Check common cases before edge cases.

### 4. Execute, Update, Repeat

After each script, update confidence.

```text
After Script 2:
- H1: ELIMINATED - statuses are correct
- H2: UNLIKELY (20%) - FK exists
- H3: LIKELY (60%) - UTC vs local mismatch
- H4: POSSIBLE (20%) - unchecked
Next: compare timestamps in both timezones
```

## Script Template

Location: `scripts/check/debug-<name>.ts`

```typescript
#!/usr/bin/env bun
/**
 * Testing: H3 (timezone issue)
 * If true: scheduledAt in UTC will be "past" when compared as local time
 * If false: times will match expectations
 */
import { dbClient_readReplica } from "@/prisma/client";

async function main() {
  // investigation logic
}

main()
  .catch(console.error)
  .finally(() => dbClient_readReplica.$disconnect());
```

Run: `bun scripts/check/debug-<name>.ts`

## Constraints

Allowed:

- `dbClient_readReplica` queries: `findMany`, `findFirst`, `count`, `aggregate`.
- Read-only services.
- Environment variables.

Forbidden:

- `dbClient`.
- Mutations: `create`, `update`, `delete`, `upsert`.
- Write services.
- Scripts without hypotheses.

## Cleanup

When done:

1. State conclusion and confidence level.
2. Summarize evidence and eliminated hypotheses.
3. Delete all `scripts/check/debug-*.ts` files created this session.

## Fixing Bugs
If prompted to fix a bug, wherever possible, fix the root cause. Wherever possible, fix by simplifying (removing loc) vs additive patching.