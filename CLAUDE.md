# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a COMP40610 Information Visualisation assignment analyzing Ireland's labour market data from CSO (Central Statistics Office). The project focuses on employment trends, examining differences across gender, age groups, education levels, and regions.

## Repository Structure

```
├── raw_datasets/           # Original CSV files from CSO High Value Datasets
│   ├── ALF01_Annual Employment Rate.csv
│   ├── ALF02_Annual Percentage of Part-time Work.csv
│   ├── ALF03_Annual Unemployment Rate.csv
│   ├── ALF04_Annual Long Term Unemployment Rate.csv
│   ├── ALF05_Annual Percentage of Potential Additional Labour Force.csv
│   ├── QLF50-Quarterly Employment Rate.csv
│   └── QLF51-Quarterly Unemployment and Long-term Unemployment Rate.csv
├── data_cleaning/          # Data processing pipeline
│   ├── data_cleaning.ipynb
│   └── combined_clean_data.csv
└── data_visualisation/     # Vega-Lite visualization specifications
    └── chart_1.vl.json
```

## Data Pipeline Architecture

**Raw Data → Cleaning → Combined Dataset → Visualizations**

1. **Raw Datasets**: Seven CSV files from CSO covering annual and quarterly labour market statistics
2. **Data Cleaning** (data_cleaning/data_cleaning.ipynb):
   - Combines five annual datasets into a single dataframe
   - Adds 'Statistic Label' column to identify metric type
   - Removes 'UNIT' column (all values are percentages)
   - Drops rows with missing 'VALUE' data
   - Outputs: combined_clean_data.csv (4,146 rows after cleaning from 7,704)
3. **Visualizations**: Vega-Lite JSON specifications for interactive charts

## Data Schema

The combined_clean_data.csv contains:
- **Statistic Label**: Employment Rate, Part-time Work Rate, Unemployment Rate, Long-term Unemployment Rate, Potential Labour Force
- **Year**: 2019-2024 (6 years)
- **Age Group**: 13 categories (e.g., "All ages", "15-24 years", "25-54 years", "55-74 years")
- **Sex**: Both sexes, Male, Female
- **Education Attainment Level**: 6 levels (0-8, primary, secondary, tertiary, etc.) - has some null values
- **NUTS 2 Region**: Ireland, Northern and Western, Southern, Eastern and Midland - has some null values
- **VALUE**: Percentage values for the statistic

## Research Questions

The analysis explores five main questions:
1. Gender differences in employment/unemployment rates across regions, education levels, and age groups
2. Gender differences in part-time work rates (examining family responsibility impact)
3. Labour market metrics by education level (with gender breakdown)
4. Temporal trends in employment/unemployment (quarterly/annual, including COVID-19 impact)
5. Age-specific employment patterns (youth vs. overall unemployment rates over time)

## Working with Jupyter Notebooks

This project uses Jupyter notebooks for data cleaning. When working with data_cleaning.ipynb:
- Dependencies: pandas, numpy, os (standard Python libraries)
- The notebook is self-contained and documents the cleaning process
- Execute cells sequentially to reproduce the cleaning pipeline

## Working with Vega-Lite Visualizations

Visualization files (*.vl.json) are Vega-Lite specifications:
- Reference the cleaned CSV data via GitHub raw URLs
- Use transforms for filtering (by year, statistic type, etc.)
- Common encodings: x (categorical), y (quantitative), color (by Sex)
- Can be viewed using Vega-Lite editor or embedded in web pages

## Data Access Notes

- The cleaned dataset is hosted on GitHub and accessed via raw URLs in visualization specs
- Token-based URLs in chart_1.vl.json may expire and need to be regenerated
- For local development, visualizations can reference local file paths instead
