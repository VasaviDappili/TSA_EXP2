# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Date:28/04/2026
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt


data = pd.read_csv("C:/Users/admin/Downloads/Chocolate Sales (2).csv")


data['Date'] = pd.to_datetime(data['Date'], format='%d/%m/%Y')


data['Amount'] = data['Amount'].replace('[\$,]', '', regex=True).astype(float)


data.set_index('Date', inplace=True)


resampled_data = data['Amount'].resample('Y').sum().to_frame()


resampled_data.index = resampled_data.index.year


resampled_data.reset_index(inplace=True)
resampled_data.rename(columns={'Date': 'Year', 'Amount': 'Sales'}, inplace=True)


years = resampled_data['Year'].tolist()
sales = resampled_data['Sales'].tolist()


X = [i - years[len(years)//2] for i in years]

n = len(X)
```
###### LINEAR TREND ESTIMATION
```
xy = [i*j for i, j in zip(X, sales)]

b = (n * sum(xy) - sum(sales) * sum(X)) / (n * sum(x2) - (sum(X)**2))
a = (sum(sales) - b * sum(X)) / n

linear_trend = [a + b * X[i] for i in range(n)]
```

###### POLYNOMIAL TREND ESTIMATION(Degree 2
```
x3 = [i**3 for i in X]
x4 = [i**4 for i in X]
x2y = [i*j for i, j in zip(x2, sales)]

coeff = [
    [n, sum(X), sum(x2)],
    [sum(X), sum(x2), sum(x3)],
    [sum(x2), sum(x3), sum(x4)]
]

Y = [sum(sales), sum(xy), sum(x2y)]

A = np.array(coeff)
B = np.array(Y)

a_poly, b_poly, c_poly = np.linalg.solve(A, B)

poly_trend = [a_poly + b_poly*X[i] + c_poly*(X[i]**2) for i in range(n)]

```

##### VISUALISING RESULT
```
print("Linear Trend Equation:")
print(f"y = {a:.2f} + {b:.2f}x")

print("\nPolynomial Trend Equation (Degree 2):")
print(f"y = {a_poly:.2f} + {b_poly:.2f}x + {c_poly:.2f}x²")


resampled_data['Linear Trend'] = linear_trend
resampled_data['Polynomial Trend'] = poly_trend


resampled_data.set_index('Year', inplace=True)


plt.plot(resampled_data.index, resampled_data['Sales'], marker='o')
plt.plot(resampled_data.index, resampled_data['Linear Trend'], linestyle='--')

plt.title("Linear Trend Estimation")
plt.xlabel("Year")
plt.ylabel("Sales")

plt.show()

plt.figure()

plt.plot(resampled_data.index, resampled_data['Sales'], marker='o')
plt.plot(resampled_data.index, resampled_data['Polynomial Trend'], marker='o')

plt.title("Polynomial Trend Estimation (Degree 2)")
plt.xlabel("Year")
plt.ylabel("Sales")

plt.show()
```

### OUTPUT
##### LINEAR TREND ESTIMATION

<img width="952" height="565" alt="image" src="https://github.com/user-attachments/assets/39071efa-5ed1-4324-97c6-58da4fe4e822" />

##### POLYNOMIAL TREND ESTIMATION(Degree 2)
<img width="874" height="465" alt="image" src="https://github.com/user-attachments/assets/9116758b-5f18-4bcf-8cd0-cd277b086c48" />


### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
