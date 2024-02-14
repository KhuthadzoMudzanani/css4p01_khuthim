# CSS Project Option 1
import pandas as pd
# Load the dataset
df = pd.read_csv('movie_dataset.csv')

# Display the structure of the dataset to see column names
print(df.head())

#              Question 1 
          
# The dataset has a column named 'Rating' that represents the movie ratings
# If your dataset has a different column name, replace 'Rating' accordingly
highest_rated_movie = df[df['Rating'] == df['Rating'].max()]

# Display the highest-rated movie
print("Highest Rated Movie:")
print(highest_rated_movie[['Title', 'Rating']])

#            Question 2
# Check for missing values in the 'Revenue (Millions)' column and handle them if necessary
# Fill missing values with the mean of the column
df['Revenue (Millions)'] = df['Revenue (Millions)'].fillna(df['Revenue (Millions)'].mean())

# Calculate the average revenue
average_revenue = df['Revenue (Millions)'].mean()

print("Average Revenue:", average_revenue)

#           Question 3
# Filter movies released between 2015 and 2017
filtered_df = df[(df['Year'] >= 2015) & (df['Year'] <= 2017)]

# Check for missing values in the 'Revenue' column and drop rows with missing values
filtered_df = filtered_df.dropna(subset=['Revenue (Millions)'])

# Calculate the average revenue
average_revenue = filtered_df['Revenue (Millions)'].mean()

print("Average Revenue of Movies from 2015 to 2017:", average_revenue)

#           Question 4
# Filter the DataFrame to include only movies released in the year 2016
movies_2016 = df[df['Year'] == 2016]

# Get the count of movies released in 2016
number_of_movies_2016 = len(movies_2016)

print(f"The number of movies released in 2016 is: {number_of_movies_2016}")

#            Question 5
# Filter rows where the director is Christopher Nolan
nolan_movies = df[df['Director'] == 'Christopher Nolan']

# Get the count of movies directed by Christopher Nolan
number_of_movies = len(nolan_movies)

# Print the result
print(f"Number of movies directed by Christopher Nolan: {number_of_movies}")

#            Question 6
# Filter movies with a rating of at least 8.0
high_rated_movies = df[df['Rating'] >= 8.0]

# Get the number of movies with a rating of at least 8.0
num_high_rated_movies = len(high_rated_movies)

print(f"Number of movies with a rating of at least 8.0: {num_high_rated_movies}")

#            Question 7
# Filter movies directed by Christopher Nolan
nolan_movies = df[df['Director'] == 'Christopher Nolan']

# Calculate the median rating
median_rating = nolan_movies['Rating'].median()

# Print the result
print(f"The median rating of movies directed by Christopher Nolan is: {median_rating}")

#            Question 8
# Group the DataFrame by the 'Year' and calculate the average rating for each year
average_ratings_by_year = df.groupby('Year')['Rating'].mean()

# Find the year with the highest average rating
year_highest_average_rating = average_ratings_by_year.idxmax()
highest_average_rating = average_ratings_by_year.max()

print(f"The year with the highest average rating is {year_highest_average_rating} with an average rating of {highest_average_rating:.2f}")

#            Question 9
# Filter movies released in 2006 and 2016
movies_2006 = df[df['Year'] == 2006]
movies_2016 = df[df['Year'] == 2016]

# Calculate the number of movies for each year
num_movies_2006 = len(movies_2006)
num_movies_2016 = len(movies_2016)

# Calculate the percentage increase
percentage_increase = ((num_movies_2016 - num_movies_2006) / num_movies_2006) * 100

# Print the result
print(f"Percentage Increase in the Number of Movies from 2006 to 2016: {percentage_increase:.2f}%")

#            Question 10
# Split the "Actors" column into a list of actors
df['Actors'] = df['Actors'].str.split(',')

# Create a list of all actors across all movies
all_actors = [actor.strip() for sublist in df['Actors'].dropna() for actor in sublist]

# Create a Pandas Series from the list of all actors
all_actors_series = pd.Series(all_actors)

# Find the most common actor
most_common_actor = all_actors_series.value_counts().idxmax()

print(f"The most common actor in all movies is: {most_common_actor}")

#            Question 11
# Split the genres in the "Genre" column and create a list of unique genres
unique_genres = set(df['Genre'].str.split('|').explode().unique())

# Print the number of unique genres
print("Number of unique genres:", len(unique_genres))

#            Question 12
# Select only numerical columns
numerical_columns = df.select_dtypes(include=['int64', 'float64'])

# Calculate correlation matrix
correlation_matrix = numerical_columns.corr()

# Print correlation matrix
print("Correlation Matrix:")
print(correlation_matrix)
