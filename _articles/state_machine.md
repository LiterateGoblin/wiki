---
title: State Machine
---
A model of a discrete system. This model is simpler than a program because it unifies different implementations of state into one representation.

## Properties

- A state machine is first described by a set of initial states. Each state describes which other state can follow it.
- A state machine halts when it is in a state where there is no possible path to another state - no state follows this state.

## Description of a State Machine Using the Assignment Definition of State

If state is defined as the assignment of a value to a variable, a state machine can be described with three items:

- The set of all variables in the system.
- The initial values of each variable in the system.
- The relationship between the values of the system variables in the current state and the values of the variables in any given future state.

## Definitions

- **state** - (an) assignment(s) of (a) value(s) to (a) variable(s).

## Examples

```
// C code
// define someNumber() to return an arbitrarily chosen number from 0 to 1000. it can return different numbers in different executions.

int i;
void main() {
  i = someNumber();
  i = i + 1;
}

// Attempted state machine:

Set of all variables = i

Initial values of all variables:
- i = 0

// Possible execution 1:
[ i : 0 ] // initial state. only possible initial state in C; C initializes i to 0.

[ i : 0 ] -> [ i : 42 ] // someNumber() returns 42

[ i : 0 ] -> [ i : 42 ] -> [ i : 43 ]

// Possible execution 2:
[ i : 0 ]

[ i : 0 ] -> [ i : 43 ]

[ i : 0 ] -> [ i : 43 ] -> [ i : 44 ]
```

When `i = 43` there are two next potential states that could follow: one where there is no next value for `i` and one where the next value of `i` is 44. There is currently no way to relate the state `i = 43` to its next state because the same state has two different next potential states - there is some unrepresented state missing.

```
int i;
void main() {
  i = someNumber(); // pc = "start"
  i = i + 1;        // pc = "middle"
}                   // pc = "done"

// Attempted state machine

- Set of all variables: i, pc

- Initial state of all variables:
i = 0
pc = "start"
```

![](.attachments.22861/mermaid-diagram-2023-08-17-225044.svg)
