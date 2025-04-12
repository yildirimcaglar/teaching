---
title: Retrieval-Augmented Generation
layout: default
---
## Overview

{: .note}
This chapter provides an introductory coverage of retrieval-augmented generation and assumes that you have a background in ML and LLMs.

Retrieval-Augmented Generation (RAG) is a technique that integrates an information retrieval component with a generative language model. Instead of relying solely on the knowledge stored in a model’s parameters, a RAG system retrieves relevant external information (e.g. documents from a knowledge base) to ground the model’s output. In essence, a RAG model combines a parametric memory (the knowledge implicit in the trained weights of an LLM) with a non-parametric memory (an external database or document index) to produce responses [^1]​. This allows the model to access up-to-date, specific facts on demand, addressing limitations of traditional LLMs that have a fixed training corpus cut-off date​ [^2]. Through the incorporation of retrieved evidence into generation, RAG can ensure the output is contextually relevant and grounded in factual information, significantly enhancing accuracy and reducing hallucinations​ [^3]. In other words, the model “augments” its generative process with real-time knowledge lookup, which improves the coherence and correctness of its answers beyond what its frozen training data provides.

```python
def my_function(a, b):
    return a*b
```

## References

[^1]: [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://proceedings.neurips.cc/paper/2020/file/6b493230205f780e1bc26945df7481e5-Paper.pdf){:target="_blank"}


[^2]: [A Survey on RAG Meeting LLMs: Towards Retrieval-Augmented Large Language Models](https://dl.acm.org/doi/abs/10.1145/3637528.3671470){:target="_blank"}

[^3]: [Retrieval Augmented Generation (RAG)](https://developers.cloudflare.com/reference-architecture/diagrams/ai/ai-rag/#:~:text=Retrieval,models%20to%20enhance%20text%20generation){:target="_blank"}




