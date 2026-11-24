# Real Options Investment Thresholds and Capacity-Stage Indicators for European Electrolyzer Manufacturing

Authors: İlker Mert, Hüseyin Yağlı, Bulut Hüner, Coşkun Özalp

This repository documents the inputs, parameter assumptions, data sources, and calculation steps of the research article (in preparation for submission):

"Real Options Investment Thresholds and Capacity-Stage Indicators for European Electrolyzer Manufacturing"


## About the Study

The study combines a McDonald–Siegel real options model of the investment threshold, technology-specific indicators of capacity stages computed from open European Hydrogen Observatory (EHO) data, and company-reported investment figures that give a monetary scale for the threshold. The three analyses are kept separate. Project value is not estimated, so the results do not establish investment decisions or profitability. Numbered references in brackets, such as [12], are the reference numbers of the manuscript. They are listed at the end of this file.

## 1. Investment Threshold Multiple

The model is the perpetual option to invest of McDonald and Siegel [3]. Project value follows a geometric Brownian motion with volatility σ. The threshold multiple is

V*/I = β / (β − 1),

where β is the positive root of the fundamental quadratic equation,

β = 1/2 − (r − δ)/σ² + sqrt( ((r − δ)/σ² − 1/2)² + 2r/σ² ).

Here r is the discount rate, δ is the opportunity cost of waiting, I is the irreversible investment cost, and V* is the critical project value. The rates are continuously compounded and are expressed per year. The multiple is theoretical and is the same for all technologies. Project value V is not estimated. Multiples are computed from unrounded inputs.

## 2. Operational Capacity Share

For each technology i, the operational share is

RR_i = Operational_i / (Operational_i + FID_i),

where both terms are capacity in GW/year from the May 2026 EHO manufacturing capacity data [47]. FID_i is the capacity classified as "Under construction/FID". A share of 100% means that no capacity is reported at the FID stage in the snapshot. It is not a completion rate.

## 3. Capacity-Growth Duration Proxy

The proxy is

λ = (K_end − K_start) / (t_end − t_start),  W = L / λ,

where K_end and K_start are the system-wide operational capacities (GW/year) at the end and start of the period, L is the total FID-stage capacity of the four technologies (GW/year), and W is converted to months by multiplying by twelve. It is a provisional indicator and not a project cycle time.

## 4. Threshold Project Value

The investment cost for a stated capacity addition is I = c × ΔK, where c is a company-reported investment intensity (EUR million per GW/year) and ΔK is the capacity addition (GW/year). The threshold project value is V* = (V*/I) × I. It is a monetary reading of the threshold and not an estimate of project value.

## Parameters and Their Sources

Parameters that do not come from the EHO release are scenario assumptions. They are not estimated from data.

| Parameter | Value | Origin and use |
| --- | --- | --- |
| r, discount rate | 8% per year | Follows Biggins et al. [12], who use the same annual rate for a wind-powered PEM electrolyzer project, citing an IRENA report and UK renewable hurdle rates. It is a hydrogen production value applied to manufacturing as an assumption. Cross-check: a median country-level discount rate of 8.2% for 2024 based on Damodaran's financial-market data is reported in [48]. Trivella [13] is not a source for the level of r. Sensitivity: 6% and 10%. |
| δ, opportunity cost of waiting | 4% per year | Illustrative value from McDonald and Siegel [3]. It is required for a finite threshold to exist. Sensitivity: 2% and 6%. |
| σL, low volatility scenario | 16% | Rounded low end of the median implied-volatility range of 16.42% to 47.10% that González-Muñoz et al. [49] report for renewable energy firms. Treated as an annual value. Not specific to electrolyzer manufacturing. |
| σB, base volatility scenario | 28.3% (0.20 × √2) | Trivella [13] assigns a volatility of 0.20 per six-month stage to hydrogen price, electricity price, electrolyzer cost, and storage cost. For independent increments the annual value is 0.20 × √2 = 0.2828. The source set these values from limited data, practitioner reports, and visual inspection of sample paths, and did not calibrate them statistically. |
| σ, six-month alternative | 20% | Trivella [13] value used directly without annualizing, reported only in Supplementary Table S4. |
| Volatility curve | 16% to 30% | Range of the continuous curve in the sensitivity analysis. |
| ΔK, capacity addition | 0.5 GW/year | Reference case chosen for illustration. |
| Sensitivity design | One at a time | σ, r, δ, and λ are varied one at a time, with λ at 0.8, 1.0, and 1.2 times its base value, as in local sensitivity analysis [52]. The ranges are assumptions and not confidence intervals. |

### Reported threshold multiples

| Case | V*/I |
| --- | --- |
| σL = 16% (r = 8%, δ = 4%) | 2.53 |
| σB = 28.3% (r = 8%, δ = 4%) | 3.41 |
| σB, r = 6% and 10% | 3.00 and 3.85 |
| σB, δ = 2% and 6% | 6.37 and 2.46 |
| σ = 20% (six-month value), r = 6%, 8%, 10% | 2.37, 2.78, 3.22 |

## Capacity Data (EHO)

| Item | Value | Source |
| --- | --- | --- |
| Dataset | Electrolyser manufacturing capacity, May 2026 release (data as of May 2026, dataset updated 27 July 2026) | European Hydrogen Observatory [47] |
| Coverage and unit | EU27, EFTA, and United Kingdom based facilities. The web page reports GW/year. The workbook column is labeled "Capacity unit (GW)" and is read as GW/year. | [47] |
| Stages | Operational and "Under construction/FID" | [47] |
| Totals | Operational 11.313 GW/year, FID stage 8.412 GW/year | Computed from [47] |
| Operational shares | AEM 3.85%, PEM 47.3%, alkaline 69.0%, SOEC 100% (no FID-stage SOEC capacity) | Computed from [47] |
| Start value for the duration proxy | 3.11 GW/year, May 2023, EU27 plus Iceland, Liechtenstein, Norway, and Switzerland, so the United Kingdom is excluded | EHO Report 01, November 2023, p. 71 [57] |
| End value | 11.31 GW/year, May 2026 | [47] |
| Resulting proxy | λ = 2.733 GW/year², W = 36.9 months (30.8 to 46.2 months at λ × 1.2 and × 0.8) | Computed |
| Start-value scenarios | 4.11 GW/year (adds 1.0 GW/year nameplate of ITM Power's Bessemer Park factory [62], 42.1 months). 3.9 GW/year, October 2023, including the United Kingdom [61], 35.2 months over 2.58 years and 40.9 months over three years. | [62], [61] |

Limits of the data: The workbook has no country field, so United Kingdom capacity cannot be separated. The year field of FID-stage rows (2026 or 2027) is not defined by the EHO as a commissioning year. The start and end values differ in coverage, which biases the proxy downward by an amount that cannot be determined. Nameplate capacity at Bessemer Park may differ from available capacity, which ITM Power reported as approximately 700 MW [58].

The EHO manufacturing capacity file and the two other EHO datasets used for supplementary tables (electrolyzer cost, 2025 release, and hydrogen production costs, 2022 to 2024 releases) are open and are available from the EHO website [47]. They are not redistributed here.

## Company-Reported Investment Figures

These figures come from public announcements and an annual report. They are not redistributed here. Each intensity comes from one observation with its own scope and date, and the intensities are not compared as a ranking of technologies.

| Technology | Source plant | Reported figure | Capacity | Intensity (EUR million per GW/year) | Source |
| --- | --- | --- | --- | --- | --- |
| Alkaline | Nel ASA, Herøya, Norway | About NOK 300 million before grants, expected 2026 and 2027, at an existing site | Up to 1 GW/year | 25.3 | [53] |
| PEM | ITM Power, planned second factory, Sheffield, United Kingdom | GBP 50 to 55 million overall (land GBP 13.4 million, shell up to GBP 16 million, fit-out and power GBP 20 to 25 million, which sum approximately to the total, so land is not added again) | 1.5 GW/year | 39.0 to 42.9 | [54] |
| SOEC | Topsoe, Herning, Denmark | Approximately DKK 2.2 billion total construction-related project expenditure for the whole project. The 2022 announcement stated over DKK 2 billion. | 500 MW/year | 589.2 (536 if DKK 2 billion is used) | [56], [55] |
| AEM | None found | Not calculated | | | |

Later events that qualify the PEM and SOEC observations: ITM Power reported in its 2022 final results that it had reviewed its plan for a second UK factory given the business climate and cost escalation, and would expand capacity at Bessemer Park instead [58]. Topsoe announced on 18 May 2026 that it will hibernate the Herning factory after proving commercial-scale manufacturing capability, until demand is robust [59]. The SOEC capacity of 500 MW/year is taken from the Topsoe investment announcement [55], and the assumption that the annual report figure refers to the same plant is stated in the manuscript.

### Currency conversion

Amounts are converted at European Central Bank (ECB) euro reference rates.

| Currency | EUR per unit | Date |
| --- | --- | --- |
| GBP | 1.1712 (0.8538 GBP per EUR) | 9 November 2021 |
| NOK | 0.0843 (11.8560 NOK per EUR) | 12 December 2025, the date of the Nel announcement |
| DKK | 0.1339 (7.4689 DKK per EUR) | 31 December 2025, end of the Topsoe reporting year |

### Threshold project values (reference case, ΔK = 0.5 GW/year)

| Technology | I (EUR million) | V* at σL (EUR million) | V* at σB (EUR million) |
| --- | --- | --- | --- |
| Alkaline | 12.6 | 32.0 | 43.2 |
| PEM | 19.5 to 21.5 | 49.4 to 54.3 | 66.6 to 73.3 |
| SOEC | 294.6 | 745.1 | 1,005.8 |
| AEM | Not calculated | Not calculated | Not calculated |

These are thresholds that project value would have to reach for a stated capacity addition under the model. They are not company costs and not estimates of project value.

## Other Background Data and Sources

| Item | Source |
| --- | --- |
| Policy benchmark: at least 40 GW of renewable hydrogen electrolyzers by 2030 and 17.5 GW/year manufacturing capacity | European Commission [1] |
| Projects at final investment decision by mid-2023 | H2 Tech, 13 July 2023 [2] |
| Share of announced electrolyzer manufacturing projects at the committed stage (fewer than 15%) | IEA [60] |
| Supply-demand transition after 2027 in a selected scenario, used as a temporal reference only | Gonçalves et al. [38] |

## Literature Search Record (Web of Science)

A search of the Web of Science Core Collection was run on 24 November 2026 with no restriction by index. The search type was Advanced Search with the topic field (TS: title, abstract, and keywords), and no restriction on year, language, or document type. The authors read the titles and abstracts of the retrieved records. The records themselves are not redistributed. The search does not replace a systematic review and covers one database only.

| Query | Search string | Records |
| --- | --- | --- |
| 1 | TS=(("real option*" OR "option value" OR "investment threshold*" OR "investment timing" OR "optimal timing" OR "irreversible investment") AND (electrolyzer* OR electrolyser* OR "water electrolysis" OR electrolysis) AND (manufactur* OR "supply chain" OR "production capacity" OR gigafactor* OR factory OR factories)) | 0 |
| 2 | TS=(("real option*" OR "investment threshold*" OR "option value") AND (hydrogen OR "power-to-hydrogen" OR "power-to-gas" OR "power to gas")) | 66 |
| 3 | TS=((electrolyzer* OR electrolyser*) AND (manufactur* OR "production capacity") AND (announced OR operational OR "final investment decision" OR FID OR pipeline OR "capacity expansion") AND (Europe* OR "European Union" OR EU27)) | 7 |

No retrieved record computes an investment threshold or option value for electrolyzer manufacturing. The full record is in Supplementary Table S5 of the manuscript.

## References

[1] European Commission (2020). A hydrogen strategy for a climate-neutral Europe. COM(2020) 301 final, Brussels, 8 July 2020.
[2] H2 Tech (2023). EU electrolyser sector juggles supply and demand. Hydrogen Economist, 13 July 2023.
[3] McDonald, R., Siegel, D. (1986). The value of waiting to invest. Quarterly Journal of Economics, 101(4), 707-727.
[12] Biggins, F., Kataria, M., Roberts, D., Brown, S. (2022). Green hydrogen investments: Investigating the option to wait. Energy, 241, 122842.
[13] Trivella, A. (2025). Optimizing electrolyzer investments for green hydrogen production under market and technology uncertainties. Renewable Energy, 249, 123081. https://doi.org/10.1016/j.renene.2025.123081
[38] Gonçalves, R., Rytter, N.G.M., Nugroho, Y., van Erp, T. (2026). Too soon, too late: An analysis of electrolyser supply and demand dynamics in Europe. International Journal of Hydrogen Energy, 238, 155142. https://doi.org/10.1016/j.ijhydene.2026.155142
[47] European Hydrogen Observatory (2025-2026). Datasets: electrolyser manufacturing capacity (May 2026 release), electrolyser cost (2025 release), hydrogen production costs (2022-2024 releases). https://observatory.clean-hydrogen.europa.eu
[48] Stargardt, M., Hugenberg, J., Winkler, C., Heinrichs, H., Linßen, J., Stolten, D. (2025). The Striking Impact of Natural Hazard Risk on Global Green Hydrogen Cost. arXiv:2503.16009.
[49] González-Muñoz, R.-I., Molina-Muñoz, J., Mora-Valencia, A., Perote, J. (2024). Real Options Volatility Surface for Valuing Renewable Energy Projects. Energies, 17(5), 1225. https://doi.org/10.3390/en17051225
[52] Saltelli, A., Ratto, M., Andres, T., Campolongo, F., Cariboni, J., Gatelli, D., Saisana, M., Tarantola, S. (2008). Global Sensitivity Analysis: The Primer. Wiley.
[53] Nel ASA (2025). Final investment decision to industrialize the next-generation pressurized alkaline platform. Press release, 12 December 2025.
[54] ITM Power plc (2021). Intention to purchase site in Sheffield for the second UK giga factory. Announcement, 9 November 2021.
[55] Topsoe (2022). Topsoe confirms final investment decision. Press release, 1 September 2022 (investment decision of 24 August 2022).
[56] Topsoe A/S (2026). Annual Report 2025. Sustainability statement, E1-3, p. 73.
[57] European Hydrogen Observatory (2023). Report 01, November 2023: The European hydrogen market landscape, p. 71.
[58] ITM Power plc (2022). Final results for the year ended 30 April 2022. Announcement, 14 September 2022.
[59] Topsoe A/S (2026). Topsoe adjusts SOEC commercialization pathway to match market outlook. Company announcement No. 09/2026, 18 May 2026.
[60] IEA (2023). The State of Clean Technology Manufacturing: An Energy Technology Perspectives Special Briefing, November 2023 Update.
[61] Hydrogen Europe (2023). Clean Hydrogen Monitor 2023, Chapter 5, pp. 73-79.
[62] ITM Power plc (2021). Launch of UK Hydrogen Strategy at official opening of Bessemer Park Gigafactory. Announcement, 17 August 2021.

## Citation

If you use the parameter documentation of this repository, please cite:

[Citation: authors, year, title, journal, to be added after publication]

## License

This documentation is made available under the MIT License.

## Contact and Data Availability

The EHO data are open and are cited in the manuscript. Company figures come from the cited public announcements and annual report. Web of Science records are not shared because of license terms. The analysis scripts and the data pre-processing steps are not publicly available because they form part of ongoing research.

Repository maintained by: [name and e-mail, to be added]

Last updated: November 2026

Note on scope: This repository contains documentation only. It contains no code and no data files. The analysis scripts and the data pre-processing steps are not shared, and the Web of Science records are not redistributed because of database license terms. The README states the formulas, every parameter value with its source, and the data used, so that each value can be traced to its origin. It does not allow the tables and figures of the paper to be reproduced, and the paper does not claim that it does.
