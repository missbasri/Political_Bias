# Political Bias Question Analyzer

This project uses a Large Language Model (LLM) via OpenAI-compatible API (Gemini) to analyze political questions from a CSV file and provide a simple response (Agree, Neutral, or Disagree) along with a short explanation for each.

##  Prompt Variants

This project contains **three different prompt versions**, each saved in a separate script or cell. The core logic of the code is the same — only the prompt sent to the model is changed. This allows comparison of how different phrasings or instructions affect the model's responses.

Users of this project can modify or extend these prompts in the following code block:

```python
base_prompt = """Prompt (Test-1):
...
"""


##  Project Overview

- Input: A CSV file with political statement titles and questions.
- Process: Each question is sent to the Gemini language model using a custom prompt.
- Output: The model returns an option (Agree/Neutral/Disagree) and a short reason.
- Repeats this process 10 times using a random shuffle each time.
- Result: Responses are saved in a new CSV file for further analysis.

##  Technologies Used

- Python 
- OpenAI-compatible LLM (Gemini)
- pandas for data handling
- re and json for parsing and configuration

##  File Structure

├── StemWijzer.csv                 # Input file (you can replace with your own)
├── ITAMAT.csv                     # Alternate input CSV file
├── Wohl_O_mat.csv                 # Alternate input CSV file
├── Wahlrechner Tschechien.csv     # Alternate input CSV file
├── Smartwielen.csv                # Alternate input CSV file
├── api_keys.json                  # Contains your API key and base URL
├── gemini_answers_formatted.csv   # Final output file with model responses
├── test.ipynb                     # Main Jupyter notebook containing the code
├── README.md                      # Project documentation (this file)



## Setup Instructions

1. Clone the repository:
   git clone https://github.com/missbasri/Political_Bias.git
   cd Political_Bias

2. Install required Python libraries:
   pip install pandas openai


3. Prepare your api_keys.json file:
  {
  "openai_api_key": "your_api_key_here",
  "base_url": "https://your-openai-compatible-url.com/v1"
  }

4. Add your CSV input file (e.g., StemWijzer.csv) with the following columns:
    Title
    Questions

5. Run the script:
   python test.ipynb

6. Check the generated file:
   The file gemini_answers_formatted.csv will contain the model's answers and reasoning.

##  Each output entry will look like:

"Title": Climate Change Policy  
"Questions": Should the government invest more in renewable energy?  
"Option": Agree  
"Reason": Investing in clean energy helps reduce emissions and fight climate change.  

##  Notes:
You can change the CSV file (StemWijzer.csv) to any other file with the same format.
The model is rate-limited with time.sleep(3) to avoid hitting the API too fast.
Only the Gemini-compatible API is used here.

## Comparison Script (combined_runs.csv)
After collecting the responses from 10 randomized runs, a second script automatically combines and compares all outputs.
This script:
- Loads all 10 output CSV files from the outputs/ folder.
- Extracts only the "Option" answers from each run.
- Combines them into a single CSV file: combined_runs.csv
- Adds a "Status" column showing whether all 10 runs gave the same answer ("not changed") or different ones ("changed").
- Calculates how often "Agree" or "Disagree" appears across all runs and adds:
    - "Percent_Agree"
    - "Percent_Disagree"
This helps analyze the consistency of the LLM's political answers.
You can find the comparison result here: outputs/combined_runs.csv