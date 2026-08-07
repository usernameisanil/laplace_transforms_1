# Unit V — Inverse Laplace Transforms

**Course:** 23A35101 — Numerical & Statistical Methods  
**University:** JNTUA College of Engineering (Autonomous)  

---

## Overview

Unit V covers the inverse Laplace Transform — the process of recovering f(t) from a given F(s). This unit focuses on systematic algebraic and theorem-based methods for inversion, culminating in the solution of ordinary differential equations using the Laplace transform approach.

> **Restructured (v2):** Topics "Inverse Laplace Transform" and "Elementary Functions" are combined as Topic 12, since identifying standard inverse transform pairs IS the foundation of all inversion methods. The Convolution Theorem is taught before ODE applications, as convolution is needed for solving certain ODEs where partial fractions alone are insufficient.

---

## Topic List (in teaching order)

| Topic No. | Topic Name | Prompt File |
|-----------|-----------|-------------|
| 12 | Inverse Laplace Transform & Elementary Functions | `prompts/unit_v/topic_12_inverse_laplace_elementary.md` |
| 13 | Method of Partial Fractions | `prompts/unit_v/topic_13_partial_fractions.md` |
| 14 | Convolution Theorem | `prompts/unit_v/topic_14_convolution_theorem.md` |
| 15 | Applications to Ordinary Differential Equations | `prompts/unit_v/topic_15_ode_applications.md` |

> **Note on numbering:** Unit IV topics are numbered 01–11; Unit V topics continue as 12–15 for a unified 15-topic course structure.

---

## Topic Descriptions

### Topic 12 — Inverse Laplace Transform & Elementary Functions

Introduces the concept of inverting F(s) back to f(t). Covers:
- **Definition:** L⁻¹{F(s)} = f(t) — the unique function f(t) such that L{f(t)} = F(s)
- **Linearity of inverse transform:** L⁻¹{aF(s) + bG(s)} = af(t) + bg(t)
- **Standard inverse pairs** (direct table lookup):
  - L⁻¹{1/s} = 1
  - L⁻¹{1/s^n} = t^(n−1)/(n−1)!
  - L⁻¹{1/(s−a)} = eᵃᵗ
  - L⁻¹{a/(s²+a²)} = sin(at); L⁻¹{s/(s²+a²)} = cos(at)
  - L⁻¹{a/(s²−a²)} = sinh(at); L⁻¹{s/(s²−a²)} = cosh(at)
- **First Shifting Theorem (inverse form):** L⁻¹{F(s−a)} = eᵃᵗ f(t)
- Worked examples using table and shifting theorem

---

### Topic 13 — Method of Partial Fractions

The primary algebraic technique for inverting F(s) when it is a rational function. Covers:
- **When to use:** F(s) = P(s)/Q(s) where degree of P < degree of Q
- **Case 1 — Non-repeated linear factors:** A/(s−a) + B/(s−b) + ...
- **Case 2 — Repeated linear factors:** A/(s−a) + B/(s−a)² + ...
- **Case 3 — Irreducible quadratic factors:** (As+B)/(s²+ps+q) + ...
- **Complete the square** for quadratics not in standard form: match to (s+a)²+b²
- Cover-up rule and comparison of coefficients
- Worked examples for each case, including combined cases

---

### Topic 14 — Convolution Theorem

Provides a powerful method to invert products F(s)·G(s) without full partial fractions. Covers:
- **Convolution definition:** (f * g)(t) = ∫₀ᵗ f(u) g(t−u) du
- **Commutativity:** f * g = g * f
- **Convolution Theorem:** L{f * g} = F(s)·G(s), equivalently L⁻¹{F(s)·G(s)} = (f * g)(t)
- **Proof** of the theorem (interchange of integration order)
- **Applying the theorem:** Given F(s)·G(s), identify f and g, then compute the convolution integral
- Worked examples: L⁻¹{1/(s(s²+a²))}, L⁻¹{1/(s²+a²)²}
- Comparison with partial fractions: when convolution is more efficient

---

### Topic 15 — Applications to Ordinary Differential Equations

Applies the complete Laplace Transform machinery to systematically solve ODEs. Covers:
- **Method outline:** (1) Take L of both sides → (2) Apply derivative formulas incorporating ICs → (3) Solve for Y(s) = L{y(t)} → (4) Invert using partial fractions / convolution
- **First-order linear ODEs with initial conditions**
- **Second-order linear ODEs with constant coefficients** (most common exam type)
- **Systems of ODEs:** Transform each equation, solve the algebraic system for Y₁(s), Y₂(s), invert
- **ODEs with discontinuous forcing functions:** using unit step function and Second Shifting Theorem
- **ODEs with impulsive forcing:** using Dirac delta function
- 4–5 fully worked examples covering each case

---

## Syllabus Coverage Map

| Syllabus Item | Covered In |
|---|---|
| Inverse Laplace transform | Topic 12 |
| Elementary functions (inverse) | Topic 12 |
| Method of partial fractions | Topic 13 |
| Convolution theorem | Topic 14 |
| Applications to ODEs | Topic 15 |

---

## Prerequisites Needed

- Unit IV: All Laplace Transform topics (01–11)
- Partial fractions (algebra prerequisite)
- First and second order ODEs: formation and general solution
- Integration techniques: substitution, integration by parts
- Complex numbers: for factoring quadratics in the denominator
