# Chatbot Application with Flask and NLTK

## Overview
This project is a simple chatbot application designed to respond to user queries based on predefined intents. The Flask framework serves the application, allowing interaction through a web interface. Natural language processing is handled using the NLTK library.

## Project Structure
```
.
├── train.py              # Training script for the chatbot model
├── train.json            # JSON file containing training data (intents, patterns, responses)
├── chat.py               # Chatbot inference script
├── app.py                # Flask web application
├── requirements.txt      # Required dependencies
├── data.pth              # Trained model weights
```

## Approach
### 1. Data Preparation
- **`train.json`** contains training data with multiple intents. Each intent includes:
  - `tag`: A unique identifier for the intent.
  - `patterns`: Example user inputs that map to the intent.
  - `responses`: Possible bot responses for the intent.

### 2. Data Preprocessing (`train.py`)
The data preprocessing phase involves several steps to prepare the textual data for model training:

- **Tokenization:**
  - Sentences from the `patterns` field are split into individual words using `nltk.word_tokenize()`.

- **Stemming:**
  - Words are reduced to their root form using the Porter Stemmer from the NLTK library to handle variations of the same word (e.g., "running" -> "run").

- **Lowercasing and Cleaning:**
  - All words are converted to lowercase to maintain consistency.
  - Punctuation and special characters like `?`, `.`, `!` are removed from the word list.

- **Creating Vocabulary:**
  - A sorted set of unique, stemmed words forms the vocabulary.

- **Bag of Words Representation:**
  - Each sentence pattern is converted into a numerical vector where each index represents a word from the vocabulary.
  - A `1` indicates the presence of a word in the sentence, and a `0` indicates its absence.

- **Label Encoding:**
  - Each intent's `tag` is assigned a numerical label for model compatibility.

### 3. Training
- Saves the trained model and associated metadata to `data.pth`.

### 4. Chatbot Inference (`chat.py`)
- Loads the trained model and word list from `data.pth`.
- Processes user input, creates a bag-of-words vector, and predicts the intent.
- Returns a random response from the matched intent.

### 5. Web Application (`app.py`)
- Flask app with two routes:
  - `/` serves the homepage.
  - `/get` returns the chatbot’s response to user input.

## Setup and Execution
### Prerequisites
Ensure you have Python 3.6.12 and the required libraries:
```bash
pip install -r requirements.txt
```

### Running the Application
1. Train the model:
```bash
python train.py
```
2. Start the Flask server:
```bash
python app.py
```
3. Access the web interface at `http://127.0.0.1:5000/`



