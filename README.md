# Auto-Sales-Analysis
### Table Of Content
- [Project overview](#project-overview)
- [Data sources](#data-sources)
- [Tools](#tools)
- [Data cleaning](#data-cleaning)
- [Exploratory data analysis](#exploratory-data-analysis)
- [Data analysis](#data-analysis)
- [Results and findings](#results-and-findings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)
### Project overview
The purpose of this analysis is to gain more insight on the sales of auto products, trends over the years and information that will help enhance sales and solve problems.

![Overview](https://github.com/user-attachments/assets/29247d2c-a83f-4076-aa73-144f166de779)

![product dashboard](https://github.com/user-attachments/assets/12d0db0b-48d6-4bd8-87fa-c5d52ddbbcf6)

![Customer dashboard](https://github.com/user-attachments/assets/da5ef897-fb57-4085-a329-6c5faf98d22b)



### Data sources 
Auto sales data: the primary data used for this analysis is the “auto sales data.csv” containing detailed information on sales auto products.

### Tools 
1.	Excel – exploring, cleaning  the data
2.	PostgreSQL – cleaning, testing, and analyzing the data
3.	PowerBi – designing the dashboard

### Data cleaning
1.	Data loading and exploration
2.	Handling missing values
3.	Data cleaning and formatting
4.	Handling data Inconsistencies

### Exploratory data analysis
This involves exploring the auto sales data to answer key questions such as:
1.	How many product category are there?
2.	What product category has the most sales?
3.	How many countries was partnered with?
4.	Which country has the most sales?
5.	What is the Sales trend over the year?
6.	Who are the high value customer in each country?
7.	Who are the top 10 global high value customers?
8.	What is the top 10 bestselling product globally?
9.	What is the top selling product among each product category

### Data analysis

```sql
--cte
WITH CustomerSales AS (
	SELECT Country,customer_name,SUM(Sales) AS TotalSales FROM auto_sales
    GROUP BY Country, customer_name),
RankedCustomers AS(
	SELECT Country,customer_name,TotalSales,
	RANK() OVER (PARTITION BY Country ORDER BY TotalSales DESC) AS Rank
    FROM CustomerSales
)
SELECT Country,customer_name,TotalSales FROM RankedCustomers WHERE Rank = 1
ORDER BY TotalSales DESC;
```
```Sql
with ProductSales as(
	select product_line,sum(sales) as total_sales ,product_code from auto_sales
    group by product_line,product_code order by total_sales desc

),
Rankedproduct as(
	select product_line,total_sales,product_code,
	rank()over(partition by product_line order by total_sales desc) as rank
	from ProductSales
)
select product_line,product_code,total_sales from Rankedproduct where rank = 1
order by total_sales desc;
```
### Results and findings
1.	There are Seven (7) product category.
2.	Classic cars has the most sales followed by Vintage cars while train has the least sales.
3.	A total of 19 countries was partnered with over the years.
4.	 USA has the most sales followed by Spain while Ireland has the least sales.
5.	A total of 3.3 mil was made in year 2018, an increase of 4.6mil was made in the year 2019 while a whooping decrease of 1.7 mil was made in 2020. Indebt  analysis showed that the dip in sales in the year 2020 was because the company was in operation  for only five (5) months with a total of 39 customers,57 orders across 14 countries, this may be as a result of COVID which was at its peak in year 2020 as a result many business were affected.
6.	High value customers  in each countries are:
    - "Euro Shopping Channel" from Spain
    - 	"Mini Gifts Distributors Ltd." From USA.
    -  Australian Collectors, Co." from Australia.
    -  La Rochelle Gifts" From France.
    -  Dragon Souveniers, Ltd." From Singapore.
    -  AV Stores, Co." From UK.
    -  Salzburg Collectables" From Austria.
    -  Danish Wholesale Imports" From Denmark.
    - L'ordine Souveniers" From Italy.
    - "Scandinavian Gift Ideas" From Sweden.
    - "Tokyo Collectables, Ltd" From Japan.
    - "Vida Sport, Ltd" From Switzerland.
    - "Baane Mini Imports" From Norway.
    - "Suominen Souveniers" From Finland.
    - "Toms Spezialitten, Ltd" From Germany.
    - "Cruz & Sons Co." From Philippines.
    - "Canadian Gift Exchange Network" From Canada.
    - "Petit Auto" From Belgium.
    - "Clover Collections, Co." From Ireland.
7. 	Top 10 global high value customers are:
    - "Euro Shopping Channel" From "Spain"
    - "Mini Gifts Distributors Ltd.” From "USA"
    - "Australian Collectors, Co." From "Australia"
    - "Muscle Machine Inc" From "USA"
    - "La Rochelle Gifts"	From "France"
    - "Dragon Souveniers, Ltd." From "Singapore"
    - "Land of Toys Inc."	From "USA"
    - "The Sharp Gifts Warehouse” From "USA"
    - "AV Stores, Co." From "UK"
    - "Anna's Decorations, Ltd" From "Australia"
8.	The top 10  Bestselling product  globally are:
    - "Classic Cars" with product code "S18_3232"
    - "Classic Cars" with product code "S10_1949"
    - "Classic Cars" with product code "S12_1108"
    - "Classic Cars" with product code "S12_3891"
    - "Classic Cars" with product code "S18_2238"
    - "Classic Cars" with product code "S18_3685"
    - "Classic Cars" with product code "S12_1099"
    - "Classic Cars" with product code "S18_1984"
    - "Trucks and Buses" with product code "S18_2319"
    - "Planes" with product code "S18_1662"
9.	Bestselling product in each product line are:
    - "Classic Cars" with product code "S18_3232”
    - "Motorcycles" with product code	"S10_4698"
    - "Planes" with product code	"S18_1662"
    - "Trucks and Buses"	with product code "S12_1666"
    - "Vintage Cars" with product code	"S18_1749"
    - "Ships" with product code	"S24_2011"
    - "Trains" with product code	"S18_3259


###  Recommendations
1.	More promotion such as social media marking, website develop and optimization content marketing etc. should be carried out to create more  awareness and showcase the benefits the company can offer.
2.	Rewards should be given to high value customers both globally and in each countries to appreciations and acknowledgement hence building a strong relationship.
3.	Classics cars should never be out of stock as it is the most sold.
4.	More awareness should be raised on other products with low sales.
### Limitations 
I encountered several inconsistencies and had to work on them in other to obtain accurate results.
