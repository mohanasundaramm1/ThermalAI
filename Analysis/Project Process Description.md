
In this project, we developed and evaluated multiple machine learning models to address alarm chattering and flooding in a thermal power plant. The goal was to improve alarm management by focusing on critical systems, prioritizing high-frequency chattering alarms, and simplifying categorical variables for better model performance. Below is a detailed breakdown of the three models developed:

---

### **Model 1: Focus on Boiler Systems (Evaporator 1, 2, 3, 4)**

#### **Approach**
The client identified the boiler systems (Evaporator 1, 2, 3, 4) as the most critical systems in the plant. We focused on analyzing alarms specific to these systems to improve prediction accuracy and reduce false negatives.

#### **Method**
1. **Data Preparation**:
   - Filtered records related to Evaporator 1, 2, 3, 4 from the "grouping of alarms" column in the dataset.
   - Extracted a unique list of **110 ATN Identifiers** associated with these systems.
   - Matched these identifiers with the training data, resulting in a filtered dataset of **6,054 rows** (`evap_df`).

2. **Model Training and Evaluation**:
   - **Target Variable**: `c-b` (Chattering Behavior).
   - **Decision Tree (Baseline)**:
     - Accuracy on validation data: **86.13%**.
   - **Decision Tree (Grid Search)**:
     - Accuracy on validation data: **87.90%**.
   - **K-Nearest Neighbors (KNN)**:
     - **K=3**: Accuracy: **89.80%**, False Negative Rate (FNR): **0.18**.
     - **Best K=6**: Accuracy: **90.13%**, FNR: **0.21**.

#### **Key Insights**
- Focusing on the boiler systems allowed us to achieve high accuracy (**90.13% with KNN**) while maintaining a relatively low false negative rate (**0.18 with K=3**).
- The **Decision Tree with Grid Search** showed improved performance over the baseline model, highlighting the importance of hyperparameter tuning.

---

### **Model 2: Prioritizing Alarm Tags Prone to Chattering**

#### **Approach**
To better analyze chattering behavior, we prioritized alarm tags that were most prone to chattering. This involved ranking alarm tags based on the frequency of chattering flags (`c-b = 1`) and focusing on the top 10 most frequent chattering tags.

#### **Method**
1. **Data Preparation**:
   - Identified the **top 10 ATN Identifiers** with the highest frequency of chattering flags.
   - These top 10 tags accounted for **58% of all chattering alarms** in the training data.
   - Renamed all other ATN Identifiers as `other_alarms` to simplify the analysis.

2. **Model Training and Evaluation**:
   - **Dataset**: `plant_df` (20,000 rows, 60:40 train-validation split).
   - **Target Variable**: `c-b`.
   - **Decision Tree (Baseline)**:
     - Accuracy on validation data: **90.40%**.
   - **Decision Tree (Grid Search)**:
     - Accuracy on validation data: **89.60%**.
   - **K-Nearest Neighbors (KNN)**:
     - **K=3**: Accuracy: **90.40%**, FNR: **0.21**.
     - **Best K=4**: Accuracy: **90.50%**, FNR: **0.29**.

#### **Key Insights**
- Prioritizing the top 10 chattering tags allowed us to focus on the most critical alarms, improving model accuracy (**90.50% with KNN**).
- The **Decision Tree with Grid Search** performed slightly worse than the baseline, suggesting that hyperparameter tuning may not always yield better results for this specific approach.

---

### **Model 3: Category Simplification**

#### **Approach**
To further improve model performance, we simplified categorical variables by grouping similar values into broader categories. For example, values like `XI-3057` and `XI-3058` were reduced to `XI` by removing numeric suffixes.

#### **Method**
1. **Data Preparation**:
   - Simplified the `ATN` column, reducing the number of unique values from **452 to 52**.
   - Renamed all ATN Identifiers other than the top 10 most frequent chattering tags as `other_alarms`.

2. **Model Training and Evaluation**:
   - **Dataset**: `o_plant_df` (20,000 rows, 60:40 train-validation split).
   - **Target Variable**: `c-b`.
   - **Decision Tree (Baseline)**:
     - Accuracy on validation data: **88.80%**.
   - **Decision Tree (Grid Search)**:
     - Accuracy on validation data: **90.30%**.
   - **Random Forest**:
     - Accuracy on validation data: **91.50%**.
   - **Gradient Boosting**:
     - Accuracy on validation data: **88.00%**.
   - **K-Nearest Neighbors (KNN)**:
     - **K=3**: Accuracy: **91.00%**, FNR: **0.18**.
     - **Best K=3**: Accuracy: **91.00%**, FNR: **0.18**.

#### **Key Insights**
- Simplifying categorical variables improved model performance, with the **Random Forest** achieving the highest accuracy (**91.50%**).
- **KNN with K=3** also performed well, with an accuracy of **91.00%** and a low false negative rate (**0.18**), making it a strong candidate for deployment.

---

### **Overall Findings and Recommendations**
1. **Best Performing Model**:
   - **Random Forest** achieved the highest accuracy (**91.50%**) in Model 3, making it the best-performing model overall.
   - **KNN with K=3** also performed well across all models, with consistent accuracy and low false negative rates.

2. **Importance of False Negative Rate (FNR)**:
   - In high-stakes environments like thermal power plants, minimizing false negatives is critical to avoid equipment damage, safety hazards, and plant shutdowns.
   - **KNN with K=3** consistently achieved a low FNR (**0.18**), making it a reliable choice for real-world deployment.

3. **Recommendations for Deployment**:
   - Deploy the **Random Forest** model for its high accuracy and robustness.
   - Continuously monitor model performance and retrain with new data to ensure optimal results.
   - Train operators to interpret and respond to predicted alarms effectively, minimizing the impact of false positives.

---

