# Situation Calculus

## Slide 8
- using models means creating a database of the particular instance
- database has a complete information

## Slide 9
- using theories means creating (truth) sentences which are satisfied by the model in slide 8
- it's like if everything is universally quantified by default if it is a free variable
- advantage of theories: globality, which allows to represent incomplete information

## Slide 13 - Definition of situation
1. Finite list of actions (kind of stored in reverse order)
2. First-order term (?)
3. Resulting state when departing from a known initial state 

Formally:
  - Initial situation $S_0$
  - Successor situation $do(a,s)$
    - Actions are functions (parametrized)

## Slide 14 - How do we represent fluents?
- We add the situation argument to the subject of the predicate
  - Open(d,s) $\rightarrow$ door d is open in situation s
- Two types
  - Relational: $closeTo(x,s)$
  - Functional: $colour(x,s)$
- This means that a predicate can be true or false for an argument depending on the situation
  - Robot
    - *SelfIn(x,S0)* is true if x is A and the robot starts from room A
    - But if the robot does *do(GoTo(B),S0)*, then *SelfIn(A,S0)* becomes false
  - Island
    - *OnIsland(A,S0)* is true if A is on the island
    - But if the next action is *do(leave(A,s),S0)*, then *OnIsland(A,S0)* becomes false

## Slide 17 - Precondition and Effect Axioms
- $Poss(repair(r,s),s) \supset hasGlue(r,s) \land broken(x,s)$
  - The robot can repair an object if it has glue and the object is broken in situation s
- $Poss(leave(p),s) \supset knowsColour(p,s)$
  - The person can leave only if it knows its own eye colour
- $ \neg broken(x, do(repair(r,x), s))$
  - The effect of repairing something is that the object is not broken anymore
- $ \neg OnIsland(p, do(leave(p), s))$
  - The effect of leaving is not being on the island anymore

## Slide 18 - Frame Axioms
- Axioms that tell us what does not change as a consequence of an action
- Opposed to effect axioms
