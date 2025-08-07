# Setup Instructions

```{tip}
The instruction below cover the specific libraries necessary for this project.
```

---

### Pre-requisities

- Python 3.8 (or higher)
- Git


### Clone Repository

`git clone https://github.com/ritika-aiml/112-review-summarization-and-extraction.git`
`cd 112-review-summarization-and-extraction`

### Setup Environment

**Create virtual environment:**
`python -m venv review_summarization_env`

**Activate virtual environment:**

On Windows:
`review_summarization_env\Scripts\activate`

On macOS/Linux:
`source review_summarization_env/bin/activate`

### Install Required Dependencies

```python
# Data manipulation and scientific computing
pip install pandas numpy scikit-learn

# Text processing and NLP
pip install textblob nltk

# Evaluation metrics
pip install rouge-score bert-score evaluate

# Extractive summarization
pip install lexrank

# Transformers and deep learning
pip install torch torchvision transformers

# Jupyter environment
pip install jupyterlab jupyter

# Utilities
pip install textwrap3
```

### Launch Jupyter Lab

Once everything is installed, start Jupyter Lab:

```python
jupyter lab
```




