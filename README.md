Ex.No.6 Development of Python Code Compatible with Multiple AI Tools

Aim: 

Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights with Multiple AI Tools.

Explanation:

Develop a python code that integrates multiple AI tool by interacting with their APIs.
Compare outputs from different APIs.
Analyze the response and the Output.

The aim is to understand how to request help from AI tools for tasks like writing Python code, integrating with APIs, comparing outputs, and generating actionable insights.
## Explanation:

This experiment demonstrates how Python can be used to:

Connect with multiple AI APIs

Send the same input prompt to different AI tools

Collect and compare their responses

Analyze outputs and generate useful insights
## OUTPUT:
import requests


 API KEYS (Replace with your keys)

OPENAI_API_KEY = "your_openai_api_key"
HUGGINGFACE_API_KEY = "your_huggingface_api_key"


 Function to call OpenAI API

def get_openai_response(prompt):
    url = "https://api.openai.com/v1/chat/completions"
    headers = {
        "Authorization": f"Bearer {OPENAI_API_KEY}",
        "Content-Type": "application/json"
    }
    data = {
        "model": "gpt-4o-mini",
        "messages": [{"role": "user", "content": prompt}]
    }

    response = requests.post(url, headers=headers, json=data)
    return response.json()["choices"][0]["message"]["content"]

 Function to call HuggingFace API
def get_huggingface_response(prompt):
    url = "https://api-inference.huggingface.co/models/gpt2"
    headers = {
        "Authorization": f"Bearer {HUGGINGFACE_API_KEY}"
    }
    data = {"inputs": prompt}

    response = requests.post(url, headers=headers, json=data)
    return response.json()[0]["generated_text"]


Compare Responses

def compare_responses(resp1, resp2):
    print("\n--- OpenAI Response ---\n", resp1)
    print("\n--- HuggingFace Response ---\n", resp2)

    # Simple comparison logic
    len1 = len(resp1)
    len2 = len(resp2)

    if len1 > len2:
        better = "OpenAI response is more detailed."
    elif len2 > len1:
        better = "HuggingFace response is more detailed."
    else:
        better = "Both responses are similar in length."

    return better

Generate Insights

def generate_insights(resp1, resp2):
    insights = []
    
    if resp1 != resp2:
        insights.append("Responses differ in content and style.")
    if len(resp1) > len(resp2):
        insights.append("OpenAI provides more descriptive answers.")
    else:
        insights.append("HuggingFace provides concise answers.")
    
    return insights


 Main Program

if __name__ == "__main__":
    prompt = input("Enter your query: ")

    openai_resp = get_openai_response(prompt)
    hf_resp = get_huggingface_response(prompt)

    comparison = compare_responses(openai_resp, hf_resp)
    insights = generate_insights(openai_resp, hf_resp)

    print("\n--- Comparison Result ---")
    print(comparison)

    print("\n--- Insights ---")
    for i in insights:
        print("-", i)
  ## OUTPUT (SAMPLE):  
  Enter your query: What is Artificial Intelligence?

--- OpenAI Response ---
Artificial Intelligence (AI) refers to...

--- HuggingFace Response ---
Artificial intelligence is...

--- Comparison Result ---
OpenAI response is more detailed.

--- Insights ---
- Responses differ in content and style.
- OpenAI provides more descriptive answers.


Result: 

The Python program was successfully developed to:

Integrate multiple AI tools using APIs

Retrieve and compare outputs from different AI systems

Analyze responses and generate meaningful insights

This experiment demonstrates how Python can automate interactions with multiple AI platforms and assist in evaluating their performance
