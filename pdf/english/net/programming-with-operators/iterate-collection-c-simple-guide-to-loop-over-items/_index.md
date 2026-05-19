---
category: general
date: 2026-04-25
description: Iterate collection C# quickly with a clear foreach loop example. Learn
  how to get object names and display string list in just a few steps.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: en
og_description: Iterate collection C# using a foreach loop example. Discover how to
  get object names and display a string list efficiently.
og_title: Iterate Collection C# – Step‑by‑Step Loop Over Items
tags:
- C#
- collections
- loops
title: Iterate Collection C# – Simple Guide to Loop Over Items
url: /net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Iterate Collection C# – How to Loop Over Items with a Foreach Loop Example

Ever needed to **iterate collection C#** but weren’t sure which construct gives you the cleanest code? You’re not alone. In many projects we end up writing verbose `for` loops just to print a few strings—wasting time and readability. The good news? A single `foreach` loop can pull out every name from an object and **display string list** in seconds.

In this tutorial we’ll walk through a complete, runnable example that shows how to **get object names**, loop over items, and output them to the console. By the end you’ll have a self‑contained snippet you can drop into any .NET 6+ console app, plus a handful of tips for edge cases and performance.

> **Pro tip:** If you’re working with large collections, consider using `Parallel.ForEach`—but that’s a topic for another day.

---

## What You’ll Learn

- How to retrieve a collection of names from an object (`GetSignatureNames` in our sample)
- The syntax and nuances of a **foreach loop example** in C#
- Ways to **display string list** in the console, including formatting tricks
- Common pitfalls when looping over items (null collections, empty results)
- A full, copy‑paste ready program you can run instantly

No external libraries are required; just the base class library that ships with .NET. If you’ve got the .NET SDK installed, you’re good to go.

---

![Iterate collection C# diagram showing a list flowing into a foreach loop and then to the console](/images/iterate-collection-csharp.png "iterate collection c# diagram")

---

## Step 1: Set Up the Sample Object

First things first—we need an object that can return a collection of names. Imagine you have a `Signature` class that holds several signatures; each signature has a `Name` property. The method `GetSignatureNames` simply extracts those names into a `IEnumerable<string>`.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace IterateCollectionDemo
{
    // A minimal representation of the object you might be working with
    public class Signature
    {
        private readonly List<string> _names = new()
        {
            "Alice Johnson",
            "Bob Smith",
            "Charlie Davis"
        };

        // This method mimics the real‑world API that returns a collection of names
        public IEnumerable<string> GetSignatureNames()
        {
            // Using LINQ to return a read‑only IEnumerable<string>
            return _names.AsReadOnly();
        }
    }
}
```

**Why this matters:** By returning `IEnumerable<string>` we keep the method flexible—callers can enumerate, query, or convert the result without copying the underlying list. It also makes it easy to **loop over items** later.

---

## Step 2: Write the Foreach Loop to Display the String List

Now that we have a source of names, let’s actually **iterate collection C#**. The `foreach` construct automatically pulls each element from the enumerable, so we don’t have to manage an index variable.

```csharp
using System;

namespace IterateCollectionDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Instantiate the object that holds our signatures
            var signature = new Signature();

            // Step 2: Retrieve the collection of signature names from the signature object
            var signatureNames = signature.GetSignatureNames();

            // Step 3: Loop over items and output each name to the console
            foreach (var name in signatureNames)
            {
                Console.WriteLine(name);
            }

            // Keep the console window open when debugging locally
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Explanation of the code:**

1. **Instantiate** `Signature` – you now have an object that knows its own names.
2. **Retrieve** the collection via `GetSignatureNames()` – this is the **get object names** step.
3. **Foreach loop example** – `foreach (var name in signatureNames)` automatically iterates over each string.
4. **Display** each `name` with `Console.WriteLine` – the classic way to **display string list** in a console app.

Because `signatureNames` implements `IEnumerable<string>`, the `foreach` loop works out of the box, handling the enumerator behind the scenes. No need to worry about off‑by‑one errors or manual bounds checking.

---

## Step 3: Run the Program and Verify Output

Compile and execute the program (e.g., `dotnet run` from the project folder). You should see:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

If you get nothing printed, double‑check that `GetSignatureNames` isn’t returning `null`. A quick defensive guard can save you headaches:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

Now the loop will gracefully handle a missing collection and simply output nothing instead of throwing a `NullReferenceException`.

---

## Step 4: Common Variations & Edge Cases

### 4.1 Looping Over a List of Complex Objects

Often you won’t be dealing with plain strings but with objects that contain multiple properties. In that case you can still **loop over items** and decide what to display:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Here we use string interpolation to combine fields—still a `foreach` loop, just a richer output.

### 4.2 Early Exit with `break`

If you only need the first matching name, break out of the loop:

```csharp
foreach (var name in signatureNames)
{
    if (name.StartsWith("B"))
    {
        Console.WriteLine(name);
        break; // stops after the first B‑name
    }
}
```

### 4.3 Parallel Enumeration (Advanced)

When the collection is huge and each iteration is CPU‑intensive, `Parallel.ForEach` can speed things up:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

Remember, `Console.WriteLine` itself is thread‑safe but the output order will be nondeterministic.

---

## Step 5: Tips for Clean and Maintainable Loops

- **Prefer `foreach` over `for`** when you don’t need an index; it reduces off‑by‑one bugs.
- **Use `IEnumerable<T>`** in method signatures to keep APIs flexible.
- **Guard against null** collections with the null‑coalescing operator (`??`).
- **Keep the loop body small**—if you find yourself writing many lines, extract a method.
- **Avoid modifying the collection** while iterating; it throws an `InvalidOperationException`.

---

## Conclusion

We’ve just demonstrated how to **iterate collection C#** using a clean **foreach loop example**, retrieve **object names**, and **display string list** in the console. The full program—object definition, retrieval, and iteration—runs as‑is, giving you a solid foundation for any scenario where you need to loop over items.

From here you might explore:

- Filtering with LINQ before looping (`signatureNames.Where(n => n.Contains("a"))`)
- Writing the output to a file instead of the console
- Using `IAsyncEnumerable<T>` for asynchronous streams

Give those a try, and you’ll see how versatile the `foreach` construct really is. Got questions about edge cases or performance? Drop a comment below, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}