# From Incremental Lift to Long-Term Customer Value

Short-term campaign measurement (incremental lift over 2–4 weeks, exposed vs. non-exposed households) tells us whether a campaign worked, but not what a customer is worth over time. This project extends that view by modelling **future purchase activity, customer "aliveness" and Customer Lifetime Value (CLV)** with a probabilistic Buy-Till-You-Die model.

## Overview

- **Data:** ~3 years of household-level transactions for Lay's products across large U.S. retailers (1 April 2018 – 21 March 2021).
- **Model:** BG/NBD (Beta-Geometric / Negative Binomial Distribution) via the [`lifetimes`](https://github.com/CamDavidsonPilon/lifetimes) library, suited to non-contractual settings where customer churn is not directly observed.
- **Validation:** 104-week calibration period, 52-week holdout period.
- **Output:** expected purchases over the next 52 weeks, P(alive), an approximate CLV, and K-Means engagement segments.

## Notebook structure

1. Business Context
2. Methodology
3. Data Preparation – exploration, calibration/holdout split, frequency / recency / T metrics
4. Model Performance and Validation – parameter interpretation, customer-level error (MAE ≈ 1.32, RMSE ≈ 1.93 purchases), validation by frequency and recency, CLV estimation
5. Customer Engagement Segmentation – K-Means on log-predicted purchases
6. Moving to Production
7. Conclusions
8. Limitations

## Repository layout

```
.
├── From_Incremental_Lift_to_Long_Term_Customer_Value.ipynb
├── data/
│   └── lays_input_transactions.csv
├── images/
│   ├── transaction_process.jpg
│   └── dropout_process.jpg
├── requirements.txt
└── README.md
```

## Getting started

```bash
git clone https://github.com/gthivaios/From-Incremental-Lift-to-Long-Term-Customer-Value.git
cd From-Incremental-Lift-to-Long-Term-Customer-Value

python -m venv .venv
# Windows: .venv\Scripts\activate   |   macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt

jupyter lab From_Incremental_Lift_to_Long_Term_Customer_Value.ipynb
```

Developed with Python 3.13.

## References

1. Fader, P. S., Hardie, B. G. S., & Lee, K. L. (2005). *"Counting Your Customers" the Easy Way: An Alternative to the Pareto/NBD Model.* Marketing Science. https://www.brucehardie.com/papers/020/fader_et_al_mksc_10.pdf
2. *Predicting Customer Lifetime Value with "Buy 'Til You Die" probabilistic models in Python.* https://medium.com/data-science/predicting-customer-lifetime-value-with-buy-til-you-die-probabilistic-models-in-python-f5cac78758d9
