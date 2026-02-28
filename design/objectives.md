# 🎯 Netra: The 5-Layer Intelligence Framework

This document outlines the core architectural layers of **Netra**, a pre-disbursement fraud detection engine for Multi-Tier Supply Chain Finance (SCF).

---

## 1. 🛡️ Integrity Layer (Invoice Authenticity)
**Goal:** Establish the fundamental legitimacy of the transaction before complex analysis begins.
- **3-Way Matching:** Automated reconciliation between Purchase Orders (PO), Invoices, and Goods Receipt Notes (GRN).
- **Invoice Fingerprinting:** Uses cryptographic SHA-256 hashing to create a unique identifier for every invoice.
- **Double-Financing Prevention:** A privacy-preserving hash registry allows cross-bank checks without revealing sensitive client data.

## 2. 📊 Capacity Layer (Economic Feasibility)
**Goal:** Identify "Phantom Scaling" and economically impossible invoicing patterns.
- **Revenue Utilization Ratio (RUR):** Correlates the total financed volume against the supplier's declared annual revenue.
- **Tier-Alignment Analysis:** Ensures that the volume of goods supplied by Tier 2 aligns with the production output of Tier 1.
- **Historical Volume Spikes:** Statistical anomaly detection for sudden, unexplained increases in invoicing.

## 3. 🕸️ Graph Layer (Network Integrity)
**Goal:** Detect structural fraud patterns that are invisible at the individual invoice level.
- **Carousel Trade Detection:** Uses graph cycle detection algorithms (NetworkX) to find artificial revenue loops (A → B → C → A).
- **Centrality Anomaly Detection:** Identifies "Bridge Nodes"—small entities with unusually high influence in the supply chain network.
- **Relationship Gap Identification:** Flags sudden, high-volume transactions between entities with no prior historical connection.

## 4. 🌊 Propagation Layer (Exposure Stability)
**Goal:** Model systemic risk and financial "contagion" across the multi-tier network.
- **Risk Contagion Modeling:** Calculates how risk spreads from a fraudulent Tier 1 node to its financially dependent Tier 2 and Tier 3 partners.
- **Exposure Amplification:** Measures the total systemic impact of a single fraudulent node.
- **Stress Simulation:** Predicts the solvency of downstream entities if a primary supplier or buyer fails.

## 5. ⚖️ Decision Layer (Explainable AI)
**Goal:** Provide actionable, transparent verdicts for banking credit officers.
- **Composite Risk Aggregation:** A weighted scoring system that combines findings from all four analytical layers.
- **Rule-Based Justification:** Outputs clear, human-readable reasons for every "Block" or "Review" decision.
- **Confidence Scoring:** Indicates the reliability of the fraud signal based on the number and severity of triggered indicators.
