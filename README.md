# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
Developed by:Rithika R
Reg.No:212224240136
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

df = pd.read_csv("/content/POPH.csv")

df['date'] = pd.to_datetime(df['date'])
df.set_index('date', inplace=True)

df = df['value']


df = df.to_frame(name='value')


df['diff'] = df['value'] - df['value'].shift(1)


result = seasonal_decompose(df['value'], model='additive', period=2)
df['seasonal_diff'] = result.resid


df['log'] = np.log(df['value'])


df['log_diff'] = df['log'] - df['log'].shift(1)


result = seasonal_decompose(df['log_diff'].dropna(), model='additive', period=2)
df['log_seasonal_diff'] = result.resid



plt.figure(figsize=(16, 16))

plt.subplot(6,1,1)
plt.plot(df['value'], label='Original')
plt.legend()
plt.title('Original Data')

plt.subplot(6,1,2)
plt.plot(df['diff'], label='Regular Difference')
plt.legend()
plt.title('Regular Differencing')

plt.subplot(6,1,3)
plt.plot(df['seasonal_diff'], label='Seasonal Adjustment')
plt.legend()
plt.title('Seasonal Adjustment')

plt.subplot(6,1,4)
plt.plot(df['log'], label='Log Transformation')
plt.legend()
plt.title('Log Transformation')

plt.subplot(6,1,5)
plt.plot(df['log_diff'], label='Log + Difference')
plt.legend()
plt.title('Log + Regular Differencing')

plt.subplot(6,1,6)
plt.plot(df['log_seasonal_diff'], label='Final Processed Data')
plt.legend()
plt.title('Log + Diff + Seasonal')

plt.tight_layout()
plt.show()
```

## OUTPUT:

### ORIGINAL DATA

<img width="1291" height="242" alt="image" src="https://github.com/user-attachments/assets/c4e578aa-beab-43cd-af26-38efc23bcf68" />



### REGULAR DIFFERENCING:

<img width="547" height="118" alt="image" src="https://github.com/user-attachments/assets/ed892504-375e-4bff-88c1-63e6a35e6c79" />


### SEASONAL ADJUSTMENT:

<img width="594" height="118" alt="image" src="https://github.com/user-attachments/assets/db563033-93f8-4d23-9cad-e7e9542da731" />



### LOG TRANSFORMATION:

<img width="556" height="118" alt="image" src="https://github.com/user-attachments/assets/1d57b75b-8551-4b78-92c9-e27f1ce875fc" />

### LOG + REGULAR DIFFERENCING:

<img width="556" height="118" alt="image" src="https://github.com/user-attachments/assets/a5cd2a0d-d0c5-4c02-9110-d3fd1ec7d6cd" />

### LOG +  DIFF + SEASONING:

<img width="628" height="105" alt="image" src="https://github.com/user-attachments/assets/d80d8a6d-a73e-4c53-9c20-9b1668e4b759" />




## RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
