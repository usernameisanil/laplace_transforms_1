# Unit IV — Laplace Transforms

**Course:** 23A35101 — Numerical & Statistical Methods  
**University:** JNTUA College of Engineering (Autonomous)  

---

## Overview

Unit IV introduces the Laplace Transform — a powerful integral transform that converts differential equations in the time-domain into algebraic equations in the s-domain. This unit builds from the definition through properties to practical evaluation techniques.

> **Restructured (v2):** Topics 01+02 merged into a single foundational topic covering Introduction and Definition together, since the definition IS the introduction. Topics 07+08 on Derivatives and Integrals are kept separate to give each sufficient depth. Topics 09+10 (Multiplication by t / Division by t) are kept separate as their proof techniques differ significantly.

---

## Topic List (in teaching order)

| Topic No. | Topic Name | Prompt File |
|-----------|-----------|-------------|
| 01 | Introduction & Definition of Laplace Transform | `prompts/unit_iv/topic_01_introduction_definition.md` |
| 02 | Conditions for Existence of Laplace Transform | `prompts/unit_iv/topic_02_conditions_existence.md` |
| 03 | Transforms of Elementary Functions | `prompts/unit_iv/topic_03_elementary_functions.md` |
| 04 | Properties of Laplace Transforms | `prompts/unit_iv/topic_04_properties.md` |
| 05 | Laplace Transform of Periodic Functions | `prompts/unit_iv/topic_05_periodic_functions.md` |
| 06 | Special Functions (Unit Step, Impulse, Gamma) | `prompts/unit_iv/topic_06_special_functions.md` |
| 07 | Laplace Transforms of Derivatives | `prompts/unit_iv/topic_07_derivatives.md` |
| 08 | Laplace Transforms of Integrals | `prompts/unit_iv/topic_08_integrals.md` |
| 09 | Multiplication by t (and tⁿ) | `prompts/unit_iv/topic_09_multiplication_by_t.md` |
| 10 | Division by t | `prompts/unit_iv/topic_10_division_by_t.md` |
| 11 | Evaluation of Integrals by Laplace Transforms | `prompts/unit_iv/topic_11_evaluation_of_integrals.md` |

---

## Topic Descriptions

### Topic 01 — Introduction & Definition of Laplace Transform

Establishes what the Laplace Transform is and why it is useful. Covers:
- **Motivation:** Converting ODEs with initial conditions into algebraic equations
- **Definition:** L{f(t)} = F(s) = ∫₀^∞ e^(−st) f(t) dt, for s > 0
- **The s-domain:** Complex frequency variable s; interpreting F(s) as a function of s
- **Linearity of the transform:** L{af(t) + bg(t)} = aF(s) + bG(s)
- Notion of a **transform pair:** f(t) ↔ F(s)
- Simple worked example: L{1} = 1/s; L{eᵃᵗ} = 1/(s−a)

---

### Topic 02 — Conditions for Existence of Laplace Transform

Establishes when L{f(t)} is guaranteed to exist. Covers:
- **Piecewise continuity:** f(t) must be piecewise continuous on [0, ∞)
- **Exponential order:** |f(t)| ≤ Me^(αt) for some constants M > 0, α; then F(s) exists for s > α
- **Sufficient conditions theorem** (with statement and interpretation)
- Counterexample: f(t) = e^(t²) does NOT have a Laplace transform
- Practical implication: most engineering functions satisfy these conditions

---

### Topic 03 — Transforms of Elementary Functions

Builds the standard Laplace transform table from first principles. Covers:
- **L{1}** = 1/s (s > 0)
- **L{tⁿ}** = n!/s^(n+1) (s > 0, n = positive integer)
- **L{eᵃᵗ}** = 1/(s−a) (s > a)
- **L{sin(at)}** = a/(s² + a²); **L{cos(at)}** = s/(s² + a²)
- **L{sinh(at)}** = a/(s² − a²); **L{cosh(at)}** = s/(s² − a²)
- Derivation of each using the definition integral
- Worked examples combining multiple elementary transforms

---

### Topic 04 — Properties of Laplace Transforms

Develops rules that allow computing transforms of complex functions from known simple ones. Covers:
- **Linearity:** L{af + bg} = aF(s) + bG(s)
- **First Shifting Theorem (s-shifting):** L{eᵃᵗ f(t)} = F(s−a)
- **Second Shifting Theorem (t-shifting):** L{f(t−a)u(t−a)} = e^(−as)F(s)
- **Change of Scale:** L{f(at)} = (1/a)F(s/a)
- **Differentiation in s-domain:** d/ds[F(s)] = −L{t·f(t)}
- **Integration in s-domain:** ∫_s^∞ F(u)du = L{f(t)/t}
- Worked examples for each property

---

### Topic 05 — Laplace Transform of Periodic Functions

Derives a special formula for periodic functions. Covers:
- **Periodic function definition:** f(t + T) = f(t) for all t ≥ 0
- **Formula:** L{f(t)} = [∫₀^T e^(−st) f(t) dt] / (1 − e^(−sT))
- **Derivation** using the geometric series for ∫₀^∞ split into intervals [0,T], [T,2T], ...
- Examples: Square wave, triangular wave, rectified sine wave
- Comparison with non-periodic transforms

---

### Topic 06 — Special Functions

Introduces three special functions commonly appearing in engineering applications. Covers:
- **Unit Step Function (Heaviside):** u(t−a) = 0 for t < a, 1 for t ≥ a; L{u(t−a)} = e^(−as)/s
- **Unit Impulse Function (Dirac Delta):** δ(t−a); sifting property; L{δ(t−a)} = e^(−as)
- **Gamma Function:** Γ(n) = ∫₀^∞ e^(−t) t^(n−1) dt; Γ(n+1) = nΓ(n); Γ(1/2) = √π
- **L{tⁿ}** for non-integer n using Gamma function: L{t^n} = Γ(n+1)/s^(n+1)
- Applications of each in modelling switched systems, impulse responses

---

### Topic 07 — Laplace Transforms of Derivatives

Shows how the Laplace Transform converts differentiation into multiplication by s. Covers:
- **First derivative:** L{f′(t)} = sF(s) − f(0)
- **Second derivative:** L{f″(t)} = s²F(s) − sf(0) − f′(0)
- **nth derivative:** L{f^(n)(t)} = s^n F(s) − s^(n−1)f(0) − ... − f^(n−1)(0)
- Initial conditions are naturally incorporated into the transform
- **Application:** Solving IVPs — transform the ODE, solve for F(s), invert
- Worked example: solving y″ + y = 0 with y(0)=1, y′(0)=0

---

### Topic 08 — Laplace Transforms of Integrals

Shows how the Laplace Transform handles integration. Covers:
- **Transform of integral:** L{∫₀ᵗ f(u) du} = F(s)/s
- **Proof** using integration by parts
- Inverse: ∫₀ᵗ f(u) du ↔ F(s)/s (division by s in s-domain)
- **Repeated integration:** L{∫∫ ... f dt} = F(s)/s^n
- Worked examples applying the theorem
- Relationship to differentiation theorem (duality)

---

### Topic 09 — Multiplication by t (and tⁿ)

Derives the rule when f(t) is multiplied by powers of t. Covers:
- **Rule:** L{t·f(t)} = −d/ds[F(s)]
- **Generalisation:** L{tⁿ·f(t)} = (−1)ⁿ · d^n/ds^n [F(s)]
- **Proof** by differentiating the definition integral under the integral sign
- Worked examples: L{t·sin(at)}, L{t·eᵃᵗ}, L{t²·cos(at)}
- Connection to Properties topic (differentiation in s-domain)

---

### Topic 10 — Division by t

Derives the rule when f(t) is divided by t. Covers:
- **Rule:** L{f(t)/t} = ∫_s^∞ F(u) du (provided limit exists as t→0⁺)
- **Existence condition:** lim_{t→0⁺} f(t)/t must be finite
- **Proof** by integrating F(s) with respect to s from s to ∞
- Worked examples: L{sin(t)/t}, L{(1−cos(at))/t}
- Application in evaluating improper integrals

---

### Topic 11 — Evaluation of Integrals by Laplace Transforms

Applies the Division by t result and other transform properties to evaluate definite integrals that are otherwise difficult. Covers:
- **Technique:** Express integrand as f(t)/t or as a Laplace-type integral, then use transform tables
- **Standard results derived:**
  - ∫₀^∞ (sin t)/t dt = π/2
  - ∫₀^∞ e^(−at) sin(bt) dt = b/(a²+b²)
  - ∫₀^∞ (sin t / t) e^(−st) dt
- Systematic method: Identify F(s) → use ∫_s^∞ F(u) du or set s=0
- Multiple worked examples with step-by-step reasoning

---

## Syllabus Coverage Map

| Syllabus Item | Covered In |
|---|---|
| Introduction | Topic 01 |
| Definition | Topic 01 |
| Conditions for existence | Topic 02 |
| Transforms of elementary functions | Topic 03 |
| Properties of Laplace transforms | Topic 04 |
| Laplace transform of periodic function | Topic 05 |
| Special functions | Topic 06 |
| Derivatives | Topic 07 |
| Integrals | Topic 08 |
| Multiplication by t | Topic 09 |
| Division by t | Topic 10 |
| Evaluation of integrals by Laplace transforms | Topic 11 |

---

## Prerequisites Needed

- Differential Calculus: derivatives, chain rule, product rule
- Integral Calculus: integration by parts, improper integrals
- Ordinary Differential Equations: first and second order ODEs, initial value problems
- Complex numbers: basic operations (for s as complex frequency)
- Partial fractions (will be used extensively in Unit V)
