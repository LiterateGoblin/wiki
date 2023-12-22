---
title: Action Formula
---

An action formula is a formula that represents how the state of a state machine will change when taking a certain action, and what conditions must be met before that action can be taken.

## Definitions

- **enabling conditions** - conditions on the first state of a step - conditions that must be true for that action to be legally taken. In TLA+, this can be thought of as "conditions with no primes". These go first in idiomatic TLA+.

## Examples

```
TMRcvPrepared(r) ==
  /\ tmState = "init"                         /* these are
  /\ [type |-> "Prepared", rm |-> r] \in msgs /* enabling conditions.
  /\ tmPrepared' = tmPrepared \cup {r}
  /\ UNCHANGED <<rmState, tmState, msgs>>
```
