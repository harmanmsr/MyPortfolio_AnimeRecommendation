# Domain Proyek
The domain of this project is the entertainment and animation industry, specifically in the context of anime recommendations. Anime is a popular form of entertainment among Japanese culture lovers and has many fans around the world. An anime recommendation system can help users find new anime that match their preferences and interests.

## Background
Anime is a popular form of entertainment among lovers of Japanese culture and has a large fan base worldwide. With the rapid growth of the anime industry, the number of anime available is becoming more and more numerous and diverse. This can make it difficult for users to find an anime that suits their interests and preferences amidst the variety of options available.

Anime recommendation systems come as a solution to help users find relevant and interesting new anime based on their preferences. By analyzing users' preferences, the recommendation system can provide recommendations that are personalized and suited to individual interests, thus improving users' experience in finding anime they like.


# Business Understanding
At this stage, we define the problems to be solved and the goals to be achieved through the development of an anime recommendation system.

## Problem Statements:
- How can we help users discover new anime that match their interests, thereby increasing user satisfaction and exploration of new content?
- Are there ways to overcome users' difficulties in selecting and finding anime relevant to their preferences, thereby increasing user engagement and interaction with the platform?
- How can we improve the user experience of watching anime by providing more personalized and relevant recommendations, thereby enriching the content that users watch and creating a stronger connection with the platform?

## Goals:
- Develop an anime recommendation system that can provide accurate and relevant recommendations to users.
- Help users find anime that matches their interests and preferences more efficiently and quickly.
- Improve user experience in exploring the world of anime by providing diverse and interesting recommendations.
  

## Solution Statements:
To achieve this goal, the proposed solution is to implement a content-based recommendation system. The system will analyze information about anime, such as synopsis and genre, to identify similarities between existing anime and user preferences. By using a content-based filtering algorithm, the system will provide suitable anime recommendations based on the content similarity with the user's previous preferred anime. This will help users find new anime that match their interests.

# Data Understanding
The dataset used comes from the [Kaggle](https://www.kaggle.com/datasets/marlesson/myanimelist-dataset-animes-profiles-reviews) website which contains information about anime, user profiles, and user reviews. In this project, the dataset used is only information about the anime.

## Overview Dataset:
This dataset "animes.csv" contains information about anime, including title, synopsis, genre, number, episodes, popularity, rating, score, and more.

### Karakteristik Data:

- The dataset has 19311 rows, 12 columns
- In the dataset columns consist of:
  - 'uid' (Unique ID for each anime),
  - 'title' (Title of the anime),
  - 'synopsis' (Synopsis or story of the anime),
  - 'genre' (Genre or category of the anime),
  - 'aired' (Anime airing period),
  - 'episodes' (Number of anime episodes),
  - 'members' (Number of members or users who added the anime to their favorites list),
  - 'popularity' (The popularity of the anime on the MyAnimeList platform),
  - 'ranked' (The rank of the anime on the MyAnimeList platform),
  - 'score' (The average score or rating of an anime based on user reviews),
  - 'img_url' (URL of the image/anime poster),
  - 'link' (URL to the anime page on MyAnimeList platform).

# Data Preparation
## Teknik Data Preparation:
1. Missing Value Handling:
- For the synopsis column, if there is a missing value, the value is filled with an empty string (" ").
- For the genre column, there are no missing values based on the information provided, so no special handling is required.

2. Synopsis and Genre Text Representation:

To convert synopsis and genre text into vector representation, the following steps can be taken:

- Synopsis:
  - Using Rake-NLTK library for keyword extraction from synopsis text.
  - Each synopsis is converted into a list of generated keywords.
- Genre:
  - Removing the characters "[", "]", "'", and "," from genre values using the replace method.
  - Each genre is converted into a string without the removed characters.

3. Merging Genres and Keywords:
- The genre and keyword columns (extracted from the synopsis) are merged into one new column, the "kata-kata" column.
- The merging is done by combining the genre and keyword values using the "+" operator, so that each entry in the "words" column contains a combined representation of the genre and keyword.

4. Vector Representation with CountVectorizer:
- Using CountVectorizer from the scikit-learn library to convert the text in the "kata-kata" column into a vector representation.
- CountVectorizer counts the frequency of words in each document and generates a vector matrix with appropriate dimensions.

# Modeling

This project uses the Content-based Filtering method

- Using the content-based filtering method to build a recommendation system.
- Apply CountVectorizer to convert synopsis, genre, and keyword text into feature vectors.
- Using cosine similarity to calculate the similarity between anime based on feature vectors.

TF-IDF (Term Frequency-Inverse Document Frequency) is a method used to calculate the weight of words in a document. It assigns higher values to words that appear more frequently in the document, but rarely appear in other documents in the dataset. CountVectorizer, on the other hand, only calculates the frequency of occurrence of a word in a document without assigning a weight based on the importance of the word in the dataset.

Calculate TF-IDF or Count Vectorizer:

    Anime A has a feature vector of [0.2, 0.5, 0.1, 0.3, 0.0], while Anime B has a feature vector of [0.1, 0.3, 0.6, 0.2, 0.4].

Calculate Dot Product:

    The dot product between Anime A and Anime B can be calculated as follows:
    Dot Product = (0.2 * 0.1) + (0.5 * 0.3) + (0.1 * 0.6) + (0.3 * 0.2) + (0.0 * 0.4) = 0.04 + 0.15 + 0.06 + 0.06 + 0.0 = 0.31. 

Calculate Norm:

    The norm or length of the Anime A vector can be calculated as the square root of the sum of the squares of each element of the vector:
    Norm of Anime A = sqrt((0.2 * 0.2) + (0.5 * 0.5) + (0.1 * 0.1) + (0.3 * 0.3) + (0.0 * 0.0)) = sqrt(0.04 + 0.25 + 0.01 + 0.09 + 0.0) = sqrt(0.39) = 0.624.

    The norm or vector length of Anime B can be calculated in the same way:
    Norm of Anime B = sqrt((0.1 * 0.1) + (0.3 * 0.3) + (0.6 * 0.6) + (0.2 * 0.2) + (0.4 * 0.4)) = sqrt(0.01 + 0.09 + 0.36 + 0.04 + 0.16) = sqrt(0.66) = 0.812.

Cosine similarity is used to measure the similarity between two vectors in a multi-dimensional space, such as feature vectors representing anime. This method measures the cosine angle between two vectors, where a value of 1 indicates perfect similarity, a value of 0 indicates complete discrepancy, and a negative value indicates the opposite direction.

Calculate Cosine Similarity:

    Cosine similarity between Anime A and Anime B can be calculated as follows:
    Cosine Similarity = Dot Product / (Anime A Norm * Anime B Norm) = 0.31 / (0.624 * 0.812) = 0.31 / 0.506 = 0.612.

## Result
### Attempt 1
Input:

- Search Type: Judul
- Search Query: _Sword Art Online_
- Number of Recommendations: 5

Output:
1. sword art online: alicization - war of underworld
2. sword art online movie: ordinal scale
3. sword art online fatal bullet: the third episode
4. sword art online fatal bullet: the third episode - pilot-ban
5. sword art online: alicization - war of underworld

### Attempt 2
Input:

- Search Type: Kata Kunci
- Search Query: _kawaii_
- Number of Recommendations: 5

Output:
1. shownoid mako-chan
2. kakko kawaii sengen! 2
3. nexus
4. reunion (music)
5. ao no exorcist movie special

### Attempt 3
Input:

- Search Type: Genre/Kategori
- Search Query: _Romance_
- Number of Recommendations: 5

Output:
1. shigatsu wa kimi no uso
2. clannad: after story
3. nodame cantabile: finale - mine to kiyora no saikai
4. inuyasha movie 3: tenka hadou no ken
5. gekkan shoujo nozaki-kun specials


# Evaluation
The evaluations used in recommendation systems such as Recommender Precision System are Precision and Recall.

1. Precision:
- Precision measures the proportion of relevant items that the recommender system considers relevant out of all items that the system considers relevant. 
- Precision formula: precision = (number of relevant items deemed relevant)/(number of items deemed relevant by the system).
- Interpretation of results:
  - Precision has a value range between 0 to 1.
  - A high precision indicates that the system tends to provide relevant recommendations and minimize irrelevant recommendations.
  - Low precision indicates that the system tends to provide many irrelevant recommendations.


2. Recall:
- Recall measures the proportion of relevant items that the recommendation system considers relevant out of all items that are actually relevant.
- Recall formula: recall = (number of relevant items deemed relevant) / (number of actually relevant items).
- Interpretation of results:
  - Recall also has a value range between 0 to 1.
  - A high recall indicates that the system was able to identify most of the relevant items.
  - A low recall indicates that the system failed to identify many relevant items.

For example, if the evaluation results show a precision of 0.8 and a recall of 0.6, it can be interpreted that:

- Among all the recommendations provided by the system, 80% were relevant to the user's preferences (precision).
- The system was able to identify 60% of all items that were actually relevant (recall).

From the results obtained that the precision and recall values given are 0, it shows that the recommendation system has not provided recommendations that are relevant to user preferences or has not been able to identify items that are actually relevant.

# Conclusion
- Our recommendation model uses cosine similarity calculation to measure the similarity between anime based on feature vectors. The system provides top-N recommendations based on the similarity.
- However, the evaluation results obtained show that the performance is still low, with precision and recall values still 0. This indicates that the recommendation model developed has not provided sufficient relevant recommendations.

Therefore, although this project provides an initial understanding of the development of an anime recommendation system, there is room for further improvement and development to achieve the previously set goals.

# References
- https://medium.com/data-folks-indonesia/recommendation-system-dengan-python-definisi-part-1-71154dc3f700
- https://medium.com/@m_n_malaeb/recall-and-precision-at-k-for-recommender-systems-618483226c54
- Shani, G., Gunawardana, A., & Meek, C. (2015). Evaluating Recommendation Systems. In Recommender Systems Handbook (pp. 257-297). Springer.
- Pandas Development Team. (2021). pandas: Powerful data structures for data analysis and manipulation. Zenodo.

