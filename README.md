# Sparkify: Predicting Customer Churn with Spark SQL

<img width="535" alt="Sparkify" src="https://user-images.githubusercontent.com/52805660/189720096-b8b900d4-f8ce-4211-9123-58922dc98333.png">

Sparkify is a fictional music-streaming service, similar to Spotify or Pandora. Users stream songs every day on a free tier with adverts or on a paid subscription, and they can upgrade, downgrade or cancel at any time. Every interaction (playing a song, a thumbs up, hearing an advert, downgrading) generates an event. The job of the data team is to predict which users are at risk of churning, either by downgrading from paid to free or by cancelling, so the business can reach them with offers before they leave.

This project loads the event log with **Apache Spark on Databricks**, explores it with **Spark SQL**, engineers user-level features and trains a **Decision Tree** classifier to flag at-risk users.

## Notebook

`sparkify_churn_spark_sql.ipynb` walks through:

1. **Exploration** of every column in the event log (numeric and categorical), with a summary of each.
2. **Cleaning**: duplicate and empty user ids are removed, null song lengths are filled with the column mean, and a `churnStatus` label is derived from the *Cancellation Confirmation* and *Submit Downgrade* pages.
3. **Feature engineering** at user level: device pivot (user agent), song count, average listening time, gender, subscription level, location pivot and page-visit counts. Highly correlated pages (Cancel vs Cancellation Confirmation) and the always-present Next Song page are dropped.
4. **Modelling** with a Decision Tree classifier.
5. **Business questions** answered with Spark SQL (below).

![Correlation between page-visit features](docs/images/page_correlation.jpg)

## What the data says

| Question | Finding |
|---|---|
| When are at-risk users most active? | At 10 am. Users not at risk peak at 6. |
| Which days? | At-risk users are more active at weekends; the rest on weekdays. |
| Paid or free? | Free is the majority in both groups. |
| Add Friend, Roll Advert, Thumbs Up | Users not at risk add more friends and give more thumbs up; at-risk users hear more adverts, a possible reason for leaving. |
| Devices | Not at risk: Windows + Chrome. At risk: Windows + Firefox. |
| Cities | At-risk users mostly come from Los Angeles; the rest from New York. |
| Time to churn after a downgrade | 28 days on average. |
| Most influential features | Pages visited, average listening minutes, gender, level and device. |

## Running it

The notebook was built for Databricks. Upload `medium_sparkify_event_data.json` to `/FileStore/tables/` (or point the `data` variable to your own path) and run the cells in order.

## Team

David Gutierrez Alarcon, Enrique Gutierrez Ibague, Jose Carlos Molano de Oro, Juan Sebastian Vargas Torres, Julian David Tarazona Torres.
