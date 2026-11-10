# Decision log

Each entry: what I decided, the alternative, and why.

## 2026-11-10 · Day 1

- **Dropped `Unnamed: 0`.** It is an old row index saved into the CSV and carries no information.
- **Dropped `Period`.** It packs year and month into one float (1948.01 to 2013.12), duplicating `YEAR` and `Month`. As a float, October (x.10) and January (x.1) are easy to confuse.
- **Treated zeros in `ALT`, `X_COR` and `Y_COR` as missing.** They occur only for Chittagong (City-Ambagan), Chuadanga and Syedpur, where 0 is impossible (Syedpur is at latitude 25.75). These stations' coordinates also use a different precision, suggesting a different source. `ALT` zeros → NaN; `X_COR`/`Y_COR` dropped because `LATITUDE`/`LONGITUDE` carry the location.
- **Coverage is uneven: 10 of 35 stations cover all 66 years (792 months).** H2 (decade warming) uses only these 10, so new stations cannot fake or hide a trend. H3 (coastal vs inland) compares overlapping years only, because many coastal stations start late.
- **Identified how missing values were filled.** A missing value was replaced with the station's mean for that month over the years that have data. Evidence:
  - Fill values repeat exactly across years for the same station, month and variable, with long decimals (e.g. Barisal January wind speed 0.453704).
  - The number of real years is recoverable from the decimals (Chuadanga February rainfall 15.444444 × 9 = 139, so 9 real years).
  - Chittagong (City-Ambagan) `Bright Sunshine` is the dataset-wide mean (6.411131) in all 48 rows.
  - Unique long decimals in `Relative Humidity` at some stations may come from a related averaging step; to be checked on Day 2.
- **Chittagong (City-Ambagan) is mostly synthetic.** 2010 is absent; 2009 temperature, rainfall, humidity and wind equal the mean of 2011–2013 (verified, e.g. January max temp (32.4 + 30.7 + 31.6) / 3 = 31.567), so 2009 was rebuilt from future years. Only 2009 cloud cover looks measured.
- **Chuadanga is largely synthetic for some variables.** Rainfall, humidity and sunshine are real for only 9 of 25 years; cloud cover for 13; temperature and wind for 23. 2009–2010 are imputed for every variable, as at City-Ambagan, which suggests a dataset-wide gap in those years.
- **Excluded City-Ambagan, Chuadanga and Syedpur from all hypothesis tests (provisional).** Alternative: keep them and flag. They have missing metadata, short late coverage and heavy imputation, so including them would bias yearly averages. They stay in the raw data; the evidence is in the notebook.

## Planned for Day 2

- **Replace exclusion with masking.** For each (station, variable, month), a value that appears in two or more years with more than one decimal is treated as a fill value and converted to NaN. Hypotheses H1–H4 are then tested on real measurements only, and the README reports the percentage of imputed values per variable. If this works, the three-station exclusion above may become unnecessary; update this log either way.