# 🌟 **Food Packaging and Distribution**

<h2 align="center" style="color:#FF6347; font-family:Arial;">Dynamic Insights for Efficient Food Packaging and Distribution</h2>

A **food packaging and distribution company**, due to market conditions, diverse sales, and high sales volume, required <span style="color:#FFA500;">dynamic</span> and <span style="color:#1E90FF;">diverse reports</span>. 

<h3 style="color:#32CD32; font-family:Arial;">Production and Sales Process Overview</h3>

Generally, the production and sales process in this industry operated as follows:
- Raw materials entered the system.
- <span style="color:#DAA520;">Underwent packaging</span>.
- The packaged products were delivered to customers.

A customer placed an order for a specific number of packages (a package refers to a bundled group of items in the facility); however, sales occurred by weight, and the cost was calculated per kilogram. Each package corresponded to a certain weight but was not fully utilized during the production process. The weight of the final product was less than the ordered weight. Therefore, the difference between the package weight and the sales weight indicated the amount of waste.

<h3 style="color:#6A5ACD; font-family:Arial;">Data Preparation</h3>

Initially, after importing the required libraries, an overview of the dataframe was necessary. Since the Excel file included two separate sheets, both sheets were read and stored in two separate variables:
- The names of these sheets were **<span style="color:#FF4500;">Transaction</span>** and **<span style="color:#4682B4;">Customer</span>**.
- Finally, the **<span style="color:#2E8B57;">Dimdate</span>** file was read and stored as well.

<h3 style="color:#20B2AA; font-family:Arial;">Structure of the Data</h3>

### **Transaction Table**

| **Column Name**       | **Description**                                                   |
|-----------------------|-------------------------------------------------------------------|
| Transaction_ID        | Transaction identifier                                           |
| Product_ID            | Product identifier                                               |
| Export                | Indicates whether the product was for export or domestic consumption |
| Industry              | Specifies the type of customer industry                          |
| City_Category         | Location category relative to the province of the customer's head office |
| Stay_In_Customer      | Number of days the customer's order stayed at the facility       |
| Material_Status       | Indicates whether the customer's product was supplied from inventory or was in production |
| Payment               | Order payment amount in rials                                    |
| Unit_Price            | Price per kilogram of the product in rials                       |
| Save_Date_Time        | Order registration time in the Persian calendar                  |
| Send_Date             | Shipping date in the Gregorian calendar                          |
| Customer_ID           | Customer code                                                   |
| Bandel                | Number of packages (each package equals 2 ± 0.05 tons; 2 tons were used in calculations) |
| Real_Weight           | Actual weight sold                                               |

### **Customers Table**

| **Column Name**       | **Description**                                                   |
|-----------------------|-------------------------------------------------------------------|
| Customer_ID           | Transaction identifier                                           |
| Province              | Name of the province                                            |
| City_Category         | Location category relative to the province of the customer's head office |
| Stay_In_Customer      | Number of days the customer's order stayed at the facility       |
| Export/Import         | Indicates whether the product was for export or domestic consumption |
| Industry_Cod          | Industry code                                                   |

<h3 style="color:#FF69B4; font-family:Arial;">Industry Code Classification</h3>

In this table, the **Industry_Cod** provided a more detailed classification of industries:
- <span style="color:#FFD700;">0 to 4</span>: Retail industry
- <span style="color:#FF7F50;">5 to 9</span>: Wholesale industry
- <span style="color:#B0E0E6;">10 to 13</span>: E-commerce industry
- <span style="color:#98FB98;">14 to 17</span>: Bulk supply industry
- <span style="color:#FFB6C1;">18 to 20</span>: Specialty goods industry

<h3 style="color:#00CED1; font-family:Arial;">Dimdate Table</h3>

The **Dimdate** table was a helper table used to convert Gregorian dates to Persian (Solar Hijri) dates and vice versa. It included:
- Day
- Month
- Year
- Month name
- Day of the week
- Week number of the year, etc., covering the years from 1320 to 1429 in the Persian calendar.

<h3 style="color:#FF4500; font-family:Arial;">Final Dataframe Preparation</h3>

Before merging the **Transaction** and **Customer** dataframes, decisions were made regarding each column. The following columns were retained:
- Transaction_ID
- Export
- Industry
- City_Category
- Payment
- Customer_ID
- Bandel
- Real_Weight
- Province
- Industry_Cod
- Waste
- Year
- Month
- Type
- Class

**Additional Steps:**
- A new column for **Waste** was added.
- The **Bandel** column was converted to kilograms.
- The **Year** and **Month** columns were extracted from Gregorian equivalents in the **Miladi** column.
- The **Product_ID** column was split into **Type** and **Class**.
- The **Payment** column was scaled to billions of tomans.

<h3 style="color:#DA70D6; font-family:Arial;">Analytical Questions</h3>

- Determine the sales amount for imports and exports for each year and month.
- Identify the top ten customers by purchase volume and total waste.
- Analyze sales, waste, and sales count for each industry by **Type** and **Class**.
- Calculate total purchase amount, sales count, and waste for each province by year.
- Examine total kilograms produced for each **City_Category** by **Type** (boxed or bulk) and **Class**.
- Categorize prices into **Low**, **Med**, and **High** using quartiles.
- Calculate average waste for the retail industry in 2020 for **High**-price purchases.

<h3 align="center" style="color:#FF6347; font-family:Arial;">Your Gateway to Optimized Food Packaging and Distribution 🚀</h3>
