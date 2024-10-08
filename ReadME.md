# Website Content Analyzer: GEN AI PS

This Python script performs web scraping, generates questions based on the scraped content using OpenAI's GPT-3.5 model, finds relevant links, and evaluates the generated questions and relevance detection.

Alert: This Program will take 2-5 minutes. Keep Patience ! HAppy Coding !

## Features

1. **Web Scraping:** Extracts content from all accessible pages linked from a specified URL.
2. **Question Generation:** Uses OpenAI's GPT-3.5 model to generate concise questions based on the scraped content.
3. **Relevant Links Extraction:** Identifies links that are most relevant to the main page content.
4. **Evaluation:** Provides a basic evaluation of the generated questions and relevance detection.

## Requirements

- Python 3.x
- Libraries: `requests`, `beautifulsoup4`, `openai`, `scikit-learn`

Install the required libraries using pip:

```bash
pip install requests beautifulsoup4 openai scikit-learn
```

## Setup

1. **OpenAI API Key:** You'll need an API key from OpenAI. You can obtain it by signing up on [OpenAI's website](https://www.openai.com/).

2. **Configuration:**
   - Replace the API key in the script by entering it when prompted.

## Code Explanation

### Imports

```python
import requests
from bs4 import BeautifulSoup
import openai
import json
from sklearn.metrics import precision_score, recall_score, f1_score
```

- **`requests`**: For making HTTP requests.
- **`BeautifulSoup`**: For parsing HTML content.
- **`openai`**: For interacting with OpenAI's API.
- **`json`**: For handling JSON data.
- **`precision_score`, `recall_score`, `f1_score`**: For evaluating performance metrics.

### Function Definitions

#### `scrape_website(url)`

Scrapes all accessible pages linked from the given URL.

- **Parameters:**
  - `url`: The starting URL for scraping.
- **Returns:**
  - `content`: A dictionary where keys are URLs and values are the text content of those pages.

#### `generate_questions(content, num_questions=10)`

Generates up to 10 concise questions based on the provided content using GPT-3.5.

- **Parameters:**
  - `content`: The text content to generate questions from.
  - `num_questions`: Number of questions to generate.
- **Returns:**
  - A list of questions, each under 80 characters.

#### `get_relevant_links(main_link, all_links, main_content, num_links=5)`

Finds the most relevant links based on the content of the main page.

- **Parameters:**
  - `main_link`: The URL of the main page.
  - `all_links`: Dictionary of all links and their content.
  - `main_content`: Content of the main page.
  - `num_links`: Number of relevant links to return.
- **Returns:**
  - A list of the most relevant links.

#### `evaluate_questions(generated_questions, reference_questions)`

Evaluates the quality of the generated questions. This is a simplified evaluation.

- **Parameters:**
  - `generated_questions`: List of questions generated by the model.
  - `reference_questions`: List of reference questions for evaluation.
- **Returns:**
  - A dictionary with scores for relevance, clarity, conciseness, and coverage.

#### `evaluate_relevance_detection(predicted_links, true_links)`

Evaluates the relevance detection performance.

- **Parameters:**
  - `predicted_links`: List of links identified as relevant.
  - `true_links`: List of actual relevant links.
- **Returns:**
  - A dictionary with precision, recall, and F1-score.

#### `print_output(file_path='output.json')`

Prints the content of the JSON file.

- **Parameters:**
  - `file_path`: Path to the JSON file.
  
### Main Function

```python
def main():
    website_url = input("Enter URL: ")
    scraped_content = scrape_website(website_url)

    output = {"webpages": []}

    for link, content in scraped_content.items():
        print(f"Processing: {link}")
        questions = generate_questions(content)
        relevant_links = get_relevant_links(link, scraped_content, content)
        topics = list(set(content.split()))[:5]

        webpage_info = {
            "url": link,
            "questions": questions[:10],
            "relevant_links": relevant_links[:5],
            "topics": topics
        }

        output["webpages"].append(webpage_info)

    # Save the output to a JSON file
    with open('output.json', 'w') as f:
        json.dump(output, f, indent=4)

    # Print the output
    print_output('output.json')

    # Example evaluation
    generated_questions = [q['questions'] for q in output['webpages']]
    reference_questions = ["Example reference question"]  # Replace with actual reference
    predicted_links = [link['relevant_links'] for link in output['webpages']]
    true_links = ["https://www.google.com/"]  # Replace with actual true links

    for questions in generated_questions:
        question_evaluation = evaluate_questions(questions, reference_questions)
        print("Question Evaluation:", question_evaluation)

    for links in predicted_links:
        relevance_evaluation = evaluate_relevance_detection(links, true_links)
        print("Relevance Detection Evaluation:", relevance_evaluation)
```

1. **Input URL:** Prompts the user to enter the URL of the website to scrape.
2. **Processing:** Scrapes the content, generates questions, finds relevant links, and organizes the output.
3. **Output:** Saves results to `output.json` and prints them.
4. **Evaluation:** Evaluates the generated questions and relevance detection.

## Running the Script

1. Ensure all required libraries are installed.
2. Run the script using Python:

   ```bash
   python script_name.py
   ```

3. Enter the OpenAI API key and the URL when prompted.

## Contributing

Feel free to open issues or submit pull requests for improvements or bug fixes.

---

This README provides a comprehensive overview of the functionality and usage of the script. Make sure to replace placeholder values like `"Example reference question"` and `true_links` with actual data for real evaluations.
