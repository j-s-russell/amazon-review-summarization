# Limitations

## 1. Dataset Size / Computational Constraints

BART and T5 are very large models - even pretrained models require a lot of compute and memory. We needed to reduce our dataset significantly so that we could feasibly fine-tune them with our review data. Without sufficient data and training time, models of this size can struggle to learn meaningful patterns for our task.

## 2. Pros/Cons Classification for Extractive Models

While they can generate overall verdicts effectively extractive models are not particularly well-suited for pros/cons classification. We used sentiment classification in order to create two subsets from which we created pros and cons summaries, but this is an imperfect approach, incorporating sentences that don't match the task and missing out on crucial information.

## 3. Lack of Negative Reviews

Since our dataset includes very popular products with a lot of reviews, they are generally highly-rated. Cons were much harder to generate in this case and our models sometimes resorted to generating neutral or positive information when they could not find negative reviews.