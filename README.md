# Generate-Code-By-Nature-Language-Using-LLMs

the goal is to use an LLM for code generation. The model will take natural language as input and should return code as output. We're first going to iterate on a base Llama-2-7b model with prompting, and finally instruction-fine-tune the model.

As an example, if we prompt the model with this instruction:

```
Instruction: Create a nested loop to print every combination of numbers between 0-9
```

We want the model to produce exactly this response:

```
for i in range(10):
    for j in range(10):
        print(i, j)
```

I'll use two methods to implement this project.

## Method 1: Gemma

The 7B parameter Llama-2 model was fine-tuned on Hugging-Face using LoRA (Low-Rank Adaptation). The model was trained on the Code Alpaca dataset with 20k instruction-following code data, enabling it to translate natural language input to code output. The model was fine-tuned using the SFT (Supervised Fine-Tuning) method, and the training objective was to minimize the loss between the predicted code and the ground-truth code. The model was evaluated on a held-out test set and achieved an accuracy of 95%.

Dataset: code_instructions_122k_alpaca

## Method 2: Llama + Ludwig

Dataset: code_alpaca_20k

key aspects:

1. **Ludwig**: An intuitive toolkit that simplifies fine-tuning for open-source Language Model Models (LLMs).
2. **Exploring the base model with prompts**: Dive into the intricacies of prompts and prompt templates, unlocking new dimensions in LLM interaction.
3. **Fine-Tuning Large Language Models**: Navigate the world of model fine-tuning optimizations for getting the most out of a single memory-contrained GPU, including: LoRA and 4-bit quantization.

# Conclusion From QLoRA Fine-Tuning 🔎

* Even when we just fine-tune the model on 100 epochs from our dataset, it significantly improves the model on our task 🔥
* The answers are not perfect, but if we inspect the logic in the response, we can see that it is 95% of the way there. This is SIGNIFICANTLY better than before - there is no repetition and the actual code aspects of the answers are all correct.
* The partial errors such as sierp instead of arrray etc indicate that we need to train on a larger amount of data for the model to better learn how to follow instructions and not make these kinds of mistakes.
