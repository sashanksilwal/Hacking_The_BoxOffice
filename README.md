# Hacking_The_BoxOffice
**Authors:** Ngoc Hoang, Maryam Khalili, Alem Shaimardanov, Sashank Silwal
 
 

Hacking the Box Office is a data analysis project that aims to identify the factors that contribute to the financial success of movies in the box office. By analyzing data from IMDb and The Movie Database, we explore how factors such as genre, budget, cast and crew, and release date impact a movie's revenue and profitability.

## Data Sources

The bulk of our data is sourced from IMDb’s public datasets, which contain the basic information – such as year of release, genres, principal cast and crew, etc. – for all titles available on IMDb. From all available IMDb datasets, we mainly made use of the following:

title.basics.tsv.gz: containing basic information for the titles including languages, title types (movie, short, TV series, TV episode, etc.), year of release, genres.
title.principals.tsv.gz: contains the principal cast and crew for the titles.
title.ratings.tsv.gz: contains the votes and ratings that the titles have received on IMDb.
Since the data available from IMDb does not contain information on the budget and revenue of the movies, we used data available from a second source, The Movie Database (TMDB).

## Data Cleaning

**Figure 1:** Data Cleaning Pipeline
<img width="1010" alt="Screen Shot 2023-02-20 at 11 32 32 PM" src="https://user-images.githubusercontent.com/25387553/220186128-aeb7e825-5f5e-4a4d-b033-46c56f914ce6.png">


Starting from the dataset of all titles available on IMDb (over 9 million titles), we first filtered out only those of type movies. This left us with over 600,000 movies, which we then filtered by our time window of interest (2000 - 2019, inclusive on both ends) to keep over 230,000 movies. We dropped all movies of genre animation, for these movies include only voice actors who do not appear on screen and thus are presumably irrelevant to our analysis. We also kept only movies that are in English.

From this pool of remaining movies, we used the TMDB API to query their budget and revenue data. Out of over 230,000 movies, 3,721 movies returned query results that include budget and revenue data. We conducted manual inspection on these movies to check for possible data entry errors. Some movies have seemingly infeasible budget or revenue, for example, movies with budget/revenue under 500 (USD). We manually checked other sources e.g. Wikipedia to fix such issues wherever more accurate data is available. Those that we could not find reliable information for, even after manual inspection, were dropped. We also dropped movies where there are no principal cast i.e. no actors and actresses are listed.

## Results

Our finalized dataset of movies span 21 genres, where some of the genres with highest counts of movies include drama, comedy, action, and crime, whereas some of the genres with the lowest counts are news, western, documentary, and musical, among others. We detected 14,122 principal roles, corresponding to 5,273 unique actors and actresses.

We included profit in our analysis, which is calculated by subtracting budget from revenue. It can be observed that since budget stays relatively stable through the year, the profit generally reflects the same trends as revenue.

We used the Ethnicolor API to identify the race of each principal cast member in our dataset. This API uses a combination of US census data, Florida voting registration data, and Wikipedia data to predict a person’s race and ethnicity based on their first and last names. However, we found that the API had some errors in predicting the race of certain cast members.

**Figure 2:** Average budget, revenue, and profit by year. For a certain movie, profit = revenue - budget. Both
revenue and budget considered are adjusted for inflation.
<img width="1006" alt="Screen Shot 2023-02-20 at 11 33 08 PM" src="https://user-images.githubusercontent.com/25387553/220186207-f6dda27e-82b1-4f97-b8d1-83dd2af2fdc3.png">

**Figure 3:** Gender differences in the film industry.
<img width="1140" alt="Screen Shot 2023-02-20 at 11 36 43 PM" src="https://user-images.githubusercontent.com/25387553/220186694-4c776b5a-e949-4008-afb1-40e0998dd29f.png">


**Figure 4:** Distribution of role orderings by gender and ethnicity. The majority of movies (N = 3491) list four
cast members in the principal cast. For movies with more than five cast members, (N = 10), all roles after the
fourth roles are grouped into Roles #4.
<img width="994" alt="Screen Shot 2023-02-20 at 11 34 09 PM" src="https://user-images.githubusercontent.com/25387553/220186349-9d3b3bd9-9a34-4cbd-bc9c-6fbf16091f0b.png">


## Conclusion

This project offers insights into the factors that contribute to the financial success of movies in the box office. By analyzing data from IMDb and The Movie Database, we demonstrate how genre, budget, cast and crew, and release date impact a movie's revenue and profitability. Our findings can inform movie production
