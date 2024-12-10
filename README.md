## Final Report: Predicting Drug Usage Based on Personality Traits and Demographics

### Project Overview
This project aimed to predict the likelihood of frequent drug usage based on demographic information and personality traits using the **Drug Consumption (Quantified)** dataset from the UCI Machine Learning Repository. By leveraging classification models, I sought to explore patterns in drug use behaviors and assess the performance of machine learning algorithms in handling imbalanced datasets.

### Objectives
1. Understand and preprocess the dataset to create a suitable input for machine learning models.
2. Use logistic regression, random forests, and gradient boosting models to predict drug use patterns.
3. Address challenges of class imbalance to improve model performance.

---

### Methodology

#### Data Preparation
- **Dataset Cleaning:** I removed fictitious and unnecessary variables, such as the fabricated "Semer" drug column and participant identifiers, to ensure data integrity.
- **Class Encoding:** Drug usage levels were encoded into binary labels, where usage in the last month was defined as frequent (positive case).
- **Exploratory Analysis:** The dataset consisted of 1,877 participants, primarily from the UK and USA, with most aged 18–34. The dataset was free of missing values and showed normally distributed personality traits.
- **Class Imbalance:** Some drugs (e.g., alcohol, caffeine) had high positive representation, while others (e.g., heroin, crack) were heavily imbalanced.

#### Modeling and Evaluation
1. **Initial Models:**
   - Logistic Regression and Random Forest models achieved high accuracy for widely used drugs but struggled with imbalanced classes. F1-scores for most drugs were low, highlighting a failure to capture minority class patterns.

2. **Gradient Boosting (XGBoost):**
   - The use of XGBoost improved overall performance, with higher F1-scores for some drugs. However, issues with class imbalance persisted, limiting the model's ability to generalize for rare drug users.

3. **Balanced XGBoost (Scale_pos_weight):**
   - To address imbalance, I implemented dynamic class weighting. This significantly improved F1-scores, particularly for less common drugs. However, performance on widely used substances like alcohol and nicotine slightly declined due to overlapping usage patterns across classes.

---

### Results and Key Insights
- **Overall Performance:**
  - The final balanced XGBoost model achieved an average accuracy of **0.88** and an F1-score of **0.87** across all drugs.
  - **88.24%** of drugs were classified as "well-predicted" based on an F1-score threshold of 0.75.

- **Class Imbalance:**
  - Drugs with high positive representation (e.g., alcohol, caffeine) exhibited high accuracy and F1-scores.
  - For imbalanced classes (e.g., heroin, crack), dynamic class weighting drastically improved performance.

- **Notable Challenges:**
  - Overlap in user profiles for widely used substances made it difficult to distinguish frequent from occasional users.
  - Rare drug usage data remained challenging, emphasizing the need for advanced techniques or additional data.

---

### Challenges Faced

1. **Initial Definition of Target Variable:**
   - At the start of the project, I defined the target variable as users who had used each drug within the last decade. This broad criterion led to poor model performance, even when employing different algorithms and balancing techniques. The low predictive accuracy and F1-scores suggested that the models struggled to find meaningful patterns in such a generalized target.
   - To address this, I narrowed the focus to users who had used the drugs within the last month, targeting frequent usage instead. While this refinement drastically improved the results on the balanced dataset, it significantly worsened the performance on the unbalanced set due to the smaller pool of positive examples. This trade-off highlighted the importance of carefully defining the prediction goal to align with project objectives.

2. **Data Integrity Issues:**
   - Initially, I had not removed participants flagged as over-claimers using the "Semer" column. Retaining this data compromised the integrity of the dataset, as these users introduced noise by falsely reporting drug usage patterns. Additionally, I included the "Chocolate" column, which was irrelevant to the objective and added unnecessary features that could distract the models.
   - Removing these columns and participants improved the dataset's quality, streamlined the features, and allowed the models to focus on the most relevant variables.

These challenges underscored the importance of thoughtful preprocessing and clear objective setting in machine learning projects. Refining the dataset and redefining the target variable were critical steps in overcoming initial performance limitations and achieving meaningful predictions.

---

### Conclusion
This project demonstrated the potential of machine learning to predict drug usage based on demographic and psychological traits. The implementation of balanced XGBoost showed that addressing class imbalance is critical for improving model performance in skewed datasets.

While the results are promising, further research could explore ensemble methods or synthetic data augmentation to refine predictions for minority classes. Overall, the project highlights the value of thoughtful preprocessing and model tuning in achieving robust predictive analytics.
