# Evaluation Methods

Our goal is to generate summaries that are as similar to the gold summaries as possible. To evaluate this similarity, we will be using two metrics: ROUGE and BERTScore.

## ROUGE

[ROUGE](https://aclanthology.org/W04-1013/ )(Recall-Oriented Understudy for Gisting Evaluation) is a set of metrics for evaluating text generation by measuring overlaps of n-grams (continuous sequences of $n$ words), word sequences, and word pairs between the generated and reference texts. Higher ROUGE scores indicate greater similarity and are commonly used to assess the quality of extractive and abstractive summaries.

- **ROUGE-1:** Measures the overlap of unigrams (each word) between generated text and reference text
- **ROUGE-2:** Measures the overlap of bigrams (each sequential pair of words) between generated text and reference text
- **ROUGE-L:** Measures the similarity based on the longest common subsequence of words

#### Formulas:

````{tab-set}
```{tab-item} ROUGE-1
Let:
- $X$: generated summary
- $Y$: gold summary
- $Count_{match}$: number of overlapping unigrams between $X$ and $Y$
- $Count_{gen}$: total number of unigrams in $X$
- $Count_{gold}$: total number of unigrams in $Y$

$$
\text{Recall }(R_1) = \frac{Count_{match}}{Count_{gold}}
$$
$$
\text{Precision }(P_1) = \frac{Count_{match}}{Count_{gen}}
$$
$$
\text{F1-score } (F_1) = \frac{2 \times P_1 \times R_1}{P_1 + R_1}
$$



```
```{tab-item} ROUGE-2
Let:
- $X$: generated summary
- $Y$: gold summary
- $Count_{match}$: number of overlapping bigrams between $X$ and $Y$
- $Count_{gen}$: total number of bigrams in $X$
- $Count_{gold}$: total number of bigrams in $Y$

$$
\text{Recall }(R_2) = \frac{Count_{match}}{Count_{gold}}
$$
$$
\text{Precision }(P_2) = \frac{Count_{match}}{Count_{gen}}
$$
$$
\text{F1-score } (F_2) = \frac{2 \times P_2 \times R_2}{P_2 + R_2}
$$
```

```{tab-item} ROUGE-L
Let:
- $X$: generated summary
- $Y$: gold summary
- $LCS(X,Y)$: length of the longest common subsequence between $X$ and $Y$
- $m$: length of generated summary $X$
- $n$: length of gold summary $Y$

$$
\text{Recall }(R_{LCS}) = \frac{LCS(X,Y)}{n}
$$
$$
\text{Precision }(P_{LCS}) = \frac{LCS(X,Y)}{m}
$$
$$
\text{F1-score } (F_{LCS}) = \frac{(1+\beta^2) \times R_{LCS} \times P_{LCS}}{R_{LCS} + \beta^2 \times P_{LCS}}
$$
```
````

## BERTScore

[BERTScore](https://arxiv.org/abs/1904.09675) is a way to measure how similar two pieces of text are by comparing semantic meaning. Instead of matching words exactly, it looks at how words are used in context and evaluates whether the ideas in both texts align. This makes BERTScore especially helpful when the wording is different but the message is still the same.

BERTScore is based on a language model called [BERT](https://arxiv.org/abs/1810.04805) (Bidirectional Encoder Representations from Transformers), which has been trained to understand the contextual meaning of words in a piece of text. The contextual meanings between generated summaries and gold summaries, which are represented by embedding vectors, are compared using cosine similarity to determine precision, recall, and F1-scores.

(more explanation here?)


```{tip}
  - Describe and explain the evaluation metrics you chose for this problem
  - Why did you choose these particular metrics over others
  - Run the evaluation metics on some dummy data to help readers understand what does a good and bad metric looks like
  - Call-out limitations of the evaluation metrics --> ie. scenario in which it might not work well
  - [optional] The evaluation methods can also be moved to a `utils.py` file so that they can be imported easily later
```
