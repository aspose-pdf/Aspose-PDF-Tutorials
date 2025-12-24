---
category: general
date: 2025-12-23
description: Get AI response instantly in C# by learning how to send chat message,
  await async completion, and create AI chat client. Follow this step‑by‑step tutorial
  for a working solution.
draft: false
keywords:
- get ai response
- send chat message
- await async completion
- create ai chat client
- initialize client with api key
language: en
og_description: Get AI response in C# by sending a chat message, awaiting async completion,
  and creating an AI chat client with an API key. Learn the full workflow now.
og_title: Get AI Response in C# – Step‑by‑Step Guide
tags:
- C#
- Aspose.Pdf.AI
- AI Chat
- Async Programming
title: Get AI Response in C# – Complete Guide to Send Chat Message with Aspose.Pdf.AI
url: /net/advanced-features/get-ai-response-in-c-complete-guide-to-send-chat-message-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Get AI Response in C# – Complete Guide to Send Chat Message with Aspose.Pdf.AI

Ever wondered how to **get AI response** from a language model without writing a massive amount of boiler‑plate code? You're not alone. Many developers hit a wall when they try to *send chat message* to a remote AI service and then wait for the answer. In this tutorial we’ll walk through the entire process—right from **initialize client with API key** to extracting the reply—so you can *await async completion* and finally **get AI response** in a clean, production‑ready way.

We'll be using Aspose.Pdf.AI's Llama endpoint, but the pattern applies to any modern chat‑completion API. By the end of this guide you’ll have a self‑contained, runnable program that **gets AI response** in just a few lines of C#. No fluff, just solid code you can copy‑paste.

## Prerequisites

Before we dive in, make sure you have:

* .NET 6.0 or later (the code uses `async`/`await` which is fully supported)
* An Aspose.Pdf.AI account with a valid API key
* Visual Studio 2022, VS Code, or any IDE you prefer
* The `Aspose.Pdf.AI` NuGet package installed (`dotnet add package Aspose.Pdf.AI`)

If any of those sound unfamiliar, don’t panic—installing the NuGet package is as easy as running one CLI command, and getting an API key is just a few clicks in the Aspose portal.

![Diagram illustrating how to get AI response using Aspose.Pdf.AI client](image-get-ai-response.png)

## Overview of the Workflow

At a high level the steps to **get AI response** are:

1. **Initialize client with API key** – creates a secure connection.
2. **Create AI chat client** – configures the Llama service.
3. **Send chat message** – packages user input into a request.
4. **Await async completion** – lets the .NET runtime handle the network call without blocking.
5. **Extract the reply** – pulls the assistant’s answer from the response payload.

Each of these stages will be covered in detail below, with code snippets and practical tips that reflect real‑world usage.

---

## How to Get AI Response with Aspose.Pdf.AI

### Step 1: Initialize Client with API key

The first thing you need is a properly authenticated client. Aspose.Pdf.AI provides a fluent builder that makes this a breeze.

```csharp
using Aspose.Pdf.AI;
using System;
using System.Collections.Generic;
using System.Threading.Tasks;

// Replace this placeholder with your real key – never commit it to source control!
const string ApiKey = "YOUR_ACTUAL_API_KEY";

using var client = LlamaClient
    .CreateWithApiKey(ApiKey)   // <-- initialize client with API key
    .Build();                    // builds the underlying HttpClient
```

**Why this matters:** Initializing the client once and re‑using it across multiple calls reduces connection overhead and ensures the API key is sent securely on every request. If you forget to wrap the client in a `using` statement, you might leak sockets—something I’ve seen cause nasty out‑of‑memory errors in long‑running services.

> **Pro tip:** Store the API key in an environment variable (`ASPOSE_PDF_AI_KEY`) and read it at runtime. This keeps secrets out of your repo and plays nicely with CI/CD pipelines.

### Step 2: Create AI Chat Client (Prepare the request object)

Now that the low‑level HTTP client is ready, we need to shape the request that the Llama service expects. This is where we **create AI chat client**‑style objects.

```csharp
var chatRequest = new LlamaChatCompletionRequest
{
    // The model name can be adjusted; "llama-2" is the default on Aspose.Pdf.AI.
    Model = "llama-2",

    // The Messages collection holds the conversation history.
    Messages = new List<ChatMessage>
    {
        // Here we **send chat message** from the user.
        ChatMessage.FromUser("Hello, AI! Can you tell me a fun fact about C#?")
    }
};
```

**Why this matters:** The `Messages` list mimics the chat history you’d see in a UI. Adding more entries (assistant replies, system prompts) can guide the model’s behavior. For a simple *get AI response* scenario, a single user message is enough, but you can extend it later for richer dialogs.

### Step 3: Send Chat Message and Await Async Completion

With the request object ready, we now **send chat message** to the remote service and **await async completion**. The `await` keyword frees the thread while the network call is in flight.

```csharp
// The method returns a LlamaChatCompletionResult asynchronously.
LlamaChatCompletionResult completionResult = await client.CreateCompletionAsync(chatRequest);
```

**Why this matters:** Using `await` prevents UI freezes in desktop apps and keeps ASP.NET request threads available for other users. If you were to call `.Result` or `.Wait()`, you’d block the thread and risk deadlocks, especially in UI contexts.

> **Common pitfall:** Forgetting the `async` keyword on the containing method leads to a compiler error. Make sure your `Main` method (or whatever entry point you use) is declared as `static async Task Main(string[] args)`.

### Step 4: Extract and Use the Reply

The response payload contains an array called `Choices`. Each choice holds a `Message` object with the assistant’s content. To **get AI response**, we simply read the first choice.

```csharp
// Guard against an empty response – a defensive check you’ll thank yourself for.
if (completionResult?.Choices?.Count > 0)
{
    string reply = completionResult.Choices[0].Message.Content;
    Console.WriteLine("🤖 AI says: " + reply);
}
else
{
    Console.WriteLine("⚠️ No response received from the AI service.");
}
```

**Why this matters:** Checking `Choices.Count` protects you from null reference exceptions if the service returns an error payload. In production you’d also inspect `completionResult.Error` for detailed diagnostics.

### Full Working Example

Putting it all together, here’s a minimal console app that **gets AI response** from Aspose.Pdf.AI:

```csharp
using Aspose.Pdf.AI;
using System;
using System.Collections.Generic;
using System.Threading.Tasks;

class Program
{
    // Keep the API key out of source control – use env var or secret manager.
    private static readonly string ApiKey = Environment.GetEnvironmentVariable("ASPOSE_PDF_AI_KEY")
                                            ?? "YOUR_FALLBACK_API_KEY";

    static async Task Main(string[] args)
    {
        // 1️⃣ Initialize client with API key
        using var client = LlamaClient
            .CreateWithApiKey(ApiKey)
            .Build();

        // 2️⃣ Build chat request (create AI chat client)
        var chatRequest = new LlamaChatCompletionRequest
        {
            Model = "llama-2",
            Messages = new List<ChatMessage>
            {
                ChatMessage.FromUser("Hello! How can I improve my async C# code?")
            }
        };

        // 3️⃣ Send chat message and await async completion
        LlamaChatCompletionResult result = await client.CreateCompletionAsync(chatRequest);

        // 4️⃣ Extract the AI response
        if (result?.Choices?.Count > 0)
        {
            string reply = result.Choices[0].Message.Content;
            Console.WriteLine($"🗨️ AI reply: {reply}");
        }
        else
        {
            Console.WriteLine("❌ Failed to get AI response.");
        }
    }
}
```

**Expected output** (may vary depending on the model’s knowledge):

```
🗨️ AI reply: To improve async code, avoid blocking calls, use ConfigureAwait(false) when you don’t need to resume on the original context, and consider using ValueTask for high‑frequency methods.
```

Run the program with `dotnet run` and you’ll see the assistant’s answer printed to the console—your first successful **get AI response**.

---

## Advanced Tips & Edge Cases

### Handling Timeouts and Retries

Network hiccups happen. Wrap the `CreateCompletionAsync` call in a retry policy (Polly is a popular library). Example:

```csharp
var retryPolicy = Policy
    .Handle<HttpRequestException>()
    .WaitAndRetryAsync(3, attempt => TimeSpan.FromSeconds(Math.Pow(2, attempt)));

LlamaChatCompletionResult result = await retryPolicy.ExecuteAsync(
    () => client.CreateCompletionAsync(chatRequest));
```

### Streaming Responses

If you need real‑time output (e.g., a chat UI), Aspose.Pdf.AI also supports streaming tokens. Switch to `CreateCompletionStreamAsync` and process each chunk as it arrives. This is beyond the scope of this basic tutorial but worth exploring for production chat bots.

### Using System Prompts

You can prepend a “system” message to shape the AI’s tone:

```csharp
Messages = new List<ChatMessage>
{
    ChatMessage.FromSystem("You are a helpful C# mentor."),
    ChatMessage.FromUser("Explain the difference between Task and ValueTask.")
}
```

### Secure Storage of API Keys

Never hard‑code secrets. In Azure, use Key Vault; in AWS, use Secrets Manager. In local dev, `.NET Secret Manager` (`dotnet user-secrets`) works nicely.

---

## Conclusion

We’ve walked through every step needed to **get AI response** in C# using Aspose.Pdf.AI: **initialize client with API key**, **create AI chat client**, **send chat message**, **await async completion**, and finally extract the reply. The complete example is ready to drop into any .NET project

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}