# Formal Proof of Nonconvexity and Discontinuity in Ride-Sharing Optimization

This repository contains the theory and proof of the nonconvexity of ride-sharing optimization problems.

📄 [Read the full proof in PDF format](Proof_ofconvexity.pdf)

## Problem Setup

Let:

- \( D = \{d_1, d_2, \dots, d_{|D|}\} \) be the set of drivers,
- \( R = \{r_1, r_2, \dots, r_{|R|}\} \) be the set of riders.

Define the binary decision variable:

\[
I_{d_i, r_j} \in \{0, 1\}, \quad \forall d_i \in D, \; \forall r_j \in R,
\]

with the interpretation:

- \( I_{d_i, r_j} = 1 \): rider \( r_j \) is assigned to driver \( d_i \),
- \( I_{d_i, r_j} = 0 \): otherwise.

Let the full vector of decision variables be:

\[
\mathbf{I} = \bigl(I_{d_1, r_1}, I_{d_1, r_2}, \dots, I_{d_{|D|}, r_{|R|}}\bigr) \in \{0,1\}^n, \quad \text{where } n = |D| \cdot |R|.
\]

The objective is to maximize a linear function:

\[
\max \sum_{i=1}^{|D|} \sum_{j=1}^{|R|} I_{d_i, r_j}.
\]

### Subject to Constraints

**Unique Assignment Constraint:**

\[
\sum_{i \in D} I_{d_i, r_j} \leq 1, \quad \forall j \in \{1, 2, \dots, |R|\}
\]

**Driver Capacity Constraint:**

\[
\sum_{j \in R} I_{d_i, r_j} \leq n_i, \quad \forall i \in \{1, 2, \dots, |D|\}
\]

**Path Deviation Constraint:**

\[
\Delta_i \leq t_i \cdot |P_i|, \quad \forall i \in \{1, 2, \dots, |D|\}
\]

---

## Convex Optimization Problem (Standard Form)

*Definition from Convex Optimization, pages 136–137:*

A convex optimization problem is one of the form:

\[
\begin{aligned}
\text{Minimize} \quad & f_0(x) \\
\text{Subject to} \quad & f_i(x) \leq 0, \quad i = 1, \dots, m, \\
& a_i^T x = b_i, \quad i = 1, \dots, p,
\end{aligned}
\]

Where:

- \( f_0(x) \) is the objective function (to be minimized),
- \( f_i(x) \) are inequality constraint functions,
- \( a_i^T x = b_i \) are equality constraints.

### Convexity Requirements

To qualify as a convex optimization problem, the following must hold:

- \( f_0(x) \) is a convex function over a convex feasible set,
- Each inequality constraint function \( f_i(x) \) is convex,
- Each equality constraint \( a_i^T x = b_i \) is affine (i.e., linear).

**Convex Function:** \( f(x_1, x_2, \ldots, x_n) \) is convex if, for each pair of points on the graph of \( f \), the line segment joining these two points lies entirely above or on the graph of \( f \).

**Convex Set:** A convex set is a collection of points such that, for each pair of points in the collection, the entire line segment joining these two points is also in the collection.

*Both definitions from Introduction to Operations Research by Frederick S. Hillier and Gerald J. Lieberman, pages 995 and 997.*

---

## Proof of Nonconvexity (by Counterexample)

We demonstrate nonconvexity by constructing a specific counterexample.

### Simplified Problem

Consider a minimal problem with:

- One driver (\( d_1 \)), i.e., \( |D|=1 \),
- Two riders (\( r_1 \) and \( r_2 \)), i.e., \( |R|=2 \),

Let \( x \equiv I_{d_i, r_j} \) and the objective:

\[
f_0(x) = f_0(I_{d_i, r_j}) = -\sum_{i=1}^{|D|} \sum_{j=1}^{|R|} I_{d_i, r_j},
\]

All constraints are trivially satisfied (e.g., unlimited capacity).

The decision variables reduce to:

\[
I_{d_1, r_1}, \quad I_{d_1, r_2} \in \{0, 1\}.
\]

---

### Convexity Requirement

**Condition 1:** \( f_0(I_{d_i, r_j}) \) is a convex function over a convex feasible set.

First, we check if the feasible set is convex. The feasible region is:

\[
\mathcal{C} = \bigl\{ (0,0), (1,0), (0,1), (1,1) \bigr\} \subseteq \{0,1\}^2.
\]

According to the definition of a convex set, let:

\[
x = (1, 0) \in \mathcal{C}, \quad y = (0, 1) \in \mathcal{C}.
\]

Take a convex combination with \( \theta = 0.5 \):

\[
z = \theta x + (1-\theta) y = 0.5 \cdot (1, 0) + 0.5 \cdot (0, 1) = (0.5, 0.5).
\]

---

### Contradiction

Clearly:

\[
z = (0.5, 0.5) \notin \mathcal{C} = \{0,1\}^2.
\]

Therefore, the set \( \mathcal{C} \) is **not** a convex set. Hence, Ride-Sharing Optimization is **not a convex problem**. We do not check for other requirements.

---

## Notes

- The feasible sets for discrete optimization problems can be thought of as exhibiting an extreme form of nonconvexity, as a convex combination of two feasible points is in general not feasible (*Nocedal and Wright, Numerical Optimization*, 2nd ed., Springer, 1999, p. 5).
- Both ILP and BILP are fundamental discrete optimization models because many real-world problems can be modeled using integer or binary decisions.