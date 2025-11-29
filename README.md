# Solow Growth Model – Econometrics Project

This repository contains the code, data preprocessing pipeline, and empirical analysis developed for a university econometrics project. The goal is to test the empirical validity of the **Solow Growth Model** and explore extensions that improve its explanatory power using modern cross-country data.

This README summarizes the project documented in the accompanying report.  [oai_citation:0‡solow_model.pdf](sediment://file_00000000d89471fc90b35860a46e22b1)

---

## 📌 Project Overview

The Solow Model predicts long-run economic growth as a function of:

- **Capital accumulation** (proxied by the saving rate)
- **Population growth**
- **Technological progress** (assumed constant across countries)

Under the Cobb–Douglas production function, the model implies that long-run income per capita depends:

- **positively** on the saving rate  
- **negatively** on population growth  

This project performs a **cross-country regression analysis** using World Bank data (2000–2023) to validate these theoretical predictions and test model extensions.

---

## 📊 Data Sources and Preprocessing

World Bank indicators used:

- GDP per capita — `NY.GDP.PCAP.CD`
- Population growth — `SP.POP.GROW`
- Gross saving rate — `NY.GNS.ICTR.ZS`
- Trade (% of GDP) — `NE.TRD.GNFS.ZS`

**Preprocessing steps:**

1. Convert datasets from wide → long format  
2. Remove aggregate entries (e.g. “World”)  
3. Exclude countries with missing values  
4. Merge datasets using **Country Name**  
5. Construct datasets for three alternative timeframes:
   - 2023 only  
   - 2000–2023 averages  
   - 2023 GDP with historical averages of fundamentals

See pages 1–3 of the PDF for details.  
 [oai_citation:1‡solow_model.pdf](sediment://file_00000000d89471fc90b35860a46e22b1)

---

## 📐 Model Specification

The main empirical model is:

\[
\ln(\text{gdp}) = \alpha + \beta \cdot \ln(\text{savings}) +
\gamma \cdot \ln(\text{population growth} + \delta + g) + \varepsilon
\]

Where:

- \( \delta + g = 0.05 \), following Mankiw, Romer & Weil (1992)
- \( \beta \): elasticity of income w.r.t. saving rate  
- \( \gamma \): elasticity w.r.t. population growth  

Model interpretation and theoretical background appear on pages 1–2.  
 [oai_citation:2‡solow_model.pdf](sediment://file_00000000d89471fc90b35860a46e22b1)

---

## 🧪 Key Results

### 1. Time-frame Comparison

Three regression datasets were tested:

| Specification | Summary |
|---------------|---------|
| **2023 only** | Lowest R²; short-run noise limits explanatory power |
| **Averages (2000–2023)** | Higher R²; coefficients strong & significant |
| **2023 GDP + historical averages** | Best performance; strongest alignment with Solow steady-state logic |

Breusch–Pagan tests indicate heteroskedasticity in most cases.  
(Results on page 3.)  
 [oai_citation:3‡solow_model.pdf](sediment://file_00000000d89471fc90b35860a46e22b1)

---

### 2. Country Group Analysis

Using a **Chow test**, the dataset is divided into:

- All countries  
- Excluding major natural resource exporters  
- OECD members only  

**Findings:**

- Excluding high-resource-rent countries reduces heteroskedasticity  
- OECD countries show weaker traditional Solow patterns  
- Population growth is positively associated with GDP in OECD group  
- Savings elasticity is largest for OECD economies  

Interpretation on page 4.  
 [oai_citation:4‡solow_model.pdf](sediment://file_00000000d89471fc90b35860a46e22b1)

---

### 3. Model Extension — Trade Openness

Trade (% of GDP) is added as:

\[
\text{ltrade} = \ln(\text{trade share})
\]

**Findings:**

- Trade is consistently **positive and significant**  
- Improves model fit (higher R²)  
- Preserves significance of core Solow variables  
- OECD results show weaker coefficients due to multicollinearity and structural differences  

See regression tables on page 5.  
 [oai_citation:5‡solow_model.pdf](sediment://file_00000000d89471fc90b35860a46e22b1)

---

### 4. Solow Parameter Validation

A restricted version of the model imposes:

\[
\beta = -\gamma
\]

This implies a capital share:

\[
\alpha = 1 - \beta = 0.33
\]

A t-test shows the implied coefficient (\(\beta = 0.5\)) cannot be rejected (p = 0.75), supporting the canonical Solow value of \( \alpha = 1/3 \).  
(See page 6.)  
 [oai_citation:6‡solow_model.pdf](sediment://file_00000000d89471fc90b35860a46e22b1)

---

## 📁 Repository Structure
├── data/                 # Processed datasets
├── scripts/              # Preprocessing and regression scripts
├── figures/              # Plots and model outputs
├── solow_model.pdf       # Full project report (source)
└── README.md             # Project documentation