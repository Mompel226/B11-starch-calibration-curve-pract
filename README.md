# Starch calibration curve — IB Biology B1.1

**By Dr Daniel Mompel Riera**

A complete, classroom-tested set of materials for the starch–iodine calibration practical:
worksheet, self-calculating results workbook, and an optional guide to doing the analysis in R.

**Live site:** https://USERNAME.github.io/REPONAME/

---

## Why this exists: the 1% starch problem

Almost every published version of this practical — textbooks, exam-board resources, the protocols
you find by searching — tells students to make standards from a **1% starch solution**, typically
across a range like 0.05% to 1.00%.

**That range cannot produce a calibration curve.** If your students have ever come back with a set
of readings that barely change from tube to tube, this is why.

Two things go wrong at once, and both come from having too much starch.

**1. The iodine runs out.** The blue colour comes from iodine trapped inside amylose helices. Once
every available helix is occupied, adding more starch produces no more colour. The curve flattens.

**2. The tube is too dark to read.** The starch–iodine complex is intensely coloured. Vernier state
that their colorimeters and spectrometers are only reliable between **0.1 and 1.0 absorbance**, and
that readings at or above 1.0 are too high to trust — above 1.0, less than a tenth of the light
reaches the detector. A 1% starch standard is roughly a hundred times past that.

Real numbers from a class running the published protocol:

| Starch / % | Absorbance |
|---|---|
| 0.00 | 0.000 |
| 0.05 | 1.806 |
| 0.10 | 1.832 |
| 0.20 | 1.985 |
| 0.50 | 2.198 |

Every reading except the blank is above the instrument's ceiling, and they are nearly identical —
a tenfold increase in starch changes the reading by about a fifth. There is no line to fit.

### The fix

Dilute the stock a hundred-fold and work in a range the instrument can actually see.

| | Published protocol | This version |
|---|---|---|
| Stock solution | 1% | **0.01%** |
| Standards | 0.05 – 1.00% | **0.001 – 0.006%** |
| Absorbance range | ~1.8 – 2.2 (unreadable) | **~0.1 – 0.63** |
| Iodine per tube | 1 drop, or 0.5 cm³ | **0.1 cm³ (100 µL), measured** |

The standards now sit inside the 0.1–1.0 window, the relationship is linear, and R² comes out
around 0.999.

A note on the iodine: 0.1 cm³ of 0.01 mol dm⁻³ keeps it in roughly ten-fold excess across the
standards — enough that it never becomes the limiting factor, without adding so much colour of its
own that the blank has to work hard. *(That multiplier is an estimate from published amylose
iodine-binding figures, not a measurement — treat it as an order of magnitude.)*

**Measure the iodine, don't drop it.** Iodine solution is itself coloured, so it contributes to
every reading. That contribution only cancels against the blank if every tube receives an identical
volume. A dropper delivers about 0.05 cm³ with roughly ±25% variation, and that variation becomes a
per-tube offset that repeating and averaging cannot remove.

---

## What's in here

| File | What it is |
|---|---|
| `index.html` | Landing page — the one link to give students |
| `calibration-curve-worksheet.docx` | The student worksheet: method, apparatus, standards table, troubleshooting, assessment criteria |
| `calibration-curve-workbook.xlsx` | Results workbook — students type readings into the yellow cells and the graph, gradient and R² appear automatically |
| `starch-curve-in-r.html` | Optional companion guide: the same analysis in R, from installing it to reading off an unknown |
| `starch_curve.R` | One-click script — reads the workbook, does the whole analysis, saves the graph |

### The workbook has four tabs

- **How to** — building the chart in Excel on macOS, step by step
- **Your data** — where students type; charts populate themselves
- **Worked example** — deliberately kept at the *old* concentrations, because the data bends. Learning to spot a plateau and exclude those points is a skill straight-line data cannot teach.
- **Why the graph flattens** — the explanation above, written for students

### Not included, on purpose

**The technician request sheet is not in this repository.** It specifies the two unknown solutions,
and this repo is public — students would have the answers. Send that one to your technician
directly. If you adopt these materials, message me and I'll send it, or just make up your own two
unknowns.

---

## Design decisions another teacher might want to know

**Two unknowns, chosen deliberately.** One sits between the standards, so it is read by
**interpolation**. The other sits above the strongest standard, so the line must be **extrapolated**
to reach it — or the sample diluted. The IB guide asks for both, and this is where students meet
the difference between "backed by my data" and "trusting the line where I have none".

**Micropipettes, not graduated pipettes, for the small volumes.** Partly accuracy — 100 µL is well
inside a micropipette's reliable range and impossible on a graduated pipette — and partly because
the practice is worth having. Three tips per group, one job each, so iodine can never reach the
starch stock.

**A cuvette per tube.** Rinsing between every reading is what pushes this practical past the end of
the lesson. Give out eight cuvettes and students fill them all, then read them all. The worksheet
still explains the rinse-and-go-low-to-high method for anyone who only has one.

**The technician makes the 0.01% solution, not the students.** It is a hundred-fold dilution; doing
it badly is the single easiest way to ruin the whole class's data.

---

## Reuse

Take it, change it, use it. If you find an error — especially in the chemistry — please open an
issue so it gets fixed for everyone.

Licence: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — use and adapt freely,
including commercially, as long as you credit **Dr Daniel Mompel Riera**.

## Sources for the claims above

- Vernier, *What is the useful absorbance range of a spectrometer or colorimeter?* — TIL 2589
- Vernier Go Direct SpectroVis Plus and Go Direct Colorimeter manuals
- MDPI, *The Iodine/Iodide/Starch Supramolecular Complex* (2024) — why the complex absorbs where it does
- MDPI, *Optimized Spectrophotometry Method for Starch Quantification* — reports a linear range of 1–100 µg/mL
- Gilson, *PIPETMAN pipette specifications* — accuracy at different fractions of nominal volume
