# 🌊 Netra: Cascade & Exposure Logic

This document details the methods used to model financial "contagion" and systemic risk propagation across the supply chain.

---

## 1. Financial Dependency Ratio (FDR)
**Goal:** Measure how much a downstream supplier (Tier 2/3) depends on an upstream entity (Tier 1) for their survival.

$$FDR_{A 	o B} = \frac{	ext{Invoice Value from A to B}}{	ext{Total Revenue of Entity B}}$$

**Significance:**
- $FDR > 0.5$: High dependency; the entity is highly vulnerable to the failure of its partner.
- $FDR < 0.2$: Low dependency; the entity is diversified and has low contagion risk.

---

## 2. Exposure Amplification Factor (EAF)
**Goal:** Calculate the total systemic impact of a single fraudulent entity across the entire supply chain.

$$EAF = \frac{\sum 	ext{Downstream Financed Exposure}}{	ext{Root Entity Financed Exposure}}$$

**Insight:**
If $EAF = 10$, a ₹1 Cr fraud at the root level has amplified into ₹10 Cr of total systemic exposure for the bank.

---

## 3. Stress Simulation Logic (SSL)
**Goal:** Simulate the solvency of the network if a key node collapses due to fraud or insolvency.

**The "What-If" Algorithm:**
1.  **Select Node A:** Target node for removal.
2.  **Calculate Revenue Loss:** For all nodes $B$ where $A 	o B$ is an edge, subtract the invoice value from $B$'s current revenue.
3.  **Check Debt Coverage:** If $New\_Revenue_B < Total\_Debt\_Obligations_B$, flag Node $B$ as "Insolvent."
4.  **Recurse:** Repeat for all neighbors of Node $B$.

---

## 4. Systemic Risk Heatmapping
Based on the **EAF** and **FDR**, Netra generates a systemic heatmap for the bank's credit officer.
- **Red Zone:** High risk of domino-effect failure.
- **Yellow Zone:** Manageable exposure but requires monitoring.
- **Green Zone:** Isolated risk with no significant propagation potential.
