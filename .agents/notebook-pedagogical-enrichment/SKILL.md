---
name: notebook-pedagogical-enrichment
description: |
  Enrich Jupyter notebooks with pedagogical markdown explanations for students.
  Trigger when the user asks to explain, document, add markdown, or format a Jupyter notebook (.ipynb) to make it suitable for students or educational purposes.
---

# Notebook Pedagogical Enrichment

A skill to transform technical Jupyter notebooks into structured, narrative-driven educational resources designed for students.

## When to Use
Trigger this skill whenever the user asks to:
- Explain the code blocks in a Jupyter notebook (`.ipynb`).
- Add Markdown formatted notes or explanations for students.
- Document step-by-step procedures in a notebook.
- Compare different Machine Learning algorithms (e.g., OLS vs Ridge vs Lasso) inside a notebook for teaching.

## Step-by-Step Workflow

### Step 1: Inspect Notebook Cells
Use a Python script to read the target `.ipynb` file and print a summary of all cells, their types, and the first lines of their source code. Do not read the entire file as a raw text view if it is very large (due to HTML outputs).
Example inspection snippet:
```python
import json
with open("notebook.ipynb", "r") as f:
    nb = json.load(f)
for i, cell in enumerate(nb["cells"]):
    source = "".join(cell.get("source", []))
    print(f"Cell {i:02d} ({cell['cell_type']}): {source[:80]}...")
```
Or use the local helper script:
```bash
python3 .agents/notebook-pedagogical-enrichment/scripts/notebook_helper.py inspect <path_to_notebook.ipynb>
```

### Step 2: Compute Exact Metrics (Dry Run)
Before writing explanations, run the notebook's code (using the workspace virtual environment, e.g., `.venv/bin/python3`) to obtain the exact training/testing scores (like MSE, $R^2$, accuracy, etc.).
Reporting exact numbers (e.g., *“the test $R^2$ is 0.217 for OLS but 0.994 for Lasso”*) makes the explanations extremely authentic and helpful.

### Step 3: Write Rich Markdown Explanations
Explanations must follow best practices in technical writing and pedagogy:
- **Use Clear Formatting**: Use bold text, bullet points, and code blocks.
- **Explain the "Why"**: Don't just say *what* the code does; explain *why* we do it (e.g., why we scale features, why a random seed is set, why data leakage is bad).
- **Use Math Formulas**: Use LaTeX syntax (e.g., `$$\text{Loss} = \text{MSE} + \alpha \sum_{j=1}^{p} w_j^2$$`) to describe the loss functions and penalties.
- **Explain Model Performance Contrast**:
  - **OLS**: Explain overfitting (memorization of training data, poor generalization).
  - **Ridge (L2)**: Explain weight shrinkage without zeroing, and why it might not be enough when there are many non-informative features.
  - **Lasso (L1)**: Explain feature selection (zeroing out uninformative weights) and why it works so well for noisy data.
- **Learning Curves**: Explain how to diagnose bias/variance by looking at the gap and convergence of training and validation scores.

### Step 4: Update the Notebook Programmatically
Always edit Jupyter notebooks by loading the JSON in Python, manipulating the `cells` list, and saving the JSON back. This preserves metadata, notebook formatting, and prevents syntax issues.

Use the following stateful matching script structure:
```python
import json

def make_markdown_cell(text):
    lines = [line + "\n" for line in text.split("\n")]
    if lines and lines[-1] == "\n":
        lines.pop()
    elif lines:
        lines[-1] = lines[-1].rstrip("\n")
    return {"cell_type": "markdown", "metadata": {}, "source": lines}

# Load, reconstruct nb["cells"] by matching cell signatures, and write back.
```

### Step 5: Validation
Verify that the output notebook is valid JSON and loads properly:
```bash
python3 -c 'import json; json.load(open("notebook.ipynb"))'
```
