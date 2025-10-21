

[1]
0s
import pandas as pd

[4]
file_path = "Superstore.csv"

[5]
0s
df = pd.read_csv(file_path)
display(df.head())


[6]
0s
display(df.isnull().sum())


[8]
0s
# Identify outliers using IQR
Q1 = df['Sales'].quantile(0.25)
Q3 = df['Sales'].quantile(0.75)
IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

outliers = df[(df['Sales'] < lower_bound) | (df['Sales'] > upper_bound)]

print(f"Number of outliers in 'Sales' column: {len(outliers)}")
display(outliers.head())


[9]
0s
import numpy as np

df['Sales_log'] = np.log1p(df['Sales'])
display(df[['Sales', 'Sales_log']].head())


[10]
0s
# Convert date columns to datetime objects
df['Order.Date'] = pd.to_datetime(df['Order.Date'])
df['Ship.Date'] = pd.to_datetime(df['Ship.Date'])

# Extract date features
df['Order_Year'] = df['Order.Date'].dt.year
df['Order_Month'] = df['Order.Date'].dt.month
df['Order_Day'] = df['Order.Date'].dt.day
df['Ship_Year'] = df['Ship.Date'].dt.year
df['Ship_Month'] = df['Ship.Date'].dt.month
df['Ship_Day'] = df['Ship.Date'].dt.day

display(df[['Order.Date', 'Order_Year', 'Order_Month', 'Order_Day', 'Ship.Date', 'Ship_Year', 'Ship_Month', 'Ship_Day']].head())

[11]
0s
df = pd.get_dummies(df, columns=['Category', 'Segment', 'Ship.Mode'])
display(df.head())

[12]
0s
unique_cities = df['City'].unique()
print(f"Number of unique cities: {len(unique_cities)}")
display(unique_cities)

[13]
# Assuming there is a 'Price per Item' that is not explicitly given,
# check for potential issues by checking relationship between these columns.

# Let's calculate a simplified 'effective price per item' and see its distribution.
df['Effective_Price_Per_Item'] = df['Sales'] / df['Quantity']

[ ]


[15]
0s
display(df[['Profit', 'Quantity', 'Shipping.Cost']].describe())

[16]
1s
# Save the cleaned DataFrame to a CSV file
cleaned_file_path = "Superstore_cleaned.csv"
df.to_csv(cleaned_file_path, index=False)

print(f"Cleaned data saved to {cleaned_file_path}")
Cleaned data saved to Superstore_cleaned.csv
df = pd.read_csv(file_path) iris_df.head()
# ANN
