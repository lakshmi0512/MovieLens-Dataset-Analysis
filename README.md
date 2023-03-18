# MovieLens-Dataset-Analysis

# Dataset:

Dataset Description:
1. movies: (movies.dat)
- MovieID::Title::Genres
Titles are identical to titles provided by the IMDB (including year of release). Genres are pipe-separated and are selected from the following genres:
Action
Adventure
Animation
Children's
Comedy
Crime
Documentary
Drama
Fantasy
Film-Noir
Horror
Musical
Mystery
Romance
Sci-Fi
Thriller
War
Western
2. ratings: (ratings.dat)
- UserID::MovieID::Rating::Timestamp

UserIDs range between 1 and 6040
MovieIDs range between 1 and 3952
Ratings are made on a 5-star scale (whole-star ratings only)
Timestamp is represented in seconds since the epoch as returned by time(2)
3. users: (users.dat)
- UserID::Gender::Age::Occupation::Zip-code
Gender is denoted by a "M" for male and "F" for female
Age is chosen from the following ranges:
1: "Under 18"
18: "18-24"
25: "25-34"
35: "35-44"
45: "45-49"
50: "50-55"
56: "56+"
Occupation is chosen from the following choices:
0: "other" or not specified
1: "academic/educator"
2: "artist"
3: "clerical/admin"
4: "college/grad student"
5: "customer service"
6: "doctor/health care"
7: "executive/managerial"
8: "farmer"
9: "homemaker"
10: "K-12 student"
11: "lawyer"
12: "programmer"
13: "retired"
14: "sales/marketing"
15: "scientist"
16: "self-employed"
17: "technician/engineer"
18: "tradesman/craftsman"
19: "unemployed"
20: "writer"


# Data Cleaning methods:
We are using Pig framework for cleaning our dataset

Movie file:

Step 1: Read in movie data using CSVLoader to take care of double quoted fields
Step 2: Replace comma in titles with '#com#'
Step 2: Remove the first tuple (column headers)
Step 3: Seperate the genres out into a tuple.
Step 4: Seperate title from date.
Step 6: Write out file with '\t' seperator
Step 7: Read it back in with '\t' seperator.
Step 8: Fix the '#com#'
Step 9: Fix movies where 'The' comes at end of title
Step 10: Write out as tab seperated file.

Rating file:

Step 1: Read in the data using CSVLoader
Step 2: For some reason first row is empty so we must remove it
Step 3: Write out file using '\t' sep.

Tag file:

Step 1: Read in file using CSVLoader
Step 2: Remove header
Step 3: Remove quotation marks from tags
Step 4: Group user and movies to create bag of tags and timestamps
Step 5: Add column that shows length of tag applied for future analysis
Step 6: Convert all tags to lowercase
Step 7: Store file using '\t'

User file:

Step 1: Read in the data using CSVLoader
Step 2: For some reason first row is empty so we must remove it
Step 3: Write out file using '\t' sep.

# In this module we are using Hive to find the following parameters to analyse the Ratings of the movies and their distribution.

1) Distribution_Of_Ratings_Across_Genres using Hive.
We need to find the Distribution of ratings across all genres.
Read the data by creating the table to house the data, populate this table with data.
See how many times each star rating was given to a movie.

2) Distribution_Of_Ratings using Hive.
We need to find the Distribution of ratings in the dataset.
Read the data by creating the table, populate this table with data.
See how many times each star rating was given to a movie.

3) Most_Popular_Rating using Hive.
We need to find Most Popular Rating among the movies. 
Read the data by creating the table, populate this table with data.
Find the star rating that was most commonly given.


# In this module we are using Pig to find the following parameters:

1) Most Liked Movie using Pig.
We need to find the Most liked movie among all the movies in the dataset.
Read back in the joined cleaned up movie and rating file with the pipe as a delimiter
Count the number of each rating each movie has
Group the ratings together by their movie
Calculate the average rating for each movie
Find the most rated movie of all movies where the movies average rating is 4.6 or above
Find the multiple most rated movies of all movies where the movies average rating is 4.0 stars or above

2) Most_Rated_Movie using Pig.
We need to find the Most rated movie among all the movies in the dataset.
Read back in the joined cleaned up movie and rating file with the pipe as a delimiter
Count the number ratings each movie has
Find the movie with the most ratings

3) User_With_Highest_Average_Rating using Pig.
We need to find users with highest average rating among all the movies that users watch.
Read back in the joined cleaned up movie and rating file with the pipe as a delimiter
Group the data by each user
Get the average rating for each user
Get the users with 5-star rating who has the most number of ratings places
See if anybody else has 100 ratings placed and a 5-star average

