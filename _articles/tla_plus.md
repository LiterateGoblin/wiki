---
title: TLA+
---
A language and modeling specification for software above the code level. It can be used to show that a system does what we intend it to do, especially complicated systems. It stands for the "Temporal Logic of Actions".

## Motivation

Programmers rarely start with a precise model of what they intend to do, and instead proceed with a volatile mental model. They may become bogged down in coding details such as what type to use for a variable rather than worry about the program itself. This leads to design errors.

## Paradigm

TLA+ models the trait that is unique about software - that fact that it proceeds in discrete steps rather than a continuous process. TLA+ is a state machine.

The relationship between these states is determined by next-state actions. Next-state actions list what *may* happen to reach another state, not what *must* happen to reach another state. To specify what *must* happen, one needs to write down a condition called a fairness property. A fairness property can be expressed as a conjunction to a typical temporal formula that includes the initial condition and the next-state relation.

TLA+ was designed to model distributed and concurrent systems. Simultaneous processes typically do not use the word sequence to represent what is occurring, but it can be done and well with TLA+.

TLA+ can only verify properties of a system that are conditions of an individual execution of that system. For example, TLA+ can be used to verify the system property that "the system does not ever produce an incorrect answer". It cannot be used to verify that "99% of executions are correct answers" because this condition cannot be applied to a single execution. ("The system does not ever produce an incorrect answer" asserts the condition "The execution is correct" on each execution.)

TLA+ is **not** an imperative programming language. TLA+ source is a mathematical formula - so each branch of a branching condition defines that the formula evaluates to, not what the computer will do next.

All values in TLA+ are a set by default.

It is more useful to approach a TLA+ specification as a description of a universe where the system **and its environment** are behaving correctly than it is to approach a specification as a description of the correct behavior of the system.

## Operators

- `/\` - conjunction operator, known to engineers as a logical AND
- `\in` - "member-of-set" operator
- `\/` - injunction operator, known to engineers as a logical OR
- `\subseteq` - subset-of operator,  checks that all elements in the left-hand set are elements in the right-hand set
- `\union` - union operator, result is a set with all elements from both operand sets
- `\intersection` - intersection operator, result is a set with each element that appears in both operand sets
- `\` - set difference operator, result is a set that contains all values from the left-hand operand that are NOT in the right-hand operand
- `[x \in S |-> e]` - an expression whose result is a function with domain S that returns e when given an element x. Functions with domains that are discrete and bounded can be thought of like an array in traditional programming languages.
- `[S -> T]` - the set of all functions such that an element in set S is an element in set T
- `[f EXCEPT ![e1] = e2]` - returns a function with the same domain as f. Its only difference from f is that when the result function is applied to e1, it returns e2 rather than f\[e1\].
- `[h1 |-> e1, ...]` - a record where field record\[h1\] evaluates to e1. Records can be thought of like structs in C and Go, like objects in JavaScript. dictionaries in Python, maps in Java, Kotlin, and Rust.
- `[ ]` - an operator that, when applied to an action, evaluates to True if and only if that action is True on every step of a behavior. Read "always". This is a unary operator where the action is written on the right-hand side.
- ` < > `  - an operator that, when applied to an formula, evaluates to True if at some point during a behavior some state satisfies that formula. Read "eventually". This is a unary operator where the formula is written on the right-hand side and surrounded in parentheses.
- `[e]_< s1, s2, ..., si >` - a construct that evaluates to `e \/ (UNCHANGED s1 /\ UNCHANGED s2 ... /\ UNCHANGED si)` . Most often observed when defining a specification in terms of a temporal formula - often the next-state relation portion will designate which variables are allowed to remain unchanged during a step (stuttering step).
- `<< e1, e2, e2 >>` - a finite sequence or tuple construct
- `Tail(<< >>)` - returns a sequence without its first element
- `Head(<< >>)` - returns the first element of a sequence
- `\o` - concatenation operator. Evaluates to a sequence with all of the elements of the second sequence after the elements of the first sequence
- `Append(<< >>, e)` - evaluates to the input sequence with `e` as a new element after the last one. `<< >> \o << e >> `
- `Len(<< >>)` - evaluates to the sequences length
- `\X` - the Cartesian product of two sets. Evaluates to the set of all finite sequences with length 2 where the first element is from the first set and the second element is from the second set.
- `~>` - evaluates to True if, when the formula on the left evaluates to True, the formula on the right evaluates to True for the current state or some future state. Read "leads to". Typically used for liveness properties.
- `WF_vars(A)` - evaluates to True iff the action A has weak fairness.

## Definitions

- **step** - a change from one state to another
- **behavior** - a sequence of state changes
- **execution** - a sequence of state changes; synonym of behavior
- **specification** - a TLA+ model of hardware or software
- **state machine** - a model where the first state satisfies some initial condition and each successive state is related by some action
- **finite state machine** - a state machine that uses a finite number of states
- **next-state action** - the conditions that may be fulfilled when moving from one state to the next
- **fairness property** - the condition(s) that must be fulfilled when moving from one state to the next
- **invariance property** - a property of a state machine that asserts that something is true for every state in every behavior
- **liveness** **property** - a property that asserts that something eventually happens given enough time
- **module-closed expression** - a TLA+ expression that, after expanding all definitions, contains only:
  - built-in TLA+ constructs and operators
  - numbers and strings
  - declared constants and variables
  - declared local identifiers.
- **module-closed formula** - a Boolean-valued module-closed expression. In other words, a module-closed expression that evaluates to a Boolean value (true or false).
- **constant expressions** - a module-complete expression that has NO declared variables and has NO non-constant operators. Assumptions must be constant formulas. A constant expression will have the same value no matter the current state.
- **state expressions** - can contain anything that a constant expression can as well as variables declared in a `VARIABLES` statement. A state expression may have a different value depending on the current state.
- **action expressions** - can contain anything that a state expression can, as well as the `'` (prime) operator and the `UNCHANGED` operator.
- **action** - an action formula
- **temporal formula** - a formula that evaluates to a Boolean value on a sequence of states (a behavior)
- **stuttering step** - a step that leaves all variables unchanged
- **deadlock** / **termination** - a behavior that has reached a state that it cannot leave. In a system not designed for this outcome, this is known as deadlock. In a system designed for this, it is called termination. Deadlock and termination can be represented as an infinite number of stuttering steps (other variables in the environment can change, but the ones in the system (ones declared by the specification) cannot).
- **safety formula** \- a temporal formula that asserts what *may* happen. If a state or step violates the safety formula, nothing in the specification after that point can cause the formula to be true once again.
- **liveness formula** - a temporal formula that asserts what *must* happen. A behavior can "recover" from a liveness formula violation later.
- **enabled** - an action A is enabled on a state s if and only if there is some state t such that A is true when moving from state s to t. This often said as "s -> t is in A step".
- **enabling condition** - a condition that must be true for action to be enabled. This condition will have no primes in it.
- **weak fairness** - asserts that if an action A is continuously enabled, then eventually an A step must occur. Weak fairness is a liveness property.
- **strong fairness** - asserts that if an action A is ever *repeatedly* enabled, then eventually an A step must occur. The states which A is enabled need not be adjacent. Strong fairness is a liveness property. Another way to say this is: "Action A cannot be repeatedly enabled forever without an A step eventually occurring".

## Reception by Engineers

Engineers have a preconceived notion that formal methods for checking the correctness of systems is a high-effort endeavor that is only feasible for trivial systems. Engineers at AWS believe this to be wrong and describe how they convinced other engineers to adopt the technology in their paper "How Amazon Web Services Uses Formal Methods". They call TLA+ "exhaustively test-able pseudo-code" rather than calling it a formal model to avoid the preconceived notions. This language may be useful in convincing your teammates.

## Author

TLA+ was initially developed by Leslie Lamport.

## Examples

```
// Given this following C code

int i;
void main() {
  i = someNumber(); // returns 1-1000
  i = i + 1;
}

// The following TLA+ formula can describe it

IF pc = "start" // note that mathematical if-then is the same as AND
  THEN (i' \in 0..1000) /\ 
       (pc' = "middle")
ELSE IF pc = "middle" // mathematical if-else is the same as OR
  THEN (i' = i + 1) /\
       (pc' = "done")
ELSE FALSE

// The following TLA+ formula is equivalent to the above, but is more idiomatic TLA+ (and is easier to read)

\/ /\ pc = "start"
   /\ i' \in 0..1000
   /\ pc' = "middle"
\/ /\ pc = "middle"
   /\ i' = i + 1
   /\ pc' = "done" 
```

## Related Quotes

*All models are wrong - some are useful.*

*If you're thinking without writing, you only think you're thinking.*
