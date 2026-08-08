---
category: general
date: 2026-04-25
description: 使用清晰的 foreach 循环示例快速遍历 C# 集合。学习如何获取对象名称并在几步内显示字符串列表。
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: zh
og_description: 使用 foreach 循环示例遍历 C# 集合。了解如何获取对象名称并高效显示字符串列表。
og_title: 遍历集合 C# – 逐步循环遍历项目
tags:
- C#
- collections
- loops
title: 遍历集合 C# – 循环遍历项目的简明指南
url: /zh/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 遍历集合 C# – 使用 foreach 循环示例进行项目循环

Ever needed to **iterate collection C#** but weren’t sure which construct gives you the cleanest code? You’re not alone. In many projects we end up writing verbose `for` loops just to print a few strings—wasting time and readability. The good news? A single `foreach` loop can pull out every name from an object and **display string list** in seconds.

In this tutorial we’ll walk through a complete, runnable example that shows how to **get object names**, loop over items, and output them to the console. By the end you’ll have a self‑contained snippet you can drop into any .NET 6+ console app, plus a handful of tips for edge cases and performance.

> **Pro tip:** If you’re working with large collections, consider using `Parallel.ForEach`—but that’s a topic for another day.

---

## 您将学到的内容

- 如何从对象中检索名称集合（示例中的 `GetSignatureNames`）
- C# 中 **foreach loop example** 的语法和细节
- 在控制台中 **display string list** 的多种方式，包括格式技巧
- 循环项目时的常见陷阱（空集合、结果为空）
- 一个完整的、可直接复制粘贴运行的程序

无需任何外部库；只需 .NET 自带的基础类库。如果已经安装了 .NET SDK，立即开始即可。

---

![遍历集合 C# 示例图，展示列表流入 foreach 循环再输出到控制台](/images/iterate-collection-csharp.png "遍历集合 C# 示例图")

---

## 第 1 步：设置示例对象

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

## 第 2 步：编写 Foreach 循环以显示字符串列表

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

## 第 3 步：运行程序并验证输出

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

## 第 4 步：常见变体与边缘情况

### 4.1 循环遍历复杂对象列表

Often you won’t be dealing with plain strings but with objects that contain multiple properties. In that case you can still **loop over items** and decide what to display:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Here we use string interpolation to combine fields—still a `foreach` loop, just a richer output.

### 4.2 使用 `break` 提前退出

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

### 4.3 并行枚举（高级）

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

## 第 5 步：保持循环简洁可维护的技巧

- **Prefer `foreach` over `for`** when you don’t need an index; it reduces off‑by‑one bugs.
- **Use `IEnumerable<T>`** in method signatures to keep APIs flexible.
- **Guard against null** collections with the null‑coalescing operator (`??`).
- **Keep the loop body small**—if you find yourself writing many lines, extract a method.
- **Avoid modifying the collection** while iterating; it throws an `InvalidOperationException`.

---

## 结论

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