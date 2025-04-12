# Customer Journey Analysis Using Markov Chain Attribution
Understanding how customers navigate an e-commerce website is crucial for identifying the most effective traffic sources and support marketing decision making. This repository applies Markov Chain Attribution to analyze website traffic, evaluating the impact of various acquisition channels such as direct visits, paid search, and display ads. 

<p align="center">
    <img src="MarkovChainDiagram.svg" width="600" height="500" />
</p>

The above displayed is a Markov Chain diagram that maps out the visitors traffic source sequences — similar to an amusement park map that shows all the attractions and the paths between them. But instead of just showing the routes, this map also displays the proportion of visitors moving from one point to another, giving insight into how users navigate toward a final destination (conversion). In evaluating the proportions, this helps to uncover how different traffic sources contribute to conversions, providing actionable insights into customer behavior.

**How to use**:

- 'Data Extraction.ipynb': Extracts public data [link](https://bigquery.cloud.google.com/table/bigquery-public-data:google_analytics_sample.ga_sessions_20170801) on Google Cloud.
- 'Multi-touch Attritbution.ipynb': Analysis on customers' (visitors') journey on the e-commerce's website.
- 'Source Performance over Time.ipynb':  Evaluates traffic source performance and forecasts revenue trends.
- 'agg_data.zip': Contains all extracted datasets from Data Extraction.ipynb.

This analysis helps businesses allocate marketing resources more effectively by understanding the influence of different acquisition channels on conversion rates.

## Main Results
### Multitorch-Attribution Model
The following is the transition matrix of the conversion rate from sources to sources, evaluated the likelihood of the visitors going from source to source. 
<p align="center">
    <img src="transition_matrix.svg" width="1000" height="800" />
</p>

