# Sales-Data-Cleaning-and-Transformation-with-Python
A practical data cleaning, transformation, validation, and data quality assurance project using Python, Pandas, and NumPy. The project transforms a complex, pivot-style retail sales CSV report into a clean, structured, and analysis-ready dataset.

## Project Overview
Real-world datasets are rarely delivered in a format that is immediately ready for analysis. This project demonstrates how to take a presentation-oriented retail sales report containing embedded headers, structural missing values, Excel serial dates, and a wide-format layout, and systematically transform it into a reliable analytical dataset.

## Dataset Transformation
### Raw Structure
The original CSV used a cross-tabular/pivot-style structure where Segment and Ship Mode information were embedded within the headers.
<img width="964" height="491" alt="Image" src="https://github.com/user-attachments/assets/3bfec76a-1d4c-42a5-9355-8a23bd97882a" />
It contained:
- 824 rows
- 13 columns
- Embedded header rows
- 12 Segment × Ship Mode sales fields
- Excel serial dates
- Structural NaN values
- Sales values stored as object

#### Final Structure
The cleaned dataset contains:
- Column	    Description
- Order Date	Date associated with the sales observation
- Ship Mode	  Shipping method
- Segment	    Customer segment
- Sales	      Sales amount
#### Final dimensions:
822 rows × 4 columns

## Data Cleaning and Transformation Process
1. Data Inspection
The raw CSV was imported using Pandas and systematically inspected to understand:
- Dataset dimensions
- Column structure
- Embedded headers
- Data types
- Missing-value patterns
- Date representation
- Sales distributions
2. Structural Analysis
The report structure was decomposed into its underlying business dimensions.
The 12 sales fields were mapped across:
- Ship Mode
- First Class
- Same Day
- Second Class
- Standard Class
- Segment
- Consumer
- Corporate
- Home Office
This mapping allowed the report to be reconstructed without losing the relationship between sales, customer segment, and shipping method.
3. Header & Structural Cleaning
The embedded Segment and Order Date header rows were identified and removed from the transactional dataset.
This isolated the 822 genuine order records from the report metadata.
4. Wide-to-Long Transformation
The original wide-format report was transformed into a tidy long-format structure:
Order Date | Ship Mode | Segment | Sales
5. Structural Missing-Value Handling
The raw report contained thousands of NaN values.
These were identified as structural missing values, rather than conventional missing observations. A blank cell represented an Order Date × Ship Mode × Segment combination with no recorded sales.
Therefore, the values were not replaced with zero.
Only genuine sales observations were retained.
6. Date Conversion
The original Order Date values were stored as Excel serial numbers, such as:
- 41289
- 41501
- 41632
These were converted into proper calendar dates using Pandas.
7. Data Type Correction
The final dataset was validated to ensure appropriate data types:
- Order Date to datetime64[ns]
- Ship Mode to object
- Segment   to object
- Sales     to float64
8. Duplicate Validation
A complete duplicate check was performed.
No duplicate observations were found.
9. Sales Quality Validation
Sales values were checked for logically invalid values.
Zero Sales: 0
Negative Sales: 0
All retained sales observations were positive.
10. Outlier Analysis
The Interquartile Range (IQR) method was used to identify statistically unusual Sales values.
- Q1: 34.5405
- Q3: 536.11
- IQR: 501.5695
- Upper Bound: 1288.46425
70 observations were identified as statistical outliers.
Rather than automatically deleting them, the transactions were inspected. The high-value observations were considered legitimate sales transactions and were therefore retained.
This preserves the integrity of the underlying business data.
11. Business Logic Validation
The final dataset was validated across all 12:
Ship Mode × Segment combinations
Record counts and sales totals were checked to ensure that the restructuring process did not introduce data loss or alter the underlying sales values.
The final dataset reconciled to:
822 valid sales observations
with all expected Ship Mode and Segment categories present.

## Technologies Used
- Python
- Pandas
- NumPy

## Skills Demonstrated
- Data Cleaning
- Data Preprocessing
- Data Transformation
- Wide-to-Long Transformation
- Tidy Data Principles
- Data Quality Assessment
- Missing Data Analysis
- Data Type Conversion
- Excel Serial Date Conversion
- Outlier Detection
- Data Validation
- Business Logic Validation
- Pandas
- NumPy
- Analytical Problem Solving
## Project Outcome
The project successfully transformed a complex 824-row, 13-column reporting dataset into a clean 822-row, 4-column analytical dataset.
## The final dataset:
-  Contains only valid sales observations
-  Uses appropriate data types
-  Contains no missing values
-  Contains no duplicate records
-  Contains no zero or negative sales
-  Preserves legitimate high-value transactions
-  Maintains the original Segment and Ship Mode relationships
-  Is structured for downstream analytical use

