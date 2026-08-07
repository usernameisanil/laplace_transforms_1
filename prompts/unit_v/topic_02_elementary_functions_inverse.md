# Prompt — Topic 02: Elementary Functions (Inverse)

**Unit:** V — Inverse Laplace Transforms
**Course:** 23A54201 — Mathematics IV (Transform Techniques)
**University:** JNTUA College of Engineering (Autonomous)
**Target Audience:** B.Tech 2nd-year engineering students (non-mathematics majors)

---

## Prompt

You are an expert mathematics professor writing a **complete, compilable LaTeX (.tex) lecture note** for B.Tech engineering students on the topic **"Inverse Laplace Transforms of Elementary Functions"**. This is Topic 02 of Unit V. Students have the inverse transform definition, Lerch's theorem, linearity, and the standard table (Topic 01). This topic solidifies their ability to invert elementary $F(s)$ expressions — those directly matching the standard table entries, or those that can be reduced to table entries via simple algebra (completing the square, factoring, partial numerator splitting). This is the basic skill needed before tackling the more powerful partial fraction method in Topic 03.

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
- `\lhead{Topic 02: Elementary Functions (Inverse Laplace)}`
- `\rhead{Unit V --- Inverse Laplace Transforms}`
- `\cfoot{\thepage}`

Configure lstlisting for Python (same style as Unit IV).

Title page: `\title{Topic 02: Elementary Functions (Inverse Laplace Transform) \\ \large Unit V --- Inverse Laplace Transforms}`, `\maketitle`, `\tableofcontents`, `\newpage`.

---

## AUDIENCE AND TONE

Same as Unit IV: enthusiastic, conversational, encouraging voice. Students are now "reading transforms backwards" — help them build the pattern-recognition skills needed.

---

## OPENING HOOK (MANDATORY)

Place inside `\begin{curiositybox}{Hook}`: Pattern recognition is the core skill of inverse Laplace transforms. When you see $F(s) = 3/(s^2+9)$, you should immediately think: "that looks like $\sin(at)$ — specifically $\sin(3t)$, since $3/(s^2+9) = \sin(3t)$'s transform with $a=3$." When you see $F(s) = s/(s^2+16)$, you should think: "that's $\cos(4t)$." This topic drills exactly that pattern recognition — building the reflex to read a transform and know its inverse instantly. By the end, you will be able to invert any elementary $F(s)$ in seconds.

---

## REQUIRED SECTIONS

### 1. Why This Topic Exists
"Before we begin, here is the honest answer to why you are reading this..."
The standard table covers individual transforms, but real F(s) expressions often require adjustment before the table applies. Two-column booktabs table (Mistake | Consequence):
- "Not adjusting numerators before inverting" | "Writing $\mathcal{L}^{-1}\{s/(s^2+4)\}$ as $\sin(2t)$ instead of $\cos(2t)$"
- "Missing the factor of $a$ in the $\sin(at)$ numerator" | "Off-by-$a$ errors in every sinusoidal inverse"
- "Applying shifting before matching the base form" | "Identifying the wrong $f(t)$ before the exponential factor"
End with a learnbox.

### 2. You Already Know This (Intuition First)
Compare to recognizing faces: at first, all faces look different. With practice, you recognise patterns instantly. Similarly, with enough exposure to transform pairs, seeing $a/(s^2+a^2)$ instantly triggers "sin" and $s/(s^2+a^2)$ triggers "cos." This topic gives you the exposure.

### 3. Type 1 — Direct Table Lookup
Inside `infobox`: Cases where $F(s)$ directly matches a table entry. Work through 6 examples systematically:
- $\mathcal{L}^{-1}\{1/s\} = 1$ (identify and state)
- $\mathcal{L}^{-1}\{6/s^4\} = t^3$ (identify $n!/s^{n+1}$ pattern: $n=3$, $3! = 6$)
- $\mathcal{L}^{-1}\{1/(s-5)\} = e^{5t}$
- $\mathcal{L}^{-1}\{4/(s^2+16)\} = \sin(4t)$ (note: $a=4$, numerator must be $a$)
- $\mathcal{L}^{-1}\{s/(s^2+16)\} = \cos(4t)$ (note: numerator is $s$)
- $\mathcal{L}^{-1}\{3/(s^2-9)\} = \sinh(3t)$

For each: state the pattern, identify the parameters, write the result.

### 4. Type 2 — Numerator Adjustment
Inside `infobox`: When the numerator needs algebraic manipulation to match the standard form. Key: multiply and divide by the required constant.

Examples:
- $\mathcal{L}^{-1}\{1/(s^2+9)\}$: need $3/(s^2+9)$ for $\sin(3t)$. So $1/(s^2+9) = (1/3) \cdot 3/(s^2+9)$ → $(1/3)\sin(3t)$.
- $\mathcal{L}^{-1}\{1/s^3\}$: need $2!/s^3 = 2/s^3$ for $t^2$. So $1/s^3 = (1/2) \cdot 2/s^3$ → $t^2/2$.
- $\mathcal{L}^{-1}\{3/(s^2-25)\}$: need $5/(s^2-25)$ for $\sinh(5t)$. So $3/(s^2-25) = (3/5) \cdot 5/(s^2-25)$ → $(3/5)\sinh(5t)$.

Show the "multiply and divide" technique explicitly for each.

### 5. Type 3 — Using the First Shifting Theorem (s-Shift)
Inside `infobox`: When the denominator contains a shifted quadratic or linear factor in the form $(s-a)^n$.
$$\mathcal{L}^{-1}\{F(s-a)\} = e^{at} \mathcal{L}^{-1}\{F(s)\} = e^{at} f(t)$$

Examples:
- $\mathcal{L}^{-1}\{1/(s+3)^4\}$: match $1/(s-(-3))^4$ → $F(s) = 1/s^4$, $f(t) = t^3/6$. Result: $e^{-3t}t^3/6$.
- $\mathcal{L}^{-1}\{(s+2)/((s+2)^2+9)\}$: recognise $(s+2)$ shift in numerator and denominator → $\cos(3t)$ shifted → $e^{-2t}\cos(3t)$.
- $\mathcal{L}^{-1}\{1/((s-1)^2+4)\}$: $F(s) = 1/(s^2+4)$ → $f(t) = (1/2)\sin(2t)$. Result: $(1/2)e^{t}\sin(2t)$.

### 6. Type 4 — Completing the Square
Inside `infobox`: When the denominator is a quadratic $s^2 + bs + c$ that does NOT factor into real linear factors. Complete the square to reduce to the shift case.

General method:
$s^2 + bs + c = (s + b/2)^2 + (c - b^2/4)$. Let $a = b/2$, $\omega^2 = c - b^2/4$.

Three cases:
1. **Underdamped** ($c > b^2/4$): $\omega^2 > 0$ → result involves $e^{-at}\sin(\omega t)$ or $e^{-at}\cos(\omega t)$.
2. **Critically damped** ($c = b^2/4$): $\omega^2 = 0$ → result involves $te^{-at}$.
3. **Overdamped** ($c < b^2/4$): $\omega^2 < 0$ → factor as real factors, use partial fractions (Topic 03).

Full worked example for each case:
- Underdamped: $\mathcal{L}^{-1}\{1/(s^2+4s+13)\}$. Complete square: $(s+2)^2+9$. Result: $(1/3)e^{-2t}\sin(3t)$.
- Critically damped: $\mathcal{L}^{-1}\{1/(s^2+4s+4)\}$. Recognise $(s+2)^2$. Result: $te^{-2t}$.
- Numerator with $s$ term: $\mathcal{L}^{-1}\{(s+1)/(s^2+2s+5)\}$. Complete square: $(s+1)^2+4$. Numerator is $(s+1)$: directly $e^{-t}\cos(2t)$.

### 7. Splitting the Numerator Technique
Inside `infobox`: When the numerator has both $s$ and constant terms and the denominator is a shifted quadratic. Strategy: write $As + B = A(s+p) + (B - Ap)$ where $p$ comes from completing the square.

Full worked example: $\mathcal{L}^{-1}\{(2s+3)/(s^2+2s+5)\}$.
- Complete square: $(s+1)^2 + 4$
- Split numerator: $2s + 3 = 2(s+1) + 1$
- $\mathcal{L}^{-1}\{2(s+1)/((s+1)^2+4)\} + \mathcal{L}^{-1}\{1/((s+1)^2+4)\}$
- $= 2e^{-t}\cos(2t) + (1/2)e^{-t}\sin(2t)$

### 8. Visualizing Inverse Transforms
**pgfplots graph (MANDATORY):** Plot the three different damping cases on the same set of axes:
- Underdamped: $f(t) = (1/3)e^{-2t}\sin(3t)$ — oscillatory decay
- Critically damped: $f(t) = te^{-2t}$ — monotone decay with initial rise
- Overdamped: $f(t) = e^{-t} - e^{-3t}$ (representative example) — monotone decay
For $t \in [0, 4]$. Grid=major, legend, different colors, labeled axes. Caption: "The denominator structure of $F(s)$ determines the qualitative behavior of the inverse transform."

### 9. Worked Examples
**Example 1:** Find $\mathcal{L}^{-1}\left\{\frac{3s+5}{s^2+6s+25}\right\}$.
**Example 2:** Find $\mathcal{L}^{-1}\left\{\frac{2}{(s+1)^3}\right\}$.
**Example 3:** Find $\mathcal{L}^{-1}\left\{\frac{4}{s^2-16} + \frac{3s}{s^2+16}\right\}$ using linearity and the standard table.

All examples inside `infobox`. End each with learnbox.

### 10. Quick Reference: Pattern Recognition Guide
Booktabs table (10+ rows): $F(s)$ Pattern | Action Required | Result $f(t)$.
This is a cheat-sheet style table covering all cases from Sections 3--7 with the matching process summarised.

### 11. Excel Example (MANDATORY)
Numerically verify that $\mathcal{L}^{-1}\{1/(s^2+4s+13)\} = (1/3)e^{-2t}\sin(3t)$:
Compare numerically computed $\mathcal{L}\{f(t)\}$ at $s=2$ to $F(2) = 1/(4+8+13) = 1/25 = 0.04$:
- Columns: t | $f(t) = (1/3)e^{-2t}\sin(3t)$ | $e^{-2t}f(t)$ | Cumulative Trapezoid Sum
- Formulas: `=(1/3)*EXP(-2*A2)*SIN(3*A2)`, `=EXP(-2*A2)*B2`, trapezoid rule
- Rows: t=0 to t=6 in steps of 0.1
End with learnbox confirming convergence to $1/25 = 0.04$.

### 12. Python Example (MANDATORY)
Provide a Python script using `sympy` that:
- Computes $\mathcal{L}^{-1}$ for all four types (direct, adjusted numerator, s-shifted, completed square)
- Uses `sympy.inverse_laplace_transform` for each
- Also numerically plots all three damping cases using matplotlib
Include expected printed output as comments. End with learnbox.

### 13. Viva-Style Oral Questions (8 questions with answers)
Cover: Type 1 pattern recognition, numerator adjustment method, the shift theorem for inverse, completing the square procedure, the three damping cases, numerator splitting technique, $\mathcal{L}^{-1}\{s/(s^2+a^2)\}$ vs. $\mathcal{L}^{-1}\{a/(s^2+a^2)\}$, what critically damped means physically.

### 14. Descriptive Questions (5 exam-style questions)
Full written-answer: find $\mathcal{L}^{-1}\{(3s-1)/(s^2+4s+20)\}$ fully, explain all four types with one example each, find $\mathcal{L}^{-1}\{(s+4)/(s^2+8s+16)\}$, apply numerator splitting to a general $F(s) = (As+B)/(s^2+2\alpha s + \omega_0^2)$, explain the three damping cases and their physical interpretation.

### 15. Practice Problems (6 problems with answer hints)
Problems: $\mathcal{L}^{-1}\{5/s^5\}$; $\mathcal{L}^{-1}\{2/(s^2-4)\}$; $\mathcal{L}^{-1}\{(s+3)/((s+3)^2+16)\}$; $\mathcal{L}^{-1}\{(2s+1)/(s^2+4s+5)\}$; $\mathcal{L}^{-1}\{3/(s+2)^4\}$; $\mathcal{L}^{-1}\{1/(4s^2+4s+5)\}$ (divide through by 4 first).

### 16. MCQs (5 questions)
5 MCQs, bold correct answer, one-line explanation. Cover: $\mathcal{L}^{-1}\{1/(s^2+9)\}$, numerator adjustment factor, completing the square result, critically damped form, shift theorem direction.

### 17. Common Mistakes Box
`mistakebox` tabular (5 rows): Mistake | What Students Do | Correct Approach.
- Writing $\mathcal{L}^{-1}\{1/(s^2+9)\} = \sin(3t)$ (missing the $1/3$ factor from numerator adjustment)
- Using the wrong denominator form for cosh vs cos
- Forgetting to carry the exponential $e^{at}$ after applying the shift
- Not splitting the numerator when it has both $s$ and constant parts
- Completing the square incorrectly (arithmetic error in $b/2$ and $c - b^2/4$)

### 18. Quick Recap
`learnbox` with 6--8 bullets: four types of elementary inverse, numerator adjustment rule, completing the square procedure, three damping cases, numerator splitting technique, the pattern recognition approach.

---

## MANDATORY QUALITY CHECKLIST

- [ ] Opening hook present in `curiositybox`
- [ ] All four types (direct, numerator adjust, s-shift, complete square) covered with worked examples
- [ ] Three damping cases shown explicitly
- [ ] Numerator splitting technique demonstrated fully
- [ ] At least 1 pgfplots graph showing all three damping cases on same axes
- [ ] Pattern recognition guide as booktabs table (10+ rows)
- [ ] At least 1 Excel column-by-column example with cell formulas shown
- [ ] At least 1 Python lstlisting with verbatim output shown
- [ ] Every major example ends with a `learnbox` "What Did We Learn?"
- [ ] All four tcolorbox environments used at least once
- [ ] `\end{document}` present at the very end
- [ ] All formulae in correct LaTeX syntax
