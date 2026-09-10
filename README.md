# Raunak Sood

M.S. Computer Science at USC · machine learning at Innovius Capital · B.S. Economics, Santa Clara.

I build measurement infrastructure — the kind that tells you when a result is real and
when it's an artifact of how the data was assembled.

[raunaksood.vercel.app](https://raunaksood.vercel.app) · [LinkedIn](https://www.linkedin.com/in/raunak-sood)

---

### [leakcheck](https://github.com/quantraunak/leakcheck) — find features that read data they were never supposed to see

Temporal leakage never throws and always improves your metrics, which is why it survives
review. `leakcheck` finds it without needing to know the right answer: move *when* a data
source became knowable, recompute, and report every feature that moved.

The exactness is the mechanism. A feature that genuinely cannot read a source gets identical
arrays through identical code and returns bit-identical floats — its difference is `0.0`, not
`1e-15` — so any movement at all is proof of an undeclared dependency rather than a number
you have to squint at.

```python
report = lc.check(compute=build_features, sources=..., timestamps=..., declared=...)
report.raise_for_leaks()
```

It caught a real one: a factor named `turnover_1m` that every reviewer had filed under
"prices and volume" — it lives in `price.py` and is built from volume — but which divides by
shares outstanding, a number that comes off a regulatory filing. It was the only member of
its group that moved when the filing calendar shifted, while eleven genuine price factors
held at exactly zero.

`Python · pandas` — metamorphic testing, applied to feature pipelines

### [bias-fingerprints](https://github.com/quantraunak/bias-fingerprints) — what a data-handling mistake is actually worth

The measurement `leakcheck` came out of. One 22-factor equity study, re-run under alternative
data conventions with everything else held fixed, so the difference between two runs is
attributable to the convention and nothing else.

Dating fundamentals on period end rather than filing date inflates measured skill by **59%**
and manufactures **four** false discoveries, while leaving eleven price-only factors unchanged
to machine precision. Conditioning the universe on current index membership does the opposite:
mean IC *falls*, but illiquidity flips from t = −1.11 to **+2.80** and the low-volatility
anomaly inverts. The two distortions correlate at −0.088.

Underneath: point-in-time index membership from reconstructed spells, SEC XBRL keyed on filing
date with restatements and the ASC 606 tag migration handled, purged and embargoed
walk-forward. And the finding that killed my own result — **59% of the decile spread was
market beta**, with Sharpe ranging 0.09–0.49 across six seeds that differed only in random
state.

`Python · LightGBM · CVXPY · pandas` · [paper](https://github.com/quantraunak/bias-fingerprints/blob/main/paper/bias_fingerprints.pdf) · [dashboard](https://quantraunak.github.io/bias-fingerprints/) · [write-up](https://raunaksood.vercel.app/work/quant)

### [Resampled Thought Trees](https://github.com/quantraunak/tot-resampled-thought-trees) — which reasoning steps actually matter

Five-author USC research on measuring the downstream utility of intermediate states in
Tree-of-Thought LLM search. Instead of judging a reasoning tree by its final answer, we log
internal states, resample search from each one, and classify nodes by whether the search
still succeeds from there — **22,350 resampling trials across 280 logged search trees** on
Game24 and constrained crossword search.

`Python` · [paper](https://github.com/quantraunak/tot-resampled-thought-trees/blob/main/docs/paper.pdf) · [write-up](https://raunaksood.vercel.app/work/reasoning)

### [Melange](https://github.com/quantraunak/Melange) — shipped, two clients, one database

A collaboration-matching app for photographers, models and stylists. Two clients — Next.js web
and Expo/React Native iOS — against one Postgres, with authorisation enforced by row-level
security on every table rather than by a trusted backend. Nine accounts and no traction; the
[status doc](https://github.com/quantraunak/Melange/blob/main/docs/STATUS.md) says so in the
first paragraph.

`Next.js · React Native · Supabase · Postgres` · [live](https://melange-psi.vercel.app)

---

Also: [filing-links](https://github.com/quantraunak/filing-links) — a construction protocol for
point-in-time firm-relationship graphs from SEC filing text, with a benchmark carrying
auditable negatives and a measured cost/quality frontier across six local LLMs.

`Python · pandas · PyTorch · LightGBM · TypeScript · Postgres · C++`
