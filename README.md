# First-Order Logic Solver: Wumpus World

[cite_start]This repository contains a First-Order Logic (FOL) Solver implemented in Python, specifically designed to navigate and reason within the Wumpus World environment[cite: 1]. [cite_start]The program utilizes automated reasoning to determine if a specific coordinate in a cave is SAFE, UNSAFE, or RISKY based on perceived sensory data such as Breezes and Stenches[cite: 54].

## Technical Overview

[cite_start]The solver is built on a custom FOL engine that processes disjunctive rules and literals to perform logical deduction[cite: 7].

### Core Components
* [cite_start]**Unification and Occurs Check**: Implements a recursive unification algorithm to find substitutions between expressions[cite: 32]. [cite_start]It includes an occurs_check to prevent infinite loops by checking if a variable appears inside the value it is being unified with[cite: 30].
* [cite_start]**Resolution Engine**: Uses proof by contradiction with a Set of Support strategy[cite: 42]. [cite_start]By negating the query and adding it to the Knowledge Base (KB), the solver looks for an empty clause to prove the query true[cite: 42, 44].
* [cite_start]**Subsumption**: To maintain efficiency, the solver identifies and discards rules that are less general than or equal to existing ones, preventing the Knowledge Base from redoing unnecessary steps[cite: 8, 46].
* [cite_start]**Advanced Inference**: When standard resolution is inconclusive (resulting in a RISKY status), the solver performs a secondary analysis of Stench and Breeze locations to deduce Wumpus-free and Pit-free cells based on grid constraints and arrow count[cite: 54, 58, 60].

## Cave File Format

[cite_start]The program processes text files representing cave environments[cite: 12]. [cite_start]These files must follow a specific structure for the parser to load facts correctly[cite: 12]:

GRID: 4x4
ARROWS: 1
PATH:
(0,0) Breeze:F Stench:F
(0,1) Breeze:T Stench:F
QUERY: (1,1)
RESOLUTION: SAFE

* [cite_start]GRID: Defines the square dimensions of the cave[cite: 13].
* [cite_start]ARROWS: The number of arrows available to the agent[cite: 13].
* [cite_start]PATH: A list of coordinates visited and the sensory data (True/False) detected at each step[cite: 14, 19, 24].
* [cite_start]QUERY: The target (x, y) coordinate to be evaluated[cite: 15, 29].
* [cite_start]RESOLUTION: The expected ground-truth answer used for verification[cite: 16].

## How to Run

1. Clone the Repository:
git clone https://github.com/your-username/wumpus-fol-solver.git
cd wumpus-fol-solver

2. Configure the Path:
[cite_start]Open the main Python script and update the file_path variable in the first code cell to point to your desired cave file[cite: 1].
puzzle_level = 'hard'
file_path = f'/path/to/your/Caves/{puzzle_level}/path_h4.txt'

3. Execute the Solver:
Run the script to process the cave file and execute the resolution queries. [cite_start]The solver will load general Wumpus World rules, parse the cave facts, and attempt to resolve the safety of the query coordinate[cite: 54].

4. View Results:
[cite_start]The solver generates an output file named group_11_path_{ID}.txt[cite: 52]. This file includes:
* [cite_start]A list of all clauses used in the Knowledge Base[cite: 52].
* [cite_start]The final query result: SAFE, UNSAFE, or RISKY[cite: 53, 54].

## Authors
* [cite_start]Jada Zorn [cite: 1]
* [cite_start]Sara Croghan [cite: 1]
