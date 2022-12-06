# Fetch Rewards Data Analyst Assessment

### First Task: Review Existing Unstructured Data and Diagram a New Structured Relational Data Model

There were 3 data sets given namely 'Receipts', 'User' and 'Brand'.

After analyzing the JSON files, it was obvious that there was no natural identifier connecting Brands to Receipts because the pipe-=delimited entries in Receipts > rewardsReceiptItemList did not have a brand ID or barcode value to link to the Brands table. It also became clear that another level of detail would be required to connect receipts to brands, which I did by creating the receipt product table to link the two tables.

<img width="1080" alt="ER" src="https://user-images.githubusercontent.com/95984580/205783049-a9e958be-33ef-40f6-8411-3d5bc76d4b79.png">



### Second Task: Write a query that directly answers a predetermined question from a business stakeholder
I have included all the queries in the FetchRewards_DA.ipynb that were executed to answer questions such as -

When considering average spend from receipts with 'rewardsReceiptStatus’ of ‘Accepted’ or ‘Rejected’, which is greater?
When considering total number of items purchased from receipts with 'rewardsReceiptStatus’ of ‘Accepted’ or ‘Rejected’, which is greater?
Which brand has the most spend among users who were created within the past 6 months?
Which brand has the most transactions among users who were created within the past 6 months?

### Third Task: Evaluate Data Quality Issues in the Data Provided

The brand data was unsuitable to be a dimension table because it contained a number of duplicates.

In addition, there didn't appear to be any information in the rewardsReceiptItemList's pipe-delimited values that would enable us to connect to the brand dimension. The rewardsReceiptItemList data might have a variety of different values in any one position, thus it took some time to figure out how to split the data into columns. Upon assesing the data, I decided to first explode the column rewardsReceiptItemList using literal_eval function after which I used json normalise function to split each dictionary to get the columns from it which is then later merged with the main dataframe as the end result.

Major Data Quality issues -

a) 'Receipts' :A large amount of values missing in 'finishedDate', 'pointsEarned', 'purchasedItemCount', 'totalSpent', 'rewardsReceiptItemList' columns.There are many outliers in the values of the "pointsEarned," "purchasedItemCount," and "totalSpent" columns. For the values of these attributes, the distribution curves are distorted. At this time, it is unclear if the outliers represent actual values or the result of mistakes or inconsistencies in the procedures that generate them.

b) 'Users' : More than half of the records are duplicate.

c) 'Brands': 'topBrand' and 'categoryCode' columns have a substantial percentage of values missing.


### Fourth Task: Communicate with Stakeholders

Hi All,

I hope you're having a good day.

I recently worked with the dataset for fetch rewards, namely the receipts, users, and brands data, and I was wanting to share my discoveries, potential problems, and gain a better understanding of the data. I'll start by providing some context on how I went about handling this data. I used Python to read, clean, and arrange the data into a more readable way because the data was in zipped json files. After the data had been cleansed, I performed some quality tests and had the following comments and questions:

1.	I saw that there were several records for the same user, last login time, and created time when I felt the urge to verify if there were unique Users by ID in the User database. I wanted to learn why this was the case.
2.	A large number of receipts contained brandcodes that were absent from the brands data. When we aggregate by brands to provide analysis, this could be a concern.
3.	I observed that the "brandCodes" are not numerical, and given my experience working with databases, I would advise making the foreign keys numerical to avoid problems that could arise when merging the data due to minute changes in the string.
4.	Additionally, the User database has a huge number of duplicate records. I would strongly advise going over them to remove any redundant records to maintain data consistency.

Finally, I discovered that the date formats were inconsistent with the typical MM/DD/YYYY or other traditional date forms. A mapping specification for this metric would aid in resolving the problem and hence ensuring data is clean & consistent.

I have a plan to deal with the issues stated above and I would love to discuss these points further.

Let me know what time works best for you.

Best,

Suman Singh
