# Prompt — Topic 06: Laplace Transform of Periodic Functions

**Unit:** IV — Laplace Transforms
**Course:** 23A54201 — Mathematics IV (Transform Techniques)
**University:** JNTUA College of Engineering (Autonomous)
**Target Audience:** B.Tech 2nd-year engineering students (non-mathematics majors)

---

## Prompt

You are an expert mathematics professor writing a **complete, compilable LaTeX (.tex) lecture note** for B.Tech engineering students on the topic **"Laplace Transform of Periodic Functions"**. This is Topic 06 of Unit IV. Students have the standard table and properties (Topics 04--05). This topic extends the toolkit to periodic signals — square waves, triangular waves, sawtooth waves — which are ubiquitous in electrical engineering and signal processing. Write as a teacher who makes this topic feel practically powerful.

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
- `\lhead{Topic 06: Laplace Transform of Periodic Functions}`
- `\rhead{Unit IV --- Laplace Transforms}`
- `\cfoot{\thepage}`

Configure lstlisting for Python (same style as Topic 01).

Title page: `\title{Topic 06: Laplace Transform of Periodic Functions \\ \large Unit IV --- Laplace Transforms}`, `\maketitle`, `\tableofcontents`, `\newpage`.

---

## AUDIENCE AND TONE

Same as Topic 01: enthusiastic, conversational voice. Connect the mathematics to real electrical engineering waveforms that students see in circuits courses.

---

## OPENING HOOK (MANDATORY)

Place inside `\begin{curiositybox}{Hook}`: The AC power supply in your home delivers a sinusoidal voltage repeating 50 times per second. A digital clock circuit uses a square wave. A sawtooth wave drives the sweep in old CRT television sets. All of these are *periodic functions* — they repeat with a fixed period T. Computing their Laplace transforms from scratch using the definition integral would require handling an infinite sum of integrals. There is a much smarter formula that condenses everything into a single integral over just ONE period. Let's derive it.

---

## REQUIRED SECTIONS

### 1. Why This Topic Exists
"Before we begin, here is the honest answer to why you are reading this..."
Engineering systems are driven by periodic inputs. Without the periodic function formula, computing $\mathcal{L}$ of a square wave requires an infinite sum. Two-column booktabs table (Mistake | Consequence):
- "Using the definition integral directly for periodic functions" | "Infinitely tedious computation — cannot be completed in exam time"
- "Forgetting the factor $1/(1-e^{-sT})$" | "Computing only the first-period integral and losing the periodic scaling"
- "Misidentifying the period T" | "Using the wrong limits in the formula"
End with a learnbox.

### 2. You Already Know This (Intuition First)
Use the **recurring payment analogy**: if you receive \$100 every month (period T = 1 month), the present value (at discount rate s) is $100 + 100e^{-s} + 100e^{-2s} + \ldots = 100/(1 - e^{-s})$. The Laplace transform formula for a periodic function works identically — integrate over ONE period, multiply by the geometric series factor $1/(1 - e^{-sT})$. The formula is literally a financial present-value calculation.

### 3. Definition of Periodic Function
Inside `infobox`: f(t) is periodic with period T > 0 if $f(t+T) = f(t)$ for all $t \geq 0$. The smallest such T is the **fundamental period**. Give examples with their periods: $\sin(\omega t)$ (period $2\pi/\omega$), square wave (period T), triangular wave (period T), sawtooth wave (period T).

### 4. The Periodic Function Theorem
Inside `infobox`:

**Theorem:** If f(t) is periodic with period T and piecewise continuous on $[0, T]$, then:
$$\mathcal{L}\{f(t)\} = \frac{1}{1 - e^{-sT}} \int_0^T e^{-st} f(t)\, dt, \quad s > 0$$

**Proof (complete, step-by-step):**
Split the integral $\int_0^\infty = \int_0^T + \int_T^{2T} + \int_{2T}^{3T} + \ldots$

For the $n$-th piece: substitute $t = u + nT$, use $f(u + nT) = f(u)$, factor out $e^{-snT}$:
$$\int_{nT}^{(n+1)T} e^{-st} f(t)\, dt = e^{-snT} \int_0^T e^{-su} f(u)\, du$$

Sum the geometric series: $\sum_{n=0}^\infty e^{-snT} = 1/(1 - e^{-sT})$ for $s > 0$.

Multiply to obtain the formula. Show every step — do not skip any summation step.

### 5. Application 1 — Square Wave
Inside `infobox`: Define the square wave with period $2a$:
$$f(t) = \begin{cases} A & 0 \leq t < a \\ -A & a \leq t < 2a \end{cases}, \quad f(t+2a) = f(t)$$

Apply the theorem: $\int_0^{2a} e^{-st} f(t)\, dt = A\int_0^a e^{-st}\, dt - A\int_a^{2a} e^{-st}\, dt$.

Evaluate both integrals, combine, factor, and obtain:
$$\mathcal{L}\{f(t)\} = \frac{A}{s} \cdot \frac{1 - e^{-as}}{1 + e^{-as}} = \frac{A}{s} \tanh\!\left(\frac{as}{2}\right)$$

Show all algebraic simplification steps.

**pgfplots graph (MANDATORY):** Plot the square wave for 3 full periods ($a=1$, $A=1$), showing clearly the alternating $+1$ and $-1$ values. Grid=major, labeled axes t and f(t). Add vertical dashed lines at $t = 1, 2, 3, 4, 5, 6$.

### 6. Application 2 — Triangular Wave
Inside `infobox`: Define the triangular wave with period $2a$:
$$f(t) = \begin{cases} t & 0 \leq t < a \\ 2a - t & a \leq t < 2a \end{cases}$$

Apply the theorem, evaluate the two integrals (using integration by parts for the linear pieces), and simplify to obtain the final form. Show all steps.

**pgfplots graph:** Plot the triangular wave for 3 periods ($a=1$). Grid=major, labeled axes.

### 7. Application 3 — Half-Wave Rectifier
Inside `infobox`: Define the half-wave rectified sine:
$$f(t) = \begin{cases} \sin(t) & 0 \leq t < \pi \\ 0 & \pi \leq t < 2\pi \end{cases}, \quad \text{period } T = 2\pi$$

Apply the theorem, evaluate $\int_0^\pi e^{-st}\sin(t)\, dt$ by integration by parts (or using the standard table result $1/(s^2+1)$ with limits), and simplify.

### 8. Worked Examples
**Example 1:** A sawtooth wave defined by $f(t) = t/T$ for $0 \leq t < T$, period $T$. Find $\mathcal{L}\{f(t)\}$ using the periodic function theorem. Show all steps.
**Example 2:** Given the full-wave rectified sine $f(t) = |\sin t|$, period $\pi$, find $\mathcal{L}\{f(t)\}$.

All examples inside `infobox`. End each with learnbox.

### 9. Excel Example (MANDATORY)
Numerically verify $\mathcal{L}\{\text{square wave}\}$ at $s=1$, $a=1$, $A=1$:
- Columns: t | f(t) (square wave values) | $e^{-t}f(t)$ | Cumulative Trapezoid Area
- Formulas: `=IF(MOD(A2,2)<1,1,-1)` for square wave, `=EXP(-1*A2)*B2`, trapezoid sum
- Rows: t = 0 to t = 10 in steps of 0.1
Compare cumulative sum to formula value $\tanh(0.5)/1 \approx 0.4621$.
End with learnbox.

### 10. Python Example (MANDATORY)
Provide a Python script using `numpy` and `scipy.integrate` that:
- Defines the square wave function using numpy
- Numerically integrates $e^{-st} f(t)$ from 0 to 50 (approximate infinite integral) at $s=1$, $T=2$
- Computes the formula result using the periodic theorem
- Prints both and compares
Include expected printed output as comments. End with learnbox.

### 11. Viva-Style Oral Questions (8 questions with answers)
Cover: definition of periodic function, statement of periodic transform theorem, how the geometric series arises in the proof, what $1/(1-e^{-sT})$ represents, how to identify T correctly, the square wave transform result, why direct integration is impractical, the half-wave rectifier application.

### 12. Descriptive Questions (5 exam-style questions)
Full written-answer: state and prove the periodic function theorem, find $\mathcal{L}$ of square wave, find $\mathcal{L}$ of triangular wave, derive $\mathcal{L}$ of half-wave rectifier, explain the geometric series connection in the proof.

### 13. Practice Problems (6 problems with answer hints)
Problems: $\mathcal{L}$ of rectangular wave (period $2T$, height $E$); $\mathcal{L}$ of staircase function; $\mathcal{L}$ of full-wave rectified cosine; $\mathcal{L}$ of a sawtooth with different slope; identify period from definition; verify square wave result using $\tanh$ identity.

### 14. MCQs (5 questions)
5 MCQs, bold correct answer, one-line explanation. Cover: periodic theorem formula, the denominator factor, period identification, square wave result, what happens when $T \to \infty$.

### 15. Common Mistakes Box
`mistakebox` tabular (5 rows): Mistake | What Students Do | Correct Approach.
- Forgetting the $1/(1-e^{-sT})$ factor
- Using the wrong period T (e.g., half-period)
- Not checking piecewise continuity before applying the theorem
- Incorrect limits in the integration over one period
- Forgetting the direction of square wave (positive/negative half)

### 16. Quick Recap
`learnbox` with 6--8 bullets: periodic function definition, theorem formula, proof strategy (geometric series), square wave result, triangular wave result, half-wave rectifier, the financial analogy.

---

## MANDATORY QUALITY CHECKLIST

- [ ] Opening hook present in `curiositybox`
- [ ] Complete proof of periodic function theorem with geometric series
- [ ] Square wave, triangular wave, AND half-wave rectifier all computed
- [ ] At least 2 pgfplots graphs (square wave and triangular wave) with labeled axes
- [ ] At least 1 booktabs table with 5+ rows
- [ ] At least 1 Excel column-by-column example with cell formulas shown
- [ ] At least 1 Python lstlisting with verbatim output shown
- [ ] Every major example ends with a `learnbox` "What Did We Learn?"
- [ ] All four tcolorbox environments used at least once
- [ ] Tanh simplification shown for square wave
- [ ] `\end{document}` present at the very end
- [ ] All formulae in correct LaTeX syntax
