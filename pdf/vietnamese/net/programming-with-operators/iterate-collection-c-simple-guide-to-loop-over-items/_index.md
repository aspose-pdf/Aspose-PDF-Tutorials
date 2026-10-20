---
category: general
date: 2026-04-25
description: Lặp qua collection trong C# nhanh chóng với ví dụ vòng foreach rõ ràng.
  Học cách lấy tên đối tượng và hiển thị danh sách chuỗi chỉ trong vài bước.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: vi
og_description: Lặp qua collection trong C# bằng ví dụ vòng foreach. Khám phá cách
  lấy tên đối tượng và hiển thị danh sách chuỗi một cách hiệu quả.
og_title: Duyệt bộ sưu tập C# – Vòng lặp từng bước qua các mục
tags:
- C#
- collections
- loops
title: Lặp qua Bộ sưu tập C# – Hướng dẫn đơn giản để duyệt các mục
url: /vi/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Iterate Collection C# – Cách Duyệt Các Mục Bằng Vòng Lặp Foreach

Ever needed to **iterate collection C#** but weren’t sure which construct gives you the cleanest code? You’re not alone. In many projects we end up writing verbose `for` loops just to print a few strings—wasting time and readability. The good news? A single `foreach` loop can pull out every name from an object and **display string list** in seconds.

In this tutorial we’ll walk through a complete, runnable example that shows how to **get object names**, loop over items, and output them to the console. By the end you’ll have a self‑contained snippet you can drop into any .NET 6+ console app, plus a handful of tips for edge cases and performance.

> **Pro tip:** If you’re working with large collections, consider using `Parallel.ForEach`—but that’s a topic for another day.

---

## Những Điều Bạn Sẽ Học

- Cách lấy một collection các tên từ một đối tượng (`GetSignatureNames` trong ví dụ của chúng tôi)
- Cú pháp và các chi tiết tinh tế của một **foreach loop example** trong C#
- Các cách để **display string list** trong console, bao gồm các mẹo định dạng
- Những bẫy thường gặp khi lặp qua các mục (collection null, kết quả rỗng)
- Một chương trình đầy đủ, sẵn sàng copy‑paste mà bạn có thể chạy ngay lập tức

No external libraries are required; just the base class library that ships with .NET. If you’ve got the .NET SDK installed, you’re good to go.

![Iterate collection C# diagram showing a list flowing into a foreach loop and then to the console](/images/iterate-collection-csharp.png "iterate collection c# diagram")

---

## Bước 1: Thiết Lập Đối Tượng Mẫu

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

**Tại sao điều này quan trọng:** By returning `IEnumerable<string>` we keep the method flexible—callers can enumerate, query, or convert the result without copying the underlying list. It also makes it easy to **loop over items** later.

---

## Bước 2: Viết Vòng Lặp Foreach Để Hiển Thị Danh Sách Chuỗi

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

**Giải thích mã:**

1. **Instantiate** `Signature` – bây giờ bạn có một đối tượng biết các tên của nó.
2. **Retrieve** collection qua `GetSignatureNames()` – đây là bước **get object names**.
3. **Foreach loop example** – `foreach (var name in signatureNames)` tự động lặp qua mỗi chuỗi.
4. **Display** mỗi `name` bằng `Console.WriteLine` – cách cổ điển để **display string list** trong một ứng dụng console.

Because `signatureNames` implements `IEnumerable<string>`, the `foreach` loop works out of the box, handling the enumerator behind the scenes. No need to worry about off‑by‑one errors or manual bounds checking.

---

## Bước 3: Chạy Chương Trình và Xác Nhận Kết Quả

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

## Bước 4: Các Biến Thể Thông Thường & Trường Hợp Đặc Biệt

### 4.1 Lặp Qua Danh Sách Các Đối Tượng Phức Tạp

Often you won’t be dealing with plain strings but with objects that contain multiple properties. In that case you can still **loop over items** and decide what to display:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

Here we use string interpolation to combine fields—still a `foreach` loop, just a richer output.

### 4.2 Thoát Sớm với `break`

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

### 4.3 Đếm Song Song (Nâng Cao)

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

## Bước 5: Mẹo Để Viết Vòng Lặp Sạch và Dễ Bảo Trì

- **Prefer `foreach` over `for`** khi bạn không cần chỉ mục; nó giảm lỗi off‑by‑one.
- **Use `IEnumerable<T>`** trong chữ ký phương thức để giữ API linh hoạt.
- **Guard against null** collections bằng toán tử null‑coalescing (`??`).
- **Keep the loop body small** — nếu bạn thấy mình viết nhiều dòng, hãy tách ra thành một phương thức.
- **Avoid modifying the collection** khi đang lặp; nó sẽ ném `InvalidOperationException`.

---

## Kết Luận

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