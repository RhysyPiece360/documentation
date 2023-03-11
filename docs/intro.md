---
sidebar_position: 1
---

How to make a request towards our api,

Example in python
```
import requests

# Define the URL of the Flask app
url = 'http://localhost:5000/get_answer'

# Define the question to ask
question = input("")

# Make a POST request to the Flask app and get JSON response
response = requests.post(url, json={'question': question})

if response.ok:
    try:
        # Try to parse the response as JSON
        answer_json = response.json()
        # Print the answer
        print(answer_json['answer'])
    except (ValueError, KeyError):
        # Handle the error if the response is empty or not a valid JSON string
        print("Failed to get a valid answer.")
else:
    # Handle the error if the response status code is not OK
    print(f"Failed to get a valid answer. Status code: {response.status_code}")

```
this program adds the ability to type a question, passes it to our api which then in return sends the output back to you
