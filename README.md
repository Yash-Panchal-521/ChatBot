# NLP Chatbot

This code implements a chatbot using Natural Language Processing (NLP) techniques. The chatbot is designed to answer questions based on a given dataset.

## Requirements
- numpy
- pandas
- nltk
- sentence_transformers
- transformers

You can install the required libraries using the following command:
```
pip install numpy pandas nltk sentence_transformers transformers
```

## Code Explanation

The code can be divided into two main parts: preprocessing and the chatbot class.

### Preprocessing
1. The code imports the necessary libraries: `numpy`, `pandas`, `nltk`, `sentence_transformers`, `util` from `sentence_transformers`, `pipeline` from `transformers`, `string`, and `re`.
2. It initializes a SentenceTransformer model (`all-MiniLM-L6-v2`) for encoding sentences into fixed-dimensional vectors and a summarization pipeline for generating summaries.
3. The `chatbot` class is defined, and its constructor initializes the class variables.
4. The constructor reads an Excel file (`Data.xlsx`) containing the dataset into a pandas DataFrame (`self.doc`).
5. The text in the dataset is preprocessed using the following steps:
   - Lowercasing: Converts all text to lowercase.
   - Stopword removal: Removes common English stopwords from the text.
   - Lemmatization: Reduces words to their base form using stemming.
   - Sentence tokenization: Splits the text into individual sentences.
   - Punctuation removal: Removes punctuation marks from the sentences.
6. The preprocessed data is stored in a new column (`pre_processed`) in the DataFrame.
7. The text in the `pre_processed` column is encoded using the SentenceTransformer model, and the embeddings are stored in another column (`embedding`) in the DataFrame.

### Chatbot Class
1. The `QA` method is defined to handle user questions and provide answers.
2. It takes a `flag` parameter that determines whether the chatbot should continue running or exit.
3. The method prompts the user to enter a question and preprocesses the question using the same steps as in the preprocessing phase.
4. The question is encoded using the SentenceTransformer model.
5. The cosine similarity between the question embedding and each document embedding is calculated to find the most similar document.
6. The DataFrame is sorted based on the similarity scores.
7. The text of the most similar document is selected as the context for summarization.
8. The summarization pipeline generates a summary for the context.
9. The summary is printed as the answer to the user's question.
10. If the user's question is one of the predefined exit phrases (e.g., "goodbye", "bye"), the method returns `True` to exit the chatbot.
11. Otherwise, it returns `False` to continue running.

### Running the Chatbot
1. An instance of the `chatbot` class is created (`bot = chatbot()`).
2. A while loop is used to continuously prompt the user for questions and provide answers until an exit phrase is entered.
3. The `QA` method is called within the loop, passing the `flag` variable to control the loop.
