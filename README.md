# no_sql_challenge

## Instructions
The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. You've been contracted by the editors of a food magazine, Eat Safe, Love, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.

## Part 1: Database and Jupyter Notebook Set Up
I used the given "NoSQL_setup_starter.ipynb" file to begin this challenge, which already included things like the necessary imports and certain bits of code to get started. I imported the db to python using the required --jsonArray parameter to successfully create the file and the --drop parameter to drop it if it already existed. The names given in the assignment for the db was "uk_food" and the given collection name was "establishments". The text used to import were copy and pasted into the markdown file as required by the assignment.

Once I had navigated into my dev environment and imported the necessary libraries, I created an instance of the Mongo client and confirmed my db and data were correctly imported by listing the databases available in MongoDB and the collections available in the "uk_food" db. I printed the first document to take a look at the key value pairs for the different areas of the collection after I had designated the variable "establishments" as the stand-in for the db.collection.


## Part 2: Update the Database
As before, I used the given starter file of the same name as in part 1. The editors of the magaine have requested modifications to the database before any analysis is done. The changes I made included adding a new halal restaurant called "Penang Flavours". I used the parameters given in the challenge documents and copy/pasted them into the VSCode. I confirmed the restaurant was added by printing it. Afterwards, I found the accurate "BusinessTypeID" for the type of business the halal restaurante is by running a query against other restaurantes of that type returning only the "BusinessTypeID" and "BusinessType" key/values. The business ID was "1", so I updated that value for the new restaurant.

The magazine I work for in this scenario is not focused on any establishments in Dover, so I deleted all establishments in that Local Authority from the database, and I confirmed my work by printing the number of documents before and after the deletion.

The next step of updating the db was to correct some of the data types. All of the numbers values were in the string format, and they needed to be changed to different formats. I updated latitude and longitude to decimals using "update_many" and updated the "RatingValue" values to integers using "update_many"

## Part 3: Exploratory Analysis
My Magazine, "Eat Safe, Love" has questions they want answered about these establishments to sort through the establishments that are or are not worth visiting. The starter file for the analyzation portion of the assignment was "NoSQL_analysis_starter.ipynb", which again included the necessary inputs and bits of code to get the process started.

The questions and analysis are included below:
### Which establishments have a hygiene score equal to 20?
Note: Unlike what we might assume on a health inspection test, for the hygiene score listed here, lower is better.

There were 41 establishments with scores equal to exactly 20 with business types ranging from elderly care facilities to sandwich shops, hotels, and regular restaurants. I was a bit surprised this number was as low as it was given the number of establishments in the dataset. The establishments were saved to a df called "query1_df".

### Which establishments in London have a RatingValue greater than or equal to 4?
Note: "RatingVAlue" is the overall rating given by the Food Authority. Scores are given 1-5 with the higher score being better.

The number of establishments in London found to have a score of at least 4 was 33. Again, I thought this value seemed low given the number of establishments that would exist in a city like London. Given that the Local Authority for London is actually not just the name London like it was with Dover earlier, I needed to use '$regex' in my query to find the necessary establishments. Again there were a wide range of establishments included in the results including cruises, restaurants, caterers, even one listed in the "Retailers - other" busines type. Looking at the .head(10) for the query2_df, these establishments typically obtained scores lower than 20 for their hygiene score. 

### What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?

This was the query I was most excited to look into because it seemed to be of the most value to a specific company. In this case that company was Penang Flavours. Looking at the top 5 establishments in their area can help determine the competition they will face and whether or not they can carve out a specific niche if they can score high enough with the Food Authority. The restaurants that were listed were: "Volunteer" (a pub/bar/nightclub), "Plumstead Manor Nursery" (a care center), "Lumbini Grocery LTD" (a grocer), "Iceland" (a supermarket), and "Howe and Co Fish and Chips-Van 17" (a food truck). Looking at these results, there doesn't appear to be any establishment in direct competition with the new establishment. In fact, none of the establishments listed seem anywhere close to Penang Flavours, so this business could carve out good business for themselves should they perform highly.

### How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas.

This is another query that I was very interested in as, if I were working for a magazine, it would help minimize costs of having my writers traveling to various different places. For example, the Local Authority of Thanet, which had the most establihsments with a hygiene score at 0 with 1,130, would be a great place to have writers visit often because of the variety and number of establishments available for them to visit. It also just so happens to be on the coast East of London, so travel should be fairly easy. A magazine could write for quite a while by visiting just the top ten Local Authorities with some stops in to cities like London and Manchester as well.
