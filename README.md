# Fetch Rewards Data Analyst Assessment

### First Task: Review Existing Unstructured Data and Diagram a New Structured Relational Data Model

There were 3 data sets given namely 'Receipts', 'User' and 'Brand'.

After analyzing the JSON files, it was obvious that there was no natural identifier connecting Brands to Receipts because the pipe-=delimited entries in Receipts > rewardsReceiptItemList did not have a brand ID or barcode value to link to the Brands table. It also became clear that another level of detail would be required to connect receipts to brands, which I did by creating the receipt product table to link the two tables.

I have attached the design for the Relational Data Model in ER.png

### Second Task: Write a query that directly answers a predetermined question from a business stakeholder
I have included all the queries in the FetchRewards_DA.ipynb that were executed to answer questions such as -

1.	When considering average spend from receipts with 'rewardsReceiptStatus’ of ‘Accepted’ or ‘Rejected’, which is greater?
2.	When considering total number of items purchased from receipts with 'rewardsReceiptStatus’ of ‘Accepted’ or ‘Rejected’, which is greater?
3.	Which brand has the most spend among users who were created within the past 6 months?
4.	Which brand has the most transactions among users who were created within the past 6 months?


### Third Task: Evaluate Data Quality Issues in the Data Provided

The brand data was unsuitable to be a dimension table because it contained a number of duplicates.

In addition, there didn't appear to be any information in the rewardsReceiptItemList's pipe-delimited values that would enable us to connect to the brand dimension. The rewardsReceiptItemList data might have a variety of different values in any one position, thus it took some time to figure out how to split the data into columns. Upon assesing the data, I decided to first explode the column rewardsReceiptItemList using literal_eval function after which I used json normalise function to split each dictionary to get the columns from it which is then later merged with the main dataframe as the end result.

Major Data Quality issues -

a) 'Receipts' :A large amount of values missing in 'finishedDate', 'pointsEarned', 'purchasedItemCount', 'totalSpent', 'rewardsReceiptItemList' columns.There are many outliers in the values of the "pointsEarned," "purchasedItemCount," and "totalSpent" columns. For the values of these attributes, the distribution curves are distorted. At this time, it is unclear if the outliers represent actual values or the result of mistakes or inconsistencies in the procedures that generate them.

b) 'Users' : More than half of the records are duplicate.

c) 'Brands': 'topBrand' and 'categoryCode' columns have a substantial percentage of values missing.


### Fourth Task: Communicate with Stakeholders

I have added the text file stating the issues that I faced ,how to tackle them & how to go about further with the stakeholder in the Communication.txt file.
