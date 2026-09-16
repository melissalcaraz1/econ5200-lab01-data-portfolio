# Data Quality Profiling — Big Mac Index

## Objective
A diagnostic analysis of The Economist's Big Mac Index dataset that identifies and corrects a purchasing-power-parity computation error, quantifies survivorship bias introduced by naive missing-data handling, and builds a reusable tool for profiling panel data structure and completeness.

## Methodology
- Diagnosed a sign/denominator error in the PPP valuation formula that inverted the over/undervaluation ranking, and corrected it to compare the implied PPP exchange rate against the actual exchange rate
- Identified a survivorship bias introduced by dropping all countries with any incomplete observation history, rather than using all data available in each period
- Quantified that bias by comparing a complete-panel-only average against an all-available-data average across the full time series
- Distinguished between missing-data mechanisms (MCAR vs. MNAR) present in the panel, rather than treating all gaps as equivalent
- Built `profile_dataframe()`, a function that classifies a dataset's structure (cross-sectional, time series, or panel), reports panel balance, and computes per-column missing-data percentages

## Key Findings
- The corrected PPP formula places Switzerland at the top of the overvalued list, consistent with its structurally high price level, and Taiwan/Indonesia at the undervalued end — the opposite of the uncorrected (buggy) ranking
- Dropping incomplete-panel countries removes 32 of 57 tracked economies, non-randomly: it excludes both discontinued entries (e.g., Russia) and countries with legitimate mid-series gaps, not just recently added ones
- The complete-panel-only average overstates the true global average Big Mac price by roughly $0.08 (about 2.1%), running higher in 33 of 45 periods
- The full panel is unbalanced (57 units × 45 periods, only 25 countries with complete coverage), and several columns carry more than 10% missing data — a structural feature of the dataset that summary statistics must account for rather than discard
- 
