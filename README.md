# 📚 Hot Rolled Steel Analysis Repository

---

## 🌟 Welcome to the Repository

This repository provides a detailed analysis framework for understanding and optimizing the processes involved in the hot rolling steel industry. It includes data handling, insights extraction, and advanced analytics for sales, waste management, and customer behavior.

---

## 📂 Dataset Information

You can download the datasets for this exercise from:
- [Steel Dataset](https://docs.google.com/spreadsheets/d/1WHi8Btw9YCuF0vbkBgphPoWb1rmxyZkA/edit?usp=drive_link)
- [Dimdate Dataset](https://docs.google.com/spreadsheets/d/1MdzmRdPKIAZMPu3XlnognXFPf8t6_XPa/edit?usp=drive_link)

---

## 🔍 Overview of Hot Rolled Steel

Hot rolled steel refers to steel that has been rolled at very high temperatures (above 1700°F), exceeding the recrystallization temperature for most types of steel. This process makes it easier to shape the steel, resulting in products with a wider variety of appearances.

A hot rolling steel company, due to market conditions, diverse sales, and high sales volume, requires dynamic and diverse reports. Generally, the production and sales process works as follows:
- Steel billets enter the system.
- They undergo rolling.
- Rolled sections are delivered to customers.

### Key Details:
- Customers place orders in bundles, but sales are based on tonnage.
- The cost is calculated per kilogram.
- Each bundle corresponds to a billet weighing 2 tons, though not fully utilized during production.
- Waste is the difference between the bundle weight and the sales tonnage.

---

## 📊 Data Structure

### **Transaction Table**

| Column Name       | Description                                                    |
|-------------------|----------------------------------------------------------------|
| Transaction_ID    | Transaction identifier                                        |
| Product_ID        | Product identifier                                            |
| Export            | Indicates export or domestic consumption                      |
| Industry          | Type of customer industry                                     |
| City_Category     | Location category relative to customer head office province   |
| Stay_In_Customer  | Days customer’s order stayed at the factory                  |
| Material_Status   | Inventory or production supply status                         |
| Payment           | Order payment amount in rials                                 |
| Unit_Price        | Price per kilogram in rials                                   |
| Save_Date_Time    | Order registration time in Persian calendar                   |
| Send_Date         | Shipping date in Gregorian calendar                           |
| Customer_ID       | Customer code                                                 |
| Bandel            | Bundles ordered (each bundle equals 2 ± 0.05 tons)           |
| Real_Weight       | Actual weight sold                                            |

### **Customer Table**

| Column Name       | Description                                                    |
|-------------------|----------------------------------------------------------------|
| Customer_ID       | Customer identifier                                           |
| Province          | Name of the province                                         |
| City_Category     | Location category relative to customer head office province   |
| Stay_In_Customer  | Days customer’s order stayed at the factory                  |
| Export/Import     | Indicates export or domestic consumption                      |
| Industry_Cod      | Industry code                                                 |

### Industry Code Classification:
- **0-4**: Construction
- **5-9**: Machining
- **10-13**: Riveting
- **14-17**: Drawing
- **18-20**: Welding

### **Dimdate Table**

A helper table to convert Gregorian dates to Persian (Solar Hijri) dates and vice versa. It includes:
- Day, Month, Year
- Month name, Day of the week
- Week number of the year
- Covers years 1320 to 1429 in the Persian calendar.

---

## 🚀 Data Preprocessing Steps

1. **Column Selection**:
   - Retain these columns in the final dataframe:
     `Transaction_ID`, `Export`, `Industry`, `City_Category`, `Payment`, `Customer_ID`, `Bandel`, `Real_Weight`, `Province`, `Industry_Cod`, `Waste`, `Year`, `Month`, `Type`, `Class`.

2. **New Columns**:
   - Add a column for `Waste`.
   - Convert `Bandel` to kilograms.

3. **Date Conversion**:
   - Add a `Miladi` column for Gregorian dates from `Save_Date_Time`.
   - Extract `Year` and `Month` from `Miladi`, then delete `Miladi`.

4. **Product_ID Split**:
   - Split `Product_ID` into `Type` and `Class` columns.

5. **Payment Scaling**:
   - Convert `Payment` from rials to billions of tomans.

---

## 📌 Analytical Questions

1. **Yearly and Monthly Sales**:
   - Determine sales for imports and exports for each year and month.
   - Use `Year` and `Month` as dataframe indexes.

2. **Top Customers**:
   - Identify the top 10 customers by purchase volume, number of purchases, and total waste.
   - Sort by total sales in descending order.

3. **Industry Insights**:
   - Analyze sales, waste, and number of sales for each industry (`Machining`, `Welding`, `Construction`, `Riveting`, `Drawing`) by `Type` and `Class`.

4. **Province Analysis**:
   - Calculate total purchases, number of purchases, and total waste for each province per year.

5. **Product Form Analysis**:
   - Determine total kilograms produced for each `City_Category`, categorized by `Type` (straight vs. coil) and `Class`.

6. **Quartile Analysis**:
   - Categorize prices into `Low`, `Med`, and `High` based on quartiles (`Q1`, `Q2`, `Q3`).
   - Add a `PriceLevel` column.

7. **Industry Filter**:
   - Filter data for industries with more than 50,000 sales and store in `Indfilter`.

8. **Waste Analysis**:
   - Report the average waste for the construction industry in 2020 for purchases with high prices, normalized by bundles.

---

## 🛠 Contribution

Feel free to fork this repository, suggest improvements, or raise issues. Collaboration is always welcome!

---

## 🌟 Acknowledgments

Thank you for exploring this repository. We hope it provides valuable insights and tools for your analysis. Please star ⭐ this project if you find it helpful!
