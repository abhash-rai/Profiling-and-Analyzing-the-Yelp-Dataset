# Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset Coursera Worksheet

This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular research question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate and communicate your intent as required.

For both parts of this assignment, use this "worksheet." It provides all the questions you are being asked, and your job will be to transfer your answers and SQL coding where indicated into this worksheet so that your peers can review your work. You should be able to use any Text Editor (Windows Notepad, Apple TextEdit, Notepad ++, Sublime Text, etc.) to copy and paste your answers. If you are going to use Word or some other page layout application, just be careful to make sure your answers and code are lined appropriately.
In this case, you may want to save as a PDF to ensure your formatting remains intact for you reviewer.

<br><br>
<img src="https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/hOlYbrgyEeeTsRKxhJ5OZg_517578844a2fd129650492eda3186cd1_YelpERDiagram.png?expiry=1679529600000&hmac=nvmhFxVZsplKHCI7ZFzklrQnhePMRDLMCO5LzAjUxH0" alt="Yelp Database Schema" style="width: 100%">
<h3 align="center"><b>Fig: Yelp Database Schema</b></h3>
<br><br>

<h1 align='center'>Part 1: Yelp Dataset Profiling and Understanding</h1>

## 1. Profile the data by finding the total number of records for each of the tables below:

<ol type="I">
  <li>Attribute table = 10000</li>
  <li>Business table = 10000</li>
  <li>Category table = 10000</li>
  <li>Checkin table = 10000</li>
  <li>elite_years table = 10000</li>
  <li>friend table = 10000</li>
  <li>hours table = 10000</li>
  <li>photo table = 10000</li>
  <li>review table = 10000</li>
  <li>tip table = 10000</li>
  <li>user table = 10000</li>
</ol>

## 2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.

<ol type="I">
  <li>Business = 10000</li>
  <li>Hours = 1562</li>
  <li>Category = 2643</li>
  <li>Attribute = 1115 </li>
  <li>Review = 9581 (Using foreign key - "user_id")</li>
  <li>Checkin = 493 </li>
  <li>Photo = 6493 (Using foreign key - "business_id")</li>
  <li>Tip = 537 (Using foreign key - "user_id")</li>
  <li>User = 10000</li>
  <li>Friend = 11</li>
</ol>

**Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.**

## 3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

> Answer: no.
	
	
**SQL code used to arrive at answer:**

```
select *
from user
where id is null
    or name is null
    or review_count is null
    or yelping_since is null
    or useful is null
    or funny is null
    or cool is null
    or fans is null
    or average_stars is null
    or compliment_hot is null
    or compliment_more is null
    or compliment_profile is null
    or compliment_cute is null
    or compliment_list is null
    or compliment_note is null
    or compliment_plain is null
    or compliment_cool is null
    or compliment_funny is null
    or compliment_writer is null
    or compliment_photos is null;
 ```
 
 ## 4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

I. Table: Review, Column: Stars
	
    min:1		max:5		avg:3.7082
		
	
II. Table: Business, Column: Stars
	
		min:1.0		max:5.0		avg:3.6549
		
	
III. Table: Tip, Column: Likes
	
		min:0		max:2		avg:0.0144
		
	
IV. Table: Checkin, Column: Count
	
		min:1		max:53		avg:1.9414
		
	
V. Table: User, Column: Review_count
	
		min:0		max:2000	avg:24.2995
		

## 5. List the cities with the most reviews in descending order:

**SQL code used to arrive at answer:**
	
    select 
        B.city,
        sum(review_count) as total_reviews
    from business B
    left join review R on
    R.id = B.id
    group by B.city
    order by total_reviews desc;
	
 **Copy and Paste the Result Below:**
	
    +-----------------+---------------+
    | city            | total_reviews |
    +-----------------+---------------+
    | Las Vegas       |         82854 |
    | Phoenix         |         34503 |
    | Toronto         |         24113 |
    | Scottsdale      |         20614 |
    | Charlotte       |         12523 |
    | Henderson       |         10871 |
    | Tempe           |         10504 |
    | Pittsburgh      |          9798 |
    | Montréal        |          9448 |
    | Chandler        |          8112 |
    | Mesa            |          6875 |
    | Gilbert         |          6380 |
    | Cleveland       |          5593 |
    | Madison         |          5265 |
    | Glendale        |          4406 |
    | Mississauga     |          3814 |
    | Edinburgh       |          2792 |
    | Peoria          |          2624 |
    | North Las Vegas |          2438 |
    | Markham         |          2352 |
    | Champaign       |          2029 |
    | Stuttgart       |          1849 |
    | Surprise        |          1520 |
    | Lakewood        |          1465 |
    | Goodyear        |          1155 |
    +-----------------+---------------+
    (Output limit exceeded, 25 of 362 total rows shown)


## 6. Find the distribution of star ratings to the business in the following cities:

### **I. Avon**

**SQL code used to arrive at answer:**

    select
        stars as Avon_star_rating,
        count(*) as count
    from business
    where city = 'Avon'
    group by Avon_star_rating;


**Copy and Paste the Resulting Table Below (2 columns – star rating and count):**

    +------------------+-------+
    | Avon_star_rating | count |
    +------------------+-------+
    |              1.5 |     1 |
    |              2.5 |     2 |
    |              3.5 |     3 |
    |              4.0 |     2 |
    |              4.5 |     1 |
    |              5.0 |     1 |
    +------------------+-------+


### **II. Beachwood**

**SQL code used to arrive at answer:**

    select
        stars as Beachwood_star_rating,
        count(*) as count
    from business
    where city = 'Beachwood'
    group by Beachwood_star_rating;

**Copy and Paste the Resulting Table Below (2 columns – star rating and count):**
	
    +-----------------------+-------+
    | Beachwood_star_rating | count |
    +-----------------------+-------+
    |                   2.0 |     1 |
    |                   2.5 |     1 |
    |                   3.0 |     2 |
    |                   3.5 |     2 |
    |                   4.0 |     1 |
    |                   4.5 |     2 |
    |                   5.0 |     5 |
    +-----------------------+-------+	


## 7. Find the top 3 users based on their total number of reviews:
		
**SQL code used to arrive at answer:**

    select
        id,
        name,
        review_count
    from user
    order by review_count desc
    limit 3;

**Copy and Paste the Result Below:**

    +------------------------+--------+--------------+
    | id                     | name   | review_count |
    +------------------------+--------+--------------+
    | -G7Zkl1wIWBBmD0KRy_sCw | Gerald |         2000 |
    | -3s52C4zL_DHRK0ULG6qtg | Sara   |         1629 |
    | -8lbUNlXVSoXqaRRiHiSNg | Yuri   |         1339 |
    +------------------------+--------+--------------+

## 8. Does posing more reviews correlate with more fans?

**Please explain your findings and interpretation of the results:**

When using below query:

    select
        review_count,
        fans
    from user
    order by fans desc;

We get the result:

    +--------------+------+
    | review_count | fans |
    +--------------+------+
    |          609 |  503 |
    |          968 |  497 |
    |         1153 |  311 |
    |         2000 |  253 |
    |          930 |  173 |
    |          813 |  159 |
    |          377 |  133 |
    |         1215 |  126 |
    |          862 |  124 |
    |          834 |  120 |
    |          861 |  115 |
    |          408 |  111 |
    |          255 |  105 |
    |         1039 |  104 |
    |          694 |  101 |
    |         1246 |  101 |
    |          307 |   96 |
    |          584 |   89 |
    |          842 |   85 |
    |          220 |   84 |
    |          408 |   81 |
    |          178 |   80 |
    |          754 |   78 |
    |         1339 |   76 |
    |          161 |   73 |
    +--------------+------+
    (Output limit exceeded, 25 of 10000 total rows shown) 

> **Looking at the result, the user with most fans of 503 has only 609 reviews. There are as far as users who reviewed twice as much as the top user but has fans 6.6 times lower than the top user. So, this finding suggest posing more reviews doesn't directly increase a user's fan and there are other factors which determine it.**

 
 
## 9. Are there more reviews with the word "love" or with the word "hate" in them?

>Answer: love

	
**SQL code used to arrive at answer:**

First, finding total reviews with the phrase 'love' using wildcards:

    select
        count(text) as reviews_with_love_phrase
    from review
    where text like "%love%";

Output:

    +--------------------------+
    | reviews_with_love_phrase |
    +--------------------------+
    |                     1780 |
    +--------------------------+

Then, finding total reviews with the phrase 'hate' using wildcards:

    select
        count(text) as reviews_with_hate_phrase
    from review
    where text like "%hate%";

Ouput:

    +--------------------------+
    | reviews_with_hate_phrase |
    +--------------------------+
    |                      232 |
    +--------------------------+
    

## 10. Find the top 10 users with the most fans:

**SQL code used to arrive at answer:**

    select 
    	name, 
	fans 
    from user
    order by fans desc
    limit 10;


**Copy and Paste the Result Below:**

    +-----------+------+
    | name      | fans |
    +-----------+------+
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
    +-----------+------+

<br><br><br>

<h1 align='center'>Part 2: Inferences and Analysis</h1>

#### 1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.
	
#### I. Do the two groups you chose to analyze have a different distribution of hours?
> Yes. Business with lower rating tend to open for more hours than higher rated business in Toronto, Ontario.

#### II. Do the two groups you chose to analyze have a different number of reviews?
> Yes. The higher rated business has slightly greater number of reviews in Toronto, Ontario.
         
#### III. Are you able to infer anything from the location data provided between these two groups? Explain.
> Yes. Businesses in Downtown Core were generally rated lower in Toronto, Ontario.

**SQL code used for analysis:**

    select
        B.neighborhood,
        B.latitude,
        B.longitude,
        max(B.city) as max_occuring_city,
        max(B.state) as max_occuring_state,
        avg(B.stars) as average_stars,
        avg(B.review_count) as average_review_count,
        avg( substr(substr(substr(H.hours, -11), -5), 1, 2) - substr(substr(H.hours, -11), 1, 2) ) as average_working_hours,
        count(*) as total_businesses_count
    from business B
    inner join hours H on 
    B.id = H.business_id
    -- I chose 'Toronto' as my choie city, 
    -- and 'state' as my choie of category with its value as 'ON'
    where B.city = 'Toronto' and B.state = 'ON'
    -- Grouping by overall (Average) star ratings now
    group by stars;
		
    
## 2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
#### I. Difference 1:
> Businesses that are still open has an average of 12.24 working hours which is 4 hours hours more than the businesses that are closed.
         
#### II. Difference 2:
> Businesses that are still open has slightly greater average review count as compared with those that are closed.

#### III. Difference 3:
> 'York' city has the highest number of open businesses while, 'Toronto' has the greatest number of closed businesses.
         
**SQL code used for analysis:**

    select
        case
            when B.is_open = 1 then "Open"
            else "Closed"
        end as is_open,
        max(B.city) as max_occuring_city,
        max(B.state) as max_occuring_state,
        avg(B.stars) as average_stars,
        avg(B.review_count) as average_review_count
    from business B
    inner join hours H on 
    B.id = H.business_id
    group by is_open;



## 3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
#### I. Indicate the type of analysis you chose to do:
> Predicting the star rating for a business.
         
#### II. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
	
> I've prepare the yelp dataset so as to enable a machine learning alorithm to use the dataset to make predictions about any business start rating. The dataset output from my query can be used to feed into a ML model directly as it is already clean. Although, data transformation may be required if needed. Note: The dataset will contain numeric as well as categorical data. <br><br> The dataset has 743 rows by 8 column features out of which 2 are categorical and 6 are numeric data. I've renamed the column feature name so as to perfectly depict what the column is about. So, understanding the dataset won't be a problem. Have fun with it!
                  
#### III. Output of your finished dataset:
        
    +---------+----------+-------+----------+-----------+--------------+---------------+-------+
    | is_open | city     | state | latitude | longitude | review_count | working_hours | stars |
    +---------+----------+-------+----------+-----------+--------------+---------------+-------+
    |       1 | Aurora   | OH    |    41.32 |  -81.3487 |           32 |             5 |   3.5 |
    |       1 | Aurora   | OH    |    41.32 |  -81.3487 |           32 |             5 |   3.5 |
    |       1 | Aurora   | OH    |    41.32 |  -81.3487 |           32 |             3 |   3.5 |
    |       1 | Aurora   | OH    |    41.32 |  -81.3487 |           32 |             5 |   3.5 |
    |       1 | Aurora   | OH    |    41.32 |  -81.3487 |           32 |             6 |   3.5 |
    |       1 | Aurora   | OH    |    41.32 |  -81.3487 |           32 |             3 |   3.5 |
    |       1 | Avondale | AZ    |   33.465 |  -112.291 |           30 |            17 |   3.0 |
    |       1 | Avondale | AZ    |   33.465 |  -112.291 |           30 |            19 |   3.0 |
    |       1 | Avondale | AZ    |   33.465 |  -112.291 |           30 |             9 |   3.0 |
    |       1 | Avondale | AZ    |   33.465 |  -112.291 |           30 |             9 |   3.0 |
    |       1 | Avondale | AZ    |   33.465 |  -112.291 |           30 |            19 |   3.0 |
    |       1 | Brampton | ON    |  43.6765 |  -79.8244 |            8 |             9 |   3.5 |
    |       1 | Brampton | ON    |  43.6765 |  -79.8244 |            8 |             9 |   3.5 |
    |       1 | Brampton | ON    |  43.6765 |  -79.8244 |            8 |             9 |   3.5 |
    |       1 | Brampton | ON    |  43.6765 |  -79.8244 |            8 |             9 |   3.5 |
    |       1 | Brampton | ON    |  43.6765 |  -79.8244 |            8 |             6 |   3.5 |
    |       1 | Brampton | ON    |  43.6765 |  -79.8244 |            8 |            18 |   3.5 |
    |       0 | Chandler | AZ    |  33.3028 |  -111.842 |          141 |             0 |   3.0 |
    |       0 | Chandler | AZ    |  33.3028 |  -111.842 |          141 |             0 |   3.0 |
    |       0 | Chandler | AZ    |  33.3028 |  -111.842 |          141 |            -2 |   3.0 |
    |       0 | Chandler | AZ    |  33.3028 |  -111.842 |          141 |             0 |   3.0 |
    |       0 | Chandler | AZ    |  33.3028 |  -111.842 |          141 |             0 |   3.0 |
    |       0 | Chandler | AZ    |  33.3028 |  -111.842 |          141 |             0 |   3.0 |
    |       0 | Chandler | AZ    |  33.3028 |  -111.842 |          141 |            -2 |   3.0 |
    |       1 | Chandler | AZ    |  33.3496 |  -111.892 |            5 |            17 |   4.0 |
    +---------+----------+-------+----------+-----------+--------------+---------------+-------+
    (Output limit exceeded, 25 of 743 total rows shown) 
         
#### IV. Provide the SQL code you used to create your final dataset:

    select
        B.is_open,
        B.city,
        B.state,
        B.latitude,
        B.longitude,
        B.review_count,
        substr(substr(substr(H.hours, -11), -5), 1, 2) - substr(substr(H.hours, -11), 1, 2) as working_hours,
        B.stars
    from business B
    inner join hours H on 
    B.id = H.business_id
    order by B.city, B.state, B.stars;
