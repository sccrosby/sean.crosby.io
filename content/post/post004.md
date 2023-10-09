---
title:       "Do dog owners prefer dogs of the same gender?"
subtitle:    "A quick EDA of popular dog colors, breeds, and preferences with a dataset of dogs and their owners from Switzerland."
description: ""
date:        2021-11-01
author:      "Sean C. Crosby"
image:       ""
tags:        ["Data Science"]
categories:  []
draft:       true
---

### The dogs of Zurich

I stumbled on this [dataset](https://www.kaggle.com/kmader/dogs-of-zurich) on Kaggle of dogs and their owners in Switzerland. With a little help from google translation it becomes clear that there is a relatively substantial dataset of around 6,000 dogs and their owners including dog gender, dog breed, owner gender, owner age, and a few other bits of information. To practice working with pandas data frames and some simple regressions I entertained a few questions, such as, what is the most popular dog color?

### Popular colors, breeds

I would have guessed (hypothesized) brown, but the ranking shows that black (schwarz in German) is the most popular accounting for about 12% of dogs followed closely by tri-color, white and brown (8-10% each). This is accomplished easily with a groupby and count of items within each color group (Hundefarbe is color)
```python
breed = df1.groupby("HUNDEFARBE").count()
```
Similarly the most popular breed was "mixed small breed" followed up by the chihuahua and Labrador retriever. I would never have guessed chihuahua was so popular!

### Dog owners

I was also curious about the owners themselves, and while we don't know a lot, we do know there age. But first I needed to determine which records were of duplicate owners for multiple dogs. I created a unique list of owner IDs and added up the number of dogs each owner has. More on that later. But examining the distribution of owners ages look very plausible, with dog ownership appearing to peak from 41-60. However, we must take care here as we do not have the underlying age distribution of the population. This result is solely the number of dog owners in each age range.

![owner age distribution](/img/dog_owner_age_distr.png)

Within this set of dog owners, however, we can ask if there are differences across owner gender. The first thing of note is that the dataset contains about twice as many female dog owners. Again, we do not know what the underlying distribution of female and males in the region, but we may suspect that dog ownership is more common for women. But what about when each gender tends to own dogs? Do women or men tend to have dogs earlier in life? The data suggest there is little difference overall, however women may tend to own dogs earlier (20's) with peak ownership later (60's). 

![owner age distribution](/img/dog_owner_age_distr_by_gender.png)

### Dog owner preferences

While these questions have been difficult to nail down without some data on the population statistics, we can examine the question of whether owners in this dataset tend to prefer a dog of the same or opposite gender. A simple pivot of both owner and dog gender is a one-liner
```python
df1us.pivot_table('ALTER', index=['GESCHLECHT'], columns = ['GESCHLECHT_HUND'], aggfunc='count')
```
And the count shows that there may indeed be a slight preference for a same-sex dog, or in other words, men have slight preference for male dogs.

|  *Count*			| male dog 	| female dog 	|
| -------- 			| ---- 		| ----- 		|
| **male owner**	| 1029 		| 865 			|
| **female owner** 	| 1838 		| 2029 			|

We can determine if this preference is significant with a chi-2 test of the table above, often called a contingency table (scipy.stats.chi2_contingency). Here we are testing whether to reject the null hypothesis, which is that dog gender is independent of owner gender. The p-value estimate for the results above is around 1e-6, quite small, allowing us to reject the null hypothesis at an alpha much less than 0.05. So there is indeed a statistically significant preference for dogs of the same gender, and even if it is rather slight we can say that Men are about 8% more likely to own a male dog while women are about 5% more likely to own a female dog

One more potentially interesting question I had was whether women or men tended to own more dogs, assuming they own at least one to make it into this dataset. The average number of dogs owned by men was 1.08 while the average number dogs owned by women was 1.12. Whether this difference is significant I am unsure, but it may point to women tending to own more dogs that men. 

### Caveats

At this point it is pertinent to bring up a major issue with this dataset and the conclusions based on gender. The dog owners here may be co-owners within a family or other partnership and such preferences above may simply be related to tendencies for one gender to be more likely to register the dog. Clearly more data is needed to really make these kinds of conclusions!


For further details and references see my [python notebook](https://github.com/sccrosby/python_data_explorations/blob/main/eda_003_swissdogs_regressions.ipynb)