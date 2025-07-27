# TonyFunkman Data Science Tasks

## Overview

This consolidated guide contains all core data science tasks for TonyFunkman, organized by workflow stage and complexity level.

---

## 📊 TASK 1: ANALYZE DATASET

_Comprehensive data analysis from exploration to insights_

### Quick Start

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

def analyze_dataset(file_path):
    """Comprehensive dataset analysis"""

    # Load data
    df = pd.read_csv(file_path)
    print(f"📊 Dataset loaded: {len(df)} rows, {len(df.columns)} columns")

    # Basic profiling
    print("\n🔍 DATASET PROFILE")
    print(f"Shape: {df.shape}")
    print(f"Memory usage: {df.memory_usage(deep=True).sum() / 1024**2:.2f} MB")

    # Missing values
    missing_data = df.isnull().sum()
    if missing_data.sum() > 0:
        print("\n❌ MISSING DATA")
        print(missing_data[missing_data > 0])

    # Basic statistics
    print("\n📈 DESCRIPTIVE STATISTICS")
    print(df.describe())

    return df
```

---

## 🛍️ TASK 2: E-COMMERCE ANALYSIS

_Specialized e-commerce analysis with customer segmentation_

### Customer Segmentation (RFM)

```python
def ecommerce_rfm_analysis(orders_df):
    """RFM customer segmentation"""

    current_date = orders_df['order_date'].max()

    rfm = orders_df.groupby('customer_id').agg({
        'order_date': lambda x: (current_date - x.max()).days,  # Recency
        'order_id': 'count',  # Frequency
        'total_amount': 'sum'  # Monetary
    })

    # Customer segmentation logic
    def segment_customers(row):
        if row['recency'] <= 30 and row['frequency'] >= 3:
            return 'Champions'
        elif row['recency'] <= 60 and row['frequency'] >= 2:
            return 'Loyal Customers'
        elif row['recency'] <= 30:
            return 'New Customers'
        else:
            return 'At Risk'

    rfm['segment'] = rfm.apply(segment_customers, axis=1)

    print("🎯 CUSTOMER SEGMENTS")
    print(rfm['segment'].value_counts())

    return rfm
```

---

## 🤖 TASK 3: BUILD ML MODEL

_Complete machine learning pipeline_

### Model Development

```python
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report

def build_ml_model(df, target_column):
    """Build and train ML model"""

    X = df.drop(columns=[target_column])
    y = df[target_column]

    # Handle categorical variables
    categorical_cols = X.select_dtypes(include=['object']).columns
    for col in categorical_cols:
        X[col] = pd.Categorical(X[col]).codes

    # Train-test split
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

    # Train model
    model = RandomForestClassifier(n_estimators=100, random_state=42)
    model.fit(X_train, y_train)

    # Evaluate
    y_pred = model.predict(X_test)
    print("📊 MODEL PERFORMANCE")
    print(classification_report(y_test, y_pred))

    return model
```

---

## 📊 TASK 4: CREATE DASHBOARD

_Interactive dashboard creation_

### Streamlit Dashboard

```python
import streamlit as st
import plotly.express as px

def create_dashboard(df):
    """Create interactive dashboard"""

    st.title("Data Science Dashboard")

    # Dataset overview
    st.header("📊 Dataset Overview")
    col1, col2 = st.columns(2)

    with col1:
        st.metric("Total Rows", len(df))
    with col2:
        st.metric("Total Columns", len(df.columns))

    # Visualizations
    numeric_cols = df.select_dtypes(include=[np.number]).columns
    if len(numeric_cols) > 0:
        selected_col = st.selectbox("Select Column", numeric_cols)
        fig = px.histogram(df, x=selected_col)
        st.plotly_chart(fig)

    # Data table
    st.dataframe(df.head(100))
```

---

## 🚀 TASK 5: DEPLOY MODEL

_Production model deployment_

### Flask API

```python
from flask import Flask, request, jsonify
import joblib

app = Flask(__name__)
model = joblib.load('model.pkl')

@app.route('/predict', methods=['POST'])
def predict():
    """API endpoint for predictions"""
    try:
        data = request.get_json()
        prediction = model.predict([list(data.values())])[0]
        return jsonify({'prediction': int(prediction)})
    except Exception as e:
        return jsonify({'error': str(e)}), 400

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

---

## 💰 TASK 6: MEASURE BUSINESS IMPACT

_ROI and business value measurement_

### ROI Calculation

```python
def calculate_roi(benefits, costs, time_period=12):
    """Calculate project ROI"""

    total_benefits = sum(benefits.values()) * time_period
    total_costs = sum(costs.values())

    roi = ((total_benefits - total_costs) / total_costs) * 100

    print("💰 ROI ANALYSIS")
    print(f"Total Benefits: ${total_benefits:,.2f}")
    print(f"Total Costs: ${total_costs:,.2f}")
    print(f"ROI: {roi:.1f}%")

    return roi
```

---

## ⚡ TASK 7: ADAPTIVE PROCESSING

_Smart data processing based on size_

### Adaptive Strategy

```python
import psutil

def adaptive_process(file_path):
    """Choose processing strategy based on data size"""

    import os
    file_size_gb = os.path.getsize(file_path) / (1024**3)
    memory_gb = psutil.virtual_memory().total / (1024**3)

    if file_size_gb < memory_gb * 0.3:
        print("🐼 Using Pandas")
        return pd.read_csv(file_path)
    else:
        print("⚡ Using Dask")
        import dask.dataframe as dd
        return dd.read_csv(file_path)
```

---

## 🔗 TASK 8: LEGACY INTEGRATION

_Connect with existing systems_

### Database Integration

```python
import sqlalchemy

def integrate_legacy_db(connection_string, query):
    """Connect to legacy database"""

    engine = sqlalchemy.create_engine(connection_string)
    df = pd.read_sql(query, engine)

    print(f"✅ Extracted {len(df)} rows from legacy system")
    return df
```

---

## 🎯 TASK 9: OPTIMIZE COSTS

_Automatic cost optimization_

### Cost Monitoring

```python
def monitor_costs():
    """Monitor and optimize costs"""

    # Simulate cost monitoring
    costs = {
        'compute': 50,
        'storage': 20,
        'network': 10
    }

    total = sum(costs.values())
    print(f"💰 Daily costs: ${total}")

    if total > 100:
        print("🚨 Budget exceeded - optimizing...")
        return optimize_resources()

    return costs

def optimize_resources():
    """Optimize resource usage"""
    optimizations = [
        "Scale down compute instances",
        "Use spot instances",
        "Optimize storage tiers"
    ]

    print("🎯 OPTIMIZATIONS:")
    for opt in optimizations:
        print(f"- {opt}")

    return optimizations
```

---

## 🎮 QUICK REFERENCE

### TonyFunkman Commands

```yaml
# Core Analysis
*analyze-data          # General dataset analysis
*analyze-ecommerce     # E-commerce specific analysis

# Machine Learning
*build-model          # Build and train ML models
*deploy-model         # Deploy models to production

# Business Intelligence
*create-dashboard     # Interactive dashboards
*measure-impact       # Business impact and ROI

# Advanced Operations
*adaptive-processing  # Smart data processing
*integrate-legacy     # Legacy system integration
*optimize-costs       # Cost optimization

# Modes
*mode-engineering     # Data engineering focus
*mode-analysis        # Analysis and BI focus
*mode-science         # ML and AI focus
*mode-production      # Production deployment focus
```

---

_This guide contains all essential TonyFunkman data science tasks in one consolidated file._
