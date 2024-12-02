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
from langchain.prompts import PromptTemplate
from langchain.chat_models import ChatOpenAI
from langchain.output_parsers import StructuredOutputParser, ResponseSchema

# Step 1: Define Prompt Template
prompt_template = PromptTemplate(
    input_variables=["topic", "length"],
    template=(
        "You are a helpful assistant. Provide the following in valid JSON format:\n"
        "- A concise summary of {topic}.\n"
        "- The word count of the summary.\n\n"
        "Response format:\n"
        "{{\n"
        '  "summary": "Your concise summary here.",\n'
        '  "word_count": 123\n'
        "}}\n\n"
        "Write a {length}-word summary about {topic}."
    )
)

# Step 2: Define the Output Parser
response_schemas = [
    ResponseSchema(name="summary", description="A concise summary of the topic."),
    ResponseSchema(name="word_count", description="The number of words in the summary."),
]
output_parser = StructuredOutputParser.from_response_schemas(response_schemas)

# Step 3: Initialize ChatGPT-4 Model
llm = ChatOpenAI(model="gpt-4", temperature=0.3, openai_api_key="********")

# Step 4: Combine Prompt and Model
chain = prompt_template | llm | output_parser

# Step 5: Execute Chain with Examples
examples = [
    {"topic": "Climate Change", "length": "50"},
    {"topic": "Artificial Intelligence", "length": "30"},
]

for example in examples:
    try:
        result = chain.invoke(example)
        print(f"Input: {example}")
        print(f"Output: {result}\n")
    except Exception as e:
        print(f"Error for input {example}: {e}\n")


```
## OUTPUT:
![image](https://github.com/user-attachments/assets/88da4942-5c5e-43cc-a160-cdaac6d1d0f1)


## RESULT:
Successfully, implemented a LangChain Expression Language (LCEL) expression that uses at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality with relevant examples of its application in real-world scenarios.
