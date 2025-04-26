# Sales_Analysis_for_an_Automobile_Company_USA-
A Data Science Project that Analysed  the sales performance of an Automobile company Based in the United States. The company’s sales transaction data generated over the past years was used for this  analysis.

## PROBLEM STATEMENT: 

#### What are the Top Most-Profitable 5 States for a Bike business in the United State ?

## DATA PRE-PROCESSING

## DATA LOADING

```Python
#import the 3 neccessary python packages 
# solution 

import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt

print ("imported")
```

```Python
#Reading the sales data in to the pandas data frame (df)

#syntax for reading:  pd.read_csv

bikes_df =  pd.read_csv("C:/Users/HP/Desktop/_EXCLUSIVE DATA SCIENCE BOOT CAMP_STUDENT FOLDER/DATA_SET/bikess.csv")

bikes_df.head()
```

![DATA LOADING](https://github.com/user-attachments/assets/ae7d832d-fb35-4a3b-9281-423fd5c26e13)

#### DATA MODIFICATION

```python
# (1). Adding the following 3 columns to your pansdas Dataframe:  bikes_df



# TotalCostPrice : To be obtained by (OrderQuantity x CostPrice_usd)


bikes_df["TotalCostPrice"] = bikes_df["OrderQuantity"] * bikes_df["CostPrice_usd"] 


# SalesRevenue : To be obtained by (OrderQuantity x SellingPrice_usd)


bikes_df["SalesRevenue"] = bikes_df["OrderQuantity"] * bikes_df["SellingPrice_usd"] 



# Profit : To be obtained by (SalesRevenue - TotalCostPrice)



bikes_df["Profit"] = bikes_df["SalesRevenue"] - bikes_df["TotalCostPrice"]


bikes_df.head()

```
![DATA MODIFICATION](https://github.com/user-attachments/assets/c59607f2-e8fa-49bc-af44-4e72d13a29af)


## DATA ANALYSIS 

#### DATA FILTERING

```python
# filtering out only the data relevant to solving the problem statement.

Is_US= bikes_df["CustomerCountry"] == "United States"
Is_Bike= bikes_df["ProductCategory"]=="Bikes"
Bike_US= bikes_df[(Is_US)& (Is_Bike)]
Bike_US.head()
```

![DATA FILTERING](https://github.com/user-attachments/assets/572fbbe7-3d90-4fab-916a-72c84c8a259d)

#### DATA AGGREGATION
```python
Bike_US.pivot_table(values= "Profit", index= "CustomerState", aggfunc= np.sum)
Total_profit_by_state =Bike_US.pivot_table(values= "Profit", index= "CustomerState", aggfunc= np.sum)
Total_profit_by_state
```

![DATA AGGREGATION](https://github.com/user-attachments/assets/c0484b1f-c7b1-449c-842a-d3b83fdae669)

#### DATA SORTING OF AGGREGATED VALUES

```python
#sorting the aggregated data in order to rank the state according to the top most profitable states in united state

Total_profit_by_state.sort_values(by= "Profit", ascending = False)
```
![DATA SORTING OF AGGREGATED VALUES](https://github.com/user-attachments/assets/7ea8354b-3685-441b-8be3-ec1a5ba2a33d)

#### RESULT BY RANKING
```python
# The top Most-Profitable 5 States for a Bike business in the United State 

top_5_states= Total_profit_by_state.sort_values(by= "Profit", ascending = False).head(5)
top_5_states
```

![RESULT BY RANKING](https://github.com/user-attachments/assets/c8fe8950-0ed7-4c06-9010-d5b85cfbab11)

## DATA VISUALIZATION 
```python
#visualizing the result 
plt.figure(figsize=(10, 6))
top_5_states.plot(kind= "bar", title= "The Top Most Profitable 5 State for Bike Product in the USA")

#adding tittle and lable to the plot 
plt.ylabel("Total Profit in Million Dollars")
plt.xlabel("States")
#showing the plot
plt.show()
```
![PROJECT_ONE_SCREENSHOT](https://github.com/user-attachments/assets/8899fbbf-6839-4376-8cf0-9969cb56deed)

