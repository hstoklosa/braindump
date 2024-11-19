# Introduction to LLMs

These basic notes answer the high-level questions:

- _What are LLMs?_
- _How do they work?_
- _What are the use cases?_

## Overview

<img src="../images/llms-roadmapsh.png" width=500 />

## What are LLMs?

LLM stands for **Large Language Models**.

LLMs are advanced AI systems designed to **understand** and **generate** human-like text based on the received input.

These models have been trained on large amounts of text data, which allows them to perform language-related tasks such as:

1. Answering questions
2. Carrying conversations
3. Summarising input text
4. Translating text

Contributors to LLM:

- OpenAI — GPT-3, GPT-4
- Meta — [OPT](https://huggingface.co/facebook/opt-66b), [OPT-IML](https://huggingface.co/facebook/opt-iml-30b), [LLaMA](https://ai.meta.com/blog/large-language-model-llama-meta-ai/)
- Google — [FLAN-T5](https://huggingface.co/google/flan-t5-xxl), [BERT](https://huggingface.co/bert-base-uncased)
- Stability AI — [StableLM](https://github.com/stability-AI/stableLM/)
- Stanford — [Alpaca](https://crfm.stanford.edu/2023/03/13/alpaca.html)
- Open-Source LLMs — [open-llms](https://github.com/eugeneyan/open-llms), [awesome-llm#open-llm](https://github.com/Hannibal046/Awesome-LLM#open-llm)

## Training an LLM Model

Training an LLM model involves 3 steps:

1. **Data Collection:** Collect data from various sources such as Wikipedia, news articles, books, websites, and so on.

2. **Training:** Put the data through a training pipeline where it is _cleaned_ and _preprocessed_ to remove any irrelevant information before feeding it into the model for training.

   The training itself requires a lot of time and vast amount of computational power.

3. **Evalutation:** Evaluate the performance of the model in order to see how well it performs on various tasks.

Output of the training pipeline = LLM model in the form of parameters or weights which capture the knowledge gained during the training process.

Parameters or weights are serialised (converted to binary) and stored in a file that can be loaded into any applications that requires language processing capabilities.

## Types of LLMs

### Base LLMs

Designed to predict the next word based on the training data and lack the ability to perform well on other tasks.

Example 1:

- **Input:** “In this book about LLMs, we will discuss”
- **Output:** “In this book about LLMs, we will discuss what LLMs are, how they work, and how you can leverage them in your applications...”

Example 2:

- **Input:** “What are some famous social networks?”
- **Output:** "Why do people use social networks?” _or_ “What are some of the benefits of social networks?”

It provides relevant text (gathered from training), but it is clearly not answering the questions.

## Instruction Tuned LLMs

Try to follow the given instruction using the data they have been trained on.

For example: if you input the sentence “What are LLMs?” it will use the data that it is trained on and try to answer the question.

**IT-LLMs are built on top of B-LLMs**

- Instruction Tuned LLMs = Base LLMs + Further Tuning + RLHF
- Base LLM is further trained using large dataset covering sample "Instructions" and how the model should perform as a result of those instructions.
- Later, it is fine-tuned using Reinforcement Learning from Human Feedback (RLHF) which allows the model to improve its performance over time.

## Conclusion

LLMs are a powerful tools that can be used to solve a variety of language-related tasks.

They have the potential to revolutionise the way we interact with computers and make our lives easier.

<br>

_Source: [https://roadmap.sh/guides/introduction-to-llms](https://roadmap.sh/guides/introduction-to-llms)_
