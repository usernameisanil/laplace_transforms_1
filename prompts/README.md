# Prompts Directory

**Course:** Transform Techniques — Laplace Transforms  
**University:** JNTUA College of Engineering (Autonomous)  

---

## Purpose

This directory contains **AI content-generation prompts** for each topic in Units IV and V. Each prompt is designed to generate a complete, lecture-quality LaTeX explanation of the topic — covering theory, formulae, worked examples, Excel/Python demonstrations, and exam-oriented problem sets.

---

## Structure

```
prompts/
├── README.md                          ← This file
├── prompt_to_generate_response.txt    ← Instructions for AI response generation
├── unit_iv/
│   ├── topic_01_introduction.md
│   ├── topic_02_definition.md
│   ├── topic_03_conditions_existence.md
│   ├── topic_04_elementary_functions.md
│   ├── topic_05_properties.md
│   ├── topic_06_periodic_functions.md
│   ├── topic_07_special_functions.md
│   ├── topic_08_derivatives.md
│   ├── topic_09_integrals.md
│   ├── topic_10_multiplication_by_t.md
│   ├── topic_11_division_by_t.md
│   └── topic_12_evaluation_of_integrals.md
└── unit_v/
    ├── topic_01_inverse_laplace_transform.md
    ├── topic_02_elementary_functions_inverse.md
    ├── topic_03_partial_fractions.md
    ├── topic_04_convolution_theorem.md
    └── topic_05_odes_applications.md
```

---

## Prompt Design Guidelines

Each prompt follows a consistent structure:

1. **Role / Audience** — Define the AI's role and the target student profile
2. **Topic Overview** — What the topic covers and why it matters
3. **LATEX SETUP REQUIREMENTS** — Exact preamble, fancyhdr values, title block
4. **AUDIENCE AND TONE** — Teaching style and language conventions
5. **OPENING HOOK** — Curiosity-triggering opening (verbatim text for curiositybox)
6. **REQUIRED SECTIONS** — Every section the output must include, in order
7. **MANDATORY QUALITY CHECKLIST** — Self-verification items before pushing

---

## Responses

Generated responses for each prompt are stored in the `responses/` directory (sibling to `prompts/`), mirroring the same `unit_iv/` and `unit_v/` folder structure.

---

## Topic Index

### Unit IV — Laplace Transforms

| Topic No. | Title | Prompt File |
|-----------|-------|-------------|
| 01 | Introduction | `unit_iv/topic_01_introduction.md` |
| 02 | Definition | `unit_iv/topic_02_definition.md` |
| 03 | Conditions for Existence | `unit_iv/topic_03_conditions_existence.md` |
| 04 | Transforms of Elementary Functions | `unit_iv/topic_04_elementary_functions.md` |
| 05 | Properties of Laplace Transforms | `unit_iv/topic_05_properties.md` |
| 06 | Laplace Transform of Periodic Functions | `unit_iv/topic_06_periodic_functions.md` |
| 07 | Special Functions | `unit_iv/topic_07_special_functions.md` |
| 08 | Derivatives | `unit_iv/topic_08_derivatives.md` |
| 09 | Integrals | `unit_iv/topic_09_integrals.md` |
| 10 | Multiplication by t | `unit_iv/topic_10_multiplication_by_t.md` |
| 11 | Division by t | `unit_iv/topic_11_division_by_t.md` |
| 12 | Evaluation of Integrals by Laplace Transforms | `unit_iv/topic_12_evaluation_of_integrals.md` |

### Unit V — Inverse Laplace Transforms

| Topic No. | Title | Prompt File |
|-----------|-------|-------------|
| 01 | Inverse Laplace Transform | `unit_v/topic_01_inverse_laplace_transform.md` |
| 02 | Elementary Functions (Inverse) | `unit_v/topic_02_elementary_functions_inverse.md` |
| 03 | Method of Partial Fractions | `unit_v/topic_03_partial_fractions.md` |
| 04 | Convolution Theorem | `unit_v/topic_04_convolution_theorem.md` |
| 05 | Applications to Ordinary Differential Equations | `unit_v/topic_05_odes_applications.md` |
