# MIT 18.06 Linear Algebra - Lecture 1: The Geometry of Linear Equations

**Instructor:** Gilbert Strang  
**Course:** MIT 18.06 Linear Algebra, Spring 2005  
**Lecture:** 1 of 34  
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
- [Questions for Understanding](#questions-for-understanding)

---

## Overview

The fundamental problem of linear algebra is to **solve systems of linear equations**. This lecture introduces three different ways to visualize and understand systems of linear equations:

1. **Row Picture** - One equation at a time (geometric view)
2. **Column Picture** - Linear combinations of column vectors â­ (most important)
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

### Method 1: Linear Combination of Columns â­ (Preferred)

**Think:** 1 × (column 1) + 2 × (column 2)

```
1[2] + 2[5] = [2 + 10] = [12]
 [1]    [3]   [1 + 6 ]   [7 ]
```

**Key Insight:** Ax is a **linear combination of the columns of A**

### Method 2: Dot Product of Rows

**Think:** Each row dots with x

```
Row 1 Â· x = [2  5] Â· [1] = 2(1) + 5(2) = 12
                     [2]

Row 2 Â· x = [1  3] Â· [1] = 1(1) + 3(2) = 7
                     [2]
```

Result: **[12, 7]áµ€**

### General Form

**For Ax = b:**
```
AÂ·x = xâ‚(column 1) + xâ‚‚(column 2) + ... + xâ‚™(column n) = b
```

This is the **fundamental way** to think about matrix-vector multiplication!

---

## Key Concepts

### Linear Combination
The **most fundamental operation** in linear algebra:
```
câ‚vâ‚ + câ‚‚vâ‚‚ + ... + câ‚™vâ‚™
```
where câ‚, câ‚‚, ..., câ‚™ are scalars and vâ‚, vâ‚‚, ..., vâ‚™ are vectors.

### Solvability
**Question:** Can we solve Ax = b for every right-hand side b?

**Depends on the columns of A:**
- If columns are **independent**: YES (non-singular, invertible)
- If columns are **dependent**: NO (singular, not invertible)

### Independence vs Dependence

**Independent columns:**
- Do not lie in the same lower-dimensional subspace
- Their combinations fill the entire space
- Matrix is invertible

**Dependent columns:**
- One or more columns can be written as combinations of others
- Their combinations fill only a subspace
- Matrix is singular

### Higher Dimensions (n Ã— n systems)

**9Ã—9 Example:**
- 9 equations, 9 unknowns
- 9 columns, each a vector in 9D space
- If columns are independent: combinations fill all of 9D space
- If column 9 = column 8: combinations fill only an 8D "plane" in 9D space

---

## Questions for Understanding

### Q1: What are the three pictures of linear systems?
- **Row Picture:** Geometric objects (lines, planes, hyperplanes) intersecting
- **Column Picture:** Linear combinations of column vectors
- **Matrix Form:** Ax = b

### Q2: What is a linear combination?
Multiplying vectors by scalars and adding them:
```
câ‚vâ‚ + câ‚‚vâ‚‚ + ... + câ‚™vâ‚™
```

### Q3: What does Ax represent geometrically?
A **linear combination** of the columns of A, with weights given by components of x.

### Q4: When can we solve Ax = b for all b?
When the columns of A are **linearly independent** (span the entire space).

### Q5: What makes a matrix singular?
When its columns are **linearly dependent** - some column can be written as a combination of others.

### Q6: Why is the column picture important?
It reveals the **fundamental structure** of linear systems and helps understand:
- When solutions exist
- The span of vectors
- Linear independence
- Vector spaces (coming in future lectures)

---

## Summary

This lecture introduced the **geometric intuition** behind linear systems:

1. **Row picture:** intersecting geometric objects
2. **Column picture:** combinations of column vectors (â­ most important)
3. **Matrix form:** compact Ax = b notation

**Central Question:** What combinations of column vectors can we produce?

**Next Step:** Systematic elimination method to solve any linear system.

---

## Additional Resources

- **Course Textbook:** *Introduction to Linear Algebra* by Gilbert Strang
- **Course Website:** [web.mit.edu/18.06](http://web.mit.edu/18.06)
- **MIT OCW:** [ocw.mit.edu/18-06S05](http://ocw.mit.edu/18-06S05)
- **Video Lectures:** [MIT OpenCourseWare YouTube](https://www.youtube.com/watch?v=ZK3O402wf1c)

---
