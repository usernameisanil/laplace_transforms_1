# Laplace Transforms Lecture Note Generation — Execution Meta-Prompt (Self-Driving)

**Repo:** `usernameisanil/laplace_transforms_1`
**Branch:** `main`
**Prompts directory:** `prompts/unit_iv/` and `prompts/unit_v/`
**Responses directory:** `responses/unit_iv/` and `responses/unit_v/`

---

## PURPOSE

This is the **one and only prompt** you need to run for every topic.
You do NOT copy-paste any topic file content. The LLM reads it from GitHub directly.

### How to trigger a run

Start a new session with an LLM that has GitHub MCP access, then send exactly:

```
Read EXECUTION_META_PROMPT.md from the repo usernameisanil/laplace_transforms_1,
follow it exactly, and process this topic file:
prompts/unit_iv/topic_01_introduction.md
```

Change the last filename for each of the 17 topics. That is all.

---

## ALL 17 TOPIC FILES

### Unit IV — Laplace Transforms
1.  `prompts/unit_iv/topic_01_introduction.md`
2.  `prompts/unit_iv/topic_02_definition.md`
3.  `prompts/unit_iv/topic_03_conditions_existence.md`
4.  `prompts/unit_iv/topic_04_elementary_functions.md`
5.  `prompts/unit_iv/topic_05_properties.md`
6.  `prompts/unit_iv/topic_06_periodic_functions.md`
7.  `prompts/unit_iv/topic_07_special_functions.md`
8.  `prompts/unit_iv/topic_08_derivatives.md`
9.  `prompts/unit_iv/topic_09_integrals.md`
10. `prompts/unit_iv/topic_10_multiplication_by_t.md`
11. `prompts/unit_iv/topic_11_division_by_t.md`
12. `prompts/unit_iv/topic_12_evaluation_of_integrals.md`

### Unit V — Inverse Laplace Transforms
13. `prompts/unit_v/topic_01_inverse_laplace_transform.md`
14. `prompts/unit_v/topic_02_elementary_functions_inverse.md`
15. `prompts/unit_v/topic_03_partial_fractions.md`
16. `prompts/unit_v/topic_04_convolution_theorem.md`
17. `prompts/unit_v/topic_05_odes_applications.md`

---

# INSTRUCTIONS FOR THE LLM

You are reading this file because the user asked you to process a specific topic.
Follow every step below in strict sequence. Do not skip any step.

---

## STEP 0: READ THE TOPIC FILE

Using your GitHub MCP tool, call `get_file_contents` with:
- `owner`: `usernameisanil`
- `repo`: `laplace_transforms_1`
- `path`: *(the topic file path the user specified)*

Read the returned content **completely and carefully** before writing a single line of LaTeX.

Extract and record the following:

| What to extract | Where to find it in the prompt file |
|---|---|
| Topic name | First `#` heading |
| Unit number and title | `**Unit:**` line |
| Exact `\lhead{}` value | Under `fancyhdr` / LATEX SETUP REQUIREMENTS block |
| Exact `\rhead{}` value | Under `fancyhdr` / LATEX SETUP REQUIREMENTS block |
| Exact `\title{}` value | LATEX SETUP REQUIREMENTS block |
| Full preamble | `## LATEX SETUP REQUIREMENTS` block |
| Opening hook text | `## OPENING HOOK` block |
| Complete ordered section list | `## REQUIRED SECTIONS` block — every `###` heading is one section |
| Minimum counts (Viva, Descriptive, Practice, MCQ) | Individual section specs |
| Mandatory quality checklist | `## MANDATORY QUALITY CHECKLIST` block |
| Output filename | Same as prompt filename with `.md` replaced by `.tex` |

Output filename mapping:
- `prompts/unit_iv/topic_03_conditions_existence.md` → `responses/unit_iv/topic_03_conditions_existence.tex`
- `prompts/unit_v/topic_04_convolution_theorem.md` → `responses/unit_v/topic_04_convolution_theorem.tex`

**Do not proceed to Step 1 until you have read and noted every section title from REQUIRED SECTIONS.**

---

## STEP 1: GENERATE THE COMPLETE LaTeX FILE

Generate a **complete, fully written, self-contained, compilable LaTeX source file**.

---

### 1a. Preamble (Non-Negotiable)

1. **Use the exact preamble from `## LATEX SETUP REQUIREMENTS`** in the topic file — copy it verbatim.
   - Always include: `amsmath`, `amssymb`, `geometry` (`margin=2.5cm`), `booktabs`, `xcolor`,
     `hyperref`, `listings`, `pgfplots`, `tcolorbox`, `enumitem`, `fancyhdr`, `tikz`, `array`.
   - `\pgfplotsset{compat=1.18}` must appear.
   - `\tcbuselibrary{skins, breakable}` must appear.
   - Add any extra packages required by specific content (e.g., `subcaption` for side-by-side figures).

2. **Define all four tcolorbox environments** in the preamble using `[1]` (positional title), NOT `[1][]`:
   ```
   \newtcolorbox{curiositybox}[1]{colback=yellow!10, colframe=orange!80!black, fonttitle=\bfseries, title=#1, breakable}
   \newtcolorbox{infobox}[1]{colback=blue!5, colframe=blue!60!black, fonttitle=\bfseries, title=#1, breakable}
   \newtcolorbox{mistakebox}[1]{colback=red!5, colframe=red!60!black, fonttitle=\bfseries, title=#1, breakable}
   \newtcolorbox{learnbox}[1]{colback=green!5, colframe=green!60!black, fonttitle=\bfseries, title=#1, breakable}
   ```

3. **Configure lstlisting** for Python in the preamble:
   ```
   \lstset{language=Python, basicstyle=\ttfamily\small, keywordstyle=\color{blue},
           commentstyle=\color{gray}, stringstyle=\color{orange},
           showstringspaces=false, numbers=left, numberstyle=\tiny,
           breaklines=true, frame=single}
   ```

4. **Configure fancyhdr** using the exact values from the topic file:
   ```
   \pagestyle{fancy}
   \fancyhf{}
   \lhead{<exact value from topic file>}
   \rhead{<exact value from topic file>}
   \cfoot{\thepage}
   ```

5. **Title block**: use the exact `\title{}` format from the topic file. Immediately after `\begin{document}` write:
   ```
   \maketitle
   \tableofcontents
   \newpage
   ```

---

### 1b. Section Generation (Non-Negotiable)

**THE GOLDEN RULE: Follow the REQUIRED SECTIONS block of the topic file exactly — in the exact order listed, with the exact titles given, with zero omissions.**

Do NOT impose a fixed section architecture from outside the topic file.
Do NOT reorder sections.
Do NOT merge sections.
Do NOT skip any section.
Do NOT add sections not listed in the topic file.

Every topic in this course has the following section pattern (exact section numbers/names vary per topic — always defer to the topic file's own REQUIRED SECTIONS list):

| Typical section | Content expected |
|---|---|
| Opening Hook | Inside `curiositybox`, using the exact text from `## OPENING HOOK` in the topic file |
| Why This Topic Exists | Motivation, engineering connections, booktabs table (skip/mistake vs consequence), ends with learnbox |
| You Already Know This (Intuition First) | Analogy-driven, plain prose, no boxes required unless the topic file says otherwise |
| Core concept sections (1 to N) | Each is one named topic — intro prose, then `infobox` with formal definitions/derivations, then at least one fully worked example, ending with learnbox where specified |
| Visualizing section | pgfplots/TikZ diagram(s) — MANDATORY at least once per topic |
| Worked Examples (standalone section) | At least the minimum count specified — each example inside `infobox`, ending with learnbox |
| Excel Example (MANDATORY) | Fully written spreadsheet walkthrough — column headers, sample rows, explicit cell formulas shown |
| Python Example (MANDATORY) | Complete, runnable Python code inside `lstlisting` — include expected output as comments |
| Viva-Style Oral Questions | Exactly the number specified (typically 8) — complete questions with full answers, no placeholders |
| Descriptive Questions | Exactly the number specified (typically 5) — exam-style, complete |
| Practice Problems | Exactly the number specified (typically 6) — with short answer hints |
| MCQs | Exactly the number specified (typically 5) — 4 options each, bold correct answer with `\textbf{}`, one-line explanation below each |
| Common Mistakes | Inside a `mistakebox` table — at least the rows specified in the topic's checklist |
| Quick Recap | Exactly 6–8 bullets as specified — topic-specific formulas and takeaways, inside learnbox |

---

### 1c. Content Quality Rules (Non-Negotiable)

6. **Opening hook**: place inside `\begin{curiositybox}{Hook}` ... `\end{curiositybox}` — use the exact text from `## OPENING HOOK` in the topic file. Never paraphrase it.

7. **Every infobox** must contain the exact formal definitions, theorems, and formulas specified in the topic file for that section. No generic filler.

8. **Every worked example** must:
   - Use concrete distinct numerical values (not the same numbers reused across different examples)
   - Show every arithmetic step — never skip
   - Never write: "it can be shown", "the reader can verify", "similarly", "(details omitted)", "continuing in the same way"
   - End with a small `learnbox` summarising the key result or method used

9. **Booktabs tables**: use `\toprule`, `\midrule`, `\bottomrule` — never bare `\hline`.

10. **MCQs**: 4 options (a) to (d), bold the correct answer with `\textbf{}`, provide a one-line explanation after each question.

11. **Diagrams**: every topic requiring a diagram must include a fully self-contained TikZ/pgfplots picture:
    - `\draw[->]` for axes where TikZ is used directly
    - Every axis labelled with `xlabel` and `ylabel` at minimum, `grid=major` where useful
    - No `\input{}`, no `\includegraphics{}`

12. **Excel section**: must include a table showing column headers with at least 3 sample rows of computed values, and explicit formulas (e.g., `=EXP(-5*A2)*EXP(-2*A2)`). End with a learnbox comparing the numerical approximation to the exact value.

13. **Python section**: must include a complete runnable script inside `\begin{lstlisting}[language=Python]` ... `\end{lstlisting}` using `sympy` (or `numpy`/`scipy` where appropriate) — cover the steps described in the topic file, include expected output as comments. End with a learnbox.

14. **Never truncate**: do not end any section with:
    - "(add more questions as needed)"
    - "(remaining examples follow the same pattern)"
    - "..."
    - "etc."
    Every question, every row, every bullet must be written out in full.

15. **Transform notation standards throughout the entire file**:
    - Laplace transform operator: `\mathcal{L}\{f(t)\} = F(s)` — never plain `L` or `f(s)`
    - Lowercase for time domain, uppercase for transform domain: `f(t) \leftrightarrow F(s)`
    - Convolution: `(f * g)(t) = \int_0^t f(\tau)g(t-\tau)\,d\tau`
    - Unit step function: `u(t-a)` or `H(t-a)` — pick one and use it consistently within a file

---

### 1d. LaTeX Correctness Rules (Non-Negotiable)

16. **tcolorbox syntax**: every `\newtcolorbox` uses `[1]` not `[1][]` — title is positional.
    Usage: `\begin{infobox}{Title text}` ... `\end{infobox}`
    Same for `curiositybox`, `learnbox`, `mistakebox`.

17. **Every environment opened must be closed**:
    - `\begin{infobox}{...}` → `\end{infobox}`
    - `\begin{tikzpicture}` → `\end{tikzpicture}`
    - `\begin{axis}` → `\end{axis}`
    - `\begin{tabular}` → `\end{tabular}`
    - `\begin{lstlisting}` → `\end{lstlisting}`

18. **No bare special characters in text mode**:
    - `\%` not `%`
    - `\$` not `$`
    - `\&` not `&` outside tabular
    - `\_` not `_` outside math

19. **No Unicode characters in LaTeX source**:
    - `---` not the Unicode em-dash
    - `\pi`, `\infty`, `\times`, `\cdot`, `\geq`, `\leq`, `\to`, `\ldots` — never paste Unicode math symbols

20. **pgfplots rules**:
    - Every `\begin{axis}` must have at minimum `xlabel` and `ylabel`
    - 3D surf plots: `samples=40` maximum
    - Close every `\begin{axis}` with `\end{axis}` before `\end{tikzpicture}`

21. **Document boundaries**:
    - First line: `\documentclass[12pt,a4paper]{article}`
    - Last line: `\end{document}`
    - Nothing before `\documentclass`, nothing after `\end{document}`

---

## STEP 2: VERIFY THE MANDATORY QUALITY CHECKLIST

Before pushing, go through the `## MANDATORY QUALITY CHECKLIST` from the topic file item by item.
If any item is not satisfied, fix the LaTeX and recheck.

In addition, verify every item in the universal checklist below:

```
UNIVERSAL PRE-PUSH CHECKLIST
-----------------------------
[ ] Preamble matches LATEX SETUP REQUIREMENTS from topic file exactly
[ ] geometry margin is 2.5cm
[ ] \newtcolorbox uses [1] not [1][] for all four boxes, with fonttitle=\bfseries
[ ] lstlisting configured for Python in preamble (language=Python, showstringspaces=false)
[ ] fancyhdr uses \pagestyle{fancy} and \fancyhf{} before setting lhead/rhead
[ ] fancyhdr lhead and rhead match exact values from topic file
[ ] \begin{document} present; immediately followed by \maketitle
[ ] \tableofcontents present; followed by \newpage
[ ] Opening hook is inside curiositybox using exact text from topic file
[ ] Every section from REQUIRED SECTIONS is present and complete
[ ] No section is reordered, merged, or skipped relative to topic file
[ ] At least 1 pgfplots/TikZ diagram with xlabel, ylabel, grid=major
[ ] Excel section includes column headers, sample rows, and explicit cell formulas
[ ] Python section contains complete runnable code in lstlisting with expected output as comments
[ ] Viva questions: correct count, all complete with full answers
[ ] Descriptive questions: correct count, all complete
[ ] Practice problems: correct count, all with answer hints
[ ] MCQs: correct count, 4 options, correct answer bolded, explanation given
[ ] Common Mistakes mistakebox: row count meets topic file minimum
[ ] Quick Recap learnbox: bullet count is 6--8 and all topic-specific
[ ] Every worked example ends with a learnbox "What Did We Learn?"
[ ] Every \begin{infobox}, \begin{curiositybox}, \begin{learnbox}, \begin{mistakebox} is closed
[ ] Every \begin{tikzpicture} closed with \end{tikzpicture}
[ ] Every \begin{axis} closed with \end{axis}
[ ] Every \begin{lstlisting} closed with \end{lstlisting}
[ ] Every \begin{tabular} closed with \end{tabular}
[ ] Booktabs tables use \toprule, \midrule, \bottomrule (no \hline)
[ ] No bare % in text mode (use \%)
[ ] No bare & outside tabular/align
[ ] No bare _ or ^ outside math mode
[ ] No Unicode characters anywhere in the .tex source
[ ] \mathcal{L} used for Laplace -- never plain L
[ ] No truncated sections -- no ellipsis, no "add more", no "same pattern"
[ ] \end{document} is the very last line of the file
```

**Do NOT push if any checklist item is unchecked. Fix, recheck, then push.**

---

## STEP 3: PUSH TO GITHUB

Using your GitHub MCP tool, call `create_or_update_file` with:

| Parameter | Value |
|---|---|
| `owner` | `usernameisanil` |
| `repo` | `laplace_transforms_1` |
| `branch` | `main` |
| `path` | See path routing rule below |
| `message` | `response: <output_filename>.tex — LaTeX lecture note for <Topic Name>, Unit <IV or V>` |
| `content` | The complete .tex file as a string |

**Path routing rule:**
- Files under `prompts/unit_iv/` → `responses/unit_iv/<output_filename>.tex`
- Files under `prompts/unit_v/` → `responses/unit_v/<output_filename>.tex`

**SHA rule (critical):**
If the output file already exists in the repo, you MUST call `get_file_contents` first to fetch its current SHA and pass it as the `sha` parameter. Pushing without SHA to an existing file causes a 422 error.

---

## STEP 4: REPORT COMPLETION

After a successful push, print this exact report (fill in all `< >` values, and list every section title exactly as it appears in the topic file):

```
=====================================================
LAPLACE TRANSFORMS -- LECTURE NOTE GENERATION COMPLETE
=====================================================
File pushed  : responses/<unit_iv or unit_v>/<output_filename>.tex
Commit SHA   : <sha from push response>
Commit URL   : <html_url from push response>
Topic        : <Topic Name>
Unit         : Unit <IV or V> -- <Unit Title>
-----------------------------------------------------
Sections generated (in order):
  <list every section title exactly as it appears in the topic file>
-----------------------------------------------------
Mandatory elements:
  Worked examples   : <count>
  Excel example     : YES
  Python example    : YES
  Viva questions    : <count>
  Descriptive Qs    : <count>
  Practice problems : <count>
  MCQs              : <count>
  Common Mistakes   : <row count>
  Quick Recap       : <bullet count> bullets
  TikZ/pgfplots     : <count>
-----------------------------------------------------
All checklist items (topic file + universal): PASSED
=====================================================
```

---

## KNOWN FAILURE MODES — PREVENT THESE

| # | Failure | Prevention |
|---|---|---|
| 1 | `\newtcolorbox{infobox}[1][]` | Use `[1]` only — title is positional, never keyword |
| 2 | Unclosed tcolorbox | Immediately write `\end{infobox}` after planning each box |
| 3 | Unicode em-dash in .tex | Type `---` — never paste the Unicode em-dash character |
| 4 | Sections reordered, merged, or skipped | Follow REQUIRED SECTIONS order exactly — never rearrange (see Golden Rule) |
| 5 | Missing Excel or Python section | Both are MANDATORY in every topic — include both always |
| 6 | Truncated assessment | Write every question fully — no ellipsis, no "add more" |
| 7 | Missing `\maketitle` | `\begin{document}` → `\maketitle` → `\tableofcontents` → `\newpage` |
| 8 | SHA missing on file update | Always fetch SHA with `get_file_contents` before updating |
| 9 | Bare `%` in text | Write `\%` or spell out "percent" |
| 10 | Wrong margin | `\geometry{margin=2.5cm}` — not `1in` |
| 11 | lstlisting not configured | Always define Python lstlisting settings in preamble |
| 12 | Plain `L{}` for transforms | Always use `\mathcal{L}` for Laplace |
| 13 | Wrong output path | `prompts/unit_iv/` → `responses/unit_iv/`; `prompts/unit_v/` → `responses/unit_v/` |
| 14 | Unicode math symbols | Use `\pi`, `\infty`, `\times`, `\cdot` — never paste Unicode equivalents |
| 15 | Diagram axes unlabelled | Label every axis (xlabel, ylabel) and every plotted curve/point |
| 16 | 3D plot timeout | `samples=40` maximum for any surf plot |
| 17 | `\hline` in tables | Use `\toprule`, `\midrule`, `\bottomrule` — never `\hline` |
| 18 | Hook text paraphrased | Copy the hook verbatim from `## OPENING HOOK` in the topic file |
| 19 | MCQ correct answer not bolded | Wrap correct option with `\textbf{}` always |
| 20 | Excel section missing formulas | Show explicit cell formulas (e.g., `=EXP(-5*A2)`), not just final values |
