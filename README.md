# EDA-layoff
An extensive data analysis of the cleaned data from layoffs
Data analysis AFTER cleaning and standardizing the data

Multiple companies worldwide across 51 countries had a layoff statistics from 2020-2023.
during that time 2020 covid there was 80,998 layoffs across multiple companies but doesn't compare to 2023 which had 125,677 layoffs. 
2021 had the least amount of layoffs being 15,823. 
The industries with the highest layoffs were consumer and retail with 45,182 and 43,613 respectively. 
The lowest layoff was Manufacturing with 20 total layoffs.
Consumer industry layoffs: 6,063 (2020), 3,600 (2021), 19,856 (2022), 15,663 (2023).
retail laysoff 8002 in 2020 and 1088 in 2021 and then jumps 20914 in 2022 then 13609 in 2023.
Transportation laysoff 14656 in 2020 and 200 in 2021 then 2022 15227 and only 3665 in 2023
Travel layed off 13983 in  2020 and only 1637 in 2022 and 1539 in 2023.
The country with the most layoffs was UNITED STATES with 256559 then india with 35993.
september of 2022 to march of 2023 a spike in layoffs from a total of 176296 to a sudden jump to 383159 in total layoffs in a few months globally.
Meta layed off 11,000, Amazon layed off 10,150 , Cisco layed off  4100, Peloton layed off 4084, Carvana, and Philips tied with laying off 4000 all in 2022
Google layed off 12,000, Microsoft layed off 10,000, Ericsson layed off 8500, amazon layed off 8000 tying with Salesforce and lastly dell layed off 6650 all in the first 3 months of 2023.

Key Insights
Overall Trends:
Total layoffs increased from 80,998 in 2020 to 125,677 in 2023, with 2021 being the lowest at 15,823, reflecting initial pandemic impact, temporary recovery, and post-pandemic corrections.

Layoffs spiked from September 2022 to March 2023, with global totals jumping from 176,296 to 383,159 in a few months.

Industry Insights

Consumer & Retail: Most affected sectors with total layoffs of 45,182 and 43,613 respectively.

Consumer: 6,063 (2020) → 3,600 (2021) → 19,856 (2022) → 15,663 (2023)

Retail: 8,002 (2020) → 1,088 (2021) → 20,914 (2022) → 13,609 (2023)

Transportation: Large layoffs in 2020 (14,656), small dip in 2021 (200), resurgence in 2022 (15,227), and decline in 2023 (3,665).

Travel: Hit hard in 2020 (13,983), gradual recovery by 2022–2023.

Manufacturing: Least affected with only 20 layoffs across all years.

Geography

United States had the highest layoffs at 256,559, followed by India at 35,993.

Tech hubs in the U.S. (Silicon Valley, Seattle, NYC) contributed disproportionately to global layoffs.

Top Companies by Year

Year	Company	Layoffs
2020	
  Uber	7,525
	Booking.com	4,375
	Groupon	2,800
	Swiggy	2,250
	Airbnb	1,900
2021	
  Bytedance	3,600
	Katerra	2,434
	Zillow	2,000
	Instacart	1,877
	WhiteHat Jr	1,800
2022
  Meta	11,000
  Amazon	10,150
	Cisco	4,100
	Peloton	4,084
	Carvana/Philips	4,000
2023	
  Google	12,000
	Microsoft	10,000
	Ericsson	8,500
	Amazon/Salesforce	8,000
	Dell	6,650
Note: Companies tied in layoffs are listed together.

Observations:
Tech Industry: Experienced massive layoffs post-pandemic after initial growth during 2020–2021.
Travel & Transportation: Volatile due to pandemic restrictions; heavy layoffs in 2020, recovery in 2021–2023.
Consumer & Retail: Layoffs were cyclical, possibly reflecting market demand and economic shifts.
Key months: Significant layoffs globally occurred between September 2022 – March 2023, aligning with economic corrections after COVID recovery.

Query to list the top 5 companies by layoffs per year (note I used a lot of other queries but this is the one i used for the last observation)
WITH Company_year (company, years, total_laid_off) as 
(
Select company, YEAR(`date`), SUM(total_laid_off)
FROM layoffs_staging2
group by company, YEAR(`date`)
), Company_Year_Rank as
(Select *,
DENSE_RANK() OVER (Partition by years Order by total_laid_off DESC) As ranking
From Company_year
Where years is not null
)
select *
from Company_Year_Rank
Where Ranking <= 5;

