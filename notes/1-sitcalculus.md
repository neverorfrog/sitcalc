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

## Slide 18 - Frame Problem
- Frame axioms tell us what does not change as a consequence of an action
- How do we get to a concise representation of frame axioms from effect axioms?
  - Main premise is that very few actions influence a fluent
  - We want to capture all the circumstances for which on object breaks following a certain action
  1) Object can break either if it is dropped and it's fragile, or if a bomb explodes near it: expressing the effect axioms in normal form
      - $ (\exists r.a=drop(r,x) \land Fragile(x)) \lor (\exists b.a=explode(b) \land NearTo(b,x,s)) \supset Broken(x,do(a,s))$
      - $ \Phi_F^+(x,a,s) \supset F(x,do(a,s))$
  2) If an object is not broken in situation s and is instead broken after $do(a,s)$ we can deduce that it was either dropped or a bomb exploded near it: causal completeness assumption, expressing the effect axioms as explanation closure axioms
      - $\neg broken(x,s) \land broken(x,do(a,s)) \supset (fragile(x,s) \land \exists r.a=drop(r,x)) \lor (nextTo(b,x,s) \land \exists b.a=explode(b))$
      - $\neg F(x,s) \land F(x,do(a,s)) \supset \Phi_F^+(x,a,s)$
  3) Object is broken if $\Phi_F^+(x,a,s)$ is true, or if it is already broken and $\Phi_F^-(x,a,s)$ is true
      - $Broken(x,do(a,s)) \equiv (\exists r.a=drop(r,x) \land Fragile(x)) \lor (\exists b.a=explode(b) \land NearTo(b,x,s)) \lor Broken(x,s) \land \neg \exists r.a = repair(r,x)$
      - $F(x,do(a,s)) \equiv \Phi_F^+(x,a,s) \lor F(x,s) \land \neg \Phi_F^-(x,a,s)$
  - We want to capture all the circumstances for which an object is repaired
    - Suppose an object can be repaired if it is broken
    - If an object is broken in situation s and is not borken after $do(a,s)$ we can dedue that it was repaired
    - $broken(x,s) \land \neg broken(x,do(a,s)) \supset \exists r.a = repair(r,x)$
    - Same reasoning as above...

