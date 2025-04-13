---
title: Introduction to the Anthropic API
layout: default
---

# Introduction to the Anthropic API

{: .summary-title }
> TL;DR
>
> This guide is a hands-on introduction to using the Anthropic API with Python, designed for students with no prior experience working with the Anthropic API. You'll learn how to:
- Connect to Anthropic's Claude models using Python
- Customize behavior using key parameters like temperature and max_tokens
- Structure and send chat-based prompts
- Receive and extract text responses from the model


## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Overview

Anthropic provides access to their LLMs such as Claude via a simple HTTP API and provides extensive [documentation](https://docs.anthropic.com/en/docs/welcome){:target="_blank"}. However, the documentation is not always beginner-friendly. This guide, therefore, will walk you through the process of using the API in Python to send prompts and receive completions (aka model responses) so you can get started quickly.

{: .important}
Before you can start using the API, you will need to make sure you have an API key. If you don't already have one, please follow the tutorial from the previous chapter to get your API key and set up the Colab Notebook environment. **This guide assumes that you have both ready to go.**


## Making a Simple API Call 

Anthropic API [^1] uses a straightforward design when it comes to making your first API call. The following is all you need to make an API call to Clause 3.7. Sonnet:

```python
import anthropic

client = anthropic.Anthropic(api_key=my_anthropic_key)

message = client.messages.create(
    model="claude-3-7-sonnet-20250219",
    max_tokens=300,
    temperature=1,
    system="You are a lazy poet. Respond only with poems.",
    messages=[
        {
            "role": "user",
            "content": [
                {
                    "type": "text",
                    "text": "Why is the sky blue?"
                }
            ]
        }
    ]
)
print(message.content[0].text)
```

Here is a sample response:

```
The Blue Canvas Above

Light journeys from the distant sun,
Through atmospheric veils it runs.
Scattered by molecules so small,
Blue wavelengths separate from all.

Rayleigh's law explains the hue,
Why shorter wavelengths form the blue.
While reds and yellows pass straight through,
The azure light spreads wide to view.

Nature's ceiling, vast and high,
A scattered canvas in the sky.
```

## Understanding the API Call
Now that you have made your first API call, let's dissect the code and try to understand what is really happening.

### 1. Connection to the API

```python
import anthropic

client = anthropic.Anthropic(api_key=my_anthropic_key)

# the rest of the code is omitted...
```
Before we can send prompts and receive responses, we need to establish a connection to the Anthropic API with our credentials. To this end, Anthropic provides their own official Python library, which is aptly called **anthropic** (the module we import at the top).

Once imported, we can access the different methods included in the Anthropic module. Using the **Anthropic()** method from the module, we instantiate an API client object of type Anthropic. This **client** enables us to talk to Anthropic's servers as it knows what API key to use for authentication and which version of the API to use.

To authenticate as legitimate users, you will need to pass in your **API key** using the **my_anthropic_key** variable. This way Anthropic knows that you are in fact allowed to use the API and can track your usage of the API.


### 2. Prompting the Model 

```python
# previous lines are omitted...
message = client.messages.create()
# most lines are omitted...
```
Having established the connection to the Anthropic API with the **client** object, you are ready to begin interacting with the Claude models. For this purpose, you need to send a message to the model just as you would send a text message to a friend. The Anthropic API uses the same mental model and provides a **client.messages** object, which is effectively a helper that manages sending chat messages and receiving responses.

To send a message, you first need to create it. That's why we need to use **client.messages.create()**. This method call enables us to send a chat completion request, which is a structured API call that does the following:

- Specifies a `model` to use (e.g., claude-3-7-sonnet-20250219)  
- Sets configuration parameters such as `max_tokens` and `temperature`
- Send a list of chat `messages` (including user and assistant turns)
- Receives a `completion`, which is the text response that the model returns


### 3. Setting the Parameters
```python
# previous lines are omitted...
message = client.messages.create(
    model="claude-3-7-sonnet-20250219",
    max_tokens=300,
    temperature=1,
    system="You are a lazy poet. Respond only with poems.",
    messages=[] 
    # the rest of the code is omitted...
)

```
In this guide, our focus is on understanding the API structure. However, it is also helpful to be familiar with what these configuration parameter mean:

| Parameter      | Type        | Description                                                                 |
|----------------|-------------|-----------------------------------------------------------------------------|
| `model`        | `str`       | The Claude model [^2] to use. Example: `"claude-3-7-sonnet-20250219"`               |
| `max_tokens`   | `int`       | Maximum number of tokens the model can generate in the response. Larger means longer response. A token is roughly 4 characters in English.         |
| `temperature`  | `float`     | Controls randomness in the generated response: 0 = deterministic, 1 = creative. Typical values: 0.2–0.8 |
| `system`       | `str` (optional) | A special instruction for Claude’s behavior across the conversation. Example: `"You are a lazy poet."` |
| `messages`     | `list`      | A list of message dictionaries. Each has a `role` (`user` or `assistant`) and `content`. |


### 4. Setting the Message
```python
# previous lines are omitted...
    messages=[
        {
            "role": "user",
            "content": [
                {
                    "type": "text",
                    "text": "Why is the sky blue?"
                }
            ]
        }
    ]
# the rest of the code is omitted...
```
The **messages** parameter is a list of dictionaries that represent a conversation history between the user and the Claude model. Each dictionary is a message, and it must include two keys: 
- role: identifies who is speaking ("user" or "assistant")
- content: the text of the message

Because a given human-model interaction scenario involves a dialogue between the user and the model, they will engage in turn-taking, which can be specified through the **role** key.

The **content** key holds a list of dictionaries that contain the prompt or the message that you want to send to the model in the **text** key and the type of the message in the **type** key (e.g., text, audio, image, etc.). When sending in your custom prompt, you would need to replace the value for the **text** key with your custom prompt (e.g., `"text": your_prompt_variable`).


### 5. Getting the Response
```python
# previous lines are omitted...
print(message.content[0].text)
```

The response returned from the model is stored in a **message** object. More specifically, the response is stored inside a **list** under the **message.content** attribute. Because of the way the Anthropic API is designed, the content attribute can contain different pieces of content, such as plain text ,images, and/or other structured data. Therefore, the API returns a list of blocks in the **content** attribute. Each block is a dictionary with a type and generated output, as in the following example:

```python
[
    {"type": "text", "text": "The Blue Canvas Above ..."}
]
```

To get the actual string from the **content** list, we need to grab the firs item in the list using **message.content[0]** and then access the text inside it using **message.content[0].text**. It's printed so that the string is formatted (if you directly display the returned string, the formatting will be ugly.)
 

## Wrapping Up

With that, you have successfully made your first API call to Claude! You are now ready to play with the parameters to get interesting results from Claude models. For more information about the API details, you're strongly encouraged to refer to the referenced documentation.


## References

[^1]: [Anthropic API Initial Setup](https://docs.anthropic.com/en/docs/initial-setup){:target="_blank"}

[^2]: [All models overview - Anthropic](https://docs.anthropic.com/en/docs/about-claude/models/all-models){:target="_blank"}

