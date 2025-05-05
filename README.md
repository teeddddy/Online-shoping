# Online-shoping
# Directory structure for the project:
# online-shopping-analysis/
# ├── data/
# ├── notebooks/
# │   └── analysis_notebook.ipynb
# ├── visualizations/
# │   ├── purchase_by_age_gender.py
# │   ├── purchase_trends_over_time.py
# │   └── feature_correlation_heatmap.py
# ├── data_preprocessing.py
# ├── eda_analysis.py
# ├── customer_behavior.py
# └── README.md

# File: data_preprocessing.py
import pandas as pd

def load_and_clean_data(filepath):
    df = pd.read_csv(filepath)
    df.dropna(inplace=True)
    df['Age'] = df['Age'].astype(int)
    df['Gender'] = df['Gender'].astype('category')
    df['Purchase_Amount'] = df['Purchase_Amount'].astype(float)
    return df

# File: eda_analysis.py
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

def show_basic_stats(df):
    print(df.describe())
    print(df['Gender'].value_counts())

def correlation_heatmap(df):
    plt.figure(figsize=(10, 6))
    sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
    plt.title('Correlation Heatmap')
    plt.show()

# File: customer_behavior.py
import pandas as pd

def segment_by_age_gender(df):
    return df.groupby(['Age', 'Gender'])['Purchase_Amount'].mean().reset_index()

# File: visualizations/purchase_by_age_gender.py
import seaborn as sns
import matplotlib.pyplot as plt

def plot_purchase_by_age_gender(df):
    sns.barplot(x='Age', y='Purchase_Amount', hue='Gender', data=df)
    plt.title('Average Purchase by Age and Gender')
    plt.show()

# File: visualizations/purchase_trends_over_time.py
import pandas as pd
import matplotlib.pyplot as plt

def plot_monthly_trends(df):
    df['Purchase_Date'] = pd.to_datetime(df['Purchase_Date'])
    df.set_index('Purchase_Date', inplace=True)
    monthly = df['Purchase_Amount'].resample('M').sum()
    monthly.plot(kind='line', figsize=(12, 6))
    plt.title('Monthly Purchase Trends')
    plt.ylabel('Total Purchase Amount')
    plt.show()

# File: visualizations/feature_correlation_heatmap.py
import seaborn as sns
import matplotlib.pyplot as plt

def plot_feature_heatmap(df):
    sns.heatmap(df.corr(), annot=True, cmap='viridis')
    plt.title('Feature Correlation Heatmap')
    plt.show()
