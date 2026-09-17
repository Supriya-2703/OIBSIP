# OASIS INFOBYTE — Data Analytics Internship

## Level 1 — Task 2: Customer Segmentation Analysis

## 📌 Project Overview

This project is part of the **Oasis Infobyte Summer Internship Program (OIBSIP)** under the **Data Analytics** track.

The objective of this project is to segment an e-commerce company's customer base based on purchasing behaviour. **RFM (Recency, Frequency, Monetary)** analysis is used to create meaningful customer features, followed by **K-Means clustering** to identify distinct customer segments.

The resulting customer segments can help businesses develop targeted marketing strategies, improve customer retention, and identify high-value customers.

---

## 🎯 Objectives

- Load and inspect an e-commerce transaction dataset.
- Clean missing, duplicate, and inconsistent records.
- Calculate customer-level RFM metrics.
- Analyze average purchase value and customer lifetime value.
- Standardize behavioral features using `StandardScaler`.
- Determine the optimal number of clusters using the Elbow Method.
- Apply K-Means clustering.
- Visualize customer segments.
- Profile and interpret each customer segment.
- Suggest targeted marketing strategies for each segment.
- Export the final customer segmentation dataset.

---

## 📂 Dataset

The project uses the **Online Retail** transactional dataset.

The dataset contains e-commerce transactions with information such as:

- Invoice number
- Product/Stock code
- Product description
- Quantity purchased
- Invoice date
- Unit price
- Customer ID
- Country

### Dataset Size

| Description                  |   Value |
| ---------------------------- | ------: |
| Original records             | 541,909 |
| Records after cleaning       | 392,692 |
| Unique customers             |   4,338 |
| Final customer-level records |   4,338 |

---

## 🧹 Data Cleaning

The following preprocessing steps were performed:

- Removed records without a `CustomerID`.
- Removed cancelled transactions.
- Removed transactions with non-positive quantities.
- Removed transactions with non-positive unit prices.
- Converted `InvoiceDate` to datetime format.
- Standardized `CustomerID`.
- Removed duplicate records.
- Created a `TotalAmount` feature.

The total transaction value was calculated as:

```text
TotalAmount = Quantity × UnitPrice
```

---

## 📊 RFM Analysis

Customer purchasing behaviour was summarized using three RFM features.

### Recency

Number of days since the customer's most recent purchase.

### Frequency

Number of unique invoices associated with the customer.

### Monetary

Total amount spent by the customer.

In addition, the project calculates:

- **Average Purchase Value**
- **Customer Lifetime Value**

For this project, historical customer spending is used as the simplified Customer Lifetime Value measure.

---

## ⚙️ Feature Standardization

The following features were selected for clustering:

```text
Recency
Frequency
Monetary
```

Because these features have different numerical scales, `StandardScaler` from Scikit-learn was used to standardize them before applying K-Means.

---

## 🔍 Elbow Method

The Elbow Method was used to determine a suitable number of customer clusters.

The evaluated values of K were:

```text
K = 2 to K = 10
```

The inertia values were:

|   K | Inertia |
| --: | ------: |
|   2 | 9014.57 |
|   3 | 5441.32 |
|   4 | 4096.30 |
|   5 | 3119.79 |
|   6 | 2473.79 |
|   7 | 2023.59 |
|   8 | 1717.01 |
|   9 | 1468.79 |
|  10 | 1281.05 |

Based on the Elbow Method, **K = 5** was selected as a reasonable balance between reducing within-cluster variation and maintaining a manageable number of customer segments.

---

## 🤖 K-Means Clustering

K-Means clustering was applied using:

```python
KMeans(
    n_clusters=5,
    random_state=42,
    n_init=10
)
```

The analysis produced **5 customer clusters**.

### Cluster Distribution

|   Cluster | Number of Customers |
| --------: | ------------------: |
|         0 |               3,048 |
|         1 |               1,063 |
|         2 |                   8 |
|         3 |                 213 |
|         4 |                   6 |
| **Total** |           **4,338** |

---

## 👥 Customer Segment Profiles

### Cluster 0 – Regular/Moderate Customers

- Largest customer segment.
- Relatively recent purchasing activity.
- Moderate purchase frequency.
- Moderate historical spending.

**Suggested strategy:**
Use loyalty rewards, personalized recommendations, and cross-selling offers to increase purchase frequency and spending.

---

### Cluster 1 – At-Risk/Inactive Customers

- High Recency values.
- Customers have not purchased recently.
- Relatively low purchase frequency and spending.

**Suggested strategy:**
Use re-engagement campaigns, personalized discounts, and targeted reminders to encourage customers to return.

---

### Cluster 2 – High-Value Frequent Customers

- Very small customer group.
- Very high purchase frequency.
- Very high monetary value.
- Recent purchasing activity.

**Suggested strategy:**
Offer VIP benefits, exclusive products, early access, and personalized offers to strengthen retention.

---

### Cluster 3 – Valuable Active Customers

- Relatively recent purchasing activity.
- Higher purchase frequency than the large moderate segment.
- Higher historical monetary value.

**Suggested strategy:**
Use loyalty programs, product bundles, personalized recommendations, and targeted cross-selling.

---

### Cluster 4 – Extremely High-Value Customers

- Very small customer group.
- Extremely high monetary value.
- High purchase frequency.
- Represents exceptional historical spenders within this dataset.

**Suggested strategy:**
Provide premium customer service, personalized relationship management, exclusive offers, and strong retention incentives.

---

## 📈 Visualizations

The project includes:

### 1. RFM Distribution Analysis

Histograms and boxplots were used to understand the distributions of Recency, Frequency, and Monetary values.

### 2. Elbow Method

Used to identify a suitable value of K for K-Means clustering.

### 3. Recency vs Monetary

Visualizes customer segments based on how recently customers purchased and how much they spent.

### 4. Frequency vs Monetary

Visualizes the relationship between purchase frequency and monetary value across customer segments.

### 5. Customer Count by Cluster

A bar chart shows the number of customers belonging to each cluster.

---

## 💡 Key Insights

- The majority of customers belong to **Clusters 0 and 1**.
- Cluster 0 represents the largest group with relatively recent and moderate purchasing behaviour.
- Cluster 1 contains customers with high Recency values and can be considered an important re-engagement segment.
- Clusters 2 and 4 contain very few customers but have exceptionally high Frequency and Monetary values.
- Cluster 3 represents a smaller group of relatively valuable and active customers.
- RFM-based clustering provides a practical way to differentiate customers according to purchasing behaviour.
- Different customer segments can be targeted with different marketing strategies rather than using a single campaign for the entire customer base.

---

## 🛠️ Technologies Used

- **Python**
- **Pandas**
- **NumPy**
- **Scikit-learn**
- **Matplotlib**
- **Seaborn**
- **Jupyter Notebook**
- **K-Means Clustering**
- **StandardScaler**

---

## 📁 Project Structure

```text
DataAnalytics-L1-CustomerSegmentation/
│
├── Customer_Segmentation.ipynb
├── OnlineRetail.csv
├── Screenshots
├── customer_rfm.csv
├── customer_segments.csv
└── README.md
```

### Output Files

**`customer_rfm.csv`**

Contains the customer-level RFM analysis and additional customer value metrics.

**`customer_segments.csv`**

Contains the final customer-level dataset with the assigned K-Means cluster.

---

## 🚀 How to Run the Project

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
```

### 2. Navigate to the project folder

```bash
cd OIBSIP/DataAnalytics-L1-CustomerSegmentation
```

### 3. Install the required libraries

```bash
pip install pandas numpy scikit-learn matplotlib seaborn openpyxl jupyter
```

### 4. Start Jupyter Notebook

```bash
jupyter notebook
```

### 5. Open

```text
Customer_Segmentation.ipynb
```

Run the notebook cells sequentially to reproduce the analysis.

---

## 📌 Project Outcome

The project successfully transformed raw e-commerce transaction data into actionable customer segments using **RFM analysis and K-Means clustering**.

The final dataset contains **4,338 customers**, each assigned to one of **5 customer segments**, providing a foundation for targeted marketing and customer relationship strategies.

---

## 👩‍💻 Author

**Supriya Bhade**

Data Analytics | Python | Machine Learning | Data Visualization

GitHub: `https://github.com/Supriya-2703`

---

## 📚 Internship

**Oasis Infobyte Summer Internship Program (OIBSIP)**
**Track:** Data Analytics
**Task:** Level 1 – Task 2: Customer Segmentation Analysis
