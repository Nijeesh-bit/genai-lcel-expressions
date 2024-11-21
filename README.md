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
import openai
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain
from langchain.output_parsers import JsonOutputParser

# Step 1: Set OpenAI API Key
openai.api_key = 'your-openai-api-key'  # Replace with your OpenAI API key

# Step 2: Define the Prompt Template with Two Parameters
prompt_template = """
You are an expert in calculating the volume of 3D shapes. Given the radius {radius} and height {height} of a cylinder, calculate its volume.
Provide the result as a formatted string: "The volume of the cylinder is {volume} cubic units."
"""

# Step 3: Instantiate the LangChain Prompt Template
prompt = PromptTemplate(template=prompt_template, input_variables=["radius", "height"])

# Step 4: Define the Model (OpenAI GPT)
def generate_volume_output(radius: float, height: float) -> str:
    # Create a chain using the prompt and LLM
    chain = LLMChain(llm=openai.Completion, prompt=prompt)

    # Step 5: Run the model and capture the output
    volume = chain.run({"radius": radius, "height": height})
    
    return volume

# Step 6: Output Parsing - Just parsing the response as a string for now
def parse_output(output: str) -> str:
    return output.strip()

# Example Usage
radius = 5
height = 10
raw_output = generate_volume_output(radius, height)
parsed_output = parse_output(raw_output)

# Display Result
print(f"Raw Output: {raw_output}")
print(f"Parsed Output: {parsed_output}")

```
