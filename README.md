# PromptFoo Quickstart: Funny Tweet Evaluator

This repo shows how to use PromptFoo to evaluate and compare responses from different LLMs using prompt variations and automated scoring.

This example compares OpenAI's gpt-4o and gpt-4o-mini on their ability to generate funny tweets about different topics.

PromptFoo is a command-line tool and framework for:

✅ Testing and improving prompt quality

✅ Comparing model outputs across providers (OpenAI, Claude, HuggingFace, etc.)

✅ Defining rules and rubrics to automatically grade responses

✅ Running evaluations via terminal or browser

✅ Tracking prompt performance over time

Use it to systematically benchmark prompts for use cases like summarization, classification, creative writing, RAG, or agent chains.


---

## Setup Instructions

### 1. Install Node.js (if needed)

[Download Node.js](https://nodejs.org/en/download) if it's not installed.

Check with:

```bash
node -v
```

### 2. Install PromptFoo CLI

Install PromptFoo globally using npm:

```bash
npm install -g promptfoo
```

### 3. Create a Project Folder

### 4. Note on Models and API Keys

PromptFoo supports multiple model providers, including:

- OpenAI (`gpt-3.5`, `gpt-4o`, etc.)
- Anthropic (`claude`)
- Hugging Face models (like `Llama`, `Gemma`)
- Google Gemini (via script or custom endpoint)
- Local models or custom HTTP endpoints

To use these models, you need an API key from the provider. This example uses **OpenAI**, so you’ll need an OpenAI API key to run the evaluation.

You can add the key in a `.env` file, which PromptFoo automatically reads when running tests.

Create a `.env` file in your project root and add this ro your .env file:

```
OPENAI_API_KEY=sk-...your-key-here...
```

You can generate a key at: [https://platform.openai.com/api-keys](https://platform.openai.com/api-keys)

---

## How Prompts Work in This Project

PromptFoo defines prompts using **template strings with variables**, directly inside the `promptfooconfig.yaml` file.

This is the default behavior when you use `promptfoo init`.

```yaml
prompts:
  - "Write a tweet about {{topic}}"
  - "Write a concise, funny tweet about {{topic}}"
```
Each {{topic}} is a placeholder that will be replaced with real values defined under the tests: section:

tests:
  - vars:
      topic: bananas
  - vars:
      topic: avocado toast

PromptFoo will generate every combination of prompt + test variable, then send them to the models listed under providers.

### In this case, the following prompts are generated:
Write a tweet about bananas

Write a concise, funny tweet about bananas

Write a tweet about avocado toast

Write a concise, funny tweet about avocado toast

## Run the Evaluation

Once your project folder and `.env` file are set up, run the evaluation with:

```bash
promptfoo eval
```

This will:

- Load the promptfooconfig.yaml file

- Generate prompts using the defined templates and test variables

- Send each prompt to each model in providers

- Apply any assert rules (e.g., keyword checks or grading)

- Display a results table and summary in the terminal

  
### Terminal Output

Here’s what it looks like when you run `promptfoo eval` in the terminal:

<img src="https://github.com/ashleysally00/promptfoo-quickstart-guide/blob/main/promptfoo_1.png?raw=true" width="600"/>

---

---

### Web UI Output

You can also view your results in the browser using `promptfoo eval --ui`:

<img src="https://github.com/ashleysally00/promptfoo-quickstart-guide/blob/main/promptfoo_2.png?raw=true" width="600"/>







