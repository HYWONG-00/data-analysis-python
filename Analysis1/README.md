# Analysis 1
## Question: What is the relationship between total income and outcome (expenses) for different business units?
```
import pandas as pd

# Load the CSV file
file_path = 'business_unit_system_cash_flow.csv'
df = pd.read_csv(file_path)

# Aggregate financial performance for each business unit
aggregate_financial_performance = df.groupby('Unidad de Negocio').agg({
    'Ingresos': 'sum',
    'Egresos': 'sum',
    'Total': 'sum'
}).reset_index()

# Calculate Net Income as Income - Expenses just to confirm the 'Total' column matches this calculation (it should)
aggregate_financial_performance['Calculated Net Income'] = aggregate_financial_performance['Ingresos'] - aggregate_financial_performance['Egresos']
aggregate_financial_performance.sort_values(ascending=False, by=['Calculated Net Income'])
```
## Highlights:
1) Desarrolladora GR shows the highest net income, approximately 74,201,722 in total, which indicates it has strong financial performance in the system.
2) Paseo Carmelina, Paseo Cortaderas, Paseo Retamas, and Paseo ServiCenter also show significant positive net incomes, which means these opeartions are profitable.
3) Lagus and Paseos - Grdi shows negative net incomes, with Paseos - Grdi having most negative net incomes for approximately -8,486,804.56. The organizations should concern on their operational improvement.
4) Some units, such as Alquileres Varios, shows a net income of 0, which means income and expenses over period are balance. The organizations should concern on their operational improvement as well.
5) The above trial provides a broad perspective on the financial health and performance of each business unit, showing which operations needs improvement and which operations are profitable. Next, we should dive deeper into the trends over time for specific units of interest, to understand the financial outcome behind better.

## Question: Draw a line chart to show the distribution for monthly income and outcome across the period
```
import matplotlib.pyplot as plt
import seaborn as sns
from pandas.tseries.offsets import MonthEnd
import locale

# Set the locale to Spanish to handle month names in Spanish
locale.setlocale(locale.LC_TIME, 'es_ES.UTF-8')

# Try converting 'Período' to datetime again
try:
    cash_flow_data['Período'] = pd.to_datetime(cash_flow_data['Período'], format='%B %Y', errors='coerce') + MonthEnd(1)
except ValueError:
    # In case of an error, reset the locale and inform the user
    locale.setlocale(locale.LC_TIME, 'C')
    raise

# Reset the locale back to default
locale.setlocale(locale.LC_TIME, 'C')

# Aggregate data by month again
monthly_data = cash_flow_data.groupby(cash_flow_data['Período']).agg({'Ingresos': 'sum', 'Egresos': 'sum'})

# Plotting the updated data
plt.figure(figsize=(15, 6))
plt.plot(monthly_data.index, monthly_data['Ingresos'], label='Ingresos', color='blue')
plt.plot(monthly_data.index, monthly_data['Egresos'], label='Egresos', color='red')
plt.title('Monthly Income (Ingresos) and Outcome (Egresos)')
plt.xlabel('Month')
plt.ylabel('Amount')
plt.legend()
plt.grid(True)
sns.despine()

plt.show()
```
## Highlights:
1) Overall, the month income and outcome is quite balance across the period, the organization might wants to focus on improvement of its operations.
2) There is sudden increase in for both income and outcome in 2022-04 which indicates there is strong business operations on-going during that period. 
3) There is another unexpected rise in company's income around 2022-07, which boosts the company's revenue during that time, as the expenses remains relatively low.


