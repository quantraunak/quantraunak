# Raunak Sood

M.S. Computer Science at USC · machine learning at Innovius Capital · B.S. Economics, Santa Clara.

[raunaksood.vercel.app](https://raunaksood.vercel.app) · [LinkedIn](https://www.linkedin.com/in/raunak-sood)

---

### [leakprobe](https://github.com/quantraunak/leakprobe) — find features that read data they were never supposed to see

Temporal leakage never throws and always improves your metrics, which is why it survives
review. `leakprobe` finds it without needing to know the right answer: move *when* a data
source became knowable, recompute, and report every feature that moved.

The exactness is the mechanism. A feature that genuinely cannot read a source gets identical
arrays through identical code and returns bit-identical floats — its difference is `0.0`, not
`1e-15` — so any movement at all is proof of an undeclared dependency rather than a number
you have to squint at.

```python
report = lp.check(compute=build_features, sources=..., timestamps=..., declared=...)
report.raise_for_leaks()
```

It caught a real one: a factor named `turnover_1m` that every reviewer had filed under
"prices and volume" — it lives in `price.py` and is built from volume — but which divides by
shares outstanding, a number that comes off a regulatory filing. It was the only member of
its group that moved when the filing calendar shifted, while eleven genuine price factors
held at exactly zero.

Benchmarked against itself on five public datasets — retail transactions, taxi trips, crime
reports, 311 requests, bike shares — with five planted leak shapes and a correct pipeline for
each. The shipped version caught **6 of 9**. All three misses had one cause: moving a
timestamp only removes rows from code that *filters* on it, so code that joins a table and
reads a column off it stayed invisible. Two more probes closed that, and the current version
catches **8 of 9 with 0 false positives on the correct pipelines**. The ninth, an outcome
stored in the event's own row under its own clock, is a miss by construction, and the
benchmark keeps it as the method's boundary.

`pip install leakprobe` · `Python · pandas` — metamorphic testing, applied to feature pipelines

### [bias-fingerprints](https://github.com/quantraunak/bias-fingerprints) — what a data-handling mistake is actually worth

The measurement `leakprobe` came out of. One 22-factor equity study, re-run under alternative
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

Then I ran the paper's own validation protocol, and it split the claim in half. Both
signatures are stable across disjoint subsamples and survive bootstrapping, but only one is
separable from clean performance at a twelve-year study's noise level: universe conditioning
is recovered at **100%**, period-end dating at **52%**, labelling 97% of *correct* tables
defective. The reason is geometric and checkable before any table is diagnosed — after
removing family means the dating signature is smaller than the within-family variation in
true performance and correlates **+0.543** with it, so a clean table already supplies most of
the defect's shape.

`Python · LightGBM · CVXPY · pandas` · [paper](https://github.com/quantraunak/bias-fingerprints/blob/main/paper/bias_fingerprints.pdf) · [dashboard](https://quantraunak.github.io/bias-fingerprints/) · [write-up](https://raunaksood.vercel.app/work/quant)

### [cardinality-eval](https://github.com/quantraunak/cardinality-eval) — the schema is not the cost

Does extraction recall degrade with the number of items a model must emit? I built documents
where the answer is known by construction — *k* verbatim filing sentences injected into
name-free filler at constant length — so no annotation is needed and *k* is exact.

Without a grammar it does: unconstrained decoding loses **0.214** recall from k=1 to k=16
(p = 0.011), while the same model on the same documents under a JSON schema does not decline
(p = 0.73). Constrained decoding was the suspect I had written down as most threatening, and
it is not the cost. Whether it is the cure is not settled at this scale: the gap between the
arms is carried by k=1, where the constrained arm returns an empty list on 13 of 25
documents, and from k=4 to k=16 both arms decline by a similar amount.

The pilot did not meet its own pre-registered k=1 validity gate, so absolute levels are not
interpretable, and the README says so first.

`Python · ollama · Qwen 3` — 450 raw model responses committed, so the result re-scores without a GPU

### [filing-links](https://github.com/quantraunak/filing-links) — a link graph, released with its ceiling attached

A construction protocol for point-in-time firm-relationship graphs from 10-K prose: a
benchmark with auditable negatives, a measured cost/quality frontier across six local LLMs,
and a pre-registered coverage gate.

The gate fired. 1,989 filings yield 1,185 edges over 125 firms — a median of **27 names per
date, 6.4%** of the tradable cross-section against the ~145 a return test needs — so the
study stops at the coverage report and the signal test stays unrun. Four explanations for
the shortfall were proposed and each refuted against cached data. What survives is the
reason: Regulation S-K compels a filer to disclose customers above 10% of revenue and imposes
no matching duty for suppliers, so extracting the S&P 500 extracts the side that is not
required to speak.

`Python · pandas · ollama` — 668 customer claims against 241 supplier claims
### [Resampled Thought Trees](https://github.com/quantraunak/tot-resampled-thought-trees) — which reasoning steps actually matter

Five-author USC research on measuring the downstream utility of intermediate states in
Tree-of-Thought LLM search. Instead of judging a reasoning tree by its final answer, we log
internal states, resample search from each one, and classify nodes by whether the search
still succeeds from there — **22,350 resampling trials across 280 logged search trees** on
Game24 and constrained crossword search.

`Python` · [paper](https://github.com/quantraunak/tot-resampled-thought-trees/blob/main/docs/paper.pdf) · [write-up](https://raunaksood.vercel.app/work/reasoning)

### [Melange](https://github.com/quantraunak/Melange) — shipped, two clients, one database

A collaboration-matching app for photographers, models and stylists, live on the iOS App
Store and the web. Two clients — Next.js web
and Expo/React Native iOS — against one Postgres, with authorisation enforced by row-level
security on every table rather than by a trusted backend. Nine accounts and no traction; the
[status doc](https://github.com/quantraunak/Melange/blob/main/docs/STATUS.md) says so in the
first paragraph.

`Next.js · React Native · Supabase · Postgres` · [live](https://melange-psi.vercel.app)

---

`Python · pandas · PyTorch · LightGBM · TypeScript · Postgres · C++`
