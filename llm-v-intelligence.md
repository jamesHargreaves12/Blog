# LLMs v Intelligence (2024)

A common belief among some high-profile figures is that Artificial General Intelligence (AGI) or even Artificial Super Intelligence (ASI) is just around the corner. According to this narrative, Large Language Models (LLMs) will revolutionize everything: replacing all jobs, solving humanity’s toughest challenges, and reshaping the world—provided we keep scaling up compute.

I remain unconvinced that LLMs are set to dominate our future.

## Current Performance of LLMs

### "Saturating the Benchmarks"

OpenAI aims to “Saturate the benchmarks” this year. Notably, the definition of "the benchmarks" focuses only on sequential reasoning or text comprehension tasks, areas where LLMs excel. While it will be impressive if OpenAI succeeds, we shouldn’t assume this alone signals the arrival of ASI.

### Where LLMs fall short

Most past ML competitions involve labeled datasets and specific outcomes to forecast. No one claims LLMs have advanced these areas. Random Forests or Gradient Boosted Decision Trees outperform LLMs on numerical or tabular data, underscoring that LLMs aren’t universal solutions.

We are, in effect, being sold a hammer and told it can handle every nail—then asked to believe it’s a complete toolkit. Below are four reasons why scaling up to even ‘smarter’ LLMs will not fundamentally change the landscape.

## “Smarter” LLMs Won't Change the Landscape

1. **Data and Context Limits**

The initial excitement around LLMs stemmed from their Zero-Shot and Few-Shot learning abilities. They generate decent results with minimal prompting. However, these techniques have a low ceiling. Transformers can only attend to a limited chunk of text and must ignore what they deem less important. This restricts how much they can learn at inference time. In contrast, traditional ML methods can keep learning from vast amounts of data, producing more accurate mappings between inputs and outputs.

2. **Sequential, Single-Hypothesis Reasoning**

Many LLM breakthroughs rely on teaching models to think through tasks one step at a time. Yet, following a single line of thought can be limiting. Even though models can backtrack when they get stuck, exploring multiple paths in this manner is extremely inefficient. For any practical compute budget, this constrains the complexity of solvable problems. Furthermore, some problems are inanetly uncertainty. You must aggregate across many scenarios to decide which outcome is most likely. This is infeasible with sequential reasoning.

3. **Weak Interactions**

Real-world predictions often involve countless, intertwined variables. LLMs can pick up on the strongest factors but struggle with subtle interactions. Traditional ML approaches can model arbitrarily complex relationships when given sufficiently large training datasets. If the task is critical, the cost of constructing a specialized dataset is well worth the consistent, accurate outcomes.

4. **Evaluation Challenges**

Alignment & Interpretability: While unaligned superintelligence dominates headlines, many companies face a simpler problem: LLMs can be unpredictable on inputs that differ slightly from their training data. Even some of the [most valuable companies](https://techcrunch.com/2024/02/23/embarrassing-and-wrong-google-admits-it-lost-control-of-image-generating-ai/) have been embarrassed when queries fell just outside their tested range. Using structured data allows more control over what a model focuses on, creating more reliable and explainable results.

## A Note on Generalism

One major selling point of LLMs is their “general” nature — they do many tasks reasonably well — a jack of all trades. For a given problem we want the best solution and so we will always prefer the specialized solution. A washing machine only does one job, but it arguably had [greater economic impact than the internet](https://www.amazon.co.uk/Things-They-Dont-About-Capitalism/dp/0141047976).

## Unique Non-Human Capabilities

LLMs impress us with their human-like synthesis of knowledge. The hope is that this will increase our productivity and allow us to focus elsewhere. However, its far from obvious this will also result in novel breakthroughs.

Contrast this with a methods that learns and acts in ways uncorrelated to human cognition. This complements our intelligence and unlocks entirely new classes of problems.

## Conclusion

LLMs have earned their reputation for versatility and language-based reasoning. They are far from becoming an all-encompassing solution to modern challenges. Their strength lies in applications where quick results and broad knowledge synthesis matter more than domain-specific optimization or interpretability. Yet, to solve problems involving specialized data or complex multi-path reasoning, other techniques remain essential. Ultimately, LLMs are a welcome addition to the data science toolkit, but they will are not AGI.

