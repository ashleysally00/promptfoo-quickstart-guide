# Running PromptFoo in Google Colab

This guide shows how to run the PromptFoo evaluation framework inside **Google Colab**, without needing local setup.

➡️ [Skip to the Quickstart Guide](#-quickstart-in-colab)


### Why Use Colab Instead of VS Code

#### 1. No Local Setup Required
- No need to install Node.js or set up the CLI locally.
- Run everything in your browser — great for quick tests or demos.

#### 2. Device Flexibility
- Works on any device (Chromebooks, tablets, etc.) without needing dev tools.

#### 3. Easy Collaboration
- Shareable notebooks allow others to reproduce and explore results without setup.

#### 4. Track Experiments
- Use Markdown + cells to document prompt iterations and results.

#### 5. Python Compatibility
- Combine PromptFoo with Python-based scripts, charts, or model outputs.

#### 6. Ideal for Work Environments
- Many workplaces restrict local installs, but Colab runs fully in the browser.
- Avoids software approval or admin permissions needed for global CLI tool

### Limitations

- **Browser viewer** (`promptfoo view`) doesn't work because `localhost` isn't supported in Colab.
- You'll view results **in the notebook output**, not a web UI.
- You'll need to install PromptFoo and dependencies in each runtime session.

## 🚀 Quickstart in Colab

### 1. Install PromptFoo

```bash
!npm install -g promptfoo
```

### 2. Create a Config File
You can write your promptfooconfig.yaml manually, or use Python to write it:

config = '''
description: "Funny Tweet Evaluation"

prompts:
  - "Write a tweet about {{topic}}"
  - "Write a concise, funny tweet about {{topic}}"

providers:
  - "openai:gpt-4o"
  - "openai:gpt-4o-mini"

tests:
  - vars:
      topic: bananas
  - vars:
      topic: avocado toast
  - vars:
      topic: new york city
    assert:
      - type: llm-rubric
        value: ensure that the output is funny
'''

with open("promptfooconfig.yaml", "w") as f:
    f.write(config)


### 3. Set Your API Key (Securely)

The safest way to store secrets in Colab is to use an input prompt so the key is not saved in the notebook:

```python
import os
```

### Ask for your API key (won't show in notebook output)
```
os.environ["OPENAI_API_KEY"] = input("Enter your OpenAI API key: ")
```

Or, for temporary usage during a session, use Colab’s form field (click the icon in the left sidebar):

### Use the secret stored in Colab (if you've added it manually)
```
import os
os.environ["OPENAI_API_KEY"] = os.environ.get("OPENAI_API_KEY")
```

> 💡 This keeps your key out of version control and notebook history.
>
> **Important:** When you use Colab during a session (i.e., while the notebook is open and the runtime is active), any environment variables like your API key:
>
> - Will be lost when the runtime disconnects (e.g., idle timeout, page refresh, or closing the notebook).
> - Must be re-entered the next time you run the notebook.

You will have to re-enter your API key the next time you run the notebook.

### 4. Run the Evaluation
```
!promptfoo eval
```
You’ll see the pass/fail table and model outputs directly in the cell.

> 💡 **Tip**  
> In Colab, you’re running everything in-memory — so files like `promptfooconfig.yaml` only persist during that session unless you explicitly save or export them.  
>  
> Unlike VS Code, where your YAML lives in your project folder automatically, in Colab:  
> - You have to create the YAML (which you did via `with open(...)`)  
> - But unless you download it or save it to Google Drive/GitHub, it’ll be lost after the session ends.  
>  
> If you're using this for experimentation or reproducibility, consider:  
> - Saving your `promptfooconfig.yaml`  
> - Taking screenshots of evaluation results  
> - Adding markdown cells with manual notes on prompt quality or failure reasons

 ## 💻 Prefer to Run Locally in VS Code?

While Google Colab is great for quick tests and collaboration, you might want to switch to a local setup if:

- You need faster execution without Colab timeouts or usage limits  
- You're working with larger projects or lots of prompt/test combinations  
- You want full terminal access to advanced PromptFoo features  
- You're integrating with local files, scripts, or private APIs  
- You want to version control everything in one place (e.g., with Git + VS Code)

Check out the [VS Code setup guide and example project](https://github.com/ashleysally00/promptfoo-quickstart-guide#readme) to run PromptFoo locally and unlock its full capabilities.

👉 [Try the local version in VS Code ›](https://github.com/ashleysally00/promptfoo-quickstart-guide#readme)



