# Customer Service Resolution Time Prediction

## Project Objective

Customer service teams frequently struggle to anticipate which service requests will require unusually long resolution times. Prolonged resolution times can increase operational costs, reduce service efficiency, and negatively impact customer satisfaction.

This project develops a machine learning classification model to predict whether a customer service request will experience excessive resolution time based on operational, service, and customer-related attributes.

The objective is to identify high-risk service requests early, enabling support teams to take proactive measures such as prioritizing resources, escalating complex cases, or assigning experienced agents.

---

## Dataset Overview

The dataset contains **700 customer service requests** with 12 variables describing service characteristics, customer attributes, and operational conditions.

### Dataset Dimensions

| Metric        | Value |
|--------------|------|
| Observations | 700  |
| Variables    | 12   |

**Target Variable:** Issue Resolution Time

---

## Key Variables

| Variable                          | Description |
|----------------------------------|------------|
| Service_Type_Code                | Category of service requested |
| Service_Cost                     | Cost associated with resolving the service request |
| Distance_to_Service_Center       | Distance between the customer and the service facility |
| Daily_Request_Volume_Avg         | Average number of requests handled per day |
| Customer_Satisfaction_Index      | Historical satisfaction score for the customer |
| Customer_Tier                    | Customer membership or priority level |
| Previous_Requests                | Number of prior service requests submitted by the customer |
| Customer_Age                     | Age of the customer |
| Support_Contacts                 | Number of interactions with support during the issue |
| Issue_Resolution_Time_Hours      | Total time required to resolve the issue |

---

## Initial Observations from the Dataset

### Resolution Time Distribution

The distribution of resolution times revealed the following statistics:

| Metric  | Value   |
|--------|--------|
| Minimum | 0 hours |
| Median  | 3.5 hours |
| Maximum | 8 hours |
| Average | 3.69 hours |

The **median resolution time (3.5 hours)** was selected as the threshold for defining excessive resolution duration.

Requests were categorized as follows:

- Resolution Time > 3.5 hours ? Excessive Resolution  
- Resolution Time ? 3.5 hours ? Normal Resolution  

Using the median ensures the threshold is data-driven and less influenced by extreme values.

---

## Feature Engineering

Several feature engineering steps were applied during preprocessing to improve the predictive capability of the model.

---

### Date Feature Extraction

The **Request_Date** variable was decomposed into additional temporal features:

- Month  
- Day of the Week  

These variables help the model capture potential temporal patterns in service demand, such as increased requests during certain periods or operational workload variations across weekdays.

---

### One-Hot Encoding of Service Type

The categorical variable **Service_Type_Code** was converted into binary indicator variables:

- service_type_1  
- service_type_2  
- service_type_3  
- service_type_4  

This transformation allows the model to capture differences in resolution complexity across various service categories.

---

### Target Variable Construction

A binary classification variable called **ExcessiveResolutionTime** was created.

| Condition                          | Label |
|-----------------------------------|-------|
| Resolution Time > 3.5 hours       | 1 (Excessive) |
| Resolution Time ? 3.5 hours       | 0 (Normal) |

This transformation converted the regression problem into a binary classification task.

### Class Distribution

The resulting dataset produced approximately balanced classes:

- Excessive resolution: 49.6%  
- Normal resolution: 50.4%  

Balanced classes are beneficial because they prevent the model from becoming biased toward a dominant category.

---

## Model Development

A **Logistic Regression** classifier was used to predict whether a service request would experience excessive resolution time.

Logistic Regression was selected because:

- It performs well on binary classification tasks  
- It provides interpretable results  
- It works efficiently with structured operational datasets  

---

## Feature Scaling

Several numerical variables such as:

- Service Cost  
- Distance to Service Center  
- Customer Age  
- Daily Request Volume  

operate on different numeric scales.

To ensure equal contribution during model training, features were standardized using **StandardScaler**.

Standardization improves model stability and helps gradient-based optimization converge faster.

---

## Train-Test Split

To evaluate model performance on unseen data, the dataset was divided into:

| Dataset      | Size |
|-------------|------|
| Training Set | 560 observations |
| Test Set     | 140 observations |

The training data was used to build the model, while the test data was reserved for evaluating generalization performance.

## Model Performance

### Training Dataset Performance

| Metric   | Score |
|----------|------|
| Accuracy | 86.1% |
| ROC-AUC  | 0.927 |

### Classification Metrics

| Class                 | Precision | Recall | F1 Score |
|----------------------|----------|--------|----------|
| Normal Resolution    | 0.86     | 0.86   | 0.86     |
| Excessive Resolution | 0.86     | 0.86   | 0.86     |

The high ROC-AUC value indicates the model has strong discriminative ability, meaning it effectively distinguishes between normal and excessive resolution cases.

---

### Test Dataset Performance

When evaluated on previously unseen data:

| Metric   | Score |
|----------|------|
| Accuracy | 79.3% |
| ROC-AUC  | 0.90  |

### Classification Metrics

| Class                 | Precision | Recall | F1 Score |
|----------------------|----------|--------|----------|
| Normal Resolution    | 0.76     | 0.84   | 0.80     |
| Excessive Resolution | 0.83     | 0.75   | 0.79     |

Although performance decreases slightly compared to the training dataset, the model still demonstrates strong predictive capability, indicating that it generalizes well to new service requests.

---

## Model Evaluation Visualizations

The model performance was further evaluated using several diagnostic visualizations:

- Confusion Matrix (Training Data)  
- Confusion Matrix (Test Data)  
- ROC Curve (Training Data)  
- ROC Curve (Test Data)  

These visualizations help illustrate:

- Classification accuracy  
- False positive and false negative rates  
- Overall model discrimination ability  

---

## Practical Business Applications

### Early Identification of High-Risk Requests

Customer service systems could automatically flag requests predicted to exceed normal resolution time thresholds.

This allows teams to intervene before delays escalate.

---

### Resource Allocation

High-risk service tickets could be:

- Assigned to senior support agents  
- Escalated earlier in the support workflow  
- Allocated additional technical resources  

---

### Service Process Optimization

Operational leaders can analyze patterns in high-risk requests to identify:

- Service categories with high complexity  
- Operational bottlenecks  
- Staffing gaps  
- Training needs for support agents  

---

## Technologies Used

| Tool          | Purpose |
|--------------|--------|
| Python        | Data analysis and modeling |
| Pandas        | Data manipulation |
| NumPy         | Numerical computations |
| Scikit-Learn  | Machine learning |
| Matplotlib    | Data visualization |

---

## Project Structure

Customer-Service-Resolution-Prediction

Customer-Service-Resolution-Prediction

data/
    customer_service_resolution_rawdata.csv

notebooks/
    Customer Service_Preprocessing.ipynb
    CustomerServiceML.ipynb

images/
    Confusion_Matrix_Testing_Data.png
    Confusion_Matrix_Training_Data.png
    ROC_Curve_Testing_Data.png
    ROC_Curve_Training_Data.png

outputs/
    data_preprocessed.csv

README.md

---

## Future Improvements

### Testing More Advanced Models

Future work could explore more sophisticated algorithms such as:

- Random Forest  
- Gradient Boosting  
- XGBoost  

These models may capture non-linear relationships and potentially improve predictive performance.

---

### Feature Importance Analysis

Analyzing feature importance would help identify which operational or customer attributes most strongly influence resolution time.

This would provide deeper insights for operational decision-making.

---

### Real-Time Deployment

The model could be integrated into a customer support ticket management system to provide real-time predictions when new service requests are submitted.

This would enable immediate risk assessment and proactive resource allocation.

---

## Author

**Adedayo Adebayo**  
Data Scientist | Business Analyst
