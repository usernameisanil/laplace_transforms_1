# Prompt — Topic 12: Evaluation of Integrals by Laplace Transforms

**Unit:** IV — Laplace Transforms
**Course:** 23A54201 — Mathematics IV (Transform Techniques)
**University:** JNTUA College of Engineering (Autonomous)
**Target Audience:** B.Tech 2nd-year engineering students (non-mathematics majors)

---

## Prompt

You are an expert mathematics professor writing a **complete, compilable LaTeX (.tex) lecture note** for B.Tech engineering students on the topic **"Evaluation of Integrals by Laplace Transforms"**. This is Topic 12 of Unit IV — the culminating application topic. Students have now mastered the full toolkit: definition, standard table, all properties (shifting, scaling, multiplication/division by t), derivatives, and integrals. Now they will use these tools to evaluate **definite integrals** that are very hard by direct methods. The key idea: if a known Laplace transform pair gives $\mathcal{L}\{f(t)\} = F(s)$, setting $s=0$ or $s=a$ (or integrating in $s$) often yields a famous definite integral. Write as a teacher who makes this feel like a satisfying mathematical payoff.

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
- `\lhead{Topic 12: Evaluation of Integrals by Laplace Transforms}`
- `\rhead{Unit IV --- Laplace Transforms}`
- `\cfoot{\thepage}`

Configure lstlisting for Python (same style as Topic 01).

Title page: `\title{Topic 12: Evaluation of Integrals by Laplace Transforms \\ \large Unit IV --- Laplace Transforms}`, `\maketitle`, `\tableofcontents`, `\newpage`.

---

## AUDIENCE AND TONE

Same as Topic 01: enthusiastic, conversational voice. This is the reward topic — make students feel proud of using all their accumulated knowledge to crack famously difficult integrals.

---

## OPENING HOOK (MANDATORY)

Place inside `\begin{curiositybox}{Hook}`: The integral $\int_0^\infty \frac{\sin t}{t}\, dt$ defeated generations of calculus students who tried direct integration — $\sin t/t$ has no elementary antiderivative. Yet with the Laplace Transform, you can evaluate it in two lines. From Topic 11: $\mathcal{L}\{\sin t / t\} = \pi/2 - \arctan(s)$. Set $s = 0$: $\int_0^\infty (\sin t/t)\, dt = \pi/2$. Done. The Laplace Transform doesn't just solve ODEs — it can evaluate any integral whose integrand is recognisable as a Laplace transform integrand. This topic teaches you the systematic strategy.

---

## REQUIRED SECTIONS

### 1. Why This Topic Exists
"Before we begin, here is the honest answer to why you are reading this..."
Many definite integrals that appear in engineering and physics cannot be evaluated by standard calculus techniques (substitution, integration by parts). Two-column booktabs table (Mistake | Consequence):
- "Trying to integrate $e^{-t}\sin t / t$ directly" | "No elementary antiderivative — stuck completely"
- "Not identifying the correct Laplace transform pair" | "Cannot set up the evaluation correctly"
- "Setting $s$ to an invalid value" | "Evaluating outside the region of convergence, getting nonsense"
End with a learnbox.

### 2. You Already Know This (Intuition First)
You have already been doing this implicitly. When you computed $\mathcal{L}\{e^{-2t}\} = 1/(s+2)$, you actually proved that $\int_0^\infty e^{-(s+2)t}\, dt = 1/(s+2)$ for all valid $s$. Setting $s=0$ gives $\int_0^\infty e^{-2t}\, dt = 1/2$ — a definite integral evaluated for free. The strategy in this topic is to choose $s$ strategically (or use the division-by-$t$ and other properties) to extract the specific definite integral you want.

### 3. The Three Strategies
Inside `infobox`: Present three systematic strategies:

**Strategy 1 — Setting s = 0:**
If $\mathcal{L}\{f(t)\} = F(s)$, then $F(0) = \int_0^\infty f(t)\, dt$. Use this when you need $\int_0^\infty f(t)\, dt$ and $F(0)$ is easy to evaluate.

**Strategy 2 — Using Division by t (Topic 11):**
$\mathcal{L}\{f(t)/t\} = \int_s^\infty F(u)\, du$. Setting $s = 0$: $\int_0^\infty f(t)/t\, dt = \int_0^\infty F(u)\, du$ — provided the integral converges.

**Strategy 3 — Using the derivative property (Topic 10):**
If $\mathcal{L}\{tf(t)\} = -F'(s)$, then $\int_0^\infty e^{-st} tf(t)\, dt = -F'(s)$. Setting $s = a$ gives $\int_0^\infty e^{-at} tf(t)\, dt = -F'(a)$.

### 4. Classic Integral 1 — $\int_0^\infty \frac{\sin t}{t}\, dt = \frac{\pi}{2}$
Inside `infobox`:
From Topic 11: $\mathcal{L}\{\sin t/t\} = \pi/2 - \arctan(s)$.
Definition: $\int_0^\infty e^{-st} \cdot \frac{\sin t}{t}\, dt = \pi/2 - \arctan(s)$.
Set $s \to 0^+$: $\int_0^\infty \frac{\sin t}{t}\, dt = \pi/2 - \arctan(0) = \pi/2$.
Check the validity: $\sin(t)/t$ is integrable on $[0,\infty)$ and the transform is valid for $s \geq 0$.
Confirm: $\int_0^\infty \frac{\sin t}{t}\, dt = \frac{\pi}{2}$. ✓

### 5. Classic Integral 2 — $\int_0^\infty e^{-at} \frac{\sin t}{t}\, dt = \frac{\pi}{2} - \arctan(a)$
Inside `infobox`:
This follows directly from the transform evaluated at $s = a > 0$:
$\int_0^\infty e^{-at} \cdot \frac{\sin t}{t}\, dt = \pi/2 - \arctan(a)$.
Evaluate explicitly for $a = 1$ (gives $\pi/2 - \pi/4 = \pi/4$) and $a = \sqrt{3}$ (gives $\pi/2 - \pi/3 = \pi/6$).

### 6. Classic Integral 3 — $\int_0^\infty t e^{-at} \sin(bt)\, dt$
Inside `infobox`:
From Topic 10: $\mathcal{L}\{t\sin(bt)\} = 2bs/(s^2+b^2)^2$.
Therefore: $\int_0^\infty e^{-st} t\sin(bt)\, dt = 2bs/(s^2+b^2)^2$.
Set $s = a$: $\int_0^\infty t e^{-at}\sin(bt)\, dt = 2ab/(a^2+b^2)^2$.
Evaluate for $a=1$, $b=1$: result is $2/(1+1)^2 = 1/2$.

### 7. Classic Integral 4 — $\int_0^\infty \frac{e^{-at} - e^{-bt}}{t}\, dt = \ln(b/a)$
Inside `infobox`:
From Topic 11: $\mathcal{L}\{(e^{-at} - e^{-bt})/t\} = \ln[(s+b)/(s+a)]$ (note: derived there as $\ln[(s-a')/(s-b')]$ — use $a \to -a$, $b \to -b$ substitution, or re-derive for $e^{-at}$).

Actually derive from scratch for $f(t) = e^{-at} - e^{-bt}$: $\mathcal{L}\{f\} = 1/(s+a) - 1/(s+b)$.
$\mathcal{L}\{f(t)/t\} = \int_s^\infty \left[\frac{1}{u+a} - \frac{1}{u+b}\right] du = \left[\ln(u+a) - \ln(u+b)\right]_s^\infty$.
Evaluate: $\lim_{u\to\infty}[\ln(u+a) - \ln(u+b)] = 0$ (since $(u+a)/(u+b) \to 1$). Lower limit: $\ln(s+b) - \ln(s+a)$.
So $\mathcal{L}\{f/t\} = \ln[(s+b)/(s+a)]$. Set $s=0$: $\int_0^\infty (e^{-at}-e^{-bt})/t\, dt = \ln(b/a)$ for $0 < a < b$.

This is the **Frullani integral** — state this connection.

### 8. Classic Integral 5 — $\int_0^\infty e^{-t} t^n\, dt = n! = \Gamma(n+1)$
Inside `infobox`:
From the standard table: $\mathcal{L}\{t^n\} = n!/s^{n+1}$.
Set $s = 1$: $\int_0^\infty e^{-t} t^n\, dt = n!$.
This is exactly the Gamma function definition $\Gamma(n+1) = \int_0^\infty t^n e^{-t}\, dt = n!$. Connection: the Laplace transform formula PROVES the Gamma function definition.

**pgfplots graph (MANDATORY):** Plot the integrand $g(t) = t^n e^{-t}$ for $n=1,2,3,4$ on the same axes for $t \in [0,12]$. Label axes, legend for each $n$, grid=major. Show how the peak shifts right and the total area equals $n!$.

### 9. Summary Table of Classic Integrals
Booktabs table (8+ rows): Integral | Transform Pair Used | Value.
Include: $\int_0^\infty \sin t/t\, dt$; $\int_0^\infty e^{-at}\sin t/t\, dt$; $\int_0^\infty te^{-at}\sin(bt)\, dt$; $\int_0^\infty (e^{-at}-e^{-bt})/t\, dt$; $\int_0^\infty t^n e^{-t}\, dt$; two more of your choice.

### 10. Worked Examples
**Example 1:** Evaluate $\int_0^\infty e^{-2t}\frac{\sin(3t)}{t}\, dt$ using the strategy "set $s=2$ in $\mathcal{L}\{\sin(3t)/t\}$".
**Example 2:** Evaluate $\int_0^\infty t^2 e^{-3t}\cos(t)\, dt$ using the multiplication-by-$t^2$ formula.
**Example 3:** Evaluate $\int_0^\infty \frac{\cos(at) - \cos(bt)}{t}\, dt$ using the division-by-$t$ property. (Result: $\ln(b/a)$.)

All examples inside `infobox`. End each with learnbox.

### 11. Excel Example (MANDATORY)
Numerically verify $\int_0^\infty e^{-t} t^3\, dt = 3! = 6$:
- Columns: t | $t^3 e^{-t}$ | Cumulative Trapezoid Sum
- Formulas: `=A2^3*EXP(-A2)`, trapezoid rule
- Rows: t = 0 to t = 20 in steps of 0.1
Show the running sum converging to 6.
End with learnbox comparing to $3! = 6$.

### 12. Python Example (MANDATORY)
Provide a Python script using `scipy.integrate.quad` and `sympy` that:
- Numerically evaluates all five classic integrals from Sections 4--8
- Symbolically verifies each using `sympy.integrate` or known results
- Computes $\pi/2$ comparison for the sinc integral
- Verifies $\int_0^\infty t^n e^{-t}\, dt = n!$ for $n = 1, 2, 3, 4, 5$
Include expected printed output as comments. End with learnbox.

### 13. Viva-Style Oral Questions (8 questions with answers)
Cover: the three strategies, how setting $s=0$ gives a definite integral, $\int_0^\infty \sin t/t\, dt$ result and derivation, the Frullani integral result, the Gamma function connection, when setting $s=0$ is valid (convergence condition), $\int_0^\infty te^{-at}\sin(bt)\, dt$ result, what this topic demonstrates about the power of Laplace transforms.

### 14. Descriptive Questions (5 exam-style questions)
Full written-answer: evaluate $\int_0^\infty \sin(t)/t\, dt$ using Laplace transforms (show all steps), prove the Frullani integral result using Laplace transforms, evaluate $\int_0^\infty t^2 e^{-at}\sin(bt)\, dt$, explain Strategy 2 (division-by-$t$ at $s=0$) with a complete example, show the connection between $\mathcal{L}\{t^n\}$ and the Gamma function $\Gamma(n+1) = n!$.

### 15. Practice Problems (6 problems with answer hints)
Problems: $\int_0^\infty e^{-3t}\sin(2t)/t\, dt$; $\int_0^\infty (e^{-2t}-e^{-5t})/t\, dt$; $\int_0^\infty t e^{-2t}\cos(3t)\, dt$; $\int_0^\infty e^{-t}\cos(t)/t\, dt$ — does this exist? (Check condition); $\int_0^\infty t^{3/2} e^{-t}\, dt$ (Gamma function); $\int_0^\infty \sin^2(t)/t^2\, dt$ (apply property twice).

### 16. MCQs (5 questions)
5 MCQs, bold correct answer, one-line explanation. Cover: $\int_0^\infty \sin t/t\, dt$ result, the Frullani integral, which strategy to use for $\int_0^\infty f(t)/t\, dt$, what setting $s=0$ extracts, the Gamma function connection.

### 17. Common Mistakes Box
`mistakebox` tabular (5 rows): Mistake | What Students Do | Correct Approach.
- Setting $s=0$ when $F(0)$ diverges (e.g., $F(s) = 1/s$)
- Confusing $\int_0^\infty F(u)\, du$ (not a useful formula) with $\int_s^\infty F(u)\, du$
- Not verifying convergence of the original integral before evaluating at $s=0$
- Missing the $s \to 0^+$ limit (not directly setting $s=0$ for improper cases)
- Using the multiplication-by-$t$ strategy when division-by-$t$ is needed

### 18. Quick Recap
`learnbox` with 6--8 bullets: three strategies, five classic integrals with values, Gamma function connection, Frullani integral, validity condition for setting $s=0$, what makes Laplace a powerful integration tool.

---

## MANDATORY QUALITY CHECKLIST

- [ ] Opening hook present in `curiositybox`
- [ ] Three strategies clearly stated in an `infobox`
- [ ] All five classic integrals evaluated completely with all steps
- [ ] Frullani integral named and its derivation shown
- [ ] Gamma function connection explicitly established
- [ ] Summary booktabs table of classic integrals (8+ rows)
- [ ] At least 1 pgfplots graph (integrand curves for different n) with labeled axes
- [ ] At least 1 Excel column-by-column example with cell formulas shown
- [ ] At least 1 Python lstlisting with verbatim output shown
- [ ] Every major example ends with a `learnbox` "What Did We Learn?"
- [ ] All four tcolorbox environments used at least once
- [ ] `\end{document}` present at the very end
- [ ] All formulae in correct LaTeX syntax
