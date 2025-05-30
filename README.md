# Blinkit-Analysis-Using-Python

#!/usr/bin/env python
# coding: utf-8

# ## Data Analysis Python Project - Blinkit Analysis

# #### Import Libraries

# In[1]:


import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns


# #### Import Raw Data

# In[2]:


df = pd.read_csv("blinkit_data.csv")


# #### Sample Data

# In[3]:


df.head(5)


# In[4]:


df.tail(5)


# #### Size of  Data

# In[5]:


print("Size of Data :", df.shape)


# #### Field Info

# In[6]:


df.info()


# #### Data Cleaning

# In[7]:


print(df["Item Fat Content"].unique())


# In[8]:


df['Item Fat Content'] = df['Item Fat Content'].replace({'LF': 'Low Fat', 'low fat': 'Low Fat', 'reg': 'Regular'})


# In[9]:


print(df["Item Fat Content"].unique())


# #### Business Requirements
# 
# #### KPI's Requirements

# In[10]:


#Total Sales
Total_sales = df['Sales'].sum()

#Average Sales
Avg_sales = df['Sales'].mean()

#Number of items sold
No_of_items_sold = df['Sales'].count()

#Average ratings
Avg_ratings = df['Rating'].mean()

#Display KPI's

print(f"Total sales: ${Total_sales:,.1f}")
print(f"Average sales: ${Avg_sales:,.0f}")
print(f"No of items sold: ${No_of_items_sold:,.0f}")
print(f"Average ratings: ${Avg_ratings:,.1f}")


# ## Charts Requirements

# #### Total Sales by Fat Content

# In[11]:


sales_by_fat = df['Item Fat Content'].value_counts()


# In[12]:


sales_by_fat


# In[13]:


# Plotting the pie chart
plt.figure(figsize=(6,6))
plt.pie(sales_by_fat, labels=sales_by_fat.index, autopct='%1.0f%%', startangle=90, colors=['skyblue', 'lightcoral'])
plt.title('Sales By Fat Content')
plt.axis('equal')  # Equal aspect ratio ensures the pie chart is circular.
plt.show()


# #### Total Sales By Item Type

# In[14]:


print(df["Item Type"].unique())


# In[15]:


# Group by Item Type and sum the sales
sales_by_item_type = df.groupby('Item Type')['Sales'].sum().sort_values(ascending=False)


# In[16]:


sales_by_item_type


# In[17]:


# Group and sum sales
sales_by_item_type = df.groupby('Item Type')['Sales'].sum().sort_values(ascending=False)

# Plotting
fig, ax = plt.subplots(figsize=(12, 6))
bars = ax.bar(sales_by_item_type.index, sales_by_item_type.values, color='darkblue')

# Add value labels on top of each bar
for bar in bars:
    height = bar.get_height()
    ax.text(bar.get_x() + bar.get_width()/2, height + 100, f'{height:.0f}', 
            ha='center', va='bottom', fontsize=9)

# Labels and title
ax.set_title('Total Sales by Item Type')
ax.set_xlabel('Item Type')
ax.set_ylabel('Sales')
plt.xticks(rotation=90, ha='right')
plt.tight_layout()
plt.show()


# #### Fat Content by Outlet for Total Sales

# In[18]:


print(df["Outlet Type"].unique())


# In[19]:


# Step 1: Aggregate total sales by Outlet Location Type and Item Fat Content
grouped = df.groupby(['Outlet Location Type', 'Item Fat Content'])['Sales'].sum().unstack(fill_value=0)

# Step 2: Plot grouped (side-by-side) bars
labels = grouped.index
low_fat = grouped['Low Fat']
regular = grouped['Regular']

x = np.arange(len(labels))  # the label locations
bar_width = 0.35

fig, ax = plt.subplots(figsize=(10, 6))
bar1 = ax.bar(x - bar_width/2, low_fat, bar_width, label='Low Fat', color='skyblue')
bar2 = ax.bar(x + bar_width/2, regular, bar_width, label='Regular', color='salmon')

# Add value labels on bars
for bars in [bar1, bar2]:
    for bar in bars:
        height = bar.get_height()
        ax.text(bar.get_x() + bar.get_width()/2, height + 100, f'{int(height)}',
                ha='center', va='bottom', fontsize=9)

# Final touches
ax.set_xlabel('Outlet Location Type')
ax.set_ylabel('Total Sales')
ax.set_title('Total Sales by Outlet Location Type and Item Fat Content')
ax.set_xticks(x)
ax.set_xticklabels(labels)
ax.legend(title='Item Fat Content')
plt.tight_layout()
plt.show()


# #### Total Sales by Outlet Establishment

# In[20]:


print(df["Outlet Establishment Year"].unique())


# In[21]:


# Group sales by year
sales_by_year = df.groupby('Outlet Establishment Year')['Sales'].sum().sort_index()

# Plotting
plt.figure(figsize=(10, 6))
plt.plot(sales_by_year.index, sales_by_year.values, marker='o', linestyle='-', color='teal')

# Annotate values on the line
for x, y in zip(sales_by_year.index, sales_by_year.values):
    plt.text(x, y + 500, f'{y:,.0f}', ha='center', va='bottom', fontsize=9)

# Labels and title
plt.title('Total Sales by Outlet Establishment Year')
plt.xlabel('Outlet Establishment Year')
plt.ylabel('Total Sales')
plt.grid(False)
plt.tight_layout()
plt.show()


# #### Sales by Outlet Size

# In[22]:


# Plotting the pie chart
Sales_by_outlet_size = df.groupby('Outlet Size')['Sales'].sum()
plt.figure(figsize=(6,6))
plt.pie(Sales_by_outlet_size, labels=Sales_by_outlet_size.index, autopct='%1.1f%%', startangle=90, colors=['skyblue', 'lightcoral', 'green'])
plt.title('Sales By outlet size')
plt.axis('equal')  # Equal aspect ratio ensures the pie chart is circular.
plt.tight_layout()
plt.show()


# #### Sales by Outlet Location

# In[23]:


df.head()


# In[24]:


# Group total sales by Outlet Location Type
sales_by_location = df.groupby('Outlet Location Type')['Sales'].sum()

# Sort for better visuals (optional)
sales_by_location = sales_by_location.sort_values()

# Plot horizontal bar chart
plt.figure(figsize=(8, 6))
bars = plt.barh(sales_by_location.index, sales_by_location.values, color='violet')

# Add value labels to bars
for bar in bars:
    plt.text(bar.get_width() + 100, bar.get_y() + bar.get_height()/2,
             f'{int(bar.get_width())}', va='center', fontsize=9)

# Labels and title
plt.xlabel('Total Sales')
plt.ylabel('Outlet Location Type')
plt.title('Total Sales by Outlet Location Type (Horizontal Bar Chart)')
plt.tight_layout()
plt.show()
