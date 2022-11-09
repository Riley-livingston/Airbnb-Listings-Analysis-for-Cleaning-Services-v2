<img src="https://i.imgur.com/OcLOedO.jpg" height = "100%" width="100%" alt = ">Airbnb Analysis for Cleaning Services"/>

<h1>Airbnb Analysis for Cleaning Services in NYC v2 - Active Directory </h1>
<h2>Key Findings</h2>

The predicted impact of every dirty review on a listing is -0.21 days booked out of 90. However, at the 95% confidence level, dirty reviews per listing's impact on days booked out of 90 is insignificant with a p-value of 0.138 and an overall model fit (R²) of 0.126.
 


<h2>Authors</h2>

<a href="https://github.com/Riley-livingston"> @RileyLivingston</a>

<h2>Description</h2>
This project consists of exploritory analysis and a multivariate linear regression of publicly available Airbnb data. This directory will guide you through the steps I took and thought process in determining the relationship between dirty reviews in Airbnb listings and days booked out of 90. version 1 of the Airbnb Listings Analysis for Cleaning Services project can be found <a href="https://github.com/Riley-livingston/AirBnb-Listings-Analysis-for-Cleaning-Services"> here. </a>

<br />

<h2>Languages and packages used</h2>

- MySQL
- Python 3.10 | Numpy | Pandas | Sklearn
  

<h2>Environments used </h2>

- VScode
- Jupyter Notebook
- Dbeaver 22.2.2

<h2>Data source</h2>

- <a href="https://drive.google.com/drive/folders/1Q2yFaDajfJ6hALKMCmrQbHnFhsti44bO?usp=sharing"> Airbnb detailed listings and reviews data NYC 09-07-2022</a>
- <a href="https://docs.google.com/spreadsheets/d/1iWCNJcSutYqpULSQHlNyGInUvHg2BoUGoNRIGa6Szc4/edit#gid=1322284596"> Data dictionary</a>

<h2>Methods</h2>

- Exploratory data analysis
- Multivariate linear regression

<h2>Data analysis process</h2>

<p align="left">
 <u>Business task</u>:
 
- Determine if there is a relationship between reviews that indicate uncleanliness of an airbnb listing and days booked out of a 90 day period.
- If that relationship exists, what is the impact of every dirty review on average days booked out of 90 for a listing on Airbnb in NYC's 5 boroughs.
 
  - KEY METRICS
    - p-value, or statistical significance of the beta coefficent of the dirty_review variable/feature on days booked out of 90 for a listing.
 
    - the vaule of the beta coefficent of the dirty review variable used in the model. A positve coefficent would indicate that dirty reviews have a postive impact on bookings while a negative beta coefficent would indicate a negative effect. Larger or smaller beta coefficents would indicate a larger impact on bookings.

    - R² or overall fit of the model. An R² closer to one would indicate that the model is really good at predicting bookings fot the next 90 days.
 
<br />
<p align="left">
 <u>Data preparation</u>: 
 
  PRIVACY AND ACESSABILITY
 
   - Data for this analysis was scrapped directly from Airbnb's website by third party <a href="https://insideairbnb.com"> insideairbnb</a>.
   - All data present in this repository as well as findings derived from analysis is publicly available information and falls under fair use. No private         information is being used including names, listings, and review details as it is all publicly displayed on Airbnb’s website.
   
 <br/>
  DATA STRUCTURE AND INTEGRITY
 
   - Data used in this analysis is organized in 2 tables (listings and reviews) and columns in csv format. 
   - Integrity of the data source was verfified by choosing 10 random listings urls from the listings table listing_url column and comparing the information from the link to the infromtion scrped and organized into columns in the reviews and listings tables.

 
<br />
<br />
<u>Documentation of data processing and cleaning</u>: <br/>
  - <a href="https://github.com/Riley-livingston/Airbnb-Listings-Analysis-for-Cleaning-Services-v2/blob/main/dirty_reviews_v2.sql"> SQL script to clean and filter the data.sql</a>
 <br />
  - <a href="https://github.com/Riley-livingston/Airbnb-Listings-Analysis-for-Cleaning-Services-v2/blob/main/clean_and_filtered_airbnb_data_v2.csv"> Cleaned and filtered data.csv</a>
 <br />
 <br />
<img src="https://i.imgur.com/AKSoy6j.png" height = "100%" width="100%" alt = ">SQL select statement with explaination"/>
   - From the listings table, host_id, host_name, and host_url are selected. host_url and host_id are used as primary keys for the listings table to unqiuely identify each host.
 <br />
 <br /> 
   - Host_total_listing count and number_of_reviews are selected and casted as integers. This turns all non-numerical data in both of those columns into NULL. The data is also tranformed to be used with operators and aggregations if needed.
 <br />
 <br />
   - Distinct comments are counted, selected from the reviews table, and aggregated into a new column called dirty_review_count that will count all distinct reviews that contain specified 'dirty review' words.
 <br />
 <br />
<img src="https://i.imgur.com/Vhpkstx.png" height = "100%" width="100%" alt = ">SQL Join statement and conditions for dirty reviews with explaination"/>
   - An inner join is made between the listings and reviews tables, returning columns where the listing id matches the id field from the review table AND where airbnb listing reviews in the comments column of the review table contain at least one of the specified dirty words contained in the LIKE statements.
 <br />
 <br />
<img src="https://i.imgur.com/HSBhnqs.png" height = "100%" width="100%" alt = ">SQL more filtering and group by order by conditions with explaination"/>
    - The inner join between the lstings and reviews tables are further filtered under the condtions that the length of the review_score_rating and review_score_cleanliness ratings are no greater than 4 characters in length.
  <br />
  <br />
    - The maximum number of reviews of any given listing is 999 so the maximum length of the number_of_reviews column was set to 3 in order to filter out potential invalid data.
  <br />
  <br />
    - The query is fianlly grouped by host_id and host_url and then ordered by the total number of dirty reviews counted in descending order as a way to gain immediate insight into potential customers to contact for cleaning services.
  <br />
  <br />
  <br />
<u>Analysis</u>:  
  <br/>
  <br />
 - In Tableau, dirty reviews per listing were calcualted for each host and the results were sorted in descending order. 
 <br />
 <br />
 - I constructed a dual axis barchart showing the top 25 hosts in the NYC's 5 boroughs sorted by dirty reviews per listing and total dirty reviews. In the tooltip, I embeded the link to the hosts unique Airbnb Url so that if the dashboards are used as a potential client list, contact information will be easily acessable.
 <br />
 <br />
 - Accross all hosts, median, 90th, and 99th perentiles for dirty reviews per listing were calculated.
 <br />
 <br />
 - I included a <a href="https://public.tableau.com/app/profile/riley.livingston/viz/Airbnbdirtyreviewproject/Dashboard2?publish=yes"> dynamic histogram </a> that can be used as a filter for targeting hosts in a specific dirty review per listing bin. To use this, click on a bin and the packed bubble diagram will filter results to only include hosts from the bin you selected.

 <br />
 <br />
 <u>Key findings</u>:
  <br />
  <br />
  - 10% of Airbnb hosts have at least 4 dirty reviews per listing. The top 1% of Airbnb hosts have at least 12.84 dirty reviews per listing.
  <br />
 - The Average Airbnb host has 1.9 dirty reviews per listing.
  <br />
 - The top 25 Airbnb hosts have between 9 and 43 dirty reviews per listing.

<br/>
<br/> 
   <img src="https://i.imgur.com/EZkpI68.png" height = "100%" width="100%" alt = "Results Snapshot: Top 25 Hosts sorted by dirty reviews per listing"/>
<br />
<br />
   <img src="https://i.imgur.com/PQiOiG5.png" height = "100%" width="100%" alt = "Results Snapshot: Distribution and percentiles of Dirty Reviews per listing grouped by host"/>
<br />
<br />
 <img src="https://i.imgur.com/lJwsSmK.png" height = "100%" width="100%" alt = "Results Snapshot: Distribution and percentiles of Dirty Reviews per listing grouped by host"/>
<br />
<img src="https://i.imgur.com/jL6f58Y.png" height = "100%" width="100%" alt = "Results Snapshot: Distribution and percentiles of Dirty Reviews per listing grouped by host"/>
<br />
<img src="https://i.imgur.com/c17Qvlf.png" height = "100%" width="100%" alt = "Results Snapshot: Distribution and percentiles of Dirty Reviews per listing grouped by host"/>
<br />
<img src="https://i.imgur.com/CMc4eOX.png" height = "100%" width="100%" alt = "Results Snapshot: Distribution and percentiles of Dirty Reviews per listing grouped by host"/>
<br />
<img src="https://i.imgur.com/iQ55qYy.png" height = "100%" width="100%" alt = "Results Snapshot: Distribution and percentiles of Dirty Reviews per listing grouped by host"/>
<br />
<br />
  - The data and results of the analysis are a snapshot of listings available from Airbnb on and before September 7th 2022. Hosts may remove or add listings at anytime and renters may post or delete reviews at anytime which may impact the results of the analysis. Seasonality bias may be present in the number of reviews that contain 'dirty' words indicating uncleanliness.</b>
<br />
<br />
  - The words used to measure dirty reviews are all weighted the same but each dirty review may differ in the severity of the uncleanliness which would impact bookings and be of greater interest to a cleaning service looking for clients.
<br />
<br />
  - A list of 15 words was selected to search for dirty reviews in the communts column of the reviews table. This list may not represnted all of the ways a person would describe uncleanliness and lead to some reviews not being included in the analysis.
<br/>
<br/>
 Future improvements:
<br/>
<br/>

