# First-Order Logic Solver: Wumpus World

This repository contains a **First-Order Logic (FOL) Solver** implemented in Python, designed to navigate and reason within the **Wumpus World** environment. The solver uses automated logical reasoning to determine whether a specific coordinate in a cave is **SAFE**, **UNSAFE**, or **RISKY**, based on perceived sensory data such as **Breezes** and **Stenches**.

---

## Technical Overview

The solver is built on a custom First-Order Logic engine that processes disjunctive rules and literals to perform logical deduction.

### Core Components

- **Unification and Occurs Check**  
  Implements a recursive unification algorithm to find substitutions between expressions.  
  Includes an `occurs_check` to prevent infinite loops by ensuring a variable does not appear inside the value it is being unified with.

- **Resolution Engine**  
  Uses proof by contradiction with a **Set of Support** strategy.  
  The query is negated and added to the Knowledge Base (KB), and the solver searches for an empty clause to prove the query true.

- **Subsumption**  
  Improves efficiency by identifying and discarding rules that are less general than or equal to existing rules, preventing redundant inference steps.

- **Advanced Inference**  
  When standard resolution is inconclusive (resulting in a **RISKY** status), the solver performs secondary analysis of **Stench** and **Breeze** locations.  
  This analysis deduces **Wumpus-free** and **Pit-free** cells using grid constraints and available arrow count.

---

## Cave File Format

The solver processes text files that describe cave environments. These files must follow a specific structure for correct parsing:

```text
GRID: 4x4
ARROWS: 1
PATH:
(0,0) Breeze:F Stench:F
(0,1) Breeze:T Stench:F
QUERY: (1,1)
RESOLUTION: SAFE
```

### Field Descriptions

- **GRID**  
  Defines the square dimensions of the cave.

- **ARROWS**  
  Specifies the number of arrows available to the agent.

- **PATH**  
  A list of visited coordinates and the sensory data (`True` or `False`) detected at each step.

- **QUERY**  
  The target `(x, y)` coordinate whose safety is being evaluated.

- **RESOLUTION**  
  The expected ground-truth answer used for verification.

---

## How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/wumpus-fol-solver.git
cd wumpus-fol-solver
```

### 2. Configure the Path

Open the main Python script and update the `file_path` variable in the first code cell to point to your desired cave file:

```python
puzzle_level = 'hard'
file_path = f'/path/to/your/Caves/{puzzle_level}/path_h4.txt'
```

### 3. Execute the Solver

Run the script to process the cave file and execute the resolution queries.  
The solver will:

- Load general Wumpus World rules  
- Parse cave-specific facts  
- Attempt to resolve the safety of the query coordinate

### 4. View Results

The solver generates an output file named:

```text
group_11_path_{ID}.txt
```

This file includes:

- A list of all clauses used in the Knowledge Base  
- The final query result: **SAFE**, **UNSAFE**, or **RISKY**

---

## Authors

- Jada Zorn  
- Sara Croghan
