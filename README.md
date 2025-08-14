# Spotify Personal Streaming Analysis  

**By Nick Gasperi**

<p align = "center">
  <img src = "images/spotify-wrapped-dashboard.png">
</p>

## **Project Background**
### **Introduction**
This project analyzes my personal Spotify streaming history from 2015–2024 to uncover listening habits and the evolution of my music taste. Having been asked *"What kind of music do you listen to?"* more times than I could count, I began to wonder myself, and decided to explore my cumulative streaming history to find the answer. By identifying trends in when, how, and what I streamed, this analysis aims to draw objective conclusions about how my listening preferences have developed over time and develop recommendations to maximize my future streaming experience.

### **About the Data** <br>
The dataset used in this analysis contains detailed records of my personal streaming activity throughout the full lifespan of my Spotify account from 2015–2024. Each row represents a streamed song or podcast episode and includes metadata such as the date-time stamp, identifying variables like track or episode name and artist or podcast name, and quantitative measures such as duration played. The data was delivered from Spotify via email, stored in 23 JSON files containing 327,123 total records. All files were aggregated into one useable dataset titled *full_streaming_history* using Power Query.

## **Executive Summary**
From 2015–2019, the total annual hours streamed on my Spotify account increased by over 1100%, reflecting a period of rapidly growing engagement. From 2019-2024, annual streaming volume remained relatively stable, decreasing by a marginal 0.8%. Streaming frequency varied by day of week and season. Weekday activity was consistently higher than weekends, streaming 24% more hours Monday–Friday on average. My streaming frequency also experienced seasonality, dipping notably during the summer months. Monthly streaming dropped by 64% from my most active period in December to my least in August. Peak listening hours occurred between 12:00–2:00 P.M. and 7:00–9:00 P.M. <br>

During the earlier years of my account, I frequently skipped tracks while exploring a wide range of new artists, peaking in 2019 with a skip rate of 54%. Skip rates steadily declined year-over-year, falling to 33% in 2024, while exploring just 3% fewer unique artists. My most-streamed artists from 2015–2020 were rappers; since 2021, each annual top artist has been a rock band. By 2024, my listening profile included a more balanced mix of media types, with annual podcast consumption increasing by 30% from 2019–2024.

## **Data Preparation**
### **Data Aggregation**<br>
* Loaded all 23 files into Power Query and used *Append Queries as New* to insert all records into one usable dataset titled ***full_streaming_history***.
  * Since the column names and data structure in each original source file matched, no additional manipulation was required to standardize the data.
* After combining the datasets, I would typically disable loading for each individual query to optimize model performance. However, since each source file contains sensitive personal information, I removed them completely.
  * Before deleting the individual queries, I created a static duplicate of ***full_streaming_history*** to eliminate external dependencies and secure the model for public sharing.

### **Data Cleaning**
Deleted Columns

* ***ip_addr***, ***conn_country***, and ***platform*** to protect sensitive personal information.
* ***audiobook_title***, ***audiobook_uri***, ***audiobook_chapter_uri***, and ***audiobook_chapter_title***, as audiobooks are not a significant part of my listening profile.
* ***incognito_mode***, as this feature was never used on my account.

Renamed Columns

* *spotify_track_uri* → ***track_id***
* *spotify_episode_uri* → ***episode_id***
* *master_metadata_track_name* → ***track_name***
* *master_metadata_album_artist_name* → ***artist_name***
* *master_metadata_album_album_name* → ***album_name***
* *episode_show_name* → ***show_name***

Created Columns

* ***sec_played***, ***min_played***, and ***hrs_played*** as alternative measures of record duration.
* ***month_streamed***, ***hr_of_day_streamed***, and     ***day_of_week_streamed*** to facilitate analysis of listening patterns.
* ***month_abbr*** to include abbreviated month names.
* ***day_of_week_id*** and ***month_abbr*** to override default alphabetical sorting of categorical data.
* ***is_track*** to indicate records representing songs and ***is_episode*** to indicate podcast episode records.
* ***media_type*** to assign either 'Track' or 'Episode' to each record for labeling visuals.

Changed Data Types

* Converted all indicator variables from TRUE/FALSE to 1/0 (Whole Number) for compatibility in visuals.

## **Summary of Insights**
### **When I Listened: Temporal Patterns**
* Total annual streaming hours increased by 1112% from 2015–2019. Streaming has remained consistent since 2019, with a change of -0.8% in total hours from 2019–2024.

<p align = "center">
  <img src = "images/spotify-hours-by-year-.png" style="width:480px">
</p>

* I most frequently streamed from 12:00–2:00 P.M., with an additional spike from 7:00–9:00 P.M.
* Weekday streaming was consistent between days and mirrored the overall time-of-day pattern. Weekend activity was lower overall and exhibited no significant temporal patterns.

<p align = "center">
  <img src = "images/spotify-timing-plots.png">
</p>

* Total streaming frequency varied seasonally. Three of the four highest-volume months occurred in the fall (October–December), while the four lowest-volume months fell in the summer (June–September).
* Total streaming hours dropped 64% from the highest-streaming month (December) to the least active month (August).

<p align = "center">
  <img src = "images/spotify-hours-by-month-.png" style="width:480px">
</p>

* Within the overall seasonal trend, music and podcast streaming exhibited differing seasonal patterns. Since music accounts for 86% of my total lifetime streaming, monthly song volume predictably folllowed the overall streaming trend. Conversely, podcast activity exhibited an inverted seasonal trendline.
  
<p align = "center">
  <img src = "images/spotify-songs-podcasts-by-month-.png" style="width:480px">
</p>

### **How I Listened: Streaming Behaviors**

* The percentage of songs I skipped peaked in 2019, skipping 54% of tracks prior to completion. Starting in 2020, my skip rate steadily declined, dropping to 33% in 2024.
* Each year since 2020, I completed more songs than I skipped.

<p align = "left">
  <img src = "images/spotify-skipped-finished-songs.png">
</p>

* From 2015–2019, the number of unique artists I streamed grew in tandem with my skip rate. This trend reversed in 2020, as I continued exploring a consistent number of artists each year, while the rate at which I skipped songs declined.
* In 2024, I explored 3% fewer artists than in 2019, while skipping 71% fewer songs.

<p align = "center">
  <img src = "images/spotify-artists-skips-.png" style="width:480px">
</p>

### **What I Listened To: Evolution of Taste**
* From 2015–2021, podcast episodes accounted for just 2% of my total streaming hours. That figure grew to 32% from 2022–2024, reflecting a major shift in the type of media I regularly streamed.
* Over 80% of my total podcast streaming hours were spent listening to just three shows.

<p align = "center">
  <img src = "images/spotify-hours-split-by-year.png" style="width:480px">
</p>

* From 2015–2020, my most streamed artist each year was a rapper. Since 2021, each top artist has been a rock band, signaling a shift in genre preference.

<p align = "center">
  <img src = "images/spotify-artist-by-year.png">
</p>

* Green Day has emerged as my most consistently streamed artist in recent years. The majority of my Green Day streaming was comprised of songs from older, classic albums. However, after spending a significant amount of time listening to the 2024 release, *Saviors*, my all-time Green Day streaming mix includes a blend of longtime favorites and newer releases.

<p align = "center">
  <img src = "images/spotify-greenday-by-year.png">
</p>

## **Reflections & Recommendations**
### **Reflections**
* My weekday streaming was substantially higher than weekends, reflecting a structured routine with more opportunities to listen during lunch and in the evening. Streaming activity on weekends and during the summer notably decreased, due to spending more time outside of my residence.
* The seasonal frequency of my podcast streaming closely mirrored the NFL calendar. Streaming rose steadily beginning in May after the NFL draft, peaked during the regular season, and tapered off late in the playoffs when there were fewer games to discuss. These trends align with the time of year when my regularly streamed podcasts released new episodes focused on NFL topics, which I am most likely to listen to.
* In my early streaming years, I frequently skipped songs while exploring new artists and genres. After my exploration peaked in 2019, I began to settle into my preferences, resulting in a declining skip rate despite streaming a similar number of unique artists annually. This shift in behavior reflects both personal growth as a more patient listener, as well as improvements in Spotify's algorithms, which now suggest more songs I am likely to enjoy.
* Over the lifetime of my account, my music taste has grown to incorporate a diverse collection of genres. While early years featured almost exclusively rap, my preferred genre as of 2024 has shifted to rock.

### **Recommendations**
1. Continue to stream at least 500 unique artists each year to encourage further genre diversity in my listening profile.
2. Embrace a more patient listening approch by continuing to finish more songs than I skip each year.
3. Stream 10% fewer hours during the winter months (December–March) to my support personal goal of spending less time on devices while at my residence.