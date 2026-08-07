# Prompt — Topic 04: Transforms of Elementary Functions

**Unit:** IV — Laplace Transforms
**Course:** 23A54201 — Mathematics IV (Transform Techniques)
**University:** JNTUA College of Engineering (Autonomous)
**Target Audience:** B.Tech 2nd-year engineering students (non-mathematics majors)

---

## Prompt

You are an expert mathematics professor writing a **complete, compilable LaTeX (.tex) lecture note** for B.Tech engineering students on the topic **"Transforms of Elementary Functions"**. This is Topic 04 of Unit IV. Students now have the definition (Topic 02) and know when the transform exists (Topic 03). This topic builds the complete standard table — the essential toolkit for all subsequent topics. Derive every result step-by-step from the definition so students understand where the table comes from, not just what it contains.

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
- `\lhead{Topic 04: Transforms of Elementary Functions}`
- `\rhead{Unit IV --- Laplace Transforms}`
- `\cfoot{\thepage}`

Configure lstlisting for Python (same style as Topic 01).

Title page: `\title{Topic 04: Transforms of Elementary Functions \\ \large Unit IV --- Laplace Transforms}`, `\maketitle`, `\tableofcontents`, `\newpage`.

---

## AUDIENCE AND TONE

Same as Topic 01: enthusiastic, conversational teaching voice. Short paragraphs, varied sentence length. This is the "building the toolkit" topic — make students feel like they are accumulating weapons for solving problems, not just memorising formulas.

---

## OPENING HOOK (MANDATORY)

Place inside `\begin{curiositybox}{Hook}`: A craftsman cannot build furniture without knowing their tools — a chisel, a hammer, a saw. A Laplace transform user cannot solve any real problem without knowing what $\mathcal{L}\{e^{at}\}$, $\mathcal{L}\{\sin(at)\}$, and $\mathcal{L}\{t^n\}$ are. This topic builds your complete toolkit — a table of 7 standard transforms, each derived step-by-step from the definition. By the end, you will be able to transform any combination of elementary functions instantly.

---

## REQUIRED SECTIONS

### 1. Why This Topic Exists
"Before we begin, here is the honest answer to why you are reading this..."
Without the standard table, every transform computation requires starting from scratch with the definition integral. Two-column booktabs table (Mistake | Consequence):
- "Memorising only the table without derivations" | "Unable to derive transforms of unfamiliar functions in exams"
- "Mixing up $\sin$ and $\cos$ transforms" | "Sign errors in all subsequent calculations"
- "Forgetting the $n!$ in $\mathcal{L}\{t^n\}$" | "Wrong answers on power function transforms"
End with a learnbox.

### 2. You Already Know This (Intuition First)
Compare to the derivatives table in Calculus 1: students memorised $d/dx[\sin x] = \cos x$, $d/dx[e^x] = e^x$, etc. — but they also understood where those came from. Similarly, the Laplace transform table is not arbitrary magic: each entry follows from the same definition integral, just evaluated for different f(t). The goal is to understand the table well enough to re-derive any entry if needed.

### 3. Derivation 1 — $\mathcal{L}\{1\} = 1/s$
Inside `infobox`: Start from $\int_0^\infty e^{-st} \cdot 1\, dt$, evaluate the improper integral step-by-step as a limit, obtain $1/s$ for $s > 0$. State the validity condition explicitly.

### 4. Derivation 2 — $\mathcal{L}\{t^n\} = n!/s^{n+1}$
Inside `infobox`: Start with $n=1$ (use integration by parts: $u=t$, $dv=e^{-st}dt$). Then generalize to $n=2$ (integration by parts twice). State the general result using the Gamma function: $\int_0^\infty t^n e^{-st}\, dt = \Gamma(n+1)/s^{n+1} = n!/s^{n+1}$ for integer $n$. Show the Gamma function connection: $\Gamma(n) = (n-1)!$ for positive integers. Validity: $s > 0$, $n > -1$.

### 5. Derivation 3 — $\mathcal{L}\{e^{at}\} = 1/(s-a)$
Inside `infobox`: Combine $e^{-st}$ and $e^{at}$ to get $e^{-(s-a)t}$, evaluate the integral, obtain $1/(s-a)$ for $s > a$. Emphasize the sign: it is $(s - a)$, NOT $(s + a)$.

### 6. Derivations 4 & 5 — $\mathcal{L}\{\sin(at)\}$ and $\mathcal{L}\{\cos(at)\}$
Inside `infobox`: Use Euler's formula method: $e^{iat} = \cos(at) + i\sin(at)$, so $\mathcal{L}\{e^{iat}\} = 1/(s-ia)$. Multiply numerator and denominator by $(s+ia)$, separate real and imaginary parts:
$$\mathcal{L}\{\cos(at)\} = \frac{s}{s^2+a^2}, \quad \mathcal{L}\{\sin(at)\} = \frac{a}{s^2+a^2}, \quad s > 0$$
Alternatively, show direct integration by parts twice (for $\sin$). Both methods shown for completeness.

### 7. Derivations 6 & 7 — $\mathcal{L}\{\sinh(at)\}$ and $\mathcal{L}\{\cosh(at)\}$
Inside `infobox`: Use the exponential definitions:
- $\sinh(at) = (e^{at} - e^{-at})/2$ → apply linearity and $\mathcal{L}\{e^{at}\}$
- $\cosh(at) = (e^{at} + e^{-at})/2$ → apply linearity and $\mathcal{L}\{e^{at}\}$
Results: $\mathcal{L}\{\sinh(at)\} = a/(s^2-a^2)$, $\mathcal{L}\{\cosh(at)\} = s/(s^2-a^2)$ for $s > |a|$.

### 8. The Complete Standard Transform Table
Present as a large booktabs table (8+ rows): f(t) | $\mathcal{L}\{f(t)\} = F(s)$ | Validity Condition.
Include all 7 derived transforms plus $\mathcal{L}\{1\}$ as a special case of $\mathcal{L}\{t^n\}$ with $n=0$.

### 9. Visualizing the Standard Transforms
**pgfplots graph (MANDATORY):** Plot four time-domain functions on the same axes (or two separate plots):
- $f(t) = e^{-t}$ (exponential decay)
- $f(t) = \sin(2t)$ (sinusoidal)
- $f(t) = t^2$ (parabolic)
- $f(t) = \cosh(t)$ (hyperbolic)
For $t \in [0, 4]$, grid=major, different colors, legend. Caption: "These four elementary functions generate the entire standard transform table."

### 10. Worked Examples
**Example 1:** Find $\mathcal{L}\{5t^3 - 3\cos(2t) + 4e^{-t}\}$ using linearity and the standard table. Show full step-by-step substitution.
**Example 2:** Find $\mathcal{L}\{\sin^2(t)\}$ using the identity $\sin^2 t = (1-\cos 2t)/2$, then applying linearity.
**Example 3:** Find $\mathcal{L}\{2\sinh(3t) - 5\cosh(t)\}$ using the standard table directly.

All examples inside `infobox`. End each with learnbox.

### 11. Excel Example (MANDATORY)
Numerically verify $\mathcal{L}\{\sin(2t)\}$ at $s=3$ equals $2/(9+4) = 2/13$:
- Columns: t | $e^{-3t}\sin(2t)$ | Cumulative Trapezoid Area
- Formulas: `=EXP(-3*A2)*SIN(2*A2)`, trapezoid rule, rows from t=0 to t=5 in steps of 0.1
End with learnbox comparing numerical result to exact $2/13 \approx 0.1538$.

### 12. Python Example (MANDATORY)
Provide a Python script using `sympy` that:
- Computes $\mathcal{L}\{t^n\}$ for $n = 1, 2, 3, 4$ symbolically
- Computes $\mathcal{L}\{\sin(at)\}$ and $\mathcal{L}\{\cos(at)\}$ symbolically
- Computes $\mathcal{L}\{\sinh(at)\}$ and $\mathcal{L}\{\cosh(at)\}$ symbolically
- Prints all results in closed form
Include expected printed output as comments. End with learnbox.

### 13. Viva-Style Oral Questions (8 questions with answers)
Cover: how to derive $\mathcal{L}\{t^n\}$, the Gamma function connection, why $n!$ appears, difference between $\sin$ and $\cos$ transforms, why $s^2 + a^2$ vs. $s^2 - a^2$ for trig vs. hyperbolic, the Euler formula method, the validity condition for each transform, how linearity extends the table.

### 14. Descriptive Questions (5 exam-style questions)
Full written-answer: derive $\mathcal{L}\{\cos(at)\}$ using Euler's formula, derive $\mathcal{L}\{t^n\}$ using reduction formula, state and verify $\mathcal{L}\{\sinh(at)\}$ using exponential definitions, find $\mathcal{L}\{3t^2 - 5e^{2t} + \cos(t)\}$ step by step, explain why the standard table alone is insufficient without linearity.

### 15. Practice Problems (6 problems with answer hints)
Problems: $\mathcal{L}\{4t^2 - 2\sin(3t)\}$; $\mathcal{L}\{e^{-2t} + 3\cosh(t)\}$; $\mathcal{L}\{\cos^2(t)\}$ (use identity); $\mathcal{L}\{t^{3/2}\}$ (Gamma function); $\mathcal{L}\{\sin(2t)\cos(2t)\}$ (use identity $\sin(2\theta) = 2\sin\theta\cos\theta$); $\mathcal{L}\{(t+1)^2\}$ (expand then transform).

### 16. MCQs (5 questions)
5 MCQs, bold correct answer, one-line explanation. Cover: $\mathcal{L}\{t^n\}$ formula, $\mathcal{L}\{\sin(at)\}$ vs. $\mathcal{L}\{\cos(at)\}$ distinction, validity condition, $\mathcal{L}\{e^{at}\}$ sign, Gamma function value.

### 17. Common Mistakes Box
`mistakebox` tabular (5 rows): Mistake | What Students Do | Correct Approach.
- Swapping $\mathcal{L}\{\sin\}$ and $\mathcal{L}\{\cos\}$ (which has s, which has a in numerator)
- Writing $1/(s+a)$ instead of $1/(s-a)$ for $e^{at}$
- Forgetting $n!$ — writing $1/s^{n+1}$ instead of $n!/s^{n+1}$
- Using $s^2 - a^2$ denominator for $\sin(at)$ (that's $\sinh(at)$)
- Applying invalid transforms where $s \leq a$ for $e^{at}$

### 18. Quick Recap
`learnbox` with 6--8 bullets: all 7 standard transforms with formulas, validity conditions, Gamma function connection, Euler formula method for trig, hyperbolic via exponentials, linearity as the multiplier.

---

## MANDATORY QUALITY CHECKLIST

- [ ] Opening hook present in `curiositybox`
- [ ] All 7 standard transforms derived step-by-step from the definition
- [ ] Complete standard table as a booktabs table
- [ ] At least 1 pgfplots graph with axis labels, legend, grid
- [ ] At least 1 Excel column-by-column example with cell formulas shown
- [ ] At least 1 Python lstlisting with verbatim output shown
- [ ] Every major example ends with a `learnbox` "What Did We Learn?"
- [ ] All four tcolorbox environments used at least once
- [ ] Gamma function connection explained
- [ ] Euler formula method shown for trig transforms
- [ ] `\end{document}` present at the very end
- [ ] All formulae in correct LaTeX syntax
