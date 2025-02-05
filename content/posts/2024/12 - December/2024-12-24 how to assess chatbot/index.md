---
title: "[Note] Parameters to assess ChatBot products ?"
date: "2024-12-24"
tags: ["#Other"]
---

```
alais:
- how to compare ai models
- how to assess chatbot products
- how to choose the best ai model
```



## Quick Comparison

Here's a table of spec comparsion for the most current model:

| Feature | Claude 3.5 Sonnet | OpenAI o1 | DeepSeek R1 |
|---------|------------------|------------|--------------|
| Model Size | Unknown | 2.8T parameters (unconfirmed) | 671B parameters (37B active per token) |
| Context Window | 200K tokens | 128K tokens | 128K tokens |
| Max Output | 4K tokens | 32K tokens | 32K tokens |
| Vision Capability | Yes | No | No |
| Knowledge Cutoff | April 2024 | Oct 2023 | Unknown |
| Cost (Input) | $3/1M tokens | $15/1M tokens | $0.55/1M tokens |
| Cost (Output) | $15/1M tokens | $60/1M tokens | $2.19/1M tokens |
| Open Source | No | No | Yes (MIT License) |
| Hallucination Rate | Unknown (Lower than previous models | Unknown (Lower than GPT-4 (0.44 on SimpleQA) | Unknown (4x higher than DeepSeek V3 |
| Performance | 40% success on autonomy tasks | High performance on AIME, Codeforces, GPQA-Diamond | Comparable to o1 on math and coding tasks |
| Special Features | Constitutional AI framework, near-perfect recall | Advanced reasoning capabilities, high accuracy on complex tasks | Resource-efficient MoE architecture, self-discovering reasoning strategies |

(updated on "2025-02-05T144338", generated using perplexity)





## Parameters to Compare

#### Context

- **context window**:
    - How much information can you feed into the chatbot at once?
    - This is typically measured in words or tokens.
- **context remainment**:
    - How many back-and-forth exchanges can occur before the chatbot begins to forget earlier parts of the conversation?
    - What's the maximum conversation length it can effectively maintain?

#### Reliability

- **hallucination**:
    - How accurate is the chatbot's information?
    - Can it resist confirming biased or incorrect assumptions in questions?
    - Does it generate false or misleading information while presenting it as fact?
- **internet access** :
    - Can the bot retrieve real-time information from external sources?
    - Does it automatically access websites, academic papers, or other online resources when needed ?
- **source transparency** :
    - Does the bot cite its sources?
    - Is it clear about where its information comes from?
    - Does it explain the basis for its responses?

#### Usability

- **writting tone**:
    - How natural and human-like is the bot's communication?
    - Can it adjust its tone to match different situations?
- **multi-model**:
    - Can the bot process different types of input beyond text?
    - Does it handle documents (PDF, DOCX), images, audio, and video?
    - Can it effectively use information from these various formats in its responses?
- **response freshness:**
    - How consistent are the bot's responses to identical questions?
    - Does it offer helpful variations in its answers?
- **legal liability**:
    - Does the bot recognize and refuse inappropriate requests?
    - How does it handle sensitive topics (political, legal, or ethical issues)?
    - Are there clear guidelines about what it won't discuss?

#### **Other**

-   **community**:
    -   Is there an active community developing extensions or plugins?
    -   Are there readily available tools to enhance the bot's capabilities using initial prompting? and can the bot be customized for specific professional needs (like writing, teaching, or specialized fields)  ?



## Reference

- [Save Your Money: My Honest Take on ChatGPT4, Claude Pro, Gemini Advanced, Perplexity Pro](https://www.youtube.com/watch?v=shWwlt76qHo&list=WL&index=6)