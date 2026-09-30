# House Prices Dataset Analysis

## Introduction

This project is an Excel data-exploration assignment on a house-price dataset. It examines which house characteristics are associated with sale price, with SalePrice as the target variable.

The workbook has two parts, and each uses a different dataset:

- **Practice Work** (sheet practice work) uses the first dataset, sheet train_HousingPrice. It covers 15 structured tasks on dataset size, variable types, missing values, descriptive statistics, grouped summaries, correlation, outliers and charts.
- **Business Problems** (sheets BP1 to BP12) use the second dataset, sheet train (3). Each sheet explores one topic: descriptive statistics, house quality, neighborhood, size, age, garage capacity, features, common house types, extreme prices, sale year, data quality and predictor selection.

## Dataset

| | train_HousingPrice (Practice Work) | train (3) (Business Problems) |
|---|---|---|
| Records (rows) | 1,460 | 1,460 |
| Variables (columns) | 23 | 81 (from Id to SalePrice) |
| Target variable | SalePrice | SalePrice |

### Practice Work: variable classification

| Classification | Variables |
|---|---|
| Categorical | MSSubClass |
| Ordinal | OverallQual (rating 1–10), OverallCond (rating 1–9) |
| Numerical | LotArea, MasVnrArea, BsmtFinSF1, BsmtUnfSF, TotalBsmtSF, 1stFlrSF, 2ndFlrSF, LowQualFinSF, GrLivArea, BsmtFullBath, BsmtHalfBath, FullBath, HalfBath, BedroomAbvGr, KitchenAbvGr, TotRmsAbvGrd, GarageYrBlt, GarageArea, OpenPorchSF, SalePrice |

### Business Problems: important variables

| Variable | Used for |
|---|---|
| SalePrice | Target variable in every Business Problem sheet |
| OverallQual | Quality vs price (BP1, BP2, BP9, BP12) |
| Neighborhood | Location vs price (BP3, BP12) |
| GrLivArea, 1stFlrSF, 2ndFlrSF, TotalBsmtSF | House size vs price (BP1, BP4, BP7, BP9, BP12) |
| YearBuilt, YearRemodAdd | House age vs price (BP1, BP5, BP12) |
| GarageCars, GarageArea | Garage capacity vs price (BP1, BP6, BP12) |
| BedroomAbvGr, FullBath, Fireplaces, OpenPorchSF, EnclosedPorch | House features vs price (BP7) |
| HouseStyle, BldgType, Foundation, RoofStyle, Heating | Frequency of common house types (BP8) |
| YrSold | Sale year vs price (BP10) |

## Practice Work

All items below use train_HousingPrice.

1. Dataset dimensions: number of rows and columns
2. Variable classification: Numerical, Categorical or Ordinal
3. Target variable identification: SalePrice
4. Missing-value analysis for all columns, flagging columns that need data-quality attention
5. Descriptive statistics for SalePrice
6. OverallQual vs SalePrice: summary table (house count, average and median price) and column chart
7. Neighborhood vs average SalePrice and number of houses: summary table and column chart
8. GrLivArea vs SalePrice: scatter plot and correlation
9. TotalBsmtSF and GarageArea vs SalePrice: correlations
10. SalePrice by YrSold: summary table and line chart
11. Box-and-whisker plot of SalePrice across OverallQual groups
12. Unusually high or low SalePrice values using quartiles and the IQR method
13. Correlation matrix (colour-scale heatmap) for OverallQual, TotalBsmtSF, GrLivArea, GarageArea and SalePrice
14. Written observations for the charts
15. A record of the Excel formula or chart method used for each question

## Descriptive Statistics

**SalePrice** (Practice Work; the extra rows come from BP1)

| Statistic | Result |
|---|---:|
| Count | 1,460 |
| Sum | 264,144,946 |
| Average (Mean) | 180,921.20 |
| Median | 163,000 |
| Mode | 140,000 |
| Minimum | 34,900 |
| Maximum | 755,000 |
| Range | 720,100 |
| Standard Deviation | 79,442.50 |
| Standard Error | 2,079.11 |
| Sample Variance | 6,311,111,264.30 |
| Kurtosis | 6.54 |
| Skewness | 1.88 |

**Selected variables** (BP1, train (3))

| Variable | Mean | Median | Std. Deviation | Minimum | Maximum |
|---|---:|---:|---:|---:|---:|
| OverallQual | 6.10 | 6 | 1.38 | 1 | 10 |
| GrLivArea | 1,515.46 | 1,464 | 525.48 | 334 | 5,642 |
| TotalBsmtSF | 1,057.43 | 991.5 | 438.71 | 0 | 6,110 |
| GarageCars | 1.77 | 2 | 0.75 | 0 | 4 |
| GarageArea | 472.98 | 480 | 213.80 | 0 | 1,418 |
| YearBuilt | 1,971.27 | 1,973 | 30.20 | 1,872 | 2,010 |

## Missing-Value Analysis

**Practice Work (train_HousingPrice)**

Missing values were checked for every column with COUNTBLANK. GarageYrBlt stores missing entries as the text NA, so it was checked with COUNTIF(..., "NA").

| Column | Missing values | Data-quality attention |
|---|---:|---|
| MasVnrArea | 8 | Yes |
| GarageYrBlt | 81 | Yes |
| All other 21 columns | 0 | No |

**Business Problems (train (3))**

- **BP11:** COUNTBLANK(A2:CC1461) returned **8** blank cells in total. SalePrice has 1,460 numeric values and 0 non-numeric values (COUNT, COUNTA). ISBLANK and ISNUMBER checks were run on the first SalePrice cell, and conditional formatting was applied to the SalePrice column. OverallQual was checked by counting houses rated 5 or below (538) and 8 or above (229).
- **BP12:** COUNTBLANK over the seven selected columns (SalePrice, OverallQual, GrLivArea, TotalBsmtSF, GarageCars, YearBuilt, Neighborhood) returned 0.

COUNTBLANK counts only empty cells. Some columns in train (3) also use the text NA (for example, Alley in the first record), which COUNTBLANK does not count.

## Outlier Analysis

The IQR method was applied to SalePrice in train_HousingPrice using QUARTILE.INC.

| Measure | Formula | Result |
|---|---|---:|
| Q1 | QUARTILE.INC(X2:X1461,1) | 129,975 |
| Q3 | QUARTILE.INC(X2:X1461,3) | 214,000 |
| IQR | Q3 − Q1 | 84,025 |
| Lower Bound | Q1 − 1.5 × IQR | 3,937.5 |
| Upper Bound | Q3 + 1.5 × IQR | 340,037.5 |
| Minimum SalePrice | MIN | 34,900 |
| Maximum SalePrice | MAX | 755,000 |

The minimum (34,900) is above the lower bound, and the maximum (755,000) is above the upper bound. A box-and-whisker plot was also created for SalePrice across OverallQual groups.

**BP9 (train (3))** also examined extreme prices using LARGE, SMALL and PERCENTILE.INC:

| Highest prices | Lowest prices | Percentile | SalePrice |
|---:|---:|---|---:|
| 755,000 | 34,900 | 5th | 88,000 |
| 745,000 | 35,311 | 25th | 129,975 |
| 625,000 | 37,900 | 75th | 214,000 |
| 611,657 | 39,300 | 95th | about 326,100 |
| 582,933 | 40,000 | | |

## Business Problems

These analyses use train (3). Each entry is named after its sheet title.

| # | Sheet | Focus | Variables | Methods and charts |
|---|---|---|---|---|
| BP1 | Descriptive statistics | Summary statistics and relationships between SalePrice and key factors | SalePrice, OverallQual, GrLivArea, TotalBsmtSF, GarageCars, GarageArea, YearBuilt | Descriptive-statistics tables, correlation matrix with colour scale, 6 scatter plots |
| BP2 | House quality vs price | Average and median SalePrice for each OverallQual rating (1–10) | OverallQual, SalePrice | AVERAGEIF, MEDIAN(FILTER), column chart, box-and-whisker plot |
| BP3 | Neighborhood vs price | SalePrice across neighborhoods (Sheet3 holds a PivotTable of average and count) | Neighborhood, SalePrice | AVERAGEIF, MEDIAN(FILTER), COUNTIF, PivotTable, bar chart, box-and-whisker plot |
| BP4 | House size vs price | Size variables against SalePrice | GrLivArea, 1stFlrSF, 2ndFlrSF, TotalBsmtSF, SalePrice | Correlation matrix with data bars, 4 scatter plots |
| BP5 | House age vs price | Build and remodel year against SalePrice, plus average price by construction period | YearBuilt, YearRemodAdd, SalePrice | AVERAGEIF(S), COUNTIF(S), correlation matrix, column chart, 2 scatter plots |
| BP6 | Garage capacity vs price | Garage variables against SalePrice | GarageCars, GarageArea, SalePrice | Correlation matrix, AVERAGEIF, COUNTIF, FILTER, scatter plot, column chart, box-and-whisker plot |
| BP7 | House features vs price | Bedrooms, bathrooms, fireplaces, basement and porch areas against SalePrice | BedroomAbvGr, FullBath, Fireplaces, TotalBsmtSF, OpenPorchSF, EnclosedPorch, SalePrice | Correlation matrix, AVERAGEIF, COUNTIF, FILTER, 4 scatter plots, column chart, box-and-whisker plot |
| BP8 | Common house types | How often each category occurs | HouseStyle, BldgType, Foundation, RoofStyle, Heating | COUNTIF, 5 column charts |
| BP9 | Extreme sale prices | Highest, lowest and percentile SalePrice values | SalePrice, OverallQual, GrLivArea | LARGE, SMALL, PERCENTILE.INC, box-and-whisker plot, 2 scatter plots |
| BP10 | SalePrice by year | Average and median SalePrice by year sold | YrSold, SalePrice | AVERAGEIF, MEDIAN(FILTER), column chart, line chart |
| BP11 | Data quality | Missing and non-numeric value checks | All columns, SalePrice, OverallQual | COUNTBLANK, COUNT, COUNTA, COUNTIF, ISBLANK, ISNUMBER, conditional formatting |
| BP12 | Price prediction | Which variables could serve as predictors of SalePrice | SalePrice (target); OverallQual, GrLivArea, TotalBsmtSF, GarageCars, YearBuilt, Neighborhood (predictors) | Role table, COUNTBLANK, correlation matrix with colour scale, 4 scatter plots |

## Excel Functions and Methods Used

**Functions**

| Category | Functions |
|---|---|
| Counting | COUNT, COUNTA, COUNTBLANK, COUNTIF, COUNTIFS |
| Summary statistics | SUM, AVERAGE, MEDIAN, MIN, MAX, STDEV.S |
| Conditional averages | AVERAGEIF, AVERAGEIFS |
| Filtering | FILTER (used inside MEDIAN and to build box-plot data) |
| Quartiles and rankings | QUARTILE.INC, PERCENTILE.INC, LARGE, SMALL |
| Correlation | CORREL |
| Data checks | ISBLANK, ISNUMBER |

**Methods**

- Variable classification (Numerical, Categorical, Ordinal)
- Descriptive statistics tables (mean, standard error, median, mode, standard deviation, variance, kurtosis, skewness, range, minimum, maximum, sum, count)
- IQR outlier method (Q1 − 1.5 × IQR and Q3 + 1.5 × IQR)
- Correlation matrices
- PivotTable (Sheet3: average and count of SalePrice by Neighborhood)
- Remove Duplicates (documented in the Practice Work method log for the neighborhood list)
- Conditional formatting: colour scales, data bars and cell-value rules

## Visualizations Used

- **Scatter plots** show the relationship between SalePrice and numeric variables: GrLivArea, OverallQual, TotalBsmtSF, GarageCars, GarageArea, YearBuilt, 1stFlrSF, 2ndFlrSF, YearRemodAdd, BedroomAbvGr, FullBath and OpenPorchSF (Practice Work, BP1, BP4, BP5, BP6, BP7, BP9, BP12).
- **Column and bar charts** compare average SalePrice across groups: OverallQual, Neighborhood, construction period, GarageCars, Fireplaces and YrSold (Practice Work, BP2, BP3, BP5, BP6, BP7, BP10).
- **Frequency column charts** show how many houses fall in each HouseStyle, BldgType, Foundation, RoofStyle and Heating category (BP8).
- **Line charts** show SalePrice by year sold (Practice Work, BP10).
- **Box-and-whisker plots** show the spread of SalePrice by OverallQual, Neighborhood, GarageCars and Fireplaces, plus overall SalePrice (Practice Work, BP2, BP3, BP6, BP7, BP9).
- **Correlation heatmaps** use colour-scale conditional formatting (Practice Work, BP1, BP5, BP6, BP7, BP12). BP4 uses data bars.

## Key Observations

**Overall SalePrice**

- The mean (180,921.20) is above the median (163,000). Skewness is 1.88 and kurtosis is 6.54.
- Prices range from 34,900 to 755,000.

**House quality (OverallQual)**

- Average SalePrice rises steadily with OverallQual, from 50,150 at rating 1 (2 houses) to 438,588.39 at rating 10 (18 houses). Median SalePrice follows the same pattern.
- Most houses sit in the middle ratings: 397 at rating 5, 374 at rating 6 and 319 at rating 7.
- OverallQual has the strongest correlation with SalePrice in both datasets (0.7910).

**Correlation with SalePrice**

| Variable | Correlation | Source |
|---|---:|---|
| OverallQual | 0.7910 | Practice Work, BP1 |
| GrLivArea | 0.7086 | Practice Work, BP1 |
| GarageCars | 0.6404 | BP1, BP6 |
| GarageArea | 0.6234 | Practice Work, BP1 |
| TotalBsmtSF | 0.6136 | Practice Work, BP1 |
| 1stFlrSF | 0.6059 | BP4 |
| FullBath | 0.5607 | BP7 |
| YearBuilt | 0.5229 | BP1, BP5 |
| YearRemodAdd | 0.5071 | BP5 |
| Fireplaces | 0.4669 | BP7 |
| 2ndFlrSF | 0.3193 | BP4 |
| OpenPorchSF | 0.3159 | BP7 |
| BedroomAbvGr | 0.1682 | BP7 |
| EnclosedPorch | −0.1286 | BP7 |

These are associations only. The analysis does not show that any variable causes changes in SalePrice.

**Neighborhood**

- Average SalePrice varies widely across the 25 neighborhoods. The highest averages are NoRidge (335,295.32, 41 houses), NridgHt (316,270.62, 77) and StoneBr (310,499, 25).
- The lowest averages are MeadowV (98,576.47, 17), IDOTRR (100,123.78, 37) and BrDale (104,493.75, 16).
- House counts also differ: NAmes has the most houses (225), followed by CollgCr (150).

**House size**

- Larger living, floor and basement areas are generally associated with higher prices. GrLivArea is the strongest of the size variables (0.7086).
- 1stFlrSF and TotalBsmtSF are strongly correlated with each other (0.8195).

**House age**

- Average SalePrice rises with construction period: 132,269.08 (before 1950), 147,545.23 (1950–1969), 161,954.33 (1970–1989), 228,404.22 (1990–1999) and 242,046.42 (2000–2009). The 2010-and-later group has one house (394,432).
- YearBuilt (0.5229) and YearRemodAdd (0.5071) both show moderate positive correlations with SalePrice.

**Garage and features**

- GarageCars and GarageArea are strongly correlated (0.8825).
- Average SalePrice by GarageCars: 103,317.28 (0 cars, 81 houses), 128,116.69 (1), 183,851.66 (2), 309,636.12 (3) and 192,655.80 (4, only 5 houses).
- Average SalePrice by Fireplaces: 141,331.48 (0, 690 houses), 211,843.91 (1, 650), 240,588.54 (2, 115) and 252,000 (3, 5 houses).
- EnclosedPorch is the only variable with a slightly negative correlation with SalePrice.

**Common house types**

- The most frequent categories are 1Story for HouseStyle (726), 1Fam for BldgType (1,220), PConc for Foundation (647, with CBlock close behind at 634), Gable for RoofStyle (1,141) and GasA for Heating (1,428).

**Sale year**

- Average SalePrice by YrSold stays in a narrow range: 177,360.84 (2008) to 186,063.15 (2007). Median SalePrice ranges from 155,000 (2010) to 167,000 (2007).
- 2010 has fewer houses (175) than the other years (304 to 338).

## Learning Outcomes

- Excel data cleaning and checking for missing values
- Data-quality analysis (COUNTBLANK, ISBLANK, ISNUMBER, conditional formatting)
- Descriptive statistics with Excel functions and summary tables
- Grouped analysis with AVERAGEIF(S), COUNTIF(S), MEDIAN(FILTER) and a PivotTable
- Correlation analysis and correlation matrices with heatmaps
- Outlier detection with the IQR method, LARGE, SMALL and percentiles
- Visualization with scatter, column, bar, line and box-and-whisker charts
- Interpretation of results and writing observations without claiming causation
- Working across two datasets in one workbook

## Conclusion

This project analyzed house sale prices in two datasets of 1,460 houses each. Practice Work covered dataset structure, missing values, descriptive statistics, grouped summaries, correlation and outliers. The 12 Business Problems covered quality, neighborhood, size, age, garage, features, house types, extreme prices, sale year, data quality and predictor selection. SalePrice differs clearly by quality, neighborhood, size and construction period, and OverallQual and GrLivArea show the strongest correlations with it. The project demonstrates Excel functions, grouped analysis, correlation, outlier detection and charting. BP12 selects OverallQual, GrLivArea, TotalBsmtSF, GarageCars, YearBuilt and Neighborhood as candidate predictors, which could support future predictive modeling of SalePrice.
