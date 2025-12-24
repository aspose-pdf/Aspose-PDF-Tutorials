---
category: general
date: 2025-12-23
description: Create chat completion request in C# using Aspose.Pdf.AI LlamaClient.
  Learn how to build the request, send it with async await, and read the assistant's
  reply – complete runnable example included.
draft: false
keywords:
- create chat completion request
- Llama client
- Aspose PDF AI
- async await
- ChatMessage
- C# AI integration
language: en
og_description: Create chat completion request in C# using Aspose.Pdf.AI LlamaClient.
  This tutorial shows the full async workflow, from client init to reading the assistant's
  reply.
og_title: Create chat completion request with Aspose.Pdf.AI – C# Guide
tags:
- C#
- AI
- Aspose
- Llama
title: Create chat completion request with Aspose.Pdf.AI LlamaClient in C# – Step‑by‑Step
  Guide
url: /net/advanced-features/create-chat-completion-request-with-aspose-pdf-ai-llamaclien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create chat completion request with Aspose.Pdf.AI LlamaClient in C#

Ever needed to **create chat completion request** from your .NET app but weren’t sure which classes to touch? You’re not the only one. Many developers hit the wall when they first play with Llama‑based services—especially when the SDK hides the plumbing behind a few fluent methods.  

In this guide we’ll walk you through the entire process of building a **create chat completion request** using the **Aspose.Pdf.AI** LlamaClient, sending it asynchronously, and extracting the assistant’s reply. By the end you’ll have a self‑contained, copy‑paste‑ready snippet that works out of the box.

> **Pro tip:** If you already have an Aspose subscription, you can reuse the same API key for both PDF manipulation and AI calls—no extra credentials needed.

## What You’ll Need

- **.NET 6** or later (the SDK targets .NET Standard 2.0, so it works on .NET Core, .NET Framework, and Xamarin)
- An **Aspose.Pdf.AI** license or a free trial API key (you’ll paste it into the code)
- Visual Studio 2022 (or any editor you prefer)
- Basic familiarity with **async await** in C# (we’ll cover the essentials)

If any of those sound unfamiliar, don’t panic—each requirement is explained as we go, and the code is heavily commented.

![Create chat completion request diagram](image.png){:alt="Diagram showing the flow of a create chat completion request using Aspose.Pdf.AI LlamaClient"}

## Step 1: Install the Aspose.Pdf.AI NuGet package and create chat completion request

Open your terminal (or Package Manager Console) and run:

```bash
dotnet add package Aspose.Pdf.AI
```

The package contains the `LlamaClient`, request/response models, and helper methods for chat interactions. After the install, you’re ready to **create chat completion request** objects.

## Step 2: Initialise the Llama client (the heart of the Llama client)

Creating a client is a one‑time operation per application lifetime. The fluent builder pattern lets you inject the API key, set a timeout, and even enable logging.

```csharp
// Initialise a singleton LlamaClient with your API key
using var llamaClient = Aspose.Pdf.AI.LlamaClient
    .CreateWithApiKey("YOUR_API_KEY")   // <-- replace with your real key
    .WithTimeout(TimeSpan.FromSeconds(30))
    .EnableLogging()                    // optional, but useful for debugging
    .Build();
```

> **Why this step matters:** The client handles HTTP pooling, retries, and JSON (de)serialization. By reusing a single instance you avoid socket exhaustion and get better performance.

## Step 3: Build the **create chat completion request** payload

The request is a simple POCO that holds a list of `ChatMessage` objects. Each message has a role (`system`, `user`, `assistant`) and content. For a basic “Hello!” exchange we only need a single user message.

```csharp
// Construct the request object that will be sent to the Llama service
var chatRequest = new Aspose.Pdf.AI.LlamaChatCompletionRequest
{
    // The Messages collection defines the conversation history.
    Messages = new List<Aspose.Pdf.AI.ChatMessage>
    {
        // Use the helper to create a user‑originated message.
        Aspose.Pdf.AI.ChatMessage.FromUser("Hello!")
    }
};
```

> **Tip:** If you need system‑level instructions (e.g., “You are a helpful PDF assistant”), prepend a `ChatMessage.FromSystem("…")` entry. This influences the model’s tone.

## Step 4: Send the request asynchronously and await the response

Network calls are inherently I/O‑bound, so we use `await` to keep the thread free. The SDK returns a `LlamaChatCompletionResult` that mirrors the OpenAI response schema.

```csharp
// Send the request and await the result.
// This call is fully async – it won’t block the UI thread in a desktop app.
var completionResult = await llamaClient.CreateCompletionAsync(chatRequest);
```

> **Why async await?** It prevents thread‑pool starvation, especially when you scale to dozens of concurrent users. The `async` keyword also signals to readers that the operation involves I/O.

## Step 5: Extract the assistant’s reply from the result

The response contains a `Choices` array; each choice holds a `Message` with `Content`. For a single‑choice request we just read the first element.

```csharp
// The assistant’s reply is stored in the first choice.
string assistantReply = completionResult.Choices[0].Message.Content;

// Output the reply to the console – you could also bind it to UI, log it, etc.
Console.WriteLine("Assistant says: " + assistantReply);
```

**Expected output**

```
Assistant says: Hello! How can I help you with your PDF needs today?
```

If you get a different answer, that’s fine—Llama models are stochastic. You can control randomness via the `Temperature` property on the request object (default is 0.7).

## Step 6: Full, runnable example (copy‑paste ready)

Below is the complete program that you can drop into a console app’s `Program.cs`. No other files are required.

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Aspose.Pdf.AI;

class Program
{
    static async Task Main(string[] args)
    {
        // 1️⃣ Initialise the Llama client with your API key.
        using var llamaClient = LlamaClient
            .CreateWithApiKey("YOUR_API_KEY")   // <-- insert your key here
            .WithTimeout(TimeSpan.FromSeconds(30))
            .EnableLogging()                    // optional
            .Build();

        // 2️⃣ Build the chat completion request (the “create chat completion request” payload).
        var chatRequest = new LlamaChatCompletionRequest
        {
            Messages = new List<ChatMessage>
            {
                // User says “Hello!”
                ChatMessage.FromUser("Hello!")
            }
        };

        // 3️⃣ Send the request asynchronously.
        LlamaChatCompletionResult completionResult = await llamaClient.CreateCompletionAsync(chatRequest);

        // 4️⃣ Retrieve and display the assistant’s reply.
        string assistantReply = completionResult.Choices[0].Message.Content;
        Console.WriteLine("Assistant says: " + assistantReply);
    }
}
```

### Running the code

1. Open a terminal in the project folder.  
2. Execute `dotnet run`.  
3. You should see the assistant’s greeting printed to the console.

If you encounter a `401 Unauthorized`, double‑check that the API key is active and not expired.

## Common Variations & Edge Cases

| Scenario | How to adapt the code |
|----------|-----------------------|
| **Multiple turns** (conversation history) | Append additional `ChatMessage.FromUser` or `ChatMessage.FromAssistant` objects to `Messages`. |
| **Changing model behavior** | Set `chatRequest.Temperature = 0.2` for deterministic answers, or `chatRequest.MaxTokens = 150` to limit length. |
| **Using a system prompt** | Insert `ChatMessage.FromSystem("You are a PDF extraction specialist.")` as the first element. |
| **Handling errors** | Wrap the `CreateCompletionAsync` call in a try/catch and inspect `LlamaException` for status codes. |
| **Streaming responses** | The SDK also offers `CreateCompletionStreamingAsync`; replace the method if you need partial replies. |

## Tips for Production‑Ready **Llama client** Integration

- **Reuse the client**: Create it once at app start (e.g., in `Program.cs` or a DI container) and inject it where needed.  
- **Secure the API key**: Store it in Azure Key Vault, AWS Secrets Manager, or environment variables—never hard‑code it in source control.  
- **Log responsibly**: Enable logging in non‑production builds only; avoid dumping full request payloads that may contain sensitive data.  
- **Throttle calls**: Respect Aspose’s rate limits (usually 20 RPS). Implement a semaphore or Polly retry policy if you anticipate bursts.  

## Conclusion

We’ve just **created a chat completion request** from scratch, sent it with **async await**, and printed the assistant’s response—all using the **Aspose.Pdf.AI LlamaClient** in C#. The tutorial covered initialization, payload construction, asynchronous execution, and practical error‑handling tips.  

Now you can extend this pattern to more sophisticated PDF‑related queries, feed the model PDF text extracted via Aspose, or even build a full‑blown chatbot that assists users in generating or editing documents on the fly.

**Next steps** you might explore:

- Adding **system prompts** to steer the model toward PDF‑specific advice.  
- Integrating **Aspose.Pdf.AI’s document analysis** APIs and feeding the results into the chat.  
- Using **streaming completions** for real‑time UI updates.  

Feel free to experiment, and don’t hesitate to drop a comment if something feels fuzzy. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}