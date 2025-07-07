

# Problem Statement

AtliQ Motors is an automotive giant from the USA specializing in electric vehicles (EV). In the last 5 years, their market share rose to 25% in electric and hybrid vehicles segment in North America. As a part of their expansion plans, they wanted to launch their bestselling models in India where their market share is less than 2%. Bruce Haryali, the chief of AtliQ Motors India wanted to do a detailed market study of existing EV/Hybrid market in India before proceeding further. Bruce gave this task to the data analytics team of AtliQ motors and Peter Pandey is the data analyst working in this team.

### Credits: 
The dataset is taken from the Vahan Sewa. Thanks to the Vahan Sewa for 
providing datasets for public access which is a great learning asset - feel free to explore 
them here: <a href = "https://vahan.parivahan.gov.in/vahan4dashboard/vahan/view/reportview.xhtml">Vahan Sewa</a> 

## Questions:

###  Preliminary Questions:
* List the top 3 and bottom 3 makers for the fiscal years 2023 and 2024 in terms of the number of 2-wheelers sold.
* Identify the top 5 states with the highest penetration rate in 2-wheeler and 4-wheeler EV sales in FY 2024.
* List the states with negative penetration (decline) in EV sales from 2022 to 2024?
* What are the quarterly trends based on sales volume for the top 5 EV makers (4-wheelers) from 2022 to 2024?
* How do the EV sales and penetration rates in Delhi compare to Karnataka for 2024?
* List down the compounded annual growth rate (CAGR) in 4-wheeler units for the top 5 makers from 2022 to 2024.
* List down the top 10 states that had the highest compounded annual growth rate (CAGR) from 2022 to 2024 in total vehicles sold.
* What are the peak and low season months for EV sales based on the data from 2022 to 2024?
* What is the projected number of EV sales (including 2-wheelers and 4-wheelers) for the top 10 states by penetration rate in 2030, based on the compounded annual growth rate (CAGR) from previous years
* Estimate the revenue growth rate of 4-wheeler and 2-wheelers EVs in India for 2022 vs 2024 and 2023 vs 2024, assuming an average unit price. Average Price =85K for 2-Wheeler, 15L for 4-Wheeler


### Secondary Questions

* What are the primary reasons for customers choosing 4-wheeler EVs in 2023 and 2024 (cost savings, environmental concerns, government incentives)?
* How do government incentives and subsidies impact the adoption rates of 2-wheelers and 4-wheelers? Which states in India provided most subsidies?
* How does the availability of charging stations infrastructure correlate with the EV sales and penetration rates in the top 5 states?
* Who should be the brand ambassador if AtliQ Motors launches their EV/Hybrid vehicles in India and why?
* Which state of India is ideal to start the manufacturing unit? (Based on subsidies provided, ease of doing business, stability in governance etc.)
* Your top 3 recommendations for AtliQ Motors.

## Data Collection

The dataset is taken from the Vahan Sewa. Thanks to the Vahan Sewa for 
providing datasets for public access which is a great learning asset - feel free to explore 
them here: Vahan Sewa 
* Dataset required to answer preliminary analysis questions. 
* Metadata 
* Supporting documents

## Data Preprocessing

### Tools Used:
* MS-Excel
* Tableau
* Canva

### Data 
* dim_date.csv
* electric_vehicle_sales_by_makers.csv
* electric_vehicle_sales_by_state.csv
### Data Description
#### dim_date.csv 
- date: The specific date for which the data is relevant. Format: DD-MMM-YY. (Data is recorded on a monthly basis)
- fiscal_year: The fiscal year to which the date belongs. This is useful for financial and business analysis.
- quarter: The fiscal quarter to which the date belongs. Fiscal quarters are typically divided as Q1, Q2, Q3, and Q4.

#### electric_vehicle_sales_by_makers.csv

- date: The date on which the sales data was recorded. Format: DD-MMM-YY. (Data is recorded on a monthly basis)
- vehicle_category: The category of the vehicle, specifying whether it is a 2-Wheeler or a 4-Wheeler.
- maker: The name of the manufacturer or brand of the electric vehicle.
- electric_vehicles_sold: The number of electric vehicles sold by the specified maker in the given category on the given date.
#### electric_vehicle_sales_by_state.csv

- date: The date on which the data was recorded. Format: DD-MMM-YY. (Data is recorded on a monthly basis)
- state: The name of the state where the sales data is recorded. This indicates the geographical location within India.
- vehicle_category: The category of the vehicle, specifying whether it is a 2-Wheeler or a 4-Wheeler.
- electric_vehicles_sold: The number of electric vehicles sold in the specified state and category on the given date.
- total_vehicles_sold: The total number of vehicles (including both electric and non-electric) sold in the specified state and category on the given date.
### Data Cleaning
- MS Excel, Power Query to clean and transform raw data.
- Removed duplicate data.
- TRIM() to clean unwanted spaces in cells.
- State DND -> Dadra & Nagar Haveli and Daman & Diu, Andaman & Nicobar Islands -> Andaman & Nicobar
## Data Visualization
Tableau is used for creating dashboards, calculated fields, parameters and analysis of the data.
### Key Points:
* Fiscal Year: The fiscal year is a one-year period used for financial reporting and budgeting, starting on April 1st and ending on March 31st of the following year in India.

* Penetration Rate: This metric represents the percentage of total vehicles that are electric within a specific region or category. It is calculated as:

		Penetration Rate =  (Electric Vehicles Sold / Total Vehicles Sold) * 100  
   This indicates the adoption level of electric vehicles.

* Compound Annual Growth Rate (CAGR): CAGR measures the mean annual growth rate over a specified period longer than one year. It is calculated as:
        
        CAGR = [(Ending Value / Beginning Value) ** 1/n] -1
### Calculated Fields & Parameters:
#### Calculated Fields-

- Date Part = DATEADD('month',9,DATE(TRIM(LEFT([Date],9))))
- Average Price = IF [Vehicle Category]='2-Wheelers' THEN 85000 ELSE 1500000 END
- Revenue = [Average Price ]*[Electric Vehicles Sold]
- CY EV Sales = IF YEAR([Date Part]) = YEAR([Current Year]) THEN [Electric Vehicles Sold] END
- CY Total Sales = IF YEAR([Date Part]) = YEAR([Current Year]) THEN [Total Vehicles Sold] END
- CY Revenue = IF YEAR([Date Part]) = YEAR([Current Year]) THEN [Revenue] END
- Index = INDEX()
- PY EV Sales = IF YEAR([Date Part]) = YEAR([Previous Year]) THEN [Electric Vehicles Sold] END
- PY Total Sales = IF YEAR([Date Part]) = YEAR([Previous Year]) THEN [Total Vehicles Sold] END
- PY Revenue = IF YEAR([Date Part]) = YEAR([Previous Year]) THEN [Revenue] END
- YoY EV Sales = (SUM([CY EV Sales])-SUM([PY EV Sales]))/SUM([PY EV Sales])
- YoY Total Sales = (SUM([CY Total Sales])-SUM([PY Total Sales]))/SUM([PY Total Sales])
- YoY Revenue = (SUM([CY Revenue])-SUM([PY Revenue]))/SUM([PY Revenue])
- Penetration Rate = SUM([Electric Vehicles Sold (Electric Vehicle Sales By State.Csv)])/SUM([Total Vehicles Sold])
- CAGR EV Sold = ZN(POWER(ZN(SUM([Electric Vehicles Sold]))/LOOKUP(ZN(SUM([Electric Vehicles Sold])),-[N Years]), ZN(1/[N Years])) - 1)
- CAGR Total Vehicle Sold = POWER(ZN(SUM([Total Vehicles Sold]))/LOOKUP(ZN(SUM([Total Vehicles Sold])),-[N Years]),1/ZN([N Years])) - 1
- Sales 2030 = ROUND(IF [Vehicle Category (Electric Vehicle Sales By State.Csv)]=="2-Wheelers" THEN POWER(1+0.922,6)* [Electric Vehicles Sold (Electric Vehicle Sales By State.Csv)] ELSE POWER(1+1.163,6)* [Electric Vehicles Sold (Electric Vehicle Sales By State.Csv)]END)
- GR 2022 Vs 2024 = ZN((SUM([Revenue])- LOOKUP(SUM([Revenue]), -2)) / LOOKUP(SUM([Revenue]),-2))
- GR 2023 Vs 2024 = ZN((SUM([Revenue])- LOOKUP(SUM([Revenue]), -1)) / LOOKUP(SUM([Revenue]),-1))
- Vehicle Category Parameter = [Vehicle Category (Electric Vehicle Sales By State.Csv)] = [Parameters].[Vehicle Category] AND [Vehicle Category] = [Parameters].[Vehicle Category]
#### Parameters-
- Current Year 

  ![image](https://github.com/user-attachments/assets/3e584f2c-5d33-4048-a195-2ecf3683d9ee)


- Previous Year

  ![image](https://github.com/user-attachments/assets/238b756c-b3b5-459c-bf93-5a2fa5541c71)

- N Years

  ![image](https://github.com/user-attachments/assets/0cf747e6-d16a-4e52-a2c8-265b9f2fa456)


- Vehicle Category

  ![image](https://github.com/user-attachments/assets/5effbbb8-48fe-4e54-9d06-71e8c5b26056)


### Visuals

![image](https://github.com/user-attachments/assets/25babb64-86e9-4e10-8d64-e3155a8b1754)


![image](https://github.com/user-attachments/assets/998337d9-6341-4d77-8ad6-df3ccb07752b)


![image](https://github.com/user-attachments/assets/f6dae6cf-b9f0-4657-a992-1fce1b47ac1a)


## Data Interpretation
- 2.07M EV sold as far in two years, generating a total revenue of ₹392.03B.
- Ola Electric tops the market in 2-Wheelers segment, and Tata Motors in 4-Wheelers segment.
- Maharashtra has the highest EV sold all over India, whereas Sikkim has not been able to sold one unit.
- Goa has the highest penetration rate followed by Kerala, Karnataka and Maharashtra.
- Rajasthan and Gujarat shows significant decline in Penetration Rate from 2023 to 2024.
- Tata Motors shows the peak in EV sales in 4-Wheelers category in quarter trends. Mahindra & Mahindra showed some progress but decline at the end of 2024. Other companies show stable progess.
- End months of year shows huge sales as compared to beginning of year, January to March registers low sales in overall EV sales.
- In 4-Wheelers segment, the craze for luxurious EV model has also risen, BMW India also launching its EV model, which is a big hit as Compounded Annual Growth Rate shows 1141% growth in two years, followed by Volvo Auto India.
- States are also taking initiatives to boost EV adoption, Meghalaya leads with 28.47% growth. Goa, Karnataka, Delhi are also taking measures for faster adoption by consumers.

## Reviews 
Thankyou for reading, any suggestions please share with me in LinkedIn :<br>
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rajat-bisht-a71b21100/)

Live Dashboard Link: <a href = "https://public.tableau.com/app/profile/rajat.bisht8107/viz/EvSalesAnalysis/FrontPage">Click Me</a> 
