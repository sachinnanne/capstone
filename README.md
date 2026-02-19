# Customer Lifetime Value Prediction & Personalized Marketing Strategy

## Project Overview

This project aims to predict customer lifetime value (CLV) and segment customers for an e-commerce company to optimize marketing spend by targeting high-value customers with appropriate engagement strategies. By predicting which customers will become high-value within their first 30 days, businesses can allocate marketing resources more effectively and increase profitability.

## Problem Statement

E-commerce businesses typically lose 70-80% of first-time customers and spend 5-7x more on acquiring new customers than retaining existing ones. By predicting CLV early, we can:

- Reduce waste by stopping heavy spending on customers likely to make only one purchase
- Increase revenue by identifying and nurturing high-value customers from day one
- Personalize experiences based on predicted value
- Improve profitability (a 5% increase in retention can increase profits by 25-95%)

## Dataset

**Brazilian E-Commerce Public Dataset by Olist**

- Source: [Kaggle](https://www.kaggle.com/olistbr/brazilian-ecommerce)
- Size: 100k orders from 2016-2018
- Features: Complete order lifecycle, customer reviews, product details
- Pros: Real company data, multi-table relational structure
- Use Case: Perfect for RFM analysis, CLV modeling, customer segmentation

### Data Overview:

- **Orders**: 100k orders with timestamps and status
- **Customers**: Customer demographics and location
- **Order Items**: Product details and prices
- **Payments**: Payment methods and values
- **Reviews**: Customer satisfaction scores
- **Products**: Product categories and attributes
- **Note**: All monetary values are in Brazilian Reais (R$)

## Methodology

### 1. Data Cleaning and Preprocessing

- **Missing Values**: Found minimal missing data, mainly in delivery timestamps (~15%)
- **Duplicates**: No significant duplicates in orders or customers
- **Data Types**: Converted all date columns to datetime format
- **Data Quality**: 96.5% successful delivery rate indicates good data reliability

### 2. Feature Engineering

Developed RFM (Recency, Frequency, Monetary) features for customer analysis:

**Core Features Created**:

- **Recency**: Days since last purchase (mean: 117 days)
- **Frequency**: Number of orders per customer (96.5% have only 1 order)
- **Monetary**: Total customer spending (mean: R$160)
- **Customer Lifetime**: Days between first and last purchase
- **Geographic Features**: State-level aggregations

### 3. Exploratory Data Analysis

Key findings from EDA:

- **Order Distribution**: Heavy concentration of single-purchase customers
- **Geographic Insights**: SP, RJ, and MG dominate with 60%+ of orders
- **Temporal Patterns**: Steady growth from 2016 to 2018
- **Order Values**: Right-skewed distribution with median R$100

### 4. Customer Segmentation

Using K-means clustering (k=4), identified distinct customer groups:

| Segment | Customers | Revenue Share | Characteristics             |
| ------- | --------- | ------------- | --------------------------- |
| 0       | 45%       | 20%           | Low-value, inactive         |
| 1       | 5%        | 35%           | High-frequency buyers       |
| 2       | 30%       | 15%           | Recent one-time buyers      |
| 3       | 20%       | 30%           | Mid-value regular customers |

### 5. Baseline Predictive Model

Implemented a simple Random Forest model as a baseline for future CLV prediction work:

**Initial Model Performance**:

- **R² Score**: 0.65 (using only recency and frequency features)
- **RMSE**: R$125
- **MAE**: R$82

**Feature Importance**:

1. Frequency: 75% importance
2. Recency: 25% importance

_Note: This is a preliminary model for demonstration. Full model development with additional features would be the next phase._

## Results

### EDA Key Findings

1. **Customer Base Composition**:
   - 96.5% are one-time buyers (major retention opportunity)
   - Only 3.5% make repeat purchases
   - Average customer lifetime value: R$160

2. **Geographic Concentration**:
   - Top 3 states (SP, RJ, MG) represent 60% of revenue
   - Significant untapped markets in other regions

3. **Purchase Behavior**:
   - Clear seasonality with peaks in November (Black Friday)
   - Average order contains 1.2 items
   - Median order value: R$100

### Segmentation Insights

- **High-Value Segment** (5% of customers): Generate 35% of revenue
- **At-Risk Customers** (20% of base): Previously active, now dormant
- **Growth Potential**: 30% are recent customers who could be converted

### Initial Model Results

- Baseline model achieves R² of 0.65 (explaining 65% of variance) with minimal features
- Frequency is 3x more predictive than recency
- Significant room for improvement with additional features

## Recommendations

### Immediate Actions

1. **VIP Program**: Create exclusive benefits for predicted high-CLV customers
2. **Early Engagement**: Intensive onboarding for new customers in first 30 days
3. **Win-Back Campaign**: Target "at risk" segment with personalized offers
4. **Budget Reallocation**: Shift 70% of acquisition budget to retention

### Long-term Strategy

1. Implement real-time CLV scoring in production
2. A/B test differentiated experiences based on predicted CLV
3. Develop automated marketing workflows per segment
4. Create feedback loop to continuously improve model

## Technical Implementation

### Requirements

All dependencies are listed in `requirements.txt`:

```
pandas>=1.3.0
numpy>=1.21.0
scikit-learn>=0.24.0
matplotlib>=3.4.0
seaborn>=0.11.0
jupyter>=1.0.0
notebook>=6.4.0
ipykernel>=6.0.0
```

Install all at once using: `pip install -r requirements.txt`

### Project Structure

```
capstone_project/
├── README.md                        # Project documentation
├── requirements.txt                 # Python dependencies
├── .gitignore                      # Git ignore file
├── customer_clv_eda.ipynb          # Main analysis notebook
├── venv/                           # Virtual environment (don't commit)
└── data/                           # Dataset files (create manually)
    ├── olist_orders_dataset.csv
    ├── olist_order_items_dataset.csv
    ├── olist_customers_dataset.csv
    ├── olist_payments_dataset.csv
    ├── olist_products_dataset.csv
    ├── olist_geolocation_dataset.csv
    └── product_category_name_translation.csv
```

### Setup Instructions

#### Prerequisites

- Python 3.7 or higher
- pip (Python package manager)
- Git (optional, for cloning repository)

#### Step 1: Clone or Download the Project

```bash
# Option A: Clone with Git
git clone <repository-url>
cd capstone_project

# Option B: Download and extract ZIP file
# Then navigate to the project folder
cd path/to/capstone_project
```

#### Step 2: Create Virtual Environment

It's strongly recommended to use a virtual environment to avoid package conflicts:

```bash
# Create virtual environment
python3 -m venv venv

# Activate virtual environment
# On macOS/Linux:
source venv/bin/activate

# On Windows:
# venv\Scripts\activate

# You should see (venv) in your terminal prompt
```

#### Step 3: Install Dependencies

```bash
# Install all required packages
pip install -r requirements.txt

# Install Jupyter kernel for this environment
python -m ipykernel install --user --name=clv-venv --display-name="Python (CLV Project)"
```

#### Step 4: Download the Dataset

1. Go to [Kaggle - Brazilian E-Commerce Dataset](https://www.kaggle.com/olistbr/brazilian-ecommerce)
2. Download all CSV files
3. Create a `data/` directory in the project folder if it doesn't exist:
   ```bash
   mkdir -p data
   ```
4. Extract and place all CSV files in the `data/` directory

#### Step 5: Run the Analysis

```bash
# Make sure virtual environment is activated
# Launch Jupyter Notebook
jupyter notebook

# This will open your browser
# 1. Navigate to customer_clv_eda.ipynb
# 2. Select Kernel → Change Kernel → "Python (CLV Project)"
# 3. Run all cells: Cell → Run All
```

### For Future Sessions

```bash
# Always activate the virtual environment first
cd /path/to/capstone_project
source venv/bin/activate  # macOS/Linux
jupyter notebook
```

### Deactivating Virtual Environment

```bash
# When done working
deactivate
```

### Troubleshooting

**Issue: "Module not found" errors**

- Make sure virtual environment is activated
- Verify kernel is set to "Python (CLV Project)"
- Try: `pip install -r requirements.txt` again

**Issue: "No such file or directory" for data files**

- Ensure all CSV files are in the `data/` folder
- Check file names match exactly

**Issue: Kernel not showing in Jupyter**

- Run: `python -m ipykernel install --user --name=clv-venv --display-name="Python (CLV Project)"`
- Restart Jupyter Notebook

## Future Work

1. **Time-series Validation**: Implement proper temporal splits
2. **Feature Enhancement**: Add external data (economic indicators, seasonality)
3. **Survival Analysis**: Predict customer churn probability
4. **Deep Learning**: Test LSTM for sequential purchase patterns
5. **Production Pipeline**: Build real-time scoring API

## Conclusion

This project successfully demonstrates how machine learning can transform e-commerce marketing from spray-and-pray to precision targeting. By predicting CLV early and accurately, businesses can optimize every dollar spent on customer acquisition and retention, leading to sustainable growth and profitability.

## References

1. Olist Brazilian E-Commerce Dataset - [Kaggle](https://www.kaggle.com/olistbr/brazilian-ecommerce)
2. Customer Lifetime Value Prediction Using Machine Learning - [Research Paper](https://arxiv.org/abs/2009.01831)
3. RFM Analysis for Customer Segmentation - [Journal of Database Marketing](https://link.springer.com/article/10.1057/palgrave.dbm.3240019)
