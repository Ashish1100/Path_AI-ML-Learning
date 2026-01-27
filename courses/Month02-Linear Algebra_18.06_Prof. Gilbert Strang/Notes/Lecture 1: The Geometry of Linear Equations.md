# MIT 18.06 – Linear Algebra
## Lecture 1: The Geometry of Linear Equations

---

## Table of Contents

1. [Objective](#1-objective)
2. [Importance](#2-importance)
3. [Concepts](#3-concepts)
   - 3.1 [Systems of Linear Equations](#31-systems-of-linear-equations)
   - 3.2 [Matrix Form of Linear Equations](#32-matrix-form-of-linear-equations)
   - 3.3 [The Row Picture](#33-the-row-picture)
   - 3.4 [The Column Picture ★](#34-the-column-picture-)
   - 3.5 [Linear Combination](#35-linear-combination)
   - 3.6 [Span and Column Space](#36-span-and-column-space)
   - 3.7 [Consistency and Inconsistency](#37-consistency-and-inconsistency)
   - 3.8 [Singular vs. Non-Singular Matrices](#38-singular-vs-non-singular-matrices)
4. [Maths](#4-maths)
   - 4.1 [Matrix-Vector Multiplication](#41-matrix-vector-multiplication-ax--b)
   - 4.2 [The 2D Case](#42-the-2D-case)
   - 4.3 [The 3D Case](#43-the-3D-case)
   - 4.4 [The 9D Case](#44-the-9D-case)
   - 4.5 [When Solvability Fails](#45-when-does-solvability-fail)
   - 4.6 [Worked Example: 2D System](#46-worked-example-2D-system)
5. [Big Question](#5-big-question)
6. [Important Questions](#6-important-questions)
   - Q1 [Column Space](#question-1-what-is-the-column-space-of-a-matrix)
   - Q2 [Non-Intersecting Planes](#question-2-if-planes-do-not-intersect-what-does-that-tell-us-about-the-system)
   - Q3 [Overdetermined Systems](#question-3-can-three-equations-in-two-unknowns-have-a-solution)
   - Q4 [Linear Dependence](#question-4-what-does-it-mean-for-the-columns-of-a-matrix-to-be-linearly-dependent)
   - Q5 [Row vs. Column Picture](#question-5-what-is-the-difference-between-the-row-picture-and-the-column-picture)
   - Q6 [Universal Solvability](#question-6-is-it-always-possible-to-solve-ax--b-for-every-right-hand-side-b)
   - Q7 [High-Dimensional Solvability](#question-7-in-high-dimensions-how-do-you-check-if-a-system-is-solvable-without-elimination)
   - Q8 [Non-Singular Matrices](#question-8-what-is-the-geometric-meaning-of-a-non-singular-matrix)
7. [Top-5 Interview Questions](#7-top-5-interview-questions)
8. [Interview Summary](#8-interview-summary)
9. [Summary](#9-summary)
10. [Additional](#10-additional)
---

## 1. Objective

This lecture introduces the fundamental problem of linear algebra: **solving systems of linear equations**. By the end of this lecture, students should understand:

- The basic structure of linear systems in matrix form (Ax = b)
- The **row picture** interpretation (geometric view via lines/planes)
- The **column picture** interpretation (geometric view via linear combinations)
- Why the column picture is essential for understanding solvability
- How geometry reveals algebraic properties that symbols alone may obscure
- The relationship between the solution of a system and the linear combinations of matrix columns

The lecture bridges elementary algebra (solving two equations in two unknowns) with the deeper geometric and algebraic frameworks that extend to arbitrary dimensions.

---

## 2. Importance

**Why this lecture is foundational:**

Linear Algebra solves the equation Ax = b, which appears ubiquitously in:

- **Engineering**: Structural analysis (forces, displacements), electrical circuits, control systems
- **Machine Learning & AI**: Neural networks train by solving optimization problems that reduce to linear systems; regression models use Aβ = y; recommendation systems rely on matrix factorization
- **Data Science**: Dimensionality reduction (PCA), matrix computations, feature transformations
- **Physics & Applied Mathematics**: Differential equations, modeling dynamical systems
- **Economics & Finance**: Input-output models, portfolio optimization, equilibrium analysis
- **Computer Graphics**: Transformations, projections, rendering

**Why matrices are more powerful than scalar equations:**

A scalar equation like ax = b (one unknown, one equation) is trivial. But:

- Systems can be **inconsistent** (no solution), **under-determined** (infinitely many), or **uniquely determined** (one solution)
- Matrices encode structure: independence, rank, null space
- Matrix notation compresses complexity: a system of 1000 equations in 1000 unknowns is written compactly as Ax = b
- The column picture reveals what right-hand sides b are **achievable**—this determines solvability globally

**The geometry tells us what algebra hides:**

Algebra manipulates symbols; geometry reveals existence, uniqueness, and structure. For example:
- Two lines in the plane either intersect (unique solution), are parallel distinct (no solution), or coincide (infinite solutions)
- Three planes in 3D generically meet at a point (unique solution), but can fail to intersect or intersect along a line/plane
- The column picture shows immediately whether b lies in the span of the columns

---

## 3. Concepts

### 3.1 Systems of Linear Equations

A **system of linear equations** is a set of equations of the form:

```
a₁₁x₁ + a₁₂x₂ + ⋯ + a₁ₙxₙ = b₁
a₂₁x₁ + a₂₂x₂ + ⋯ + a₂ₙxₙ = b₂
                ⋮
aₘ₁x₁ + aₘ₂x₂ + ⋯ + aₘₙxₙ = bₘ
```

**Intuition:** We have m constraints and n unknowns. The solution is the set of all x = (x₁, x₂, …, xₙ) satisfying all equations simultaneously.

**Example:**
```
2x - y = 0
-x + 2y = 3
```

Solving: From the first equation, y = 2x. Substituting into the second: -x + 2(2x) = 3 ⟹ 3x = 3 ⟹ x = 1, y = 2.

---

### 3.2 Matrix Form of Linear Equations

A system of m equations in n unknowns can be written compactly as:

**Ax = b**

where:
- A is an m × n **coefficient matrix** (rows = equations, columns = variables)
- x is an n × 1 **unknown vector**
- b is an m × 1 **right-hand side vector**

**Example:**
```
┌─      ─┐ ┌─   ─┐   ┌─   ─┐
│  2  -1 │ │  x  │   │  0  │
│ -1   2 │ │  y  │ = │  3  │
└─      ─┘ └─   ─┘   └─   ─┘
```

Here, A = [[2, -1], [-1, 2]], x = [x, y]ᵀ, b = [0, 3]ᵀ.

---

### 3.3 The Row Picture

The **row picture** interprets the system geometrically by plotting each equation as a geometric object:

- In 2D: Each linear equation ax + by = c is a **line**
- In 3D: Each linear equation ax + by + cz = d is a **plane**
- In ℝⁿ: Each equation defines an (n-1)-dimensional **hyperplane**

The solution is the **intersection** of all these geometric objects.

**Example (2×2 case):**

For 2x - y = 0 and -x + 2y = 3:

- **First equation** 2x - y = 0 ⟹ y = 2x is a line through the origin with slope 2
  - Points: (0,0) ✓, (1,2) ✓, (½, 1) ✓
  
- **Second equation** -x + 2y = 3 is a line NOT through the origin
  - When y = 0: x = -3, so the point (-3, 0) lies on this line
  - When x = 0: y = 3/2, so the point (0, 3/2) lies on this line
  - We can verify: if x = 1, y = 2: -1 + 4 = 3 ✓

- **Solution:** The two lines intersect at (x, y) = (1, 2)

**Example (3×3 case):**

```
2x - y + 0z = 0
-x + 2y - z = -1
0x - 3y + 4z = 4
```

Each equation defines a plane in 3D space:
- **First plane:** 2x - y = 0 is a vertical plane (parallel to the z-axis) containing the origin
- **Second plane:** -x + 2y - z = -1 passes through points satisfying this constraint
- **Third plane:** -3y + 4z = 4 also does not pass through the origin

Generically, three non-parallel planes meet at a single point. The row picture becomes harder to visualize in higher dimensions.

---

### 3.4 The Column Picture ★

The **column picture** is the key geometric insight. We interpret Ax as a **linear combination of the columns of A**:

**Ax = x₁(column 1) + x₂(column 2) + ⋯ + xₙ(column n) = b**

**Meaning:** The unknown vector x tells us *how much* of each column to take.

**Example (2×2 case):**

```
┌─      ─┐ ┌─   ─┐   ┌─   ─┐
│  2  -1 │ │  x  │   │  0  │
│ -1   2 │ │  y  │ = │  3  │
└─      ─┘ └─   ─┘   └─   ─┘
```

The columns are:
- Column 1: a₁ = [2, -1]ᵀ
- Column 2: a₂ = [-1, 2]ᵀ
- Right-hand side: b = [0, 3]ᵀ

The equation asks: *Find scalars x and y such that* x[2, -1]ᵀ + y[-1, 2]ᵀ = [0, 3]ᵀ

Solution: x = 1, y = 2 means take 1 copy of column 1 and 2 copies of column 2:
```
1·[2, -1]ᵀ + 2·[-1, 2]ᵀ = [2, -1]ᵀ + [-2, 4]ᵀ = [0, 3]ᵀ ✓
```

**Geometric view:** Plot the two column vectors in 2D space. The solution vector x describes a path:
- Start at the origin
- Move 1 unit in the direction of column 1, reaching (2, -1)
- From there, move 2 units in the direction of column 2 (i.e., 2 times (-1, 2)), adding (-2, 4)
- End point: (2-2, -1+4) = (0, 3), which is exactly b

---

### 3.5 Linear Combination

A **linear combination** of vectors v₁, v₂, …, vₙ is any sum of the form:

**c₁v₁ + c₂v₂ + ⋯ + cₙvₙ**

where c₁, c₂, …, cₙ are scalars (real numbers).

**Intuition:** A linear combination is a weighted sum. Each vector contributes with its own weight (scalar multiple).

**Example:**
```
3·[1, 0]ᵀ + 2·[0, 1]ᵀ = [3, 2]ᵀ
```

The result is a new vector. The key insight of the column picture is that solving Ax = b is equivalent to asking: *Can we write b as a linear combination of the columns of A?*

---

### 3.6 Span and Column Space

The **span** of a set of vectors is the set of all possible linear combinations of those vectors.

The **column space** of a matrix A (denoted C(A)) is the span of the columns of A:

**C(A) = {Ax : x ∈ ℝⁿ}**

**Solvability Criterion:** The system Ax = b has a solution if and only if b ∈ C(A) (i.e., b lies in the column space of A).

**Example:**
If A = [[1, 0], [0, 1]] (identity matrix), then C(A) = ℝ² (the entire 2D plane). Any b ∈ ℝ² is achievable.

If A = [[1, 2], [1, 2]] (columns are linearly dependent), then C(A) is a line in 2D (the span of [1, 1]ᵀ). Most right-hand sides b are not achievable.

---

### 3.7 Consistency and Inconsistency

**Consistent system:** A system Ax = b is **consistent** if it has at least one solution.

**Inconsistent system:** A system Ax = b is **inconsistent** if it has no solution.

**Row picture interpretation:**
- 2 lines: Consistent if they intersect (one point) or coincide (infinitely many); Inconsistent if parallel and distinct
- 3 planes: Consistent if they meet at a point or along a line (or all three coincide); Inconsistent if they don't all share a common point

**Column picture interpretation:**
- Consistent if b ∈ C(A)
- Inconsistent if b ∉ C(A)

**Example of inconsistency:**
```
x + y = 1
x + y = 2
```

In the row picture: Two parallel lines (same slope, different intercepts) — no intersection.

In the column picture: [1, 1]ᵀ x + [1, 1]ᵀ y = [1, 2]ᵀ.

Both columns are the same; their span is the line {t[1, 1]ᵀ}. The vector [1, 2]ᵀ does not lie on this line, so there is no solution.

---

### 3.8 Singular vs. Non-Singular Matrices

A matrix A is:
- **Non-singular** (or **invertible**) if A has full rank, meaning its columns are linearly independent
- **Singular** (or **non-invertible**) if A does not have full rank, meaning its columns are linearly dependent

**Consequence:**
- If A is non-singular, then Ax = b has a unique solution for every b
- If A is singular, then either:
  - No solution exists (if b ∉ C(A))
  - Infinitely many solutions exist (if b ∈ C(A) and the system is underdetermined)

**Geometric intuition:**
- Non-singular: The columns "fill" the entire space; we can reach any target b
- Singular: The columns lie in a lower-dimensional subspace; we can only reach b if it lies in that subspace

**Example of singularity:**
```
A = ┌─     ─┐
    │  2  4 │
    │  1  2 │
    └─     ─┘
```

Column 2 is 2 × Column 1. The two columns are **linearly dependent**. The column space is a line through the origin.
- For b = [1, 0.5]ᵀ (which lies on the line): infinitely many solutions
- For b = [0, 1]ᵀ (which does not lie on the line): no solution

---

## 4. Maths

### 4.1 Matrix-Vector Multiplication: Ax = b

**Definition:** For a matrix A (size m × n) and vector x (size n × 1), the product Ax is computed in **two equivalent ways**:

**Method 1: Column combination (Professor Strang's preferred method)**
```
Ax = [a₁ | a₂ | ⋯ | aₙ] · [x₁, x₂, …, xₙ]ᵀ 
   = x₁a₁ + x₂a₂ + ⋯ + xₙaₙ
```

**Method 2: Row-wise (dot products)**
```
(Ax)ᵢ = (row i of A) · x = aᵢ₁x₁ + aᵢ₂x₂ + ⋯ + aᵢₙxₙ
```

**Example:**
```
┌─     ─┐ ┌─   ─┐
│  2  5 │ │  1  │
│  1  3 │ │  2  │
└─     ─┘ └─   ─┘
```

**Method 1 (columns):**
```
= 1·[2, 1]ᵀ + 2·[5, 3]ᵀ 
= [2, 1]ᵀ + [10, 6]ᵀ 
= [12, 7]ᵀ
```

**Method 2 (rows):**
- Row 1: 2·1 + 5·2 = 2 + 10 = 12
- Row 2: 1·1 + 3·2 = 1 + 6 = 7
- Result: [12, 7]ᵀ

**Key insight:** The column interpretation reveals that Ax is always a linear combination of the columns of A. This is central to understanding when Ax = b has a solution.

---

### 4.2 The 2D Case

**System:**
```
2x - y = 0        ...(1)
-x + 2y = 3       ...(2)
```

**Matrix form:**
```
┌─      ─┐ ┌─   ─┐   ┌─   ─┐
│  2  -1 │ │  x  │   │  0  │
│ -1   2 │ │  y  │ = │  3  │
└─      ─┘ └─   ─┘   └─   ─┘
```

**Row picture:**

| Equation | Geometric interpretation | Algebraic solution |
|----------|-------------------------|-------------------|
| 2x - y = 0 | Line through origin; slope = 2 | y = 2x; passes through (0,0), (1,2), (0.5, 1) |
| -x + 2y = 3 | Line not through origin; slope = 0.5 | y = 0.5x + 1.5; passes through (-3,0), (0,1.5), (1,2) |
| **Intersection** | **Point (1,2)** | **Check Eq. (1):** 2(1) - 2 = 0 ✓; **Check Eq. (2):** -1 + 2(2) = 3 ✓ |

**Column picture:**

The columns of A are:
```
a₁ = [2, -1]ᵀ,    a₂ = [-1, 2]ᵀ
```

We seek x, y such that:
```
x·[2, -1]ᵀ + y·[-1, 2]ᵀ = [0, 3]ᵀ
```

**Geometric construction:**
1. Plot a₁ = (2, -1) from the origin (arrow pointing right-down)
2. Plot a₂ = (-1, 2) from the origin (arrow pointing left-up)
3. To reach b = (0, 3):
   - Move 1 unit in the direction of a₁: reach point (2, -1)
   - From (2, -1), move 2 units in the direction of a₂: move 2(-1, 2) = (-2, 4)
   - Final position: (2, -1) + (-2, 4) = (0, 3) ✓

The solution x = 1, y = 2 tells us that b is in the span of {a₁, a₂}.

---

### 4.3 The 3D Case

**System:**
```
2x - y = 0
-x + 2y - z = -1
-3y + 4z = 4
```

**Matrix form:**
```
┌─         ─┐ ┌─   ─┐   ┌─    ─┐
│  2  -1  0 │ │  x  │   │   0  │
│ -1   2 -1 │ │  y  │ = │  -1  │
│  0  -3  4 │ │  z  │   │   4  │
└─         ─┘ └─   ─┘   └─    ─┘
```

**Row picture:**

Each equation defines a plane in 3D space:

| Equation | Plane description |
|----------|-------------------|
| 2x - y = 0 | Vertical plane (parallel to z-axis); contains the origin |
| -x + 2y - z = -1 | Tilted plane; doesn't pass through the origin |
| -3y + 4z = 4 | Vertical plane (parallel to x-axis); doesn't pass through the origin |

Three non-parallel planes generically intersect at a single point. Here, the solution is x = (0, 0, 1) (which the professor verified by inspection).

**Verification:**
- Eq. 1: 2(0) - 0 = 0 ✓
- Eq. 2: -(0) + 2(0) - 1 = -1 ✓
- Eq. 3: -3(0) + 4(1) = 4 ✓

**Column picture:**

The columns are:
```
a₁ = [2, -1, 0]ᵀ,    a₂ = [-1, 2, -3]ᵀ,    a₃ = [0, -1, 4]ᵀ
```

We seek x, y, z such that:
```
x·a₁ + y·a₂ + z·a₃ = [0, -1, 4]ᵀ
```

Since a₃ = [0, -1, 4]ᵀ is exactly b, the solution is immediate: x = 0, y = 0, z = 1.

---

### 4.4 The 9D Case

**System:**
```
a₁₁x₁ + a₁₂x₂ + ... + a₁₉x₉ = b₁
a₂₁x₁ + a₂₂x₂ + ... + a₂₉x₉ = b₂
...
a₉₁x₁ + a₉₂x₂ + ... + a₉₉x₉ = b₉
```


**Matrix form:**
```
┌                           ┐ ┌    ┐   ┌    ┐
│  a₁₁   a₁₂   ...   a₁₉    │ │ x₁ │   │ b₁ │
│  a₂₁   a₂₂   ...   a₂₉    │ │ x₂ │   │ b₂ │
│   ⋮     ⋮     ⋱      ⋮     │ │  ⋮  │ = │  ⋮ │
│  a₉₁   a₉₂   ...   a₉₉    │ │ x₉ │   │ b₉ │
└                           ┘ └    ┘   └    ┘
```
The same concepts from our 3D example extend naturally to 9-dimensional space (ℝ⁹), though we lose the ability to visualize them directly.

#### Row Picture in 9D

In 9-dimensional space, each linear equation defines an **8-dimensional hyperplane**. A hyperplane in n-dimensional space always has dimension n-1.

For a 9×9 system with 9 equations:
- Each equation like a₁x₁ + a₂x₂ + ⋯ + a₉x₉ = b defines an 8D hyperplane in ℝ⁹
- With full rank (non-parallel hyperplanes), all **9 hyperplanes intersect at a single point**
- This unique intersection point is our solution vector in 9D space

Just as three non-parallel planes in 3D meet at a point, nine "generic" (non-parallel, independent) hyperplanes in 9D meet at exactly one point.

#### Column Picture in 9D

The column picture remains conceptually identical:

**Given:**
- Matrix **A** has 9 columns: **a**₁, **a**₂, …, **a**₉ (each is a 9D vector)
- Right-hand side vector **b** (also 9D)

**Find:** Coefficients x₁, x₂, …, x₉ such that: x₁·a₁ + x₂·a₂ + ⋯ + x₉·a₉ = b


We're looking for a **linear combination of nine 9D column vectors** that produces **b**. If one of the columns equals **b** exactly (as a₃ did in our 3D example), the solution is immediate.

#### Key Differences from 3D

| Aspect | 3D | 9D |
|--------|----|----|
| Geometric object per equation | 2D plane | 8D hyperplane |
| Intersection of 2 equations | Line (1D) | 7D hyperplane |
| Full system intersection | Point (unique solution) | Point (unique solution) |
| Visualization | Possible to sketch | Requires projection/abstraction |

#### Underdetermined Systems

If we have fewer than 9 equations in 9D, the intersection is a higher-dimensional subspace:
- **1 equation**: 8D hyperplane
- **2 equations**: 7D subspace (intersection of two 8D hyperplanes)
- **8 equations**: 1D line
- **k equations**: (9-k)-dimensional subspace

The geometric intuition remains: each additional constraint "slices" away one dimension until we reach a unique point (or determine the system has no solution).


---

### 4.5 When Does Solvability Fail?

**Singular matrix (columns linearly dependent):**

If the columns of A are linearly dependent, they do not span all of ℝᵐ. They span a lower-dimensional subspace (a plane, line, or point in higher dimensions).

**Example:**
```
A = ┌─     ─┐
    │  2  4 │
    │  1  2 │
    └─     ─┘
```

Column 2 = 2 × Column 1. Both columns point in the same direction. Their span is a line in 2D.

For this matrix:
- b = [1, 0.5]ᵀ is on the line (solution exists)
- b = [0, 1]ᵀ is not on the line (no solution)

**In 3D (three columns):**

If Column 3 = Column 1 + Column 2 (or any other linear dependence), then:
- The three columns span at most a 2D plane in 3D space
- Any b off this plane is unreachable
- The system is singular (not invertible)

---

### 4.6 Worked Example: 2D System

**Problem:** Solve
```
┌─     ─┐ ┌─   ─┐   ┌─   ─┐
│  3  1 │ │  x  │   │  5  │
│  1  2 │ │  y  │ = │  4  │
└─     ─┘ └─   ─┘   └─   ─┘
```

**Row picture approach:**
```
3x + y = 5      ⟹     y = 5 - 3x
x + 2y = 4      ⟹     y = (4 - x)/2
```

Setting them equal:
```
5 - 3x = (4 - x)/2
10 - 6x = 4 - x
6 = 5x
x = 6/5
```

```
y = 5 - 3·(6/5) = 5 - 18/5 = (25 - 18)/5 = 7/5
```

**Solution:** x = [6/5, 7/5]ᵀ

**Column picture approach:**
```
x·[3, 1]ᵀ + y·[1, 2]ᵀ = [5, 4]ᵀ
```

This gives:
```
3x + y = 5  and  x + 2y = 4
```

(Same equations as the row picture, so solving proceeds identically.)

---

## 5. Big Question

### What does it mean for Ax = b to have a solution?

**Algebraic answer:** The system has a solution if elimination (Gaussian elimination) succeeds—that is, we can reduce the augmented matrix [A | b] to row echelon form without encountering a contradiction (like 0 = 1).

**Geometric answer (the key insight):** The system Ax = b has a solution if and only if b lies in the **column space** of A; that is, b must be a linear combination of the columns of A.

```
b ∈ C(A) = span{a₁, a₂, …, aₙ}
```

### When does a system of equations fail?

A system fails (has no solution) when b is **not** in the column space of A.

**Row picture:** 
- 2D: Two parallel distinct lines have no intersection
- 3D: Three planes that do not share a common point (e.g., two planes intersect in a line, but the third plane misses that line)

**Column picture:** 
- The columns of A do not span enough of the space to reach b
- Equivalently, the matrix is **singular** (columns are linearly dependent) and b happens to lie outside the lower-dimensional subspace they span

**Example of failure:**
```
┌─     ─┐ ┌─   ─┐   ┌─   ─┐
│  1  1 │ │  x  │   │  1  │
│  2  2 │ │  y  │ = │  3  │
└─     ─┘ └─   ─┘   └─   ─┘
```

Both columns are proportional (column 2 = 2 × column 1). The column space is a line.

Row 2 is 2 × row 1, so we need 2·1 = 3, which is false. **No solution.**

### What does geometry tell us that algebra hides?

**Geometry reveals existence globally.** Algebra (elimination) is a step-by-step procedure; it doesn't immediately tell we whether a solution exists until we complete the process. 

**Geometry provides intuition:**
- In 2D, we can *see* whether two lines intersect
- In 3D, we can *visualize* whether planes meet
- For n dimensions, the column picture generalizes: Does b lie in the span of the columns?

**Deeper insight:** The column space and null space (which we'll study later) completely characterize the solution structure:
- If Ax₀ = b (particular solution) and Axₕ = 0 (homogeneous solution), then all solutions are x = x₀ + xₕ
- This is impossible to see from elimination alone until rows are manipulated

---

## 6. Important Questions

### Question 1: What is the column space of a matrix?

**Answer:** The column space of a matrix A, denoted C(A), is the set of all linear combinations of the columns of A:

```
C(A) = {Ax : x ∈ ℝⁿ}
```

It is a **subspace** of ℝᵐ (the space of the right-hand side b).

**Geometric intuition:** In 2D, if A has two linearly independent columns, C(A) = ℝ² (entire plane). If the columns are proportional, C(A) is a line.

**Example:**
```
A = ┌─     ─┐
    │  1  2 │
    │  0  0 │
    └─     ─┘
```
Columns: (1, 0) and (2, 0). Both lie on the x-axis, so C(A) = {(t, 0) : t ∈ ℝ}, a 1D line.

---

### Question 2: If planes do not intersect, what does that tell us about the system?

**Answer:** If three (or more) planes in 3D do not share a common point, the system of linear equations is **inconsistent** and has **no solution**.

**Row picture:** Inconsistency occurs when:
- Two planes are parallel and distinct (they never meet)
- Three planes are positioned so that their pairwise intersections don't form a common line/point

**Example:**
```
x + y + z = 1
x + y + z = 2
```
Both equations have the same left-hand side but different right-hand sides. Geometrically, these represent two parallel planes that don't intersect. **No solution.**

---

### Question 3: Can three equations in two unknowns have a solution?

**Answer:** **Yes, but it's "overdetermined."** A system with more equations than unknowns (m > n) may or may not have a solution.

**Row picture:** Three lines in 2D. For a solution to exist, all three lines must meet at a single point.

**Column picture:** We have two columns (each a 2D vector) and we want to write a 3D vector b as their linear combination. The two columns span at most a 2D subspace of ℝ³. For a solution to exist, b must lie in that subspace (a 2D plane inside 3D space).

**Example (solution exists):**
```
x + y = 3
2x + 2y = 6
x - y = 1
```
Solution: x = 2, y = 1. Check: 2 + 1 = 3 ✓, 4 + 2 = 6 ✓, 2 - 1 = 1 ✓

(Note: Equations 1 and 2 are redundant; effectively, we have two independent equations.)

**Example (no solution):**
```
x + y = 1
x + y = 2
2x + 2y = 3
```
No solution (inconsistent).

---

### Question 4: What does it mean for the columns of a matrix to be linearly dependent?

**Answer:** Columns are **linearly dependent** if there exist scalars c₁, c₂, …, cₙ (not all zero) such that:

```
c₁a₁ + c₂a₂ + ⋯ + cₙaₙ = 0
```

In other words, one column can be written as a linear combination of others.

**Implication:** The columns do not span all of ℝᵐ. For instance, if n = 3 and the columns are linearly dependent, they span at most a 2D plane, not all of ℝᵐ (if m ≥ 3).

**Example:**
```
┌─     ─┐
│  1  2 │
│  1  2 │
└─     ─┘
```
a₂ = 2a₁, so 2a₁ - a₂ = 0. The columns are linearly dependent.

**Consequence for solvability:** If columns are linearly dependent, the matrix is **singular** (not invertible). The system Ax = b either has no solution or infinitely many solutions, but never a unique solution.

---

### Question 5: What is the difference between the row picture and the column picture?

**Answer:**

| Aspect | Row Picture | Column Picture |
|--------|-----------|-----------------|
| **Focus** | One equation at a time | All equations simultaneously |
| **Geometric object** | Lines (2D), planes (3D), hyperplanes (nD) | Vectors and their linear combinations |
| **Intersection** | Points, lines, or planes where all equations are satisfied | The point where we find the right linear combination to reach b |
| **Visualization difficulty** | Easy in 2D, hard in 3D+, almost impossible in high dimensions | Less intuitive at first, but generalizes beautifully to high dimensions |
| **Advantage** | Familiar from elementary algebra | Reveals column space structure; critical for understanding solvability |
| **Weakness** | Doesn't scale to high dimensions | Harder to visualize in 3D without practice |

**Example (2×2 system):**
```
┌─      ─┐ ┌─   ─┐   ┌─   ─┐
│  2  -1 │ │  x  │   │  0  │
│ -1   2 │ │  y  │ = │  3  │
└─      ─┘ └─   ─┘   └─   ─┘
```

- **Row picture:** Two lines on a 2D graph; find their intersection at (1, 2)
- **Column picture:** Take 1 copy of [2, -1]ᵀ and 2 copies of [-1, 2]ᵀ; verify they sum to [0, 3]ᵀ

---

### Question 6: Is it always possible to solve Ax = b for every right-hand side b?

**Answer:** **No, not for singular matrices.** Only for non-singular (invertible) matrices does every b have a unique solution.

**Criterion:** Ax = b has a solution for every b if and only if the columns of A span all of ℝᵐ and A is square (m = n). In that case, A is non-singular and invertible.

**Non-singular matrix (good case):**
```
A = ┌─     ─┐
    │  1  0 │
    │  0  1 │
    └─     ─┘
⟹ C(A) = ℝ², all b solvable
```

**Singular matrix (problematic case):**
```
A = ┌─     ─┐
    │  1  2 │
    │  1  2 │
    └─     ─┘
⟹ C(A) = a 1D line, only some b solvable
```
- If the columns are **independent**, they span the entire \( n \)-dimensional space ℝⁿ.
  Then **yes**, for any \( b \), there is a solution.

- If the columns are **dependent (singular)**, they lie on a flat surface  
  (a **plane** or **line**) inside the larger space.

- In this case, we can only solve for \( b \) **if \( b \) lies on that plane**.

- If \( b \) sticks out of the plane, the system is **inconsistent**  
  (no solution).

### Geometry vs Algebra
- **Algebra** hides the issue in errors like *“divide by zero”* or *“\( 0 = 1 \)”*.
- **Geometry** shows the real reason: the vectors are *flat* and cannot reach the target.

---

### Question 7: In high dimensions, how do you check if a system is solvable without elimination?

**Answer:** Theoretically, check if b ∈ C(A). Practically, you must perform elimination (Gaussian elimination) to find the row echelon form and check for contradictions.

However, the **column picture** provides intuition: If the columns are linearly independent, almost any b is reachable. If the columns are dependent, some b will be unreachable.

**Numerical test:** Compute the rank of A and the rank of the augmented matrix [A | b]:
- If rank(A) = rank([A | b]) = n (number of unknowns), then a unique solution exists
- If rank(A) = rank([A | b]) < n, then infinitely many solutions exist
- If rank(A) < rank([A | b]), then no solution exists

---

### Question 8: What is the geometric meaning of a non-singular matrix?

**Answer:** A non-singular (invertible) matrix A is one whose columns are **linearly independent** and span all of ℝᵐ (in the square case, m = n).

**Geometrically:**
- In 2D: Two non-singular columns point in different directions; their spans fill the entire plane
- In 3D: Three non-singular columns point in different directions (not coplanar); their spans fill all of 3D space
- In general: n non-singular columns in ℝⁿ span all of ℝⁿ

**Consequence:** For any b ∈ ℝⁿ, there exists a unique x such that Ax = b.

**Example:**
```
A = ┌─     ─┐
    │  2  1 │
    │  1  3 │
    └─     ─┘
```
Columns (2, 1) and (1, 3) are not proportional (linearly independent), so A is non-singular. For any b, Ax = b has a unique solution.

---

## 7. Top-5 Interview Questions

### 1. Explain the column space of a matrix and why it matters for solvability.

**Answer:** 
The column space of A is the span of its columns—all vectors obtainable as Ax. The system Ax = b has a solution if and only if b lies in the column space. This is the fundamental solvability criterion. If the columns are linearly independent, the column space spans all of ℝᵐ, so every b is reachable. If the columns are dependent, the column space is lower-dimensional, so some b values are unreachable. In machine learning, the rank (dimension of column space) determines whether a least-squares problem has a unique solution.

---

### 2. You have a system with more equations than unknowns. When does it have a solution?

**Answer:** 
Such an **overdetermined system** (more rows than columns) has a solution only if the right-hand side b lies in the column space of A. Geometrically, if we have m equations in n unknowns with m > n, the columns span at most an n-dimensional subspace of ℝᵐ. For a solution to exist, b must lie in that subspace. If it doesn't, the system is inconsistent. In practice, no exact solution exists; we find a least-squares approximation instead.

---

### 3. Differentiate between singular and non-singular matrices in terms of solvability.

**Answer:** 

| Property | Non-singular | Singular |
|----------|--------------|----------|
| **Columns** | Linearly independent | Linearly dependent |
| **Determinant** | Non-zero | Zero |
| **Invertibility** | A⁻¹ exists | No inverse |
| **Ax = b solution** | Unique solution for all b | 0 or infinitely many solutions |
| **Column space** | Entire ℝⁿ (for square A) | Proper subspace of ℝⁿ |

A non-singular matrix guarantees a unique solution for every right-hand side. A singular matrix fails for some b—either no solution or infinitely many.

---

### 4. How does the row picture relate to the column picture geometrically?

**Answer:** 
The row picture and column picture are two views of the same system. The row picture plots one constraint at a time (lines, planes); the solution is their intersection. The column picture asks: "What linear combination of columns produces b?" Algebraically equivalent, but geometrically distinct. The row picture fails to scale beyond 3D; the column picture generalizes naturally to high dimensions. In practice, we solve using elimination (row operations), but we interpret solvability via the column picture.

---

### 5. In a machine learning context, why do we care about the column space and rank of the design matrix?

**Answer:** 
In regression, we have n features (columns of the design matrix A) and m samples (rows). If the features are linearly dependent (e.g., one feature is a linear combination of others), A is rank-deficient, and the normal equations AᵀA x = Aᵀb have infinitely many solutions (the features don't uniquely determine the target). Conversely, if features are independent, the system has a unique solution. High multicollinearity (near-dependence) makes the solution numerically unstable. Understanding rank and column space is critical for feature engineering and diagnosing model issues.

### 6: Can 3 equations in 2 unknowns have a solution?

**Answer:**
- **Generally, no.**

**Row Picture:**  
Three lines in a 2D plane usually form a triangle and do not share a single common point.

**Condition for a solution:**  
A solution exists only if the third line passes **exactly through** the intersection of the first two.  
This requires the vector 'b' to be a **linear combination of the columns** of the 3×2 matrix A.

### 7: How do you conceptually multiply a matrix by a vector?

**Answer:**  
Do **not** think of rows. Think of **columns**.

A x = x₁(col₁) + x₂(col₂) + … + xₙ(colₙ)

The result is a **weighted sum of the columns** of A.

### 8: What is a **singular matrix**?

**Answer:**  
A square matrix whose columns are **not linearly independent**.  
Geometrically, the columns lie in a **lower-dimensional space**  
(e.g., three vectors lying on a 2D plane).

- Determinant = **0**
- Matrix is **not invertible**

### 9: If Ax = 0, what is the **trivial solution**?

**Answer:**  
The solution is always x = 0 (the zero vector).

- Every linear space passes through the **origin**.
- If A is **non-singular**, this is the **only** solution.
- If A is **singular**, there are **non-zero solutions**  
  (vectors in the **null space**).

### 10: What does it mean for a system to be **linear**?

**Answer:**  
Variables are only multiplied by constants and added.  
Geometrically, linear systems preserve lines and planes  
(planes don’t curve).

### 11: Why is **Linear Algebra** important for **Machine Learning**?

**Answer:**  
ML models represent data as **vectors** and transformations as **matrices**.  
Understanding column spaces helps with:
- Dimensionality reduction
- Feature independence

### 12: If I have a 3×3 matrix and **Col₃ = Col₁ + Col₂**, is it invertible?

**Answer:**  
No. The columns are **dependent**.  
The column space is only a **2D plane** in 3D space.  
The matrix is **singular**.

---

### 13: Interpret Ax = b physically.

**Answer:**  
If columns of A are **movement directions** and x is  
“how far to move,” then Ax = b asks:
> *How far do I move in each direction to arrive at location b?*


---

## 8. Interview Summary

What an interviewer expects you to know about Lecture 1:

- **Matrix–Vector multiplication** is a *linear combination of columns*.
- The difference between **\( n \) equations in \( n \) unknowns** vs. **\( m \) equations in \( n \) unknowns**.
- **Geometric visualization of singular matrices**  
  (e.g., planes collapsing to a line or a plane).
- **Terminology**:
  - Linear Combination  
  - Span  
  - Independence  
  - Singular
- The ability to **switch mentally** between:
  - *Solving equations*  
  - *Adding vectors*
- The system **\( Ax = 0 \)** always has the **trivial solution** \( x = 0 \).
- For a random vector **\( b \)**, a **singular matrix \( A \)** usually has **no solution**.

> **Don’t just do the algebra — visualize the space.**


1. **Matrix form Ax = b:** Understand the structure: A is the coefficient matrix, x is the unknown vector, b is the right-hand side. Be able to write a system of equations in matrix form and vice versa.

2. **Row picture:** Interpret each equation as a geometric object (line in 2D, plane in 3D). The solution is the intersection point. Know why this fails to visualize in higher dimensions.

3. **Column picture ★ (most important):** Ax is a linear combination of the columns of A. The system has a solution if and only if b is in the column space. This is the fundamental solvability insight.

4. **Linear combination:** A weighted sum of vectors. The entire left-hand side of Ax = b is a linear combination of columns, and x gives the weights.

5. **Column space:** The span of the columns of A; the set of all achievable right-hand sides. Solvability: b ∈ C(A) ⟺ solution exists.

6. **Linear dependence:** Columns are dependent if one is a linear combination of others (or if a non-trivial combination equals zero). Dependent columns mean A is singular, and not all b are reachable.

7. **Non-singular vs. singular:** Non-singular = columns independent = all b solvable. Singular = columns dependent = some b unsolvable.

8. **When systems fail:** A system is inconsistent (no solution) when b is not in the column space. The row picture shows this as non-intersecting geometric objects; the column picture shows it as b lying outside the column space.

9. **Geometry reveals structure:** Unlike elimination, which is a black-box algorithm, geometry immediately shows why a system is solvable or not. A line parallel to another line shows inconsistency visually; a dependent column shows it algebraically.

10. **Scalability:** The column picture scales to arbitrary dimensions via linear algebra; the row picture does not. Always think in terms of column combinations for high-dimensional problems.

---

## 9. Summary

**Lecture 1: The Geometry of Linear Equations**

The fundamental problem of linear algebra is to solve Ax = b. This lecture introduces two complementary geometric interpretations:

**Row Picture:** Plot each equation as a geometric object (line, plane, hyperplane). The solution is their intersection. Intuitive in low dimensions but fails to generalize.

**Column Picture ★:** Interpret Ax as a linear combination of the columns of A. The unknowns x are the weights. The system has a solution if and only if b lies in the column space C(A)—the span of the columns.

**Key Concepts:**
- Ax = b is solvable ⟺ b ∈ C(A)
- Non-singular matrix: columns span all of ℝⁿ ⟹ unique solution for all b
- Singular matrix: columns span a proper subspace ⟹ some b have no solution, others have infinitely many
- Linear dependence of columns ⟹ matrix is singular

**Key Formulas:**
```
Ax = x₁a₁ + x₂a₂ + ⋯ + xₙaₙ = b

C(A) = {Ax : x ∈ ℝⁿ}
```

**Big Insights:**
1. Matrix multiplication is a linear combination of columns, not just algebra
2. Solvability is geometric: Does b lie in the column space?
3. The column picture generalizes to any dimension; the row picture does not
4. Rank, column space, and linear dependence are the bedrock concepts for all of linear algebra

---

## 10. Additional

### MIT OpenCourseWare (Official Course Materials)
- **Full course:** http://ocw.mit.edu/18-06S05
- **Lecture 1 video:** https://www.youtube.com/watch?v=ZK3O402wf1c (39:49)
- **Course syllabus, problem sets, exams:** http://ocw.mit.edu/18-06S05

### Textbooks
**Strang, G.** (2016). *Introduction to Linear Algebra* (5th ed.). Wellesley-Cambridge Press.
   - The official course text; clear, geometric exposition

### Problem Sets & Practice
- **MIT OCW Problem Sets:** http://ocw.mit.edu/18-06S05

### Computational Platforms
- **Python (NumPy/SciPy):** `np.linalg.solve()` for systems, `np.linalg.matrix_rank()` for rank computation
- **Mathematica/Wolfram Language:** Symbolic and numerical computation

---

### Key Takeaways for Further Study

1. **Master the column picture:** It is the foundation for understanding rank, null space, linear independence, and all core linear algebra concepts.
2. **Connect geometry and algebra:** Elimination (Lecture 2) is the algorithmic procedure; geometry is the conceptual framework.
3. **Generalize to n dimensions:** Even though you cannot draw in 9D, the principles (column space, span, linear combinations) are identical.
4. **Recognize solvability patterns:** Before computing, ask: Are the columns independent? Does the matrix have full rank? Is b in the column space?
5. **Applications abound:** Optimization, machine learning, differential equations, network analysis, and finance all reduce to solving Ax = b variants.

---
