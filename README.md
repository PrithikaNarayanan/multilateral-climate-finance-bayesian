# Climate Justice or Climate Rhetoric?

**Does international multilateral climate finance reach the most vulnerable countries?**

A Bayesian analysis of USD 761.9 billion in multilateral climate finance disbursed to 152 countries between 2000 and 2023, testing whether allocation follows the principle that countries facing the greatest climate risks should receive the most support.

LSE MSc Statistics · ST451 Bayesian Machine Learning · 2026

---

## Headline finding

More vulnerable countries receive *less* per-capita climate finance, not more. The vulnerability coefficient is negative under every robustness check applied: both informative and sceptical priors (P(β < 0) ≥ 98.5%), all four income groups in the hierarchical model, leave-one-out cross-validation, and Student-t likelihood. Nine countries housing 2.01 billion of the world's most climate-exposed people receive USD 1.32 per person per year — against a vulnerability-proportional benchmark of USD 5.12.

The per-capita framing is what changes the conclusion. India receives USD 42.9bn in absolute terms (the dataset's largest recipient) but only USD 31 per person (among the worst-served). Prior studies reporting positive vulnerability–finance relationships use absolute flows; this study shows the relationship inverts when the outcome is measured per person.

## Methods

- **Gaussian Mixture Model clustering** (K = 4, selected on substantive grounds over BIC-optimal K = 2) identifies four country typologies on the vulnerability × finance plane. The C3 cluster (India, China, Brazil, Indonesia) demonstrates that vulnerability does not mechanically block access — institutional capacity to develop bankable projects does.
- **Bayesian linear regression** with PyMC (NUTS, 4 chains × 2,000 draws) under informative and sceptical priors, with PSIS-LOO-CV, WAIC, and Pareto-k diagnostics.
- **Hierarchical Bayesian model** with partial pooling across income groups, addressing the systematic within-group residual bias of the pooled fit.
- **Robustness extensions**: Student-t likelihood (learns ν from the data; ν ≈ 1.1 indicates near-Cauchy tails absorbing zero-inflation rather than genuine heavy noise), and a Frisch–Waugh–Lovell decomposition isolating readiness-specific from shared variance.

## Key result on mechanism

ND-GAIN vulnerability and institutional readiness correlate at ρ = −0.887 in this dataset. Adding raw readiness shrinks vulnerability coefficients by 46.5% on average; under orthogonalised readiness, coefficients move *away* from zero by 42.3%. Roughly 89% of the apparent shrinkage reflects shared variance. The honest reading is not that institutional capacity is or is not the mechanism — vulnerability and institutional weakness are empirically inseparable in cross-sectional multilateral flows, and the disbursement architecture treats them as a single condition.

## Policy quantification

Under the Gaussian-likelihood counterfactual, redistributing the COP29 USD 300bn pledge in proportion to modelled vulnerability would route USD 101.7bn/year to the nine gap countries versus USD 26.2bn under current architecture — a USD 75.5bn structural gap. Under the Student-t bound, the gap shrinks to roughly USD 50bn. The direction is robust; the magnitude is best read as the bracket [USD 50bn, USD 75bn].

## Data

| Source | Coverage | Use |
|---|---|---|
| International Multilateral Public Climate Finance Dataset (Fan et al., 2025, Figshare) | 185 countries, 2000–2023 | Project-level finance flows, instrument type |
| ND-GAIN Country Index (Notre Dame) | 192 countries, 2010–2023 avg | Vulnerability sub-dimensions, readiness |
| World Bank WDI | 266 country codes | GDP per capita, population, GNI per capita |

Final merged panel: 152 countries, USD 761.9 billion total finance.

## Repository contents

```
├── ST451_63046_Report.pdf       Final 10-page article
├── ST451_63046_executed_file.ipynb   Full notebook with executed outputs
```
Global seed = 42 throughout. PyMC 5.27, ArviZ 0.23.

## References

Fan, S., Wang, C., Zhong, H., Dong, X., & An, K. (2025). *International Public Multilateral Climate Finance Dataset from 2000 to 2023*. Figshare. https://doi.org/10.6084/m9.figshare.28171535

Lee, N., Matthews, S., & Reid, J. (2025). Does World Bank Climate Adaptation Finance Go to the Most Vulnerable Countries? *Center for Global Development*.

Notre Dame Global Adaptation Initiative (2026). *ND-GAIN Country Index*. https://gain.nd.edu

Tennant, E., Gilmore, E., Schroeder, H., & Waitz, I. A. (2024). Impact of climate vulnerability on the allocation of climate finance: global evidence. *Science of the Total Environment*, 920, 171004.

Vehtari, A., Gelman, A., & Gabry, J. (2017). Practical Bayesian model evaluation using leave-one-out cross-validation and WAIC. *Statistics and Computing*, 27(5), 1413–1432.

Weiler, F., Klöck, C., & Dornan, M. (2018). Vulnerability, good governance, or donor interests? The allocation of aid for climate change adaptation. *World Development*, 104, 65–77.
