# Feature count for harmonic encoding

**Model:** claude-sonnet-4-6

### User

why did i use only 11 features? i know it translated 11 from using the logistcal map problem for encoding, but for harmonics what is the actual number needed of input features?

---

### Assistant

Looking at your code carefully, the 11 was indeed inherited from the logistic map convention, and it's a category error when applied to harmonics. Here's why:

## The Logistic Map vs. Harmonics: Different Input Dimensionality

**Logistic map:** 1 free parameter (`r`) → 11 features were all transformations of that single value.

**Harmonics:** Any pair (n, m) decomposes canonically as:
```
n = p·g,  m = q·g,  where gcd(p, q) = 1
```
So you have **3 truly independent integers** (p, q, g). For Euler GS specifically, you have **2** — because GS depends only on the prime factorization of `p·q`, and `g` is completely irrelevant.

---

## Your 11 Features, Honestly Audited

**Carry g (irrelevant for GS):**
- `log_n_low` = log2(p·g) — mixes relevant and irrelevant
- `log_n_high` = log2(q·g) — mixes relevant and irrelevant
- `log_gcd` = log2(g+1) — pure noise for GS prediction
- `log_diff` = log2(g(q−p)+1) — mixed

**Pure functions of p and q (actually useful):**
- `log_p_num` = log2(p+1)
- `log_q_den` = log2(q+1)
- `log_ratio` = log2(q/p)
- `p_frac` = p/(p+q)
- `tenney_h` = log2(p·q+1)
- `log_p_plus_q` = log2(p+q+1)
- `log_euler_dist` = log2(p+q) ← **nearly identical to log_p_plus_q**

The last two differ by `log2((p+q+1)/(p+q))`, which shrinks toward zero as complexity grows. They are **functionally redundant** across most of your dataset.

---

## What the Correct Number Actually Is

| Purpose | Independent inputs | Minimum useful features |
|---|---|---|
| Predict Euler GS | p, q only | **2** |
| Characterize full harmonic pair | p, q, g | **3** |
| Encode for ML with pi/e basis | p → 3–5 terms, q → 3–5 terms | **6–10** |

The probe run already told you this implicitly — notice that all three `log_q_den` encoded variants dominate the importance table (`_gauss` 9.28%, `_pow_e` 9.10%, `_exp_neg` 8.96%), which are all transformations of a single variable `q`. The model is essentially learning that `q` (denominator of reduced ratio) is the primary carrier of dissonance, with `p` secondary. That's a 2-variable problem.

---

## What to Actually Do

Instead of encoding 11 ad-hoc derived features, encode the 2 fundamental variables directly:

```python
# Encode p (numerator) with e-basis (bounded, consonance-side)
encode_e_func(log2(p), "p_num", scale=SCALE_5LIM)   # 3 features

# Encode q (denominator) with e-basis (dominant signal per probe)
encode_e_func(log2(q), "q_den", scale=SCALE_5LIM)   # 3 features

# Encode product p·q with pi-basis (complexity grows, dissonance side)
encode_pi_func(log2(p*q), "tenney", scale=SCALE_TH)  # 5 features

# Optional: encode g only if predicting voicing-dependent targets
encode_e_func(log2(g), "gcd", scale=SCALE_GCD)       # 3 features
```

That gives you **11–14 features** but derived from the actual independent structure of the problem, not inherited from a 1D analogy. The key difference is you'd be encoding `p` and `q` *directly* rather than encoding their sums, differences, and ratios — which are all lower-information projections of the same two numbers.

The fact that `eenc_log_q_den` variants dominate at nearly 3× any other feature is the probe telling you: **the denominator `q` is the problem's primary axis, encode it thoroughly and directly.**

---

