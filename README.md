# PPPloans_USASpending_DataMerge
Objective: Putting together a time-series data set of businesses that were awarded federal government contracts every year from 2015 to 2022 and received loans from the Paycheck Protection Program (PPP) due to COVID-19.

Task: Merging data from PPP loan recipients in 2020 and 2021 from the SBA with USASpending.gov Award Archive Data from 2015 to 2022 from the US Department of Treasury. 

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

Result, number of PPP recipients FOR THIS ANALYSIS: 933,404 businesses that were recipients of PPP loans up to $150,000 nationwide based on the criteria above. 

## Step 2: USASpending.gov Data Collection and Transformation ##
#### 2a: USASpending.gov Data Collection: #### 
I retrieved USASpending.gov Award Data Archive (2015 to 2022) on June 30, 2023 from https://www.usaspending.gov/download_center/award_data_archive

The data consisted of 2 to 7 .csv files (2GB avg.) for each year (2015 to 2022). 

Using Python, I wrote scripts to access the content of each file and parse the data, retaining the following columns (variables) only for each file and year. 

Variables for 2015: BusinessUEI,	2015_total_dollars_obligated,	2015_total_outlayed_amount_for_overall_award,	2015_current_total_value_of_award,	2015_base_and_all_options_value,	2015_potential_total_value_of_award,	2015_number_of_offers_received,	BusinessName,	City,	State,	ZipCode,	NAICS,	NAICSDescription,	alaskan_native,	american_indian	indian_tribe,	native_hawaiian	tribally_owned,	veteran_owned,	service_disabled_veteran,	woman_owned	WOSB,	econ_disadv_WOSB,	jointVenture_WOSB,	jointVenture_econ_disadv_WOSB	minority_owned,	subcontinent_asian_indian_american,	asian_pacific_american,	black_american,	hispanic_american	native_american,	other_minority,	usaspending_permalink.


#### 2a: USASpending.gov Data Transformation and Cleanup: ####

1. USing PostgreSQL, I wrote a SQL script to merge the different files for each year into one main file for that year. For example, for 2015, I ran SQL Code [2015_Contracting_DataMerger.sql](https://github.com/JCNdongo/PPPloans_USASpending_DataMerge/blob/main/2015_Contracting_DataMerger.sql). I repeated the process for 2016-2022. Result: "All_2015_Contracting" SQL table with 352,700 entries (unique entries of businesses that were awarded federal government contracts in 2015); "All_2016_Contracting" SQL table with 354,761 entries; "All_2017_Contracting" SQL table with 366,910 entries; "All_2018_Contracting" SQL table with 369,037 entries; "All_2019_Contracting" SQL table with 362,658 entries; "All_2020_Contracting" SQL table with 361,321 entries; "All_2021_Contracting" SQL table with 343,544 entries; "All_2022_Contracting" SQL table with 346,074 entries. 
2. I exported the tables as csv files.  
3. I wrote a Python script to merge the newly created files into one main file with contracting data for the entire time-series period (2015 to 2022), keeping only businesses that were awarded federal contracts every year from 2015 to 2022: [Merging_2015to2022_Contracting_Data.ipynb](https://github.com/JCNdongo/PPPloans_USASpending_DataMerge/blob/main/Merging_2015to2022_Contracting_Data.ipynb), resulting in All_2015to2022_Contracting.csv file with 303,459 businesses that were awarded federal government contracts perenially from 2015 to 2022.

Result, number of businesses that were awarded federal government contracts perenially from 2015 to 2022 FOR THIS ANALYSIS: 303,459.

## Step 3: Merging PPP and USASpending.gov Data ##
#### 3a: Merging PPP_up_to_150k_Aggregate.csv and All_2015to2022_Contracting.csv files: #### 

I wrote a Python script to merge the PPP_up_to_150k_Aggregate.csv and All_2015to2022_Contracting.csv files: [Merging_PPP_and_AllContracting2015to2022_V1.ipynb]().  

Result, number of PPP recipients that were awarded federal government contracts perenially from 2015 to 2022 FOR THIS ANALYSIS: 1,622 businesses.

The new merged file was saved as "MERGED_PPP_ALLContractingV1.csv". After further cleaning, the file will be further be used to begin the analysis.

#### 3b: Challenges and limitations: #### 

The only common indicator/data point that the csv files shared was the business names (businessnane column). 

The names in the PPP file was provided by the business owners at the time of the loan application, and the names on the contracting files were entered by federal contracting officers. Consequently, there may have been spelling discrepancies, which explains that only 1,622 business names were captured when merging the files as those names were the only ones sharing the same spelling in both files. Nevertheless, a sample size of 1,622 is sufficient to begin the analysis.
