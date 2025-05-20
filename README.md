# Customer Journey Analysis: Evaluating Traffic Sources & Conversion Paths
Understanding how customers navigate the Google Merchandise Store is critical for optimizing marketing strategies. This analysis leverages Markov Chain Attribution to assess the impact of different traffic sources—such as direct visits, paid search, and display ads—on conversions. By modeling customer paths, which can identify channels contribute most to revenue and where marketing resources should be allocated for maximum return on investment.

<p align="center">
    <img src="MarkovChainDiagram.svg" width="600" height="500" />
</p>

The above displayed is a Markov Chain diagram that maps out the visitors traffic source sequences — similar to an amusement park map that shows all the attractions and the paths between them. But instead of just showing the routes, this map also displays the proportion of visitors moving from one point to another, giving insight into how users navigate toward a final destination (conversion). In evaluating the proportions, this helps to uncover how different traffic sources contribute to conversions, providing actionable insights into customer behavior.

**Key Insights**

1. Direct, paid search and organic search dominate high-converting paths.
2. Direct Traffic shows strong late-stage influence and initial engagement.
3. Referrals contribute to early awareness but require retargeting to drive conversions.
4. Multi-touch attribution reveals that most conversions involve direct, display ads, and paid search, potential improvement on revenue and conversion by leading traffic to those sources with cross-channel strategies.

**Navigation of Analysis**

For transparency and reproducibility, this project includes the following resources in the `vscode` and `data` folder:

- `Data Extraction.ipynb`: Extracts data of the Google merchaandise store [link](https://bigquery.cloud.google.com/table/bigquery-public-data:google_analytics_sample.ga_sessions_20170801) on Google Cloud using SQL queries and Python, cleaned datasets stored in `agg_data.zip`.
- `Multi-touch Attritbution.ipynb`: Analysis on customers' (visitors') journey on the store website.
- `agg_data.zip`: Contains all extracted datasets from Data Extraction.ipynb.

## Data
The data is a public data of the Google merchandise store on Google Cloud with information of the website visits between August 2016 to August 2017. The following attributes were extracted for the analysis:

- fullVisitorId: Visitor ID.
- date: Date of the visit.
- transactions: The number of transactions during this visit.
- transactionRevenue: Total money spent on the website during this visit.
- source: The name of the access source the visitor used to visit the store website. (e.g. google.com, facebook.com, etc.)
- medium: The general access source the visitor used to visit the store website. (e.g. direct, referral, search, etc.)

Most variable are accurate to their definitions, exccept there are missing medium in the website, its impact will be assessed before deciding how to treat them. 

## Results
### Exploratory Data Analysis
The following is the word cloud of all the source and medium from all visits:
<p align="center">
    <img src="wordclouds.svg" width="1000" height="500" />
</p>

- The most common way of visitors assessing the website is 'direct', following through the sources from 'Partners', 'youtube' and 'google', such as advertisements and paid search.
- Direct and Referral is the most common assess to the website by visitors. There are a few visits with unknown medium from Google Analytics.



| Medium   | Total Visits (%) | Revenue in Billions ($) |
| -------- | ------- | -----------------------|
| Direct  | 41.11 |  1190  |   
| Search | 29.00 |  205  |
| Display Ad | 25.94 | 78  |
| Referral | 1.82 | 40 |
| Paid Search | 1,45 | 25 |
| Affiliate | 0.68 | 0.59 |
| Unknown | 0.01  | 0.001 |
| All | 100 | 1538.591 |

From the above table:
- Around 41% of visits were by direct, and the reveneue generated is significantly greater than the other mediums.
- The unknown visits are only the 0.01% of all visits, with less than 0.01 percent (< 0.001 / 1538.591)revenue generated from the grand total revenue. Since the medium cannot be traced back, removed the unknown visits.


The following figure shows the average revenue generated and total transactions made by medium:
<p align="center">
    <img src="transactions_avg_revenue_with_ci_by_medium.svg" width="1000" height="500" />
</p>

- 'Direct' and 'Search' has the highest number of transactions (around 8000 and around 2000), then followed by 'Display Ad', 'Paid Search', and 'Referral', lastly, 'Affiliate' being the least.
- 'Display Ad' has a significantly higher average revenue by transaction at 0.5 billion dollars per transaction, so it is most likely to attract high-value customers. The other mediums has around 0.1 billion dollars per transaction, except for 'Affiliate' at around 0.05.

From the above observations, most visits were made with direct or organic search assess, where majority of the revenue came from. Implying that it is more likely that transactions were made by returning visitors or visitors that knows the website or the store, but this is not a factor that can be easily improved or controlled. From other medium, 'Display Advertisemnt' has the highest potential in genenrating revenue, and improving the quality of the advertisements that tailor towards the target audiences, which can lead to an increase of visits and transactions. 

### Markov Chain Attribution Model
The following is a heatmap of the transition matrix of the percentage of visits from sources to sources of the starting source, which also includes:

- 'start' the starting point when the visitor first assess the website since August 2016.
- 'null' as the end point of most recent visits before August 2017.
- 'conversion' is when the visitor converted and made a purchase on the website.

For example, from 'start' to 'Affiliate', there is a 1.8\% of all visits starting at 'start' that ends at 'Affiliate'.
<p align="center">
    <img src="transition_matrix.svg" width="1000" height="800" />
</p>
The main observations are:

- The three main entry source of the website is 'Direct' (38\%), 'Referral' (26\%), and 'Search' (33\%), which most visitors were introduced to the website from those sources. The other sources have less than 2\%. 
- Most purchases and conversiosn occurred through 'Direct' (1.2\%), 'Display Ad' (1.1\%), and 'Paid Search' (0.93\%).
- The sources with the highest 'null' percentage are 'Referral', 'Search', and 'Affiliate', implying these sources are more unlikely to keep visitors and customers to return to the website.
- For the source to source interactions, the path to the same sources has second highest percentage right under 'null'. 'Paid Search' and 'Display Ad' has a higher percentage (2.2\% and 4.4\%) of visits going to 'Direct'; 'Paid Search' has the highest percentage (1\%) going to 'Display Ad', and 'Display Ad' has a similar percentage (0.86\%) going to 'Paid Search'.

## Recommendations
- Most visits and revenue were generated from organic search and direct assess, suggesting that most purchases were likely made by returning visitors since the visitors must have known the website. Therefore reallocate budget on the sources that are more likely to keep visitors revisiting, being paid search and displayed advertisements, improving and investing more on the quality and quantity of these sources. Furthermore, paid search and displayed advertisements have higher conversion rate compared to the other sources. 
- On the other hand, drop affiliation if they make losses since affilate has the lowest conversion rate and high exit percentage compared to other sources. Even though referral also has a high exit percentage, it is one of the main source that introduce visitors to the websites that can be controlled by the company, so it is better to keep and maintain partnerships in referrals.

## Questions
- Is 'IsTrueDirect' a reliable label for true direct access? Unable to check the labeled visits based on the data. 
- What's the commission rate for different partnerships? This determines whether affiliate is making losses throughout the year, and relocate budget to different partners that can make referrals to the target consumers based on return of ad spent (ROAS). Can the commission be renegotiated?
- Why does referral have a high exit percentage? Which referral site drives the most high-intent traffic? And can we exclude spam referrals?
