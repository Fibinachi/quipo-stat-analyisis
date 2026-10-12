# Khipu as Spreadsheet: Calculation, Cell References, and Structural Arithmetic

**Date:** 2026-10-12
**Status:** Research in progress. Not yet peer-reviewed.
**Data:** Open Khipu Repository (OKR), 612 khipu with decoded values

---

## Thesis

Khipu are not passive records. They are calculation workbooks. The evidence:

1. Values repeat across positions in cell-reference patterns (same value + same color, multiple locations)
2. Same-color, co-located values show arithmetic relationships (addition, subtraction, multiplication)
3. 59% of the corpus (361/612 khipu) shows at least one structural arithmetic signal

---

## 1. Cell References: The 52-Thread (Khipu 1000519)

In khipu 1000519, section C (ordinals 45-90), the value 52 appears on MB (dark blue) cords at three positions:

| Tile | Ordinal | Color | Value | Part |
|------|---------|-------|-------|------|
| #7   | 51      | MB    | 52    | Part 2 |
| #26  | 70      | MB    | 52    | Part 5 |
| #31  | 75      | MB    | 52    | Part 6 |

Same value, same color, three positions across three structural parts. This is not three independent entries of 52. It is a single quantity referenced in three places — functionally equivalent to Excel's `=G17`.

**Implication:** Khipu encode relationships between values, not just static entries. Repetition is the reference mechanism. Analysis must map the reference graph (source vs pointer), not just list values.

---

## 2. Structural Arithmetic: Corpus-Wide Scan

**Method:** For each of 612 khipu, every non-zero value was tested against every other value for:
- Addition (a + b = c)
- Subtraction (a - b = c)
- Multiplication (a × b = c)
- Division (a / b = c)
- Repetition (same value + color, 3+ occurrences)

**Structural filter:** A hit counts as structural only if all values share the same cord color AND are within 15 ordinals of each other. This distinguishes intentional calculation from coincidental value-matching.

**Results:**

| Operation | Structural hits | Khipu affected | % of corpus |
|-----------|----------------|----------------|-------------|
| Addition | 28,367 | 246 | 40% |
| Subtraction | 54,020 | 358 | 59% |
| Multiplication | 1,747 | 145 | 24% |
| **Any** | **84,134** | **361** | **59%** |

For comparison, raw value-matching (no color/position filter) produced 1.9M addition hits and 7.9M subtraction hits — overwhelmingly coincidental. The structural filter reduces this to <1.5%, isolating the signal.

**Limitation:** The structural filter cannot prove intent for any single hit. It establishes that same-color, co-located arithmetic is widespread (59% of khipu), which is inconsistent with pure coincidence.

---

## 3. Hand-Verified Cases

### 3a. Khipu 1000588: 10 + 11 = 21

| Block | Ordinal | Color | Value |
|-------|---------|-------|-------|
| 1 | 1 | W | 10 |
| 2 | 15 | W | 11 |
| 3 | 29 | W | 21 |

Sequential blocks, same color (W), clean addition: 10 + 11 = 21. Block 14 also contains W=10 and W=21 together; block 15 contains W=21.

### 3b. Khipu 1000519, Section D: 13 × 2 = 26

| Ordinal | Color | Value |
|---------|-------|-------|
| 92 | W | 13 |
| 97 | W | 26 |

Consecutive records, same color, exact doubling.

---

## 4. Format Specification (Working Draft)

Based on structural analysis of 1000588, 1000519, and corpus-wide patterns:

1. **A khipu is a workbook.** Possibly multiple documents on one cord. Segment by schema before classifying.
2. **Color is the field type.** No universal color semantics — each document defines its own schema (white carries data in 1000588; MB carries the reference thread in 1000519).
3. **Position is the cell address.** Ordinal order matters. Records are cord groups.
4. **Knots are the values.** Decimal, positional. (Settled.)
5. **Dividers are structural.** Repeated color patterns mark sections or categories (e.g., `W W [MB|PG] W MB MB` in 1000588; PR-delimited parts in 1000519 section C).
6. **Repetition is reference.** Same value + same color in multiple positions = cell pointer.
7. **Proximity + color = operation.** Same-color values grouped together with arithmetic relationships encode calculation. The operator is positional (sum after addends), not symbolic.
8. **Cord level is nesting.** Subsidiary cords are sub-fields of the parent pendant.

**Open questions:** Field labels (what the numbers denote); whether subtraction/division have distinct positional encodings vs. inverse reads of addition/multiplication.

---

## 5. Sources and Data

- **Primary data:** Open Khipu Repository (OKR), https://github.com/khipulab/open-khipu-repository
- **Decoder:** Custom Python decoder for OKR knot data (see `~/workspace/quipu-analysis/decoder.py`)
- **Database:** SQLite, 612 khipu with decoded cord values
- **Analysis scripts:** `~/workspace/quipu-analysis/` (math scan, structural test, positional analysis)
- **Visualizations:** `~/workspace/quipu-analysis/language-hunt/` (1000588 and 1000519 block reconstructions)

---

## 6. Relationship to Prior Work

This builds on the repository's existing findings:
- "Six structural form types" — the workbook model extends this: form types are spreadsheet templates
- "Imperial grammar, local sentences" — color roles vary by document, consistent with local schemas on imperial templates
- "Cord colors are ecologically patterned" — color-as-field-type is compatible with ecological patterning

---

## License

CC-BY 4.0
