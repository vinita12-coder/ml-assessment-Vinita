# Machine Learning Assessment - Part B: Business Case Analysis

## Scenario: Promotion Effectiveness at a Fashion Retail Chain

A fashion retailer has 50 stores in different locations like urban, semi-urban, and rural areas. Every month, they run different types of promotions like Flat Discount, BOGO, Free Gift, etc. The goal is to find which promotion works best for each store to increase the number of items sold.

---

## B1. Problem Formulation

### (a) ML Problem Formulation

Based on my understanding, the main goal is to predict how many items will be sold in a store under a specific promotion.

**Target Variable:**
The target variable is `items_sold`, which shows how many items are sold in a store in a given month.

**Input Features:**
Some important features I would consider are:

* Store details like store size and location type
* Promotion type (Flat Discount, BOGO, etc.)
* Time-related features like month, weekend, festival
* Competition density
* Past sales data

**Problem Type:**
This is a **supervised learning regression problem** because the output is a number (items sold), not categories.

For example, the model needs to predict values like 100, 200, or 500 items. So regression models like Linear Regression or Random Forest can be used.

---

### (b) Why Items Sold is Better than Revenue

Using revenue as a target can be confusing in this case.

For example, if prices change due to discounts, revenue will also change even if customer interest is high. So revenue does not always reflect the real performance of a promotion.

Also, some promotions like BOGO or Free Gifts may increase the number of items sold but not increase revenue directly.

On the other hand, `items_sold` directly shows how customers are responding to a promotion.

So it is a better measure to compare different promotions.

**Important point:**
This shows that in machine learning, we should always choose a target variable that directly matches the business goal.

---

### (c) Alternative to One Global Model

Using one single model for all stores may not give accurate results because all stores are different.

For example, a promotion that works well in an urban store may not work the same way in a rural store.

So instead of one model, I would:

* Group similar stores based on location, size, and past performance
* Train separate models for each group

This will help the model learn better patterns for each type of store.

---

## B2. Data and EDA Strategy

### (a) Joining the Tables

The data comes from multiple tables, so we need to combine them.

* transactions + store attributes using `store_id`
* transactions + promotion details using promotion info
* transactions + calendar using date

After joining, one row will represent:
one store + one month + one promotion

Before training the model, I would:

* Calculate total items_sold per store per month
* Count number of days
* Check average competition density

---

### (b) EDA Plan

Before building the model, I would first explore the data.

1. **Sales by promotion type**
   To see which promotions perform better

2. **Monthly sales trend**
   To check seasonality (like festival sales increase)

3. **Location vs promotion performance**
   To understand which promotion works better in which location

4. **Correlation between features**
   To check relationships between variables

These steps will help in better feature selection and model building.

---

### (c) Handling Promotion Imbalance

Since most data (around 80%) has no promotion, the model may become biased.

It may not learn the effect of promotions properly.

To handle this, I would:

* Give more importance to promotion data
* Create a feature like `has_promotion`
* Try separate modelling for promotion and non-promotion cases

---

## B3. Model Evaluation and Deployment

### (a) Train-Test Split Strategy

Since this is time-based data, I would not use random split.

Instead:

* Use earlier data for training
* Use latest data for testing

This avoids mixing past and future data.

**Metrics I would use:**

* RMSE → for large errors
* MAE → for average error
* R² score → to check model performance

---

### (b) Understanding Model Recommendations

If the model suggests different promotions for the same store in different months, I would try to understand why.

I would:

* Check feature importance
* Use tools like SHAP

For example:

* In festival months, some promotions may work better
* In normal months, discounts may work better

This can be explained to the marketing team in simple terms.

---

### (c) Deployment Process

After training, the model can be saved.

Each month:

* New data will be prepared
* Model will predict sales for each promotion
* Best promotion will be selected

To monitor:

* Compare predicted vs actual sales
* If error increases, retrain the model

Also, in real life, decisions may also depend on budget and other business factors.

---
