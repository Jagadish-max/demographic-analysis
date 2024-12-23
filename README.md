# demographic-analysis
import pandas as pd
order_details = pd.read_excel(r"C:\Users\91789\\Downloads\\order_details.xlsx")
order_details
order_details.isnull().sum()
order_details.dropna()
cooking_sessions=pd.read_excel(r"C:\Users\91789\\Downloads\\cooking_sessions.xlsx")
cooking_sessions
cooking_sessions.isnull().sum()
cooking_sessions.drop_duplicates()
user_details=pd.read_excel(r"C:\Users\91789\\Downloads\\user_details.xlsx")
user_details
merged_data = pd.merge(cooking_sessions, order_details, on="User ID", how="inner")
merged_data
popular_dishes = order_details['Dish Name'].value_counts().head(10)
popular_dishes
import matplotlib.pyplot as plt
popular_dishes.plot(kind='bar',color='red',figsize=(10,5))
plt.title("Top Dishes")
plt.xlabel("Dish Name")
plt.ylabel("Number of Orders")
plt.show()
location=final_data['Location'].value_counts()
location
Spaghetti_max=final_data[final_data['Dish Name_x']=='Spaghetti']
Spaghetti_max
location_counts = Spaghetti_max['Location'].value_counts()
location_counts
age_order_counts=final_data.groupby('Age')['Order ID'].count()
age_order_counts
#grouping by age and counting no of orders
import matplotlib.pyplot as plt
age_order_counts.plot(kind='ba',color='green',figsize=(10,10))
plt.title('Orders by Age')
plt.xlabel('Age')
plt.ylabel('Number of Orders')
plt.show()
combined_analysis = final_data.groupby(['Age','Location'])['Order ID'].count().reset_index()

combined_analysis = combined_analysis.sort_values(['Age','Location'])

print("Combined Analysis:")
print(combined_analysis)

combined_pivot = combined_analysis.pivot_table(values='Order ID', index=['Age'], columns=['Location'], fill_value=0)

import seaborn as sns

plt.figure(figsize=(12, 8))
sns.heatmap(combined_pivot, annot=True,cmap="coolwarm")
plt.title("Orders by Age,Location")
plt.xlabel("Location")
plt.ylabel("Age")
plt.show()
