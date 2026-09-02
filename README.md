# What Determines Health Insurance Premiums?

### An explainable machine-learning analysis of the 2026 CMS Marketplace

Health insurance premiums can feel difficult to understand. This project examines whether Marketplace premiums are mainly determined by visible plan characteristics or whether insurer pricing behaves like a black box.

The analysis combines the 2026 CMS Rate Public Use File and Plan Attributes Public Use File. It uses exploratory analysis, hypothesis testing and predictive modelling to measure the influence of age, tobacco use, location, metal level, plan type, deductibles, out-of-pocket limits and insurer identity.

## Main finding

Marketplace premiums are **mostly explainable, but not completely transparent**.

- A nonlinear model using public plan characteristics explained **83.3%** of premium variation.
- Adding insurer identity increased the explained variation to **90.2%**.
- The best model had a median absolute percentage error of **4.1%**.
- It predicted **79.5%** of premiums within 10% of their recorded values.

The improvement after adding insurer identity shows that the company offering the plan contains pricing information that is not fully captured by the other public characteristics. However, the strong performance of the public-factor model means that pricing does not behave like a complete black box.

## Analysis highlights

The final modelling dataset contains:

- **24,146** premium observations
- **4,013** health plans
- **30** states
- **180** state–issuer combinations
- **349** rating areas

### Premium differences by metal level

Metal level describes how healthcare costs are shared between the insurer and the customer. More generous plans generally charge higher premiums.

| Metal level | Median monthly premium |
|---|---:|
| Catastrophic | $431 |
| Bronze | $539 |
| Expanded Bronze | $558 |
| Silver | $727 |
| Gold | $763 |
| Platinum | $1,455 |

The steady rise from Bronze to Platinum shows that benefit generosity is an important premium driver. Metal level is not a measure of healthcare quality; it mainly represents how costs are divided.

### Other important findings

- Premiums increased strongly with age. The premium for an adult aged 64 or older was about **3 times** the premium for a 21-year-old.
- Tobacco-rated premiums were typically **15% higher** than non-tobacco premiums.
- Median state premiums ranged from approximately **$450 in New Hampshire** to **$1,050 in Wyoming**.
- Plans with higher deductibles and out-of-pocket limits generally had lower premiums.
- PPO plans had higher median premiums than HMO and EPO plans.
- Geography, insurer, plan type, metal level and HSA eligibility were among the strongest predictive features.

## Hypotheses tested

The analysis tested whether premiums differ meaningfully across major pricing factors.

| Hypothesis | Method | Result |
|---|---|---|
| Premiums are equal across metal levels | Kruskal–Wallis test | Rejected |
| Premiums are equal across plan types | Kruskal–Wallis test | Rejected |
| Premiums are equal across states | Kruskal–Wallis test | Rejected |
| Deductible and premium are unrelated | Spearman correlation | Rejected |

All four tests remained statistically significant after adjustment for multiple testing. Metal level and deductible had the strongest effects among these tests.

## Models compared

| Model | Features | R² on log premium | Median percentage error |
|---|---|---:|---:|
| Linear | Public factors | 77.9% | 9.0% |
| Linear | Public factors and issuer | 87.5% | 6.8% |
| Nonlinear | Public factors | 83.3% | 5.8% |
| Nonlinear | Public factors and issuer | **90.2%** | **4.1%** |

The nonlinear models performed better because premium relationships are not entirely straight lines. The comparison with and without issuer identity provides a practical way to estimate how much of pricing is explained by visible plan information.

## View the complete analysis

Open [`insurance-analysis-publish-ready.ipynb`](insurance-analysis-publish-ready.ipynb) to see the complete workflow, statistical results and chart outputs.

The notebook covers:

- data validation and preparation;
- premium distributions and outliers;
- state, issuer, plan type and metal-level comparisons;
- age, tobacco and geographic pricing;
- hypothesis testing and effect sizes;
- correlation and interaction analysis;
- linear and nonlinear predictive models;
- permutation importance;
- prediction errors and residual analysis; and
- an evidence-based assessment of pricing transparency.

## Data source

The project uses official public-use data from the U.S. Centers for Medicare & Medicaid Services:

[CMS Marketplace Public Use Files](https://www.cms.gov/marketplace/resources/data/public-use-files)

Required 2026 files:

- Rate Public Use File
- Plan Attributes Public Use File

The source files are not stored in this repository because they are large and are maintained by CMS.

## Tools

- Python
- pandas and NumPy
- Matplotlib and Seaborn
- SciPy and statsmodels
- scikit-learn
- Jupyter Notebook / Kaggle



## Conclusion

Premium differences largely follow visible and understandable factors: age, tobacco rating, geography, benefit generosity, plan design and cost sharing. Insurer identity adds substantial predictive information, which indicates that some pricing behaviour remains company-specific. The evidence therefore supports a balanced conclusion: Marketplace premium pricing is **mostly explainable, but not a completely open system**.

## Author

**Abiodun Alabi**  
Data Analyst and Data Scientist
