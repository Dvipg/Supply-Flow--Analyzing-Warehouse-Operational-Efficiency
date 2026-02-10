# Warehouse Operational Efficiency EDA Roadmap (SupplyFlow)

## 1) Dataset familiarity checklist (non-coding)

**Dataset files in repo**
- `SupplyFlow FMCG Solutions.xlsx` (main data table).
- `Data Description.docx` (data dictionary / business definitions).

**Quick dataset snapshot (from the Excel sheet)**
- Rows: **25,000** data rows (25,001 including header).
- Columns: **24** fields.
- Field list (as header row):
  - `Ware_house_ID`
  - `WH_Manager_ID`
  - `Location_type`
  - `WH_capacity_size`
  - `zone`
  - `WH_regional_zone`
  - `num_refill_req_l3m`
  - `transport_issue_l1y`
  - `Competitor_in_mkt`
  - `retail_shop_num`
  - `wh_owner_type`
  - `distributor_num`
  - `flood_impacted`
  - `flood_proof`
  - `electric_supply`
  - `dist_from_hub`
  - `workers_num`
  - `wh_est_year`
  - `storage_issue_reported_l3m`
  - `temp_reg_mach`
  - `approved_wh_govt_certificate`
  - `wh_breakdown_l3m`
  - `govt_check_l3m`
  - `product_wg_ton`

**Data dictionary alignment (from Data Description)**
- Confirm the meaning and units of each variable (e.g., “issues in last 3 months”, “distance from hub”, binary indicators).
- Identify which columns are categorical, binary indicators, or numeric metrics.

---

## 2) EDA roadmap (step-by-step, consulting style)

### Step A — Data audit (structure + quality)
1. **Schema review**
   - Verify data types (numeric vs categorical vs binary flags).
   - Check for ID columns and treat them as identifiers (not features).
2. **Missingness / completeness**
   - Missing value counts & percentage per column.
   - Decide treatment rules (drop, impute, or flag).
3. **Data consistency**
   - Validate ranges (e.g., negative values in counts or distances).
   - Confirm category labels are consistent (no spelling/case duplicates).

### Step B — Create the “Efficiency Index” (consulting KPI)
1. **Define KPI components**
   - Negative drivers: breakdowns, storage issues, transport issues, refill requests, flood impacts.
   - Positive drivers: workers count, electric backup, flood-proof, temperature regulation.
2. **Normalization**
   - Scale numeric features (min-max or z-score) before combining.
3. **Score design**
   - Construct a 0–100 index or standardized score.
   - Document the weight logic (equal weights or business-weighted).
4. **Efficiency classes**
   - Create “Efficient” vs “Inefficient” based on median or percentile split.

### Step C — Univariate EDA (single variable insights)
- Distributions for numeric fields (hist/box plots).
- Frequency tables for categorical/binary fields.
- Identify outliers or extreme values.

### Step D — Bivariate & multivariate EDA (drivers & relationships)
- **Efficiency score vs**
  - `workers_num` (staffing effect)
  - `dist_from_hub` (logistics distance effect)
  - `wh_est_year` (warehouse age effect)
- **Issue rates vs infra**
  - `storage_issue_reported_l3m` vs `temp_reg_mach`
  - `wh_breakdown_l3m` vs `electric_supply`
- **Regional variation**
  - `zone` and `WH_regional_zone` vs efficiency score.
- **Competitive pressure**
  - `Competitor_in_mkt` vs efficiency score / issue rates.

### Step E — Business interpretation layer
- Translate key relationships into operational stories:
  - Staffing gaps → higher breakdowns or delays.
  - Poor infrastructure → more storage issues.
  - Distance from hub → higher transport issues.
- Draft 3–5 “executive insights” with impact framing.

---

## 3) Suggested project file structure (no code yet)

```
.
├── data/
│   ├── raw/
│   │   └── SupplyFlow FMCG Solutions.xlsx
│   ├── docs/
│   │   └── Data Description.docx
│   └── processed/
│       └── (future cleaned data output)
├── notebooks/
│   ├── 01_data_audit.ipynb
│   ├── 02_eda_univariate.ipynb
│   ├── 03_eda_bivariate.ipynb
│   └── 04_efficiency_index.ipynb
├── reports/
│   ├── figures/
│   └── eda_findings.md
├── dashboards/
│   └── (Power BI / Tableau files)
├── docs/
│   ├── eda_roadmap.md
│   └── methodology.md
└── README.md
```

---

## 4) EDA output checklist (what we’ll deliver)

- Data quality summary table (missingness + types).
- Efficiency Index definition + distribution plot.
- Top 5 drivers and their effect direction.
- Regional performance comparison.
- Draft 5–7 actionable insights for recommendations.

---

## 5) Next approval gate (before coding)

- Confirm which tools you want to use for EDA (Python notebook / Excel / both).
- Confirm the Efficiency Index logic (equal weights vs business weights).
- Approve the proposed file structure or request edits.
