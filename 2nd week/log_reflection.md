Cleaning Code Court AI Code Trials

1 Code df drop duplicates
Verdict Keep
Reason Removes duplicate row 96 and restores grid count to 96

2 Code df item str title
Verdict Reject
Reason Converts lowercase oil b to Oil B blindly when row 40 is actually mislabelled Staple A

3 Code df price str replace comma astype float
Verdict Modify
Reason Fails on missing values and converts sentinel 9999 to float 9999 0 skewing statistics

4 Code df dropna
Verdict Reject
Reason Deletes valid observations that can be accurately imputed using city price parity


Documented Cleaning Log

Row 96
Column All
Original Value Duplicate row
Action Exclude
Cleaned Value Removed
Reason Duplicate of row 8

Row 40
Column item
Original Value oil b
Action Correct
Cleaned Value Staple A
Reason Mislabelled item name matching Staple A price trend

Row 17
Column price
Original Value 1 250
Action Correct
Cleaned Value 109 0
Reason Typo entry corrected to match City 1 price plus 6 0 PKR spread

Row 30
Column price
Original Value 9999
Action Correct
Cleaned Value 157 5
Reason Sentinel value imputed from City 2 price minus 6 0 PKR spread

Row 5
Column price
Original Value NaN
Action Correct
Cleaned Value 206 0
Reason Missing observation imputed from City 1 price plus 6 0 PKR spread


Reflection

Auditing the dataset showed that simple AI cleaning code misses context errors like mislabelled item names and sentinel numbers  
By checking the data against the rule that City 2 is 6 0 PKR higher than City 1 we corrected errors cleanly without deleting good data  
The final dataset has 96 rows matching all 12 dates 4 items and 2 cities

