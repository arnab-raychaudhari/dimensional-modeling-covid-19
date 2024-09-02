# InsightSphere: Dimensional Modeling of Covid-19 Data

## Executive Summary

The profound impact of the COVID-19 pandemic has transformed daily life, altering work and interaction patterns, while exposing the inherent fragility of the global community. This crisis has highlighted the vulnerabilities of health systems worldwide. The final project focuses on analyzing a comprehensive COVID dataset to demonstrate the application of analytics in strengthening resilience against global shocks like the recent pandemic.

To achieve this, daily country-level data spanning from January 1st, 2020, to November 29th, 2023, was compiled, encompassing 1,429 days of information for all countries worldwide from Our World in Data. After confirming the data’s suitability for dimensional modeling, an analytical database was established. Following a thorough review of the dataset, three analytical questions were formulated, which are elaborated upon in the subsequent sections.

## Core Insights

![dimension](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/87fb103daff130dd7ca1cc8512a94cf4b1e53499/dimension.svg) Utilizing techniques like dimensional modeling expedites the extraction of valuable information from extensive datasets.

![analytics](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/87fb103daff130dd7ca1cc8512a94cf4b1e53499/analytics.svg) Analytics applied to COVID data have proven instrumental in aiding health experts and government officials in adapting their responses effectively.

![covid](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/87fb103daff130dd7ca1cc8512a94cf4b1e53499/covid.svg) Noteworthy statistics reveal that 51% of all COVID-related deaths occurred in 2021, the yearly percentage of total cases in 2023 is 6%, and 71% of the global population has received at least one dose of the vaccine. These figures exemplify the world's collective response to the pandemic.

## Data Acquisition

The data used in this project is sourced from the GitHub repository managed by Our World in Data, encompassing country-level data for every nation globally. The extensive dataset comprises 358,802 observations and 67 variables, categorized into 8 metrics: Vaccinations, Testing and Positivity, Hospital & ICU, Confirmed Cases, Confirmed Deaths, Reproduction Rate, Policy Responses, and other variables of interest. The table below offers a more detailed perspective.

![Metric description and no.of variables](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/8ff0b8a95a326781f81672e5060a77bcf6bf128a/Metric-description-variable-count.png)

![Metric and variables](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/8ff0b8a95a326781f81672e5060a77bcf6bf128a/Metric-and-variables.png)

## Real World Impact

Does the topic have a real impact on the world?

- Analytics have been leveraged by governments and decisions makers to navigate the pandemic (Policy)
- Can save millions of lives
- Useful to adjust international and national responses to pandemic

Is the data in a suitable format given the time constraint?

- Dataset is in a clean format
- Data was collected by internationally recognized organization
- Data is suitable for dimensional modeling

## Data wrangling and Dimensional Modeling

The data used was sourced from a single CSV file, eliminating the need for merging or any other manipulation of the original data. The dataset was uploaded to EC2 (which was spun up using an AMI that came with Ubuntu 20.04 w/Python, R, Spark) for examination using csvkit and command-line tools. The decision was made to proceed without dropping any observations. The following section outlines the steps taken in this phase of the project and details the challenges anticipated due to the commitment to retain all observations.

![data wrangling](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/f6bc7726592bd9b4d7d2c89e68537258fee53278/data-wrangling.png)

### General Observations

- NA values: We have noticed that we have missing values for certain variables which was expected.
- Hospital and ICU variables have the highest number of missing values

### Challenges

- Take into account the NA values when designing the analytical questions
- Create views
- Unavailable information that could be useful (such as state level information)

The Dimensional modeling section of the project can be broken down into three main parts. First, a star schema was designed for the analytical database. Next, the design was implemented by creating the necessary tables (fact and dimensions). Finally, the data was loaded into the database.

### Star Schema

![start-schema](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/8f7fc52fcf74830fedb3fb70e4dc1be489fc592e/star-schema.png)

### Creating tables and bulk upload

![tables and bulk upload](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/e021d3e7f9902d1b62d6f074975cf35b12fa207c/tables-and-bulk-upload.png)

At each step of the process and at its conclusion, the number of rows loaded into the tables was verified to ensure they matched the expected values.

## Analytical Questions

Before addressing the analytical question, the dataset was thoroughly explored through the execution of several queries. This exploration helped in formulating more specific questions. The following summary highlights some key elements visualized during this process, providing a general understanding of the dataset.

![summary-highlights](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/09f12202029b1279938ed7fcf193c1c443553b90/summary-highlights-of-dataset.png)

![deaths-world-view](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/09f12202029b1279938ed7fcf193c1c443553b90/summary-highlights-deaths-world-view.png)

## Dimensional Deliberations: Formulating Key Analytical Questions

1 - On January 30th, 2021, the EU authorized covid vaccines. Is there a significant difference in the trends of the weekly changes of the percentage of vaccinated populations of countries with the highest average stringency index compared to the countries with the lowest up to a year after the EU authorization of the vaccines?

2 - Research indicates that specific factors like smoking and age play a role in determining individuals' vulnerability. Is it possible to evaluate, for each continent, which country is most vulnerable based on factors such as the percentage of the population that smokes, the cardiovascular death rate, and the percentage of the population aged 65 and above? Following this, can we analyze the virus's impact in these countries by comparing the number of deaths to those in the same continent that are, by the same criteria, considered the least vulnerable?

3 - Assessing a nation’s response to the pandemic and conversely the pandemic’s impact on a nation can be gauged by the reported numbers of new cases. Are there notable variations in the trends of monthly total new cases across different continents? Upon analyzing these trends, determine whether the cumulative new cases reported are distributed uniformly across all countries within a continent or if a specific country predominantly contributes to this total. In the case where one country significantly influences the total new cases, can we offer insights into potential factors contributing to why that specific country is disproportionately affected by new cases.

### Deep Diving into Analytical Question 1

On January 30th, 2021, the EU authorized covid vaccines. Is there a significant difference in the trends of the weekly percentages of vaccinated populations of countries with the highest average stringency index compared to the countries with the lowest up to a year after the EU authorization of the vaccines?

![deep-dive-aq1-img-1](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/c469ec18466fc8c856666bea15911a1c37a88df9/deep-dive-q1-image1.png)

![deep-dive-aq1-img-2](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/c469ec18466fc8c856666bea15911a1c37a88df9/deep-dive-q1-image2.png)

### Deep Diving into Analytical Question 2

Research suggests that factors like smoking and age influence individuals’ vulnerability. Can the most vulnerable country on each continent be identified based on factors such as smoking prevalence, cardiovascular death rate, and the percentage of the population aged 65 and above? Additionally, can the impact of the virus in these countries be analyzed by comparing the number of deaths to those in countries on the same continent that are considered the least vulnerable by the same criteria?

![deep-dive-aq2-img-1](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/c469ec18466fc8c856666bea15911a1c37a88df9/deep-dive-q2-image1.png)

![deep-dive-aq2-img-2](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/c469ec18466fc8c856666bea15911a1c37a88df9/deep-dive-q2-image2.png)

![deep-dive-aq2-img-3](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/c469ec18466fc8c856666bea15911a1c37a88df9/deep-dive-q2-image3.png)

### Deep Diving into Analytical Question 3

Assessing a nation’s response to the pandemic, as well as the pandemic’s impact on a nation, can be evaluated by examining the reported numbers of new cases. Are there notable variations in the patterns of monthly total new cases across different continents? Upon analyzing these trends, it is important to determine whether the cumulative new cases are uniformly distributed across all countries within a continent or if a specific country predominantly contributes to the total. In cases where one country significantly influences the majority of new cases, insights into potential factors contributing to why that specific country is disproportionately affected could be explored.

![deep-dive-aq3-img-1](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/20e8fbd012f7d9f2854e76a5a36ebc2686db9bf5/deep-dive-q3-image1.png)

![deep-dive-aq3-img-2](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/c469ec18466fc8c856666bea15911a1c37a88df9/deep-dive-q3-image2.png)

![deep-dive-aq3-img-3](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/c469ec18466fc8c856666bea15911a1c37a88df9/deep-dive-q3-image3.png)

![deep-dive-aq3-img-4](https://github.com/arnab-raychaudhari/dimensional-modeling-covid-19/blob/c469ec18466fc8c856666bea15911a1c37a88df9/deep-dive-q3-image4.png)
