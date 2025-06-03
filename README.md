## Data Analysis Python Project - Blinkit Analysis

#### Import Libraries


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

#### Import Raw Data


```python
df = pd.read_csv("blinkit_data.csv")
```

#### Sample Data


```python
df.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Fat Content</th>
      <th>Item Identifier</th>
      <th>Item Type</th>
      <th>Outlet Establishment Year</th>
      <th>Outlet Identifier</th>
      <th>Outlet Location Type</th>
      <th>Outlet Size</th>
      <th>Outlet Type</th>
      <th>Item Visibility</th>
      <th>Item Weight</th>
      <th>Sales</th>
      <th>Rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Regular</td>
      <td>FDX32</td>
      <td>Fruits and Vegetables</td>
      <td>2012</td>
      <td>OUT049</td>
      <td>Tier 1</td>
      <td>Medium</td>
      <td>Supermarket Type1</td>
      <td>0.100014</td>
      <td>15.10</td>
      <td>145.4786</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Low Fat</td>
      <td>NCB42</td>
      <td>Health and Hygiene</td>
      <td>2022</td>
      <td>OUT018</td>
      <td>Tier 3</td>
      <td>Medium</td>
      <td>Supermarket Type2</td>
      <td>0.008596</td>
      <td>11.80</td>
      <td>115.3492</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Regular</td>
      <td>FDR28</td>
      <td>Frozen Foods</td>
      <td>2010</td>
      <td>OUT046</td>
      <td>Tier 1</td>
      <td>Small</td>
      <td>Supermarket Type1</td>
      <td>0.025896</td>
      <td>13.85</td>
      <td>165.0210</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Regular</td>
      <td>FDL50</td>
      <td>Canned</td>
      <td>2000</td>
      <td>OUT013</td>
      <td>Tier 3</td>
      <td>High</td>
      <td>Supermarket Type1</td>
      <td>0.042278</td>
      <td>12.15</td>
      <td>126.5046</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Low Fat</td>
      <td>DRI25</td>
      <td>Soft Drinks</td>
      <td>2015</td>
      <td>OUT045</td>
      <td>Tier 2</td>
      <td>Small</td>
      <td>Supermarket Type1</td>
      <td>0.033970</td>
      <td>19.60</td>
      <td>55.1614</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.tail(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Fat Content</th>
      <th>Item Identifier</th>
      <th>Item Type</th>
      <th>Outlet Establishment Year</th>
      <th>Outlet Identifier</th>
      <th>Outlet Location Type</th>
      <th>Outlet Size</th>
      <th>Outlet Type</th>
      <th>Item Visibility</th>
      <th>Item Weight</th>
      <th>Sales</th>
      <th>Rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8518</th>
      <td>low fat</td>
      <td>NCT53</td>
      <td>Health and Hygiene</td>
      <td>1998</td>
      <td>OUT027</td>
      <td>Tier 3</td>
      <td>Medium</td>
      <td>Supermarket Type3</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>164.5526</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>8519</th>
      <td>low fat</td>
      <td>FDN09</td>
      <td>Snack Foods</td>
      <td>1998</td>
      <td>OUT027</td>
      <td>Tier 3</td>
      <td>Medium</td>
      <td>Supermarket Type3</td>
      <td>0.034706</td>
      <td>NaN</td>
      <td>241.6828</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>8520</th>
      <td>low fat</td>
      <td>DRE13</td>
      <td>Soft Drinks</td>
      <td>1998</td>
      <td>OUT027</td>
      <td>Tier 3</td>
      <td>Medium</td>
      <td>Supermarket Type3</td>
      <td>0.027571</td>
      <td>NaN</td>
      <td>86.6198</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>8521</th>
      <td>reg</td>
      <td>FDT50</td>
      <td>Dairy</td>
      <td>1998</td>
      <td>OUT027</td>
      <td>Tier 3</td>
      <td>Medium</td>
      <td>Supermarket Type3</td>
      <td>0.107715</td>
      <td>NaN</td>
      <td>97.8752</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>8522</th>
      <td>reg</td>
      <td>FDM58</td>
      <td>Snack Foods</td>
      <td>1998</td>
      <td>OUT027</td>
      <td>Tier 3</td>
      <td>Medium</td>
      <td>Supermarket Type3</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>112.2544</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>



#### Size of  Data


```python
print("Size of Data :", df.shape)
```

    Size of Data : (8523, 12)
    

#### Field Info


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 8523 entries, 0 to 8522
    Data columns (total 12 columns):
     #   Column                     Non-Null Count  Dtype  
    ---  ------                     --------------  -----  
     0   Item Fat Content           8523 non-null   object 
     1   Item Identifier            8523 non-null   object 
     2   Item Type                  8523 non-null   object 
     3   Outlet Establishment Year  8523 non-null   int64  
     4   Outlet Identifier          8523 non-null   object 
     5   Outlet Location Type       8523 non-null   object 
     6   Outlet Size                8523 non-null   object 
     7   Outlet Type                8523 non-null   object 
     8   Item Visibility            8523 non-null   float64
     9   Item Weight                7060 non-null   float64
     10  Sales                      8523 non-null   float64
     11  Rating                     8523 non-null   float64
    dtypes: float64(4), int64(1), object(7)
    memory usage: 799.2+ KB
    

#### Data Cleaning


```python
print(df["Item Fat Content"].unique())
```

    ['Regular' 'Low Fat' 'low fat' 'LF' 'reg']
    


```python
df['Item Fat Content'] = df['Item Fat Content'].replace({'LF': 'Low Fat', 'low fat': 'Low Fat', 'reg': 'Regular'})
```


```python
print(df["Item Fat Content"].unique())
```

    ['Regular' 'Low Fat']
    

#### Business Requirements

#### KPI's Requirements


```python
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
```

    Total sales: $1,201,681.5
    Average sales: $141
    No of items sold: $8,523
    Average ratings: $4.0
    

## Charts Requirements

#### Total Sales by Fat Content


```python
sales_by_fat = df['Item Fat Content'].value_counts()
```


```python
sales_by_fat
```




    Item Fat Content
    Low Fat    5517
    Regular    3006
    Name: count, dtype: int64




```python
# Plotting the pie chart
plt.figure(figsize=(6,6))
plt.pie(sales_by_fat, labels=sales_by_fat.index, autopct='%1.0f%%', startangle=90, colors=['skyblue', 'lightcoral'])
plt.title('Sales By Fat Content')
plt.axis('equal')  # Equal aspect ratio ensures the pie chart is circular.
plt.show()
```


    
![png](https://github.com/RatneshRavindra/Blinkit-Analysis-Using-Python/blob/ded2bfd277555ea1060207bfdeaaa8dc74240fa5/Sales%20by%20fat%20content.png)
    


#### Total Sales By Item Type


```python
print(df["Item Type"].unique())
```

    ['Fruits and Vegetables' 'Health and Hygiene' 'Frozen Foods' 'Canned'
     'Soft Drinks' 'Household' 'Snack Foods' 'Meat' 'Breads' 'Hard Drinks'
     'Others' 'Dairy' 'Breakfast' 'Baking Goods' 'Seafood' 'Starchy Foods']
    


```python
# Group by Item Type and sum the sales
sales_by_item_type = df.groupby('Item Type')['Sales'].sum().sort_values(ascending=False)
```


```python
sales_by_item_type
```




    Item Type
    Fruits and Vegetables    178124.0810
    Snack Foods              175433.9204
    Household                135976.5254
    Frozen Foods             118558.8814
    Dairy                    101276.4596
    Canned                    90706.7270
    Baking Goods              81894.7364
    Health and Hygiene        68025.8388
    Meat                      59449.8638
    Soft Drinks               58514.1650
    Breads                    35379.1198
    Hard Drinks               29334.6766
    Others                    22451.8916
    Starchy Foods             21880.0274
    Breakfast                 15596.6966
    Seafood                    9077.8700
    Name: Sales, dtype: float64




```python
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
```


    
![png](https://github.com/RatneshRavindra/Blinkit-Analysis-Using-Python/blob/ded2bfd277555ea1060207bfdeaaa8dc74240fa5/Total%20sales%20by%20item%20type.png)
    


#### Fat Content by Outlet for Total Sales


```python
print(df["Outlet Type"].unique())
```

    ['Supermarket Type1' 'Supermarket Type2' 'Grocery Store'
     'Supermarket Type3']
    


```python
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
```


    
![png](https://github.com/RatneshRavindra/Blinkit-Analysis-Using-Python/blob/ded2bfd277555ea1060207bfdeaaa8dc74240fa5/Total%20sales%20by%20outlet%20location%20type%20and%20item%20fat%20content.png)
    


#### Total Sales by Outlet Establishment


```python
print(df["Outlet Establishment Year"].unique())
```

    [2012 2022 2010 2000 2015 2020 2011 1998 2017]
    


```python
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
```


    
![png](https://github.com/RatneshRavindra/Blinkit-Analysis-Using-Python/blob/ded2bfd277555ea1060207bfdeaaa8dc74240fa5/Total%20sales%20by%20outlet%20establishment%20year.png)
    


#### Sales by Outlet Size


```python
# Plotting the pie chart
Sales_by_outlet_size = df.groupby('Outlet Size')['Sales'].sum()
plt.figure(figsize=(6,6))
plt.pie(Sales_by_outlet_size, labels=Sales_by_outlet_size.index, autopct='%1.1f%%', startangle=90, colors=['skyblue', 'lightcoral', 'green'])
plt.title('Sales By outlet size')
plt.axis('equal')  # Equal aspect ratio ensures the pie chart is circular.
plt.tight_layout()
plt.show()
```


    
![png](https://github.com/RatneshRavindra/Blinkit-Analysis-Using-Python/blob/ded2bfd277555ea1060207bfdeaaa8dc74240fa5/Sales%20by%20outlet%20size.png)
    


#### Sales by Outlet Location


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Fat Content</th>
      <th>Item Identifier</th>
      <th>Item Type</th>
      <th>Outlet Establishment Year</th>
      <th>Outlet Identifier</th>
      <th>Outlet Location Type</th>
      <th>Outlet Size</th>
      <th>Outlet Type</th>
      <th>Item Visibility</th>
      <th>Item Weight</th>
      <th>Sales</th>
      <th>Rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Regular</td>
      <td>FDX32</td>
      <td>Fruits and Vegetables</td>
      <td>2012</td>
      <td>OUT049</td>
      <td>Tier 1</td>
      <td>Medium</td>
      <td>Supermarket Type1</td>
      <td>0.100014</td>
      <td>15.10</td>
      <td>145.4786</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Low Fat</td>
      <td>NCB42</td>
      <td>Health and Hygiene</td>
      <td>2022</td>
      <td>OUT018</td>
      <td>Tier 3</td>
      <td>Medium</td>
      <td>Supermarket Type2</td>
      <td>0.008596</td>
      <td>11.80</td>
      <td>115.3492</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Regular</td>
      <td>FDR28</td>
      <td>Frozen Foods</td>
      <td>2010</td>
      <td>OUT046</td>
      <td>Tier 1</td>
      <td>Small</td>
      <td>Supermarket Type1</td>
      <td>0.025896</td>
      <td>13.85</td>
      <td>165.0210</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Regular</td>
      <td>FDL50</td>
      <td>Canned</td>
      <td>2000</td>
      <td>OUT013</td>
      <td>Tier 3</td>
      <td>High</td>
      <td>Supermarket Type1</td>
      <td>0.042278</td>
      <td>12.15</td>
      <td>126.5046</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Low Fat</td>
      <td>DRI25</td>
      <td>Soft Drinks</td>
      <td>2015</td>
      <td>OUT045</td>
      <td>Tier 2</td>
      <td>Small</td>
      <td>Supermarket Type1</td>
      <td>0.033970</td>
      <td>19.60</td>
      <td>55.1614</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
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
```


    
![png](https://github.com/RatneshRavindra/Blinkit-Analysis-Using-Python/blob/ded2bfd277555ea1060207bfdeaaa8dc74240fa5/Total%20sales%20by%20outlet%20location%20type.png)
    

