# Website Content Analyzer

A Tkinter-based desktop application that allows users to analyze website content by generating questions and finding relevant links using OpenAI's API.

## Features

- Scrapes content from a given website URL.
- Generates concise questions based on the website's content.
- Identifies and lists relevant links from the website.
- Provides a simple GUI for easy interaction.

## Prerequisites

- Python 3.x
- OpenAI API Key

## Installation

1. **Clone the Repository**

   ```bash
   git clone https://github.com/yourusername/website-content-analyzer.git
   cd website-content-analyzer
   ```

2. **Install Required Packages**

   Create a virtual environment (optional but recommended) and install the required packages using `pip`. You can install dependencies from `requirements.txt`.

   ```bash
   pip install -r requirements.txt
   ```

   If you don't have `requirements.txt`, manually install the packages using:

   ```bash
   pip install requests beautifulsoup4 openai
   ```

## Usage

1. **Run the Application**

   Execute the Python script to start the Tkinter GUI application.

   ```bash
   python app.py
   ```

2. **Enter OpenAI API Key**

   - Open the application.
   - Enter your OpenAI API key in the "OpenAI API Key" field.

3. **Enter Website URL**

   - Enter the URL of the website you want to analyze in the "Website URL" field.

4. **Process the Website**

   - Click the "Process" button to start analyzing the website. 
   - The application will scrape the website, generate questions, and find relevant links. 
   - A message will be displayed indicating the progress and completion of the process.

5. **View Results**

   - Results will be displayed in the scrollable text area at the bottom of the window.

## Code Overview

- **scrape_website(url)**: Scrapes the provided URL to gather all hyperlinks and their content.
- **generate_questions(content, num_questions=10)**: Generates concise questions based on the provided content using OpenAI's GPT-3.5-turbo model.
- **get_relevant_links(main_link, all_links, main_content, num_links=5)**: Finds relevant links based on the content of the main link.
- **process_website()**: Handles the main processing logic, including setting the API key, scraping the website, generating questions, and displaying results.

## GUI Components

- **API Key Entry Field**: For inputting the OpenAI API key.
- **URL Entry Field**: For inputting the website URL to be analyzed.
- **Process Button**: Starts the processing of the website.
- **Result Text Area**: Displays the results in a scrollable text box.
- **Wait Message Label**: Shows a message indicating the process duration.

## Contributing

1. **Fork the Repository**

   Click the "Fork" button at the top right of this repository's page.

2. **Clone Your Fork**

   ```bash
   git clone https://github.com/yourusername/website-content-analyzer.git
   ```

3. **Create a Branch**

   ```bash
   git checkout -b feature/your-feature-name
   ```

4. **Make Changes**

   Modify the code as needed and test your changes.

5. **Commit Your Changes**

   ```bash
   git add .
   git commit -m "Add your message here"
   ```

6. **Push to Your Fork**

   ```bash
   git push origin feature/your-feature-name
   ```

7. **Create a Pull Request**

   Go to the original repository and click "New Pull Request" to submit your changes.


## Contact

For any questions or issues, please open an issue in the GitHub repository or contact pradeepkr848115@gmail.com.
