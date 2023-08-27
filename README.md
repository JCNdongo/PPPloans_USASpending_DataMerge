# PPPloans_USASpending_DataMerge
Merging data from PPP loan recipients in 2020 and 2021 with USASpending.gov Award Archive Data from 2015 to 2022. 


PPP files retrieved on January 9, 2023 from SBA's website: https://www.sba.gov/funding-programs/loans/covid-19-relief-options/paycheck-protection-program/ppp-data 


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
#### Step 1: I created a single file for all PPP loans up to $150k by merging the 12 original files above, filtering the "ProcessingMethod" column by PPP, and dropping columns that will not be used for the analysis:#### 
https://github.com/JCNdongo/PPPloans_USASpending_DataMerge/blob/main/All_PPP_upto150k.ipynb 

####Data cleanup of All_PPP_upto150k.csv file:
1. Filtered by "Existing or more than 2 years old" and "Unanswered" to remove startups and businesses < 2yrs old, resulting in 933,266 entries (rows)
2. Renamed "BorrowerName" as "BusinessName"
3. Saved the file as PPP_up_to_150k_Aggregate.csv
