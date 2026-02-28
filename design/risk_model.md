# 📊 Netra: Risk Calculation Model

This document specifies the mathematical formulas and logic used to calculate base risk, propagation, and composite scoring in the **Netra** engine.

---

## 1. Base Risk Calculation (BR)

Base risk is the initial fraud probability assigned to an entity based on its primary activities.

$$BR = (w_I \cdot R_I) + (w_E \cdot R_E) + (w_N \cdot R_N)$$

Where:
- **$R_I$ (Integrity Risk):** Score from 3-way matching and fingerprinting.
- **$R_E$ (Economic Risk):** Score derived from Revenue Utilization Ratio (RUR).
- **$R_N$ (Network Risk):** Score from cycle detection and centrality analysis.
- **$w_I, w_E, w_N$:** Assigned weights (e.g., 0.3, 0.4, 0.3).

---

## 2. Economic Feasibility Metric: RUR

The Revenue Utilization Ratio is the core metric for detecting "Phantom Scaling."

$$RUR = \frac{	ext{Total Financed Invoice Value (Annual)}}{	ext{Declared Annual Revenue}}$$

**Risk Mapping:**
- $RUR < 1$: Normal (Risk 0.1)
- $1 \le RUR < 2$: Elevated (Risk 0.3)
- $2 \le RUR < 4$: High (Risk 0.6)
- $RUR \ge 4$: Extreme / Impossible (Risk 0.9)

---

## 3. Propagation Risk (PR)

Propagation risk is the risk "inherited" by an entity based on its financial dependency on a risky partner.

$$PR_B = Risk_A 	imes Dependency_{A 	o B}$$

Where:
- **$Dependency_{A 	o B}$:** The percentage of Entity B’s revenue sourced from Entity A.

---

## 4. Composite Risk Aggregation (CRA)

The final risk score used for the pre-disbursement decision.

$$CRA = \sum (w_k \cdot R_k) + PR$$

**Thresholds and Decisions:**
- **CRA < 0.3:** Approve Disbursement (Low Risk)
- **0.3 \le CRA \le 0.6:** Manual Credit Review Required (Medium Risk)
- **CRA > 0.6:** Block Disbursement (High Risk)

---

## 5. Explainability Layer

For every `CRA > 0.3`, the system generates a justification string by identifying the highest contributor to the score.

*Example:* 
`IF RUR > 4.0: APPEND "PHANTOM_SCALING_DETECTED"`
`IF CYCLE_FOUND: APPEND "CIRCULAR_TRADE_DETECTED"`
