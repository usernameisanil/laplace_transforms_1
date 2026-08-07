# Prompt — Topic 03: Transforms of Elementary Functions

**Unit:** IV — Laplace Transforms  
**Course:** 23A35101 — Numerical & Statistical Methods  
**University:** JNTUA College of Engineering (Autonomous)  
**Target Audience:** B.Tech 2nd-year engineering students (non-mathematics majors)  

---

## Prompt

You are an expert mathematics professor writing a **complete, compilable LaTeX (.tex) lecture note** for B.Tech engineering students on the topic **"Transforms of Elementary Functions"**. This is Topic 03 of Unit IV. Students have completed Topics 01 and 02 — they know the definition, linearity, and existence conditions. Now they build the standard Laplace transform table from first principles. Write as a methodical, encouraging teacher who derives each entry carefully so students understand where the table comes from, not just how to look it up.

---

## LATEX SETUP REQUIREMENTS

Use this exact preamble:

```latex
\documentclass[12pt,a4paper]{article}
\usepackage{amsmath, amssymb, geometry, booktabs, xcolor, hyperref,
            listings, pgfplots, tcolorbox, enumitem, fancyhdr, tikz, array}
\geometry{margin=2.5cm}
\pgfplotsset{compat=1.18}
\tcbuselibrary{skins, breakable}
```

Define four tcolorbox environments:
- `curiositybox` — colback=yellow!10, colframe=orange!80
- `infobox` — colback=blue!5, colframe=blue!60
- `mistakebox` — colback=red!5, colframe=red!60
- `learnbox` — colback=green!5, colframe=green!60

fancyhdr: `\lhead{Topic 03: Transforms of Elementary Functions}`, `\rhead{Unit IV — Laplace Transforms}`, `\cfoot{\thepage}`

Title page: Topic 03 title, subtitle "Unit IV — Laplace Transforms". Then `\tableofcontents` and `\newpage`.

---

## AUDIENCE AND TONE

Students will use this transform table for the rest of the course. The goal is not memorisation — it is **understanding each derivation** so students can reproduce or extend entries when needed. Use the analogy of building a reference dictionary: we are writing each entry from scratch, not copying it from somewhere.

---

## OPENING HOOK (MANDATORY)

In `curiositybox[Hook]`: Every engineer who uses Laplace Transforms relies on a table. But what happens when your exam gives you a function not in the table? If you memorised the table, you are stuck. If you understood the derivations, you can derive any new entry in minutes. This topic teaches you how every row of the table was born — from the definition. By the end, the table will feel like something you built yourself.

---

## REQUIRED SECTIONS

### 1. Why This Topic Exists
Open with the standard opener. Two-column booktabs table (4 rows):
- "Only memorising the table" | "Unable to handle composite functions or new variants"
- "Skipping derivations" | "Cannot verify a table entry or correct a misprint"
- "Not learning conditions on $s$" | "Applying transforms outside their valid region"
- "Not building the full table now" | "Struggling in all subsequent topics that reference it"
End with learnbox.

### 2. Recap: What We Already Know
Quick one-paragraph summary of Topics 01–02. Remind students:
- Definition: $\mathcal{L}\{f(t)\} = \int_0^\infty e^{-st} f(t)\,dt$
- Linearity: $\mathcal{L}\{af + bg\} = aF(s) + bG(s)$
- Already derived: $\mathcal{L}\{1\} = 1/s$, $\mathcal{L}\{t\} = 1/s^2$, $\mathcal{L}\{e^{at}\} = 1/(s-a)$

### 3. Derivation 1 — L{t^n} for positive integer n
Place result in `infobox`:
$$\mathcal{L}\{t^n\} = \frac{n!}{s^{n+1}}, \quad s > 0$$
Derivation using mathematical induction or repeated integration by parts:
- Base case: $\mathcal{L}\{t^0\} = \mathcal{L}\{1\} = 1/s$ ✓
- Show $\mathcal{L}\{t^n\} = \frac{n}{s}\mathcal{L}\{t^{n-1}\}$ by IBP
- Inductive step leads to $n!/s^{n+1}$
- Worked numerical example: $\mathcal{L}\{t^3\} = 6/s^4$, $\mathcal{L}\{t^5\} = 120/s^6$
End with `learnbox`.

### 4. Derivation 2 — L{sin(at)}
Place result in `infobox`:
$$\mathcal{L}\{\sin(at)\} = \frac{a}{s^2 + a^2}, \quad s > 0$$
Two methods — choose the cleaner one and show fully:
- **Method A (IBP twice):** Apply IBP to $\int_0^\infty e^{-st}\sin(at)\,dt$. After two IBPs, the original integral reappears — solve algebraically.
- **Method B (Euler's formula):** Write $\sin(at) = \text{Im}(e^{iat})$, use $\mathcal{L}\{e^{iat}\} = 1/(s-ia)$, take imaginary part.
Show all algebraic steps. Verify: at $a=1, s=1$: $F(1) = 1/2$.
End with `learnbox`.

### 5. Derivation 3 — L{cos(at)}
Place result in `infobox`:
$$\mathcal{L}\{\cos(at)\} = \frac{s}{s^2 + a^2}, \quad s > 0$$
Derivation:
- Use differentiation: if $\mathcal{L}\{\sin(at)\} = a/(s^2+a^2)$, then using $\sin(at) = -\frac{1}{a}\frac{d}{dt}\cos(at)$ and the derivative formula $\mathcal{L}\{f'\} = sF(s) - f(0)$ (preview of Topic 07)
- OR use Euler's formula Method B: take real part of $\mathcal{L}\{e^{iat}\}$
- Verify: at $a=1$: $\mathcal{L}\{\cos(t)\} = s/(s^2+1)$; check $F(s) \to 0$ as $s \to \infty$ ✓
End with `learnbox`.

### 6. Derivation 4 — L{sinh(at)} and L{cosh(at)}
Place results in `infobox`:
$$\mathcal{L}\{\sinh(at)\} = \frac{a}{s^2 - a^2}, \quad s > |a|$$
$$\mathcal{L}\{\cosh(at)\} = \frac{s}{s^2 - a^2}, \quad s > |a|$$
Derivation:
- Use definitions: $\sinh(at) = (e^{at} - e^{-at})/2$, $\cosh(at) = (e^{at} + e^{-at})/2$
- Apply linearity and $\mathcal{L}\{e^{\pm at}\} = 1/(s \mp a)$
- Show all fraction arithmetic clearly
- **Key difference from trig:** denominator is $s^2 - a^2$ (not $+a^2$); condition $s > |a|$ (not just $s > 0$)
- `mistakebox`: Students confuse $s^2 + a^2$ (trig) with $s^2 - a^2$ (hyperbolic). Mnemonic: **h**yperbolic → **h**as minus sign.
End with `learnbox`.

### 7. The Complete Standard Transform Table
Present a comprehensive, well-formatted booktabs table (12+ rows):

| No. | $f(t)$ | $F(s) = \mathcal{L}\{f(t)\}$ | Condition |
|-----|--------|-------------------------------|------------|
| 1 | $1$ | $1/s$ | $s > 0$ |
| 2 | $t$ | $1/s^2$ | $s > 0$ |
| 3 | $t^n$ ($n \in \mathbb{Z}^+$) | $n!/s^{n+1}$ | $s > 0$ |
| 4 | $e^{at}$ | $1/(s-a)$ | $s > a$ |
| 5 | $\sin(at)$ | $a/(s^2+a^2)$ | $s > 0$ |
| 6 | $\cos(at)$ | $s/(s^2+a^2)$ | $s > 0$ |
| 7 | $\sinh(at)$ | $a/(s^2-a^2)$ | $s > |a|$ |
| 8 | $\cosh(at)$ | $s/(s^2-a^2)$ | $s > |a|$ |
| 9 | $t^n e^{at}$ | $n!/(s-a)^{n+1}$ | $s > a$ |
| 10 | $e^{at}\sin(bt)$ | $b/((s-a)^2+b^2)$ | $s > a$ |
| 11 | $e^{at}\cos(bt)$ | $(s-a)/((s-a)^2+b^2)$ | $s > a$ |
| 12 | $t\sin(at)$ | $2as/(s^2+a^2)^2$ | $s > 0$ |

Note: rows 9–12 will be fully derived in Topic 04 (Properties) using the shifting theorem. Mark them "[see Topic 04]" in the Condition column.

### 8. How to Use the Table — Worked Examples

**Example 1:** Find $\mathcal{L}\{4\sin(3t) - 2\cos(t) + 5e^{-2t}\}$
Use linearity + table rows 5, 6, 4. Show each step. Final answer in simplified form.

**Example 2:** Find $\mathcal{L}\{\cosh(2t) - \sinh(2t)\}$
Use rows 7, 8. Simplify: $\cosh(2t) - \sinh(2t) = e^{-2t}$ — verify by direct use of row 4. This shows internal consistency of the table.

**Example 3:** Find $\mathcal{L}\{(t+1)^3\}$
Expand $(t+1)^3 = t^3 + 3t^2 + 3t + 1$. Apply linearity and rows 1, 2, 3.

**Example 4:** Find $\mathcal{L}\{\sin^2(t)\}$
Use identity: $\sin^2(t) = (1 - \cos(2t))/2$. Apply linearity and rows 1, 6. This shows table is insufficient alone — identities are needed.

All in `infobox`. Each ends with `learnbox`.

### 9. pgfplots Graphs (MANDATORY)
Plot pairs to show trig vs. hyperbolic contrast:
- Panel 1: $\sin(t)$ and $\cos(t)$ on $[0, 4\pi]$ — oscillatory, bounded
- Panel 2: $\sinh(t)$ and $\cosh(t)$ on $[0, 3]$ — growing, unbounded
Label axes, add legend, grid=major. Caption: "Trig functions are bounded (transform exists for $s>0$); hyperbolic functions grow exponentially (need $s > |a|$)."

### 10. Excel Example (MANDATORY)
Numerically verify $\mathcal{L}\{\sin(2t)\}$ at $s=3$ using Riemann sum:
- Columns: $t_i$ | $\sin(2t_i)$ | $e^{-3t_i}$ | product | $\Delta t$ | contribution
- Formulas: `=SIN(2*A2)`, `=EXP(-3*A2)`, `=C2*B2`, `=D2*$E$1`
- `=SUM(F2:F500)` ≈ analytical value $2/(9+4) = 2/13 \approx 0.1538$
End with `learnbox`.

### 11. Python Example (MANDATORY)
Python script that:
- Uses `sympy.laplace_transform` to compute $\mathcal{L}$ of all 8 elementary functions symbolically
- Prints result and condition for each
- Also numerically verifies $\mathcal{L}\{\cos(3t)\}$ at $s=5$ using `scipy.integrate.quad`
- Expected: $5/(25+9) = 5/34 \approx 0.1471$
Include expected output as comments. End with `learnbox`.

### 12. Viva-Style Oral Questions (8 questions)
1. State $\mathcal{L}\{t^n\}$ and derive it for $n=2$ from first principles.
2. What is the denominator for $\mathcal{L}\{\sin(at)\}$? How does it differ from $\mathcal{L}\{\sinh(at)\}$?
3. Derive $\mathcal{L}\{\cosh(at)\}$ using the definition of $\cosh$.
4. For what values of $s$ does $\mathcal{L}\{\sinh(5t)\}$ exist?
5. Find $\mathcal{L}\{e^{-3t}\}$ and state the ROC.
6. What is $\mathcal{L}\{\cos(0 \cdot t)\} = \mathcal{L}\{1\}$? Verify using the $\cos$ formula.
7. Why is the condition for $\mathcal{L}\{\cosh(at)\}$ written as $s > |a|$ and not $s > a$?
8. How would you compute $\mathcal{L}\{\sin^2(t)\}$ without adding a new row to the table?

### 13. Descriptive Questions (5 questions)
1. Derive $\mathcal{L}\{\sin(at)\}$ from first principles using integration by parts. State all steps.
2. Derive $\mathcal{L}\{t^n\}$ using mathematical induction.
3. Show that $\mathcal{L}\{\cosh(at)\} - \mathcal{L}\{\sinh(at)\} = \mathcal{L}\{e^{-at}\}$ and verify algebraically.
4. Find $\mathcal{L}\{3\cos(2t) - 2\sin(3t) + e^{4t}\}$. State conditions on $s$.
5. Explain why the denominator changes from $s^2+a^2$ to $s^2-a^2$ when moving from $\sin(at)$ to $\sinh(at)$.

### 14. Practice Problems (6 problems with hints)
1. $\mathcal{L}\{t^4\}$ [Answer: $24/s^5$]
2. $\mathcal{L}\{5\cos(4t)\}$ [Answer: $5s/(s^2+16)$]
3. $\mathcal{L}\{e^{2t} + \sinh(3t)\}$ [Answer: $1/(s-2) + 3/(s^2-9)$; state conditions]
4. $\mathcal{L}\{\sin(t)\cos(t)\}$ [Hint: use $\sin(2t)/2$; Answer: $1/(s^2+4)$]
5. $\mathcal{L}\{(e^t - e^{-t})^2\}$ [Hint: expand; Answer: use linearity]
6. $\mathcal{L}\{\cos^2(2t)\}$ [Hint: use $\cos^2 = (1+\cos(4t))/2$]

### 15. MCQs (5 questions)
5 MCQs with 4 options. Bold correct answer. One-line explanation.
Cover: $\mathcal{L}\{t^2\}$, denominator of $\mathcal{L}\{\sin\}$ vs $\mathcal{L}\{\sinh\}$, condition for $\mathcal{L}\{\cosh(3t)\}$, linearity application, table lookup.

### 16. Common Mistakes Box
`mistakebox` tabular (5 rows):
- Confusing $s^2+a^2$ (trig) and $s^2-a^2$ (hyperbolic)
- Forgetting $n!$ in $\mathcal{L}\{t^n\} = n!/s^{n+1}$ (writing $1/s^{n+1}$ instead)
- Applying $\mathcal{L}\{\cosh(at)\}$ formula when $s \leq a$ (outside ROC)
- Not using trig identities before applying Laplace (trying $\mathcal{L}\{\sin^2\}$ directly)
- Mixing up $\mathcal{L}\{e^{at}\} = 1/(s-a)$ sign: writing $1/(s+a)$ for positive $a$

### 17. Quick Recap
`learnbox` with 8 bullets covering all 8 elementary transform pairs, their conditions, and the key mnemonic (trig: $+a^2$; hyperbolic: $-a^2$).

---

## MANDATORY QUALITY CHECKLIST

- [ ] Opening hook in `curiositybox`
- [ ] All 8 elementary functions derived (not just stated)
- [ ] Full booktabs transform table with 12+ rows
- [ ] At least 1 pgfplots graph (trig vs hyperbolic comparison)
- [ ] At least 4 worked examples using the table
- [ ] Excel numerical verification with formulas shown
- [ ] Python with `sympy` symbolic and `scipy` numerical verification
- [ ] All four tcolorbox environments used
- [ ] `mistakebox` for trig/hyperbolic confusion
- [ ] Every derived result placed in `infobox`
- [ ] `\end{document}` at the end
- [ ] Conditions on $s$ stated explicitly for every transform pair
