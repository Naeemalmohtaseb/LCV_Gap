# Environmental Justice Gap Analysis: Identifying Underrepresented Communities

## Executive Summary

This project analyzes the intersection of environmental burden and political representation across 3,500+ U.S. counties, revealing critical gaps where communities facing the highest environmental hazards receive the least political advocacy. By combining EPA's EJSCREEN environmental data, CDC's Social Vulnerability Index, and League of Conservation Voters (LCV) scorecard data, this analysis identifies 197 counties experiencing extreme "justice gaps" affecting over 11.5 million Americans.

**Key Finding:** Communities with high environmental burdens are systematically underrepresented in environmental policy-making, with Republican-represented counties showing a +0.59 justice gap compared to -1.43 for Democratic counties—a 2.02-point disparity that demands urgent attention.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Methodology](#methodology)
3. [Key Findings](#key-findings)
4. [Technical Implementation](#technical-implementation)
5. [Data Sources](#data-sources)
6. [Installation & Usage](#installation--usage)
7. [Interactive Dashboard](#interactive-dashboard)
8. [Future Enhancements](#future-enhancements)
9. [Policy Implications](#policy-implications)
10. [Contact](#contact)

## Project Overview

### The Problem

Environmental justice communities—predominantly low-income and minority populations—bear a disproportionate burden of environmental hazards while often lacking adequate political representation to advocate for their needs. This project quantifies this "justice gap" by creating a novel metric that combines:

* **Environmental Burden**: Exposure to pollutants, proximity to hazardous facilities, and other environmental risks
* **Political Representation**: Congressional representatives' environmental voting records (LCV scores)
* **Social Vulnerability**: Community resilience factors including poverty, education, and demographic composition

### Research Questions

1. Which communities face the highest environmental burdens with the least political representation?
2. How do justice gaps vary by political party, geography, and demographics?
3. What is the scale of population affected by severe environmental justice gaps?
4. Which states and counties should be prioritized for intervention?

## Methodology

### Justice Gap Index 2.0

The project introduces a sophisticated **Justice Gap Index 2.0** that uses Z-score normalization to create comparable metrics across diverse geographies:

```
Justice Gap Index = Burden Z-score - LCV Z-score

Where:
- Positive values indicate underrepresentation (high burden, low advocacy)
- Negative values indicate overrepresentation (low burden, high advocacy)
- Values > 2 indicate extreme gaps requiring urgent intervention
```

### Data Integration Pipeline

1. **Census Tract Level Analysis**

   * 86,082 census tracts analyzed from EJSCREEN 2024
   * Population-weighted aggregation to county level
   * Handles 230 environmental and demographic variables

2. **County-Level Integration**

   * Merged with CDC Social Vulnerability Index (3,144 counties)
   * Matched to congressional districts via spatial analysis
   * Linked to representative LCV scores (548 members of Congress)

3. **Population Weighting**

   * All environmental metrics weighted by tract population
   * Prevents rural bias in burden calculations
   * Reveals true human impact of environmental hazards

### Statistical Analysis

* **Regression Modeling**: OLS regression explains 5.2% of LCV score variation through environmental burden
* **Demographic Disparity Analysis**: Calculates burden rates by race and income
* **Spatial Clustering**: Identifies geographic patterns in justice gaps
* **Party Comparison**: T-tests confirm significant differences between party representations

## Key Findings

### 1. Extreme Justice Gaps Affect Millions

* **197 counties** (6% of total) have extreme justice gaps exceeding 2 standard deviations
* **11.5 million Americans** live in the 50 highest-gap counties
* **6.4 million** reside in the top 100 priority counties

### 2. Partisan Disparity in Environmental Representation

| Party      | Avg Justice Gap | Counties | Population | Avg LCV Score |
| ---------- | --------------- | -------- | ---------- | ------------- |
| Republican | +0.59           | 2,343    | 168.4M     | 18.95%        |
| Democratic | -1.43           | 966      | 166.0M     | 71.68%        |

The 2.02-point gap between parties represents fundamentally different approaches to environmental protection.

### 3. Demographic Disproportionality

Communities of color and low-income populations face systematically higher environmental burdens:

* **People of Color**: 1.83x more likely to live in high-burden areas (44.5% vs 24.3% baseline)
* **Low-Income**: 1.54x higher exposure rate (37.5% vs 24.3% baseline)
* These disparities persist even after controlling for geographic and economic factors

### 4. Geographic Concentration

| State        | Avg Gap Score | Priority Counties | Notable Issues                       |
| ------------ | ------------- | ----------------- | ------------------------------------ |
| Oklahoma     | 0.417         | 11                | Extreme gaps, oil/gas pollution      |
| Arkansas     | 0.386         | 11                | Agricultural runoff, low LCV scores  |
| South Dakota | 0.361         | 6                 | Native American communities affected |
| Louisiana    | 0.341         | 3                 | Cancer Alley, petrochemical burden   |
| Mississippi  | 0.339         | 3                 | Historic environmental racism        |

### 5. Extreme Cases Requiring Immediate Attention

Top 5 Priority Counties:

1. **Muskogee County, OK**: Gap = 3.92, Pop = 66,606
2. **Buffalo County, SD**: Gap = 3.87, Pop = 1,859 (largely Native American)
3. **Todd County, SD**: Gap = 3.84, Pop = 9,353
4. **Seminole County, OK**: Gap = 3.81, Pop = 23,592
5. **Texas County, OK**: Gap = 3.80, Pop = 21,144

## Technical Implementation

### Technology Stack

* **Python 3.8+**: Core analysis engine
* **Pandas/NumPy**: Data manipulation and computation
* **Plotly Dash**: Interactive web dashboard
* **GeoPandas**: Spatial analysis and congressional district mapping
* **Scikit-learn**: Statistical modeling
* **Matplotlib/Seaborn**: Static visualizations

### Key Components

1. **Data Processing Pipeline**

   * Loads and cleans three major datasets
   * Performs population-weighted aggregation
   * Creates composite vulnerability scores

2. **Justice Gap Calculation**

   * Implements Z-score normalization
   * Calculates Justice Gap Index 2.0
   * Performs demographic disparity analysis

3. **Interactive Dashboard**

   * Real-time filtering and exploration
   * Multiple synchronized visualizations
   * Export capabilities for further analysis

4. **Statistical Analysis**

   * Regression modeling
   * Party comparison statistics
   * Demographic burden calculations

## Data Sources

### 1. EPA EJSCREEN 2024

* 86,082 census tracts
* 230 indicators (air quality, hazardous proximity, demographics)

### 2. CDC Social Vulnerability Index (SVI) 2022

* 3,144 counties
* 15 social factors in 4 themes

### 3. LCV Scorecard 2023-2024

* 548 members of Congress
* Voting records, party affiliation, annual/lifetime scores

### 4. Congressional District Shapefiles

* 118th Congress
* TIGER/Line shapefiles from Census Bureau

## Installation & Usage

```bash
# Prerequisites
Python 3.8 or higher
pip install -r requirements.txt
```

### Quick Start

```bash
git clone https://github.com/yourusername/environmental-justice-gap.git
cd environmental-justice-gap
pip install -r requirements.txt
jupyter notebook environmental_justice_analysis.ipynb
python dashboard.py
```

Visit `http://localhost:8050` to use the dashboard

## Interactive Dashboard

### Features

1. **State-Level Choropleth Map**
2. **Party Comparison Visualization**
3. **Burden vs Representation Scatter Plot**
4. **Priority Counties Table**
5. **Demographic Disparity Charts**

### Deployment

* Local (Dash)
* Heroku / AWS / GitHub Pages

## Future Enhancements

1. **District-Level Accuracy**
2. **Time Series Analysis**
3. **Health Outcomes Integration**
4. **Machine Learning Forecasting**
5. **Real-time Monitoring**
6. **Global Comparisons**

## Policy Implications

* Prioritize funding to high-gap counties
* Track representation gaps for accountability
* Reform permitting and regulatory thresholds
* Targeted green job investment in high-burden areas

## Acknowledgments

* EPA EJSCREEN Team
* CDC SVI Team
* League of Conservation Voters
---

*"In a world of environmental injustice, data can illuminate the path to equity. This project aims to transform numbers into action, statistics into justice, and analysis into advocacy."*
