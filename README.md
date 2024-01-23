# Movie Recommendation System

This project implements a movie recommendation system using content-based filtering. The system suggests movies based on textual features such as genres, keywords, cast, and crew information. The implementation is done in Python using Jupyter Notebook.

## Prerequisites

Make sure you have the required libraries installed. You can install them using the following:

```bash
pip install pandas scikit-learn
```

## Dataset

The project uses the [TMDB 5000 Movie Dataset](https://www.kaggle.com/tmdb/tmdb-movie-metadata), which includes information about movies, credits, and genres. The dataset is loaded into a Pandas DataFrame for analysis and recommendation.

## Getting Started

1. **Mount Google Drive:**
   If you are using Google Colab, mount your Google Drive to access the dataset. Update the file paths accordingly.

   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```

2. **Load and Merge Dataset:**
   Load the movie dataset and credits dataset, and merge them based on the 'title' column.

   ```python
   movies_df = pd.read_csv('/content/drive/MyDrive/tmdb_5000_movies.csv')
   credits = pd.read_csv('/content/drive/MyDrive/tmdb_5000_credits.csv')
   movies_df = movies_df.merge(credits, on='title')
   ```

3. **Preprocess and Combine Features:**
   Combine relevant features (genres, keywords, cast, crew) into a single column and fill any missing values.

   ```python
   movies_df['combined_features'] = movies_df['genres'] + " " + movies_df['keywords'] + " " + movies_df['cast'] + " " + movies_df['crew']
   movies_df = movies_df.fillna('')
   ```

4. **Vectorize Text Data:**
   Use CountVectorizer to convert text data into a matrix of token counts.

   ```python
   from sklearn.feature_extraction.text import CountVectorizer
   count_vectorizer = CountVectorizer()
   count_matrix = count_vectorizer.fit_transform(movies_df['combined_features'])
   ```

5. **Calculate Cosine Similarity:**
   Calculate cosine similarity between movies based on the combined features.

   ```python
   from sklearn.metrics.pairwise import cosine_similarity
   cosine_sim = cosine_similarity(count_matrix, count_matrix)
   ```

6. **Recommendation Function:**
   Implement a function to recommend movies based on user input (movie title).

   ```python
   def recommend_movies(movie_title):
       # Implementation details in the code
   ```

7. **Test the Recommendation System:**
   Test the recommendation system by providing a movie title.

   ```python
   user_input_movie = "The Dark Knight Rises"
   recommended_movies = recommend_movies(user_input_movie)
   print(f"Recommended movies for {user_input_movie}:")
   for i, movie in enumerate(recommended_movies, 1):
       print(f"{i}. {movie}")
   ```

## Genre-Based Recommendation

Additionally, the project includes a function to recommend movies based on a specified genre.

```python
def recommend_movies_by_genre(user_input_genre):
    # Implementation details in the code
```

Test the genre-based recommendation system by providing a genre.

```python
user_input_genre = "Action"
recommended_genre_movies = recommend_movies_by_genre(user_input_genre)
print(f"Recommended {user_input_genre} movies:")
for i, movie in enumerate(recommended_genre_movies, 1):
    print(f"{i}. {movie}")
```

## Conclusion

This movie recommendation system provides personalized suggestions based on user input and is customizable to recommend movies from a specific genre. Feel free to explore and modify the code to suit your preferences and dataset characteristics.
