# Data Quality Assessment
## Dataset Structure
- Rows: 2,000
- Columns: 15
- Analysis period: 2023–2025
## Row Granularity
Each row represents one e-commerce order.
The `Order_ID` field contains 2,000 unique values for 2,000 records.
## Sales Validation
The reported `Total_Sales` field was compared with an expected sales calculation:
`Quantity × Unit Price × (1 − Discount_Percent / 100)`
A sales ratio was calculated as:
`Total_Sales / Expected_Sales`
## Findings
The 2,000 records fall into three clear groups:
| Pattern | Number of Records |
|---|---:|
| Ratio approximately 1 | 1,706 |
| Ratio approximately 0.1 | 178 |
| Ratio approximately 10 | 116 |
| **Total** | **2,000** |
This indicates that the original `Total_Sales` field contains inconsistent scaling for 294 records.
- 178 records appear to have sales values approximately 10 times too small.
- 116 records appear to have sales values approximately 10 times too large.
- 1,706 records are consistent with the expected calculation, allowing for small rounding differences.
## Cleaning Decision
The original `Total_Sales` field will be preserved for traceability.
A new field, `Corrected_Total_Sales`, will be calculated using:
`Quantity × Unit Price × (1 − Discount_Percent / 100)`
Values will be rounded to two decimal places.
## Status
Sales validation completed.
Corrected sales values created for analysis.
