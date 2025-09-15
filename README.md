# Product Recommendation System — Market Basket Analysis (MBA)

A practical Market Basket Analysis project for an e-commerce dataset to uncover product associations and enable smarter cross-sell, inventory optimization, and targeted marketing. As part of academic project. 

---

## 1) Overview

In competitive online retail, predicting and understanding co-purchasing behavior is key to improving customer experience and sales. We apply **Association Rule Mining** (Apriori) to discover product affinities and generate actionable rules for cross-selling and merchandising. :contentReference[oaicite:0]{index=0}

---

## 2) Problem Statement

How can we identify robust item associations from transaction data to:
- recommend complementary products,
- optimize inventory and promotions, and
- support targeted marketing flows? :contentReference[oaicite:1]{index=1}

---

## 3) Dataset

**Source:** UCI Machine Learning Repository (Online Retail, 2010-12-01 to 2011-12-09), UK-based non-store retailer.  
**Main fields:** `InvoiceNo`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `UnitPrice`, `Country`. :contentReference[oaicite:2]{index=2}

---

## 4) Method

We use **Market Basket Analysis (MBA)** via association rules:
- **Support** — frequency of itemset in transactions  
- **Confidence** — reliability of the rule X⇒Y  
- **Lift** — strength of association beyond chance

This supports:
- Discovery of product associations
- Cross-selling strategy design
- Inventory & placement decisions
- Campaign refinement (bundles, emails, PDP recommendations) :contentReference[oaicite:3]{index=3}

---

## 5) Workflow

1. **EDA & Data Understanding**
   - Identify negatives (refunds/damages), missing descriptions, inconsistencies, and a right-skewed distribution of items per invoice.  
2. **Preprocessing**
   - Filter cancellations/negatives where appropriate  
   - Handle rare items and class imbalance  
   - Normalize/encode as needed  
3. **Association Rule Mining**
   - Apriori frequent itemsets
   - Rule generation + threshold tuning (support/confidence/lift)
4. **Evaluation & Visualization**
   - Compare rule volumes/quality across thresholds
   - Inspect top single vs. multi-item consequents
5. **Interpretation & Business Mapping** :contentReference[oaicite:4]{index=4}

---

## 6) Data Issues & Handling

- **Negative prices/quantities:** indicate returns or special cases → filtered or treated separately  
- **Missing values:** especially in `Description` → cleaned/standardized  
- **Inconsistent product text:** harmonized where possible  
- **Right-skewed items/invoice:** acknowledged in threshold choices  
- **Rare items & imbalance:** tuned support to avoid noise from ultra-rare SKUs :contentReference[oaicite:5]{index=5}

---

## 7) Threshold Tuning — Key Findings

We compared several (support, confidence) settings:

- **(0.05, 0.50):** Many rules; includes weak to moderate associations; useful for broad discovery.  
- **(0.05, 0.70):** Fewer rules; low-reliability rules filtered out; retains strong candidates.  
- **(0.10, 0.70):** Much stricter; only top-frequency rules survive; can be too narrow for this dataset.  
- **(0.06, 0.70):** Balanced; surfaces frequent associations and reveals additional stable patterns.  

**Takeaway:**  
- Increasing **support** reduces rule count and focuses on more frequent, meaningful patterns.  
- Increasing **confidence** boosts reliability, but the **support threshold** has a larger impact on the overall rule set. Choose thresholds according to business goals (coverage vs. precision). :contentReference[oaicite:6]{index=6}

---

## 8) Example Associations (Illustrative)

Frequent co-occurrences include variants within the same family or complementary items, e.g.:

- *Charlotte Bag Pink Polkadot* ↔ *Strawberry Charlotte Bag*  
- *Retrospot Cake Cases* ↔ *Regency Cakestand 3-tier*  
- *Lunch Bag Cars Blue* ↔ *RED RETROSPOT CHARLOTTE BAG*  

(See notebook visuals for the complete set.) :contentReference[oaicite:7]{index=7}

---

## 9) How to Run

1. **Clone repo & open the notebook:**
   - `ecommerce.ipynb` — end-to-end pipeline (EDA → preprocessing → Apriori → rules/plots).  
2. **Environment (Python ≥3.10):**
   - `pandas`, `numpy`, `mlxtend`, `scikit-learn`, `matplotlib` (or `plotly`), `seaborn` (optional)
3. **Steps:**
   - Load data (provide CSV path in the notebook)
   - Execute cells sequentially
   - Adjust `min_support`, `min_confidence`, and `min_lift` to explore trade-offs
   - Export rules to CSV for downstream use (marketing/merchandising)

> Tip: Start with `min_support=0.06, min_confidence=0.70, min_lift>1.0`, then widen/narrow to match business coverage.

---

## 10) Repository Structure


├── ecommerce.ipynb # Full analysis & rule mining pipeline
├── data/ # (Place raw/cleaned CSVs here)
├── outputs/
│ ├── rules/ # Exported rules CSVs
│ └── plots/ # Figures for threshold comparisons
└── README.md # This file

---

## 11) Results & Discussion → Key Insights

- **Support is the main dial** for rule volume and generality; confidence refines reliability.  
- Low-to-moderate support uncovers more patterns (incl. long tail); stricter support surfaces stable, high-impact bundles.  
- Top rules align with intuitive product families and giftable sets, validating merchandising heuristics. :contentReference[oaicite:8]{index=8}

---

## 12) Limitations & Future Work

- **Text quality & rare SKUs:** Improve description standardization and product taxonomy mapping.  
- **Seasonality & time-aware rules:** Mine per-month/season to capture shifts.  
- **User-level personalization:** Combine MBA with user embeddings or sequence models.  
- **A/B testing:** Validate uplift from cross-sell widgets and curated bundles in production. :contentReference[oaicite:9]{index=9}

---

## 13) Practical Uses

- **PDP/Cart Widgets:** “Frequently bought together” recommendations  
- **Bundles & Promotions:** Auto-generate bundle candidates by lift/support  
- **Inventory & Placement:** Co-locate and forecast complementary demand  
- **CRM/Email:** Rule-driven next-best-offer segments

---

## 14) License

This project is for educational purposes. Check data source terms before redistribution.
