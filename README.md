# First-Order Logic Solver: Wumpus World

This repository contains a First-Order Logic (FOL) Solver implemented in Python, specifically designed to navigate and reason within the Wumpus World environment. The program utilizes automated reasoning to determine if a specific coordinate in a cave is SAFE, UNSAFE, or RISKY based on perceived sensory data such as Breezes and Stenches.

## Technical Overview

The solver is built on a custom FOL engine that processes disjunctive rules and literals to perform logical deduction.

### Core Components
* **Unification and Occurs Check:** Implements a recursive unification algorithm to find substitutions between expressions. It includes an occurs_check to prevent infinite loops during variable binding.
* **Resolution Engine:** Uses proof by contradiction with a Set of Support strategy. By negating the query and adding it to the Knowledge Base (KB), the solver looks for an empty clause to prove the query true.
* **Subsumption:** To maintain efficiency, the solver identifies and discards rules that are less general than existing ones, preventing the Knowledge Base from redoing unnecessary steps.
* **Advanced Inference:** When standard resolution is inconclusive (resulting in a RISKY status), the solver performs a secondary analysis of Stench and Breeze locations to deduce Wumpus-free and Pit-free cells.

## Cave File Format

The program processes text files representing cave environments. These files must follow a specific structure for the parser to load facts correctly:

```text
GRID: 4x4
ARROWS: 1
PATH:
(0,0) Breeze:F Stench:F
(0,1) Breeze:T Stench:F
QUERY: (1,1)
RESOLUTION: SAFE
