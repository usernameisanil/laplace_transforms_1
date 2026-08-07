# Prompt — Topic 04: Properties of Laplace Transforms

**Unit:** IV — Laplace Transforms  
**Course:** 23A35101 — Numerical & Statistical Methods  
**University:** JNTUA College of Engineering (Autonomous)  
**Target Audience:** B.Tech 2nd-year engineering students (non-mathematics majors)  

---

## Prompt

You are an expert mathematics professor writing a **complete, compilable LaTeX (.tex) lecture note** for B.Tech engineering students on the topic **"Properties of Laplace Transforms"**. This is Topic 04 of Unit IV. Students have completed Topics 01–03 and have the standard transform table. Now they learn the rules that allow them to compute transforms of complex functions by combining known simple ones — without re-deriving from the definition each time. Write as an enthusiastic teacher who shows how each property is a power-up that extends the table dramatically.

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

fancyhdr: `\lhead{Topic 04: Properties of Laplace Transforms}`, `\rhead{Unit IV — Laplace Transforms}`, `\cfoot{\thepage}`

Title page: Topic 04 title, subtitle "Unit IV — Laplace Transforms". Then `\tableofcontents` and `\newpage`.

---

## AUDIENCE AND TONE

Students have the basic table but feel limited. Show them how each property multiplies the power of the table. Use the analogy of cheat codes in a game: the basic table is the character, each property is an upgrade. By the end of this topic, they can handle functions the table never explicitly listed.

---

## OPENING HOOK (MANDATORY)

In `curiositybox[Hook]`: You can find $\mathcal{L}\{\sin(3t)\}$ using the table. But what about $\mathcal{L}\{e^{-2t}\sin(3t)\}$? Or $\mathcal{L}\{t^2\cos(4t)\}$? Or $\mathcal{L}\{\sin(3(t-2))u(t-2)\}$? None of these are directly in the table. But once you learn the four properties in this topic, every single one of these becomes a one-line calculation. The properties are the real power of the Laplace Transform.

---

## REQUIRED SECTIONS

### 1. Why This Topic Exists
Open with the standard opener. Two-column booktabs table (4 rows):
- "Only using the basic table" | "Unable to handle $e^{at}f(t)$, $f(t-a)$, or $t^n f(t)$ variants"
- "Not learning proofs" | "Cannot adapt properties to new situations"
- "Skipping change of scale" | "Stuck when frequency is scaled"
- "Not linking properties to each other" | "Missing the unified structure of the transform"
End with learnbox.

### 2. Property 1 — Linearity (Recap and Formalise)
Place in `infobox`:
$$\mathcal{L}\{\alpha f(t) + \beta g(t)\} = \alpha F(s) + \beta G(s)$$
- Brief proof (already done in Topic 01 — just reference and state cleanly).
- Example: $\mathcal{L}\{3e^{2t} - 4\sin(t) + 7\}$ — apply linearity directly, cite table rows.
- Emphasise: this is the workhorse of all computations.
End with `learnbox`.

### 3. Property 2 — First Shifting Theorem (s-Shifting)
Place in prominent `infobox`:

**Theorem:** If $\mathcal{L}\{f(t)\} = F(s)$, then:
$$\mathcal{L}\{e^{at} f(t)\} = F(s - a)$$

- **Proof:** Substitute directly into the definition:
$$\mathcal{L}\{e^{at}f(t)\} = \int_0^\infty e^{-st} e^{at} f(t)\,dt = \int_0^\infty e^{-(s-a)t} f(t)\,dt = F(s-a)$$
- **Interpretation:** Multiplying $f(t)$ by $e^{at}$ in the time domain shifts $F(s)$ to $F(s-a)$ in the $s$-domain — replace every $s$ with $s-a$.
- **Worked examples (3 examples, all in `infobox`):**
  - $\mathcal{L}\{e^{3t}\sin(2t)\} = \frac{2}{(s-3)^2+4}$
  - $\mathcal{L}\{e^{-t}\cos(4t)\} = \frac{s+1}{(s+1)^2+16}$
  - $\mathcal{L}\{e^{2t}t^3\} = \frac{6}{(s-2)^4}$
- `mistakebox`: Students replace $s$ with $s+a$ when they should replace with $s-a$ for $e^{at}$. Mnemonic: $e^{at}$ shifts the graph of $F(s)$ to the **right** by $a$ (since we need $s > a$ for convergence).
- **Connection to Table:** This explains rows 9–11 of Topic 03 table (the $e^{at}f(t)$ entries).
End with `learnbox`.

### 4. Property 3 — Second Shifting Theorem (t-Shifting)
Place in prominent `infobox`:

**Theorem:** If $\mathcal{L}\{f(t)\} = F(s)$, then for $a > 0$:
$$\mathcal{L}\{f(t-a)\, u(t-a)\} = e^{-as} F(s)$$

where $u(t-a)$ is the **unit step function** (Heaviside): $u(t-a) = 0$ for $t < a$, $1$ for $t \geq a$.

- **Proof by substitution:** Let $\tau = t - a$, so $t = \tau + a$, $dt = d\tau$:
$$\int_0^\infty e^{-st} f(t-a)u(t-a)\,dt = \int_a^\infty e^{-st}f(t-a)\,dt = \int_0^\infty e^{-s(\tau+a)}f(\tau)\,d\tau = e^{-as}F(s)$$
- **Interpretation:** A time-delay of $a$ in the $t$-domain multiplies $F(s)$ by $e^{-as}$ in the $s$-domain.
- **Key point:** The function must be written as $f(t-a) \cdot u(t-a)$ — not just $f(t-a)$. Show how to rewrite functions into this form.
- **Worked examples (3 examples, all in `infobox`):**
  - $\mathcal{L}\{(t-2)^2 u(t-2)\}$: use $f(t) = t^2$, $F(s) = 2/s^3$, result: $2e^{-2s}/s^3$
  - $\mathcal{L}\{\sin(t-\pi)u(t-\pi)\}$: $f(t) = \sin(t)$, result: $e^{-\pi s}/(s^2+1)$
  - Express $g(t) = \begin{cases}0 & t < 3 \\ (t-3)^2 & t \geq 3\end{cases}$ as $f(t-3)u(t-3)$ and find $\mathcal{L}\{g\}$
- `mistakebox`: Students apply this theorem to $f(t)u(t-a)$ (without shifting the argument) — result is WRONG. Must first rewrite as $f(t-a)u(t-a)$ by shifting the function.
- **pgfplots graph (MANDATORY):** Show $f(t) = t^2$ and its delayed version $f(t-2)u(t-2)$ on the same axes. Clearly show the zero region $[0, 2)$ and the shifted parabola. Label axes, add grid=major.
End with `learnbox`.

### 5. Property 4 — Change of Scale
Place in `infobox`:

**Theorem:** If $\mathcal{L}\{f(t)\} = F(s)$, then:
$$\mathcal{L}\{f(at)\} = \frac{1}{a} F\!\left(\frac{s}{a}\right), \quad a > 0$$

- **Proof:** Substitute $u = at$, $t = u/a$, $dt = du/a$:
$$\int_0^\infty e^{-st} f(at)\,dt = \int_0^\infty e^{-s(u/a)} f(u) \frac{du}{a} = \frac{1}{a}F\!\left(\frac{s}{a}\right)$$
- **Interpretation:** Scaling time by $a$ scales the $s$-variable by $1/a$ and scales the amplitude by $1/a$.
- **Worked examples (2 examples):**
  - $\mathcal{L}\{\sin(3t)\}$: use $\mathcal{L}\{\sin(t)\} = 1/(s^2+1)$, apply scale with $a=3$: $\frac{1}{3} \cdot \frac{1}{(s/3)^2+1} = \frac{3}{s^2+9}$ ✓ (matches table)
  - $\mathcal{L}\{e^{2t}\}$: use $\mathcal{L}\{e^t\} = 1/(s-1)$, apply scale with $a=2$: $\frac{1}{2} \cdot \frac{1}{s/2-1} = \frac{1}{s-2}$ ✓
End with `learnbox`.

### 6. Properties Summary Table
Present all four properties in a single clean booktabs table:

| Property | Time Domain | $s$-Domain | Proof Method |
|---|---|---|---|
| Linearity | $\alpha f + \beta g$ | $\alpha F(s) + \beta G(s)$ | Linearity of integral |
| First Shifting ($s$-shift) | $e^{at}f(t)$ | $F(s-a)$ | Direct substitution |
| Second Shifting ($t$-shift) | $f(t-a)u(t-a)$ | $e^{-as}F(s)$ | Substitution $\tau = t-a$ |
| Change of Scale | $f(at)$ | $\frac{1}{a}F(s/a)$ | Substitution $u = at$ |

### 7. Combined Applications — Advanced Examples

**Example 1:** $\mathcal{L}\{e^{-3t}(2\cos(4t) - 5\sin(4t))\}$
Step 1: Linearity. Step 2: First shifting theorem applied to each term.
Final answer: $\dfrac{2(s+3)}{(s+3)^2+16} - \dfrac{20}{(s+3)^2+16}$

**Example 2:** $\mathcal{L}\{(2t-1)^2 u(2t-1)\}$  
Rewrite: $2t-1 = 2(t-1/2)$. Apply second shifting with $a=1/2$, then change of scale.

**Example 3:** $\mathcal{L}\{e^{2t}\sin^2(t)\}$  
Step 1: $\sin^2(t) = (1 - \cos(2t))/2$. Step 2: Linearity. Step 3: First shifting.

All in `infobox`. Each ends with `learnbox`.

### 8. Differentiation in the s-Domain (Preview of Topic 09)
Place in `infobox` as a forward-reference:
$$\mathcal{L}\{t\, f(t)\} = -\frac{d}{ds}F(s) \quad \Rightarrow \quad \mathcal{L}\{t^n f(t)\} = (-1)^n \frac{d^n}{ds^n}F(s)$$
- Derive the $n=1$ case: differentiate $F(s) = \int_0^\infty e^{-st}f(t)dt$ under the integral sign w.r.t. $s$.
- One worked example: $\mathcal{L}\{t\sin(2t)\} = -\frac{d}{ds}\frac{2}{s^2+4} = \frac{4s}{(s^2+4)^2}$
- Note: full treatment in Topic 09 (Multiplication by t). This is just a preview.

### 9. pgfplots Visualization (MANDATORY)
Two panels:
- Panel 1: $F(s) = 1/(s^2+1)$ and its shifted version $F(s-2) = 1/(s-2)^2+1$ on the same axes — visual demonstration of the First Shifting Theorem in the $s$-domain.
- Panel 2: $f(t) = \sin(t)$ and $f(t-2)u(t-2)$ on the same $t$-axis — visual demonstration of the Second Shifting Theorem in the time domain.
Label axes, add legend and grid=major for both panels.

### 10. Excel Example (MANDATORY)
Numerically verify the First Shifting Theorem:
- Compute $\mathcal{L}\{e^{2t}\sin(3t)\}$ at $s=5$ numerically using Riemann sum
- Analytical: $3/((5-2)^2+9) = 3/(9+9) = 3/18 = 1/6 \approx 0.1667$
- Columns: $t_i$ | $e^{2t_i}$ | $\sin(3t_i)$ | product | $e^{-5t_i}$ | integrand | $\Delta t$ | contribution
- Formula: `=EXP(2*A2)*SIN(3*A2)*EXP(-5*A2)`
End with `learnbox`.

### 11. Python Example (MANDATORY)
Python script using `sympy`:
- Symbolically verify all four properties for specific functions
- Test First Shifting: $\mathcal{L}\{e^{3t}\cos(2t)\}$ — compute directly and via $F(s-3)$
- Test Second Shifting: $\mathcal{L}\{(t-1)^2 u(t-1)\}$ — compute and compare with $e^{-s} \cdot 2/s^3$
- Print results side-by-side confirming equality
Include expected output as comments. End with `learnbox`.

### 12. TikZ Property Map (MANDATORY)
Draw a TikZ concept map:
- Centre node: "Laplace Transform Table"
- Four surrounding nodes: "+ Linearity", "+ s-Shifting", "+ t-Shifting", "+ Scale Change"
- Each node has an arrow labelled with what new class of functions it unlocks:
  - Linearity → "Linear combinations"
  - s-Shifting → "Exponentially modulated functions: $e^{at}f(t)$"
  - t-Shifting → "Time-delayed functions: $f(t-a)u(t-a)$"
  - Scale → "Frequency-scaled functions: $f(at)$"

### 13. Viva-Style Oral Questions (8 questions)
1. State the First Shifting Theorem and give one example.
2. State the Second Shifting Theorem. What is the role of $u(t-a)$?
3. What is the difference between $s$-shifting and $t$-shifting?
4. If $\mathcal{L}\{f(t)\} = F(s)$, what is $\mathcal{L}\{e^{-5t}f(t)\}$?
5. Why must the function be written as $f(t-a)u(t-a)$ and not $f(t)u(t-a)$?
6. Prove the change of scale theorem.
7. Find $\mathcal{L}\{t\sin(at)\}$ using differentiation in $s$.
8. If $\mathcal{L}\{\cos(2t)\} = s/(s^2+4)$, find $\mathcal{L}\{e^{3t}\cos(2t)\}$.

### 14. Descriptive Questions (5 questions)
1. State and prove the First Shifting Theorem (s-shifting). Apply it to find $\mathcal{L}\{e^{2t}\sin(3t)\}$.
2. State and prove the Second Shifting Theorem (t-shifting). Find $\mathcal{L}\{(t-3)^2 u(t-3)\}$.
3. Prove the change of scale property. Verify using $\mathcal{L}\{\cos(at)\}$.
4. Find $\mathcal{L}\{e^{-t}(3\cos(2t) - 2\sin(2t))\}$ using the First Shifting Theorem.
5. Express the function $g(t) = \begin{cases}0 & 0 \leq t < \pi \\ \sin(t-\pi) & t \geq \pi\end{cases}$ using the unit step function and find its Laplace Transform.

### 15. Practice Problems (6 problems with hints)
1. $\mathcal{L}\{e^{4t}t^2\}$ [Answer: $2/(s-4)^3$]
2. $\mathcal{L}\{e^{-2t}\cos(5t)\}$ [Answer: $(s+2)/((s+2)^2+25)$]
3. $\mathcal{L}\{(t-1)^3 u(t-1)\}$ [Answer: $6e^{-s}/s^4$]
4. $\mathcal{L}\{\sin(2(t-\pi/4))u(t-\pi/4)\}$ [Answer: $2e^{-\pi s/4}/(s^2+4)$]
5. $\mathcal{L}\{\cos(3t)\}$ via Change of Scale from $\mathcal{L}\{\cos(t)\}$ [Answer: $s/(s^2+9)$]
6. $\mathcal{L}\{e^{3t}\sin^2(t)\}$ [Hint: trig identity first, then s-shift]

### 16. MCQs (5 questions)
5 MCQs. Bold correct answer. One-line explanation.
Cover: what $e^{at}$ does in s-domain, result of $t$-shift, change of scale formula, combined property application, unit step function role.

### 17. Common Mistakes Box
`mistakebox` tabular (5 rows):
- Shifting $s$ in the wrong direction: $F(s+a)$ instead of $F(s-a)$ for $e^{at}$
- Applying $t$-shift to $f(t)u(t-a)$ instead of $f(t-a)u(t-a)$
- Forgetting the $e^{-as}$ factor when applying the second shifting theorem
- Not rewriting argument: using $f(2t-3)$ without converting to $f(2(t-3/2))$ form
- Applying change of scale to $a < 0$ (theorem requires $a > 0$)

### 18. Quick Recap
`learnbox` with 6–8 bullets:
- Linearity: $\mathcal{L}\{\alpha f + \beta g\} = \alpha F + \beta G$
- s-Shift: $\mathcal{L}\{e^{at}f(t)\} = F(s-a)$ (replace $s$ with $s-a$)
- t-Shift: $\mathcal{L}\{f(t-a)u(t-a)\} = e^{-as}F(s)$ (multiply by $e^{-as}$)
- Scale: $\mathcal{L}\{f(at)\} = \frac{1}{a}F(s/a)$
- All three non-trivial properties proved by direct substitution into definition
- Second shifting requires exact form $f(t-a)u(t-a)$ — argument AND window must both shift
- These four properties together allow computation of transforms of virtually all engineering functions

---

## MANDATORY QUALITY CHECKLIST

- [ ] Opening hook in `curiositybox`
- [ ] All four properties stated in `infobox` with full proofs
- [ ] At least 2 pgfplots graphs (s-shift and t-shift visualisations)
- [ ] TikZ property concept map present
- [ ] At least 3 combined advanced examples
- [ ] s-shift mistakebox (wrong direction of shift)
- [ ] t-shift mistakebox (argument not shifted)
- [ ] Excel numerical verification of First Shifting Theorem
- [ ] Python symbolic verification using sympy
- [ ] All four tcolorbox environments used
- [ ] `\end{document}` at the end
- [ ] Forward reference to Topic 09 (Multiplication by t) included
- [ ] All worked examples end with `learnbox`
