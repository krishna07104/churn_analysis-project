

---

#  Customer Churn Analysis

This project analyzes customer churn data to identify key patterns influencing churn behavior. The analysis involves **data cleaning, exploration, and visualization using Python libraries**.

---

##  **Requirements**

```bash
pip install pandas
pip install matplotlib
pip install seaborn
pip install numpy
```

---

##  **Import Libraries**

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
```

---

##  **Load Dataset**

```python
churn_analysis = pd.read_csv("customer churn.csv")
churn_analysis.head()
```

---

##  **Data Cleaning**

### Replace empty strings in `TotalCharges` with 0 and convert to float:

```python
df['TotalCharges'] = df['TotalCharges'].replace(" ", 0)
df['TotalCharges'] = df['TotalCharges'].astype(float)
```

 **Explanation:**
Replaced null values with zero where tenure is zero and changed datatype from object to float.

---

### Check data info:

```python
df.info()
```

### Check for null values:

```python
df.isnull().sum().sum()
```

 **Conclusion:**
No null values found in the dataset.

---

### Describe dataset:

```python
df.describe()
```

---

### Check duplicate customer IDs:

```python
df["customerID"].duplicated().sum()
```

---

### Convert SeniorCitizen (0 or 1) to Yes/No for better understanding:

```python
def conv(value):
    if value == 0:
        return 'no'
    else:
        return 'yes'
df['SeniorCitizen'] = df['SeniorCitizen'].apply(conv)
```

---

##  **Data Visualization**

### Churn Count Bar Plot

```python
churn = df['Churn'].value_counts()
col = ["green", "red"]
plt.bar(churn.index, churn.values, color=col)
plt.xlabel('Churn')
plt.ylabel('Count')
plt.title('Churn Count')

# Add text on top of each bar
for index, value in enumerate(churn.values):
    plt.text(index, value + 1, str(value), ha='center')

plt.show()
```

 **Note:**
Green indicates customers who have not churned out, red indicates those who have churned out.

---

### Churn Distribution Pie Chart

```python
plt.figure(figsize=(4,4))
churn = df['Churn'].value_counts()
plt.pie(churn, labels=churn.index)
plt.title('Churn Distribution')
plt.show()
```

 **Conclusion:**
**26.5%** of customers have churned out.

---

### Churn Analysis by Gender

```python
sns.countplot(x="gender", data=churn_analysis, hue='Churn')
plt.title("Churn Analysis by Gender")
plt.show()
```

---

### Churn Analysis by Senior Citizen

```python
ax = sns.countplot(x="SeniorCitizen", data=churn_analysis, hue='Churn')
ax.bar_label(ax.containers[0])
plt.title("Churn Analysis by Senior Citizen")
plt.show()
```

---

### Stacked Bar Chart: Gender vs Churn Percentage

```python
ct = pd.crosstab(churn_analysis['gender'], churn_analysis['Churn'])
ct_percent = ct.div(ct.sum(axis=1), axis=0) * 100

ax = ct_percent.plot(kind='bar', stacked=True, figsize=(6, 4), colormap='Set2')

for i, row in enumerate(ct_percent.values):
    cumulative = 0
    for j, val in enumerate(row):
        if val > 0:
            ax.text(i, cumulative + val / 2, f"{val:.1f}%", ha='center', va='center', fontsize=8)
            cumulative += val

plt.title("Gender-wise Churn Percentage")
plt.ylabel("Percentage")
plt.show()
```

---

##  **Conclusion**

 Data was cleaned, processed, and visualized to understand churn distribution.
 **Key insights** included churn percentage, gender-based churn, and senior citizen analysis.

---

### **Future Scope**

* Build predictive models to identify churn-prone customers.
* Perform correlation analysis to understand feature impacts.
* Design targeted strategies to reduce churn.

---

If you want, I can format this into a **final README.md file** for your GitHub project upload today. Let me know.
