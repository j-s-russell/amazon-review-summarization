# Traditional Methods

---

## Extractive Models

```{figure} images/extractive.png
:alt: Extractive Summarization
:width: 500px
:align: left
:figclass: my-image

*Image courtesy of [medium.com](https://andongluis.github.io/nlg-blog/Summarization-post/)*
```

Extractive summarization models aim to create summaries by identifying and selecting the most important sentences or phrases directly from the original text. Instead of generating new sentences (as we'll see with our deep learning models), these models work by ranking and extracting existing content based on features like sentence relevance, position, or similarity to the overall document. The result is a condensed version of the original text that preserves its wording and structure, making extractive methods simpler and more interpretable than abstractive approaches. These models are especially useful when factual accuracy and similarity to the original writing style are priorities.

---

### KL-Sum

The [KL-Sum](https://iq.opengenus.org/k-l-sum-algorithm-for-text-summarization/#google_vignette) algorithm creates summaries by selecting sentences that minimize the [Kullback-Leibler (KL) divergence](https://aiml.com/what-is-kl-divergence/) between the word distribution of the summary and that of the original document. KL divergence measures how one probability distribution differs from another, which can be applied in our case to ensure that the word frequency distribution of our generated summary closely matches that of all reviews for that product. Once the KL divergences have been computed, KL-Sum greedily adds the closest matching sentence until a fixed number of sentences has been reached. 

We will use KL-Sum because it focuses on preserving the original review content distribution and captures the overall themes and key points of reviews. It tends to exclude overly emotional or repetitive sentences, which are common in product reviews, and accurately finds information-rich sentences.

---

### LexRank

[LexRank](https://www.cs.cmu.edu/afs/cs/project/jair/pub/volume22/erkan04a-html/erkan04a.html) is a graph-based algorithm that selects sentences based on how "central" they are to the rest of the text. It treats each sentence as a node in a graph, where edges represent similarity (typically cosine similarity based on TF-IDF vectors) between sentences. LexRank then uses a variant of the [PageRank](https://web.stanford.edu/class/cs54n/handouts/24-GooglePageRankAlgorithm.pdf) algorithm (the original Google Search algorithm) to compute the importance of each sentence. Like KL-Sum, a fixed number of the most important sentences are selected for the summary.

We will use LexRank because it excels at identifying central and consensus-based sentences in a document. Given that product reviews often repeat similar opinions in different ways, LexRank picks the most representative points, making it effective for capturing common sentinements and key features across reviews.

---

```{seealso}
There are several other widely used extractive summarization methods. Here are a few suggestions:
- [TextRank](https://aclanthology.org/W04-3252/)
- [Maximum Marginal Relevance (MMR)](https://www.cs.cmu.edu/~jgc/publication/The_Use_MMR_Diversity_Based_LTMIR_1998.pdf)
- [Latent Semantic Analysis (LSA)](https://arxiv.org/abs/2207.14687)
```


