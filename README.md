# Did You Forget? — Grocery Recommendation System

A grocery recommendation system that predicts **5 items a customer is likely to have forgotten** from their most recent order.

**Best Kaggle Recall@5: 0.26829**

## Overview

The system uses a customer's historical purchase behavior and the visible items in their latest basket to predict withheld SKUs.

The final solution combines:

* Repeat-purchase and recency features
* Basket-level item associations
* PPMI-SVD item embeddings
* Collaborative filtering
* Category-level behavior
* Global popularity signals
* Five independently trained recommendation models
* Weighted rank-vote ensemble

A key finding was that only **~47% of hidden items were previously purchased** by the customer, so the system also focuses on discovering items the customer has not bought before.

## Results

| Approach         | Kaggle Recall@5 |
| ---------------- | --------------: |
| Single GBM       |     0.245–0.257 |
| 3-model ensemble |           0.264 |
| 5-model ensemble |     **0.26829** |

The final ensemble improved performance primarily through **model diversity** across features, hyperparameters, random seeds, and training samples.

## Evaluation

A leakage-free offline evaluation framework was developed by simulating the competition:

```text
Historical Orders
       ↓
Hold out target order
       ↓
Hide a portion of items
       ↓
Rebuild features without target information
       ↓
Train & predict
       ↓
Calculate Recall@5
```

This made offline evaluation closely match leaderboard performance.

## Dataset

The dataset contains:

* **638 customers**
* **2,595 orders**
* **632 SKUs**
* **28,984 historical purchase records**

Main columns:

```text
Order
SKU
Member
Delivery Date
```

## Running the Project

Install dependencies:

```bash
pip install -r requirements.txt
```

Then open and run:

```text
Grocery_RecSys.ipynb
```

The notebook generates the recommendations and submission file:

```text
Grocery_rec_5_sets.csv
```

## Documentation

For the complete methodology, feature engineering details, experiments, model architecture, and analysis, see the accompanying **project PDF**.

