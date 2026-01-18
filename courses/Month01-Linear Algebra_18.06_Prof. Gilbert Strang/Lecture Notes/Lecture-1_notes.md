# Lecture 1: The Geometry of Linear Equations

**Instructor:** Gilbert Strang  
**Course:** MIT 18.06 Linear Algebra  
**Lecture:** 1  
**Topic:** The Geometry of Linear Equations  
**Video:** [Watch on YouTube](https://www.youtube.com/watch?v=ZK3O402wf1c)  
**Course Page:** [web.mit.edu/18.06](http://web.mit.edu/18.06)

---

## Table of Contents
- [Overview](#overview)
- [The Fundamental Problem](#the-fundamental-problem)
- [Three Perspectives on Linear Systems](#three-perspectives-on-linear-systems)
  - [Row Picture](#row-picture)
  - [Column Picture](#column-picture)
  - [Matrix Form](#matrix-form)
- [2x2 System Example](#2x2-system-example)
- [3x3 System Example](#3x3-system-example)
- [Matrix-Vector Multiplication](#matrix-vector-multiplication)
- [Key Concepts](#key-concepts)
- [Important Questions](#important-questions)

---

## Overview

The fundamental problem of linear algebra is to **solve systems of linear equations**. This lecture introduces three different ways to visualize and understand systems of linear equations:

1. **Row Picture** - One equation at a time (geometric view)
2. **Column Picture** - Linear combinations of column vectors (most important)
3. **Matrix Form** - Compact algebraic representation

We start with n equations and n unknowns (square system).

---

## The Fundamental Problem

Given a system of linear equations, find the values of unknowns that satisfy all equations simultaneously.

**Standard Form:**
```
a₁₁x₁ + a₁₂x₂ + ⋯ + a₁ₙxₙ = b₁  
a₂₁x₁ + a₂₂x₂ + ⋯ + a₂ₙxₙ = b₂  
⋮  
aₙ₁x₁ + aₙ₂x₂ + ⋯ + aₙₙxₙ = bₙ
```
---

## Three Perspectives on Linear Systems

### Row Picture

**Geometric interpretation:** Each equation represents a geometric object
- In 2D: each equation is a **line**
- In 3D: each equation is a **plane**
- In nD: each equation is a **hyperplane**

**Solution:** The point(s) where all geometric objects intersect.

### Column Picture

**Key Concept:** View the system as a **linear combination** of column vectors.

**Linear Combination:** Taking vectors and multiplying each by a scalar, then adding them together.

```
x₁ (column 1) + x₂ (column 2) + ⋯ + xₙ (column n) = b
```

This is the **most fundamental operation** in linear algebra!

**Question to ask:** What combination of the column vectors produces the right-hand side vector b?

### Matrix Form

Compact representation: **Ax = b**

Where:
- **A** = coefficient matrix (m × n)
- **x** = vector of unknowns (n × 1)
- **b** = right-hand side vector (m × 1)

---

## 2x2 System Example

### Problem Setup

```
2x - y = 0
-x + 2y = 3
```

**Coefficient Matrix A:**
```
A = [ 2  -1]
    [-1   2]
```

**Unknown Vector x:**
```
x = [x]
    [y]
```

**Right-hand Side b:**
```
b = [0]
    [3]
```

**Matrix Form:** Ax = b

### Row Picture (2D)

**Equation 1:** 2x - y = 0  
- Passes through origin (0, 0) 
- Another point: (1, 2) 
- This is a **line** through these points  

**Equation 2:** -x + 2y = 3  
- When y = 0: x = -3 → point (-3, 0)  
- When x = -1: y = 1 → point (-1, 1)  
- This is a **line** through these points  

**Solution:** Where the two lines intersect → **(x, y) = (1, 2)**  

**Verification:**  
- Equation 1: 2(1) - 2 = 0 
- Equation 2: -1 + 2(2) = 3

### Column Picture (2D) 

Rewrite as linear combination:
```
x[2 ] + y[-1] = [0]
 [-1]    [2 ]   [3]
```

**Interpretation:** 
- Find scalars x and y such that x times column 1 plus y times column 2 equals b

**Geometric View:**
- Column 1: vector (2, -1)
- Column 2: vector (-1, 2)
- Goal: Combine these to get (0, 3)

**Solution Process:**
1. Take 1 of column 1: (2, -1)
2. Add 2 of column 2: 2(-1, 2) = (-2, 4)
3. Result: (2, -1) + (-2, 4) = (0, 3) 

**Answer:** x = 1, y = 2

**Important Question:** Can we solve for **every** right-hand side b?

**Answer for this 2×2 case:** YES!  
All linear combinations of these two vectors fill the entire 2D plane.

---

## 3x3 System Example

### Problem Setup

```
2x - y     = 0
-x + 2y - z = -1
   - 3y + 4z = 4
```

**Matrix Form:**
```
A = [ 2  -1   0]     x = [x]     b = [ 0]
    [-1   2  -1]         [y]         [-1]
    [ 0  -3   4]         [z]         [ 4]
```

### Row Picture (3D)

**Each equation represents a plane in 3D space**

**Equation 1:** 2x - y = 0
- A plane through origin
- Points: (0,0,0), (1,2,0), (0,0,1)

**Equation 2:** -x + 2y - z = -1
- Another plane
- Points: (1,0,0), (0,-1/2,0), (0,0,1)

**Equation 3:** -3y + 4z = 4
- Third plane
- Points: (0,-4/3,0), (0,0,1), (any x, -4/3, 0)

**Solution:** The single point where all three planes meet

### Column Picture (3D)

```
x[ 2] + y[-1] + z[ 0] = [ 0]
 [-1]    [ 2]    [-1]   [-1]
 [ 0]    [-3]    [ 4]   [ 4]
```

**Geometric View:**
- Three vectors in 3D space
- Find combination that produces b

**Special Case in This Example:**
- Notice b = (0, -1, 4) is exactly column 3!
- Solution: x = 0, y = 0, z = 1

### Alternative Right-hand Side

**New b = (1, 1, -3)** (sum of columns 1 and 2)

Solution becomes: **x = 1, y = 1, z = 0**

This shows: 1(column 1) + 1(column 2) + 0(column 3) = new b

### Big Question: Can We Solve for All b?

**Question:** Do the linear combinations of the three columns fill all of 3D space?

**Answer for this matrix:** YES! This is a **non-singular** (invertible) matrix.

**When would the answer be NO?**
- If all three columns lie in the same plane
- Example: column 3 = column 1 + column 2 (dependent columns)
- Then combinations only fill a **plane**, not all of 3D space
- Such matrices are **singular** (not invertible)

---

## Matrix-Vector Multiplication

**How to multiply a matrix A by a vector x?**

### Example:
```
[2  5] [1]   = ?
[1  3] [2]
```

### Method 1: Linear Combination of Columns (Preferred)

**Think:** 1 × (column 1) + 2 × (column 2)

```
1[2] + 2[5] = [2 + 10] = [12]
 [1]    [3]   [1 + 6 ]   [7 ]
```

**Key Insight:** Ax is a **linear combination of the columns of A**

### Method 2: Dot Product of Rows

**Think:** Each row dots with x

```
Row 1 · x = [2  5] · [1] = 2(1) + 5(2) = 12  
                     [2]  

Row 2 · x = [1  3] · [1] = 1(1) + 3(2) = 7  
                     [2]
```

Result: **[12, 7]**

### General Form

**For Ax = b:**
```
A·x = x₁ (column 1) + x₂ (column 2) + ⋯ + xₙ (column n) = b
```

This is the **fundamental way** to think about matrix-vector multiplication!

---

## Key Concepts

### 1. Linear Combination (Definition)

**Definition:** Given vectors v₁, v₂, …, vₙ ∈ ℝᵐ and scalars c₁, c₂, …, cₙ ∈ ℝ, a **linear combination** is:

c₁v₁ + c₂v₂ + ⋯ + cₙvₙ = Σᵢ₌₁ⁿ cᵢvᵢ

**Properties:**
- Result is a vector in ℝᵐ (same space as original vectors)
- Scalars can be any real numbers (positive, negative, zero)
- Order doesn't matter (commutative)

---

### 2. Span (All Linear Combinations)

**Definition:** The **span** of vectors {v₁, v₂, …, vₙ} is the set of ALL possible linear combinations:

span{v₁, …, vₙ} = { Σᵢ₌₁ⁿ cᵢvᵢ | cᵢ ∈ ℝ }

**Key Question:**  
What is span{c₁, c₂, …, cₙ}?

**Examples:**

**2D Case:**

span{ [2, -1]ᵀ , [-1, 2]ᵀ } = ℝ²  
(entire 2D plane)

**Why?**  
These two vectors are not parallel (linearly independent), so their combinations fill all of ℝ².

**3D Case:**

span{ [2, -1, 0]ᵀ , [-1, 2, -3]ᵀ , [0, -1, 4]ᵀ } = ℝ³  
(entire 3D space)

**Why?**  
These three vectors are linearly independent, so they span all of ℝ³.

---

### 3. Linear Independence

**Definition:** Vectors v₁, …, vₙ are **linearly independent** if:

c₁v₁ + c₂v₂ + ⋯ + cₙvₙ = 0  
⇒ c₁ = c₂ = ⋯ = cₙ = 0

**In words:**  
The ONLY way to make the zero vector is with all zero coefficients.

**Equivalently:**  
No vector can be written as a linear combination of the others.

**Examples:**

**Independent:**  
[1, 0]ᵀ , [0, 1]ᵀ  
(standard basis vectors)

**Dependent:**  
[1, 2]ᵀ , [2, 4]ᵀ  
(second = 2 × first)

---

### 4. Column Space

**Definition:** The **column space** of matrix A, denoted C(A), is the span of its columns:

C(A) = span{a₁, a₂, …, aₙ}

where aᵢ are the columns of A.

**Significance:**  
C(A) is the set of all vectors b such that:

A·x = b  

has a solution.


### 5. Solvability
**Question:** Can we solve Ax = b for every right-hand side b?

**Depends on the columns of A:**
- If columns are **independent**: YES (non-singular, invertible)
- If columns are **dependent**: NO (singular, not invertible)

#### Central Question

**Can we solve** A·x = b **for every** b?

---

#### Case 1: Non-Singular (Invertible) Matrix 

**Conditions (all equivalent):**
1. Columns of A are **linearly independent**
2. Columns span ℝⁿ (full space)
3. C(A) = ℝⁿ
4. Matrix A has **full rank** (rank = n)
5. det(A) ≠ 0
6. A is **invertible**

**Result:**

For **EVERY** b ∈ ℝⁿ,  
A·x = b has a **UNIQUE solution**

**Example:** Matrix from Examples 1 and 2

A =
[ 2  -1   0  
 -1   2  -1  
  0  -3   4 ]

is non-singular (columns are independent).

---

#### Case 2: Singular Matrix 

**Conditions:**
1. Columns of A are **linearly dependent**
2. At least one column is a combination of others
3. Columns do NOT span ℝⁿ
4. C(A) ⊊ ℝⁿ (proper subset)
5. Rank < n
6. det(A) = 0

**Result:**

A·x = b has a solution  
**ONLY when** b ∈ C(A)

**Most** b values → **no solution** exists!

---

#### Example of Singular System (3D)

**Scenario:** Third column = first column + second column

A =
[ 1   0   1  
  0   1   1  
  0   0   0 ]

**Analysis:**
- Column 3 = Column 1 + Column 2
- Third column gives **no new information**
- All combinations:

c₁c₁ + c₂c₂ + c₃(c₁ + c₂)  
= (c₁ + c₃)c₁ + (c₂ + c₃)c₂

- Only 2 independent columns  
→ span a **plane** in ℝ³

**Solvability:**
- Can solve for b **in the plane**
- Cannot solve for b **outside the plane**

**Geometric picture:**  
Column space C(A) is a **2D plane** in 3D space.

---

#### Test for Solvability

**Method 1:** Check if b ∈ C(A)
- Can b be written as linear combination of columns?

**Method 2:** Use elimination
- If elimination succeeds → solvable
- If get 0 = nonzero → not solvable

**Method 3:** Check rank
- If rank(A) = n → solvable for all b
- If rank(A) < n → solvable only for some b

---

#### Higher Dimensions (n × n systems)

**9 × 9 Example:**
- 9 equations, 9 unknowns
- 9 columns, each a vector in 9D space
- If columns are independent: combinations fill all of 9D space
- If column 9 = column 8: combinations fill only an 8D "plane" in 9D space

---

### Comparison of Methods

| Aspect | Column Method | Row Method |
|--------|---------------|------------|
| **Viewpoint** | Linear combinations | Dot products |
| **Conceptual** | Modern, preferred by Strang | Traditional |
| **Connects to** | Span, column space | Individual equations |
| **Best for** | Understanding structure | Quick calculation |
| **Generalizes** | Excellently to higher dimensions | Less intuitive in high-D |

**Both methods give the same answer!**

---

## Quick Reference

### Notation
- **A**: m × n matrix (m rows, n columns)
- **x**: n × 1 column vector (unknowns)
- **b**: m × 1 column vector (right-hand side)
- **aᵢ**: i-th column of A
- **rᵢ**: i-th row of A

### Key Formulas

**System of Equations:**  
A·x = b

**Column Picture:**  
x₁a₁ + x₂a₂ + ⋯ + xₙaₙ = b

**Linear Combination:**  
c₁v₁ + c₂v₂ + ⋯ + cₙvₙ

**Span:**  
span{v₁, … , vₙ} = { c₁v₁ + ⋯ + cₙvₙ | cᵢ ∈ ℝ }

**Linear Independence:**  
c₁v₁ + ⋯ + cₙvₙ = 0 ⇒ c₁ = ⋯ = cₙ = 0

**Column Space:**  
C(A) = span{columns of A}

---

### Fundamental Operations

**Linear Combination:**  
c₁v₁ + c₂v₂ + ⋯ + cₙvₙ  
→ Most important operation in linear algebra!

**Matrix-Vector Product:**  
A·x = x₁a₁ + x₂a₂ + ⋯ + xₙaₙ  
→ View as linear combination of columns!

#### 3. Solvability Condition

A·x = b is solvable for all b  
⇔ columns of A are linearly independent

---

### Key Terms

| Term | Meaning |
|------|---------|
| **Linear combination** | Weighted sum of vectors |
| **Span** | All possible linear combinations |
| **Linearly independent** | No vector is a combination of others |
| **Column space** | Span of columns of a matrix |
| **Non-singular** | Invertible, full rank, det ≠ 0 |
| **Singular** | Not invertible, dependent columns |
| **Solvable** | 𝒃 is in the column space |

---

## Higher Dimensions

### 9-Dimensional Example

**System:** 9 equations, 9 unknowns

A·x = b,   A ∈ ℝ⁹ˣ⁹,   x, b ∈ ℝ⁹

**Column Picture:**  
x₁c₁ + x₂c₂ + ⋯ + x₉c₉ = b

where each cᵢ ∈ ℝ⁹ (9-component vectors).

---

### Visualization Challenge

**Can't draw 9D space!** But we can think about it abstractly:

**Good Case (Non-singular):**
- 9 linearly independent vectors in ℝ⁹
- Their combinations **fill all of** ℝ⁹
- Can reach **any** b ∈ ℝ⁹
- Solution exists for **every** right-hand side

**Bad Case (Singular):**
- Example: 9th column = 8th column
- Only 8 independent columns
- Combinations fill an **8-dimensional hyperplane** in ℝ⁹
- Can reach only b in this hyperplane
- Most b values → no solution

---

### Random Matrices

**Fact:** Random n × n matrix is non-singular with probability 1.

**PYTHON Example:**
```python
import numpy as np

A = np.random.rand(9, 9)  # Almost certainly invertible
```

---

## Important Questions

### Q1: What are the three pictures of linear systems?
- **Row Picture:** Geometric objects (lines, planes, hyperplanes) intersecting
- **Column Picture:** Linear combinations of column vectors
- **Matrix Form:** Ax = b

### Q2: What is a linear combination?
Multiplying vectors by scalars and adding them:
```
c₁v₁ + c₂v₂ + ⋯ + cₙvₙ
```

### Q3: What does Ax represent geometrically?
A **linear combination** of the columns of A, with weights given by components of x.

### Q4: When can we solve Ax = b for all b?
**Equivalent Questions:**
- Do the columns of A span the entire space?
- Are the columns linearly independent?
- Is A invertible (non-singular)?

**Answer:**
- **YES** — If columns are linearly independent  
  → They span the entire space  
  → A is invertible  
  → Unique solution exists for every 𝒃  

- **NO** — If columns are linearly dependent  
  → They do NOT span the space  
  → A is singular  
  → No solution for some 𝒃


### Q5: What makes a matrix singular?
When its columns are **linearly dependent** - some column can be written as a combination of others.

### Q6: Why is the column picture important?
It reveals the **fundamental structure** of linear systems and helps understand:
- When solutions exist
- The span of vectors
- Linear independence
- Vector spaces (coming in future lectures)

### Q7: When is there no solution for some 𝒃?

**Answer:**
There is **no solution** when:

- Columns of A lie in the **same plane** (in 3D)
- All linear combinations stay **inside that plane**
- Any 𝒃 **outside the plane** cannot be reached
- Therefore, system becomes **inconsistent**

**Conclusion:**  
No solution exists for those 𝒃 outside the column space.

---

## Top 5 Interview Questions


### 1. What are the three ways to view a linear system Ax = b?

### Question  
Explain the **row picture, column picture, and matrix picture**. When is each useful?

### Answer  

**Row picture**
- Each row = one equation  
- 2D → line, 3D → plane  
- Solution = intersection point  
- Best for visualization in low dimensions  

**Column picture (most important)**
- Columns of A are vectors  
- Solve:  
  x₁a₁ + x₂a₂ + ⋯ + xₙaₙ = b  
- Key question: *Is b in span of columns?*  
- Best for theory, ML, and high dimensions  

**Matrix picture**
- Compact form: Ax = b  
- Used for computation (elimination, algorithms)

---

### 2. Solve a 2×2 system using column picture

### Question  
Solve:

2x − y = 0  
−x + 2y = 3  

### Solution  

Column form:

x[2, −1]ᵀ + y[−1, 2]ᵀ = [0, 3]ᵀ  

From equations:

2x − y = 0 → y = 2x  
−x + 2(2x) = 3  
3x = 3 → x = 1  
y = 2  

**Answer:**  
x = 1, y = 2  

**Geometric meaning:**  
1 copy of column1 + 2 copies of column2 = b

---

### 3. When does Ax = b have a unique solution for all b?

### Question  
Give conditions for solvability for every b.

### Answer  

All are equivalent:

- Columns span ℝⁿ  
- Columns are linearly independent  
- rank(A) = n  
- det(A) ≠ 0  
- A is invertible  
- Unique solution for every b  

**Interpretation:**  
Column space = ℝⁿ → every b is reachable

---

### 4. When does Ax = b have no solution?

### Question  
Give a geometric condition and example.

### Answer  

**Condition**
- Columns lie in lower dimension (line/plane)  
- Column space ≠ ℝⁿ  
- Some b lie outside → no solution  

**Example**

A =[1  2  
    2  4]

Column2 = 2 × column1 → dependent  
Column space = line  

Choose  
b = [3, 7]ᵀ  

Line requires y = 2x  
But 7 ≠ 6 → outside column space  

**Result:**  
No solution exists

---

### 5. What does matrix–vector multiplication Ax mean?

### Question  
Give two interpretations.

### Answer  

### (1) Column interpretation

If A = [a₁ a₂ … aₙ], then:

Ax = x₁a₁ + x₂a₂ + ⋯ + xₙaₙ  

→ Linear combination of columns  
→ Core idea in linear algebra & ML  

### (2) Row interpretation

Each entry:

(Ax)ᵢ = rowᵢ · x  

→ Dot product with rows  
→ Plugging into equations  

**Why column view matters**
- Explains span, rank, solvability  
- Scales to high dimensions  
- Foundation of ML models

---

### Interview Summary

| Concept | Key Insight |
|--------|-------------|
| Ax = b | Linear combination problem |
| Solvable for all b | Columns span ℝⁿ |
| No solution | b outside column space |
| Unique solution | Independent columns |
| Ax meaning | Column combinations |

---

## Summary

This lecture introduced the **geometric intuition** behind linear systems:

1. **Row picture:** intersecting geometric objects
2. **Column picture:** combinations of column vectors (most important)
3. **Matrix form:** compact Ax = b notation

**Central Question:** What combinations of column vectors can we produce?

---

## Additional Resources

- **Course Textbook:** *Introduction to Linear Algebra* by Gilbert Strang
- **Course Website:** [web.mit.edu/18.06](http://web.mit.edu/18.06)
- **MIT OCW:** [ocw.mit.edu/18-06S05](http://ocw.mit.edu/18-06S05)
- **Video Lecture:** [MIT OpenCourseWare YouTube](https://www.youtube.com/watch?v=ZK3O402wf1c)

---
