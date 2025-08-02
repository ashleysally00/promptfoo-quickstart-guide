# Using an External prompts.txt File with PromptFoo

The main [Quickstart Guide (README)](./README.md) shows how to run PromptFoo using prompts written directly inside the `promptfooconfig.yaml` file. That's great for quick tests or small projects.

But if you have **lots of prompts**, or want to **easily swap them in and out**, it's better to store them in a separate file like `prompts.txt`.

This guide shows how to do that.

---

## 🧾 Why Use an External prompts.txt File?

- Keeps your config file clean  
- Easier to manage many prompts without editing YAML  
- You can reuse or substitute different prompt files for different evaluations

---

## 📁 Folder Structure

```
your-project/
├── promptfooconfig.yaml
├── prompts.txt
├── .env
└── with_prompts.txt_file.md
```

---

## 📄 prompts.txt

Each line is one complete prompt. Example:

```
I have a dentist appointment at 3pm, and I need to pick up my kid by 5. Is there time to go to the gym before that?
Can I fit in a workout between my 2pm meeting and a 4pm call if I need 15 minutes travel time?
What should I do first: finish my report due at 6pm or go to the grocery store? It's 4:15 now.
```

---

## ⚙️ promptfooconfig.yaml

When you run `promptfoo init`, PromptFoo creates a default `promptfooconfig.yaml` with prompts defined inline, like this:

```yaml
prompts:
  - "Write a tweet about {{topic}}"
```

To use an external file instead:

1. Delete the `prompts:` block
2. Replace it with this line:

```yaml
promptsFile: prompts.txt
```

Then your full config will look like this:

```yaml
promptsFile: prompts.txt

providers:
  - id: openai:gpt-4o
    config:
      model: gpt-4o
      apiKeyEnvVar: OPENAI_API_KEY

tests:
  - vars: {}

assertions:
  - type: icontains
    value: "because"
  - type: llm-rubric
    value: "Does the response show correct time reasoning and give a helpful plan?"
```

---

## 🔄 Swapping Prompt Files

You can temporarily test a different prompt file by changing:

```yaml
promptsFile: prompts_alt.txt
```

This allows you to maintain different prompt sets for different projects or evaluation goals.

---

## 🚀 How to Run

Make sure your `.env` file includes your OpenAI API key:

```ini
OPENAI_API_KEY=sk-...your-key-here...
```

Then run the evaluation in your terminal:

```bash
promptfoo eval
```

To view the results in your browser:

```bash
promptfoo eval --ui
```

---

## ✅ Use Case: Time Reasoning

This example tests the model's ability to reason through real-world scheduling constraints — a realistic scenario for personal assistants, planners, or productivity tools.

