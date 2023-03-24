# NoSQL-Challenge
## Eat Safe, Love - Analysis

The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. In this challenge, the aim is to evaluate some of the ratings data for a food magazine, 'Eat Safe, Love', in order to help their journalists and food critics decide where to focus future articles.

The assignment has 3 sections: first 2 parts Database and Jupyter Notebook Set Up
and Update the Database are completed in NoSQL_setup.ipynb. The 3rd section is Exploratory Analysis where specific questions are analyzed in the NoSQL_analysis.ipynb.


## Part 1: Database and Jupyter Notebook Set Up 

For this part, using the NoSQL_setup.ipynb, first step was to import the data provided in the establishments.json from Terminal by naming the database uk_food and the collection establishments. Next, we imported the dependencies and created an instance of the Mongo Client.

Confirmed that the database was created and loaded the data properly by:

- List the databases you have in MongoDB. Confirm that uk_food is listed.
- List the collection(s) in the database to ensure that establishments is there.
- Find and display one document in the establishments collection using find_one and display with pprint.

Assigned the establishments collection to a variable to prepare the collection for use.


## Part 2: Update the Database

The magazine editors have some requested modifications for the database before performing any queries or analysis for them. Make the following changes to the establishments collection:

1. An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine has asked to include it in the analysis. So, the new restaurant 'Penang Flavours' information was added to the database.
2. Updated the new restaurant BusinessTypeID by finding the BusinessTypeID for "Restaurant/Cafe/Canteen" and returning only the BusinessTypeID and BusinessType fields.
3. The magazine is not interested in any establishments in Dover, so checked how many documents contain the Dover Local Authority. Then, removed any establishments within the Dover Local Authority from the database, and checked the number of documents to ensure they were deleted.
4. Converted latitude and longitude to decimal numbers form stings.


## Part 3: Exploratory Analysis

Eat Safe, Love has specific questions which they want to look into to help them find the locations they wish to visit and avoid. Some notes to be aware of while exploring the dataset:

- RatingValue refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating. Note: This field also includes non-numeric values such as 'Pass', where 'Pass' means that the establishment passed their inspection but isn't given a number rating.
- The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse. This means, the higher the value, the worse the establishment is in these areas.

Questions the magazine is interested in are as follows: 

### 1. Which establishments have a hygiene score equal to 20?
 
 For answering this question, only the establishmensts with hygiene score of 20 were used to create a query, then used count_documents to display the number of documents in the result. After that, used pprint to print the first document. Next, converted the results to a Pandas DataFrame, printed the number of rows in the DataFrame, and displayed the first 10 rows.

### 2. Which establishments in London have a RatingValue greater than or equal to 4?

For this question, query was created for establishments in London with a RatingValue greater than or equal to 4 and using $regex to find the London Local Authority. Then displayed the number of documents in the result and printed the first document in the result. After that, converted the results to a Pandas DataFrame, printed the number of rows in the DataFrame, and displayed the first 10 rows.

### 3. What are the top 5 establishments with a RatingValue of '5', sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?

To answer this question, compared the geocode to find the nearest locations and searched within 0.01 degree on either side of the latitude and longitude of the new restaurant. 
Query was created with establishments with a RatingValue of '5' and the geo locations. The results for the top 5 establishments were sorted by lowest to highest hygiene score. Returned results of the documents were based on query, sort and limit and then used pprint to print the results. Then, converted the results to a Pandas DataFrame, printed the number of rows in the DataFrame, and displayed the first 10 rows.

### 4. How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas.

For this question, used the aggregation method. The Pipeline consisted of: 
- match query - this query matched establishments with a hygiene score of 0.
- group query - grouped the matches by Local Authority.
- sort values - sorted the matches from highes to lowest
Returned results of the documents were based on the aggregation of the Pipeline and then used pprint to print the first 10 results. Then, converted the results to a Pandas DataFrame, printed the number of rows in the DataFrame, and displayed the first 10 rows.


<img width="309" alt="Screenshot 2023-03-23 at 10 50 17 PM" src="https://user-images.githubusercontent.com/120361200/227412162-311f1f40-d06f-4a75-b548-2c9d07c4d07b.png">
