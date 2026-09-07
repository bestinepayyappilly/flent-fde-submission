# Flent FDE take-home — submission

Bestine Payyappilly · **Problem 1, the market-listing trust layer** · September 2026

Everything is in this repository, so nothing needs to come through email.

| | |
|---|---|
| **Approach note** | [`approach-note.pdf`](approach-note.pdf) — 4 pages |
| **Execution plan** | [`execution-plan.pdf`](execution-plan.pdf) — FLT-1 parent + 8 sub-issues |
| **Proof of work** | [`flent-trust-layer-bestine.zip`](flent-trust-layer-bestine.zip) — the full repo, 1.3 MB |
| **Deployed** | [flent-trust-layer.vercel.app](https://flent-trust-layer.vercel.app) |

## Five minutes

Download the zip, unzip it, and run:

```
cd flent-trust-layer/trust-layer
python3 trust_layer.py       # scores the packet deal: 86 listings -> a decision
python3 stress_test.py       # 7 reproducible attacks on that decision
python3 outcomes_check.py    # tests my own premise against Flent's history
```

Python 3.8+, standard library only. No install step, no dependencies.

Or open [flent-trust-layer.vercel.app](https://flent-trust-layer.vercel.app), which
runs the same engine over an API rather than reimplementing it, so the site cannot
drift from the script.

## What it concludes

**The benchmark is publishable. The verdict is not.** The layer refuses to say whether
₹56,000 is above or below market on this deal, because the surviving comparables mix
two rent conventions and the deviation flips sign depending on which one they use —
₹5,000 a month apart, opposite decisions. It returns one question for Supply instead
of a number, and recording the answer on the site re-scores the deal in front of you.

Three findings the submission rests on:

1. **Cleaning is a null result.** 86 rows to 20, and the median moves ₹500. Filtering
   does not fix the rate, it collapses the sample — and only 25 of the 66 removed rows
   were not evidence.
2. **The maintenance fork decides the deal.** No cleaning rule reaches it, because the
   information was never scraped.
3. **Confidence must not be a function of `n`.** Every defect *raises* `n`, so grading
   on sample size lets surviving junk buy confidence. The engine grades on how hard the
   call is to overturn: ~20 attacks, and this call survives 18.

And one that argues against my own choice of problem: `outcomes_check.py` reads Flent's
own history and finds revenue forecasts landing within 2% of plan while fill-time
forecasts run 23% long. The layer makes one input honest; the data says it was not the
input doing the damage. That is in the note, and it reorders the execution plan.

`trust-layer/FAILURES.md` inside the zip is the honest version of the note: nine
defects found by attacking my own build, four still open, and two findings withdrawn
after they turned out to be wrong.
