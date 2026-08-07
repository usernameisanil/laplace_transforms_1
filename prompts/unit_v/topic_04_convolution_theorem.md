# Prompt — Topic 04: Convolution Theorem

**Unit:** V — Inverse Laplace Transforms
**Course:** 23A54201 — Mathematics IV (Transform Techniques)
**University:** JNTUA College of Engineering (Autonomous)
**Target Audience:** B.Tech 2nd-year engineering students (non-mathematics majors)

---

## Prompt

You are an expert mathematics professor writing a **complete, compilable LaTeX (.tex) lecture note** for B.Tech engineering students on the topic **"Convolution Theorem"**. This is Topic 04 of Unit V. Students have partial fractions (Topic 03) for inverting products of transforms in some cases. The Convolution Theorem provides an alternative approach: $\mathcal{L}^{-1}\{F(s)G(s)\} = (f * g)(t)$, where $*$ is the convolution integral. This is both a theoretical result and a practical tool — especially when partial fractions are awkward or when solving integral equations. Prove the theorem rigorously, define convolution carefully with all its properties, and show applications to both inverse transforms and integral equations. Write as a teacher who makes convolution feel geometrically intuitive, not just algebraically formal.

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
- `\lhead{Topic 04: Convolution Theorem}`
- `\rhead{Unit V --- Inverse Laplace Transforms}`
- `\cfoot{\thepage}`

Configure lstlisting for Python (same style as Unit IV).

Title page: `\title{Topic 04: Convolution Theorem \\ \large Unit V --- Inverse Laplace Transforms}`, `\maketitle`, `\tableofcontents`, `\newpage`.

---

## AUDIENCE AND TONE

Same as Unit IV: enthusiastic, conversational voice. Convolution is geometrically rich — use the "sliding window" or "echo" analogy to make the integral feel physical, not abstract.

---

## OPENING HOOK (MANDATORY)

Place inside `\begin{curiositybox}{Hook}`: You have mastered partial fractions. But consider $\mathcal{L}^{-1}\{1/[(s^2+a^2)(s^2+b^2)]\}$ where $a \neq b$. You could decompose by partial fractions — but the algebra gets messy with complex roots. Now imagine instead: $F(s) = 1/(s^2+a^2)$ and $G(s) = 1/(s^2+b^2)$ are individually recognisable as $\sin(at)/a$ and $\sin(bt)/b$. The Convolution Theorem says: $\mathcal{L}^{-1}\{F(s)G(s)\} = (f * g)(t) = \int_0^t f(\tau)g(t-\tau)\, d\tau$. You do one integral instead of a messy partial fraction. The Convolution Theorem is your power tool for products of transforms.

---

## REQUIRED SECTIONS

### 1. Why This Topic Exists
"Before we begin, here is the honest answer to why you are reading this..."
Products of transforms arise naturally from ODEs, integral equations, and system analysis. Partial fractions can handle many cases, but convolution handles all cases and has deeper theoretical importance. Two-column booktabs table (Mistake | Consequence):
- "Thinking $\mathcal{L}^{-1}\{F(s)G(s)\} = f(t)g(t)$" | "Completely wrong — the product rule does NOT apply to inverse Laplace"
- "Not computing the convolution integral correctly" | "Wrong limits or wrong variable substitution"
- "Forgetting convolution is commutative" | "Computing the harder order instead of the easier"
End with a learnbox.

### 2. You Already Know This (Intuition First)
Use the **acoustic echo analogy**: convolution $(f * g)(t)$ is like an audio system where $f(\tau)$ is the input signal and $g(t-\tau)$ is the impulse response (echo profile). At each moment $t$, the output is the sum of all past inputs weighted by the echo — $\int_0^t f(\tau) g(t-\tau)\, d\tau$. The output at time $t$ depends on the entire history from 0 to $t$. This is physically meaningful: it captures how a system "remembers" its past inputs.

### 3. Definition of Convolution
Inside `infobox`:
$$(f * g)(t) = \int_0^t f(\tau) g(t-\tau)\, d\tau$$

Properties of convolution:
- **Commutativity:** $f * g = g * f$ (prove by substituting $u = t - \tau$)
- **Associativity:** $(f * g) * h = f * (g * h)$
- **Distributivity:** $f * (g + h) = f * g + f * h$
- **Identity:** $f * \delta = f$ (convolution with the delta function)
- **Zero element:** $f * 0 = 0$

Full proof of commutativity: substitute $u = t - \tau$ in the integral, change limits, show $f * g = g * f$. Show every step.

### 4. The Convolution Theorem
Inside `infobox`:

**Theorem:** If $\mathcal{L}\{f(t)\} = F(s)$ and $\mathcal{L}\{g(t)\} = G(s)$, then:
$$\mathcal{L}\{(f * g)(t)\} = F(s) \cdot G(s)$$

Equivalently:
$$\mathcal{L}^{-1}\{F(s) G(s)\} = (f * g)(t) = \int_0^t f(\tau) g(t-\tau)\, d\tau$$

**Complete proof:**
$$\mathcal{L}\{f * g\} = \int_0^\infty e^{-st} \left[\int_0^t f(\tau) g(t-\tau)\, d\tau\right] dt$$
Interchange order of integration: the region $0 \leq \tau \leq t < \infty$ becomes $\tau \leq t < \infty$, so integrate $\tau$ from 0 to $\infty$ and $t$ from $\tau$ to $\infty$:
$$= \int_0^\infty f(\tau) \left[\int_\tau^\infty e^{-st} g(t-\tau)\, dt\right] d\tau$$
Substitute $u = t - \tau$ in the inner integral ($t = u + \tau$, $dt = du$, limits: 0 to $\infty$):
$$= \int_0^\infty f(\tau) e^{-s\tau} \left[\int_0^\infty e^{-su} g(u)\, du\right] d\tau = G(s) \int_0^\infty f(\tau) e^{-s\tau}\, d\tau = F(s)G(s)$$
Show every step explicitly.

### 5. Computing Convolution Integrals
Inside `infobox`: The four steps to evaluate $(f * g)(t)$:
1. Write $\int_0^t f(\tau) g(t-\tau)\, d\tau$
2. Substitute the explicit forms of $f$ and $g$
3. Treat $t$ as a constant and integrate over $\tau$ from 0 to $t$
4. Simplify the result (depends on $t$)

Worked derivation: compute $(e^{at} * e^{bt})(t)$ for $a \neq b$:
$$\int_0^t e^{a\tau} e^{b(t-\tau)}\, d\tau = e^{bt} \int_0^t e^{(a-b)\tau}\, d\tau = e^{bt} \cdot \frac{e^{(a-b)t}-1}{a-b} = \frac{e^{at}-e^{bt}}{a-b}$$
Verify: $\mathcal{L}\{(e^{at}-e^{bt})/(a-b)\} = [1/(s-a) - 1/(s-b)]/(a-b)$, which equals $\mathcal{L}\{e^{at}\}\mathcal{L}\{e^{bt}\} = 1/[(s-a)(s-b)]$. ✓

### 6. Application 1 — Inverting Products via Convolution
Inside `infobox`:
**Example:** Find $\mathcal{L}^{-1}\{1/[s(s^2+a^2)]\}$ using convolution.
- $F(s) = 1/s$ → $f(t) = 1$
- $G(s) = 1/(s^2+a^2)$ → $g(t) = \sin(at)/a$
- $(f*g)(t) = \int_0^t 1 \cdot \frac{\sin(a(t-\tau))}{a}\, d\tau = \frac{1}{a}\left[-\frac{\cos(a(t-\tau))}{a}\right]_0^t = \frac{1-\cos(at)}{a^2}$

Verify: $\mathcal{L}\{(1-\cos(at))/a^2\} = (1/a^2)[1/s - s/(s^2+a^2)] = 1/[s(s^2+a^2)]$. ✓

Show all integration steps.

### 7. Application 2 — Solving Integral Equations
Inside `infobox`: A Volterra integral equation of the second kind:
$y(t) = f(t) + \lambda \int_0^t k(t-\tau) y(\tau)\, d\tau$

Taking $\mathcal{L}$: $Y(s) = F(s) + \lambda K(s) Y(s)$ → $Y(s) = F(s)/[1 - \lambda K(s)]$.

Fully worked example: Solve $y(t) = \sin t + \int_0^t \cos(t-\tau) y(\tau)\, d\tau$.
- $\mathcal{L}$: $Y = 1/(s^2+1) + s/(s^2+1) \cdot Y$
- $(1 - s/(s^2+1)) Y = 1/(s^2+1)$
- $(s^2-s+1)/(s^2+1) \cdot Y = 1/(s^2+1)$
- $Y = 1/(s^2-s+1)$
- Complete the square: $s^2 - s + 1 = (s-1/2)^2 + 3/4$
- Invert: $y(t) = \frac{2}{\sqrt{3}} e^{t/2} \sin(\sqrt{3}t/2)$
Show every step.

### 8. Visualizing Convolution
**pgfplots graph (MANDATORY):** Illustrate convolution of $f(t) = e^{-t}$ and $g(t) = u(t)$ (unit step):
- Plot $f(\tau) = e^{-\tau}$
- Plot $g(t-\tau)$ for a fixed $t=2$: this is $u(2-\tau) = 1$ for $0 \leq \tau \leq 2$, 0 otherwise (reflected and shifted)
- Shade the overlap region $0 \leq \tau \leq 2$
- The area of the overlap at each $t$ is $(f*g)(t) = 1 - e^{-t}$
- Plot $(f*g)(t) = 1-e^{-t}$ as a separate graph
Grid=major, labeled axes, legend for each curve. Caption: "Convolution at time $t=2$ is the integral of $f(\tau) \cdot g(2-\tau)$ — the area under the product."

### 9. Comparison: Convolution vs. Partial Fractions
Booktabs table: Criterion | Partial Fractions | Convolution.
Rows: When to use, Algebraic complexity, Requires polynomial factoring, Handles all rational F(s)G(s), Useful for integral equations, Gives closed-form f(t) directly.

### 10. Worked Examples
**Example 1:** Use convolution to find $\mathcal{L}^{-1}\{1/[(s^2+1)^2]\}$.
Hint: $F(s) = G(s) = 1/(s^2+1)$ → $f = g = \sin t$. Compute $(\sin * \sin)(t) = \int_0^t \sin\tau\sin(t-\tau)\, d\tau$ using the product-to-sum identity. Show all steps.

**Example 2:** Solve the integral equation $y(t) + \int_0^t y(\tau) e^{-(t-\tau)}\, d\tau = t$ using Laplace transforms and convolution.

**Example 3:** Use convolution to find $\mathcal{L}^{-1}\{s/(s^2+a^2)^2\}$.

All examples inside `infobox`. End each with learnbox.

### 11. Excel Example (MANDATORY)
Numerically verify convolution $(e^{-t} * \sin t)(t)$ at $t=2$:
Exact value: $\int_0^2 e^{-\tau}\sin(2-\tau)\, d\tau$ (compute analytically in the LaTeX for comparison).
- Columns: $\tau$ | $e^{-\tau}$ | $\sin(2-\tau)$ | Product | Trapezoid Sum
- Formulas: `=EXP(-A2)`, `=SIN(2-A2)`, `=B2*C2`, trapezoid rule
- Rows: $\tau$ = 0 to $\tau$ = 2 in steps of 0.05
End with learnbox comparing numerical and analytical values.

### 12. Python Example (MANDATORY)
Provide a Python script using `numpy` and `scipy.integrate` that:
- Numerically computes $(f * g)(t)$ for $f(t) = e^{-t}$ and $g(t) = \sin t$ for $t \in [0, 6]$
- Computes the closed-form result analytically (using integration result) and plots both
- Verifies the convolution theorem: takes $\mathcal{L}$ of the convolution numerically and compares to $F(s)G(s)$
Include expected printed output as comments. End with learnbox.

### 13. Viva-Style Oral Questions (8 questions with answers)
Cover: definition of convolution, commutativity proof, convolution theorem statement, complete proof (key step: change of order of integration), why $\mathcal{L}^{-1}\{FG\} \neq fg$, how to solve integral equations using convolution, the echo/LTI system interpretation, comparison with partial fractions.

### 14. Descriptive Questions (5 exam-style questions)
Full written-answer: state and prove the convolution theorem, prove commutativity of convolution, find $\mathcal{L}^{-1}\{1/[s(s+1)^2]\}$ using convolution, solve a given Volterra integral equation completely, explain the physical interpretation of convolution in an LTI system.

### 15. Practice Problems (6 problems with answer hints)
Problems: $(1 * e^{-t})(t)$; $\mathcal{L}^{-1}\{1/s^2(s+1)\}$ via convolution; solve $y = 1 + \int_0^t \sin(t-\tau)y(\tau)\, d\tau$; $(e^{at} * t)(t)$; $\mathcal{L}^{-1}\{1/(s^2+1)^2\}$; solve $y(t) = e^{-t} - \int_0^t e^{-(t-\tau)}y(\tau)\, d\tau$.

### 16. MCQs (5 questions)
5 MCQs, bold correct answer, one-line explanation. Cover: convolution theorem formula, $\mathcal{L}^{-1}\{F(s)G(s)\}$, commutativity, upper limit of the convolution integral, $(f*\delta)(t)$ result.

### 17. Common Mistakes Box
`mistakebox` tabular (5 rows): Mistake | What Students Do | Correct Approach.
- Thinking $\mathcal{L}^{-1}\{F(s)G(s)\} = f(t)g(t)$
- Wrong upper limit in the convolution integral (using $\infty$ instead of $t$)
- Not replacing $g$'s argument: writing $g(\tau)$ instead of $g(t-\tau)$
- Forgetting to substitute $u = t-\tau$ when using commutativity to simplify the integral
- Not checking whether partial fractions would be easier before committing to convolution

### 18. Quick Recap
`learnbox` with 6--8 bullets: convolution definition, commutativity property and proof, theorem statement and proof, $(f*g)(t)$ computation steps, inverting products, solving integral equations, comparison with partial fractions.

---

## MANDATORY QUALITY CHECKLIST

- [ ] Opening hook present in `curiositybox`
- [ ] Convolution definition with all five properties (commutativity proved)
- [ ] Full proof of convolution theorem (change of order of integration — every step)
- [ ] Worked derivation of $(e^{at} * e^{bt})$ with verification
- [ ] Inverting $1/[s(s^2+a^2)]$ via convolution shown completely
- [ ] Volterra integral equation solved using Laplace + convolution
- [ ] At least 1 pgfplots visualisation of sliding window/overlap
- [ ] Comparison table: convolution vs. partial fractions
- [ ] At least 1 Excel column-by-column numerical convolution with formulas
- [ ] At least 1 Python lstlisting with numerical and symbolic verification
- [ ] Every major example ends with a `learnbox` "What Did We Learn?"
- [ ] All four tcolorbox environments used at least once
- [ ] `\end{document}` present at the very end
- [ ] All formulae in correct LaTeX syntax
