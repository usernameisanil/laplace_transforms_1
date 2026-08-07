# Prompt — Topic 03: Method of Partial Fractions

**Unit:** V — Inverse Laplace Transforms
**Course:** 23A54201 — Mathematics IV (Transform Techniques)
**University:** JNTUA College of Engineering (Autonomous)
**Target Audience:** B.Tech 2nd-year engineering students (non-mathematics majors)

---

## Prompt

You are an expert mathematics professor writing a **complete, compilable LaTeX (.tex) lecture note** for B.Tech engineering students on the topic **"Method of Partial Fractions for Inverse Laplace Transforms"**. This is Topic 03 of Unit V. Students can invert simple F(s) directly (Topics 01--02). Now they face complex rational $F(s) = P(s)/Q(s)$ where $Q(s)$ has multiple roots. Partial fractions decompose these into simple pieces that each match a table entry. This is the most widely-used technique for inverting Laplace transforms in ODE solving. Cover all three cases: distinct real roots, repeated roots, and complex conjugate roots. Write as a teacher who makes the algebraic mechanics feel logical and systematic.

---

## LATEX SETUP REQUIREMENTS

Use this exact preamble (add any extra packages needed by the content):

```latex
\documentclass[12pt,a4paper]{article}
\usepackage{amsmath, amssymb, geometry, booktabs, xcolor, hyperref,
            listings, pgfplots, tcolorbox, enumitem, fancyhdr, tikz, array}
\geometry{margin=2.5cm}
\pgfplotsset{compat=1.18}
\tcbuselibrary{skins, breakable}
```

Define these four tcolorbox environments in the preamble:
- `\newtcolorbox{curiositybox}` — colback=yellow!10, colframe=orange!80
- `\newtcolorbox{infobox}` — colback=blue!5, colframe=blue!60
- `\newtcolorbox{mistakebox}` — colback=red!5, colframe=red!60
- `\newtcolorbox{learnbox}` — colback=green!5, colframe=green!60

Set up fancyhdr with:
- `\lhead{Topic 03: Method of Partial Fractions}`
- `\rhead{Unit V --- Inverse Laplace Transforms}`
- `\cfoot{\thepage}`

Configure lstlisting for Python (same style as Unit IV).

Title page: `\title{Topic 03: Method of Partial Fractions \\ \large Unit V --- Inverse Laplace Transforms}`, `\maketitle`, `\tableofcontents`, `\newpage`.

---

## AUDIENCE AND TONE

Same as Unit IV: enthusiastic, conversational, patient voice. Partial fractions feel mechanical — make it feel satisfying by showing how each case reduces to a recognisable table entry.

---

## OPENING HOOK (MANDATORY)

Place inside `\begin{curiositybox}{Hook}`: After solving an ODE in the s-domain, you often get something like $Y(s) = (3s+7)/[(s+1)(s^2+4)]$. You cannot invert this directly — it does not match any standard table entry. But if you split it into $A/(s+1) + (Bs+C)/(s^2+4)$, suddenly you have two pieces, each directly invertible: $Ae^{-t}$ and $B\cos(2t) + (C/2)\sin(2t)$. The method of partial fractions is the "divide and conquer" strategy for inverting any rational transform. Master it and you can invert virtually anything.

---

## REQUIRED SECTIONS

### 1. Why This Topic Exists
"Before we begin, here is the honest answer to why you are reading this..."
Most ODE solutions produce rational $F(s)$ with denominator degree $\geq 2$. The standard table entries are simple — partial fractions break complex rational functions into those simple pieces. Two-column booktabs table (Mistake | Consequence):
- "Trying to invert without decomposing first" | "No table entry matches — stuck completely"
- "Using wrong form for repeated roots" | "Incomplete decomposition — missing $A_2/(s-a)^2$ terms"
- "Treating complex roots incorrectly" | "Getting complex-valued $f(t)$ instead of real sinusoidal functions"
End with a learnbox.

### 2. You Already Know This (Intuition First)
Compare to **breaking a complex fraction in arithmetic**: $7/12 = 3/4 - 1/6$. You break one hard fraction into two easy ones. Partial fractions do the same for rational functions: one hard $P(s)/Q(s)$ becomes several easy $A/(s-r)$, $B/(s-r)^2$, $(Cs+D)/(s^2+as+b)$ fractions. Each piece then maps directly to a table entry.

### 3. Prerequisite: Proper Rational Functions
Inside `infobox`: $F(s) = P(s)/Q(s)$ is proper if $\deg(P) < \deg(Q)$. If $\deg(P) \geq \deg(Q)$, perform **polynomial long division** first to reduce to a proper fraction plus a polynomial.

Example: $F(s) = (s^3+2s)/(s^2+1)$. Long division gives $s + (s)/(s^2+1)$. The polynomial part $s$ inverts to $\delta'(t)$ (derivative of delta — note this); the proper fraction inverts normally.

Booktabs table: degree condition | action | example.

### 4. Case 1 — Distinct Real Roots
Inside `infobox`: If $Q(s) = (s-r_1)(s-r_2)\cdots(s-r_n)$ with all $r_i$ distinct:
$$\frac{P(s)}{Q(s)} = \frac{A_1}{s-r_1} + \frac{A_2}{s-r_2} + \cdots + \frac{A_n}{s-r_n}$$

**Heaviside cover-up method:** $A_k = P(r_k)/Q'(r_k)$ where $Q'$ is the product of remaining factors.

**General method:** multiply both sides by $Q(s)$, substitute specific values of $s$ to find each $A_k$.

Fully worked example: $F(s) = (3s+7)/[(s+1)(s-2)(s+3)]$.
- Find $A, B, C$ by cover-up or substitution
- Write: $A/(s+1) + B/(s-2) + C/(s+3)$
- Invert: $f(t) = Ae^{-t} + Be^{2t} + Ce^{-3t}$
Show every algebraic step.

### 5. Case 2 — Repeated Real Roots
Inside `infobox`: If $Q(s)$ contains $(s-r)^m$ as a factor:
$$\frac{P(s)}{(s-r)^m \cdot R(s)} = \frac{A_1}{s-r} + \frac{A_2}{(s-r)^2} + \cdots + \frac{A_m}{(s-r)^m} + \cdots$$

Finding coefficients: $A_m = \lim_{s\to r} (s-r)^m F(s)$; lower coefficients by differentiation or by substituting convenient values of $s$.

Fully worked example: $F(s) = (s+3)/[(s-1)^2(s+2)]$.
- Decompose: $A/(s-1) + B/(s-1)^2 + C/(s+2)$
- Find each coefficient step by step
- Invert: $Ae^t + Bte^t + Ce^{-2t}$
Show every step.

Another example: $F(s) = 2/[s^2(s+1)]$.
Decompose: $A/s + B/s^2 + C/(s+1)$.
Invert using standard table: $A + Bt + Ce^{-t}$.

### 6. Case 3 — Complex Conjugate Roots (Irreducible Quadratic)
Inside `infobox`: If $Q(s)$ contains an irreducible quadratic $(s^2 + as + b)$ with $a^2 - 4b < 0$:
$$\frac{P(s)}{(s^2+as+b)\cdot R(s)} = \frac{As+B}{s^2+as+b} + \cdots$$

Strategy: complete the square in $s^2 + as + b = (s+p)^2 + q^2$, then split numerator:
$As + B = A(s+p) + (B - Ap)$. Each piece matches a shifted $\cos$ or $\sin$.

Fully worked example: $F(s) = (s^2+2s+3)/[(s^2+2s+5)(s-1)]$.
- Decompose: $(As+B)/(s^2+2s+5) + C/(s-1)$
- Find $C$ by cover-up: $C = F(s)(s-1)|_{s=1}$
- Find $A, B$ by equating numerator coefficients
- Complete square: $s^2+2s+5 = (s+1)^2+4$
- Invert: $e^{-t}(\alpha\cos(2t) + \beta\sin(2t)) + Ce^t$
Show all steps.

### 7. Case 4 — Repeated Complex Roots (Advanced)
Inside `infobox` (brief): If $(s^2+as+b)^2$ appears, the decomposition is:
$(A_1 s + B_1)/(s^2+as+b) + (A_2 s + B_2)/(s^2+as+b)^2$.
After completing the square, the second term inverts to $te^{-pt}\sin(qt)$ type functions. Give one brief example with the final form stated (not fully derived — this is complex enough to state).

### 8. Systematic Procedure Summary
Inside `infobox`: Step-by-step algorithm:
1. Check if F(s) is proper; if not, do polynomial division first.
2. Factor Q(s) completely into linear and irreducible quadratic factors.
3. Write the partial fraction form based on the root types.
4. Find all coefficients using cover-up (for distinct roots) + substitution/equating coefficients.
5. Invert each term using the standard table (+ completing the square for quadratic terms).
6. Combine all terms for the final $f(t)$.

### 9. Coefficient-Finding Methods Summary
Booktabs table: Method | When to Use | How It Works.
Rows: Heaviside cover-up (distinct linear roots), substitution of convenient $s$ values, equating coefficients of like powers of $s$, differentiation method for repeated roots.

### 10. pgfplots Visualization
**pgfplots graph (MANDATORY):** For the Case 1 example, plot $f(t) = Ae^{-t} + Be^{2t} + Ce^{-3t}$ with numerical values substituted. For $t \in [0, 2]$, show each component term separately and their sum. Grid=major, different colors, legend, labeled axes. Caption: "Each partial fraction term contributes one exponential mode — the total solution is a superposition."

### 11. Worked Examples
**Example 1:** Find $\mathcal{L}^{-1}\left\{\frac{2s^2+5s+3}{(s+1)(s+2)(s+3)}\right\}$ (three distinct roots).
**Example 2:** Find $\mathcal{L}^{-1}\left\{\frac{1}{s^2(s^2+4)}\right\}$ (repeated root $s=0$ and complex pair).
**Example 3:** Find $\mathcal{L}^{-1}\left\{\frac{s^3+2}{(s-1)(s^2+4)}\right\}$ (needs polynomial division since deg numerator = deg denominator; actually adjust example to ensure proper).

All examples inside `infobox`. End each with learnbox.

### 12. Excel Example (MANDATORY)
Numerically verify the Case 2 example result. For $F(s) = (s+3)/[(s-1)^2(s+2)]$, the inverse is $f(t) = Ae^t + Bte^t + Ce^{-2t}$ (compute exact $A$, $B$, $C$ in the LaTeX, then use them here):
- Columns: t | $f(t)$ (exact formula with computed A, B, C) | $e^{-3t}f(t)$ (integrand at $s=3$) | Cumulative Trapezoid Sum
- Formulas using exact coefficients, trapezoid rule
- Rows: t=0 to t=4 in steps of 0.05
Compare cumulative sum to $F(3)$ computed directly.
End with learnbox.

### 13. Python Example (MANDATORY)
Provide a Python script using `sympy` that:
- Performs partial fraction decomposition of all three main examples symbolically using `sympy.apart`
- Computes the inverse transform of each decomposed form
- Verifies by taking the forward transform and comparing to original $F(s)$
Include expected printed output as comments. End with learnbox.

### 14. Viva-Style Oral Questions (8 questions with answers)
Cover: when partial fractions are applicable (proper fraction condition), the three cases, Heaviside cover-up for distinct roots, how to handle repeated roots, what to do with irreducible quadratics, completing the square step, how many constants to expect (equals degree of denominator), combining partial fractions with the shift theorem.

### 15. Descriptive Questions (5 exam-style questions)
Full written-answer: state the three cases and decomposition forms, solve a given Case 1 example completely, solve a given Case 2 example completely, solve a given Case 3 example completely, explain when polynomial long division is needed and demonstrate.

### 16. Practice Problems (6 problems with answer hints)
Problems: $\mathcal{L}^{-1}\{(2s+1)/[(s+1)(s+3)]\}$; $\mathcal{L}^{-1}\{1/[s(s^2+1)]\}$; $\mathcal{L}^{-1}\{s/[(s-1)(s^2+2s+5)]\}$; $\mathcal{L}^{-1}\{(s^2+s+1)/[s^2(s+1)]\}$; $\mathcal{L}^{-1}\{3/(s^2+s)^2\}$ (repeated quadratic — state approach); $\mathcal{L}^{-1}\{(s^3+1)/[s^2(s^2+4)]\}$ (check if proper first).

### 17. MCQs (5 questions)
5 MCQs, bold correct answer, one-line explanation. Cover: proper fraction condition, number of constants in Case 2, form of decomposition for irreducible quadratic, Heaviside cover-up formula, which case applies when denominator has $(s^2+4)$.

### 18. Common Mistakes Box
`mistakebox` tabular (5 rows): Mistake | What Students Do | Correct Approach.
- Using $A/(s-r)^2$ only for repeated root (forgetting the $A_1/(s-r) + A_2/(s-r)^2$ form)
- Treating $s^2+4$ as $(s+2)(s-2)$ (it doesn't factor over reals — it's an irreducible quadratic)
- Not performing polynomial long division before partial fractions
- Wrong numerator form for quadratic factor — using $A$ instead of $As+B$
- Computational error in finding constants — not verifying by recombining

### 19. Quick Recap
`learnbox` with 6--8 bullets: proper fraction check, three cases, cover-up for distinct roots, repeated root form, irreducible quadratic form + completing the square, systematic 6-step procedure, Python/sympy as a verification tool.

---

## MANDATORY QUALITY CHECKLIST

- [ ] Opening hook present in `curiositybox`
- [ ] All three main cases (distinct, repeated, complex) with full worked examples
- [ ] Heaviside cover-up method explained and demonstrated
- [ ] Proper fraction condition and long division shown
- [ ] Repeated root coefficient-finding via substitution/differentiation
- [ ] Complex root: completing the square + numerator splitting demonstrated
- [ ] At least 1 pgfplots graph showing component terms of Case 1 solution
- [ ] Summary booktabs table of coefficient-finding methods
- [ ] At least 1 Excel column-by-column example with cell formulas shown
- [ ] At least 1 Python lstlisting with `sympy.apart` and inverse transform shown
- [ ] Every major example ends with a `learnbox` "What Did We Learn?"
- [ ] All four tcolorbox environments used at least once
- [ ] `\end{document}` present at the very end
- [ ] All formulae in correct LaTeX syntax
