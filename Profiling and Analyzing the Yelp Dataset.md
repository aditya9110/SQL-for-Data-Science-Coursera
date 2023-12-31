# Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset Coursera Worksheet

	Analysed By: Aditya Mahimkar

	Dated On: 10 September 2023


This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular research question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate and communicate your intent as required.

For both parts of this assignment, use this "worksheet." It provides all the questions you are being asked, and your job will be to transfer your answers and SQL coding where indicated into this worksheet so that your peers can review your work. You should be able to use any Text Editor (Windows Notepad, Apple TextEdit, Notepad ++, Sublime Text, etc.) to copy and paste your answers. If you are going to use Word or some other page layout application, just be careful to make sure your answers and code are lined appropriately.
In this case, you may want to save as a PDF to ensure your formatting remains intact for you reviewer.

## Yelp Dataset ER Diagram
![Yelp Dataset ER Diagram](https://github.com/aditya9110/SQL-for-Data-Science-Coursera/blob/main/Yelp%20Dataset%20ER%20Diagram.png)

## Part 1: Yelp Dataset Profiling and Understanding

### 1. Profile the data by finding the total number of records for each of the tables below:
	
i. Attribute table = 10000

ii. Business table = 10000

iii. Category table = 10000

iv. Checkin table = 10000

v. elite_years table = 10000

vi. friend table = 10000

vii. hours table = 10000

viii. photo table = 10000

ix. review table = 10000

x. tip table = 10000

xi. user table = 10000


### 2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

i. Business = 10000

ii. Hours = 1562

iii. Category = 2643

iv. Attribute = 1115

v. Review = 10000 (using id) 8090 (using business_id), 9581 (using user_id)

vi. Checkin = 493

vii. Photo = 10000 (using id) 6493 (using business_id)

viii. Tip = 3979 (using business_id), 537 (using user_id)

ix. User = 10000

x. Friend = 11

xi. Elite_years = 2780

Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.	



### 3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

**Answer: No**
	
SQL code used to arrive at answer:

```sql
-- checking null for each column using OR operation.
SELECT COUNT(*) 
FROM user 
WHERE id || name || review_count || yelping_since || useful || funny || cool || fans || average_stars || compliment_hot || compliment_more || compliment_profile || compliment_cute || compliment_list || compliment_note || compliment_plain || compliment_cool || compliment_funny || compliment_writer || compliment_photos IS NULL
```

	
### 4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

i. Table: Review, Column: Stars

	min: 1		max: 5		avg: 3.7082
	

ii. Table: Business, Column: Stars

	min: 1		max: 5		avg: 3.6549
	

iii. Table: Tip, Column: Likes

	min: 0		max: 2		avg: 0.0144
	

iv. Table: Checkin, Column: Count

	min: 1		max: 53		avg: 1.9414
	

v. Table: User, Column: Review_count

	min: 0		max: 2000		avg: 24.2995
		

### 5. List the cities with the most reviews in descending order:

SQL code used to arrive at answer:

```sql
SELECT city, SUM(review_count) AS ReviewCount 
FROM business
GROUP BY city
ORDER BY ReviewCount DESC
```

Copy and Paste the Result Below:

| city            | ReviewCount |
|-----------------|-------------|
| Las Vegas       |       82854 |
| Phoenix         |       34503 |
| Toronto         |       24113 |
| Scottsdale      |       20614 |
| Charlotte       |       12523 |
| Henderson       |       10871 |
| Tempe           |       10504 |
| Pittsburgh      |        9798 |
| Montréal        |        9448 |
| Chandler        |        8112 |
| Mesa            |        6875 |
| Gilbert         |        6380 |
| Cleveland       |        5593 |
| Madison         |        5265 |
| Glendale        |        4406 |
| Mississauga     |        3814 |
| Edinburgh       |        2792 |
| Peoria          |        2624 |
| North Las Vegas |        2438 |
| Markham         |        2352 |
| Champaign       |        2029 |
| Stuttgart       |        1849 |
| Surprise        |        1520 |
| Lakewood        |        1465 |
| Goodyear        |        1155 |

(Output limit exceeded, 25 of 362 total rows shown)
	

### 6. Find the distribution of star ratings to the business in the following cities:

i. Avon

SQL code used to arrive at answer:

```sql
SELECT stars, COUNT(stars) AS Count 
FROM business
WHERE city = 'Avon'
GROUP BY stars
ORDER BY stars ASC
```


Copy and Paste the Resulting Table Below (2 columns – star rating and count):

| stars | Count |
|-------|-------|
|   1.5 |     1 |
|   2.5 |     2 |
|   3.5 |     3 |
|   4.0 |     2 |
|   4.5 |     1 |
|   5.0 |     1 |


ii. Beachwood

SQL code used to arrive at answer:

```sql
SELECT stars, COUNT(stars) AS Count 
FROM business
WHERE city = 'Beachwood'
GROUP BY stars
ORDER BY stars ASC
```

Copy and Paste the Resulting Table Below (2 columns – star rating and count):
	
| stars | Count |
|-------|-------|
|   2.0 |     1 |
|   2.5 |     1 |
|   3.0 |     2 |
|   3.5 |     2 |
|   4.0 |     1 |
|   4.5 |     2 |
|   5.0 |     5 |


### 7. Find the top 3 users based on their total number of reviews:
		
SQL code used to arrive at answer:

```sql
SELECT name, review_count AS ReviewCount 
FROM user
ORDER BY ReviewCount DESC
LIMIT 3
```
	
Copy and Paste the Result Below:

| name   | ReviewCount |
|--------|-------------|
| Gerald |        2000 |
| Sara   |        1629 |
| Yuri   |        1339 |
		

### 8. Does posing more reviews correlate with more fans?

Please explain your findings and interpretation of the results:

There seems to be no correlation between reviews and fans. Consider example of Gerald with 2000 reviews, which is highest but have
don't have the highest fans. Rather Amy with just 609 reviews have highest fans. Also consider users like William, Roanna, .Hon,
Yuri who have 1000+ reviews but don't have fans more than 150 which proves no correlation between reviews and fans.

SQL code: 

```sql
SELECT name, review_count, fans
FROM user
ORDER BY fans DESC
```

Results:
| name      | review_count | fans |
|-----------|--------------|------|
| Amy       |          609 |  503 |
| Mimi      |          968 |  497 |
| Harald    |         1153 |  311 |
| Gerald    |         2000 |  253 |
| Christine |          930 |  173 |
| Lisa      |          813 |  159 |
| Cat       |          377 |  133 |
| William   |         1215 |  126 |
| Fran      |          862 |  124 |
| Lissa     |          834 |  120 |
| Mark      |          861 |  115 |
| Tiffany   |          408 |  111 |
| bernice   |          255 |  105 |
| Roanna    |         1039 |  104 |
| Angela    |          694 |  101 |
| .Hon      |         1246 |  101 |
| Ben       |          307 |   96 |
| Linda     |          584 |   89 |
| Christina |          842 |   85 |
| Jessica   |          220 |   84 |
| Greg      |          408 |   81 |
| Nieves    |          178 |   80 |
| Sui       |          754 |   78 |
| Yuri      |         1339 |   76 |
| Nicole    |          161 |   73 |


	
### 9. Are there more reviews with the word "love" or with the word "hate" in them?

**Answer: Reviews with the word "love" (1780) are more than those with the word "hate" (232).**


SQL code used to arrive at answer:

```sql
SELECT COUNT(CASE WHEN text LIKE '%love%' THEN text END) AS CountLove,
COUNT(CASE WHEN text LIKE '%hate%' THEN text END) AS CountHate
FROM review
```

Results:
| CountLove | CountHate |
|-----------|-----------|
|      1780 |       232 |

	
	
### 10. Find the top 10 users with the most fans:

SQL code used to arrive at answer:

```sql
SELECT name, fans
FROM user
ORDER BY fans DESC
LIMIT 10
```

Copy and Paste the Result Below:

| name      | fans |
|-----------|------|
| Amy       |  503 |
| Mimi      |  497 |
| Harald    |  311 |
| Gerald    |  253 |
| Christine |  173 |
| Lisa      |  159 |
| Cat       |  133 |
| William   |  126 |
| Fran      |  124 |
| Lissa     |  120 |
	
		

## Part 2: Inferences and Analysis

### 1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.
	
City: **Las Vegas**	

Category: **Shopping**

#### i. Do the two groups you chose to analyze have a different distribution of hours?
**Yes.** There is a difference in the distribution of hours in the business belonging to different groups. 2-3 stars group have longer 
working hours compared to 4-5 stars group as shown in the table below.


#### ii. Do the two groups you chose to analyze have a different number of reviews?
**Yes.** Number of reviews is positively correlated to star rating they have. 2-3 stars group have a total of 6 reviews while businesses
from 4-5 stars group have 36 reviews which highlights the difference.
         
         
#### iii. Are you able to infer anything from the location data provided between these two groups? Explain.
**Yes,** although all the businesses are situated in Las Vegas, the postal code of each business is different. This means each business
is located in different neighborhoods or districts within Las Vegas.


SQL code used for analysis:

```sql
SELECT name, city, postal_code, latitude, longitude,
CASE 
    WHEN stars BETWEEN 2.0 AND 3.0 THEN '2-3'   -- creating new column starRange with label encoding of star ratings
    WHEN stars BETWEEN 4.0 AND 5.0 THEN '4-5'
    ELSE NULL
END starRange,
review_count, hours 
FROM business b
INNER JOIN category c ON b.id = c.business_id
INNER JOIN hours h ON b.id = h.business_id
WHERE category = 'Shopping' AND city = 'Las Vegas' AND starRange IS NOT NULL
ORDER BY starRange ASC
```

Result:
| name                           | city      | postal_code | latitude | longitude | starRange | review_count | hours                |
|--------------------------------|-----------|-------------|----------|-----------|-----------|--------------|----------------------|
| Walgreens                      | Las Vegas | 89121       |  36.1007 |  -115.091 | 2-3       |            6 | Monday|8:00-22:00    |
| Walgreens                      | Las Vegas | 89121       |  36.1007 |  -115.091 | 2-3       |            6 | Tuesday|8:00-22:00   |
| Walgreens                      | Las Vegas | 89121       |  36.1007 |  -115.091 | 2-3       |            6 | Friday|8:00-22:00    |
| Walgreens                      | Las Vegas | 89121       |  36.1007 |  -115.091 | 2-3       |            6 | Wednesday|8:00-22:00 |
| Walgreens                      | Las Vegas | 89121       |  36.1007 |  -115.091 | 2-3       |            6 | Thursday|8:00-22:00  |
| Walgreens                      | Las Vegas | 89121       |  36.1007 |  -115.091 | 2-3       |            6 | Sunday|8:00-22:00    |
| Walgreens                      | Las Vegas | 89121       |  36.1007 |  -115.091 | 2-3       |            6 | Saturday|8:00-22:00  |
| Red Rock Canyon Visitor Center | Las Vegas | 89161       |  36.1357 |  -115.428 | 4-5       |           32 | Monday|8:00-16:30    |
| Red Rock Canyon Visitor Center | Las Vegas | 89161       |  36.1357 |  -115.428 | 4-5       |           32 | Tuesday|8:00-16:30   |
| Red Rock Canyon Visitor Center | Las Vegas | 89161       |  36.1357 |  -115.428 | 4-5       |           32 | Friday|8:00-16:30    |
| Red Rock Canyon Visitor Center | Las Vegas | 89161       |  36.1357 |  -115.428 | 4-5       |           32 | Wednesday|8:00-16:30 |
| Red Rock Canyon Visitor Center | Las Vegas | 89161       |  36.1357 |  -115.428 | 4-5       |           32 | Thursday|8:00-16:30  |
| Red Rock Canyon Visitor Center | Las Vegas | 89161       |  36.1357 |  -115.428 | 4-5       |           32 | Sunday|8:00-16:30    |
| Red Rock Canyon Visitor Center | Las Vegas | 89161       |  36.1357 |  -115.428 | 4-5       |           32 | Saturday|8:00-16:30  |
| Desert Medical Equipment       | Las Vegas | 89118       |  36.0964 |  -115.187 | 4-5       |            4 | Friday|8:00-17:00    |
| Desert Medical Equipment       | Las Vegas | 89118       |  36.0964 |  -115.187 | 4-5       |            4 | Tuesday|8:00-17:00   |
| Desert Medical Equipment       | Las Vegas | 89118       |  36.0964 |  -115.187 | 4-5       |            4 | Thursday|8:00-17:00  |
| Desert Medical Equipment       | Las Vegas | 89118       |  36.0964 |  -115.187 | 4-5       |            4 | Wednesday|8:00-17:00 |
| Desert Medical Equipment       | Las Vegas | 89118       |  36.0964 |  -115.187 | 4-5       |            4 | Monday|8:00-17:00    |

		
		
### 2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
i. **Difference 1:** Average ratings of open businesses is more than those which are closed.
         
         
ii. **Difference 2:** Large difference in review count of open businesses as open business tends to get more review and ratings compared
to closed businesses.

iii. **Difference 3:** Based on Query 2, the checkin count is low for closed business as no customer footfall being experienced in the 
closed shops, while lot of open business have hugh customer footfall.
         
         
         
SQL code used for analysis:

**Query 1:**
```sql
SELECT is_open, AVG(stars) AS AverageRating, SUM(review_count) AS ReviewCount
FROM business
GROUP BY is_open
```

| is_open |     AverageRating | ReviewCount |
|---------|-------------------|-------------|
|       0 | 3.520394736842105 |       35261 |
|       1 | 3.679009433962264 |      269300 |

**Query 2:**
```sql
SELECT is_open, SUM(count) AS CheckinCount
FROM business b INNER JOIN checkin c ON b.id = c.business_id
GROUP BY is_open
```

| is_open | CheckinCount |
|---------|--------------|
|       0 |           15 |
|       1 |          823 |
	
	
### 3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
#### i. Indicate the type of analysis you chose to do: 
**Predict the Customer Footfall to Restaurants.**
         
         
#### ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
To predict the number range of checkin to restaurants across the different states and countries based on selected business information.
The prediction will help to make an assumption on the volume of customers to the establishment. This allows for better planning and 
management of the customer service. Will use the checkin table and business table for the purpose. Also the prediction can be drilled
down to predict the busy hours for the restaurants using date column in checkin table.
                           
                  
#### iii. Output of your finished dataset:
| name                                | city      | state | stars | review_count | DayOfWeek | Hour  | checkin_count |
|-------------------------------------|-----------|-------|-------|--------------|-----------|-------|---------------|
| Stella's Pizza & Italian Restaurant | Avon Lake | OH    |   2.0 |           16 | Friday    | 21:00 |             1 |
| Stella's Pizza & Italian Restaurant | Avon Lake | OH    |   2.0 |           16 | Monday    | 15:00 |             1 |
| Stella's Pizza & Italian Restaurant | Avon Lake | OH    |   2.0 |           16 | Monday    | 22:00 |             1 |
| Stella's Pizza & Italian Restaurant | Avon Lake | OH    |   2.0 |           16 | Thursday  | 0:00  |             1 |
| Stella's Pizza & Italian Restaurant | Avon Lake | OH    |   2.0 |           16 | Sunday    | 0:00  |             2 |
| Stella's Pizza & Italian Restaurant | Avon Lake | OH    |   2.0 |           16 | Sunday    | 1:00  |             1 |
| Stella's Pizza & Italian Restaurant | Avon Lake | OH    |   2.0 |           16 | Sunday    | 23:00 |             1 |
| Stella's Pizza & Italian Restaurant | Avon Lake | OH    |   2.0 |           16 | Sunday    | 20:00 |             1 |
| Stella's Pizza & Italian Restaurant | Avon Lake | OH    |   2.0 |           16 | Tuesday   | 22:00 |             1 |
| Stella's Pizza & Italian Restaurant | Avon Lake | OH    |   2.0 |           16 | Saturday  | 21:00 |             1 |
| Stella's Pizza & Italian Restaurant | Avon Lake | OH    |   2.0 |           16 | Saturday  | 23:00 |             3 |
| Stella's Pizza & Italian Restaurant | Avon Lake | OH    |   2.0 |           16 | Saturday  | 1:00  |             1 |
| Pizza Cutter                        | Avon Lake | OH    |   4.0 |           11 | Tuesday   | 22:00 |             1 |
| Pizza Cutter                        | Avon Lake | OH    |   4.0 |           11 | Tuesday   | 0:00  |             2 |
| Pizza Cutter                        | Avon Lake | OH    |   4.0 |           11 | Tuesday   | 1:00  |             3 |
| Pizza Cutter                        | Avon Lake | OH    |   4.0 |           11 | Tuesday   | 21:00 |             1 |
| Pizza Cutter                        | Avon Lake | OH    |   4.0 |           11 | Wednesday | 21:00 |             1 |
| Pizza Cutter                        | Avon Lake | OH    |   4.0 |           11 | Wednesday | 23:00 |             3 |
| Pizza Cutter                        | Avon Lake | OH    |   4.0 |           11 | Wednesday | 17:00 |             1 |
| Pizza Cutter                        | Avon Lake | OH    |   4.0 |           11 | Monday    | 23:00 |             2 |
| Pizza Cutter                        | Avon Lake | OH    |   4.0 |           11 | Monday    | 22:00 |             3 |
| Pizza Cutter                        | Avon Lake | OH    |   4.0 |           11 | Monday    | 18:00 |             1 |
| Pizza Cutter                        | Avon Lake | OH    |   4.0 |           11 | Monday    | 21:00 |             3 |
| Pizza Cutter                        | Avon Lake | OH    |   4.0 |           11 | Sunday    | 19:00 |             1 |
| Pizza Cutter                        | Avon Lake | OH    |   4.0 |           11 | Saturday  | 19:00 |             1 |

(Output limit exceeded, 25 of 510 total rows shown)
         
         
#### iv. Provide the SQL code you used to create your final dataset:

```sql
SELECT name, city, state, stars, review_count, 
    SUBSTR(date, 0, INSTR(date, '-')) AS DayOfWeek,   -- seperating day and hour for more refined data analysis and prediction
    SUBSTR(date, INSTR(date, '-')+1) AS Hour, COUNT AS checkin_count   -- INSTR is index of substring in the string
FROM business b
INNER JOIN checkin c ON b.id = c.business_id
```
