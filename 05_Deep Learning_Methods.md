# Deep Learning Methods

Unlike extractive summarization, abstractive summarization uses novel phrasing in its generated text. This requires a deeper understanding of language semantics and context to mimic human writers. Deep learning has revolutionalized summarization tasks by enabling models to develop a strong language understanding and sensible generation capabilities. One model in particular has fundamentally accelerated this progress - the Transformer.

---

## Transformers: The Building Blocks of Language Models

```{figure} images/transformer.png
:alt: Extractive Summarization
:width: 500px
:align: left
:figclass: my-image

*[Figure 1: The Transformer - model architecture](https://arxiv.org/pdf/1706.03762)*
```

The Transformer model, introduced by Vaswani et al. in the 2017 paper ["Attention is all you need"](https://arxiv.org/abs/1706.03762), is a deep learning architecture for natural language processing tasks. Its core innovation is the [self-attention mechanism](https://aiml.com/explain-self-attention-and-masked-self-attention-as-used-in-transformers/), which enables the model to compute dependencies between all tokens in a sequence in parallel. This allows the model to dynamically focus on the most relevant parts of the input when encoding or generating text. Thanks to its scalability, parallelism, and strong performance on sequence-to-sequence tasks, the Transformer became the foundation for many state-of-the-art models in abstractive summarization.

### **Key Features:**

````{grid} 1 2 2 3
:gutter: 3

```{grid-item-card} Self-Attention
:class-header: bg-primary text-white
- Computes how much focus each token in a sequence should place on every other token
- Captures contextual relationships dynamically (e.g., resolving pronouns or related phrases)
- Enables the model to encode dependencies regardless of their distance in the sequence
```

```{grid-item-card} Multi-Head Attention
:class-header: bg-secondary text-white
- Runs multiple self-attention operations in parallel (“heads”), each with its own set of learned weights
- Allows the model to learn different types of relationships (syntactic, semantic) simultaneously
- The outputs of all heads are concatenated and linearly transformed to enhance expressiveness
```

```{grid-item-card} Positional Encoding
:class-header: bg-success text-white
- Injects information about token positions since self-attention alone has no notion of order
- Typically uses sinusoidal functions or learned embeddings to represent position
- Ensures the model can distinguish between sequences like “the cat sat” vs. “sat the cat"

```
````

---

## Model 1: BART

BART (Bidirectional and Auto-Regressive Transformers) is a sequence-to-sequence model for natural language generation, introduced by Lewis et al. ([2020](https://arxiv.org/abs/1910.13461)). BART combines two popular and highly effective transformer-based natural language models: [BERT](https://arxiv.org/abs/1810.04805) (Bidirectional Encoder Representations from Transformers) and [GPT](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf) (Generative Pretrained Transformers). 


**BERT:**
- Introduced by Devlin et al. ([2018](https://arxiv.org/abs/1810.04805))
- Encoder-only architecture
- Processes text bidirectionally, meaning it looks at both the left and right context of each word to better understand its meaning
- Pretrained using Masked Language Modeling (random input tokens are masked so that the model is trained to predict the original token) and Next Sentence Prediction (model is trained to predict if sentence B follows sentence A)
- Very effective to understanding-based NLP tasks like classification and NER (named entity recognition)

**GPT:**
- Introduced by Radford et al. ([2018](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf))
- Decoder-only architecture
- Reads text from left to right (unidirectional)
- Trained using a causal language modeling objective, meaning it predicts the next word in a sequence using only previous words as input
- High performance on text generation tasks

**BART:**
- Combines BERT's encoder (bidirectional context understanding) and GPT's decoder (autoregressive generation)
- Pretrained using a denoising autoencoder objective, where text is corrupted and the model learns to reconstruct the original
- Highly effective for sequence-to-sequence tasks like summarization or translation

Using the pretrained encoder-decoder BART model, we will fine-tune with our customer reviews and gold summaries. BART's flexible architecture allows it to be fine-tuned with relatively modest data and compute, making it a strong baseline across a wide range of natural language processing tasks. 

---

## Model 2: T5

T5 (Text-to-Text Transfer Transformer), introduced by Raffel et al. ([2019](https://arxiv.org/abs/1910.10683)) is another sequence-to-sequence model used to natural language processing tasks. It works by representing all problems as converting an input text into an output text, such as a group of reviews into a summary or a question into an answer. While BART applies a variety of corruptions to its input that it is trained to reconstruct, T5 applies span corruption, which replaces spans of text with a single placeholder token that the model learns to fill in. T5 was pretrained on the [Colossal Clean Crawled Corpus (C4)](https://opendatalab.com/OpenDataLab/C4), a large-scale text dataset of various cleaned webpages. We will leverage T5's flexible architecture to fine-tune it for our review summarization task.

---

```{seealso}
We chose BART and T5 due to their strong baseline performance and computational feasibility. There are several other effective deep learning language models for our summarization task that were not included:
- [PEGASUS](https://research.google/blog/pegasus-a-state-of-the-art-model-for-abstractive-text-summarization/)
- [Longformer-Encoder-Decoder (LED)](https://arxiv.org/abs/2004.05150)
- [ProphetNet](https://arxiv.org/abs/2001.04063)
```