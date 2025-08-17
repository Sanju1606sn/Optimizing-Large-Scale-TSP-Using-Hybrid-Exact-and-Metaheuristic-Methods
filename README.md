# Large-Scale TSP Optimization with Exact, Heuristic & Metaheuristic Approaches

##  Project Overview

The **Traveling Salesman Problem (TSP)** is one of the most widely studied combinatorial optimization problems. It involves finding the shortest possible route that visits a set of cities exactly once and returns to the origin. Although the problem is simple to state, it is **NP-hard**, making it computationally challenging to solve for large-scale datasets.

This project focuses on solving a **100-city TSP instance** using a mix of **exact optimization methods, heuristics, and metaheuristic algorithms**. The primary goals of the project were:

* To compare **mathematical optimization solvers** (PuLP & Gurobi) with **metaheuristic approaches** (Genetic Algorithm & Simulated Annealing).
* To leverage **OR-Tools heuristics** as warm-start solutions for large-scale TSP and evaluate their effect on solver performance.
* To **visualize the optimized routes** interactively using **Folium maps** for better interpretability.

---

##  Methodology

### 🔹 Data

* The dataset consisted of **100 cities**, each defined by its coordinates (latitude, longitude).
* The **Euclidean distance matrix** was computed as the cost metric for route optimization.

### 🔹 Exact Optimization

* **PuLP** (an open-source linear programming library) was used to model the TSP as a **Mixed Integer Linear Program (MILP)**.
* **Gurobi**, a state-of-the-art commercial solver, was integrated with PuLP for large-scale optimization.
* The standard **Miller–Tucker–Zemlin (MTZ)** formulation was applied to eliminate sub-tours.
* To accelerate convergence, **warm-starting with OR-Tools heuristics** (Nearest Neighbor & Savings heuristic) was performed.
* Additional **parameter tuning** in Gurobi (cutting planes, MIP gap tolerance) was explored for performance improvement.

### 🔹 Heuristic Warm-Starts

* **OR-Tools** was used to generate fast heuristic solutions.
* These solutions were passed to Gurobi as an **initial feasible solution**.
* This reduced solver effort in the branch-and-bound process and improved the final solution quality.

### 🔹 Metaheuristic Approaches

Two population-based/metaheuristic approaches were implemented:

1. **Genetic Algorithm (GA)**

   * Initial population generated using random permutations of city order.
   * Crossover (Order Crossover) and mutation (Swap Mutation) operators applied.
   * Elitism strategy ensured best solutions carried over generations.
   * GA converged to near-optimal solutions with consistent results.

2. **Simulated Annealing (SA)**

   * Started with a random feasible solution.
   * Iteratively applied local swaps while probabilistically accepting worse solutions (to escape local minima).
   * Cooling schedule controlled the acceptance probability.
   * While effective, SA was slower in reaching high-quality solutions compared to GA.

### 🔹 Visualization

* Optimized tours were plotted using **Folium**, providing interactive maps.
* Each city was marked, and the optimal route was drawn as a polyline across all 100 cities.
* Visualization made it easy to interpret how solvers and heuristics structured routes.

---

##  Results

* **Gurobi (with warm-start)** outperformed PuLP and achieved a **27.5% faster convergence** compared to starting from scratch.
* **Genetic Algorithm (GA)** provided the **best metaheuristic solution**, balancing exploration and exploitation effectively.
* **Simulated Annealing (SA)** found feasible solutions but required more iterations to match GA’s performance.
* **Route visualization with Folium** confirmed that warm-start and GA-based solutions closely resembled the optimal tour.

### Key Observations:

* For **large-scale instances (100 cities)**, exact methods struggle without heuristics.
* **Warm-starting with OR-Tools** significantly boosts solver efficiency.
* **Metaheuristics** provide competitive alternatives when solver runtimes become prohibitive.

---

##  Tools & Libraries

* **Optimization Libraries:** PuLP, Gurobi, OR-Tools
* **Metaheuristics:** Custom Python implementation of Genetic Algorithm & Simulated Annealing
* **Visualization:** Folium, Matplotlib
* **Data Handling:** NumPy, Pandas

---

##  Future Work

* Extend to **multi-objective TSP** (e.g., minimizing distance and risk simultaneously).
* Apply **Ant Colony Optimization (ACO)** and **Particle Swarm Optimization (PSO)** for further benchmarking.
* Integrate **real-world datasets** (road networks, travel time, traffic data).
* Deploy a **dashboard application** where users can upload city coordinates and visualize optimized tours.

---

##  Conclusion

This project demonstrates that solving large-scale TSP requires a **hybrid approach**:

* **Exact solvers (PuLP/Gurobi)** guarantee optimality but scale poorly.
* **Heuristics (OR-Tools warm-start)** significantly speed up exact optimization.
* **Metaheuristics (GA & SA)** provide near-optimal solutions with lower computational cost.

By combining mathematical programming with intelligent heuristics and metaheuristics, the project provides an effective framework for addressing large-scale routing problems, with direct applicability in **logistics, supply chain, and transportation systems**.

---


