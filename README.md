All code is created and executed in Google Colab, so you can see all outputs.
We added csv files as result of detection potentielly cheated answersheets for all methods we used

### Final Join Summary

This section details the final data processing steps, including joining various datasets and performing additional data cleaning and feature engineering, using the dataset loaded from 'final_join_202407030718.csv'. Here's an overview of the process:

- *Data Loading and Initial Processing*:
  - Loads the dataset and displays initial information such as column names and shape.
  - Removes specific candidates and duplicate rows based on key columns to ensure data integrity.

- *Datetime Conversion and Missing Value Handling*:
  - Converts 'firstSeenAt' and 'lastAnsweredAt' columns to datetime format.
  - Replaces NaN values in the 'answer_score' column with 0.

- *Response Time Calculation*:
  - Calculates the response time for each question by computing the difference between 'lastAnsweredAt' and 'firstSeenAt'.
  - Drops rows where response time is negative or NaN.
  - Computes the expected response time as the average response time per question.

- *Difficulty Calculation*:
  - Calculates the difficulty of each question based on the total answer scores and maximum scores.
  - Adjusts the difficulty to be within a range of 0 to 1 by taking the absolute difference from 1.

- *Total Testing Time and Exam Score*:
  - Computes the total testing time for each exam by summing the response times.
  - Calculates the total exam score by summing the answer scores for each candidate.

- *Correctness and Sequence Order*:
  - Defines 'answeredCorrectly' based on whether the answer score equals the maximum score.
  - Calculates the sequence order of questions for each candidate based on the 'firstSeenAt' timestamp.

- *Data Grouping and Sorting*:
  - Groups the data by 'paperId', 'candidateId', and 'answerSheetId'.
  - Sorts each group by sequence order to ensure the correct order of responses.

- *Final DataFrame Preparation*:
  - Selects relevant columns to create the final DataFrame.
  - Renames columns and rounds response times to three decimal places.
  - Provides detailed information and descriptive statistics for the final DataFrame.
  - Saves the final DataFrame to a CSV file for further analysis.

These steps ensure the dataset is clean, well-structured, and ready for subsequent analysis and machine learning tasks.

### Data Investigation (Finding Outliers) Summary

This section details the process of investigating and identifying outliers in the dataset loaded from 'final_df_all_candidates.csv'. Here's an overview of the process:

- *Data Loading and Initial Inspection*:
  - Loads the dataset and checks for data types and missing values to understand the structure and completeness of the data.

- *Response Time Analysis*:
  - *Scatter Plot*: Creates a scatter plot of response times by answer sheet ID to visualize distribution and identify outliers.
  - *99th Percentile Line*: Adds a line at the 99th percentile to highlight extreme values.

- *Outlier Identification and Removal*:
  - Identifies candidate IDs with response times above the 99th percentile and removes these outliers from the dataset.
  - Provides descriptive statistics for the cleaned dataset to compare with the original.

- *Further Outlier Investigation*:
  - *Scatter Plot Update*: Recreates the scatter plot for the cleaned dataset, including a 99th percentile line for the updated data.
  - Identifies candidate IDs with response times exceeding a specific threshold (e.g., 14,000 seconds) and removes these additional outliers.
  - Provides updated descriptive statistics to reflect the further refined dataset.

- *Summary of Results*:
  - Describes the distribution of response times, total testing times, and exam scores before and after outlier removal.
  - Highlights the effectiveness of outlier detection and removal in cleaning the data for subsequent analysis.

These steps ensure the dataset is clean and free from extreme outliers, providing a more accurate foundation for further analysis and machine learning tasks.

## EDA Section Summary

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

## Statistical Methods Summary

This section outlines various statistical methods applied to detect potential cheating in examinations using the dataset loaded from 'final_df.csv'. Here's an overview of the techniques used:

- *Aberrance Detection Based on Difficulty*:
  - Calculates the correctness rate for each student at different difficulty levels and identifies students who performed unusually well on difficult questions and poorly on easy ones.
  - Merges performance data back into the main dataset and applies thresholds to flag potential cheaters based on performance anomalies.

- *Aberrance Detection Based on Response Time*:
  - Computes deviations from expected response times and identifies outliers using a strict threshold (e.g., 4 standard deviations), flagging potential cheaters based on their response times.
  
- *Cosine Similarity-Based Collusion Detection*:
  - Utilizes cosine similarity to detect patterns of collusion among candidates by comparing their answer patterns across the same set of questions.
  - Identifies pairs of students with suspiciously high similarity scores, suggesting potential collaboration or cheating.

- *Kullback-Leibler Divergence Analysis*:
  - Applies KL divergence to compare individual response time distributions against group averages, identifying students whose response patterns significantly deviate from the norm.
  
- *Common Potential Cheaters Identification*:
  - Integrates results from all methods to identify students consistently flagged across different statistical tests, enhancing the reliability of potential cheating detections.
  
- *Multiple Method Validation*:
  - Combines flags from various methods to identify students potentially cheating on several fronts, providing a robust mechanism for ensuring the validity of results.

These methods collectively enhance the detection of anomalous behaviors and potential cheating, supporting a fair assessment process.

### Z2, KS, KL Indices Summary

This section outlines the use of Z2, KS, and KL indices to detect potential cheating in examinations using the dataset loaded from 'final_df.csv'. Here's an overview of the techniques used:

- *Data Normalization and Z-Score Calculation*:
  - Normalizes response times using Min-Max Scaling to standardize the data.
  - Calculates Z-scores (Z2) for the normalized response times to identify outliers.

- *KL Divergence and KS Statistic Calculation*:
  - *KL Divergence*: Computes the Kullback-Leibler divergence between individual response time distributions and the overall distribution to identify significant deviations.
  - *KS Statistic*: Uses the Kolmogorov-Smirnov test to compare individual response time distributions with the overall distribution, identifying significant differences.

- *Anomaly Detection*:
  - Sets thresholds for anomaly detection using Z-scores, KL divergence, and KS statistic to flag potential cheaters.
  - Identifies potential cheaters whose Z-scores, KL divergence, or KS statistics exceed the set thresholds.

- *Visualization*:
  - Visualizes the distribution of response times, Z-scores, KL divergence, and KS statistics, highlighting the anomalies detected.
  - Generates histograms to compare the general distribution with that of the flagged potential cheaters.

- *Summary of Results*:
  - Calculates and prints the number and percentage of flagged candidates based on the statistical methods applied.
  - Saves the processed data to a CSV file for further analysis.

These methods provide a robust framework for detecting anomalous behaviors and potential cheating, enhancing the fairness and integrity of the examination process.

### Guttman and ML Methods Summary

This section details the application of Guttman and various machine learning (ML) methods to detect potential cheating in examinations using the dataset. Here's an overview of the techniques and methods used:

- *Clustering Techniques*:
  - *K-Means Clustering*: Identifies potential cheaters by grouping data into clusters and flagging anomalies. Displays unique candidate IDs and common potential cheaters identified by K-Means Clustering.
  - *DBSCAN*: Applies Density-Based Spatial Clustering of Applications with Noise (DBSCAN) to detect outliers in the data, assuming outliers indicate potential cheaters.

- *Anomaly Detection*:
  - *Isolation Forest*: Detects anomalies in the dataset by isolating observations that are significantly different from the majority. Displays unique candidate IDs identified by Isolation Forest.
  - *Combined Results*: Integrates results from Isolation Forest, K-Means Clustering, and DBSCAN to identify common potential cheaters across all methods.

- *Visualization and Reporting*:
  - *Unique Candidate IDs*: Displays the list of unique potential cheaters identified by each method (Isolation Forest, K-Means Clustering, DBSCAN).
  - *Combined Results*: Combines results from all three methods to provide a comprehensive list of potential cheaters. Displays and saves the unique candidate IDs identified by the combined methods.
  - *Common Cheaters*: Identifies and reports common potential cheaters flagged by all three methods, ensuring robust detection.
  - *Data Export*: Saves the results to CSV and Excel files for further analysis and reporting.

- *Summary of Results*:
  - Calculates and prints the number and percentage of flagged candidates based on the combined results from all methods.
  - Displays the candidate IDs of potential cheaters identified by all three methods and exports the detailed results for further analysis.

These methods collectively enhance the detection of anomalous behaviors and potential cheating, supporting a fair assessment process.



### Finding Common AnswerSheets Summary

This section describes the process of identifying common answer sheets flagged by multiple cheating detection methods using the dataset loaded from 'final_df.csv'. Here's an overview of the process:

- *Data Loading and Preparation*:
  - Loads the dataset and various candidate lists identified by different methods.
  - Removes duplicates and ensures data integrity across all datasets.

- *Combining Results from Multiple Methods*:
  - Loads and processes answer sheet IDs flagged by different methods, including Clustering, Isolation Forest, and DBSCAN.
  - Converts answer sheet IDs to standard Python lists for further processing.

- *Unique AnswerSheet Identification*:
  - Combines unique answer sheet IDs from all methods into a single DataFrame.
  - Flags each answer sheet based on which methods identified it as suspicious.

- *Multi-Flagged Cheater Identification*:
  - Calculates the total number of flags each answer sheet received.
  - Identifies answer sheets flagged by at least four different methods.

- *Summary of Results*:
  - Extracts and displays the final set of cheaters' candidate IDs and corresponding answer sheet IDs.
  - Calculates and prints the number and percentage of flagged candidates based on the combined results from all methods.
  - Provides detailed statistics and prints the final results for further analysis.

These steps ensure a robust approach to identifying potential cheaters by cross-referencing multiple detection methods, enhancing the reliability and accuracy of the results.
