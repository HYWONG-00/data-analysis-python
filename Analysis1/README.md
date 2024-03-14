# data-analysis-python
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

