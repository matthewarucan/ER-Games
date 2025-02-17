![](assets/GAMING-min.png)

# ER-Games

# 1. ASK Phase (Defining the Problem & Business Goals)

## 1.1: Key Questions to Answer
- How can ER Games align its new puzzle-RPG hybrid game with current industry trends?
- Besides the US, which international markets should ER Games focus on?
- How do changing consumer preferences and demographics influence ER Games' marketing and sales strategy?

## 1.2: Business Context
ER Games is a small company competing against larger RPG game studios. They have released a demo to test consumer interest and identify target demographics. Founder’s View: Market the game outside the US first (especially in Japan & Europe). Consultant’s View: Launch globally without a phased approach.

## 1.3: Stakeholders
- James Spier: ER Games founder

# 2. PREPARE Phase (Collecting & Understanding the Data)

## 2.1 Data Sources:
Console Data (Game Sales & Reviews)
- Name, platform, genre, developer, publisher, release year.
- Sales data: NA, Europe, Japan, and Other regions.
- User & critic reviews: Ratings & number of reviews.
- ESRB ratings: Audience appropriateness.
- Population Data (Market Size & Trends)
- 8064 Entries, 15 Columns

Population Data (1995-2017) for different countries.
- Country Name: name of the country
- Country code: code of the country used in public data
- All other variables from 1995 to 2017: population of the country in that year
- 265 Entries, 25 Columns

## 2.2: Data Credibility and ROCCC Assessment

I will use ROCCC to assess whether this data has issues with bias or credibility.

- **Reliable**: Sales data is likely accurate, but critic & user reviews may contain bias or gaps. Population data is reliable if sourced from reputable databases.
- **Original**: The console data comes from a third-party source (likely a gaming database or review aggregator). The population data is from a public dataset (likely a government or UN source). The credibility depends on the reputation of these sources.
- **Comprehensive**: Game data is detailed (genre, platform, sales, reviews), but user demographics are missing. Population data lacks breakdowns like age groups or gaming habits.
- **Current**: No, the data is not current. Population data stops at 2017 (not fully up-to-date). Game data’s relevance depends on its last update—if recent, it’s useful; if outdated, trends may not align with 2025 market dynamics.
- **Cited**: Not explicitly mentioned. We need to verify the sources of the datasets.

# 3: PROCESS PHASE
In the process phase, we ensure our data is clean by correcting or removing inaccurate, corrupted, improperly formatted, duplicate, or incomplete entries within the dataset.

##### Preview of our Raw Console Data
![](assets/raw_data.png)

##### Preview of our Raw Population Data
![](assets/raw_data_population.png)

## 3.1: Reviewing Our Data in Excel
We open your worksheet to review headers, data types, and any obvious issues such as extra spaces or misformatted dates. We also adjust column sizes to ensure clear visibility of the data. Additionally, locking the header columns keeps the column labels visible while scrolling horizontally through a large dataset, making it easier to identify which data corresponds to each column (View -> Freeze First Column). Lastly, we want to add commas separating our numbers to read it easier.

#### 3.1.1: Quick Filtering
We want to quickly filter our data to check for any NULL, NA, or 0 values. Use Data → Filter to review unique values and identify any irregularities in each column.

## 3.2: Data Cleaning
#### 3.2.1: Remove Extra Spaces and Standardize Text Case
We want to remove extra spaces using the TRIM function on our text data to eliminate leading, trailing, or extra spaces.

To ensure consistency (e.g., names in proper case), we use the PROPER function in Excel to capitalize the first letter of each word in a text string. It also capitalizes any other letters that follow a non-letter character. 

We conduct these steps for each column involving text so that it prevents lookup errors caused by inconsistent spacing or casing.

#### 3.2:2: Remove Duplicate Rows
We want to eliminate rows that are completely duplicate data in the whole row. In the Remove Duplicates dialog box, make sure the 'My list has headers' checkbox is selected if your dataset includes headers. To ensure that an entire row matches exactly before a duplicate is removed, check all columns so that Excel compares the values in every column of each row. If any columns are left unchecked, Excel will only use the selected columns to determine duplicates, which may result in partial matches rather than complete row duplicates.

## 3.3: Adding Column for Console Data
We aim to add and calculate new columns to better address our key questions: How can ER Games align its new puzzle-RPG hybrid game with current industry trends? Beyond the US, which international markets should ER Games prioritize? And how do shifting consumer preferences and demographics impact ER Games' marketing and sales strategy?

#### 3.3.1: Critic and User Score Region Weight for Europe, Japan, and North America
By combining sales and reception data, ER Games can gain deeper insights into its game's performance, as sales alone may be driven by hype or brand recognition rather than genuine enjoyment. Critic and user scores provide a crucial layer of quality perception, helping to determine whether players truly appreciate the game or if sales are influenced by other factors. This approach enables ER Games to assess not only revenue but also customer satisfaction across different regions.

We create 6 new columns: critic score eu region weight, critic score jp region weight, critic score na region weight, user score eu region weight, user score jp region weight, and user score na region weight.

For the critic score region weight, we multiply the region's sales for a specific game by the critic score, and vice versa for the user score.

##### User Score Region Wight Formula (e.g. =IFERROR(G2*L2, "0"))
![](assets/user_score_region_weight.png)

##### Critic Score Region Wight Formula (e.g. =IFERROR(G2*J2, "0"))
![](assets/critic_score_region_weight.png)


# 4: ANALYZE PHASE
In this step, we calculate key metrics, analyze patterns, and summarize data to provide insights that address our business objectives.

#### Graph 1: Average Region Sales Per Genre
![](assets/genre_sales_avg_region.png)
Using the console data, we create a pivot table with values in the columns and genres in the rows, calculating the average of 'na_sales,' 'eu_sales,' and 'jp_sales.' The highest average sales are for role-playing games in Japan and shooter games in the EU and NA regions.

#### Graph 2: Average Region Sales Per Gaming Platform
![](assets/plateform_sales_avgregion.png)
Using the console data, we created a pivot table with platform names in the rows and sales values in the columns, calculating the average for 'na_sales,' 'eu_sales,' and 'jp_sales.'

Overall, the consoles with the highest average sales include the PS4, Wii U, and Xbox 360. The top-selling console by average game sales varies by region: the PS4 leads in North America, the 3DS in Japan, and the Xbox 360 in Europe.

#### Graph 3: Sales Per Capita Over Time by Region
![](assets/sales_per_capita_year.png)
We create a pivot table with 'year_of_release' in the rows, 'Values' in the columns, and 'Sum of eu_sales' and 'Sum of jp_sales' in the values. Next, we determine the population of Japan and the EU for each year using VLOOKUP to retrieve these values from the population table (e.g., =VLOOKUP(E$3, 'Population Count'!$A$3:$S$7, 2, FALSE)). Once we obtain the population count for each year, we calculate sales per capita by dividing sales by the corresponding population count (e.g., =C4/E4). Finally, we compute the average sales per capita for each region.

#### Graph 4: Population For Each Region
![](assets/population_per_region.png)
We create a simple pivot table with 'Country Name' as our columns, 'Values' as our rows, and the sum of sales for each year as the values. The data shows an exponential population increase in the EU and US, while Japan's population experiences a significant decline.

#### Graph 5: Weighted Average User Score by Genre and Region 
![](assets/user_score.png)
We create this histogram by generating a pivot table with 'genre' and 'values' in the rows and the following metrics in the values section: 'sum of user score EU region weight,' 'sum of user score NA region weight,' 'sum of user score JP region weight,' 'sum of EU sales,' 'sum of JP sales,' and 'sum of NA sales.' This results in a pivot table that breaks down each genre by these values.

To calculate the weighted average user score for each region, we divide the 'sum of user score region weight' by the 'sum of region sales.' The weighted average user score represents overall player satisfaction in different regions, adjusted for the number of units sold. Our analysis shows that Japan consistently has the highest weighted average user score across all gaming genres compared to the EU and NA.

#### Graph 6: Weighted Average Critic Score by Genre and Region
![](assets/critic_score.png)
We follow the same steps as in 'Graph 5,' but instead of using the user score, we use the critic score. To create this histogram, we generate a pivot table with 'genre' as the row variable and the following metrics in the values section: 'sum of critic score EU region weight,' 'sum of critic score NA region weight,' 'sum of critic score JP region weight,' 'sum of EU sales,' 'sum of JP sales,' and 'sum of NA sales.' This pivot table categorizes each genre by these values.

To calculate the weighted average critic score for each region, we divide the 'sum of critic score region weight' by the 'sum of region sales.' This weighted average critic score reflects overall player satisfaction in different regions, adjusted for the number of units sold.

Our analysis shows that Japan has the highest critic scores for most gaming genres, except for role-playing, action, and shoo

#### Graph 7:
![](assets/Puzzle-Sales-Per-Capita.png)
Breaking down the sales per capita over time by region for the Puzzle genre in Japan and the EU, we see that puzzle game sales across all consoles are trending downward overall.

#### Graph 8:
![](assets/role-playing-sales-per-capita.png)
Breaking down the sales per capita over time by region for the Role-Playing genre in Japan and the EU, we see that Japan has had a higher sales per capita every year. Japan's sales per capita peaked in 2008 at nearly 0.120, while the EU's peak occurred in 2011 at 0.026.

#### Graph 9: Regional Market Share of Puzzle/Role-Playing Games on Non-PC Platforms
![](assets/marketshare-non-pc.png)
Europe and North America are the primary markets for PC-based Puzzle and Role-Playing games, with the EU maintaining a dominant share over time. In contrast, Japan's contribution to these genres on PC is minimal, suggesting a stronger preference for other platforms, such as consoles. Sales distribution fluctuates year by year, with occasional spikes in North American sales, but overall, the European market remains the most significant.

#### Graph 10: Regional Market Share of Puzzle/Role-PLaying Games on PC Platforms
![](assets/marketshare-pc.png)
North America is the largest market for Puzzle and Role-Playing games on non-PC platforms, with Japan and Europe following closely behind. Unlike the PC market, Japan plays a significantly larger role in non-PC sales, reinforcing the idea that Japanese gamers prefer consoles and handheld devices for these genres. Additionally, the non-PC market exhibits a more balanced and stable sales distribution over time compared to the fluctuations seen in the PC market.


# 5. SHARE AND ACT PHASE
# ER Games Market Strategy Analysis

## 1. How can ER Games align its new puzzle-RPG hybrid game with current industry trends?
The data suggests that **Japan is a strong RPG market**, historically showing the highest sales per capita for the genre.  
Puzzle games, on the other hand, have seen a **decline in sales per capita across all regions**.

### Strategy:
- **Hybrid Approach:** Since ER Games is making a **Puzzle-RPG hybrid**, they should focus on **highlighting RPG mechanics** while incorporating puzzle elements strategically.
- **Platform Strategy:** Japanese gamers tend to prefer **consoles and handhelds over PC** for these genres. ER Games should prioritize **console releases in Japan** over PC.
- **Critical Reception & Quality:** Japan has **higher weighted user and critic scores for RPGs**. High-quality gameplay and storytelling will be crucial for success.
- **Marketing Strategy:**  
  - Emphasize **role-playing aspects in Japan**.  
  - Leverage **puzzle mechanics in Europe and North America**, where the genre balance is more even.

## 2. Besides the US, which international markets should ER Games focus on?
- **Japan:** The **highest RPG sales per capita historically** suggest that Japan is a key market.
- **Europe:** Has a **higher overall sales per capita than Japan (0.21 vs. 0.19)**, meaning more games are sold per person.

### Regional Differences:
- **Japan remains a strong RPG market** and should be targeted for the RPG aspect of the game.
- **Puzzle games in Japan and the EU are now on par**, meaning **Europe has more potential for growth in this genre**.
- **North America is the largest non-PC market**, but **Europe has a more stable sales distribution**.

### Action Plan:
- Prioritize **Japan for RPG-focused marketing**.
- Position **Europe as a key puzzle-game market**.
- Implement a **console-first approach** to align with platform preferences.

## 3. How do changing consumer preferences and demographics influence ER Games' marketing and sales strategy?
- **Demographic Shift:** Japan’s **declining population** suggests a **shrinking market size**. However, their **strong RPG preference** means they are still a core audience.
- **Puzzle Genre Decline:** Puzzle game sales have been **trending downward**, so ER Games should ensure its puzzle mechanics **enhance rather than replace RPG elements**.
- **Platform Preferences:** Since Japan prefers **consoles and handhelds over PC** for these genres, ER Games should optimize for **console-first development**.
- **Sales Stability:** The **non-PC market is more balanced and stable** than the PC market, meaning ER Games should expect **steadier sales if targeting consoles**.

### Marketing Adjustments:
- **Japan:** Focus on **storytelling and RPG depth** to attract dedicated RPG fans.
- **Europe:** Leverage **puzzle-solving mechanics** as an engagement hook.
- **North America:** Position the game as a **hybrid experience that blends strategy (puzzle) with adventure (RPG)**.








