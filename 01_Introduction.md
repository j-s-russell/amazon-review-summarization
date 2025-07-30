
# Introduction

---

## Automated Review Summarization

In this project, we'll explore models that summarize product reviews. If you've ever used a website to make an online purchase, book a hotel, or make a restaurant reservation, chances are you've read customer reviews. These are important to ensure you are choosing the best available option and to know what to expect when you receive it. However, this can be a challenging and tedious process as many reviews are uninformative or irrelevant for your preferences. Automated review summarization aims to accurately and concisely convey the most important details of the product or service, aggregating the perspectives of many different buyers. This can also help sellers understand their product or service better and thereby improve it.

---

## Machine Learning Concepts

We will be using two main types of algorithms for summarization: extractive (selects and ranks sentences directly from the original text) and abstractive (generates new sentences that capture the meaning of the original text).

````{grid} 1 2 2 2
:gutter: 2

```{grid-item-card} Extractive Methods
:class-header: bg-primary text-white
- **KL-Sum:** Selects sentences minimizing the KL divergence between the summary and the word distribution of all reviews.
- **LexRank:** Graph-based algorithm that ranks sentences by their centrality using cosine similarity and PageRank-like algorithms
```

```{grid-item-card} Abstractive Methods
:class-header: bg-secondary text-white
- **BART:** A transformer-based summarization model trained to reconstruct original text from a corrupted version, helping it learn how to generate fluent and coherent summaries even when the wording or structure changes.
- **T5:** Transformer model that treats summarization as a text generation problem, using task-specific prompts like "summarize:" to guide output.
```
````

---

## Dataset

We will be using the AmaSum dataset, introduced by Brazinskas et al. ([2021](https://arxiv.org/abs/2109.04325)). This contains user reviews for over 31,000 products, as well as professional human-written summaries. These summaries include a brief verdict, a list of pros, and a list of cons. Due to the large amount of text in this dataset and the size of the models we plan to use, we will use a subset of roughly 2,000 products.

---

## Project Roadmap

- **Exploratory Data Analysis:** Analyze the reviews and summaries in our dataset
- **Data Preprocessing:** Remove unnecessary columns and apply review selection
- **Define Evaluation Metrics:** Describe and demonstrate ROUGE and BERTScore
- **Test Extractive Models:** Apply KL-Sum and LexRank algorithms for summarization
- **Test Abstractive Models:** Apply transformer-based BART and T5 models for summarization
- **Compare Results:** Analyze how the four models performed according to our two metrics
- **Conclusion:** Wrap up by discussing the current state of review summarization, this project's limitations, and possible areas for improvement
