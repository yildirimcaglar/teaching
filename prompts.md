---
title: Prompt Engineering
layout: default
---

Retrieval-Augmented Generation (RAG) is a technique that integrates an information retrieval component with a generative language model. Instead of relying solely on the knowledge stored in a model’s parameters, a RAG system retrieves relevant external information (e.g. documents from a knowledge base) to ground the model’s output. In essence, a RAG model combines a parametric memory (the knowledge implicit in the trained weights of an LLM) with a non-parametric memory (an external database or document index) to produce responses [^1]​. This allows the model to access up-to-date, specific facts on demand, addressing limitations of traditional LLMs that have a fixed training corpus cut-off date​
medium.com
. By incorporating retrieved evidence into generation, RAG can ensure the output is contextually relevant and grounded in factual information, significantly enhancing accuracy and reducing hallucinations​
developers.cloudflare.com
​
aclanthology.org
. In other words, the model “augments” its generative process with real-time knowledge lookup, which improves the coherence and correctness of its answers beyond what its frozen training data provides.

```python
def my_function(a, b):
    return a*b
```

## References

[^1]: [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://proceedings.neurips.cc/paper/2020/file/6b493230205f780e1bc26945df7481e5-Paper.pdf){:target="_blank"}