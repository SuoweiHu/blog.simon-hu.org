---
title: "LLM: Prompt Engineering"
date: "2024-04-28"
categories: ["LLM"]
---





----

## Intuition Behind this Post ? 

The reason I wanted to know a little more about how this topic (Prompt Engineering) is getting scoped, and how people in the area have contributed till this date, is because I wanted to utilise one of the super-search tool I've been using since the past fre year: **Raycast**, just a little bit better.

![2024-04-28T153443](2024-04-28T153443.png)

I know **Raycast** have been having the feature of "<u>AI Command</u>" for almost around 1 year now, of which allows you to use any of the AI prompt as a "command" to run; On the raycast community I saw people using it for change tones, enhanec writting, find synonyms, and etc, but for me personally, its just extremely weird having to use it as a <u>one-time command</u>, my experience with the ChatGPT before it came out is usually more towards a continues, step-by-step process. 

A surprise for me came out for me on 24 April 2024, **Raycast** formally anncouned their "<u>AI Preset</u>" feature. With the new feature you are allowed to create your own preset and have it opened as a <u>continuable chat box</u> (where you specify the system instruction and continue the conversation based on that), rather than one-time command. 

![2024-04-28T152656](2024-04-28T152656.png)

This feature has made using AI in my day-to-day workflow much more intuitve, and I'd consider it as a great opportunity for myself to dive a little bit more into the AI hype. 

So in order to use this new feature well, I will first have to under stand how to configure these preset, this post will cover just one of the parameter users can alter: <u>system instruction</u>. You can consider this as the pre-configurations of the LLMs before you start the conversations, these pre-configurations can involve: 

-   The format of the **input** (e.g. list, json, html, etc)
-   The scope of the **questions** (e.g. what to include, what to exclude)
-   The expected **action to perform** (e.g, find bug, fix grammer, enhance writting, change tone) 
-   The format of the **output** (dot points, length, tone, etc)
-   Provide **example** of the input & output pairs (like ChatGPT is an LLM model that...., explain what is AlphaGo)
-   more.

To understand this well I will need to learn a little bit more about the topic: "Prompt Engineering"



---

## What is Prompt Engineering ? 

To understand what is Prompt Engineering, let's quickly reference some of the resource found online: 

-   >   Prompt engineering is enabled by in-context learning, defined as a model's <u>ability to temporarily learn from prompts</u>. The ability for in-context learning is an emergent ability of large language models. In-context learning itself is an emergent property of model scale, meaning 
    >
    >   -- In-context learning - **Wikipedia**

-   >   Prompt engineering is the process of <u>structuring an instruction</u> that can be <u>interpreted</u> and <u>understood</u> by a generative AI model. A prompt is natural language text <u>describing the task</u> that an AI should perform ... Prompt engineering may involve <u>phrasing a query</u>, <u>specifying a style</u>, <u>providing relevant context</u> or <u>assigning a role</u> to the AI such as "Act as a native French speaker". A prompt <u>may include a few examples</u> for a model to learn from, such as asking the model to complete "maison → house, chat → cat, chien →" (the expected response being dog), an approach called few-shot learning.
    >
    >   -- Prompt engineering - **Wikipedia**

-   >   Prompt engineering is a relatively new discipline for developing and optimizing prompts to efficiently use language models (LMs) for a wide variety of applications and research topics. Prompt engineering skills help to better understand the capabilities and limitations of large language models (LLMs) ... Researchers use prompt engineering to improve the <u>capacity</u> of LLMs on a wide range of common and complex tasks such as question answering and arithmetic reasoning. Developers use prompt engineering to design robust and effective prompting techniques that <u>interface with LLMs and other tools</u>.
    >
    >   -- Prompt Engineering Guide - **promptingguide.ai**

So to recap the findings, we found : prompt engineering is a technique enabled by LLM's ability to temporaily learn from the prompt; we use prompt engineering to pre-configure the model via describing the task, phrasing a query, specifying a style, provide context, assign role, and give example; And as a result enable the model to complete more complex task in a more consistent, accurate and precise manner. 







---

## Terminologies in Prompt Engineering ? 



### Prompt Elements

According to website [promptingguide.ai](https://www.promptingguide.ai/introduction/elements), aprompt contains any of the following elements:

-   **Instruction** - a specific task or instruction you want the model to perform

-   **Context** - external information or additional context that can steer the model to better responses

-   **Input Data** - the input or question that we are interested to find a response for

-   **Output Indicator** - the type or format of the output.



### Prompt Techniques

According to [Amir Aryani](https://medium.com/@amiraryani/8-types-of-prompt-engineering-5322fff77bdf) and [PromptingGuide.AI](https://www.promptingguide.ai/techniques), there are dozens of common prompt engineering technique (method): 



1.   #### **Zero-shot learning** 

     >   Large language models (LLMs) today, such as GPT-3.5 Turbo, GPT-4, and Claude 3, are tuned to follow instructions and are trained on large amounts of data, <u>large-scale training</u> makes these models capable of performing some tasks in a "zero-shot" manner. Zero

     Provide no prior example to the model, give instruction directly.

     ```
     Prompt1:   What is the color of the sky? 
     Output1:   Blue
     ```

     

2.   #### **Few-shot learning**

     >   While large-language models demonstrate remarkable zero-shot capabilities, they still fall short on more complex tasks when using the zero-shot setting. Few-shot prompting can be used as a technique to <u>enable in-context learning</u> where we provide demonstrations in the prompt to steer the model to better performance.

     Provide one or many examples to help model understand the pattern, and then give instruction.

     ```
     Prompt1:   A "whatpu" is a small, furry animal native to Tanzania. An example of a sentence that uses the word whatpu is: We were traveling in Africa and we saw these very cute whatpus.
                To do a "farduddle" means to jump up and down really fast. An example of a sentence that uses the word farduddle is:
     Output1:   When we won the game, we all started to farduddle in celebration.
     ```



3.   #### **Chain-of-Thought Prompting**

     >   Introduced in [Wei et al. (2022)](https://arxiv.org/abs/2201.11903), chain-of-thought (CoT) prompting enables complex reasoning capabilities through <u>intermediate reasoning steps</u>. You can combine it with few-shot prompting to get better results on more complex tasks that require reasoning before responding.

     Provide not only example, but also step-by-step progress (i.e. chain-of-thought) of how you get to the answer. 

     ```
     Prompt1:   Q: The odd numbers in this group add up to an even number: 4, 8, 9, 15, 12, 2, 1. 
                A: Adding all the odd numbers (9, 15, 1) gives 25. The answer is False.
                ... 
                ... more examples
                ... 
                Q: The odd numbers in this group add up to an even number: 15, 32, 5, 13, 82, 7, 1. 
                A: ?
     Output1:   Q: The odd numbers in this group add up to an even number: 15, 32, 5, 13, 82, 7, 1.
                A: Adding all the odd numbers (15, 5, 13, 7, 1) gives 41. The answer is False.
     ```



4.   #### **Generate Knowledge Prompting** 

     >   LLMs continue to be improved and one popular technique includes the ability to incorporate knowledge or information to help the model make more accurate predictions. Using a similar idea, can the model also be used to generate <u>knowledge before making a prediction</u>? That's what is attempted in the paper by [Liu et al. 2022(opens in a new tab)](https://arxiv.org/pdf/2110.08387.pdf) -- generate knowledge to be used as part of the prompt.

     Provide some knowledge in the prompt that are not examples but will assists with answer.

     ```
     Prompt1:    QuestionPart of golf is trying to get a higher point total than others. Yes or No?
                 Knowledge: The objective of golf is to play a set of holes in the least number of strokes. A round of golf typically consists of 18 holes. Each hole is played once in the round on a standard golf course. Each stroke is counted as one point, and the total number of strokes is used to determine the winner of the game.
                 Explain and Answer: 
     Output1:    No, the objective of golf is not to get a higher point total than others. 
                 Rather, the objective is to play a set of holes in the least number of strokes. 
                 The total number of strokes is used to determine the winner of the game, not the total number of points.
     ```



5.   #### **Prompt Chaining**

     >   To improve the reliability and performance of LLMs, one of the important prompt engineering techniques is to <u>break tasks into its subtasks</u>. Once those subtasks have been identified, the LLM is prompted with a subtask and then its <u>response is used as input to another prompt</u>. This is what's referred to as prompt chaining, where a task is split into subtasks with the idea to create a chain of prompt operations.

     Breakdown a single query into multi-step prompts, use output of one prompt as input of the another prompt.

     ```
     Prompt1:     Give me a list of commonly seem vegitables used in Italian food. 
     Output1:     1. Tomatoes
                  2. Peppers
                  ...
     		     ... (vegitable)
       		     ...
                  9. Radishes
     Prompt2:     Could you tell me explain how can the first one on the list being used as flavouring ?
     Output2:     Tomatoes are commonly used in Italian cuisine as a flavoring agent in various dishes such as sauces, soups, and stews. 
                  They are often cooked down to create a rich, savory base that enhances the overall taste of the dish. 
                  Tomatoes also provide a natural acidity and sweetness, adding depth and complexity to the flavors of Italian recipes.
     ```

     

     

6.   #### **Other Techniques**

     Below are some other prompting technique or method being metioned in the posts:

     -   Amir Aryani

         -   One-shot learning 

         -   Negative Prompting 

         -   Hybrid Prompting

         -   Iterative Prompting

     -   PromptingGuide.A

         -   Tree of Thoughts

         -   Retrieval Augmented Generation

         -   Automatic Reasoning and Tool-use

         -   Automatic Prompt Engineer

         -   Active-PromptDirectional Stimulus Prompting 

         -   Program-Aided Language Models

         -   ReAct

         -   Reflexion

         -   Multimodal CoT

         -   Graph Prompting

     

     

---

## Refernece 

-   **What is Prompt Engineering**
    -   https://en.wikipedia.org/wiki/Prompt_engineering
    -   https://www.promptingguide.ai/
-   **Prompt Termonologies**
    -   https://www.promptingguide.ai/
    -   [8 Types of Prompt Engineering - Amir Aryani](https://medium.com/@amiraryani/8-types-of-prompt-engineering-5322fff77bdf)