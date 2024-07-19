All code is created and executed in Google Colab, so you can see all outputs.
We added csv files as result of detection potentielly cheated answersheets for all methods we used

EDA — ## EDA Section Summary

This section of the repository contains scripts for Exploratory Data Analysis (EDA) conducted on the dataset. The primary steps and visualizations in this EDA are outlined as follows:

- *Data Loading*: Data is imported using Pandas, with the source file 'final_df.csv' downloaded directly within the script.
- *Initial Data Exploration*:
  - Basic data characteristics are reviewed using data.head(), data.info(), and data.describe() to understand the dataset structure, information types, and statistical summaries.
- *Duplicate Removal*: Identifies and removes duplicate records to ensure data integrity.
- *Score Distribution Analysis*:
  - Histograms display the distribution of answer_score and maxScore across the dataset, providing insight into the scoring patterns.
- *Correctness Analysis*:
  - A bar chart illustrates the count of answers categorized by correctness, aiding in understanding the frequency of correct versus incorrect answers.
- *Difficulty and Response Time Analysis*:
  - Distribution of Difficulty is analyzed through histograms and scatter plots, correlating it with the Expected response time and ResponseTime to identify trends and outliers.
  - Detailed analysis of response times includes histograms, boxplots, and a correlation matrix to explore the relationship between observed and expected response times.
- *Exam and Candidate Performance Exploration*:
  - The number of questions answered by each candidate is visualized, and the relationship between exam scores and answer scores is analyzed through scatter plots and histograms.
  - Further, the analysis delves into how well questions were answered in relation to their difficulty and the overall exam score, using bar plots and scatter plots for a nuanced understanding.

These analyses are critical for gaining insights into the dataset, identifying patterns, and preparing the data for further machine learning tasks. The visualizations help in understanding the underlying structure and any potential anomalies in the data.
