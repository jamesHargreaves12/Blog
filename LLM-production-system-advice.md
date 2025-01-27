## LLM in Productions

Many production systems are integrating large language models (LLMs) in ways that are fundamentally flawed. While these models offer remarkable capabilities, their naive deployment often leads to inefficiencies, poor user experiences, and wasted resources. This essay critiques these practices and presents practical recommendations for better utilization of LLMs.

### Cost

The computational requirements for each request—and therefore the associated cost—are substantial for large models. Importantly, the expense isn’t limited to training; the computation spent per query is high (and getting higher with OpenAI's O-series models), leading to high marginal costs. This makes large language models less economical for routine tasks.

Google provides the world’s best search engine for free and monetizes through occasional ad clicks, enabling it to be immensely profitable (even considering R&D costs). This is feasible because the marginal cost of each search is incredibly low, allowing R&D costs to be amortized across billions of queries. If the cost of a search were 10,000 times higher (as some estimates suggest for LLMs), users would either have to endure countless ads or pay for each search, drastically reducing usage.

### Latency

LLMs are slow. Latency matters for user engagement. For instance, Google’s research shows that a 400ms delay results in a 0.44% drop in search volume. The latency we are talking about with LLMs is orders of magnitude higher.

This latency is jarring in chat applications and catastrophic in other contexts, forcing product teams to invest time in mitigating it. Instead of building better features, developers often find themselves designing clever loading spinners to mask delays.

### Existing Infrastructure

Routing user queries directly to an LLM hosting service can expose API keys, enabling users to send unlimited queries at your expense. To prevent this, it’s standard to route queries through your API, which introduces new challenges.

Many web servers are optimized for small, quick queries that don’t hold server resources for long. Sending large amounts of text to and from an LLM disrupts these assumptions.

### Streaming

Waiting for an LLM query to finish before displaying text results in an unusable user experience. We are forced to stream data incrementally to the user, but this introduces new problems. Atomic web requests are a much simpler, faster, and more robust primitive to program with.

- If an atomic web request fails, we can just retry it without the user being aware. However, a failure mid-stream—once the user has received partial output—means you cannot mask the failure from the user. The retry logic is often impossible without starting the stream from the beginning.
- This compounds with the fact that you will get more errors. Maintaining long-lived connections increases the likelihood of failure, especially on mobile networks.
- If your application renders anything more complicated than raw text—such as HTML links—you don’t know how to display token X until you have seen token X+n. Either you spend your time trying to solve this problem or force your users to deal with unpleasant jitter.

### Unstructured Output

User interfaces are designed to present information to the user and highlight what is and isn’t important. When the data being displayed to the user is structured, it allows designers to prioritize and present information effectively. When data is unstructured, creating rules for its presentation becomes complex, resulting in a degraded user experience.

One common workaround to the "wall of text" experience is to manually post-process the LLM output, generating custom UI elements on the fly. However, language is inherently ambiguous, and writing rules for processing unstructured text often leads to UIs littered with poorly handled edge cases and bugs.

A better approach is to prompt the LLM to generate the output in the form you want it. For example, you could give it an HTML template to fill in. Even if the LLM fails to follow the template, the result is often coherent. Users prefer experiences that are degraded rather than unusable.

### Batch Mode

Many issues associated with LLMs arise from their use in real-time user interactions. When used in batch mode—for example, during development or backend processing—these problems diminish significantly.

Often, a complicated (and unreliable) RAG (Retrieval-Augmented Generation) system  can be improved by replacing it with a database of key entities and relationships plus a set of predefined queries. Building out such a database used to be prohibitively expensive; it no longer is with LLMs.

Another underappreciated benefit of this approach is that mistakes can be fixed. When a mistake is found, you just issue an update to the affected row. If your alternative was to modify the prompts, it’s almost impossible to work out the impact. So you often just fail to fix the issue.

### Closing Thoughts

While most problems with LLMs can be mitigated, doing so diverts developer time from adding value elsewhere—building features and improving user experiences.

**Key Recommendations:**

1. Limit the use of LLMs in user-facing systems wherever possible.
2. Use LLMs to translate unstructured user inputs into structured data for other systems, rather than exposing raw outputs.
3. Avoid extensive post-processing of LLM outputs. Instead, guide the LLM to generate structured or UI-ready output directly.
4. Leverage LLMs aggressively in batch mode to produce structured datasets, integrating them into live systems for scalable and maintainable solutions.&#x20;
