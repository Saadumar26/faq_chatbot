# FAQ Chatbot

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Saadumar26/codealpha_faq_chatbot/blob/main/FAQ_Chatbot.ipynb)
&nbsp;
![Python Version](https://img.shields.io/badge/python-3.x-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

An interactive and intelligent FAQ Chatbot designed to provide instant answers to frequently asked questions. This project leverages Natural Language Processing (NLP) techniques to understand user queries and match them with the most relevant answers from a predefined knowledge base.

The chatbot is built to run in a Jupyter Notebook, JupyterLab, or Google Colab environment, utilizing `ipywidgets` for a user-friendly and interactive chat interface.

## Features

-   **One-Click Setup:** Run the entire chatbot directly in your browser using Google Colab.
-   **Interactive UI:** A clean and simple chat interface within your notebook environment.
-   **NLP-Powered Matching:** Uses TF-IDF and Cosine Similarity to find the best answer, even if the user's phrasing doesn't exactly match the question.
-   **Text Preprocessing:** Includes a robust text preprocessing pipeline that cleans user input by lowercasing, removing special characters, tokenizing, removing stopwords, and lemmatizing.
-   **Confidence Scoring:** Displays a confidence score for each match, indicating how certain the bot is about the relevance of its answer.
-   **Easy to Customize:** The knowledge base of questions and answers can be easily updated by modifying a simple list of dictionaries in the code.
-   **Chat Management:** Users can clear the chat history with a single click to start a new conversation.

## Tech Stack

-   **Backend:** Python
-   **NLP Libraries:**
    -   `NLTK (Natural Language Toolkit)`: For text preprocessing tasks like tokenization, stopword removal, and lemmatization.
    -   `Scikit-learn`: For TF-IDF vectorization and calculating cosine similarity.
-   **Numerical Operations:** `NumPy`
-   **Interactive UI:** `IPython Widgets` for creating the chat interface in Jupyter/Colab.

## Getting Started

You can run this project in two ways:

### 1. Run with Google Colab (Recommended)

Click the "Open in Colab" badge at the top of this README to open the notebook directly in Google Colab.

### 2. Run on a Local Machine

Follow these instructions to get a copy of the project up and running on your local machine.

#### Prerequisites

-   Python 3.x
-   Jupyter Notebook or JupyterLab

#### Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/Saadumar26/codealpha_faq_chatbot.git
    cd codealpha_faq_chatbot
    ```

2.  **Install the required Python libraries:**
    ```bash
    pip install nltk numpy scikit-learn ipywidgets
    ```

3.  **Run the script in a Jupyter environment.** The first time you run the code, it will automatically download the necessary NLTK datasets:
    -   `punkt` (for tokenization)
    -   `stopwords` (for filtering common words)
    -   `wordnet` and `omw-1.4` (for lemmatization)

    If you need to download them manually, you can run this Python code:
    ```python
    import nltk
    nltk.download('punkt')
    nltk.download('stopwords')
    nltk.download('wordnet')
    nltk.download('omw-1.4')
    ```

## Usage

1.  **Customize the FAQs:**
    Open the notebook and locate the `faqs` list. You can add, remove, or modify the questions and answers to fit your specific needs.
    ```python
    # Add your FAQs here - You can modify this list with your own questions and answers
    faqs = [
        {
            "question": "What are your business hours?",
            "answer": "We are open Monday through Friday from 9 AM to 6 PM, and Saturday from 10 AM to 4 PM. We are closed on Sundays."
        },
        {
            "question": "How can I track my order?",
            "answer": "You can track your order by logging into your account and visiting the 'My Orders' section. You'll receive a tracking number via email once your order ships."
        },
        # ... add more FAQs here
    ]
    ```

2.  **Launch the Chatbot:**
    -   Open the `FAQ_Chatbot.ipynb` file in your chosen environment (Colab, Jupyter Notebook, or JupyterLab).
    -   Run all the cells. The interactive chat widget will appear at the bottom.

3.  **Interact with the Bot:**
    -   Type your question into the input field.
    -   Press `Enter` or click the `Send` button.
    -   The bot will display the best-matching answer along with a confidence score.
    -   Click the `Clear Chat` button to reset the conversation.

## How It Works

The chatbot's logic is broken down into three main classes:

1.  **`TextPreprocessor`**: This class is responsible for cleaning the text. It takes raw text (either a user's query or an FAQ question) and processes it by:
    -   Converting to lowercase.
    -   Removing punctuation and special characters.
    -   Splitting the text into individual words (tokenization).
    -   Removing common English words that don't add much meaning (stopwords).
    -   Reducing words to their base or root form (lemmatization).

2.  **`FAQMatcher`**: This is the core engine of the chatbot.
    -   It first preprocesses all the questions from the FAQ list.
    -   It then uses `TfidfVectorizer` to convert the preprocessed questions into a matrix of TF-IDF features. This technique evaluates how relevant a word is to a document in a collection of documents.
    -   When a user asks a question, it preprocesses and vectorizes the query in the same way.
    -   Finally, it calculates the **Cosine Similarity** between the user's query vector and all the FAQ question vectors. The FAQ with the highest similarity score is chosen as the best match.
    -   A threshold is used to ensure that the bot only provides an answer if it is reasonably confident in the match.

3.  **`FAQChatbot`**: This class builds and manages the user interface using `ipywidgets`. It handles user input, calls the `FAQMatcher` to find an answer, and displays the conversation history in a user-friendly format.

## Contributing

Contributions are welcome! If you have ideas for improvements or want to fix a bug, please feel free to:

1.  Fork the Project
2.  Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3.  Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4.  Push to the Branch (`git push origin feature/AmazingFeature`)
5.  Open a Pull Request

## License

This project is licensed under the MIT License - see the `LICENSE` file for details.
