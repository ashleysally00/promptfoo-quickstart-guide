# PromptFoo Quickstart: Funny Tweet Evaluator

This repo shows how to use PromptFoo to evaluate and compare responses from different LLMs using prompt variations and automated scoring.This version is designed for local use in **VS Code** or another terminal-based environment.

👉 Want to run this in Google Colab? Check out the [Colab Quickstart Guide](https://github.com/ashleysally00/promptfoo-quickstart-guide/blob/main/run_in_colab.md) 


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

<p align="center">
  <img src="images/promptfoo_2.png" width="750" alt="PromptFoo terminal output 2">
</p>

---

<p align="center">
  <img src="images/promptfoo_2.png" width="750" alt="PromptFoo terminal output 2">
</p>



### Web UI Output

To see your results displayed like this, click the local URL printed in your terminal after running `promptfoo eval --ui`.

<p align="center">
  <img src="images/results_displayed_in_broswer.png" width="750" alt="PromptFoo browser UI">
</p>


# Summary of Evaluation

## Models Tested
- `openai:gpt-4o`
- `openai:gpt-4o-mini`

## Prompt Templates
- `"Write a tweet about {{topic}}"`
- `"Write a concise, funny tweet about {{topic}}"`

## Test Topics
- `bananas`
- `avocado toast`
- `new york city`

## Assertions
- One used `icontains` (e.g., must include "avocado")
- One used `javascript` scoring (favor shorter tweets)
- One used `llm-rubric` to judge funniness

**Total Test Combinations:** 12 (2 models × 2 prompts × 3 topics)

## 📊 Results Breakdown

| Topic | GPT-4o | GPT-4o-mini | Outcome |
|-------|--------|-------------|---------|
| **Bananas** | ✅ PASS for both prompts and both models (4 passes) — both models generated accurate, friendly, and funny tweets. |
| **Avocado Toast** | ✅ PASS for all — models met the requirements (included the word "avocado", were short/funny). |
| **New York City** | ❌ FAIL on both models for the **non-funny** version of the prompt — failed the **llm-rubric** check. The funny versions **passed**. |

**Total: 10 PASSES, 2 FAILS → 83.33% Pass Rate**

## Where It Failed

- **Failures occurred with the prompt:** `"Write a tweet about New York City"` (non-funny version)
- **Reason for failure:** The generated tweets were **descriptive or sentimental** but not **funny**, which violated your LLM rubric assertion: "Ensure that the output is funny"
- **This shows:** The models do fine with direct or joke-style prompts, but when not nudged toward humor, they miss the "funny" requirement even when it's implied by the test.

## Takeaways

- The **funniness rubric** works well — it accurately flagged serious outputs as failures.
- **Prompt wording matters**: adding "funny" helps steer models toward the correct tone.
- **Both models perform similarly**, though GPT-4o responses are slightly more detailed.
- This simple setup is effective so far for testing tone/creativity, not just factual correctness.

  ## 💡 Running in Google Colab Instead

If you want to use PromptFoo without installing anything locally — for example, if you're:

- on a Chromebook or restricted work machine  
- sharing results with teammates or collaborators  
- running quick tests without setting up Node.js or the CLI  

Then try running this project in [Google Colab using this quickstart guide](https://github.com/ashleysally00/promptfoo-quickstart-guide/blob/main/run_in_colab.md).

It supports the same evaluations and browser UI — right from your browser.

👉 [Open the Colab Quickstart Guide ›](https://github.com/ashleysally00/promptfoo-quickstart-guide/blob/main/run_in_colab.md)

## Resources

- [Official PromptFoo Docs](https://promptfoo.dev/docs)
- [PromptFoo GitHub Repository](https://github.com/promptfoo/promptfoo)






