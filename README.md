# PPPloans_USASpending_DataMerge
Merging data from PPP loan recipients in 2020 and 2021 with USASpending.gov Award Archive Data from 2015 to 2022. 

## Step 1: PPP Loan Data Collection and Transformation ##
#### 1a: PPP Data Collection: #### 
I retrieved PPP files  on January 9, 2023 from the SBA's website: https://www.sba.gov/funding-programs/loans/covid-19-relief-options/paycheck-protection-program/ppp-data 

Using Python, I accessed the files' contents, parse the data, and created a single file for all PPP loans up to $150k by merging the 12 original files below, filtering the "ProcessingMethod" column by PPP, and dropping columns that will not be used for the analysis: [All_PPP_upto150k.ipynb.](https://github.com/JCNdongo/PPPloans_USASpending_DataMerge/blob/main/All_PPP_upto150k.ipynb)


public_up_to_150k_1_230101.csv,
public_up_to_150k_2_230101.csv,
public_up_to_150k_3_230101.c sv,
public_up_to_150k_4_230101.csv,
public_up_to_150k_5_230101.csv,
public_up_to_150k_6_230101.csv,
public_up_to_150k_7_230101.csv,
public_up_to_150k_8_230101.csv,
public_up_to_150k_9_230101.csv,
public_up_to_150k_10_230101.csv,
public_up_to_150k_11_230101.csv,
public_up_to_150k_12_230101.csv.

#### 1b: PPP Data Transformation and Cleanup: ####
1. I retrieved the "All_PPP_upto150k.csv" single file with all PPP loan data, made a copy "All_PPP_upto150k_copy.csv"
2. In the copy, I renamed the columns BorrowerName and CurrentApprovalAmount, respectively, "BusinessName" and "PPPInitialApprovalAmount".
3. Using Python, I did the following: [Cleaning_All_PPP_upto150k.ipynb](https://github.com/JCNdongo/PPPloans_USASpending_DataMerge/blob/main/Cleaning_All_PPP_upto150k.ipynb)

(a) delete the columns "ProcessingMethod", "CurrentApprovalAmount", and "UndisbursedAmount", (b) remove every "BusinessName" titled "NOT AVAILABLE", and every "BusinessAgeDescription" titled "New Business or 2 years or less" or "Startup, Loan Funds will Open Business", (c) in columns "HubzoneIndicator" and "LMIIndicator", replace Y with 1 and N with 0 to make the variables numerical and binary to facilitate the analysis (1 for Yes; 0 for No), and (d) save the file as PPP_up_to_150k_Aggregate.csv

Result, number of PPP recipients FOR THIS ANALYSIS: 933,405 businesses that were recipients of PPP loans up to $150,000 nationwide based on the criteria above. 

## Step 2: USASpending.gov Data Collection and Transformation ##
#### 2a: USASpending.gov Data Collection: #### 
I retrieved USASpending.gov Award Data Archive (2015 to 2022) on June 30, 2023 from https://www.usaspending.gov/download_center/award_data_archive

The data consisted of 2 to 7 .csv files (2GB avg.) for each year (2015 to 2022). 

Using Python, I wrote scripts to access the content of each file and parse the data, retaining the following columns (variables) only for each file and year: 

#### 2a: USASpending.gov Data Transformation and Cleanup: ####

1. USing PostgreSQL, I wrote a SQL script to merge the different files for a given year into one. For example, for 2015, I ran SQL Code [2015_Contracting_DataMerger.sql](https://github.com/JCNdongo/PPPloans_USASpending_DataMerge/blob/main/2015_Contracting_DataMerger.sql). Result: "All_2015_Contracting" SQL table with 352,700 entries (unique entries of businesses that were awarded federal government contracts in 2015); "All_2016_Contracting" SQL table with 354,761 entries; 
2. I exported the table as a csv file. I repeated the process for 2016-2022. 
3. Using Python, I wrote a scrip to merge the newly created files into one main file with contracting data for the entire time-series period (2015 to 2022).
