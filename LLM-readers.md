## LLMs are better readers than writers 

Generative AI has become almost synonymous with LLMs, and their generative capabilities are without a doubt the most magical thing I have ever seen. However, is this truly where the value lies? There's a huge amount of money banking on the answer being yes. My belief is that the majority of the value of LLMs lies in their ability to understand text rather than simply generate it.

## The Underappreciated UX Impact of LLMs

I have been writing software as a hobby, academically, and professionally for 16 years now. One thing I always loved was that I could make it do exactly what I wanted, and I could always understand why it behaved the way it did. You could do anything once you discovered the correct syntax / api.

However, I always hated the process of finding that bit of syntax - getting to the right page is inconvenient, slow, and meandering. When speaking to humans, we share common sense, even when talking to complete strangers. This means you don't have to reiterate the obvious every time. Furthermore, if you ask a colleague about debugging Kubernetes and then follow up with a question about persistent storage, you don't need to reiterate that you're only asking about Kubernetes.

One of the most profound workflow changes brought by LLMs is their ability to handle underspecified queries effectively. In traditional workflows, success often depended on how precisely a problem was framed. With LLMs, this barrier is significantly lowered—they intuitively grasp context and intent without requiring users to provide exhaustive details. As a programmer, this has a big impacts on my ability to stay in the flow and continue to focus on the problem at hand. I would go as far as to say that if the same input simply crafted the perfect Google search query rather than rendering the example, I would use this over ChatGPT—it would be much easier to recover when it gets things wrong. Caveat: I'm not going to claim this is the case for queries in modes outside of the programming assistant.

## LLMs for Application Builders

LLMs understand unstructured data better than any tool we’ve had before. They grasp the meaning of text, what’s relevant to your query, and even the content of images.

LLMs can reliably translate information between domains:

- "Translate this English sentence into French."
- "What is happening in this image?"
- "Re-write this Python code in Rust (a high-performance programming language)."
- "Extract the ingredients mentioned in this recipe."

Examples like the last one are particularly exciting.


We live in a sea of text documents, articles, and PDFs—a vast majority of humanity’s knowledge base resides in them. Until recently, this information has been essentially unusable to software systems and their programmers. Efforts to extract this data, such as regex parsing or building syntax trees, rarely made it out of the proof of concept stage - drowning in edge cases. LLMs excel at parsing these documents, understanding the author’s intent, and extracting key facts.
These facts can then be fed into narrower, more specialized systems.

### Building Datasets

You can build structured datasets from unstructured text.

Given a structured dataset, your problem starts to resemble those we’ve solved over the past 30 years while building the internet. This unlocks the huge array of battle-tested tools and best practices:

- **Databases**: Perfect for fast queries, robust joins, ACID compliance, and data permissioning.
- **Caching Layers**: Enable fast retrieval for common queries. In structured systems, many subqueries look the same. This is not true in free-form queries; for example, 15% of Google searches are entirely new every day ([source](https://searchengineland.com/google-reaffirms-15-searches-new-never-searched-273786)).
- **Web Servers**: Built around the assumption that most queries are small (data-wise) and quick (low resource usage).
- **Programming Languages**: Control system behavior and enforce business logic in guaranteed, trustworthy, and reliable ways.
- **User Interfaces (UI)**: Structured data allows UIs to focus on display and interaction. As data becomes less structured, the problem becomes harder, and user experience suffers. Our current best UIs for LLMs are essentially “walls of text” that leave users to deal with the complexity.
- **Structured Data Predictions**: Gradient boosting frameworks, linear models, or classical ensembles are all designed to work on structured data. These are simpler, easy to reason about, and in almost all cases more effective and predicting the thing you care about.
