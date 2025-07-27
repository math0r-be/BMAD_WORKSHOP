# Data Science Core Tasks - TonyFunkman Complete Guide

## Overview

This consolidated guide contains all core data science tasks for TonyFunkman, organized by workflow stage and complexity level. Each task includes practical examples, error handling, and production-ready implementations.

---

## 📊 TASK 1: ANALYZE DATASET

_Comprehensive data analysis from exploration to insights_

### Quick Start

```python
# Basic dataset profiling with error handling
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from functools import wraps
import logging

# Error handling decorator
def handle_data_errors(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        try:
            return func(*args, **kwargs)
        except FileNotFoundError as e:
            logging.error(f"Data file not found: {e}")
            raise ValueError(f"Dataset file not accessible: {e}")
        except pd.errors.EmptyDataError:
            logging.error("Dataset is empty")
            raise ValueError("Dataset contains no data")
        except MemoryError:
            logging.error("Dataset too large for available memory")
            raise ValueError("Dataset exceeds memory limits. Consider chunking.")
        except Exception as e:
            logging.error(f"Unexpected error: {e}")
            raise
    return wrapper

@handle_data_errors
def analyze_dataset(file_path, sample_size=None):
    """Comprehensive dataset analysis with error handling"""

    # Load data with size check
    if sample_size:
        df = pd.read_csv(file_path, nrows=sample_size)
        print(f"📊 Loaded sample of {len(df)} rows")
    else:
        df = pd.read_csv(file_path)
        print(f"📊 Loaded {len(df)} rows, {len(df.columns)} columns")

    # Basic profiling
    print("\n🔍 DATASET PROFILE")
    print(f"Shape: {df.shape}")
    print(f"Memory usage: {df.memory_usage(deep=True).sum() / 1024**2:.2f} MB")

    # Missing values analysis
    missing_data = df.isnull().sum()
    missing_percent = (missing_data / len(df)) * 100
    missing_df = pd.DataFrame({
        'Missing Count': missing_data,
        'Missing Percentage': missing_percent
    }).sort_values('Missing Percentage', ascending=False)

    print("\n❌ MISSING DATA")
    print(missing_df[missing_df['Missing Count'] > 0])

    # Data types and basic stats
    print("\n📈 DESCRIPTIVE STATISTICS")
    print(df.describe(include='all'))

    return df, missing_df
```

### Advanced Analysis

```python
def advanced_data_analysis(df):
    """Advanced statistical analysis and insights"""

    # Correlation analysis
    numerical_cols = df.select_dtypes(include=[np.number]).columns
    if len(numerical_cols) > 1:
        correlation_matrix = df[numerical_cols].corr()

        plt.figure(figsize=(10, 8))
        sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', center=0)
        plt.title('Correlation Matrix')
        plt.show()

    # Outlier detection
    for col in numerical_cols:
        Q1 = df[col].quantile(0.25)
        Q3 = df[col].quantile(0.75)
        IQR = Q3 - Q1
        outliers = df[(df[col] < Q1 - 1.5 * IQR) | (df[col] > Q3 + 1.5 * IQR)]

        if len(outliers) > 0:
            print(f"⚠️ {col}: {len(outliers)} outliers detected ({len(outliers)/len(df)*100:.1f}%)")

    # Distribution analysis
    categorical_cols = df.select_dtypes(include=['object']).columns
    for col in categorical_cols[:5]:  # Limit to first 5 categorical columns
        print(f"\n📊 {col} distribution:")
        print(df[col].value_counts().head())
```

---

## 🛍️ TASK 2: ANALYZE E-COMMERCE DATA

_Specialized e-commerce analysis with customer segmentation_

### Customer Segmentation (RFM Analysis)

```python
def ecommerce_rfm_analysis(orders_df):
    """RFM (Recency, Frequency, Monetary) customer segmentation"""

    # Calculate RFM metrics
    current_date = orders_df['order_date'].max()

    rfm = orders_df.groupby('customer_id').agg({
        'order_date': lambda x: (current_date - x.max()).days,  # Recency
        'order_id': 'count',  # Frequency
        'total_amount': 'sum'  # Monetary
    }).rename(columns={
        'order_date': 'recency',
        'order_id': 'frequency',
        'total_amount': 'monetary'
    })

    # RFM scoring (1-5 scale)
    rfm['r_score'] = pd.qcut(rfm['recency'], 5, labels=[5,4,3,2,1])
    rfm['f_score'] = pd.qcut(rfm['frequency'].rank(method='first'), 5, labels=[1,2,3,4,5])
    rfm['m_score'] = pd.qcut(rfm['monetary'], 5, labels=[1,2,3,4,5])

    # Customer segmentation
    def segment_customers(row):
        if row['r_score'] >= 4 and row['f_score'] >= 4:
            return 'Champions'
        elif row['r_score'] >= 3 and row['f_score'] >= 3:
            return 'Loyal Customers'
        elif row['r_score'] >= 4:
            return 'New Customers'
        elif row['f_score'] >= 3:
            return 'Potential Loyalists'
        elif row['r_score'] >= 2:
            return 'At Risk'
        else:
            return 'Lost Customers'

    rfm['segment'] = rfm.apply(segment_customers, axis=1)

    # Segment analysis
    segment_summary = rfm.groupby('segment').agg({
        'recency': 'mean',
        'frequency': 'mean',
        'monetary': 'mean'
    }).round(2)

    print("🎯 CUSTOMER SEGMENTS")
    print(segment_summary)

    return rfm, segment_summary

def calculate_customer_lifetime_value(rfm_df):
    """Calculate Customer Lifetime Value"""

    avg_order_value = rfm_df['monetary'] / rfm_df['frequency']
    purchase_frequency = rfm_df['frequency'] / (rfm_df['recency'] / 365)  # Annual frequency
    customer_lifespan = 365 / rfm_df['recency']  # Estimated lifespan in years

    clv = avg_order_value * purchase_frequency * customer_lifespan

    print(f"💰 CUSTOMER LIFETIME VALUE")
    print(f"Average CLV: ${clv.mean():.2f}")
    print(f"Median CLV: ${clv.median():.2f}")
    print(f"Top 10% CLV: ${clv.quantile(0.9):.2f}")

    return clv
```

---

## 🤖 TASK 3: BUILD ML MODEL

_Complete machine learning model development workflow_

### Model Development Pipeline

```python
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.preprocessing import StandardScaler, LabelEncoder
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report, confusion_matrix
import joblib

def build_ml_model(df, target_column, problem_type='classification'):
    """Complete ML model building pipeline"""

    print("🤖 BUILDING ML MODEL")
    print("=" * 30)

    # Data preparation
    X = df.drop(columns=[target_column])
    y = df[target_column]

    # Handle categorical variables
    categorical_cols = X.select_dtypes(include=['object']).columns
    for col in categorical_cols:
        le = LabelEncoder()
        X[col] = le.fit_transform(X[col].astype(str))

    # Handle missing values
    X = X.fillna(X.mean())

    # Train-test split
    X_train, X_test, y_train, y_test = train_test_split(
        X, y, test_size=0.2, random_state=42, stratify=y if problem_type == 'classification' else None
    )

    # Feature scaling
    scaler = StandardScaler()
    X_train_scaled = scaler.fit_transform(X_train)
    X_test_scaled = scaler.transform(X_test)

    # Model selection and training
    if problem_type == 'classification':
        model = RandomForestClassifier(n_estimators=100, random_state=42)
    else:
        from sklearn.ensemble import RandomForestRegressor
        model = RandomForestRegressor(n_estimators=100, random_state=42)

    # Train model
    model.fit(X_train_scaled, y_train)

    # Cross-validation
    cv_scores = cross_val_score(model, X_train_scaled, y_train, cv=5)
    print(f"Cross-validation scores: {cv_scores}")
    print(f"Average CV score: {cv_scores.mean():.3f} (+/- {cv_scores.std() * 2:.3f})")

    # Predictions and evaluation
    y_pred = model.predict(X_test_scaled)

    if problem_type == 'classification':
        print("\n📊 CLASSIFICATION REPORT")
        print(classification_report(y_test, y_pred))

        print("\n🔢 CONFUSION MATRIX")
        print(confusion_matrix(y_test, y_pred))
    else:
        from sklearn.metrics import mean_squared_error, r2_score
        mse = mean_squared_error(y_test, y_pred)
        r2 = r2_score(y_test, y_pred)
        print(f"\n📊 REGRESSION METRICS")
        print(f"MSE: {mse:.3f}")
        print(f"R²: {r2:.3f}")

    # Feature importance
    feature_importance = pd.DataFrame({
        'feature': X.columns,
        'importance': model.feature_importances_
    }).sort_values('importance', ascending=False)

    print("\n🎯 TOP 10 FEATURE IMPORTANCE")
    print(feature_importance.head(10))

    # Save model
    model_filename = f"model_{problem_type}_{target_column}.joblib"
    joblib.dump({
        'model': model,
        'scaler': scaler,
        'feature_columns': X.columns.tolist(),
        'label_encoders': {}  # Store label encoders if needed
    }, model_filename)

    print(f"\n💾 Model saved as: {model_filename}")

    return model, scaler, feature_importance
```

### Model Optimization

```python
from sklearn.model_selection import GridSearchCV

def optimize_model_hyperparameters(X_train, y_train, model_type='random_forest'):
    """Hyperparameter optimization using Grid Search"""

    print("⚙️ OPTIMIZING HYPERPARAMETERS")
    print("=" * 35)

    if model_type == 'random_forest':
        model = RandomForestClassifier(random_state=42)
        param_grid = {
            'n_estimators': [50, 100, 200],
            'max_depth': [None, 10, 20, 30],
            'min_samples_split': [2, 5, 10],
            'min_samples_leaf': [1, 2, 4]
        }

    # Grid search with cross-validation
    grid_search = GridSearchCV(
        model, param_grid, cv=5, scoring='accuracy', n_jobs=-1, verbose=1
    )

    grid_search.fit(X_train, y_train)

    print(f"Best parameters: {grid_search.best_params_}")
    print(f"Best cross-validation score: {grid_search.best_score_:.3f}")

    return grid_search.best_estimator_
```

---

## 📊 TASK 4: CREATE DASHBOARD

_Interactive dashboard creation with business insights_

### Streamlit Dashboard

```python
import streamlit as st
import plotly.express as px
import plotly.graph_objects as go

def create_data_dashboard(df, title="Data Science Dashboard"):
    """Create interactive Streamlit dashboard"""

    st.title(title)
    st.sidebar.title("Dashboard Controls")

    # Dataset overview
    st.header("📊 Dataset Overview")
    col1, col2, col3 = st.columns(3)

    with col1:
        st.metric("Total Rows", len(df))
    with col2:
        st.metric("Total Columns", len(df.columns))
    with col3:
        st.metric("Missing Values", df.isnull().sum().sum())

    # Data filtering
    st.sidebar.header("Filters")

    # Numeric column filter
    numeric_cols = df.select_dtypes(include=[np.number]).columns
    if len(numeric_cols) > 0:
        selected_numeric = st.sidebar.selectbox("Select Numeric Column", numeric_cols)

        # Range slider for numeric column
        min_val, max_val = float(df[selected_numeric].min()), float(df[selected_numeric].max())
        range_values = st.sidebar.slider(
            f"{selected_numeric} Range",
            min_val, max_val, (min_val, max_val)
        )

        # Filter dataframe
        filtered_df = df[
            (df[selected_numeric] >= range_values[0]) &
            (df[selected_numeric] <= range_values[1])
        ]
    else:
        filtered_df = df

    # Visualizations
    st.header("📈 Visualizations")

    # Distribution plot
    if len(numeric_cols) > 0:
        fig_hist = px.histogram(
            filtered_df, x=selected_numeric,
            title=f"Distribution of {selected_numeric}"
        )
        st.plotly_chart(fig_hist, use_container_width=True)

    # Correlation heatmap
    if len(numeric_cols) > 1:
        corr_matrix = filtered_df[numeric_cols].corr()
        fig_corr = px.imshow(
            corr_matrix,
            title="Correlation Matrix",
            color_continuous_scale="RdBu"
        )
        st.plotly_chart(fig_corr, use_container_width=True)

    # Categorical analysis
    categorical_cols = df.select_dtypes(include=['object']).columns
    if len(categorical_cols) > 0:
        selected_cat = st.sidebar.selectbox("Select Categorical Column", categorical_cols)

        fig_bar = px.bar(
            filtered_df[selected_cat].value_counts().head(10),
            title=f"Top 10 {selected_cat} Values"
        )
        st.plotly_chart(fig_bar, use_container_width=True)

    # Data table
    st.header("📋 Data Table")
    st.dataframe(filtered_df.head(100))

    # Download filtered data
    csv = filtered_df.to_csv(index=False)
    st.download_button(
        label="Download Filtered Data as CSV",
        data=csv,
        file_name="filtered_data.csv",
        mime="text/csv"
    )

# To run: streamlit run dashboard.py
```

---

## 🚀 TASK 5: DEPLOY ML MODEL

_Production model deployment with monitoring_

### Model Deployment Pipeline

```python
import pickle
from flask import Flask, request, jsonify
import pandas as pd
import numpy as np
from datetime import datetime
import logging

app = Flask(__name__)

# Load model
def load_model(model_path):
    """Load trained model and preprocessing components"""
    with open(model_path, 'rb') as f:
        model_components = pickle.load(f)
    return model_components

# Model serving endpoint
@app.route('/predict', methods=['POST'])
def predict():
    """API endpoint for model predictions"""
    try:
        # Get input data
        data = request.get_json()

        # Convert to DataFrame
        input_df = pd.DataFrame([data])

        # Load model components
        model_components = load_model('model.pkl')
        model = model_components['model']
        scaler = model_components['scaler']
        feature_columns = model_components['feature_columns']

        # Preprocess input
        input_df = input_df[feature_columns]  # Ensure correct column order
        input_scaled = scaler.transform(input_df)

        # Make prediction
        prediction = model.predict(input_scaled)[0]
        probability = model.predict_proba(input_scaled)[0].max() if hasattr(model, 'predict_proba') else None

        # Log prediction
        logging.info(f"Prediction made: {prediction}, Probability: {probability}")

        # Return response
        response = {
            'prediction': int(prediction) if isinstance(prediction, np.integer) else float(prediction),
            'probability': float(probability) if probability else None,
            'timestamp': datetime.now().isoformat(),
            'model_version': '1.0'
        }

        return jsonify(response)

    except Exception as e:
        logging.error(f"Prediction error: {str(e)}")
        return jsonify({'error': str(e)}), 400

@app.route('/health', methods=['GET'])
def health_check():
    """Health check endpoint"""
    return jsonify({
        'status': 'healthy',
        'timestamp': datetime.now().isoformat(),
        'model_loaded': True
    })

if __name__ == '__main__':
    logging.basicConfig(level=logging.INFO)
    app.run(host='0.0.0.0', port=5000, debug=False)
```

### Docker Deployment

```dockerfile
# Dockerfile for model deployment
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

---

## 💰 TASK 6: MEASURE BUSINESS IMPACT

_ROI calculation and business value measurement_

### Business Impact Framework

```python
class BusinessImpactTracker:
    """Track and measure business impact of data science projects"""

    def __init__(self, project_name, baseline_metrics):
        self.project_name = project_name
        self.baseline_metrics = baseline_metrics
        self.impact_history = []

    def calculate_roi(self, benefits, costs, time_period_months=12):
        """Calculate Return on Investment"""

        total_benefits = sum(benefits.values()) * time_period_months
        total_costs = sum(costs.values())

        roi = ((total_benefits - total_costs) / total_costs) * 100
        payback_period = total_costs / (sum(benefits.values()) or 1)

        print("💰 ROI CALCULATION")
        print(f"Total Benefits (12 months): ${total_benefits:,.2f}")
        print(f"Total Costs: ${total_costs:,.2f}")
        print(f"ROI: {roi:.1f}%")
        print(f"Payback Period: {payback_period:.1f} months")

        return {
            'roi_percentage': roi,
            'payback_months': payback_period,
            'net_benefit': total_benefits - total_costs
        }

    def track_kpi_improvement(self, kpi_name, before_value, after_value):
        """Track KPI improvements"""

        improvement = after_value - before_value
        improvement_pct = (improvement / before_value) * 100 if before_value != 0 else 0

        impact_record = {
            'date': datetime.now(),
            'kpi': kpi_name,
            'before': before_value,
            'after': after_value,
            'improvement': improvement,
            'improvement_pct': improvement_pct
        }

        self.impact_history.append(impact_record)

        print(f"📈 {kpi_name} IMPROVEMENT")
        print(f"Before: {before_value:,.2f}")
        print(f"After: {after_value:,.2f}")
        print(f"Improvement: {improvement:,.2f} ({improvement_pct:+.1f}%)")

        return impact_record

# Example usage
def measure_project_impact():
    """Example of measuring project business impact"""

    tracker = BusinessImpactTracker("Customer Churn Prediction", {
        'monthly_churn_rate': 0.05,
        'customer_acquisition_cost': 100,
        'average_customer_value': 1200
    })

    # Calculate ROI
    benefits = {
        'reduced_churn': 50000,  # Monthly benefit from reduced churn
        'improved_targeting': 20000  # Monthly benefit from better targeting
    }

    costs = {
        'development': 150000,  # One-time development cost
        'infrastructure': 5000,  # Monthly infrastructure cost
        'maintenance': 10000  # Monthly maintenance cost
    }

    roi_result = tracker.calculate_roi(benefits, costs)

    # Track KPI improvements
    tracker.track_kpi_improvement('churn_rate', 0.05, 0.035)  # 5% to 3.5%
    tracker.track_kpi_improvement('customer_lifetime_value', 1200, 1450)

    return tracker
```

---

## ⚡ TASK 7: ADAPTIVE DATA PROCESSING

_Intelligent processing strategy based on data size_

### Adaptive Processing Framework

```python
import psutil
import dask.dataframe as dd

class AdaptiveDataProcessor:
    """Automatically adapt processing strategy based on data size"""

    def __init__(self):
        self.memory_gb = psutil.virtual_memory().total / (1024**3)
        self.strategies = {
            'small': 'pandas',
            'medium': 'dask',
            'large': 'spark'
        }

    def assess_data_size(self, file_path):
        """Assess data size and recommend processing strategy"""

        import os
        file_size_gb = os.path.getsize(file_path) / (1024**3)

        # Sample data to estimate memory usage
        sample_df = pd.read_csv(file_path, nrows=1000)
        sample_memory = sample_df.memory_usage(deep=True).sum()

        # Estimate total memory needed
        with open(file_path, 'r') as f:
            total_lines = sum(1 for _ in f) - 1

        estimated_memory_gb = (sample_memory * total_lines / 1000) / (1024**3)

        # Recommend strategy
        if estimated_memory_gb < self.memory_gb * 0.3:
            strategy = 'pandas'
        elif estimated_memory_gb < self.memory_gb * 0.8:
            strategy = 'dask'
        else:
            strategy = 'spark'

        print(f"📊 DATA ASSESSMENT")
        print(f"File size: {file_size_gb:.2f} GB")
        print(f"Estimated memory: {estimated_memory_gb:.2f} GB")
        print(f"Available memory: {self.memory_gb:.2f} GB")
        print(f"Recommended strategy: {strategy}")

        return strategy, estimated_memory_gb

    def process_with_pandas(self, file_path):
        """Process with pandas for small datasets"""
        print("🐼 Processing with Pandas")
        return pd.read_csv(file_path)

    def process_with_dask(self, file_path):
        """Process with Dask for medium datasets"""
        print("⚡ Processing with Dask")
        return dd.read_csv(file_path)

    def process_with_spark(self, file_path):
        """Process with Spark for large datasets"""
        print("🔥 Processing with Spark")
        try:
            from pyspark.sql import SparkSession
            spark = SparkSession.builder.appName("DataProcessing").getOrCreate()
            return spark.read.csv(file_path, header=True, inferSchema=True)
        except ImportError:
            print("⚠️ Spark not available, falling back to Dask")
            return self.process_with_dask(file_path)

    def adaptive_process(self, file_path):
        """Main method for adaptive processing"""

        strategy, memory_estimate = self.assess_data_size(file_path)

        if strategy == 'pandas':
            return self.process_with_pandas(file_path)
        elif strategy == 'dask':
            return self.process_with_dask(file_path)
        else:
            return self.process_with_spark(file_path)
```

---

## 🔧 TASK 8: OPTIMIZE COSTS & PERFORMANCE

_Automatic resource optimization_

### Cost Monitoring

```python
class CostPerformanceOptimizer:
    """Monitor and optimize costs and performance"""

    def __init__(self, budget_limits):
        self.budget_limits = budget_limits
        self.current_costs = {'compute': 0, 'storage': 0, 'network': 0}

    def monitor_costs(self, cloud_provider='aws'):
        """Monitor current cloud costs"""

        # Simulate cost monitoring (in real implementation, use cloud APIs)
        costs = {
            'compute': np.random.uniform(20, 80),
            'storage': np.random.uniform(5, 25),
            'network': np.random.uniform(2, 15)
        }

        self.current_costs.update(costs)
        total_daily = sum(costs.values())

        print("💰 COST MONITORING")
        print(f"Daily costs: ${total_daily:.2f}")
        print(f"Monthly projection: ${total_daily * 30:.2f}")

        # Check budget alerts
        if total_daily > self.budget_limits.get('daily', 100):
            print("🚨 Daily budget exceeded!")
            self.optimize_costs()

        return costs

    def optimize_costs(self):
        """Automatically optimize costs"""

        optimizations = []

        # Check for over-provisioned resources
        if self.current_costs['compute'] > 50:
            optimizations.append({
                'action': 'scale_down_compute',
                'savings': 20,
                'description': 'Reduce compute instance size'
            })

        # Suggest spot instances
        optimizations.append({
            'action': 'use_spot_instances',
            'savings': 60,
            'description': 'Switch to spot instances for batch jobs'
        })

        print("🎯 COST OPTIMIZATIONS")
        for opt in optimizations:
            print(f"- {opt['description']}: {opt['savings']}% savings")

        return optimizations

    def monitor_performance(self):
        """Monitor system performance"""

        metrics = {
            'cpu_usage': psutil.cpu_percent(),
            'memory_usage': psutil.virtual_memory().percent,
            'latency_ms': np.random.normal(500, 100)  # Simulated
        }

        print("📊 PERFORMANCE METRICS")
        for metric, value in metrics.items():
            print(f"{metric}: {value:.1f}")

        return metrics
```

---

## 🔗 TASK 9: INTEGRATE LEGACY SYSTEMS

_Connect with existing enterprise systems_

### Legacy Database Integration

```python
class LegacySystemIntegrator:
    """Integrate with legacy database systems"""

    def __init__(self, system_type):
        self.system_type = system_type
        self.query_translator = self._get_query_translator()

    def _get_query_translator(self):
        """Get appropriate query translator"""
        if 'oracle' in self.system_type.lower():
            return self._translate_oracle_query
        elif 'db2' in self.system_type.lower():
            return self._translate_db2_query
        else:
            return self._translate_generic_query

    def _translate_oracle_query(self, modern_query):
        """Translate to Oracle-compatible SQL"""
        oracle_query = modern_query.replace('LIMIT', 'AND ROWNUM <=')
        oracle_query = oracle_query.replace('NOW()', 'SYSDATE')
        return oracle_query

    def _translate_db2_query(self, modern_query):
        """Translate to DB2-compatible SQL"""
        db2_query = modern_query.replace('LIMIT', 'FETCH FIRST')
        return db2_query

    def _translate_generic_query(self, modern_query):
        """Generic query translation"""
        return modern_query

    def extract_legacy_data(self, connection_string, query):
        """Extract data from legacy system"""

        print(f"🔗 Connecting to {self.system_type} system")

        # Translate query for legacy system
        legacy_query = self.query_translator(query)

        try:
            import sqlalchemy
            engine = sqlalchemy.create_engine(connection_string)
            df = pd.read_sql(legacy_query, engine)

            print(f"✅ Extracted {len(df)} rows from legacy system")
            return df

        except Exception as e:
            print(f"❌ Legacy system connection failed: {e}")
            return pd.DataFrame()

    def transform_legacy_data(self, df):
        """Transform legacy data to modern format"""

        print("🔄 Transforming legacy data")

        # Handle legacy date formats
        date_columns = df.select_dtypes(include=['object']).columns
        for col in date_columns:
            if 'date' in col.lower():
                try:
                    df[col] = pd.to_datetime(df[col], errors='coerce')
                except:
                    pass

        # Handle legacy encoding
        string_columns = df.select_dtypes(include=['object']).columns
        for col in string_columns:
            try:
                df[col] = df[col].str.encode('latin-1').str.decode('utf-8', errors='ignore')
            except:
                pass

        print("✅ Legacy data transformation completed")
        return df
```

---

## 🎯 USAGE EXAMPLES

### Complete Data Science Workflow

```python
def complete_data_science_workflow(data_file):
    """Example of complete data science workflow using all tasks"""

    print("🚀 STARTING COMPLETE DATA SCIENCE WORKFLOW")
    print("=" * 50)

    # 1. Adaptive data processing
    processor = AdaptiveDataProcessor()
    df = processor.adaptive_process(data_file)

    # 2. Data analysis
    analyzed_df, missing_analysis = analyze_dataset(data_file)

    # 3. Build ML model
    if 'target' in df.columns:
        model, scaler, importance = build_ml_model(df, 'target')

    # 4. Measure business impact
    impact_tracker = measure_project_impact()

    # 5. Create dashboard
    create_data_dashboard(df, "Complete Analysis Dashboard")

    print("✅ Workflow completed successfully!")

    return {
        'data': df,
        'model': model if 'target' in df.columns else None,
        'impact': impact_tracker,
        'analysis': missing_analysis
    }

# Run complete workflow
# result = complete_data_science_workflow('your_data.csv')
```

---

## 📚 QUICK REFERENCE

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
*optimize-costs       # Cost and performance optimization

# Modes
*mode-engineering     # Data engineering focus
*mode-analysis        # Analysis and BI focus
*mode-science         # ML and AI focus
*mode-production      # Production and deployment focus
```

### Best Practices

1. **Always handle errors** - Use try-catch blocks and logging
2. **Start with data quality** - Check for missing values and outliers
3. **Validate assumptions** - Test statistical assumptions before modeling
4. **Monitor in production** - Track model performance and business metrics
5. **Document everything** - Maintain clear documentation for reproducibility

---

_This consolidated guide contains all essential data science tasks for TonyFunkman. Each task is production-ready with error handling, best practices, and real-world examples._
