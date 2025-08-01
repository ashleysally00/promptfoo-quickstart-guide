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






