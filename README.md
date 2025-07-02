# 🧠 Genetic Algorithm for Vehicle Routing Problem with Time Windows (VRPTW)

This project implements a Genetic Algorithm (GA) to solve a variant of the **Vehicle Routing Problem (VRP)** with **Time Windows** and **Capacity Constraints**. The dataset and problem formulation are adopted from the research paper:

> **"Optimization strategy of mixed-integer linear planning in logistics distribution"** by Yuhua Li, published in *Applied Mathematics and Nonlinear Sciences, 2024* [DOI: 10.2478/amns-2024-1904]:contentReference[oaicite:0]{index=0}.

While the paper solves the VRPTW using a **Mixed-Integer Linear Programming (MILP)** approach and achieves superior performance, this project explores a **metaheuristic alternative** via a **Genetic Algorithm** for scenarios where MILP may be infeasible due to scale or real-time requirements.

---

## 🧩 Problem Description

- **Depot**: Single starting and ending location for all routes.
- **Vehicles**: 5 vehicles with a fixed cost and capacity of 1100 kg each.
- **Customers**: 24 customers with spatial coordinates, demand (kg), and both required and acceptable time windows.
- **Objective**: Minimize the **total cost**, comprising:
  - Transport cost (distance × unit cost)
  - Fixed vehicle cost
  - Penalty cost for violating time windows or exceeding capacity

---

## 📚 Dataset Source

The customer and depot data are based on the actual logistics dataset used in the cited paper's case study on Company A’s distribution operations in H City. Each customer has:
- A unique `(x, y)` location
- A delivery demand in kg
- An acceptable and a required delivery time window in minutes since 5:00 AM (start time)

---

## 🔧 Genetic Algorithm Design

### Key Components
- **Population Size**: 100
- **Generations**: 300
- **Chromosome**: List of routes (one per vehicle), each a list of customer IDs
- **Initialization**: Priority-based customer sorting by time window, randomized vehicle assignment
- **Selection**: Top half (feasible solutions preferred)
- **Crossover**: Route-level swap with repair mechanisms
- **Mutation**:
  - *Intra-route*: Local search using route timing penalty optimization
  - *Inter-route*: Customer migration between routes (if capacity allows)
- **Fitness Function**: Inverse of total cost including penalties and fixed costs

### Penalty Functions
- Adaptive penalty weights for early and late deliveries
- High penalty for overloading vehicles

---

## 📈 Results Summary

After 300 generations, the best GA solution achieved:

| Metric                  | Value (CNY)  |
|-------------------------|--------------|
| 🚚 Fixed Vehicle Cost    | 500          |
| 🛣️ Transport Cost        | 6279.43      |
| ⏰ Time Penalty Cost     | 860.14       |
| 💰 Total Cost            | **7639.56**  |

### Final Routes

Each vehicle's route, total load, distance, cost, and penalties are printed and plotted. For instance:

Vehicle 1:
  Route: Depot -> 24 -> 2 -> 18 -> 15 -> 17 -> Depot
  Load: 1067 kg
  Distance: 554.69 units
  Transport Cost: 1386.72 CNY
  Penalty Cost: 88.82 CNY

Vehicle 2:
  Route: Depot -> 13 -> 10 -> 8 -> 12 -> Depot
  Load: 971 kg
  Distance: 503.25 units
  Transport Cost: 1258.12 CNY
  Penalty Cost: 141.28 CNY

Vehicle 3:
  Route: Depot -> 16 -> 21 -> 4 -> 6 -> 14 -> Depot
  Load: 1074 kg
  Distance: 569.05 units
  Transport Cost: 1422.62 CNY
  Penalty Cost: 17.56 CNY

Vehicle 4:
  Route: Depot -> 1 -> 7 -> 11 -> 9 -> 5 -> 3 -> 19 -> Depot
  Load: 967 kg
  Distance: 643.19 units
  Transport Cost: 1607.96 CNY
  Penalty Cost: 348.75 CNY

Vehicle 5:
  Route: Depot -> 22 -> 23 -> 20 -> Depot
  Load: 957 kg
  Distance: 241.60 units
  Transport Cost: 604.01 CNY
  Penalty Cost: 108.29 CNY


A **Matplotlib animation** is also generated to visualize vehicle movement from the depot to customer points.

---

## 📉 Comparison with MILP

The MILP model presented in the paper achieved:
- Lower penalty cost (third vehicle’s penalty reduced by **66.40%**)
- Better load balancing and fewer violations
- Precise global optimization via solver-based methods (Matlab + GAMS)

In contrast, while the GA solution performs decently and respects constraints, it does not match the MILP result in terms of cost minimization or delivery punctuality due to the stochastic nature and local search limitations of genetic algorithms.

---

## ✅ Strengths

- Easy to scale to larger datasets
- No requirement for MILP solvers
- Integrated route repair and timing optimization
- Visual feedback for debugging and presentation

---

## ⚠️ Limitations

- Slower convergence compared to exact solvers
- Stochastic: results vary by run
- May not reach global optimum without hybridization
- No advanced neighborhood search (e.g., inter-route 2-opt)

---

## 🧪 Future Improvements

- Add **inter-route 2-opt** and **3-opt** heuristics
- Integrate **K-means initialization** to improve early population diversity
- Combine GA with **local search (memetic)** or **simulated annealing**
- Constraint-aware crossover operators

---

## 📂 Files

- `vrp_ga.py` – Main Python code implementing the GA
- `README.md` – This project description
- `Optimization_strategy_of_mixed-integer_linear_plan.pdf` – Source research paper

---

## 👨‍💻 Author

**Istiaqe Ahamed**

Email: istiaqeahamed09@gmail.com

LinkedIn: [linkedin.com/in/istiaqeahamed](https://www.linkedin.com/in/istiaqe-ahamed/)

GitHub: [github.com/ias09](https://github.com/ias09)

ORCID: [0009-0009-5729-7312](https://orcid.org/0009-0009-5729-7312)

Dataset and benchmark inspiration from Yuhua Li (2024). Optimization Strategy of Mixed-Integer Linear Planning in Logistics Distribution. Published in Applied Mathematics and Nonlinear Sciences.
  DOI: 10.2478/amns-2024-1904
---

## 📜 License

This project is open-sourced under the MIT License.

## 📚 Reference
Yuhua Li (2024). Optimization Strategy of Mixed-Integer Linear Planning in Logistics Distribution.
Published in Applied Mathematics and Nonlinear Sciences.

DOI: 10.2478/amns-2024-1904
---

