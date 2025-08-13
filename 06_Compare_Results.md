# Comparative Analysis

This section will compare the generated summaries from our traditional extractive models (KL-Sum and LexRank) with our fine-tuned deep learning abstractive models (BART and T5). We will compare ROUGE scores, BERTScores, and inspect the generated summaries for clarity and usefulness.

## ROUGE Results

Let's first look at how our summaries compare in terms of word overlap. Our extractive models should perform well when the gold summaries contain many phrases taken from the source text, since extractive methods retrieve sentences verbatim. In contrast, our abstractive models should perform well when the gold summaries contain more paraphrasing.

**Verdicts:**

|Model|rouge1|rouge2|rougeL|
|---|---|---|---|
|BART|**0\.2146**|**0\.0410**|0\.1619|
|KL-Sum|0\.1404|0\.0102|0\.0917|
|LexRank|0\.1576|0\.0136|0\.1134|
|T5|0\.2086|0\.0346|**0\.1625**|

**Pros:**

|Model|rouge1|rouge2|rougeL|
|---|---|---|---|
|BART|0\.0145|**0\.0001**|0\.0144|
|KL-Sum|0\.0070|0\.0000|0\.0070|
|LexRank|0\.0143|0\.0000|0\.0142|
|T5|**0\.0184**|**0\.0001**|**0\.0182**|

**Cons:**

|Model|rouge1|rouge2|rougeL|
|---|---|---|---|
|BART|0\.0182|**0\.0001**|0\.0182|
|KL-Sum|0\.0076|0\.0000|0\.0076|
|LexRank|0\.0083|0\.0000|0\.0083|
|T5|**0\.0185**|0\.0000|**0\.0185**|

For the overall verdicts, our abstractive models significantly outperformed our extractive models across all ROUGE scores. This is likely due to more abstractive gold summaries in which the human writers used more unique phrasing and did not copy reviews directly. 

Since pros and cons summarization is not as straighforward a task as generating an overall verdict, all four models struggled to generate consistent summaries. On average, the abstractive models also achieved better performance on pros and cons summaries, with LexRank also achieving comparable performance. It's important to note that this review dataset only includes products with a significant number of reviews (at least 100) and have generally high ratings, so cons were sparser than pros and thus harder to summarize.

---

## BERTScore Results

Next, we'll analyze our BERTScore results and see how our generated summaries compare in terms of semantic similarity. While the raw scores are less interpretable, they can help us understand performance between models regardless of phrasing.

**Verdicts:**

|Model|precision|recall|f1|
|---|---|---|---|
|BART|0\.8805|**0\.8739**|**0\.8771**|
|KL-Sum|0\.8258|0\.8595|0\.8423|
|LexRank|0\.8612|0\.8594|0\.8602|
|T5|**0\.8809**|0\.8708|0\.8757|


**Pros:**

|Model|precision|recall|f1|
|---|---|---|---|
|BART|0\.5979|0\.7786|0\.6763|
|KL-Sum|0\.5786|0\.7773|0\.6633|
|LexRank|0\.6063|**0\.7809**|0\.6824|
|T5|**0\.6067**|0\.7802|**0\.6825**|


**Cons:**

|Model|precision|recall|f1|
|---|---|---|---|
|BART|0\.6073|0\.8027|0\.6913|
|KL-Sum|0\.5725|0\.7849|0\.6619|
|LexRank|0\.578|0\.7853|0\.6657|
|T5|**0\.6125**|**0\.8033**|**0\.6949**|

We see patterns similar to the ROUGE results in these BERTScore tables - abstractive models tend to outperform across all summary types, particularly with verdicts. Performance drops significantly for pros and cons. T5 achieves the best overall performance, especially in terms of precision. One point to note is the difference between precision and recall for pros and cons, where recall is consistently much higher across all models. This demonstrates that the generated summaries cover most of the underlying meaning in the gold summaries, but include details that aren't mentioned in the gold summaries, which suggests are summaries are too long. This may not be an issue as this additional information may be useful, although extractive models may pick irrelevant sentences and abstractive deep learning models may hallucinate.

---

## Generated Summaries

To better understand our results, let's take a look at the gold summary and our generated summaries for a sample product. While ROUGE and BERTScore capture important information regarding the accuracy of the generated summary, they do not everything that is necessary for a quality summary.

The following summaries were generated for a chew toy for dogs (Nylabone Barbell Power Chew Durable Dog Toy).

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
A tough, durable nylon bone that will keep your dog busy for a long period of
time.

**Pros:**  
Durable nylon material keeps dogs from chewing away at the bone, It's a good
size for power chewers, and it's easy to carry around

**Cons:**  
A few dogs have been known to chew through this toy within a few hours

::::

BART's summaries are concise and informative, highlighting its ideal size and portability in addition to durability. BART manages to generate a sensible cons summary, although it contradicts the durability claims in the verdict and pros summary. This highlights a major challenge in review summarization - reviews can contain conflicting information based on their particular experience. 

::::{admonition} T5
**Verdict:**  
This toy is a great option for those who want a durable bone for their dog's
teeth.

**Pros:**  
The nylon bone is hard, durable and odor-free, It isn't a power chewer but it
keeps them busy.

**Cons:**  
It is not a chewing toy for dogs, but if your dog is an aggressive chewer, this
may be the one for you

::::

T5 generates mostly sensible summaries, but struggles with some incoherent language. Like the extractive models, T5 struggles with generating cons, incorrectly stating "it is not a chewing toy for dogs". 

This is just one example, but it highlights some difficulties in review summarization. Product reviews contain much more noise than typical text input for these models, making it difficult to concisely and accurately summarize all reviews. One area most models struggled with was generating cons, likely due to a lack of negative reviews. Additionally, abstractive models struggled with repetition and some incoherent language. More data and further training may be necessary to correct these issues.

