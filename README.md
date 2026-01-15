# Code Explainer Bot

## Overview
This project implements a simple Python-based LLM bot that takes a Python error or code snippet as input and generates a plain-language explanation for different audience levels (beginner, intermediate, developer). It uses Google Gemini LLM models via the `genai` client.

## 1️⃣ Notebook with Working Code

The notebook `code-explainer-bot.ipynb` was set up for this project. It contains different sections:

| Section                        | Description                                                                                                             |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| **Imports**            | Import libraries |
| **Setup**              | Load API key from `.env`. & initialize client |
| **Audience Mapping**   | Map audience options to enable easy entry through numbers |
| **Core Functions**     | Define LLM call function `explain_error()` with audience argument and code leak detection; handles retry on code leak (hard-coded to 5 retries) / model selection can be adapted here |
| **Interactive Bot**    | Single-run loop where a user pastes a traceback/error and selects audience level; runs once unless user opts to continue; includes escape (`Q` / `quit`) |
| **Test Scenarios**     | Hard-coded examples with audience pre-defined to test bot; can be run independently |
| **Reflection / Notes** | My thoughts, learnings, challenges, model choices, etc. |

## 2️⃣ Access & Run the Bot
Open the notebook in VS Code and run all cells sequentially; they must be run once before interactive bot or test cases

### Usage
* Paste a Python error or code snippet into the input prompt (or use the hard-coded test cases)
* Select audience level (1=beginner, 2=intermediate, 3=developer)
* The bot will provide an explanation without giving working code
* Use `Q` or `quit` to exit the interactive loop

### Test Cases
These can be run independently after the core functions are loaded; audiences are pre-defined for these
* NameError (beginner)
* TypeError (beginner)
* IndexError (intermediate)
* ModuleNotFoundError (intermediate)
* ZeroDivisionError (developer)

### Notes
* Code leak detection is implemented to ensure the bot does not output executable code
* Interactive mode allows single-run input per loop iteration

## 3️⃣ Short Reflection Report
### Challenges
- Adjusting input format from separate code/error to a singled pasted block required updating prompt handling
- Preventing model from returning code (*code leak detection* + retry loop)
- Ensuring single-run interactive mode with optional continuation
- Managing audience selection dynamically for each test case
### Key Learnings
- LLM prompts can be adapted to control explanation style without changing model
- Designing safe interaction patterns (no code execution, retry on code leaks) is important
- Notebooks require careful state management: all functions must be defined before running test scenarios
- Mapping audience levels to numbers simplifies user input and reduces errors
- Hard-coded test cases provide reproducible evaluation
### Possible Future Extensions
- Add output text wrapping for better user experience
- Build fully interactive chatbot UI (like Streamlit) for error explanations
- Add a logging system for repeated errors and explanations
- Allow dynamic switching between models if one model is exhausted or unavailable