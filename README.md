# Design and Implementation of LangChain Expression Language (LCEL) Expressions

## AIM:
To design and implement a LangChain Expression Language (LCEL) expression that uses at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality with relevant examples of its application in real-world scenarios.

## PROBLEM STATEMENT:
The objective is to create a LangChain expression that combines a prompt, a model, and an output parser to effectively handle user input and generate meaningful outputs. The expression should leverage LangChain's capabilities to create a structured and reusable flow for transforming data based on a prompt and processing it with a model (e.g., LLM or any other model).

## DESIGN STEPS:

### STEP 1: Identify the Components
- **Prompt**: A well-structured prompt that defines the kind of output expected from the model. It should include dynamic parameters that allow it to handle various inputs.
- **Model**: An LLM or any model capable of processing the input defined by the prompt. This could be OpenAI's GPT models or others integrated into LangChain.
- **Output Parser**: A function or method that parses the output of the model to extract relevant information, ensuring that the output is in the required format.

### STEP 2: Set Up LangChain
Install LangChain if not installed yet:

```bash
pip install langchain openai
```

### STEP 3: Implement the Expression Using LangChain
 - Create a prompt that accepts two parameters.
 - Utilize a pre-trained LLM (e.g., OpenAI's GPT-4) to process the prompt.
 - Add an output parser to extract specific information or format the result.

## Program:
```python
import os
import openai
from langchain.chat_models import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain.schema.runnable import RunnablePassthrough  # Import this

os.environ['OPENAI_API_KEY'] = "your-api-key"

prompt = ChatPromptTemplate.from_template(
    "Tell me a short joke about {topic}"
)
output_parser = StrOutputParser()
model = ChatOpenAI(model="gpt-4")
chain = (
    {"topic": RunnablePassthrough()} 
    | prompt
    | model
    | output_parser
)

result = chain.invoke("ice cream")
print(result)

```
## OUTPUT:
![image](https://github.com/user-attachments/assets/b592897c-a26f-4bf8-b8c4-86c341c63505)

## RESULT:
Successfully, implemented a LangChain Expression Language (LCEL) expression that uses at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality with relevant examples of its application in real-world scenarios.
