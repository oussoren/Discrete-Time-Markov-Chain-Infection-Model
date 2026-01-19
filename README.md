# Discrete-Time-Markov-Chain-Infection-Model

**Status:** Active Development
**Technologies:** Python, NumPy, Matplotlib, SciPy

### Project Overview
This project implements a spatial simulation engine to model the stochastic propagation of an agent (e.g., a virus or signal) across a 2D grid. Unlike standard iterative simulations, this engine utilizes **Discrete-Time Markov Chains (DTMC)** and linear algebra optimizations to project state distributions over time efficiently.

The core goal is to model "absorption" events—such as total infection or signal decay—using matrix operations rather than computationally expensive Monte Carlo loop iterations for every single step.

### Key Features (Resume Highlights)
* **Vectorized State Transitions:** Replaces $O(k)$ iterative loops with matrix exponentiation ($P_k = P^k$) to project states to time $t=k$ in logarithmic time complexity.
* **Component Decomposition:** Separates "Movement" and "Survival/Infection" probabilities into distinct transition matrices to allow for modular environment adjustments.
* **Absorbing State Analysis:** Calculates the cumulative likelihood of absorption (final state) analytically using fundamental matrix sets.
* **2D Grid Modeling:** Maps spatial coordinates to a flattened state vector for linear algebra processing.

### Mathematical Background
The system models the probability distribution $\pi_t$ at time $t$ given an initial distribution $\pi_0$ and a transition matrix $P$:

$$\pi_t = \pi_0 P^t$$

To handle the "absorption" (e.g., when an agent stops moving or a node is fully infected), the transition matrix is organized into canonical form:

$$P = \begin{pmatrix} Q & R \\ 0 & I \end{pmatrix}$$

Where $Q$ represents transient states (active spread) and $I$ represents absorbing states.

### Roadmap & Future Improvements
**Short-Term (Current Focus):**
- [ ] **Visualization:** Add heatmap generation to visualize the probability density of infection across the grid at $t=10, 50, 100$.
- [ ] **Boundary Conditions:** Refine edge-case behavior (reflecting vs. absorbing boundaries).

**Long-Term (Q2 2026):**
- [ ] **Time-Inhomogeneous Chains:** Allow transition matrices to evolve over time (e.g., introducing "quarantine" measures that alter probabilities at $t=50$).
- [ ] **SIR Integration:** Expand the state space to model Susceptible-Infected-Recovered dynamics rather than simple binary occupancy.
- [ ] **Performance Benchmarking:** Quantify the runtime difference between iterative simulation vs. matrix exponentiation for large grid sizes ($N > 10,000$).
