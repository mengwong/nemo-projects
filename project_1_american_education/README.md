# Project 1: Standardized Testing, Statistical Summaries and Inference on the SAT and ACT 2017 and 2018 Datasets

## Project Goal

In this project, I am an employee of the College Board and need to recommend where money should be spent to improve SAT participation rates, which shows in percentage how much of the student population took that particular test. For example, an 80% participation rate in SATs in a state means that 80% of students in that state took the SAT. 

As such, this project aims to identify factors that affect **participation rates** and **scores** for the SAT.

This notebook utilises **Exploratory Data Analysis** and references state government websites to reach recommendations and conclusions.

## Problem Statement

### Introduction
In the United States of America (USA), students sit various entrance exams to enter college. Two popular entrance exams are the SAT and the ACT. Both exams are administered by separate non-profit organisations. The not-for-profit [College Board](https://www.collegeboard.org/) administers the SAT, while the nonprofit [ACT organisation](https://www.act.org/) administers the ACT.

Students frequently sit both exams as they are both common admission requirements for USA colleges. While both of these exams [differ in content](https://blog.prepscholar.com/act-vs-sat), they are similar enough in format to make comparisons to each other thanks to a recent change in format, discussed below.

To keep up with modern test-taking methodology and changes, a new format for the SAT exams was released in March 2016. [Several major changes were made](https://blog.prepscholar.com/new-sat-format-2016), such as standardising the order in which subjects were tested, as well as the amount of time and number of questions given. This mean that the format was more aligned with the ACT's.

### Project goals and why they matter

In this project, I am an employee of the College Board (linked above) and need to recommend where money should be spent to improve SAT participation rates, which shows in percentage how much of the student population took that particular test. For example, an 80% participation rate in SATs in a state means that 80% of students in that state took the SAT. 

As such, this project aims to identify factors that affect **participation rates** and **scores** for the SAT.

#### Why participation rates and scores in different states matter

As [this blog post explains](https://blog.prepscholar.com/average-sat-and-act-scores-by-stated-adjusted-for-participation-rate), Participation rates matter because states with low SAT participation have artificially higher SAT scores. This is because only highly motivated students will take the SAT and they are more likely to score higher than the average student. As such, they _bias score averages_.

#### Why a biased score average for a state is detrimental

As [Kate Sundquit explains](https://blog.collegevine.com/here-are-the-average-sat-scores-by-state/), Average SAT scores by state matters because the score is used to help colleges form a diverse class. One factor involved in making such a decision is by considering the geographical factors. Students compete with other students within the same state. 

If SAT scores are artificially high, students that scored high marks may not be accepted into the college because their score may be lower than the average. The score also affects scholarship grants, again disadvantaging those with high scores that aren't the cream of the crop.

This ultimately leads to colleges accepting only the top students, which [perpetuates class inequality](https://www.cnbc.com/2019/10/03/rich-students-get-better-sat-scores-heres-why.html) as students who are top scorers generally tend to come from rich families.

For these reasons, it is imperative to improve participation rates in states where participation rates are low.



## Summary of Conclusions

To improve SAT participation rates, do the following:

1. **Improve Education Infrastructure**
2. **Encourage Post-Secondary Education**
3. **Push Policies That Make SAT or ACT Compulsory**

We will see these recommendations theoretically applied to Oregon to improve their SAT participation rates.

## Notebook Contents

- 2017 Data Import & Cleaning
- 2018 Data Import and Cleaning
- Exploratory Data Analysis
- Data Visualization
- Descriptive and Inferential Statistics
- Outside Research
- Conclusions and Recommendations

## Datasets

- [SAT 2017 Scores](./data/sat_2017.csv), shape: (51, 5)
- [SAT 2018 Scores](./data/sat_2018.csv), shape: (51, 7)
- [ACT 2017 Scores](./data/act_2017.csv), shape: (51, 5)
- [ACT 2018 Updated Scores](./data/act_2018_updated.csv), shape: (51, 7)

All of these datasets are eventually combined to form [final_df](./data/final.csv), shape: (51, 21), with [merged_2017_df](./data/combined_2017.csv), shape: (51, 11), as an intermediary dataset.

### Sources for Datasets

- [SAT 2017 Data Source here](https://blog.collegevine.com/here-are-the-average-sat-scores-by-state/)
- [ACT 2017 Data Source here](https://blog.prepscholar.com/act-scores-by-state-averages-highs-and-low0s)
- [ACT 2017 Data Source here](https://blog.prepscholar.com/act-scores-by-state-averages-highs-and-lows)
- [SAT 2018 Data Source here](https://reports.collegeboard.org/archive/sat-suite-program-results/2018/state-results)
- [ACT 2018 Data Source here](http://www.act.org/content/dam/act/unsecured/documents/cccr2018/Average-Scores-by-State.pdf)

In addition, state-by-state average results and participation for the SAT  and SAT are referred to.

- [2018 SAT reported results (HTML)](https://newsroom.collegeboard.org/more-2-million-students-class-2018-took-sat-highest-ever)
- [2018 ACT reported results (pdf)](http://www.act.org/content/dam/act/unsecured/documents/cccr2018/Average-Scores-by-State.pdf)

## Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|state|object|SAT|Name of State. Unlike ACT 2017, there is no national average|
|sat_2017_participation|float|SAT|Participation rates in percentage for SAT 2017, between **0-100**|
|sat_2017_evidence_based_reading_and_writing|float|SAT|Average Reading and Writing score for SAT 2017, between **200-800**|
|sat_2017_math|float|SAT|Average Math score for SAT 2017, between **200-800**|
|sat_2017_total|float|SAT|Sum of Average Math and Reading and Writing score for SAT 2017, between **400-1600**|
|||||
|state|object|ACT|Name of State, including National Average on row 0. This National Average is removed after cleaning|
|act_2017_participation|float|ACT|Participation rates in percentage for ACT 2017, between **0-100**|
|act_2017_english|float|ACT|Average English score for ACT 2017, between **1-36**|
|act_2017_math|float|ACT|Average Math score for ACT 2017, between **1-36**|
|act_2017_reading|float|ACT|Average reading score for ACT 2017, between **1-36**|
|act_2017_science|float|ACT|Average science score for ACT 2017, between **1-36**|
|act_2017_composite|float|ACT|A score composed of English, Math, Reading, and Science scores for ACT 2017, normalised to **1-36**|

These apply similarly for SAT and ACT 2018 features.

|Feature|Type|Dataset|Description|
|---|---|---|---|
|state|object|SAT|Name of State. Unlike ACT 2017, there is no national average|
|sat_2018_participation|float|SAT|Participation rates in percentage for SAT 2017, between **0-100**|
|sat_2018_evidence_based_reading_and_writing|float|SAT|Average Reading and Writing score for SAT 2017, between **200-800**|
|sat_2018_math|float|SAT|Average Math score for SAT 2017, between **200-800**|
|sat_2018_total|float|SAT|Sum of Average Math and Reading and Writing score for SAT 2017, between **400-1600**|
|||||
|state|object|ACT|Name of State, including National Average on row 0. This National Average is removed after cleaning|
|act_2018_participation|float|ACT|Participation rates in percentage for ACT 2017, between **0-100**|
|act_2018_average_english_score|float|ACT|Average English score for ACT 2017, between **1-36**|
|act_2018_average_math_score|float|ACT|Average Math score for ACT 2017, between **1-36**|
|act_2018_average_reading_score|float|ACT|Average reading score for ACT 2017, between **1-36**|
|act_2018_average_science_score|float|ACT|Average science score for ACT 2017, between **1-36**|
|act_2018_average_composite_score|float|ACT|A score composed of English, Math, Reading, and Science scores for ACT 2017, normalised to **1-36**|

They then get combined with 'state' being the common column name to final_df.

## Learning Goals for this Project

- basic statistics (distributions, confidence intervals, hypothesis testing)
- many Python programming concepts
- programmatically interacting with files and directories
- visualizations
- EDA
- working with Jupyter notebooks for development and reporting
