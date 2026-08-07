# Prompt — Topic 05: Applications to Ordinary Differential Equations

**Unit:** V — Inverse Laplace Transforms
**Course:** 23A54201 — Mathematics IV (Transform Techniques)
**University:** JNTUA College of Engineering (Autonomous)
**Target Audience:** B.Tech 2nd-year engineering students (non-mathematics majors)

---

## Prompt

You are an expert mathematics professor writing a **complete, compilable LaTeX (.tex) lecture note** for B.Tech engineering students on the topic **"Applications of Laplace Transforms to Ordinary Differential Equations"**. This is Topic 05 of Unit V — the grand finale. Students now have the complete Laplace toolkit: forward transforms (Unit IV) and all inverse methods (Unit V Topics 01--04). This topic applies everything to solve a wide variety of ODEs: first-order, second-order with constant coefficients, ODEs with discontinuous forcing (unit step), ODEs with impulse forcing (delta function), and systems of simultaneous ODEs. Conclude with a circuit analysis application. Write as a teacher who makes students feel the complete power of what they have learned across both units.

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
- `\lhead{Topic 05: Applications to ODEs}`
- `\rhead{Unit V --- Inverse Laplace Transforms}`
- `\cfoot{\thepage}`

Configure lstlisting for Python (same style as Unit IV).

Title page: `\title{Topic 05: Applications to Ordinary Differential Equations \\ \large Unit V --- Inverse Laplace Transforms}`, `\maketitle`, `\tableofcontents`, `\newpage`.

---

## AUDIENCE AND TONE

This is the culminating topic. Use a triumphant, confident tone — "You have earned this." Make every ODE feel like a complete story from problem to solution. Show the full 4-step Laplace workflow for every problem. Reward students' patience through two full units.

---

## OPENING HOOK (MANDATORY)

Place inside `\begin{curiositybox}{Hook}`: Two full units. Twelve topics in Unit IV, five topics in Unit V. You have learned the definition, existence conditions, all standard transforms, five operational properties, derivatives, integrals, multiplication and division by $t$, evaluation of integrals, inverse transforms, partial fractions, and convolution. All of it has been building toward one destination: solving ordinary differential equations that arise in electrical circuits, mechanical systems, control engineering, and heat flow. This is that destination. In this topic, you will solve ODEs that would take pages using classical methods — each solved in under half a page using the Laplace Transform. Let's go.

---

## REQUIRED SECTIONS

### 1. Why This Topic Exists
"Before we begin, here is the honest answer to why you are reading this..."
This is the payoff for learning everything in Units IV--V. The Laplace method handles discontinuous and impulsive inputs — things the classical ODE methods cannot handle easily. Two-column booktabs table (Mistake | Consequence):
- "Skipping Units IV--V and going directly to the ODE solutions" | "No understanding of *why* each step works — just following a recipe"
- "Forgetting to substitute initial conditions before inverting" | "Getting the wrong particular solution without ICs"
- "Not recognising which inversion method to use" | "Stuck at Y(s) — cannot recover y(t)"
End with a learnbox.

### 2. The Universal 4-Step Workflow
Inside `infobox`: Present the complete algorithm one final time, now fully equipped:

**Step 1:** Apply $\mathcal{L}$ to both sides of the ODE. Use:
- $\mathcal{L}\{y'\} = sY(s) - y(0)$
- $\mathcal{L}\{y''\} = s^2Y(s) - sy(0) - y'(0)$
- $\mathcal{L}\{y'''\} = s^3Y(s) - s^2y(0) - sy'(0) - y''(0)$

**Step 2:** Substitute the given initial conditions $y(0)$, $y'(0)$, etc.

**Step 3:** Solve for $Y(s) = \mathcal{L}\{y(t)\}$ algebraically.

**Step 4:** Invert $Y(s)$ using the appropriate method:
- Direct table lookup (Topics V-01, V-02)
- Partial fractions (Topic V-03)
- Completing the square + shift (Topic V-02)
- Convolution (Topic V-04)

**TikZ flowchart (MANDATORY):** A detailed flowchart showing the complete decision tree for Step 4: "Is F(s) directly in the table?" → yes: invert directly; → no: "Does the denominator have repeated roots?" → yes: use partial fractions Case 2; → "Does it have complex/quadratic factors?" → yes: complete the square; etc. Make it a proper decision flowchart with diamond-shaped decision nodes and rectangular action nodes.

### 3. Application 1 — First-Order ODE
Inside `infobox`: Solve completely:
$$y' + 3y = e^{-t}, \quad y(0) = 2$$

Step 1: $sY - 2 + 3Y = 1/(s+1)$
Step 2: $(s+3)Y = 2 + 1/(s+1) = (2s+3)/(s+1)$
Step 3: $Y = (2s+3)/[(s+1)(s+3)]$
Step 4: Partial fractions: $(2s+3)/[(s+1)(s+3)] = A/(s+1) + B/(s+3)$.
Find $A = 1/2$, $B = 3/2$. Check.
$Y = (1/2)/(s+1) + (3/2)/(s+3)$
$y(t) = \frac{1}{2}e^{-t} + \frac{3}{2}e^{-3t}$

Show every single algebraic step. Verify the solution by substituting back into the ODE.

### 4. Application 2 — Second-Order ODE, Constant Coefficients
Inside `infobox`: Solve completely:
$$y'' - 3y' + 2y = 4e^{-t}, \quad y(0) = 1, \quad y'(0) = 0$$

Step 1: $(s^2Y - s - 0) - 3(sY - 1) + 2Y = 4/(s+1)$
Step 2: $(s^2 - 3s + 2)Y = s - 3 + 4/(s+1) = (s^2-2s+1)/(s+1)$
Step 3: $Y = (s-1)^2/[(s-1)(s-2)(s+1)] = (s-1)/[(s-2)(s+1)]$
Step 4: Partial fractions: $A/(s-2) + B/(s+1)$. Find $A = 1/3$, $B = 2/3$.
$y(t) = \frac{1}{3}e^{2t} + \frac{2}{3}e^{-t}$

Show every step. Verify.

### 5. Application 3 — Underdamped Oscillator
Inside `infobox`: Solve completely:
$$y'' + 2y' + 5y = 0, \quad y(0) = 1, \quad y'(0) = -1$$

Step 1: $(s^2Y - s + 1) + 2(sY - 1) + 5Y = 0$
Step 2: $(s^2 + 2s + 5)Y = s + 1$
Step 3: $Y = (s+1)/(s^2+2s+5)$
Step 4: Complete square: $s^2+2s+5 = (s+1)^2+4$. Numerator: $s+1$.
$Y = (s+1)/[(s+1)^2+4]$ → $y(t) = e^{-t}\cos(2t)$

Show every step. Plot the solution.

**pgfplots graph (MANDATORY):** Plot $y(t) = e^{-t}\cos(2t)$ for $t \in [0, 4\pi]$. Also plot the envelope curves $\pm e^{-t}$ as dashed lines. Grid=major, labeled axes, legend. Caption: "The damped sinusoidal response — $y$ oscillates with exponentially decaying amplitude."

### 6. Application 4 — ODE with Discontinuous Forcing (Unit Step)
Inside `infobox`: Solve completely:
$$y'' + y = f(t), \quad y(0) = 0, \quad y'(0) = 0$$
where $f(t) = \begin{cases} 1 & 0 \leq t < \pi \\ 0 & t \geq \pi \end{cases} = 1 - u(t-\pi)$

Step 1: $(s^2+1)Y = \mathcal{L}\{1 - u(t-\pi)\} = 1/s - e^{-\pi s}/s$
Step 2: $Y = 1/[s(s^2+1)] - e^{-\pi s}/[s(s^2+1)]$
Step 3: Partial fractions: $1/[s(s^2+1)] = 1/s - s/(s^2+1)$ → $\mathcal{L}^{-1} = 1 - \cos t$.

For the second term: $\mathcal{L}^{-1}\{e^{-\pi s} \cdot 1/[s(s^2+1)]\} = [1-\cos(t-\pi)] u(t-\pi) = [1+\cos t] u(t-\pi)$.

$y(t) = (1-\cos t) - [1+\cos t] u(t-\pi)$

Evaluate: for $0 \leq t < \pi$: $y = 1 - \cos t$; for $t \geq \pi$: $y = -2\cos t$.

Show all steps. Plot $y(t)$ for $t \in [0, 3\pi]$ using pgfplots, showing the behaviour change at $t = \pi$.

### 7. Application 5 — ODE with Impulse Forcing (Dirac Delta)
Inside `infobox`: Solve completely:
$$y'' + 4y = 3\delta(t-2), \quad y(0) = 1, \quad y'(0) = 0$$

Step 1: $(s^2+4)Y - s = 3e^{-2s}$
Step 2: $Y = s/(s^2+4) + 3e^{-2s}/(s^2+4)$
Step 3: Invert first term: $\cos(2t)$.
Invert second term using second shifting theorem: $\mathcal{L}^{-1}\{e^{-2s}/(s^2+4)\} = (1/2)\sin(2(t-2))u(t-2)$.

$y(t) = \cos(2t) + \frac{3}{2}\sin(2(t-2)) u(t-2)$

Show all steps. Explain physically: the system oscillates freely at $\omega=2$, then at $t=2$ an instantaneous impulse of magnitude 3 is applied, adding a new sinusoidal term.

### 8. Application 6 — System of ODEs
Inside `infobox`: Solve the simultaneous system:
$$x' = x + y, \quad y' = x - y, \quad x(0) = 1, \quad y(0) = 0$$

Take $\mathcal{L}$ of both equations:
$sX - 1 = X + Y$ → $(s-1)X - Y = 1$
$sY - 0 = X - Y$ → $-X + (s+1)Y = 0$

Solve the linear algebraic system for $X(s)$ and $Y(s)$ using Cramer's rule or elimination:
Determinant: $(s-1)(s+1) - 1 = s^2 - 2$.
$X = (s+1)/(s^2-2)$; $Y = 1/(s^2-2)$

Invert: $\sqrt{2} = a$: $X(s) = (s)/( s^2-2) + 1/(s^2-2)$.
$x(t) = \cosh(\sqrt{2}t) + (1/\sqrt{2})\sinh(\sqrt{2}t)$
$y(t) = (1/\sqrt{2})\sinh(\sqrt{2}t)$

Show all Cramer's rule steps.

### 9. Application 7 — RLC Circuit
Inside `infobox`: An RLC series circuit with $R=2$, $L=1$, $C=1/5$ has the ODE:
$i'' + 2i' + 5i = 10\cos(t)$, $i(0) = 0$, $i'(0) = 0$.

Apply Laplace, solve for $I(s)$, invert using partial fractions + completing the square. Obtain $i(t)$ as a sum of transient (decaying) and steady-state (sustained) terms.

$$i(t) = e^{-t}(A\cos 2t + B\sin 2t) + C\cos t + D\sin t$$

Find all constants. Interpret: the first part is the **transient response** (decays to zero), the second part is the **steady-state response** (persists indefinitely).

**pgfplots graph:** Plot $i(t)$ for $t \in [0, 10]$, also showing the steady-state component separately as a dashed curve. Grid=major, legend, labeled axes.

### 10. Summary: All Inverse Methods and When to Use Them
Booktabs table (5+ rows): Situation | Recommended Method | Example.
Rows: $F(s)$ directly in table; $F(s)$ has distinct real denominator roots; repeated roots; irreducible quadratic in denominator; $F(s) = F_1(s) \cdot F_2(s)$ and partial fractions are complex; integral equation.

### 11. Excel Example (MANDATORY)
Numerically verify the first-order ODE solution $y(t) = \frac{1}{2}e^{-t} + \frac{3}{2}e^{-3t}$ against the ODE $y' + 3y = e^{-t}$, $y(0) = 2$:
- Columns: t | $y(t)$ exact | $y'(t)$ exact | $3y(t)$ | $y'+3y$ | $e^{-t}$
- Formulas: `=0.5*EXP(-A2)+1.5*EXP(-3*A2)`, `=-0.5*EXP(-A2)-4.5*EXP(-3*A2)`, `=3*B2`, `=C2+D2`, `=EXP(-A2)`
- Rows: t=0 to t=3 in steps of 0.25
Show $y'+3y = e^{-t}$ holds numerically.
End with learnbox confirming the solution satisfies the ODE.

### 12. Python Example (MANDATORY)
Provide a comprehensive Python script using `sympy` and `scipy.integrate.odeint` that:
- Solves all three main ODE examples symbolically using `sympy.dsolve` and via Laplace (using the workflow)
- Verifies by numerically integrating each ODE with `odeint` and comparing to the exact Laplace solution
- Plots the numerical and Laplace solutions together for the damped oscillator (Application 3)
- Solves the system of ODEs from Application 6 symbolically
Include expected printed output as comments. End with learnbox.

### 13. Viva-Style Oral Questions (8 questions with answers)
Cover: the 4-step Laplace workflow, what happens to initial conditions in Step 2, why the Laplace method handles discontinuous inputs better than classical methods, what $u(t-a)$ does in the forcing term, how an impulse (delta function) forcing manifests in the solution, the transient vs. steady-state interpretation, the simultaneous ODE approach (system of algebraic equations), what determines whether the solution is oscillatory or monotone.

### 14. Descriptive Questions (5 exam-style questions)
Full written-answer: solve a given second-order IVP completely via Laplace transforms, solve a given ODE with unit step forcing, solve a given ODE with delta function forcing, solve a system of two simultaneous first-order ODEs, explain the transient-steady-state decomposition in the RLC circuit example.

### 15. Practice Problems (6 problems with answer hints)
Problems:
1. $y'' + 4y' + 4y = t e^{-2t}$, $y(0) = 0$, $y'(0) = 0$
2. $y'' - 4y = \sin(2t)$, $y(0) = 0$, $y'(0) = 1$
3. $y'' + 9y = \cos(3t)$, $y(0) = 1$, $y'(0) = 0$ (resonance case)
4. $y'' + y = u(t-\pi)$, $y(0) = 0$, $y'(0) = 1$
5. $y'' + 2y' + y = \delta(t-1)$, $y(0) = 0$, $y'(0) = 0$
6. System: $x' - y = \sin t$, $y' + x = \cos t$, $x(0) = 1$, $y(0) = 0$

### 16. MCQs (5 questions)
5 MCQs, bold correct answer, one-line explanation. Cover: $\mathcal{L}\{y''\}$ formula with ICs, what $e^{-as}Y(s)$ becomes in t-domain, what delta function forcing adds to the solution, the transient vs. steady state distinction, why Laplace handles ICs automatically.

### 17. Common Mistakes Box
`mistakebox` tabular (5 rows): Mistake | What Students Do | Correct Approach.
- Forgetting the $-sy(0) - y'(0)$ terms in $\mathcal{L}\{y''\}$
- Not converting piecewise forcing to unit step form before applying $\mathcal{L}$
- Using $\mathcal{L}\{\delta(t-a)\} = 1$ instead of $e^{-as}$
- Solving for $Y(s)$ but then not inverting (leaving the answer in s-domain)
- Not verifying the solution by substitution after inverting

### 18. Quick Recap
`learnbox` with 6--8 bullets: 4-step workflow, IVP solution format, discontinuous forcing via unit steps, impulse forcing via delta, system of ODEs approach, RLC circuit transient/steady-state, which inversion method to choose, the complete toolkit summary.

---

## MANDATORY QUALITY CHECKLIST

- [ ] Opening hook present in `curiositybox`
- [ ] TikZ flowchart for the Step 4 decision tree
- [ ] All seven applications solved completely (no steps skipped)
- [ ] Application 3 (underdamped): pgfplots with envelope curves
- [ ] Application 4 (discontinuous forcing): pgfplots showing behaviour change at $t=\pi$
- [ ] Application 6 (system of ODEs): Cramer's rule shown step by step
- [ ] Application 7 (RLC circuit): transient vs. steady-state interpreted
- [ ] Summary "when to use which method" booktabs table
- [ ] At least 1 Excel column-by-column example verifying ODE solution with formulas
- [ ] Python script solving and verifying multiple ODEs symbolically and numerically
- [ ] Every major example ends with a `learnbox` "What Did We Learn?"
- [ ] All four tcolorbox environments used at least once
- [ ] `\end{document}` present at the very end
- [ ] All formulae in correct LaTeX syntax
- [ ] Tone is triumphant and celebratory — students have earned this
