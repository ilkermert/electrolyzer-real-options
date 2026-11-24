# Real Options Investment Thresholds and Capacity-Stage Indicators for European Electrolyzer Manufacturing

Authors: İlker Mert, Hüseyin Yağlı, Bulut Hüner, Coşkun Özalp

This repository contains representative code excerpts and methodological documentation for the research article (in preparation for submission):

"Real Options Investment Thresholds and Capacity-Stage Indicators for European Electrolyzer Manufacturing"

It follows the manuscript's component order: each subsection below states the methodological component as described in the paper, immediately followed by a representative code excerpt implementing it. The excerpts are also available as stand-alone files.



## About the Study

The study combines a McDonald–Siegel real options model of the investment threshold, technology-specific indicators of capacity stages computed from open European Hydrogen Observatory (EHO) data, and company-reported investment figures that give a monetary scale for the threshold. The three analyses are kept separate. Project value is not estimated, so the results do not establish investment decisions or profitability.

| File | Content | Manuscript item |
| --- | --- | --- |
| `threshold_multiple.py` | Threshold multiple V*/I for given σ, r and δ | Tables 2 and 3, Supplementary Table S4 |
| `capacity_indicators.py` | Operational capacity share and capacity-growth duration proxy | Tables 4 and 5 |
| `threshold_project_value.py` | Investment cost and threshold project value | Table 6 |

## 1. Investment Threshold Multiple

The model is the perpetual option to invest of McDonald and Siegel. Project value follows a geometric Brownian motion with volatility σ. The threshold multiple is V*/I = β/(β−1), where β depends on σ, the discount rate r and the opportunity cost of waiting δ. The multiple is theoretical. Project value V is not estimated.

```python
def threshold_multiple(sigma, r=R_DISCOUNT, delta=DELTA_WAITING):
    """Return (V*/I, beta) for the given parameters."""
    x = (r - delta) / sigma ** 2
    beta = 0.5 - x + np.sqrt((x - 0.5) ** 2 + 2 * r / sigma ** 2)
    return beta / (beta - 1), beta
```

Volatility is a scenario input and is not calibrated to data. The low scenario is σL = 16%. The base scenario is σB = 0.20 × √2 = 28.3%, the annualized value of a six-month per-stage figure, under the assumption of independent increments. The six-month value of 20% is used directly only in Supplementary Table S4.

## 2. Operational Capacity Share

The operational share of a technology is the operational capacity divided by the sum of operational and FID-stage capacity, in GW/year, taken from the May 2026 EHO manufacturing capacity data.

```python
p = df.pivot_table(index="Technology", columns="Status",
                   values="Capacity unit (GW)", aggfunc="sum", fill_value=0.0)
p = p.rename(columns={"Operational": "operational", "Under construction/FID": "fid"})
p["share"] = p["operational"] / (p["operational"] + p["fid"])
```

A share of 100% means that no capacity is reported at the FID stage in the snapshot. It is not a completion rate.

## 3. Capacity-Growth Duration Proxy

The proxy W = L/λ divides the capacity at the FID stage, L, by the growth rate of operational capacity, λ, between two dates. It is a provisional indicator and not a project cycle time.

```python
def duration_proxy_months(fid_gw, start_gw, end_gw, years):
    lam = (end_gw - start_gw) / years
    return fid_gw / lam * 12.0
```

## 4. Threshold Project Value

The investment cost for a stated capacity addition is I = c × ΔK, where c is a company-reported investment intensity and ΔK is the capacity addition in GW/year. The threshold project value is V* = multiple × I. It is a monetary reading of the threshold and not an estimate of project value.

```python
def investment_cost(intensity_eur_per_gw_year, delta_k_gw_year=0.5):
    return intensity_eur_per_gw_year * delta_k_gw_year

def threshold_project_value(multiple, investment):
    return multiple * investment
```

## Parameters

| Symbol | Meaning | Value |
| --- | --- | --- |
| r | Discount rate | 8% per year |
| δ | Opportunity cost of waiting | 4% per year |
| σL | Low volatility scenario | 16% |
| σB | Base volatility scenario (annualized) | 28.3% |
| ΔK | Capacity addition | 0.5 GW/year |
| L | Capacity at the FID stage | 8.412 GW/year |
| Start and end capacity | May 2023 and May 2026 | 3.11 and 11.31 GW/year |

## Data Sources

- Manufacturing capacity data are open releases of the European Hydrogen Observatory (reference [47] in the manuscript). The capacity table needs the columns `Technology`, `Status` and `Capacity unit (GW)`.
- Company-reported investment figures are taken from the public announcements and the annual report cited in the manuscript. They are not redistributed here.

## Software Environment

Python 3, NumPy and pandas. Each file runs on its own (`python file.py`) and prints the values reported in the manuscript for its part of the analysis. [Package versions: to be added]

## How to Read the Results

The excerpts reproduce the formulas and the headline values of the manuscript, for example V*/I of 2.53 and 3.41 under the two volatility scenarios and a duration proxy of 36.9 months. They do not reproduce every table and figure. The sensitivity tables, the figures and the technology-specific tables depend on parts of the analysis that are not included.

Note on scope: These are representative excerpts of the core calculations, included for transparency and to show how each step was done. The complete analysis script, the data pre-processing steps and the figure-generation code are not included, see "Contact and Data Availability" below. This repository does not allow the tables and figures of the paper to be reproduced, and the paper does not claim that it does.

## Citation

If you use this code or methodology in your research, please cite:

[Citation: authors, year, title, journal, to be added after publication]

## License

This code is made available under the MIT License.

## Contact and Data Availability

The EHO data are open and are cited in the manuscript. The complete analysis script and the data pre-processing steps are not publicly available because they form part of ongoing research.

Repository maintained by: [name and e-mail, to be added]

This README accompanies representative code excerpts for the article referenced above. Last updated: November 2026
