# Prompt — Topic 05: Properties of Laplace Transforms

**Unit:** IV — Laplace Transforms
**Course:** 23A54201 — Mathematics IV (Transform Techniques)
**University:** JNTUA College of Engineering (Autonomous)
**Target Audience:** B.Tech 2nd-year engineering students (non-mathematics majors)

---

## Prompt

You are an expert mathematics professor writing a **complete, compilable LaTeX (.tex) lecture note** for B.Tech engineering students on the topic **"Properties of Laplace Transforms"**. This is Topic 05 of Unit IV. Students have the standard transform table (Topic 04) and now need operational shortcuts — properties that let them handle exponential multipliers, time delays, time scaling, and more without re-deriving from the definition every time. Write as a teacher who makes each property feel like a "cheat code" that unlocks new problem-solving power.

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
- `\lhead{Topic 05: Properties of Laplace Transforms}`
- `\rhead{Unit IV --- Laplace Transforms}`
- `\cfoot{\thepage}`

Configure lstlisting for Python (same style as Topic 01).

Title page: `\title{Topic 05: Properties of Laplace Transforms \\ \large Unit IV --- Laplace Transforms}`, `\maketitle`, `\tableofcontents`, `\newpage`.

---

## AUDIENCE AND TONE

Same as Topic 01: enthusiastic, conversational, energetic voice. Frame each property as a powerful shortcut. Use active language: "This is where it gets exciting", "Think of this as a cheat code", "You no longer need to integrate — just shift!"

---

## OPENING HOOK (MANDATORY)

Place inside `\begin{curiositybox}{Hook}`: What if you could find $\mathcal{L}\{e^{3t}\sin(2t)\}$ without touching a single integral? You already know $\mathcal{L}\{\sin(2t)\} = 2/(s^2+4)$ from the standard table. The First Shifting Theorem says: multiply $f(t)$ by $e^{at}$ in time domain → shift $s$ to $s-a$ in the transform. So $\mathcal{L}\{e^{3t}\sin(2t)\} = 2/((s-3)^2+4)$. Done. No integration. Just a substitution. This topic gives you five such shortcuts — once learned, they eliminate hours of integral computation.

---

## REQUIRED SECTIONS

### 1. Why This Topic Exists
"Before we begin, here is the honest answer to why you are reading this..."
The standard table covers only pure functions. Real engineering signals involve exponential multipliers, time delays, and time scaling. Without properties, every such function requires starting from the definition integral. Two-column booktabs table (Mistake | Consequence):
- "Ignoring the First Shifting Theorem" | "Spending 10 minutes on an integral that takes 10 seconds with the theorem"
- "Confusing s-shifting with t-shifting" | "Applying the wrong theorem and getting wrong answers"
- "Forgetting the unit step function in Second Shifting Theorem" | "Missing the u(t-a) multiplier in the answer"
End with a learnbox.

### 2. You Already Know This (Intuition First)
Compare to **phone number extensions**: the main office number is 1800-XXX-XXXX (F(s)), but dialling extension +3 means you add 3 to reach a different department (F(s-3)). Shifting the argument is like dialling a related but different destination. Similarly, multiplying by $e^{at}$ in the t-domain is just "dialling a different s-value."

### 3. Property 1 — First Shifting Theorem (s-Shifting)
Inside `infobox`:
**Theorem:** If $\mathcal{L}\{f(t)\} = F(s)$, then $\mathcal{L}\{e^{at}f(t)\} = F(s-a)$.

**Proof:** $\mathcal{L}\{e^{at}f(t)\} = \int_0^\infty e^{-st} e^{at} f(t)\, dt = \int_0^\infty e^{-(s-a)t} f(t)\, dt = F(s-a)$. Every step shown.

**Inverse form:** $\mathcal{L}^{-1}\{F(s-a)\} = e^{at}f(t)$.

Worked application: $\mathcal{L}\{e^{3t}\sin(2t)\}$ — show substitution step by step.

Booktabs table (5 rows): applying the theorem to $e^{at} \cdot 1$; $e^{at} \cdot t^n$; $e^{at}\sin(bt)$; $e^{at}\cos(bt)$; $e^{at} t^2$.

### 4. Property 2 — Second Shifting Theorem (t-Shifting)
Inside `infobox`:
**Unit Step Function:** $u(t-a) = \begin{cases} 0 & t < a \\ 1 & t \geq a \end{cases}$. $\mathcal{L}\{u(t-a)\} = e^{-as}/s$.

**Theorem:** If $\mathcal{L}\{f(t)\} = F(s)$, then $\mathcal{L}\{f(t-a) \cdot u(t-a)\} = e^{-as} F(s)$ for $a \geq 0$.

**Proof:** Substitution $\tau = t - a$ in the integral $\int_a^\infty e^{-st} f(t-a)\, dt$. Show all steps.

**Inverse form:** $\mathcal{L}^{-1}\{e^{-as}F(s)\} = f(t-a) \cdot u(t-a)$.

**pgfplots graph (MANDATORY):** Side-by-side: (Left) $f(t) = t^2$ for $t \geq 0$; (Right) $f(t-2)u(t-2) = (t-2)^2$ for $t \geq 2$, zero elsewhere. Clearly show the time delay of 2 units. Grid=major, labeled axes.

Worked example: find $\mathcal{L}\{(t-2)^2 u(t-2)\}$.

### 5. Property 3 — Change of Scale
Inside `infobox`:
**Theorem:** $\mathcal{L}\{f(at)\} = \frac{1}{a} F\!\left(\frac{s}{a}\right)$ for $a > 0$.

**Proof:** Substitution $u = at$ in the integral. Show all steps.

Worked example: given $\mathcal{L}\{\sin t\} = 1/(s^2+1)$, find $\mathcal{L}\{\sin(3t)\}$ using this property and verify against the standard table result $3/(s^2+9)$.

### 6. Property 4 — Multiplication by tⁿ (Introduction)
Inside `infobox`: State the property (full derivation is Topic 10):
$$\mathcal{L}\{t^n f(t)\} = (-1)^n \frac{d^n}{ds^n} F(s)$$
For $n=1$: $\mathcal{L}\{t f(t)\} = -F'(s)$.

Worked example: $\mathcal{L}\{t \sin(at)\} = -\frac{d}{ds}\left[\frac{a}{s^2+a^2}\right] = \frac{2as}{(s^2+a^2)^2}$. Show the differentiation step-by-step.

### 7. Property 5 — Division by t (Introduction)
Inside `infobox`: State the property (full derivation is Topic 11):
$$\mathcal{L}\!\left\{\frac{f(t)}{t}\right\} = \int_s^\infty F(u)\, du$$
Condition: $\lim_{t \to 0^+} f(t)/t$ must exist.

Worked example: given $\mathcal{L}\{\sin t\} = 1/(s^2+1)$, find $\mathcal{L}\{\sin t / t\} = \int_s^\infty \frac{du}{u^2+1} = \pi/2 - \arctan(s)$. Show all integral steps.

### 8. Summary Properties Table
Large booktabs table (7+ rows): Property Name | Formula | Validity/Notes.
Include: Linearity, First Shifting (s-shift), Second Shifting (t-shift), Change of Scale, Multiplication by t^n, Division by t, and one additional property of your choice.

### 9. Worked Examples
**Example 1:** Find $\mathcal{L}\{e^{-2t}\cos(3t)\}$ using First Shifting Theorem. Show every substitution step.
**Example 2:** Express the piecewise function $f(t) = \begin{cases} 0 & 0 \leq t < 1 \\ t-1 & t \geq 1 \end{cases}$ using unit step functions, then find its Laplace transform using the Second Shifting Theorem.
**Example 3:** Find $\mathcal{L}\{t^2 e^{-t}\}$ using the First Shifting Theorem applied to $\mathcal{L}\{t^2\} = 2/s^3$.

All examples inside `infobox`. End each with learnbox.

### 10. Excel Example (MANDATORY)
Numerically verify the First Shifting Theorem: compare $\mathcal{L}\{e^{2t}\sin(t)\}$ at $s=4$ using:
(a) Direct numerical integration of $e^{-4t} \cdot e^{2t} \sin(t)$ (columns: t | integrand | running sum)
(b) Formula result: $1/((4-2)^2 + 1) = 1/5 = 0.2$
Formulas: `=EXP(-4*A2)*EXP(2*A2)*SIN(A2)`, rows t=0 to t=6 in steps of 0.1.
End with learnbox confirming the theorem numerically.

### 11. Python Example (MANDATORY)
Provide a Python script using `sympy` that:
- Verifies First Shifting Theorem: computes $\mathcal{L}\{e^{at}f(t)\}$ symbolically and compares to F(s-a)
- Tests with $f(t) = \cos(bt)$, $f(t) = t^2$, $f(t) = \sin(bt)$ for symbolic $a$ and $b$
- Verifies Change of Scale property for $f(t) = e^{-t}$
Include expected printed output as comments. End with learnbox.

### 12. Viva-Style Oral Questions (8 questions with answers)
Cover: statement of First Shifting Theorem, proof idea, statement of Second Shifting Theorem, what $u(t-a)$ does, why $e^{-as}$ appears in t-shifting, Change of Scale formula, Multiplication by t formula, when Division by t is valid.

### 13. Descriptive Questions (5 exam-style questions)
Full written-answer: state and prove First Shifting Theorem, state and prove Second Shifting Theorem, derive Change of Scale property, find $\mathcal{L}\{te^{at}\}$ using multiplication by t, find $\mathcal{L}\{(1-\cos t)/t\}$ using division by t.

### 14. Practice Problems (6 problems with answer hints)
Problems: $\mathcal{L}\{e^{-3t}t^2\}$; $\mathcal{L}\{e^{t}\cos(2t)\}$; $\mathcal{L}\{(t-1)u(t-1)\}$; $\mathcal{L}\{t\cos(at)\}$ by multiplication by t; $\mathcal{L}\{(e^{at}-1)/t\}$ by division by t; $\mathcal{L}\{\sin(2t+\pi/3)\}$ (expand using trig identity, then use table).

### 15. MCQs (5 questions)
5 MCQs, bold correct answer, one-line explanation. Cover: First Shifting result, Second Shifting with unit step, Change of Scale formula, Multiplication by t formula, what happens to $e^{-as}$ in the second shifting theorem.

### 16. Common Mistakes Box
`mistakebox` tabular (5 rows): Mistake | What Students Do | Correct Approach.
- Applying First Shifting by shifting $t$ instead of $s$
- Forgetting $u(t-a)$ in the Second Shifting inverse
- Using Change of Scale without dividing by $a$
- Applying Division by t when $\lim_{t \to 0} f(t)/t$ does not exist
- Confusing $F(s-a)$ with $F(s+a)$ (sign of the shift)

### 17. Quick Recap
`learnbox` with 6--8 bullets: all five properties with compact formulas, the key trick of each, when to use which property, common pitfalls avoided.

---

## MANDATORY QUALITY CHECKLIST

- [ ] Opening hook present in `curiositybox`
- [ ] First and Second Shifting Theorems both proved, not just stated
- [ ] At least 1 pgfplots graph showing time delay (Second Shifting Theorem)
- [ ] Summary properties booktabs table with 7+ rows
- [ ] At least 1 Excel column-by-column example with cell formulas shown
- [ ] At least 1 Python lstlisting with verbatim output shown
- [ ] Every major example ends with a `learnbox` "What Did We Learn?"
- [ ] All four tcolorbox environments used at least once
- [ ] Piecewise function expressed using unit step functions
- [ ] `\end{document}` present at the very end
- [ ] All formulae in correct LaTeX syntax
