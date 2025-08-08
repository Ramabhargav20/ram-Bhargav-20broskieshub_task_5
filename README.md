# ram-Bhargav-20broskieshub_task_5
#data analysis on CSV files.
#analyze sales data using pandas.
#using tools python ,vs code>
#hints/mini guide:load CSV using pandas.
#use GROUPBY(), SUM(),PLOT().

# Step 1: Import libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Step 2: Load CSV
df = pd.read_csv('sales_data.csv')  # replace with your file path

# Step 3: Preview data
print(df.head())
print(df.info())

# Step 4: Add 'Sales' column
df['Sales'] = df['Quantity'] * df['Price']

# Step 5: Total Sales Overview
total_sales = df['Sales'].sum()
print(f"Total Sales: ${total_sales:.2f}")

# Step 6: Sales by Product
sales_by_product = df.groupby('Product')['Sales'].sum().sort_values(ascending=False)
print(sales_by_product)

# Plot Sales by Product
plt.figure(figsize=(10, 6))
sales_by_product.plot(kind='bar', color='skyblue')
plt.title('Sales by Product')
plt.ylabel('Sales ($)')
plt.xlabel('Product')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Step 7: Sales by Category
sales_by_category = df.groupby('Category')['Sales'].sum()
print(sales_by_category)

# Step 8: Monthly Trends (if date column exists)
df['Date'] = pd.to_datetime(df['Date'])
df['Month'] = df['Date'].dt.to_period('M')
monthly_sales = df.groupby('Month')['Sales'].sum()

# Plot Monthly Sales
monthly_sales.plot(kind='line', marker='o')
plt.title('Monthly Sales Trend')
plt.ylabel('Sales ($)')
plt.xlabel('Month')
plt.grid(True)
plt.tight_layout()
plt.show()

# Step 9: Region-wise Sales
region_sales = df.groupby('Region')['Sales'].sum()
region_sales.plot(kind='pie', autopct='%1.1f%%', figsize=(6, 6))
plt.title('Sales by Region')
plt.ylabel('')
plt.tight_layout()
plt.show()


