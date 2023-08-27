# PPPloans_USASpending_DataMerge
Merging data from PPP loan recipients in 2020 and 2021 with USASpending.gov Award Archive Data from 2015 to 2022. 

## Step 1: PPP Loan Data Collection and Transformation ##
#### 1a: PPP Data Collection:#### 
I retrieved PPP files  on January 9, 2023 from the SBA's website: https://www.sba.gov/funding-programs/loans/covid-19-relief-options/paycheck-protection-program/ppp-data 
I created a single file for all PPP loans up to $150k by merging the 12 original files below, filtering the "ProcessingMethod" column by PPP, and dropping columns that will not be used for the analysis: https://github.com/JCNdongo/PPPloans_USASpending_DataMerge/blob/main/All_PPP_upto150k.ipynb 

public_up_to_150k_1_230101.csv,
public_up_to_150k_2_230101.csv,
public_up_to_150k_3_230101.csv,
public_up_to_150k_4_230101.csv,
public_up_to_150k_5_230101.csv,
public_up_to_150k_6_230101.csv,
public_up_to_150k_7_230101.csv,
public_up_to_150k_8_230101.csv,
public_up_to_150k_9_230101.csv,
public_up_to_150k_10_230101.csv,
public_up_to_150k_11_230101.csv,
public_up_to_150k_12_230101.csv.

#### 1b: PPP Data Transformation and Cleanup:####
1. I retrieved the "All_PPP_upto150k.csv" single file with all PPP loan data
1. Within the file, I renamed the "BorrowerName" column "BusinessName" and dropped additional columns retaining only 
2. Saved the file as PPP_up_to_150k_Aggregate.csv

## Step 2: USASpending.gov Data Collection and Transformation ##
#### 2a: USASpending.gov Data Collection:#### 
On June 30, 2023, I retrieved USASpending.gov Award Data Archive from 2015 to 2022  from https://www.usaspending.gov/download_center/award_data_archive
The data consisted of 2 to 7 .csv files (2GB avg.) for each year (2015 to 2022). 
Using Python, I condensed the files and produced one file for the entire time-series period. 

#### 2a: PPP Data Collection:####
