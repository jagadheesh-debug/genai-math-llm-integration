## Integration of Currency Exchange with a Chat Completion System using LLM Function Calling

### AIM:
To design and implement a Python function for retrieving the exchange rate of a currency and integrate it with a Chat Completion System using the Function Calling feature of a Large Language Model (LLM).

### PROBLEM STATEMENT:
Develop a Python application that uses the Function Calling capability of an LLM to identify a user's request for a currency exchange rate. The LLM should automatically invoke a predefined Python function that returns the exchange rate of the requested currency in JSON format. This demonstrates how LLMs can interact with external functions to provide structured and reliable information.

### DESIGN STEPS:

#### STEP 1:
Import the required Python libraries (openai, json, os, and dotenv) and configure the OpenAI API key.

#### STEP 2:
Create a Python function get_exchange_rate(currency) that stores sample exchange rates in a dictionary and returns the corresponding exchange rate in JSON format.

#### STEP 3:
Define the function schema, send the user's query to the Chat Completion API, allow the LLM to invoke the appropriate function, parse the function arguments, execute the Python function, and display the JSON response.

### PROGRAM:
```
Name : P PARTHIBAN
Register number : 212223230145
```
```python
import os
import openai

from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv()) 
openai.api_key = os.environ['OPENAI_API_KEY']
```
```python
import json

def get_exchange_rate(currency):
    """Get the exchange rate of a currency to INR"""

    exchange_rates = {
        "USD": 87.50,
        "EUR": 102.30,
        "GBP": 118.40,
        "JPY": 0.59
    }

    result = {
        "currency": currency,
        "exchange_rate": exchange_rates.get(currency, "Not Available"),
        "base_currency": "INR"
    }

    return json.dumps(result)
```
```python
functions = [
    {
        "name": "get_exchange_rate",
        "description": "Get the current exchange rate of a currency to INR.",
        "parameters": {
            "type": "object",
            "properties": {
                "currency": {
                    "type": "string",
                    "description": "Currency code (e.g., USD, EUR, GBP, JPY)"
                }
            },
            "required": ["currency"]
        }
    }
]
```
```python
messages = [
    {
        "role": "user",
        "content": "What is the exchange rate of USD?"
    }
]
```
```python
import openai
```
```python
response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=messages,
    functions=functions
)
```
```python
print(response)
```
```python
response_message = response["choices"][0]["message"]
```
```python
response_message
```
```python
response_message["content"]
```
```python
response_message["function_call"]
```
```python
json.loads(response_message["function_call"]["arguments"])
```
```python
args = json.loads(response_message["function_call"]["arguments"])
```
```python
function_response = get_exchange_rate(**args)
print(function_response)
```
### OUTPUT:

#### OpenAI API Response
<img width="1005" height="691" alt="GENAI1" src="https://github.com/user-attachments/assets/91894fd6-897e-43cb-a0f3-66a4923350dc" />

#### Assistant Message with Function Call
<img width="650" height="177" alt="GENAI2" src="https://github.com/user-attachments/assets/b42459b3-8916-4d60-a50c-4371be39726d" />

#### Extracted Function Call Details
<img width="573" height="71" alt="GENAI3" src="https://github.com/user-attachments/assets/861d3822-ab9d-4aff-9a14-8263dd95be4c" />

#### Function Response (JSON Output)
<img width="751" height="44" alt="GENAI4" src="https://github.com/user-attachments/assets/a1a5c387-88d0-4a6b-a3bb-1929dcca61dd" />

### RESULT:
The currency exchange function was successfully integrated with the Chat Completion System using the Function Calling feature of an LLM. The model correctly identified the required function, passed the appropriate parameter, executed the Python function, and returned the exchange rate as a structured JSON response. 
