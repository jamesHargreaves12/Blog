# Implications of transformer architecture
The auto regressive nature of transformer inference means that they cannot perform well when there what I am going to call "competing attention networks".

E.g. consider a point were:
- there are two possible continuations in the output.
- Which ever path is taken lowers the probability of the other path being a valid continuation.

At this point which ever path has the strongest attention is chosen. From that point the new predictions are fed back into the transformers attention network hence making it less likely that it ever goes down the second path. This means it is critical that the correct path is chosen at this point. 

This problem will be made worse by COT reasoning. Rather than the LLM having a single token to get the answer correct. It has to pick the right path at a point where it is less obvious it is making a critical descision.


## More concretely here is an example:
Input:
```
You are an expert nutritionist. Given a paper and a supplement you will tell the user if the paper is "Positive", "Negative", "Neutral" (found no positive or negative impact), "Complicated" (evidence both for and against use of the supplement), "Unmentioned" (The paper doesn't examine the supplement's impact).

Supplement: Collagen
Title: The Potential of Triterpenoids from Loquat Leaves (Eriobotrya japonica) for Prevention and Treatment of Skin Disorder.
Abstract: The leaves of loquat (<i>Eriobotrya japonica</i>) possess high medicinal value and have been used as traditional medicines. However, there are no evidence-based studies on the skin-care effects of <i>E. japonica</i> leaves. To explore new biological activities of <i>E. japonica</i> leaves against skin disorder and to gain a better understanding of the chemical components associated with bioactivities, we evaluated 18 triterpenoids from <i>E. japonica</i> leaves on anti-melanogenesis, anti-acne, anti-allergy and anti-aging activities. Our results revealed that eight compounds showed anti-melanogenesis activity, of which ursolic acid (<b>1</b>) and maslinic acid (<b>7</b>) were the most potent with the similar selective index to that of arbutin. Structure-activity relationship and possible mechanism of active compounds were proposed. Twelve compounds exhibited anti-acne effect; ursolic acid (<b>1</b>), maslinic acid (<b>7</b>), corosolic acid (<b>8</b>) and euscaphic acid (<b>12</b>) showed highest activities against <i>P. acnes</i>. Four compounds displayed anti-allergy and anti-inflammatory activity; 3-epicorosolic acid (<b>9</b>) and euscaphic acid (<b>12</b>) showed marked activity against β-hexosaminidase release. Finally, ursolic acid (<b>1</b>), pomolic acid (<b>10</b>), colosolic acid (<b>8</b>) and its methylated derivative (<b>6</b>) exhibited the highest anti-aging activity by stimulating collagen and hyaluronic acid (HA) production. Our findings provide valuable evidence that <i>E. japonica</i> leaves have potential applications as ingredients of function foods or cosmetics for health benefits and a number of triterpenoids may play an important role in these bioactivities.

Does this paper support use of Collagen? Please briefly explain your reasoning followed by "Final Answer:  Positive/Negative/Neutral/Complicated/Unmentioned"
```

ChatGPT(3.5):
```
This paper does provide support for the use of Collagen. In the abstract, it is mentioned that ursolic acid, pomolic acid, colosolic acid, and its methylated derivative exhibited the highest anti-aging activity by stimulating collagen and hyaluronic acid production. This suggests that Collagen, which is known for its role in skin health and anti-aging, may have a positive impact in this context.

Final Answer: Positive
```

The “sentiment attention network” overpowered the “mentioned attention network” early on and then the autoregressive nature meant that this followed through all the way to the answer. 


Note that the above is from GPT 3.5. I did also experiment with GPT4 and I think the output was better (did note that Collagen is not being used as a supplement) but it still failed to get the correct label (this time it was "complicated"). In my (and many others) experience GPT4 is significantly better at understanding the intention of the prompt and not getting tripped up on e.g. Per-Entity Sentiment vs Sentiment of the piece as a whole. However, I think this is due to a better attention network rather than actually adressing the limitation of the architecture.

## Implications for prompting:
You should try and avoid asking for output which will have competing attention networks. In the above example, this means asking it separately if the supplement is unmentioned vs if the paper is positive towards the supplement.


## Potential Solutions:

- Could automatically detect the competing attention networks and solve this properly.
- Explore both paths and rerank? Or maybe something smarter like [Incremental Beam Manipulation](https://aclanthology.org/2021.eacl-main.219/)