
# Project Overview

This project focuses on building a movie recommendation system using several movie datasets. The goal of this project is to assist users in finding movies that match their preferences by utilizing recommendation algorithms. 

With the ever-growing amount of content in the entertainment industry, recommendation systems have become very important to offer personalized suggestions to users. This project aims to implement a **Content-Based Filtering** approach, to address the problem of finding movies that users want to watch based on user preferences.

# Business Understanding

### Problem Statements:
- How can we build a movie recommendation system that provides personalized movie suggestions to users?
- How accurate is the built recommendation system to provide relevant and satisfying movie suggestions to users, so as to enhance user experience in selecting content according to their preferences? 

### Goals:
- To develop a recommendation system that provides accurate movie recommendations.
- To implement the Content-Based Filtering recommendation approach.

### Solution Approach:
1. **Content-Based Filtering**: This approach uses movie metadata (such as genre, keywords) to recommend similar movies based on the user's previous preferences.

# Data Understanding

### Dataset:
- **Movies Metadata**: Contains metadata for movies such as genre, title, release date, etc. However, when modeled, only the columns `original_title`, `genres`, `vote_average`, `overview` and `Id` are used.
- **Keywords Dataset**: Contains keywords associated with the movie.
- **Disney+Movie**: Contains metadata for movies such as title, release year, watch rating, minimum duration, genre, rating, votes, movie director.

### Data Source:
- [The Movies Dataset](https://www.kaggle.com/rounakbanik/the-movies-dataset)
- Disney+ Movies

# Modeling and Result

Here are some steps in making a recommendation system built using the **Content-Based Filtering** approach:

1. **Content-Based Filtering**:
   - Using **TF-IDF Vectorizer** to extract features.
   - Apply **Cosine Similarity** to find the movie that is most similar to the user's preference.
   - Creating a function to generate 15 recommended movies based on user preferences.
   - With the method used, it is efficient in recommending movies with similar characteristics according to what the user is looking for or what the user is interested in.
   
### Top-15 Recommendations:
- The **`Content-Based Filtering`** approach provides a Top-15 list of recommended movies based on user preferences.

# Evaluation

### Evaluation Metrics:
1. **Cosine Similarity** is used to measure how similar the movies are in terms of their attributes (for content-based filtering).
2. **Precision** is used to evaluate the performance of content-based filtering based on user preferences. The precision score achieved was **73.3%**.”

This metric was chosen because it fits the purpose of recommending movies based on similarity or based on user interaction. 

### Conclusion:
Overall, the developed model has provided a fairly good solution to the problem statement, with a precision of 73.3% which shows that the model is able to provide accurate recommendations. The model also managed to achieve the goals set, although there is room for further improvement to enhance precision and user experience.

Precision measures how accurate the recommendations provided by the model are, i.e. the proportion of recommended movies that users liked out of all those suggested. A value of 73.3% indicates that about 3 out of 4 recommended movies match the user's preferences. This means that the model successfully provides relevant and quality recommendations and addresses the need to provide personalized suggestions.

# Tools and Language Used in This Project
- Python programming language
- Pandas
- NumPy
- Seaborn
- Matplotlib
- Difflib
- scikit-learn
