# Housing-price-prediction

Sure! Below is a simple README file template for your project, which includes the steps and descriptions along with expected outputs (such as images/plots).

---

# House Prices Analysis Project

## Overview

This project involves exploring and analyzing a dataset of house prices, with the objective of cleaning the data, visualizing key trends, and understanding the relationships between different features and house prices. It includes tasks such as handling missing values, encoding categorical variables, and visualizing the distribution of key features such as the number of bedrooms and the average house price by the number of bedrooms.

## Files Included

1. **house_prices.csv** - The dataset containing house prices and various features related to each property.
2. **house_price_analysis.py** - Python script for performing data analysis, cleaning, and visualizations.

## Output

## Steps 

### 1. Data Loading and Initial Exploration

First, the dataset is loaded and basic exploration is done to understand the structure of the data, including checking for missing values and statistical summaries.


```python
print(df.head())  # Display the first 5 rows of the dataset
print(df.info())  # Dataset structure and types
print(df.describe())  # Descriptive statistics
```

### 2. Handling Missing Values

The script drops rows where the target value (SalePrice) is missing and fills missing numeric values with the mean of the column. Categorical columns have missing values filled with the mode.

### 3. Encoding Categorical Variables

Categorical variables are encoded using one-hot encoding (via `pd.get_dummies`) to convert them into numerical features for modeling.

```python
df = pd.get_dummies(df, drop_first=True)
```

### 4. Inspecting Rows with Erroneous Bedroom Data

The analysis identifies rows where the number of bedrooms (`Bedroom AbvGr`) is 0, which might indicate erroneous data. These rows are removed from the dataset.


```python
print(df[df['Bedroom AbvGr'] == 0])  # Inspect rows with 0 bedrooms
df_cleaned = df[df['Bedroom AbvGr'] > 0]  # Clean data
```

### 5. Plotting the Distribution of the Number of Bedrooms

A histogram is generated to show the distribution of the number of bedrooms in the dataset.

```python
plt.figure(figsize=(10, 6))
sns.histplot(df['Bedroom AbvGr'], bins=range(0, df['Bedroom AbvGr'].max() + 1), kde=False)
plt.title('Distribution of Number of Bedrooms')
plt.xlabel('Number of Bedrooms')
plt.ylabel('Frequency')
plt.show()
```

### 6. Average House Prices by Number of Bedrooms

A bar plot is created to show the average house price (`SalePrice`) for each number of bedrooms.


```python
plt.figure(figsize=(12, 8))
sns.barplot(x=df_cleaned['Bedroom AbvGr'], y=df_cleaned['SalePrice'], estimator=np.mean, palette='viridis')
plt.title('Average House Prices by Number of Bedrooms (Cleaned Data)', fontsize=16, fontweight='bold')
plt.xlabel('Number of Bedrooms', fontsize=12)
plt.ylabel('Average SalePrice', fontsize=12)
plt.xticks(fontsize=10)
plt.yticks(fontsize=10)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()
```

**Expected Output Image**:

![Average House Prices by Number of Bedrooms](output_images/average_house_price_by_bedrooms.png)

### 7. Top Features Correlated with SalePrice

A correlation matrix is computed to identify the top 10 features most strongly correlated with the target variable `SalePrice`. A bar plot visualizes these features.

**Output**: A bar plot showing the top 10 features correlated with house price.

```python
correlation_matrix = df.corr()
top_features = correlation_matrix['SalePrice'].abs().sort_values(ascending=False).index[1:11]
plt.figure(figsize=(12, 8))
top_feature_corr = correlation_matrix.loc[top_features, 'SalePrice']
sns.barplot(x=top_feature_corr.values, y=top_feature_corr.index, palette='viridis')
plt.title('Top 10 Features Correlated with SalePrice', fontsize=16, fontweight='bold')
plt.xlabel('Correlation with SalePrice', fontsize=12)
plt.ylabel('Features', fontsize=12)
plt.grid(axis='x', linestyle='--', alpha=0.7)
plt.show()
```

## Installation

1. Clone the repository or download the project folder.
2. Install the required libraries:

```bash
pip install pandas numpy matplotlib seaborn
```

3. Run the script:

```bash
python house_price_analysis.py
```

## Conclusion

This project provides insights into the house pricing data by cleaning, visualizing, and analyzing key features. The generated plots help understand the distribution of house prices, the impact of bedrooms on pricing, and the most influential features for house pricing.

--- 


