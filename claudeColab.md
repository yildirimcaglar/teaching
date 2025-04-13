---
title: How to Set up Anthropic in Google Colab
layout: default
---

# How to Set up Anthropic in Google Colab

{: .summary-title }
> TL;DR
>
> This tutorial will walk you through how to:
- Create an Anthropic API key
- Store it securely as a secret in Google Colab
- Set up the Anthropic library in Google Colab


## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Getting an Anthropic API Key

To access Claude models, you will need to create a developer account at [Anthropic Console](https://console.anthropic.com/){:target="_blank"}.

Once logged in, you will be presented with your dashboard. To get started, click **Get API Keys**
<figure>
  <a name="fig1"></a>
  <img src="/assets/img/colab_anthropic/a1.png" alt="Step 1" width="400"/>
</figure>

This will take you to the API keys page, where you can see a list of your API keys. If you already have any API keys, they will be listed in the table. To creat a new key, simply click the **Create Key** button.
<figure>
  <a name="fig2"></a>
  <img src="/assets/img/colab_anthropic/a2.png" alt="Step 2" width="500"/>
</figure>

This will open a pop-up window where you can give a name to your key (it's customary to use one key per project). Name your key and click the **Add** button.

<figure>
  <a name="fig2"></a>
  <img src="/assets/img/colab_anthropic/a3.png" alt="Step 3" width="400"/>
</figure>

Upon creating your API key, you will be prompted to save it. Copy the key immediately and save it in a secure text file. You won’t be able to view it again!

<figure>
  <a name="fig2"></a>
  <img src="/assets/img/colab_anthropic/a4.png" alt="Step 4" width="400"/>
</figure>


{: .highlight}
> If you lose access to your key, you will need to delete it and add a new one. There is no way to restore it.

## Setting up Google Colab
Go to [Google Colab](https://colab.research.google.com/){:target="_blank"} and add a new Notebook.

It's very important that you never directly copy/paste your API key into your code files. Instead, you should store your API key separately in a secret or an external file for security and privacy. API keys are like passwords — they grant access to your account and usage quota. If you hardcode your key directly into your code (especially in shared notebooks or public repositories), anyone who sees the code could misuse your key, potentially leading to unexpected charges or data exposure. 

Using secrets in Google Colab or environment variables ensures that your sensitive credentials remain hidden and protected while keeping your code clean and safe to share. That's why, we will store our API key in a secret.

To do so, click the key icon on the left navigation menu on Colab:
>   <figure>
        <a name="fig5"></a>
        <img src="/assets/img/colab_anthropic/a5.png" alt="Step 5" width="500"/>
    </figure>

This will bring up the Secrets window. To add a new secret, click **Add new secret**:

><figure>
>        <a name="fig6"></a>
>        <img src="/assets/img/colab_anthropic/a6.png" alt="Step 6" width="500"/>
>    </figure>

Then give your secret a name, specifically `my_anthropic_key`,  and paste your copied API key into the value field. You will also need to toggle on the Notebook access option, so that you can access the key via Notebook (in the next step).
<figure>
    <a name="fig7"></a>
    <img src="/assets/img/colab_anthropic/a7.png" alt="Step 7" width="500"/>
</figure>

## Accessing a Secret Key in Notebook 
To access the secret key you just saved, copy the corresponding code from the Secrets window and paste into a new cell in your Notebook file. Here I'm saving it in `my_anthropic_key` and showing the first few characters to verify that the key is being accessed properly.

<figure>
    <a name="fig8"></a>
    <img src="/assets/img/colab_anthropic/a8.png" alt="Step 8" width="500"/>
</figure>

{: .important}
> Be sure to update the key name to be retrieved to match the same key name you entered. Also be sure to save it in the `my_anthropic_key` variable, which will be used in a subsequent guide.

## Installing Anthropic on Colab

Now that you have access to your API key. You can go ahead and start working with Claude models in Notebook. But first you will need to install the Anthropic module. Simply run the following code snippet inline:

```python
!pip install anthropic
```

This will install the module and should run without any issues on Colab.
<figure>
    <a name="fig9"></a>
    <img src="/assets/img/colab_anthropic/a9.png" alt="Step 9" width="400"/>
</figure>


With the module installed, you are ready to start interacting with Anthropic models, which will be covered in the next guide.


