# Analysis: Kőszegi-Rabin (2006) PPE — Second-Hand Car Seller

## Follow-up: Is Part 3 right as well?

**No, Part (iii) is ❌ NOT correct.** It contains two errors:

1. **The proof method is invalid:** The step μ(v − p') = μ(v) + μ(−p') uses a property (additivity) that **does not hold** for the piecewise-linear loss-aversion function μ. The function μ is only "linear" within each piece (gains or losses separately), not additive across the kink at zero. Since v > 0 and −p' < 0, these arguments have opposite signs, and additivity fails.

2. **The claimed result is false:** Under the assumed "always sell" reference, U\_sell(v) ≠ U\_no-sell in general. Direct computation gives:
   - U\_sell(v) = v + ηΔ(1−λ)/4
   - U\_no-sell = v + ηv(1−λ)
   - Difference = η(λ−1)(Δ − 4v)/4 ≠ 0 in general

**Numerical example:** With v = 10, Δ = 5 (where p̲ = v − Δ = 5 is the lower bound and p̄ = v + Δ = 15 is the upper bound of the price range), η = 1, λ = 2:
- U\_sell(10) = 10 + 1·5·(1−2)/4 = **8.75**
- U\_no-sell = 10 + 1·10·(1−2) = **0**
- These are clearly not equal (**8.75 ≠ 0**)

See [Part (iii) Detailed Analysis](#part-iii--wrong-both-method-and-result) below for the full explanation with counterexamples and the correct approach.

---

## Original Question

> Given this question, except for Part 3, is the answer correct? If not, can you pinpoint exact steps and methods where we went wrong?

## Summary of Findings

| Part | Computations | Result | Verdict |
|------|-------------|--------|---------|
| (i)  | ✅ Correct (given assumed reference) | ✅ Correct | ✅ OK |
| (ii) | ✅ Correct (given assumed reference) | ✅ Correct | ✅ OK |
| (iii)| ❌ Invalid linearity argument | ❌ Result does NOT hold in general | ❌ Wrong |
| (iv) | ✅ Derivative is correct | ⚠️ Conclusion relies on wrong Part (iii); Step 4 consistency is wrong | ⚠️ Partially wrong |
| **Final answer** | — | Sell iff p > v | ✅ **Correct** (but proof path is flawed) |

---

## Detailed Analysis

### Part (i): ✅ Correct

The expressions for U\_sell(p) are correct under the assumed "always sell" reference.

**What's right:**
- Consumption utility: m(0) + m(p) = p ✓
- Car dimension gain-loss: μ(0 − 0) = 0 ✓ (reference car = 0, actual car = 0)
- Money dimension: correctly split at p' = p into gain region [p̲, p] and loss region [p, p̄] ✓
- Integral formulation is correct ✓

**Final formula is correct:**

$$U_{\text{sell}}(p) = p + \frac{1}{\bar{p}-\underline{p}} \left[ \eta\int_{\underline{p}}^{p}(p-p')\,dp' + \eta\lambda\int_{p}^{\bar{p}}(p-p')\,dp' \right]$$

---

### Part (ii): ✅ Correct

The expressions for U\_no-sell are correct under the assumed reference.

**What's right:**
- Consumption utility: m(v) + m(0) = v ✓
- Car dimension: actual = v, reference = 0 → gain μ(v) = ηv ✓
- Money dimension: actual = 0, reference = p' > 0 → always a loss μ(−p') = −ηλp' ✓
- Integration using E[p'] = v (mean of symmetric distribution) ✓
- Independence from p ✓

**Final formula is correct:**

$$U_{\text{no-sell}} = v + \eta v(1 - \lambda)$$

---

### Part (iii): ❌ Wrong (both method and result)

The student already acknowledges this part may have issues. Here is the precise diagnosis:

#### Error 1: Invalid use of "linearity"

The student writes: μ(v − p') = μ(v + (−p')) = μ(v) + μ(−p')

**This is wrong.** The function μ is defined as:

$$\mu(x) = \begin{cases} \eta x & \text{if } x \geq 0 \\ \eta\lambda x & \text{if } x < 0 \end{cases}$$

This is **piecewise linear** (linear within each piece, no curvature), but it is **NOT additive** across the kink at zero. The property μ(a + b) = μ(a) + μ(b) fails when a and b have different signs. Here a = v > 0 and b = −p' < 0 always have opposite signs, so this property cannot be used.

**Why it fails — the key intuition:** The loss-aversion kink at zero means losses are weighted by λ > 1 relative to gains. Splitting v − p' into μ(v) + μ(−p') applies the loss multiplier λ to the full −p' term, but the correct computation should only apply λ to the portion of v − p' that is actually negative (if any).

**Counterexample 1:** Let v = 10, p' = 3 (so v − p' = 7 > 0, a gain):
- μ(v − p') = μ(7) = 7η
- μ(v) + μ(−p') = μ(10) + μ(−3) = 10η + (−3ηλ) = η(10 − 3λ)
- For λ = 2: correct value = 7η, but student's method gives η(10 − 6) = 4η ≠ 7η ❌

**Counterexample 2:** Let v = 10, p' = 12 (so v − p' = −2 < 0, a loss):
- μ(v − p') = μ(−2) = −2ηλ
- μ(v) + μ(−p') = μ(10) + μ(−12) = 10η + (−12ηλ) = η(10 − 12λ)
- For λ = 2: correct value = −4η, but student's method gives η(10 − 24) = −14η ≠ −4η ❌

**General formula for the error:**
μ(v) + μ(−p') − μ(v − p') = ηp'(λ − 1) when v > p' (gain case), and = −ηv(λ − 1) when v < p' (loss case). Since λ > 1, the error is always nonzero.

#### Error 2: The result U\_sell(v) = U\_no-sell does NOT hold under the "always sell" reference

By direct computation (verified symbolically), substituting p = v into U\_sell:

$$U_{\text{sell}}(v) = v + \frac{\eta\Delta(1 - \lambda)}{4}$$

where Δ = p̄ − v = v − p̲ is the half-spread of the price distribution (recall the distribution is centered at v, i.e., p̄ − v = v − p̲ by the problem setup).

Meanwhile:

$$U_{\text{no-sell}} = v + \eta v(1 - \lambda)$$

**The difference is:**

$$U_{\text{sell}}(v) - U_{\text{no-sell}} = \frac{\eta(\lambda - 1)(\Delta - 4v)}{4}$$

These are equal **only when Δ = 4v**, which is not true in general. Under the "always sell" reference, U\_sell(v) ≠ U\_no-sell for arbitrary price spreads.

**Numerical verification:**

| Parameters | U\_sell(v) | U\_no-sell | Equal? |
|-----------|-----------|-----------|--------|
| v=10, Δ=5, η=1, λ=2 | **8.75** | **0** | ❌ No |
| v=5, Δ=3, η=0.5, λ=3 | **4.25** | **0** | ❌ No |
| v=5, Δ=20, η=1, λ=2 (special: Δ=4v) | **0** | **0** | ✅ Yes (special case only) |

---

### Part (iv): ⚠️ Partially Wrong

#### ✅ Derivative computation is CORRECT

The Leibniz rule application is correct:

$$\frac{dU_{\text{sell}}}{dp} = 1 + \frac{\eta(p - \underline{p}) + \eta\lambda(\bar{p} - p)}{\bar{p} - \underline{p}} > 0$$

Both boundary terms vanish (since the integrand is zero at p' = p), and the partial derivatives under the integral are both 1. Since η > 0, λ > 1, and all terms are positive, U\_sell is strictly increasing in p. ✓

#### ✅ U\_no-sell is independent of p ✓

#### ❌ The conclusion relies on Part (iii) which is wrong

The logic "U\_sell increasing + U\_no-sell constant + **equal at v**" would correctly imply "sell iff p > v" — but the crucial third premise (Part iii) is not established. Without proving U\_sell(v) = U\_no-sell, we cannot determine the threshold.

#### ❌ Step 4: PPE consistency argument is WRONG

The student claims:

> "This strategy is self-confirming: the reference point (the price lottery) does not change based on whether the realized price is above or below v"

**This is incorrect.** If the strategy is "sell iff p > v", the reference lottery is:
- With probability 1/2: outcome (0, p) with p ~ U[v, p̄] (sold)
- With probability 1/2: outcome (v, 0) (kept car)

This is **different** from the assumed "always sell" reference (0, p') with p' ~ U[p̲, p̄]. The strategy is NOT self-confirming with the assumed reference.

---

## Correct Approach

To properly establish the PPE, use the **endogenous reference** corresponding to a threshold strategy.

### Setup

Consider a threshold strategy: sell iff p ≥ p\*. The reference lottery F depends on p\*:
- With probability α = (p̄ − p\*)/(p̄ − p̲): sell → outcome (0, p) with p ~ U[p\*, p̄]
- With probability β = (p\* − p̲)/(p̄ − p̲): don't sell → outcome (v, 0)

### Equilibrium condition

For the threshold p\* to be consistent, the seller must be indifferent at p = p\*:

$$U_{\text{sell}}(p^*) = U_{\text{no-sell}}(p^*)$$

where both utilities are computed with the reference corresponding to threshold p\*.

### Derivation

Computing the full gain-loss utilities with the endogenous reference and imposing the equilibrium condition yields:

$$p^*(1 + \beta\eta + \alpha\eta\lambda) = v(1 + \alpha\eta + \beta\eta\lambda)$$

### Verification that p\* = v is a solution

At p\* = v: since the distribution is centered at v, we have α = β = 1/2.

- LHS = v(1 + η/2 + ηλ/2)
- RHS = v(1 + η/2 + ηλ/2)

**LHS = RHS ✓**

This confirms p\* = v satisfies the equilibrium condition with the correct endogenous reference.

### Uniqueness and PPE

The equilibrium equation is quadratic in p\*, yielding two solutions:
1. **p\* = v** (the interior solution)
2. **p\* = [Δη(λ+1) + 2Δ − ηv(λ−1)] / [η(λ−1)]** — obtained by solving the quadratic equilibrium equation; this second root typically falls outside the valid price range [p̲, p̄] (e.g., for v=10, Δ=5, η=1, λ=2 it gives p\*=15=p̄, i.e., the boundary "never sell" strategy)

Since U\_sell is strictly increasing in p, the interior PE (p\* = v) gives strictly higher ex ante expected utility than the boundary PE. Therefore, the strategy **"sell if and only if p > v"** is the **unique Preferred Personal Equilibrium (PPE)**.

---

## Summary of All Errors

### In Parts (i) and (ii) — no computational errors
The computations are internally correct given the assumed "always sell" reference. However, this reference is valid only for analyzing whether "always sell" is a PE — it does not directly establish the "sell iff p > v" result.

### In Part (iii) — two errors
1. **Invalid linearity**: μ(x + y) = μ(x) + μ(y) does NOT hold for the piecewise-linear loss-aversion function
2. **Result is false**: Under the "always sell" reference, U\_sell(v) ≠ U\_no-sell in general

### In Part (iv) — two errors
1. **Conclusion depends on wrong Part (iii)**: Without U\_sell(v) = U\_no-sell, the threshold argument doesn't follow
2. **PPE consistency (Step 4) is wrong**: The "always sell" reference is NOT consistent with the "sell iff p > v" strategy

### Final answer
Despite the flawed proof, the final answer **"sell iff p > v"** is **correct**. It can be properly established using the endogenous reference approach shown above.
