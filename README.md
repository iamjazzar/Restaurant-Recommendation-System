# Restaurant Recommendation System

## Problem Description
Recommendation System which returns top 3 recommendations which provide business Id based on ratings and review text.

## Approach
The architecture of the Feature Extraction model for System

![The architecture](https://raw.githubusercontent.com/ahmedaljazzar/Restaurant-Recommendation-System/blob/master/architecture.png)

### Matrix Factorization

I followed traditional approach matrix factorization or latent factor collaborative filtering. Initially constructed rating matrix 𝑀 ∈ R$×& where index contains user id, columns contains business id and values filled with ratings. I factorize the matrix 𝑀 into two matrices 𝑃 ∈ R$×( and 𝑄 ∈ R(×& and solved the following optimization problem

$*& ∑ (𝑀 − (𝑃𝑄) )6 + 𝜆(‖𝑃‖6 + ‖𝑄‖6) ................. equation 1 +∈R,×-,∈R-×/ (*,3)∈: *,3 *,3

To extract the features from the text for a specific user, first pool all the reviews together form a single paragraph. I applied TFIDF vectorizer from sci-kit learn package to extract the features from the text. I followed the same approach for each business id (each restaurant). After all, we got the feature vectors P for user Id and Q for business Id.

Applied equation 1, to minimize the objective function (via stochastic gradient descent) I executed for 100 iterations and it took around 12 hours of time as the dimensions of the dataset is pretty huge. I stored the feature vectors and vectorizer in pickle file so that I can re-utilize the P and Q for prediction.

### Prediction
Simply the inner product of the feature vector of plain text and feature vectors of business Id. Out of all, top N records to be fetched. I achieved an accuracy of 68.4% on the validation set

### Deployment
I Developed basic webpage using Python, Flask, and Restful API.

## Execution Instructions

### Type 1 
To access the web application, you may open your local server link to test the recommendation engine. This web link contains text box and submit button.

### Type 2 
As I used REST API, you may execute below command predict the top 3 recommendation restaurants

```bash
curl http://localhost:8000 -d "Input Text=I am interested in non-vegetarian"
```

### Type 3
Simple Program execution
- Unzip the quest_global zip file
- Download the pickle file from below location and store in classification folder. Please let me know if you don’t have access.
https://drive.google.com/file/d/1gmauZBet-Rma-PGQ_5okyvmk_601W662/view?usp=sharing
- Install requirements.txt file from recommendation folder using 
```
Pip3 install -r requirements.txt
```
- Run below command to execute the python file
```bash
Python3 recommendation.py
```
