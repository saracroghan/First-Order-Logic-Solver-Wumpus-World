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

GRID: 4x4
ARROWS: 1
PATH:
(0,0) Breeze:F Stench:F
(0,1) Breeze:T Stench:F
QUERY: (1,1)
RESOLUTION: SAFE


GRID: Defines the square dimensions of the cave.


ARROWS: The number of arrows available to the agent.


PATH: A list of coordinates visited and the sensory data (True/False) detected at each step.



QUERY: The target (x, y) coordinate to be evaluated.



RESOLUTION: The expected ground-truth answer used for verification.

How to Run
Clone the Repository:

Bash

git clone [https://github.com/your-username/wumpus-fol-solver.git](https://github.com/your-username/wumpus-fol-solver.git)
cd wumpus-fol-solver
Configure the Path: Open the main Python script and update the file_path variable to point to your desired cave file.

Python

puzzle_level = 'hard'
file_path = f'/path/to/your/Caves/{puzzle_level}/path_h4.txt'
Execute the Solver: Run the script to process the cave file and execute the resolution queries. The solver will load general Wumpus World rules, parse the cave facts, and attempt to resolve the safety of the query coordinate.


View Results: The solver generates an output file named group_11_path_{ID}.txt. This file includes:

A list of all clauses used in the Knowledge Base.

The final query result: SAFE, UNSAFE, or RISKY.

Authors
Jada Zorn 

Sara Croghan
