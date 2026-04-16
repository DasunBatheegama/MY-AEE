# Week 01 Prompt Engineering Essentials

## 1) Week Goal
This week builds a practical prompt engineering foundation with reusable templates, model routing, token awareness, and notebook based experiments.

## 2) What You Completed
1. Created a central prompt template catalog in utils/prompts.py.
2. Practiced zero shot prompting.
3. Practiced few shot prompting with example blocks.
4. Practiced chain of thought and tree of thought reasoning patterns.
5. Practiced structured output design with JSON schema.
6. Set up a unified LLM client that supports OpenAI, Google, and Groq.
7. Added token estimation and context management helpers.
8. Added call logging to logs/runs.csv.
9. Added model and behavior configuration files in config.

## 3) Project Layout
1. notebooks contains all Week 01 exercises.
2. utils contains reusable Python helpers.
3. config contains runtime settings and model mapping.
4. data contains tiny practice corpus files.
5. logs stores LLM run history.

## 4) Environment Setup
1. Open terminal in the Week 01 folder.
2. Sync dependencies.

```powershell
uv sync
```

3. Activate the virtual environment.

```powershell
.\.venv\Scripts\Activate.ps1
```

4. Create environment file from sample.

```powershell
cp .env.sample .env
```

5. Add your API keys inside .env.

```env
OPENAI_API_KEY=your_openai_key
GEMINI_API_KEY=your_gemini_key
GROQ_API_KEY=your_groq_key
```

## 5) How To Run Week 01
1. Start Jupyter.

```powershell
jupyter notebook
```

2. Open notebooks in this order.
3. Run cells from top to bottom inside each notebook.

```text
notebooks/00_setup.ipynb
notebooks/01_decoding_and_tokens.ipynb
notebooks/02_prompt_structure_patterns.ipynb
notebooks/03_zero_few_cot_tot.ipynb
notebooks/04_structured_outputs_json_schema.ipynb
notebooks/prompt_techniques.ipynb
```

## 6) Key Prompt Templates Used
1. zero_shot.v1
2. few_shot.v1
3. cot_reasoning.v1
4. tot_reasoning.v1
5. json_extract.v1

Prompt ids must match exactly.
Extra spaces cause prompt lookup errors.

## 7) Common Issues And Fixes
1. NameError render is not defined.
   Run the first import cell before running later cells.
2. KeyError Prompt not found.
   Ensure prompt id is exact, for example use cot_reasoning.v1 and not cot_reasoning .v1.
3. API key errors for OpenAI, Gemini, or Groq.
   Confirm keys are set in .env and the notebook kernel was restarted after update.

## 8) Outputs To Check
1. Notebook outputs for each technique.
2. logs/runs.csv for latency, tokens, retries, and metadata.
3. Prompt behavior differences across model tiers from config/models.yaml.

## 9) Quick Validation Run
Use this simple flow in a notebook cell.

```python
from utils.prompts import render
from utils.router import pick_model
from utils.llm_client import LLMClient

prompt_text, spec = render(
    "zero_shot.v1",
    role="assistant",
    instruction="Summarize this text in one sentence",
    constraints="Use plain language",
    format="One sentence"
)

model = pick_model("google", "general")
llm = LLMClient("google", model)

messages = [{"role": "user", "content": f"{prompt_text}\n\nPrompt engineering is practical and iterative."}]
response = llm.chat(messages, temperature=0.2)
print(response["text"])
```

## 10) Week 01 Outcome
You now have a reusable prompt engineering starter system with provider flexibility, template discipline, and notebook based experimentation ready for Week 02 expansion.
