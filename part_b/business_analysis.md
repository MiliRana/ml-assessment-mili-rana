# Business Case Analysis

## B1. Problem Formulation

### (a)
The target variable is **items_sold**, which tells us how many products were sold in a store during a given time period.

The input features can include store details (like store size and location type), promotion type, competition density, and time-related factors such as month, weekends, and festivals.

This is a **supervised learning regression problem** because we are predicting a continuous numeric value (items sold) using past data.

---

### (b)
Using items_sold is better than revenue because revenue can change due to pricing, discounts, or expensive products. This may not clearly show how effective a promotion is.

Items_sold directly reflects how customers respond to promotions, so it is a more reliable measure.

This shows an important principle in machine learning: the **target variable should match the actual business goal**.

---

### (c)
Using one single global model for all stores may not work well because stores in different locations behave differently.

A better approach is to use **segmented models**, for example separate models for urban, semi-urban, and rural stores.

This allows the model to capture differences in customer behavior and improve prediction accuracy.

---

## B2. Data and EDA Strategy

### (a)
The four tables (transactions, store attributes, promotions, and calendar) can be joined using common fields like **store_id** and **date**.

The final dataset should have one row per **store per day (or time period)**.

Before modelling, we can aggregate data such as total items sold, number of transactions, and average basket size for each store and time period.

---

### (b)
The following EDA steps would be useful:

- **Distribution of items_sold** to understand how sales are spread and check for skewness  
- **Correlation analysis** to see which features are related to sales  
- **Sales by promotion type** to compare effectiveness of different promotions  
- **Time-based trends** (monthly or seasonal) to identify patterns like festival spikes  

These insights help in better feature engineering and model selection.

---

### (c)
Since 80% of transactions have no promotion, the data is imbalanced.

This can make the model biased towards predicting lower sales or ignoring the effect of promotions.

To handle this:
- Create a feature indicating whether a promotion is applied  
- Use proper evaluation metrics  
- Consider balancing techniques if needed  

---

## B3. Model Evaluation and Deployment

### (a)
A **time-based train-test split** should be used, where older data is used for training and newer data is used for testing.

A random split is not suitable here because it mixes past and future data, which can cause **data leakage**.

Evaluation metrics:
- **RMSE (Root Mean Squared Error)**: gives higher penalty to large errors  
- **MAE (Mean Absolute Error)**: shows the average error in predictions  

These metrics help us understand how close the predictions are to actual sales.

---

### (b)
Feature importance helps us understand which factors are influencing the model’s decisions.

For example, in December, factors like festivals and holidays may increase demand, so Loyalty Points Bonus works better. In March, demand may be lower, so discounts may perform better.

This explains why the model gives different recommendations for the same store in different months.

---

### (c)
The trained model can be saved using tools like joblib or pickle.

Each month:
- New data is collected  
- It is passed through the same preprocessing pipeline  
- The model predicts the expected sales or best promotion  

For monitoring:
- Track errors over time  
- Check if model performance is decreasing  
- Retrain the model when needed  

This ensures the model stays accurate and useful.
