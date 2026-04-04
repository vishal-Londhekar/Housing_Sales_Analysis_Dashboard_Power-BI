# 🏡 Danish Housing Market Sales Analytics — Power BI Business Intelligence Dashboard

<p align="center">
  <img src="https://img.shields.io/badge/Tool-Power%20BI%20Desktop-F2C811?logo=powerbi&logoColor=black" />
  <img src="https://img.shields.io/badge/Domain-Real%20Estate%20%7C%20Housing%20Market%20Analytics-2e86ab" />
  <img src="https://img.shields.io/badge/Dashboard%20Pages-3-blueviolet" />
  <img src="https://img.shields.io/badge/Records-100%2C000%20Transactions-orange" />
  <img src="https://img.shields.io/badge/Period-1992–2024%20(32%20Years)-blue" />
  <img src="https://img.shields.io/badge/Status-Production%20Ready-brightgreen" />
</p>

---

## 📌 Table of Contents

- [Business Problem](#-business-problem)
- [Project Objective](#-project-objective)
- [Dataset Description](#-dataset-description)
- [Data Cleaning & Preparation](#-data-cleaning--preparation)
- [Data Modeling](#-data-modeling)
- [Key KPIs & Metrics](#-key-kpis--metrics)
- [Dashboard Walkthrough](#-dashboard-walkthrough)
- [Business Insights](#-business-insights)
- [Business Recommendations](#-business-recommendations)
- [Tools & Technologies](#-tools--technologies)
- [How to Use](#-how-to-use)
- [Project Structure](#-project-structure)
- [Screenshots](#-screenshots)
- [Author](#-author)

---

## 🧩 Business Problem

### The Real Estate Industry Challenge

The Danish housing market — one of Northern Europe's most mature and data-rich property ecosystems — presents a complex analytical challenge for every participant. Buyers, sellers, investors, mortgage lenders, urban planners, and government policymakers all operate in a market shaped by forces that interact in non-obvious ways: **interest rate cycles, inflation dynamics, geographic supply-demand imbalances, property type preferences, and macro-economic shocks**.

Without a unified analytical view across these dimensions, each stakeholder makes high-stakes decisions in isolation:

**1. Buyers Overpay or Miss the Market**
Without visibility into price-per-square-metre trends by region, house type, and macro-economic context, buyers cannot distinguish a fair price from an overvalued property. They lack comparative intelligence to negotiate from a position of knowledge.

**2. Sellers Misprice Their Properties**
Sellers who don't understand their local market's offer-to-purchase dynamics — whether properties sell above or below asking, and by how much — routinely leave money on the table or price themselves out of the market.

**3. Investors Cannot Identify Value Zones**
Property investors need a multi-dimensional view of regional yield potential, price momentum, and macro-economic headwinds (rising rates, inflation) to allocate capital efficiently. A single-metric approach misses the risk-adjusted opportunity entirely.

**4. Mortgage Lenders Lack Market Context for Risk Assessment**
Banks and mortgage institutions need to understand regional price volatility, offer-to-purchase gaps, and the macro environment to calibrate lending risk appropriately. A 32-year transaction view provides the cycle context that single-year data cannot.

### Who Benefits

| Stakeholder | Business Value |
|---|---|
| **Property Investors** | Identify highest-value regions and property types by risk-adjusted return |
| **Homebuyers** | Understand fair-value benchmarks and optimal timing relative to interest rate cycles |
| **Real Estate Agencies** | Position listings accurately using regional and property-type price intelligence |
| **Mortgage Banks** | Calibrate loan risk using regional volatility and macro-economic correlation data |
| **Urban Planners & Government** | Identify supply-constrained regions driving price escalation |
| **Property Developers** | Select house types and locations with the strongest demand fundamentals |

---

## 🎯 Project Objective

This project delivers a **three-page, interactive Power BI dashboard** built on 100,000 Danish residential property sales records spanning 32 years (1992–2024), enriched with macroeconomic indicators. It transforms transactional data into structured, decision-ready market intelligence.

**Business Goals:**
- Provide a 32-year price trend view across house types, regions, and macro-economic cycles
- Quantify the regional price premium — particularly the Capital Region (Copenhagen) vs. Jutland divergence — to guide geographic investment allocation
- Surface the relationship between mortgage interest rates, inflation, bond yields, and housing prices to support cycle-aware market timing
- Enable sales type performance analysis (regular vs. family vs. auction) to reveal true market pricing dynamics

**Analytical Goals:**
- Build calculated columns and DAX measures: YOY Sales Growth, Median Sales Price Change, Last 12-Month Sales, YTD Sales, Average SQM Price, and Offer-to-SQM Ratio
- Enable multi-dimensional drill-through via four interactive slicers (Region, Area, City, Sales Type)
- Deploy a Key Drivers AI visual to identify primary statistical drivers of purchase price variation
- Visualise macro-economic indicator correlation with housing prices through a combo chart

---

## 📋 Dataset Description

### Source

| Property | Detail |
|---|---|
| **Primary File** | `Housing_Data.csv` |
| **Schema Reference** | `Housing_Data_Column_Definitions.xlsx` (19 field definitions) |
| **Records** | 100,000 residential property transactions |
| **Time Period** | January 1992 – October 2024 (32 years, 130 quarters) |
| **Geography** | Denmark — 4 regions, 8 areas, hundreds of cities |
| **Missing Values** | `city` (11 nulls), `dk_ann_infl_rate%` (77 nulls), `yield_on_mortgage_credit_bonds%` (77 nulls) |

### Full Field Dictionary

#### 📅 Temporal Fields

| Field | Type | Description |
|---|---|---|
| `date` | Date | Transaction recording date (daily granularity — 1992 to 2024) |
| `quarter` | String | Fiscal quarter label — e.g., `2024Q3` |

#### 🏠 Property Identification & Classification Fields

| Field | Type | Description & Value Distribution |
|---|---|---|
| `house_id` | Integer | Unique property identifier |
| `house_type` | String | Villa (54,214 / 54%), Apartment (19,354 / 19%), Summerhouse (11,344 / 11%), Townhouse (10,184 / 10%), Farm (4,904 / 5%) |
| `sales_type` | String | Regular sale (88,232 / 88%), Family sale (8,224 / 8%), Other (2,489 / 2.5%), Auction (1,055 / 1%) |
| `year_build` | Integer | Year of construction — range: 1000–2024, mean: 1955 |
| `address` | String | Street address |
| `zip_code` | Integer | Postal code |
| `city` | String | Municipality city (e.g., København S, Horsens, Aalborg) |
| `area` | String | District / zone (e.g., Capital Copenhagen, South Jutland, North Zealand) |
| `region` | String | Administrative region: Jutland (49,937), Zealand (39,740), Fyn & islands (9,264), Bornholm (1,059) |

#### 💰 Price & Size Fields

| Field | Type | Key Statistics |
|---|---|---|
| `purchase_price` | Integer (DKK) | **Primary KPI.** Min: 250K, Median: 1.40M, Mean: 1.93M, Max: 46M DKK |
| `sqm_price` | Float (DKK/m²) | Median: 12,071 DKK/m², Mean: 16,407 DKK/m², Max: 75,000 DKK/m² |
| `sqm` | Integer (m²) | Property size — Min: 26m², Median: 123m², Mean: 129m², Max: 984m² |
| `no_rooms` | Integer | Rooms: 1–15, Mode: 4 rooms (28,117 properties) |
| `%_change_between_offer_and_purchase` | Integer (%) | Negative = sold below asking. Mean: −2.1%, Median: 0%. Range: −49% to +49% |

#### 📈 Macroeconomic Fields

| Field | Type | Description |
|---|---|---|
| `nom_interest_rate%` | Float (%) | Nominal mortgage interest rate at time of sale. Range: 0%–9.5%, Mean: 1.68% |
| `dk_ann_infl_rate%` | Float (%) | Annual Danish CPI inflation rate |
| `yield_on_mortgage_credit_bonds%` | Float (%) | Danish mortgage credit bond yield — key lending cost indicator. Mean: 4.1% |

---

## 🔧 Data Cleaning & Preparation

### Missing Value Treatment

**`city` — 11 null values (0.01%):**
Negligible proportion. Records retained with `BLANK()` in city-dependent visuals — valid for all non-city aggregations.

**`dk_ann_infl_rate%` and `yield_on_mortgage_credit_bonds%` — 77 nulls each (0.08%):**
These correspond to Q4 2024 transactions where final macroeconomic data has not yet been published by Statistics Denmark. Treated as `BLANK()` in Power BI — macro indicator visuals dynamically exclude these records from averages to prevent zero-inflation distortion.

### Transformations Applied

**Date Parsing:**
The `date` field is ingested as string and converted to a proper Date data type in Power Query, enabling the native Date Hierarchy (`Year → Quarter → Month → Day`) used in the Sales Performance Analysis page drill-through.

**Calculated Column — `Age`:**
```
Age = 2024 - year_build
```
Enables property age-based segmentation in the Key Drivers AI visual and property vintage analysis.

**Calculated Column — `Offer Price`:**
Back-calculated from `purchase_price` and `%_change_between_offer_and_purchase` to reconstruct the original listing price. This derived field enables the Offer-to-Purchase ratio analysis and `Offer to SQM Ratio by Sales Type` visual.

### DAX Measures Created

| Measure Name | Business Purpose |
|---|---|
| `YOY_Sales_Growth` | Market momentum — % change in transaction count vs. same quarter prior year |
| `Median Sales Price Change` | Quarter-on-quarter median price delta — trend direction indicator |
| `Units Sold in Last Year & Quarter` | Rolling 12-month + latest quarter transaction count |
| `Last 12 Month Sales` | Annualised market volume for current activity assessment |
| `Total YTD Sales` | Year-to-date transaction value for annual performance tracking |
| `Average Price SQM` | Average SQM price in current filter context — comparability metric |
| `Sales By Region` | Transaction count by region — geographic distribution measure |
| `Offer to SQM Ratio` | Avg Offer Price ÷ Avg SQM Price — listing price efficiency indicator |

---

## 🗄️ Data Modeling

### Schema Design

The model uses a **single flat-table schema** with one primary fact table (`Housing`) and one measures table (`Measures Table 2`):

```
┌────────────────────────────────────────────────────────────┐
│                  Housing (Primary Fact Table)               │
│                      100,000 records                        │
├──────────────────────────────┬─────────────────────────────┤
│  DIMENSION FIELDS            │  MEASURE FIELDS             │
│  ──────────────────          │  ──────────────────         │
│  house_id (PK)               │  purchase_price             │
│  date → Date Hierarchy       │  sqm_price                  │
│  house_type                  │  sqm                        │
│  sales_type                  │  no_rooms                   │
│  region                      │  %_change_offer_purchase    │
│  area                        │  nom_interest_rate%         │
│  city                        │  dk_ann_infl_rate%          │
│  zip_code / address          │  yield_on_mortgage_bonds%   │
│  year_build                  │                             │
│                              │  CALCULATED COLUMNS         │
│                              │  ──────────────────         │
│                              │  Offer Price (derived)      │
│                              │  Age (2024 − year_build)    │
└──────────────────────────────┴─────────────────────────────┘
                  │
┌─────────────────▼────────────────────────────────────────── ┐
│              Measures Table 2 (DAX Calculation Layer)        │
│                                                              │
│  YOY_Sales_Growth     │  Total YTD Sales                    │
│  Median Price Change  │  Average Price SQM                  │
│  Units Sold (YQ)      │  Sales By Region                    │
│  Last 12 Month Sales  │  Offer to SQM Ratio                 │
└─────────────────────────────────────────────────────────────┘
```

### Why Single-Table Architecture?

Each record represents one transaction — all temporal, geographic, property, and macroeconomic dimensions are captured at the same grain. The single-table design:
- Allows all four slicer filters to propagate correctly without complex relationship management
- Derives the Date Hierarchy natively from the `date` column without a separate calendar table
- Keeps all DAX measures in the same filter context — no RELATED() complexity or cross-table ambiguity

### Slicer Architecture — 4 Cascading Interactive Filters

| Slicer | Field | Behaviour |
|---|---|---|
| Region | `Housing.region` | Top-level geographic filter — 4 values |
| Area | `Housing.area` | Sub-filters within selected Region — 8 areas |
| City | `Housing.city` | Sub-filters within selected Area — hundreds of cities |
| Sales Type | `Housing.sales_type` | Cross-cuts all geographic selections — 4 transaction categories |

---

## 📐 Key KPIs & Metrics

### Market-Level Summary KPIs

| KPI | Value | Business Significance |
|---|---|---|
| **Total Transactions** | 100,000 | 32-year statistically robust market panel |
| **Median Purchase Price** | 1,400,000 DKK | Market mid-point — less distorted by luxury outliers than mean |
| **Mean Purchase Price** | 1,926,000 DKK | 38% gap between mean and median signals strong luxury segment skew |
| **Median SQM Price** | 12,071 DKK/m² | Cross-property and cross-region comparability benchmark |
| **Peak SQM Price** | 75,000 DKK/m² | Luxury apartment ceiling — Capital Region premium |
| **Median Offer-to-Purchase Change** | 0% | 64% of sales close exactly at asking price |
| **Properties Sold Above Asking** | 2,268 (2.3%) | Competitive bidding is rare — peaked at 6.9% in 2021 (COVID surge) |
| **Properties Sold Below Asking** | 33,765 (33.8%) | Systematic downward negotiation — mean discount: 2.1% |

### Regional Price Benchmarks

| Region | Transactions | Median Price (DKK) | Median SQM Price (DKK/m²) | Premium vs. Jutland |
|---|---|---|---|---|
| **Zealand (Copenhagen)** | 39,740 | **1,850,000** | **17,061** | **+73%** |
| Fyn & islands | 9,264 | 1,202,000 | 10,227 | Parity |
| Jutland | 49,937 | 1,200,000 | 9,837 | Baseline |
| Bornholm | 1,059 | 875,000 | 8,147 | −17% |

### Property Type Benchmarks

| House Type | Count | Median Price (DKK) | Avg Offer Discount |
|---|---|---|---|
| **Apartment** | 19,354 | **1,950,000** | −1.3% (lowest discount) |
| Farm | 4,904 | 1,700,000 | −1.6% |
| Townhouse | 10,184 | 1,720,000 | −1.6% |
| Villa | 54,214 | 1,300,000 | −2.4% |
| Summerhouse | 11,344 | 977,500 | −2.6% (highest discount) |

### Sales Type Pricing Divergence

| Sales Type | Count | Median Price (DKK) | Discount vs. Regular Sale |
|---|---|---|---|
| Regular Sale | 88,232 | 1,475,000 | Baseline |
| Other Sale | 2,489 | 1,087,596 | −26% |
| Family Sale | 8,224 | 950,000 | **−35.6%** |
| Auction | 1,055 | 850,000 | **−42%** |

---

## 🖥️ Dashboard Walkthrough

*A stakeholder-ready analytical narrative for each of the three dashboard pages.*

---

### 🏘️ Page 1 — Housing Market Overview

**Visual Types:** 2 KPI Cards + Line Chart + Bar Chart + Scatter Chart + Shape
**Key Metrics:** `Units Sold in Last Year & Quarter`, `Last 12 Month Sales`, `YOY_Sales_Growth`, `Median Sales Price Change`
**Custom Branding:** Header `1.png` image + branded shape elements

**Presenting to Stakeholders:**

The page opens with two headline KPI cards establishing current market scale: how many units transacted in the most recent reporting year-quarter, and the rolling 12-month volume. These living numbers answer the first question every property market participant asks: *"Is the market active right now?"*

**Year-on-Year Sales Growth by Sales Type (Bar Chart):**
This market momentum indicator breaks YOY volume growth by transaction category. A pattern where regular sales grow while auction volumes spike is a classic early-recession signal — distressed sellers begin appearing at auction. Conversely, surging regular sales alongside contracting auctions signals healthy, demand-driven market conditions. The bar chart tells the market cycle story at a glance and arms a real estate fund manager with the context to decide whether to accelerate acquisitions or enter a holding pattern.

**Median Sales Price Change Over Time (Line Chart):**
The 32-year price trend line narrates the full Danish housing cycle story:
- **1992–2004:** Stable, modest appreciation in a low-rate environment
- **2004–2007:** Rapid bubble acceleration — prices overshoot fundamentals
- **2008–2013:** Correction and prolonged stagnation following the financial crisis
- **2014–2021:** Sustained recovery accelerating through COVID stimulus and zero-rate policy
- **2022–2024:** Remarkable resilience despite rising interest rates — prices hold at 2.0M DKK median

**Regional Price Scatter Chart:**
Each region is plotted by transaction volume vs. median purchase price, immediately revealing that Zealand (Capital Region) dominates on both dimensions — the highest-priced and most liquid market. Bornholm sits at the opposite corner: low volume, low price. This geographic segmentation view enables investors to consciously position between high-competition/high-return (Zealand) and lower-competition/emerging-value markets (Jutland, Bornholm).

**Decisions This Page Enables:**
- Market timing — buyer's market or seller's market based on YOY volume trends?
- Regional capital allocation — which regions show momentum vs. stagnation?
- Cycle positioning — where in the 32-year historical cycle does the current market sit?

---

### 📊 Page 2 — Sales Performance Analysis

**Visual Types:** 2 Bar Charts + Data Table + Donut Chart + Key Drivers AI Visual
**Key Measures:** `Total YTD Sales`, `Average Price SQM`, `Offer to SQM Ratio`, `Sales By Region`
**Date Drill-Through:** Year → Quarter → Month → Day hierarchy on bar charts

**Presenting to Stakeholders:**

This page answers the operational question: *"How is market performance distributed, and what statistically drives price variation across the 100,000 transactions?"*

**Sales by Region — Donut Chart:**
The regional market share donut immediately establishes Jutland (~50%) and Zealand (~40%) as the two dominant markets, with Fyn & islands and Bornholm as secondary. For a property developer allocating land acquisition budget across Denmark, this chart establishes where the addressable market volume is — and the Page 1 regional scatter confirms which market commands the best return per transaction. Volume × price premium is the investor's product.

**Offer to SQM Ratio by Sales Type (Bar Chart):**
The pricing intelligence centrepiece of the page. By comparing offer price per square metre against transaction price per square metre for each sales type, the visual surfaces systematic pricing gaps that are invisible in absolute price analyses:
- **Auction sales:** Offer-to-SQM ratios significantly below regular — distressed pricing at acute discount
- **Family sales:** Intra-family wealth transfer at 35.6% below regular market rates — creates nearby valuation distortions
- **Regular sales:** The market-rate benchmark all other types are assessed against

**Total YTD Sales and Average SQM Price (Bar Charts with Date Drill-Through):**
The Date Hierarchy enables a mortgage banker to navigate from annual sales totals → quarterly performance → monthly patterns — the granularity unavailable in static market reports. Identifying which specific quarters drive annual anomalies is the first step toward seasonal pricing strategy.

**Key Drivers AI Visual:**
Power BI's AI-driven Key Drivers visual identifies the primary statistical factors predicting `purchase_price` variation across all 100,000 records:
- **Region:** Zealand properties carry a ~73% SQM price premium over Jutland — the single largest structural driver
- **House Type:** Apartments in the Capital Region command the highest per-SQM values
- **Property Age:** Properties under 10 years command a 68% price premium over 40–60-year stock
- **Number of Rooms:** Non-linear premium — each additional room adds disproportionately above 5 rooms

**Decisions This Page Enables:**
- Portfolio construction — which sales types offer the most predictable transaction dynamics?
- SQM pricing targets — what price should a developer target for a new development in a given region?
- Performance review — which quarters represent the strongest market window for listing a property?

---

### 🏠 Page 3 — House Type Analysis

**Visual Types:** 2 Clustered Bar Charts + Line-Column Combo Chart + 4 Slicers
**Key Fields:** `house_type`, `Avg Offer Price`, `Avg purchase_price`, `sqm`, `sqm_price`, `nom_interest_rate%`, `dk_ann_infl_rate%`, `yield_on_mortgage_credit_bonds%`
**Interactive Slicers:** Region, Area, City, Sales Type (all Dropdown, all cascading)

**Presenting to Stakeholders:**

This is the most interactive page — combining the most granular property analysis with the full macro-economic context. Four cascading slicers allow stakeholders to isolate any combination of geography and transaction type, dynamically refiltering all three visuals.

**AVG Offer Price vs. Purchase Price by House Type (Clustered Bar Chart):**
Side-by-side bars for each of the five house types compare average listing price against average transaction price. The gap between these two bars tells the negotiation story per property type. When filtered to `Region = Zealand` + `Sales Type = regular_sale`:
- **Apartments** show the smallest gap — urban apartments are most liquid and price-efficient
- **Villas** show the largest absolute gap — larger properties carry more negotiating room
- **Summerhouses** show the highest percentage discount — leisure properties attract the most buyer negotiation power

**AVG SQM vs. SQM Price by House Type (Clustered Bar Chart):**
The companion visual revealing the density-value relationship. Apartments occupy the smallest average footprint but command the highest SQM price. Farms are the largest properties at the lowest SQM rate. This directly answers the investor question: *"Which property type offers the best value density and liquidity?"* — the answer is consistently Apartments in Zealand.

**AVG Inflation / Interest Rate / Mortgage Yield by House Type (Line-Column Combo Chart):**
This macro-economic overlay is the dashboard's most contextually powerful visual. It renders the three macroeconomic indicators (nominal interest rate, annual inflation rate, mortgage credit bond yield) alongside transaction volume patterns by house type — revealing which property categories sustain activity in high-rate environments vs. which face sharp volume contractions.

The critical macro narrative visible in this chart: during the **zero nominal rate era (2013–2021)**, housing prices rose 43% from 1.375M to 1.97M DKK. When rates rose to 3.5% by 2024, the market showed counter-intuitive resilience — prices fell only 2.3% in 2022, then recovered to a new high of 2.0M DKK by 2024. This price stickiness in a rising-rate environment — particularly for Apartments and Villas — signals that **supply constraints, not just cheap credit, are the fundamental driver** of Danish housing values.

**Decisions This Page Enables:**
- Property type selection — which type maintains the best price support in rising-rate environments?
- Macro timing — when rates are at X%, which property types historically show the strongest price resilience?
- Geographic micro-market isolation — combining Region + Area + City + Sales Type slicers for hyper-local analysis

---

## 💡 Business Insights

> *Translating 32 years of Danish housing data into actionable market intelligence.*

### Insight 1 — The Copenhagen Premium Is Structural, Not Cyclical — And It Has Been Widening for 30 Years

Zealand's median SQM price (17,061 DKK/m²) is **73% higher** than Jutland's (9,837 DKK/m²). This gap has expanded throughout the dataset — from parity in the early 1990s to the current substantial premium. It is driven by urbanisation, employment concentration, and persistent housing supply constraints in Greater Copenhagen. This is not speculative inflation — it is a structural economic reality. Investors incorporating this premium into long-term capital allocation theses are not speculating; they are following the data.

### Insight 2 — Apartments Are the Most Price-Efficient and Demand-Resilient Asset Class

With a mean SQM price of 31,553 DKK/m² in Zealand apartments vs. 13,507 DKK/m² for villas nationally, apartments command the highest density value and the smallest offer-to-purchase discount (−1.3%). Their stronger price efficiency reflects higher demand relative to supply and superior liquidity. For investors building rental portfolios, the per-SQM premium apartments command translates directly into higher rental yields and faster resale timelines.

### Insight 3 — The Zero-Rate Era Created Exceptional Returns That Rising Rates Have Not Reversed

During eight years of zero nominal rates (2013–2021), median prices rose 43% from 1.375M to 1.97M DKK. When rates returned to 3.52% by 2024, the expected correction did not materialise — prices recovered to 2.0M DKK (Q3 2024). This resilience proves that **supply constraints, not merely cheap credit, are the primary price driver** in the Danish housing market. Investors waiting for a rate-driven price correction should recalibrate their assumptions — the 32-year data does not support it.

### Insight 4 — Family Sales Create a 35.6% Systemic Discount — An Invisible Valuation Distortion

8,224 family sale transactions closed at a median of 950,000 DKK vs. 1,475,000 DKK for regular sales — a **35.6% below-market transfer** for intra-family wealth management purposes. These are not market-clearing prices — they are intentional discounts. However, they create valuation distortions in nearby comparables. Sophisticated buyers who understand when adjacent properties were sold as family transactions can avoid being anchored to artificially low comparables when negotiating regular-market purchases.

### Insight 5 — The COVID Volume Surge (2020–2021) Reversed; The Price Gains Did Not

Transaction volumes surged 34% from 5,849 in 2019 to 7,837 in 2021 while prices rose 15%. As rates rose in 2022, volumes fell 30% to 5,437. But prices only dipped 2.3% — then recovered. This **price stickiness** reveals that Danish sellers have significant reservation prices: they withdraw from the market rather than accepting deep discounts, maintaining price floors even during adverse rate environments. Sellers who held in 2022 and returned to market in 2023–2024 were vindicated by the data.

### Insight 6 — New Properties (< 10 Years) Command a 68% Premium Over Mid-Age Stock

Properties built within the last decade command a median of 2,250,000 DKK vs. 1,348,000 DKK for 60–100-year-old properties — a 68% newness premium that is statistically the strongest property-characteristic driver of price beyond location. For developers, this premium more than justifies the construction cost differential between greenfield new-build and mid-century renovation. The data makes the economic case for new construction in constrained markets.

### Insight 7 — Auction Sales Represent a 42% Structural Discount — A Contrarian Institutional Opportunity

The 1,055 auction transactions in the dataset transacted at a median of 850,000 DKK — 42% below the 1,475,000 DKK regular sale median. Critically, these distressed properties are **not geographically concentrated** in low-demand areas — they appear across all regions, including Zealand. For institutional buyers with the due-diligence capacity to assess condition and title risk, the auction channel represents the single most systematic pricing discount in the Danish market.

### Insight 8 — 1-Bedroom Properties Command the Highest SQM Price — Signalling a Compact Housing Supply Gap

Single-room properties command 27,799 DKK/m² vs. 12,330 DKK/m² for 7-room properties — nearly 2.3x higher per square metre for the smallest properties. This counter-intuitive premium reveals an acute supply shortage in the compact urban housing segment. Small-footprint properties in urban centres face the most intense demand relative to available stock, making 1- and 2-bedroom development the most price-resilient niche in the current Danish housing market.

---

## 💼 Business Recommendations

**1. Reallocate Investment Weighting Toward Zealand Apartments in High-Rate Environments**
Zealand apartments show the smallest price dislocation during rising rate cycles (−1.3% offer discount vs. −2.4% for villas). Institutional investors should weight their Danish property portfolio toward urban apartments when the nominal rate exceeds 2.5% — this segment consistently defends its price floor better than any other property-type/region combination in the 32-year dataset.

**2. Develop a Family Sale Identification System for Nearby Opportunity Mapping**
Real estate agencies should build a pipeline that flags recently completed family sale transactions in a postcode. These below-market closings create comparables distortions — making adjacent regular-sale listings appear over-priced when they are fairly valued. Agents with this intelligence can pre-empt buyer objections and accelerate transactions in family-sale-affected micro-markets.

**3. Target Summerhouse Buyers Outside Peak Season for Maximum Negotiation Leverage**
Summerhouses show the highest systematic discount (−2.55%) and the lowest competitive bidding rate. This category gives buyers the most negotiating power — particularly outside the June–August leisure season. Buyer-side advisors should structure offers 5–8% below asking on summerhouses, particularly in Jutland and Bornholm where supply is least constrained.

**4. Configure Power BI Data Alerts on YOY Sales Growth for Automated Market Signal Notifications**
The `YOY_Sales_Growth` measure should trigger automated Data Alerts via Power BI Service when crossing pre-defined thresholds: >+15% growth signals a heating market requiring supply response; <−10% signals a cooling market requiring pricing strategy review. This transforms the dashboard from retrospective reporting into a **real-time market signal system** for property fund managers.

**5. Launch a Premium New-Build Advisory Service Leveraging the Age Premium**
The 68% price premium for properties under 10 years is systematically under-utilised in agency pricing models. A specialist advisory service quantifying the exact new-build premium by city and property type — derived from the SQM price differential visible in this dataset — could command premium advisory fees while delivering measurably better pricing outcomes for new-build developer clients.

**6. Develop a Bornholm Early-Entry Investment Thesis Ahead of Emerging Urbanisation**
Bornholm's median SQM price (8,147 DKK/m²) represents a 52% discount to the Zealand benchmark. Improving digital infrastructure, ferry connectivity, and remote-work adoption position Bornholm as a potential early-stage urbanisation opportunity. Investors who entered the Fyn market 10–15 years early captured 13,600 DKK/m² appreciation. The Bornholm thesis is supported by current pricing data and macro-demographic trends — the entry window remains open.

**7. Establish an Auction Channel Advisory Practice for Institutional Buyers**
The 42% auction discount vs. regular sales — present across all regions — creates a systematic value-capture opportunity for institutional buyers with due-diligence capacity. A dedicated auction monitoring and pre-bid assessment service, built on this dataset's geographic and pricing data, could generate consistent alpha for a property fund willing to accept the execution complexity of auction acquisitions.

---

## 🛠️ Tools & Technologies

| Tool / Technology | Role in Project |
|---|---|
| **Microsoft Power BI Desktop** | Primary BI platform — data modeling, DAX, dashboard design |
| **Power Query (M Language)** | Data ingestion, date parsing, null handling, data type assignment |
| **DAX (Data Analysis Expressions)** | 8 calculated measures + 2 calculated columns (`Age`, `Offer Price`) |
| **CSV Source** | `Housing_Data.csv` — 100,000 rows × 19 fields |
| **Excel Schema Reference** | `Housing_Data_Column_Definitions.xlsx` — 19 field definitions |
| **Power BI Key Drivers AI Visual** | Automated statistical driver identification for `purchase_price` variation |
| **Date Hierarchy (Power BI Native)** | Year → Quarter → Month → Day drill-through on `date` field |
| **Line-Column Combo Chart** | Macro overlay (interest rate + inflation + bond yield) vs. price trends |
| **Custom Brand Assets** | Two PNG images embedded for professional dashboard identity |
| **Interactive Slicers (4)** | Region, Area, City, Sales Type — all Dropdown, cascading cross-page filters |
| **Power BI Service** | Cloud publishing and automated Data Alert configuration |

---

## ▶️ How to Use

### Prerequisites

- **Microsoft Power BI Desktop** — free download from [powerbi.microsoft.com/desktop](https://powerbi.microsoft.com/desktop/)
- Windows OS (Power BI Desktop is Windows-native; Mac users access via Power BI Service browser)
- No external database required — all data is embedded inside the `.pbix` file

### Opening the Dashboard

```
1. Clone or download this repository to your local machine
2. Open: Housing_Sales_Analysis.pbix in Power BI Desktop
3. The embedded data model loads automatically — no data connection setup required
4. Navigate between pages via the bottom tabs:
      ├── Housing Market Overview       →  KPIs + 32-year trend line + YOY growth + scatter
      ├── Sales Performance Analysis    →  Regional donut + Key Drivers AI + drill-through tables
      └── House Type Analysis           →  Offer/Purchase comparison + macro overlay + 4 slicers
```

### Interacting with the Dashboard

**Geographic Multi-Level Filtering (House Type Analysis page):**
```
→ Select a Region (e.g., Zealand) from the Region slicer
→ Area slicer auto-updates to Zealand areas only
→ Select an Area (e.g., Capital, Copenhagen)
→ City slicer updates to cities in that area
→ All three page visuals dynamically update to the isolated geography
→ Add Sales Type = regular_sale for clean market-rate analysis
```

**Date Drill-Through (Sales Performance Analysis page):**
```
→ Click on any bar in the YTD Sales or Average SQM Price bar charts
→ Click the drill-down arrow: Year → Quarter → Month granularity
→ Identify which specific periods drive performance anomalies
→ Right-click → Drill Up to return to annual view
```

**Key Drivers AI Exploration:**
```
→ On Sales Performance Analysis page, interact with the Key Drivers visual
→ Toggle between "What influences purchase_price to increase?" 
→ Switch between "Key Influencers" tab (individual factors) and "Top Segments" tab (combinations)
→ Use findings to build investment thesis around the highest-impact property characteristics
```

**Publishing and Alerting via Power BI Service:**
```
→ Home ribbon → Publish → select your Power BI workspace
→ In Power BI Service, navigate to the Housing Market Overview page
→ Click the KPI card → set Data Alert thresholds on YOY_Sales_Growth
→ Configure email notifications when market growth crosses +15% or drops below −10%
```

---

## 📁 Project Structure

```
Danish-Housing-Market-Analytics/
│
├── Housing_Sales_Analysis.pbix            # Power BI workbook — all data + visuals + DAX embedded
│
├── Housing_Data.csv                       # Source dataset — 100,000 transactions × 19 fields
│
├── Housing_Data_Column_Definitions.xlsx   # Field dictionary — 19 column definitions with descriptions
│
├── Screenshots/                           # Dashboard page exports
│   ├── 01_Housing_Market_Overview.png     # KPIs, 32-year price trend, YOY growth, regional scatter
│   ├── 02_Sales_Performance_Analysis.png  # Regional donut, Key Drivers AI, date drill-through
│   └── 03_House_Type_Analysis.png         # Offer/Purchase bars, macro overlay, 4 slicers
│
└── README.md                              # Project documentation (this file)
```

### Internal Power BI Model Reference

| Component | Detail |
|---|---|
| **Dashboard Pages** | 3 (Housing Market Overview, Sales Performance Analysis, House Type Analysis) |
| **Visual Types** | Line Chart, Scatter, Bar (×3), Clustered Bar (×2), Combo Chart, Donut, Table, Cards (×2), Key Drivers AI, Slicers (×4), Shapes (×3) |
| **Source Table** | `Housing` — 100,000 records × 19 fields |
| **Measures Table** | `Measures Table 2` — 8 DAX measures |
| **Calculated Columns** | 2 (`Age`, `Offer Price`) |
| **Date Hierarchy** | Native Power BI: Year → Quarter → Month → Day |
| **Slicers** | 4 Dropdown (Region → Area → City → Sales Type — cascading) |
| **AI Visual** | Key Drivers visual on Sales Performance Analysis page |

---

## 📸 Screenshots

> *Export pages from Power BI Desktop: File → Export → Export to PDF. Save individual page captures to the `Screenshots/` folder.*

### Page 1 — Housing Market Overview
<img width="1300" height="722" alt="image" src="https://github.com/user-attachments/assets/d36c5eb0-d124-4ff9-b4cd-4b138ae1e27c" />

> Two KPI cards (Units Sold, 12-Month Sales) + 32-year median price trend line + YOY Sales Growth bar chart by sales type + regional price scatter chart. Custom branded header image.

### Page 2 — Sales Performance Analysis
<img width="1324" height="719" alt="image" src="https://github.com/user-attachments/assets/40492611-136c-4069-870e-fa1cd78c4df6" />

> Sales by Region donut + YTD Sales and Average SQM Price bar charts with Year→Quarter→Month drill-through + Key Drivers AI visual + regional performance table.

### Page 3 — House Type Analysis
<img width="1310" height="717" alt="image" src="https://github.com/user-attachments/assets/87e26313-6556-4776-b379-58d5e52fecfe" />

> Offer vs. Purchase Price clustered bar chart + SQM vs. SQM Price clustered bar chart + macro-economic combo chart (interest rate + inflation + bond yield by house type) + 4 cascading dropdown slicers.

---

## 👤 Author

<table>
  <tr>
    <td align="center">
      <b>Vishal Londhekar</b><br/>
      <i>Data Analyst | Business Analyst</i><br/><br/>
      <a href="https://github.com/vishal-Londhekar">🔗 GitHub</a>
    </td>
  </tr>
</table>

> *"The Danish housing market is one of the most data-rich property ecosystems in the world — 32 years of transactions, macroeconomic cycles, and regional dynamics encoded in 100,000 rows. This dashboard transforms that complexity into the clarity that turns market knowledge into financial decisions."*

---

## ⭐ If this project strengthened your real estate analytics portfolio, please star the repository!

---

<p align="center">
  <img src="https://img.shields.io/badge/Built%20with-Power%20BI-F2C811?logo=powerbi" />
  <img src="https://img.shields.io/badge/Market-Danish%20Housing%201992–2024-2e86ab" />
  <img src="https://img.shields.io/badge/Transactions-100%2C000-orange" />
  <img src="https://img.shields.io/badge/Regions-4%20%7C%20House%20Types-5-blueviolet" />
  <img src="https://img.shields.io/badge/AI%20Feature-Key%20Drivers%20Visual-blue" />
</p>
