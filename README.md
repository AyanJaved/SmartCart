# SmartCart - Customer Segmentation

A machine learning project that segments customers based on their demographics, income, and purchasing behavior using unsupervised clustering techniques.

---

## About the Project

SmartCart analyzes customer data from a retail/e-commerce context to group customers into meaningful segments. These segments help businesses understand their customer base and tailor marketing strategies accordingly. The project uses PCA for dimensionality reduction and both K-Means and Agglomerative Clustering to identify 4 distinct customer groups.

---

## Dataset

**File:** `smartcart_customers.csv` — 2240 customer records

Key features used:

| Feature | Description |
|---|---|
| Year_Birth | Customer's birth year (used to derive Age) |
| Income | Annual household income |
| Education | Education level |
| Marital_Status | Marital status |
| Kidhome / Teenhome | Number of kids and teenagers at home |
| Dt_Customer | Date the customer joined |
| MntWines, MntFruits, etc. | Spending on various product categories |
| Recency | Days since last purchase |
| Response | Response to marketing campaign |

---

## Project Workflow

### 1. Data Loading
- Loaded customer dataset using `pandas`

### 2. Data Pre-Processing
- Missing `Income` values filled with **median**
- Outliers removed: Age > 90 and Income > 600,000

### 3. Feature Engineering
New features derived from existing columns:

| New Feature | Description |
|---|---|
| Age | Calculated as 2026 - Year_Birth |
| Customer_Tenure_Days | Days since the customer joined |
| Total_Spending | Sum of spending across all product categories |
| Total_Children | Sum of Kidhome + Teenhome |
| Education | Simplified to: Undergraduate, Graduate, Postgraduate |
| Living_With | Simplified to: Partner or Alone |

### 4. Encoding
- `OneHotEncoder` applied to `Education` and `Living_With`

### 5. Scaling
- `StandardScaler` applied to all features before clustering

### 6. Dimensionality Reduction
- `PCA` applied — both 2D and 3D projections visualized
- 3 principal components used for clustering

### 7. Optimal K Selection
Two methods used to find the best number of clusters:
- **Elbow Method** — WCSS plotted for K = 1 to 10, optimal K detected using `KneeLocator`
- **Silhouette Score** — Scored for K = 2 to 10 and plotted

### 8. Clustering
Two algorithms applied with **4 clusters**:

| Algorithm | Details |
|---|---|
| K-Means | n_clusters=4, random_state=42 |
| Agglomerative Clustering | n_clusters=4, linkage=ward |

### 9. Cluster Characterization
- Cluster distribution visualized using count plot
- Income vs. Total Spending scatter plot colored by cluster
- Cluster summary table showing mean values per group

---

## Tech Stack

- **Language:** Python 3
- **Notebook:** Jupyter Notebook
- **Libraries:**
  - `pandas` — data manipulation
  - `matplotlib` & `seaborn` — visualization
  - `scikit-learn` — preprocessing, PCA, clustering, metrics
  - `kneed` — automatic elbow point detection

---

## Installation and Setup

1. **Clone the repository**
```bash
git clone https://github.com/AyanJaved/SmartCart.git
cd SmartCart
```

2. **Install required libraries**
```bash
pip install pandas matplotlib seaborn scikit-learn kneed
```

3. **Run the notebook**
```bash
jupyter notebook smartcart.ipynb
```

Make sure `smartcart_customers.csv` is in the same directory as the notebook.

---

## Project Structure

```
SmartCart/
│
├── smartcart.ipynb              # Main Jupyter Notebook
├── smartcart_customers.csv      # Customer dataset
└── README.md                    # Project documentation
```

---

## License

This project is open source and available under the [MIT License](LICENSE).
