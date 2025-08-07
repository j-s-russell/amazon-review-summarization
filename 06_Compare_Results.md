# Comparative Analysis

This section will compare the generated summaries from our traditional extractive models (KL-Sum and LexRank) with our fine-tuned deep learning abstractive models (BART and T5). We will compare ROUGE scores, BERTScores, and inspect the generated summaries for clarity and usefulness.

## ROUGE Results

Let's first look at how our summaries compare in terms of word overlap. Our extractive models should perform well when the gold summaries contain many phrases taken from the source text, since extractive methods retrieve sentences verbatim. In contrast, our abstractive models should perform well when the gold summaries contain more paraphrasing.

**Verdicts:**

|Model|rouge1|rouge2|rougeL|
|---|---|---|---|
|BART|0\.2235|0\.0424|0\.1654|
|KL-Sum|0\.1404|0\.0102|0\.0917|
|LexRank|0\.1576|0\.0136|0\.1134|
|T5|0\.2166|0\.0393|0\.1688|

**Pros:**

|Model|rouge1|rouge2|rougeL|
|---|---|---|---|
|BART|0\.0122|0\.0001|0\.0122|
|KL-Sum|0\.007|0\.0|0\.007|
|LexRank|0\.0143|0\.0|0\.0142|
|T5|0\.0161|0\.0001|0\.016|

**Cons:**

|Model|rouge1|rouge2|rougeL|
|---|---|---|---|
|BART|0\.012|0\.0001|0\.012|
|KL-Sum|0\.0076|0\.0|0\.0076|
|LexRank|0\.0083|0\.0|0\.0083|
|T5|0\.0168|0\.0|0\.0168|

For the overall verdicts, our abstractive models significantly outperformed our extractive models across all ROUGE scores. This is likely due to more abstractive gold summaries in which the human writers used more unique phrasing and did not copy reviews directly. 

Since pros and cons summarization is not as straighforward a task as generating an overall verdict, all four models struggled to generate consistent summaries. On average, the abstractive models also achieved better performance on pros and cons summaries, with LexRank also achieving comparable performance. It's important to note that this review dataset only includes products with a significant number of reviews (at least 100) and have generally high ratings, so cons were sparser than pros and thus harder to summarize.

---

## BERTScore Results

Next, we'll analyze our BERTScore results and see how our generated summaries compare in terms of semantic similarity. While the raw scores are less interpretable, they can help us understand performance between models regardless of phrasing.

**Verdicts:**

|Model|precision|recall|f1|
|---|---|---|---|
|BART|0\.8764|0\.8764|0\.8763|
|KL-Sum|0\.8258|0\.8595|0\.8423|
|LexRank|0\.8612|0\.8594|0\.8602|
|T5|0\.8818|0\.8725|0\.877|


**Pros:**

|Model|precision|recall|f1|
|---|---|---|---|
|BART|0\.5994|0\.7785|0\.6772|
|KL-Sum|0\.5786|0\.7773|0\.6633|
|LexRank|0\.6063|0\.7809|0\.6824|
|T5|0\.6097|0\.7769|0\.683|


**Cons:**

|Model|precision|recall|f1|
|---|---|---|---|
|BART|0\.5992|0\.803|0\.6862|
|KL-Sum|0\.5725|0\.7849|0\.6619|
|LexRank|0\.578|0\.7853|0\.6657|
|T5|0\.6122|0\.8024|0\.6944|

We see patterns similar to the ROUGE results in these BERTScore tables - abstractive models tend to outperform across all summary types, particularly with verdicts. Performance drops significantly for pros and cons. T5 achieves the best overall performance, especially in terms of precision. One point to note is the difference between precision and recall for pros and cons, where recall is consistently much higher across all models. This demonstrates that the generated summaries cover most of the underlying meaning in the gold summaries, but include details that aren't mentioned in the gold summaries, which suggests are summaries are too long. This may not be an issue as this additional information may be useful, although extractive models may pick irrelevant sentences and abstractive deep learning models may hallucinate.

---

## Generated Summaries

To better understand our results, let's take a look at the gold summary and our generated summaries for a sample product. While ROUGE and BERTScore capture important information regarding the accuracy of the generated summary, they do not everything that is necessary for a quality summary.

::::{admonition} Gold Summary
**Verdict:**  
Nylabone’s best offering for large breeds is this sturdy and bulky nylon
barbell, and its longevity is well worth the price.

**Pros:**  
Extra thick and sturdy nylon barbell shape, Fried chicken flavor dogs love,
Covered in teeth-cleaning nubs, Hefty weight, Available in large and giant
sizes, this toy is for tough chewers

**Cons:**  
Best for dogs over 50 pounds, It’ll hurt if you step on it by accident

::::

::::{admonition} Kl-Sum
**Verdict:**  
This particular toy has been in his possession for over a month and is still not
falling to pieces, and it is still one of his favorites. The only thing that I
do not like about it is that it is so heavy that I am scared to toss it anywhere
in my house because it is heavy enough to leave marks or dents on the
baseboards.

**Pros:**  
I'm always looking for new chew toys for my 100 pound Pitt Bull, and this seemed
like it was worth a try. In any case, it is the first toy that has outlasted my
dog's interest and that is an accomplishment. I recently purchased another
monster size Nylabone and was so pleased with it that I wanted to get this one
too.

**Cons:**  
I purchased several Nylabones- this one in Medium, a synthetic cow hoof, a
synthetic antler, a chicken flavored dental bone and on a whim, a Philly
Cheesesteak flavored bone. She has had this for a couple of months now and has
hardly done any damage to it! My pup, who usually destroys everything we give to
her, is still trying to make a dent in this one.

::::

These summaries are somewhat informative, although the pros and cons are less detailed. The generated cons represent a key issue with the sentiment-based extractive summarization method, which is some sentences can be misclassified, resulting in a positive review in the generated cons.

::::{admonition} LexRank
**Verdict:**  
My dogs are able to chew through just about everything. Would definitely
recommend to anyone who has a dog that loves to chew!

**Pros:**  
Nylabone is a great product, loved by all 3 dogs and long lasting. This is
advertised as: "Long-lasting chew toy in delicious peanut butter flavor
challenges even the most aggressive chewers and discourages destructive chewing.
My guy chews through virtually any toy I give him quickly, and his love for
chewing is limited to toys, so I'm happy to keep him supplied.

**Cons:**  
She has had this for a couple of months now and has hardly done any damage to
it! I have a 50 lb lab and she loves to chew on hard toys. Not a good feeling.

::::

LexRank's summaries are relatively clear and informative, highlighting the durability of the product. However, it runs into the same problem as KL-Sum where the phrase "hardly done any damage to it" is classified as negative, when in fact it's positive. Additionally, it includes sentences like "not a good feeling", which does not provide any useful information.

::::{admonition} BART
**Verdict:**  
A good choice for power-chewer dogs who are looking for a chew toy that will
keep them busy and prevent them from eating their food.

**Pros:**  
Durable, durable nylon bone that's easy to chew, Available in three flavors,
including peanut butter, which is ideal for dogs with a love of peanut butter
and peanut butter-flavored food, Can be used by dogs with an aggressive chewer,
Can also be used as a chew toy

**Cons:**  
The toy is heavy, making it difficult for some dogs to chew through it in a
hurry

::::

BART's summary is a bit more informative, highlighting the variety of flavors in addition to the durability. However, it struggles with repetition and does not generate constructive cons.

::::{admonition} T5
**Verdict:**  
This toy is a great choice for dogs who prefer to chew on a soft bone that isn't
too hard.

**Pros:**  
The Nylabone is a durable, durable nylon bone that's hard and durable, It's a
great choice if you're a serious power chewer

**Cons:**  
if your dog is a power chewer, this toy is not for her

::::

T5 also struggles with repetition. The pros and cons also include a direct contradiction, showing the model is unsure that a dog being a "power chewer" is ideal for this product.

This is just one example, but it highlights some difficulties in review summarization. One area all models struggled with was generating cons, which likely means that there were few negative reviews. Additionally, abstractive models struggled with repetition and some incoherent language. More data and further training may be necessary to correct these issues.

