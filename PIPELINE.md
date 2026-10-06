# Opportunity Pipeline

## Lifecycle

```text
NEW
 ↓
VALIDATING
 ↓
BUILD
 ↓
LAUNCH
 ↓
GROW
 ↓
MAINTAIN
 ↓
KILL (possible from any stage)
```

## Current state

### VALIDATING

1. **GST Exception Resolver** — obtain real CA data and validate time saved.
2. **Agent Permission Diff** — prove developers care about permission drift in CI/PRs.
3. **WhatsApp Stalled Deal Detector** — validate whether identifying stalled conversations is valuable enough to pay for.

### BUILD

None.

### LAUNCH

None.

### GROW / MAINTAIN

None.

### KILL

None yet.

## Promotion rules

### NEW → VALIDATING

Requires credible evidence and a concrete validation experiment.

### VALIDATING → BUILD

Prefer:

- multiple independent evidence sources;
- identifiable payer;
- painful recurring workflow;
- MVP achievable quickly;
- successful user validation;
- clear distribution path.

### BUILD → LAUNCH

Only when the smallest useful workflow works reliably.

### LAUNCH → GROW

Only when users return and at least some users demonstrate willingness to pay.

### ANY → KILL

Kill when evidence materially weakens, economics fail, platform risk becomes unacceptable, or validation repeatedly fails.

## Important

Do not confuse "technically possible" with "worth building."
