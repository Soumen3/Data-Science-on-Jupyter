# Review Data Cleaning
### Python Code
```python
import pandas as pd
from textblob import TextBlob
import string

dataset = pd.read_excel('user_review.xls')

# Deleting null value if available
dataset.dropna(inplace=True)

# Perform basic text preprocessing (e.g., lowercasing, removing punctuation).
def preprocess_review(review):
    # Convert review to lowercase
    review = review.lower()
    
    # Remove punctuation marks
    review = review.translate(str.maketrans('', '', string.punctuation))
    return review
    
dataset['review'] = dataset['review'].apply(preprocess_review)

# Generating sentiment of the review using TextBlob
def create_sentiment(review):
	blob = TextBlob(review)
	if blob.sentiment.polarity > 0:
		return 'Positive'
	elif blob.sentiment.polarity < 0:
		return 'Negative'
	else:
		return 'Neutral'
		
dataset['sentiments'] = dataset['review'].apply(create_sentiment)

```

### Approach
 1. I've used the ```pandas``` library to read the data and to create data frame. 
 2. Using ```dropna()``` method the null values are deleted (if available)
 3. The texts are converted to lowercase and then removed the punctuations. 
 4. Then using the ```textblob``` library the sentiment of the review is created and stored it in another column name sentiments.

### Challenges

 -  At the time of creating sentiments of the review.
	 1. I Google about how to create sentiment of texts.
	 2. I found the ```textblob``` library.
	 3. I learned how to create sentiment using the library.


