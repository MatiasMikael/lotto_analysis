# Lottery Data Analysis Project

## Overview
This project analyzes lottery jackpot data from 2002 to 2018, showcasing trends in jackpot frequency and total prize amounts over time. The analysis was performed using several tools and techniques to preprocess, clean, and visualize the data.

## Tools Used
*Microsoft Excel*: For initial data cleaning and preprocessing.
*Snowflake (Community Edition)*: For storing, managing, and querying the data using SQL.
*Tableau Public*: For creating interactive visualizations.
*CSV Format*: For transferring data between tools.

## Process

* 1. Data Collection and Preparation

Raw lottery data in Excel format was downloaded.
The data contained unnecessary columns (e.g., notes), which were removed in Excel.
The data was filtered to include only records from *2002 onwards*, as the focus was on euro-denominated jackpots.
Columns were renamed to:
*Year*
*Jackpots*
*Total Prize (EUR)*
The *Total Prize (EUR)* column was cleaned and formatted to include commas for thousand separators and to display amounts in millions of euros.
* 2. Database Creation and Data Querying

A *database* and *table* were created in Snowflake:
```sql
CREATE DATABASE lotto_analysis;
USE lotto_analysis;

CREATE TABLE lotto_results (
Year INTEGER,
Total_Jackpots INTEGER,
Total_Prize_EUR FLOAT
);
```

Data was uploaded into Snowflake and queried using SQL.

The following SQL query was used to aggregate the data:
```sql
SELECT
Year,
SUM(Jackpots) AS Total_Jackpots,
SUM(Total_Prize_EUR) AS Total_Prize_EUR
FROM lotto_results
WHERE Year >= 2002
GROUP BY Year
ORDER BY Year;
```

The resulting data contained:

A single row for each year *(2002–2018)*.
The total number of jackpots and total prize amounts for each year.
The queried data was exported from Snowflake in *CSV format*.

* 3. Data Visualization

The aggregated data was imported into *Tableau Public*.
Three key visualizations were created:
*Annual Number of Jackpots*: A bar chart showing the total number of jackpots per year.
*Jackpots vs. Total Prizes Over Time*: A dual-axis chart comparing the number of jackpots and total prize amounts for each year.
*Yearly Development of Total Prize*: A line chart illustrating the trend in total prize amounts over time.
* Visualizations

* 1. Annual Number of Jackpots

This bar chart shows the total number of jackpots per year.
*Insights:*
The number of jackpots increased over time, with a notable peak in #2015# #(48 jackpots)#.
There were years with fewer jackpots, such as #2002–2005#, indicating a gradual increase over the years.
* 2. Jackpots vs. Total Prizes Over Time

This dual-axis chart compares the number of jackpots #(green bars)# with the total prize amount #(orange line)# for each year.
Insights:
In *2015*, the highest number of jackpots *48* also corresponded to one of the highest total prize amounts.
Total prizes are not always proportional to the number of jackpots, as seen in *2008* and *2017*, where total prizes peaked despite moderate jackpot counts.
* 3. Yearly Development of Total Prizes

This line chart shows the growth of total prize amounts over time.
Insights:
There is a steady increase in total prize amounts from *2002 to 2018*, peaking in *2017* at €138 million.
The trend indicates growing lottery popularity or changes in prize structures over the years.

---

## License

The *project's code and documentation* are licensed under the **MIT License**.  
The *data* used in this project is licensed under **Public Domain**, and the dataset can be accessed (https://www.avoindata.fi/data/fi/dataset/loton-miljoonavoitot).
