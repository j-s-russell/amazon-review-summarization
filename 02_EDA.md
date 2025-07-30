# Data Description

---

## Background

This dataset was created in a paper by Brazinskas et al. ([2021](https://arxiv.org/abs/2109.04325)), which aimed to use human-generated summaries to train a language model to effectively summarize product reviews. These summaries come from four professional product review platforms:

- bestreviews.com (BR)
- cnet.com
- pmag.co.uk (PM)
- runrepeat.com (RR)

These sources mostly focus on electronic consumer products, while RR focuses on sports shoes. The professional reviewers utilize several sources of information such as public customer reviews, online research, and testing products themselves. Their summaries focus on clear writing that allow potential buyers to make informed purchases. Each summary includes a 1-2 sentence verdict, a list of pros, and a list of cons. A sample product and summary are shown below.

```{figure} images/example_product.jpg
:alt: Example Product
:width: 300px
:align: left
:figclass: my-image

*Image: Hoover Vacuum Cleaner from Amazon.com*
```
**Verdict:** "Despite some quality concerns, this canister model offers some of Hoover's best features for a price that's significantly lower than similar models by some competing brands."

**Pros:** 
- Features the brand's WindTunnel technology in a bagless model with a dirt cup that is easy to empty and clean
- Has washable and reusable filter
- Steers easily around objects
- Cord recoils back into the unit for easy storage

**Cons:**
- Suction power tends to diminish over time
- Has been known to overheat
- Vacuum head and tubing are prone to clogging with debris

---

## Dataset Features

The full dataset includes 31,483 products and summaries, with an average of 326 reviews per product. We will be using a subset of this dataset with 5000 products, with a maximum of 100 reviews per product. While the dataset includes product metadata such as ratings and review authors, we will focus purely on the reviews and summaries. The full dataset is  available on [this GitHub repository](https://github.com/abrazinskas/SelSum/tree/master/data) for the original paper.

---

## Review Selection

The following notebook will preprocess the dataset so that it includes only the necessary text for our summarization models. In addition to removing unused columns, we will be applying various review selection methods to limit the number of reviews per product to 15 due to computational restraints. We will utilize the following three methods:

````{grid} 1 2 2 3
:gutter: 3

```{grid-item-card} Random
:class-header: bg-primary text-white
- Randomly select 15 reviews per product
- Easiest and fastest method
```

```{grid-item-card} Clustering
:class-header: bg-secondary text-white
- Use [K-Means clustering](https://www.geeksforgeeks.org/machine-learning/k-means-clustering-introduction/) to create 15 distinct review clusters, then select the centermost review from each one.
- Effective at creating diverse review sets
- Reviews may not always be informative
```

```{grid-item-card} Similarity Regression
:class-header: bg-secondary text-white
- Define a similarity metric between reviews and gold summaries, then train a regression model to predict similarity and select reviews with the highest similarity scores
- Effective at selecting informative reviews
- Limited diversity in review selections
```
````

We will create columns for all three of these review subsets in the following notebook.




```{tip}
 - Describe the dataset and why you chose it
 - Explain from where the dataset was procured (ie. the methodology used to get the data)
 - Discuss Columns and number of instances
 - Anything else that you would like readers to know about this data
```

