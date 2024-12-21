# Food Packaging and Distribution

A food packaging and distribution company, due to market conditions, diverse sales, and high sales volume, required dynamic and diverse reports. Generally, the production and sales process in this industry operated as follows: raw materials entered the system, underwent packaging, and the packaged products were delivered to customers. A customer placed an order for a specific number of packages (a package refers to a bundled group of items in the facility); however, sales occurred by weight, and the cost was calculated per kilogram. Each package corresponded to a certain weight but was not fully utilized during the production process. The weight of the final product was less than the ordered weight. Therefore, the difference between the package weight and the sales weight indicated the amount of waste.

Initially, after importing the required libraries, an overview of the dataframe was necessary. Since the Excel file included two separate sheets, both sheets were read and stored in two separate variables. The names of these sheets were **Transaction** and **Customer**. Finally, the **Dimdate** file was read and stored as well.

The **Transaction** table had 13 columns as described below:

| Column Name       | Description                                                   |
|-------------------|---------------------------------------------------------------|
| Transaction_ID    | Transaction identifier                                       |
| Product_ID        | Product identifier                                           |
| Export            | Indicates whether the product was for export or domestic consumption |
| Industry          | Specifies the type of customer industry                      |
| City_Category     | Location category relative to the province of the customer's head office |
| Stay_In_Customer  | Number of days the customer's order stayed at the facility   |
| Material_Status   | Indicates whether the customer's product was supplied from inventory or was in production |
| Payment           | Order payment amount in rials                                |
| Unit_Price        | Price per kilogram of the product in rials                   |
| Save_Date_Time    | Order registration time in the Persian calendar              |
| Send_Date         | Shipping date in the Gregorian calendar                      |
| Customer_ID       | Customer code                                                |
| Bandel            | Number of packages (each package equals 2 ± 0.05 tons; 2 tons were used in calculations) |
| Real_Weight       | Actual weight sold                                           |

The **Customers** sheet contained six columns as described below:

| Column Name       | Description                                                   |
|-------------------|---------------------------------------------------------------|
| Customer_ID       | Transaction identifier                                       |
| Province          | Name of the province                                         |
| City_Category     | Location category relative to the province of the customer's head office |
| Stay_In_Customer  | Number of days the customer's order stayed at the facility   |
| Export/Import     | Indicates whether the product was for export or domestic consumption |
| Industry_Cod      | Industry code                                                |

In this table, the **Industry_Cod** provided a more detailed classification of industries: - Codes 0 to 4 represented the **retail** industry. - Codes 5 to 9 represented the **wholesale** industry. - Codes 10 to 13 represented the **e-commerce** industry. - Codes 14 to 17 represented the **bulk supply** industry. - Codes 18 to 20 represented the **specialty goods** industry.

The **Dimdate** table was a helper table used to convert Gregorian dates to Persian (Solar Hijri) dates and vice versa. This table included comprehensive calendar information such as: - Day - Month - Year - Month name - Day of the week - Week number of the year, etc., covering the years from 1320 to 1429 in the Persian calendar.

Before merging the **Transaction** and **Customer** dataframes, decisions were made regarding each column. In the final dataframe, only the following columns were retained:

Transaction_ID
Export
Industry
City_Category
Payment
Customer_ID
Bandel
Real_Weight
Province
Industry_Cod
Waste
Year
Month
Type
Class

A new column for waste was added to the dataframe as described earlier. The column was named exactly **Waste**.

Additionally, the **Bandel** column was converted to kilograms and stored in the same column.

The **Year** and **Month** columns were converted to the Gregorian format. To calculate these values: - A new column named **Miladi** was added to the dataframe by converting the Persian dates in the **Save_Date_Time** column to their Gregorian equivalents. - The year and month were extracted from the **Miladi** column and stored in the **Year** and **Month** columns, respectively. - Finally, the **Miladi** column was deleted after extraction.

The **Product_ID** column was split into three separate columns using the dot (`.`) as a delimiter: - The first column was named **Type**. - The second column was named **Class**. - The third column was discarded.

The **Payment** column, which was in rials, was scaled to billions of tomans.

Now that clean and standardized data was prepared, the following questions were answered:

We wanted to determine the sales amount for imports and exports for each year and each month of that year. The **Year** and **Month** columns were set as the index of the dataframe.

The top ten customers with the highest purchase volume were identified, including the number of purchases and the total production waste for each. This table was sorted in descending order based on the total sales amount.

The sales amount, the production waste, and the number of sales for each industry (retail, wholesale, e-commerce, bulk supply, and specialty goods) in each **Type** and **Class** subcategory were determined.

The total purchase amount for each province in each year was calculated. Additionally, the number of purchases and the total production waste for each province were reported.

In the industry, packaged goods could be produced either as boxed items or bulk supplies. Boxed goods were produced in discrete packages, while bulk supplies were prepared in larger quantities. The **Type** column indicated the production form: - **B** represented boxed goods. - **L** represented bulk supplies.

The total kilograms of products produced for each **City_Category**, categorized by the **Type** (boxed or bulk) and their respective **Class**, were determined.

Quartiles were used to divide the data into four parts using three points. These quartiles were referred to as the first quartile, second quartile, and third quartile, commonly denoted as **Q1**, **Q2**, and **Q3**, respectively. To determine quartiles, the data was sorted in ascending order. - **Q1** (the first quartile or lower quartile) was the value below which 25% of the observations fell. - **Q2** (the second quartile) was the median, which split the dataset into two halves, where 50% of the observations were smaller and 50% were larger. - **Q3** (the third quartile or upper quartile) was the value above which 25% of the observations fell and below which 75% of the observations fell.

The values in the **Price** column were categorized into three groups: - Prices strictly below **Q1** were labeled as **Low**. - Prices between **Q1** and **Q3** (inclusive) were labeled as **Med**. - Prices above **Q3** were labeled as **High**.

These categorizations were stored in a new column called **PriceLevel**.

A function named **Categorize** was defined and applied to the dataframe using the `apply` method to achieve this.

A filter command was used to extract the part of the dataframe related to industrial codes with more than **50,000 sales**. This filtered data was stored in a variable named **Indfilter**.

Finally, the **average waste** for the **retail industry** in the year **2020** for purchases with **High** prices, normalized by the number of packages, was calculated and reported.
