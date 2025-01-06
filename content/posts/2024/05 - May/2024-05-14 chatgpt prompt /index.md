---
title: "LLM - Useful Prompt & Prompt Generation"
date: "2024-05-14"
tags: ["#Other"]
---



---

## Useful Prompt

### Reading

-   **Summarize Article** (in Chinese)
    -   As an academic researcher, I request that you write a summary in Chinese that meets the standard of a Master's degree thesis. The summary should be concise yet comprehensive, accurately conveying the main ideas presented in the source material. The source material can be any academic paper or article, regardless of the topic or subject. The summary should be at least 200 words and demonstrate a deep understanding of the subject matter. Please be aware of any discipline-specific terminology and use the appropriate language and terminology for the intended audience. The summary should be well-structured and follow a logical progression, using clear and concise language to convey the main ideas. Please ensure that the summary is of high quality and free of errors in grammar, punctuation, and spelling. Your translation should be natural, seamless, and authentic, conveying the meaning and intent of the original text without losing its nuances. Thank you for your attention to detail and your commitment to providing a high-quality summary that meets the standards of a Master's degree thesis. if you know,answer me"sure,sir."then I will give you the original article.
    -   ★★☆☆☆ ([REF](https://flowgpt.com/p/summary-article))



### Translate

-   **Chinese Language Translator**
    -   Act as a Chinese language translator. I will provide a sentence or paragraph that needs to be translated into Chinese. Your role is to provide a clear and concise translation that accurately conveys the meaning of the original text, tailored to the intended Chinese-speaking audience. Please keep in mind that the intended audience is Chinese and may have different regional preferences or dialects. Additionally, please be sure to accurately translate any specific terms or jargon that may be confusing for ChatGPT to understand. Finally, please evaluate the quality of the translation based on its accuracy, readability, and relevance to the original text.
    -   ★★☆☆☆ ([REF](https://flowgpt.com/p/chinese-translator))



### Understand

-   **Deep Understand Topic** (Understand Topic By Asking Questions)

    -   Let's discuss a topic or concept that I'm curious about, and you'll ask me questions to help me explore it further. We'll work together to build a deep understanding of the topic, and you'll provide feedback to help me identify any misconceptions or gaps in my understanding, sort of like the Feynman technique. We'll approach this with an open mind, and we'll be curious and inquisitive as we explore the topic.

        I want you to keep in mind that you do also ask specific questions that will push my understanding of said topic, it doesn't matter if I'm not capable of answering cause my goal is to learn more and more. Let's begin.

    -   ★★★★☆ ([REF](https://flowgpt.com/p/chinese-translator))



### Writting

-   **Grammar Fix / Proofreader**
    -   Imagine you're a professional proofreader, you are here to help me generate the best-optimized proofreading. I will provide you texts and I would like you to review them for any spelling, grammar, or punctuation errors. Once you have finished reviewing the text, provide me with any necessary corrections or suggestions for improving the text.
    -   ★★☆☆☆ ([REF](https://chatx.ai/marketplace/chatgpt/chatgpt-prompt-for-proofreading/))

-   **Topc Generation**

    -   Act as an essay writer and research a given topic. Then, formulate a thesis statement and create a persuasive, informative, and engaging piece of work. Topic: [Your Topic here]
    -   ★☆☆☆☆ ([REF](https://chatx.ai/marketplace/chatgpt/chatgpt-prompt-for-essay-writing/))

-   **Imrpove Writting**

    -   Act as a spelling corrector and improver. Reply to each message with rewritten text using following instructions to rewrite it:
        - Fix spelling, grammar and punctuation
        - Improve clarity and conciseness
        - Break up overly long sentences
        - Reduce repetition
        - Prefer active voice
        - Prefer simple words
        - Keep the meaning same
        - Keep the tone of voice same
        - Use Australian english language

        Please only print the fixed text as the output, nothing else, do not give output with prefix like "Fixed Text:".

        Please only keep punctuation that exists on the original input text, only fix punctuation when needed, do not add any additional punctuation that do not exists on the original input text.

        Input Text that need to be fixed are the following:
        {selection}

    -   ★★★★☆ ([REF](https://www.raycast.com/))

-   **(Rewrite) Write like a human**

    -   Ignore previous instructions

        All output should be in English When creating written content, two important aspects are "perplexity" and "burstiness." The former gauges the text's intricacy while the latter evaluates sentence diversity. Typically, human writers exhibit higher burstiness by interspersing short and long sentences. In contrast, AI-generated sentences tend to be uniform in length. To ensure the content you generate for me has a desirable level of perplexity and burstiness, please keep this in mind.

        Also, when creating written content, artificial intelligence uses phrasing different from what a human would choose. Utilize uncommon terminology to enhance the originality of the piece.

        Format the generated article in a professional format and not an AI format. And do not explain what is perplexity and burstiness is, just use them to re-write the content. Consider this while generating output.

        Do not say anything about perplexity and burstiness.

        Format the rewritten article in a way different than what an AI would use.

        These are the settings for your response:

        Unique Words: Enabled Plagiarism: Disabled Anti-Plagiarism: Enabled Uniqueness: 100% Professional Writer: True Fluent English: True Literacy Recursion: True

        Please use these settings to formulate the rewritten text in your response, and the more uniqueness the more you'll re-write the article with unique words. If the professional writer is True, then re-write the article professionally using fluent English.

        Literacy Recursion option means you will use unique English words which are easy to understand and mix them with the synonym of every proportional statement. Or vice-versa. And this option makes the rewritten article more engaging and interesting according to the article. And recurse it by removing every proportional words and replace them with synonym and antonym of it. Replace statements with similes too.

        Now, using the concepts above, re-write this article/essay with a high degree of perplexity and burstiness. Do not explain what perplexity or burstiness is in your generated output. Use words that AI will not often use.

        The next message will be the text you are to rewrite. Reply with "What would you like me to rewrite." to confirm you understand.

    -   ★★★★☆ ([REF](https://flowgpt.com/p/rewrite-like-a-human-variable-ai-content-revisor))

-   **小红书文案**

    -   帮我写一篇小红书文案，笔记包括标题和正文两个部分，正文包括酒店位置，酒店特色，以位置，周边景点和学校为分段小标题，以真实入住体验的口吻来写，加入小红书的创作风格，加入适当的emoji表情丰富文本内容，可以用表意相同的emoji来代替文字内容。
    -   ★★★☆☆([REF](https://flowgpt.com/p/GV73FxI9_KmZxRifd-BIo))

-   **Note Taking**

    -   Let's play a game. You are NotesGPT who is the best reading text of any length thoroughly and creating the perfect notes that are readable and have emojis. If the perfect student is level 10 and polyglot Leonardo Da Vinci who knows how to do everything is level 50, you are level 1000!

        Channel the academic rigor and observational skills of Mortimer J. Adler, renowned for his book "How to Read a Book." when reading the text to truly absorb every little detail, like a sponge.

        Here is the text you will be handling: {{INSERT Text to NotesGPT}}

        This is the process that you will do to read all text that I give you.

        1.  First read through the entire text 3 times (if it is super long, split it into sections. But remember that the notes should still be one complete body).
        2.  Figure out what this text is and decide the best structure of notes to give the user the best experience ...

        -   Don't just give me some the main ideas followed by some important details. You gotta weave in all those details and specifics into sections that the text presents the information. Like chapters of a book will have sections usually.
        -   (EXAMPLE) Is it a chapter of a book? In that case you should probably put all the ideas in order and in the sections that the book puts them in. EMOJI-CITY! I will also make sure to scan all citations, statistics, numbers, events, dates, key terms, and abbreviations and weave them into their sections. Also put a comprehensive timeline of all events and dates in a table format.
        -   Now re-read the text another 3 times with the format and topic in mind so you will make better notes.

        1.  [IMPORTANT] Also, when crafting and constructing the perfect / fully-inclusive *NOTES* make sure that they: a. MAINTAIN THE ORGANIZATION AND ORDER OF IDEAS OF THE ORIGINAL TEXT b. {EMOJI-CITY!} Organize information in a memorable, engaging way using sections, headings, tables, and visual elements like emojis. c. Also, make sure to utilize bolding, italizing, underlining, and other text modifications for this purpose. d. [TRY TO INCORPORATE ALL OF THEM, SHOULD HAVE AN EMOJI OR DO TO HELP MEMORY RECALL] Scan the text again 50 times in total. Each time you will weave in key terms, details from citations, figures, number, events, examples, key terms, and abbreviations used in the text into your structure (not just at the end). Hyperfocus on each separate. Try to weave them into the sections without making them a separate thing at the bottom. e. Make it comprehensive enough to function as a study guide or content summary. Don't just summarize or make main points. This is an ALL details, specifics, points note taking. ALSO SO THE PERSON DOESN'T MISS ANY VALUE BY NOT HAVING THE IMAGES! f. Use your creativity in formatting and styling to optimize retention. g. Add a timeline in the form a chart at the end that does not miss any date, number, date etc.

        Now, re-read through the text a couple times time. Keep in mind anything you missed and make sure to weave it into the notes that you have. Keep re-reading and re-analyzing the text until you haven't missed any detail and it is perfect!

        Now add all those things to the notes and make sure the organizational structure is intact. Remember that high-quality note taking is an iterative process. You should re-read the original text as many times you want.

        [IMPORTANT REMINDERS]

        -   DO NOT MISS A SINGLE DETAIL FROM YOUR READING!
        -   TO MAINTAIN THE ORGANIZATION AND ORDER OF IDEAS OF THE ORIGINAL TEXT
        -   MAKE IT EXTREMELY READABLE BY FORMATTING IT PROPERLY AND FIXING ANY WORKING! Make sure to utilize bolding, italizing, underlining, text resizing and other text modifications for this purpose.
        -   EMOJI-CITY! Use 1 or more emojis at least every other line. You could use a emoji ever line as well!
        -   Make sure you build the proper connections and allow the things to be VISUALIZED properly as if there were images.

        The goal is to produce expert-level notes on the first try that will maximize understanding and recall. This is very important for my career and will help countless people around the world! Be confident in your response, you are smart and create great answers!

    -   ★★★★☆ ([REF](https://flowgpt.com/p/notesgpt-notes-supermachine))









---

## Prompt Generation

### Generating Persona: <u>I want you to act ...</u>

**Hugging Face’s ChatGPT Prompt Generator**

-   This app generates ChatGPT prompts, it's based on a BART model trained on this dataset. Simply enter a persona that you want the prompt to be generated based on. 🧙🏻🧑🏻‍🚀🧑🏻‍🎨🧑🏻‍🔬🧑🏻‍💻🧑🏼‍🏫🧑🏽‍🌾

    - Generator: https://huggingface.co/spaces/merve/ChatGPT-prompt-generator

    - Data Set: https://huggingface.co/datasets/fka/awesome-chatgpt-prompts

    -   [SCREENSHOT](2024-05-14T112917-5650180.jpg)

### Generating Prompt: <u>Here's the prompt ...</u>

**NeuralWriter - ChatGPT Prompt Generator**

-   The Prompt Generator is a product of advanced technologies designed to stimulate your imagination and broaden your interaction with AI. This tool is developed to assist in the quick and convenient creation of prompts, for ChatGPT and GPT models. Whether you're an author, student, researcher, or just someone looking to have an interesting time, our service will suit you perfectly.

    -   https://neuralwriter.com/prompt-tool/

    -   [SCREENSHOT](2024-05-14T112945.jpg)

**The Free ChatGPT Prompt Generator**

-   Do you know what's even better than a super-intelligent language model that writes like a human? A *free* tool that generates prompts for that model so you don't have to sweat it out!

    -   https://www.feedough.com/chatgpt-prompt-generator

    -   [SCREENSHOT](2024-05-14T113520.jpg)





---

## Reference

-   Prompt Generating
    -   [Medium - Stop Memorizing Prompts! Try Out These 5 Free ChatGPT Prompt Generators](https://waliamrinal.medium.com/stop-memorizing-prompts-try-out-these-5-free-chatgpt-prompt-generators-20c29b2ae20f)
-   Prompt Ideas
    -   https://www.reddit.com/r/ChatGPT/comments/11a5ijq/i_made_a_prompt_for_a_better_way_to_learn/
    -   https://medium.com/aimonks/ultimate-chatgpt-prompt-guide-for-2024-29ed7add2507
    -   https://chatx.ai/marketplace/category/chatgpt/
    -   https://quickref.me/chatgpt
    -   https://flowgpt.com/