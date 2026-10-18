---
category: general
date: 2026-04-25
description: C# でコレクションを素早く反復処理する、分かりやすい foreach ループの例。オブジェクト名の取得方法と文字列リストの表示を数ステップで学びましょう。
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: ja
og_description: C# の foreach ループでコレクションを反復し、オブジェクト名を取得して文字列リストを効率的に表示する方法を紹介します。
og_title: C#でコレクションを反復 – アイテムをステップバイステップでループ
tags:
- C#
- collections
- loops
title: C# コレクションの反復 – アイテムをループするシンプルガイド
url: /ja/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Iterate Collection C# – How to Loop Over Items with a Foreach Loop Example

コレクションを **iterate collection C#** したいけど、どの構文が最もすっきりしたコードになるか迷ったことはありませんか？ 多くのプロジェクトで、数行の文字列を出力するだけなのに冗長な `for` ループを書いてしまい、時間と可読性を犠牲にしています。 良いニュースは、たった一つの `foreach` ループでオブジェクトからすべての名前を取り出し、 **display string list** を瞬時に実現できることです。

このチュートリアルでは、**オブジェクト名を取得**し、アイテムをループし、コンソールに出力する完全な実行可能サンプルを順を追って解説します。 最後まで読めば、.NET 6+ のコンソールアプリにそのまま貼り付けられる自己完結型スニペットと、エッジケースやパフォーマンスに関するいくつかのヒントが手に入ります。

> **Pro tip:** 大規模なコレクションを扱う場合は `Parallel.ForEach` の使用を検討してください — ただしこれは別のトピックです。

---

## What You’ll Learn

- サンプル内の `GetSignatureNames` を使ってオブジェクトから名前のコレクションを取得する方法
- C# における **foreach loop example** の構文と細かなポイント
- コンソールで **display string list** する方法（フォーマットのコツを含む）
- ループ時の一般的な落とし穴（null コレクション、空結果など）
- すぐに実行できる、コピー＆ペースト可能なフルプログラム

外部ライブラリは不要です。 .NET に同梱されている Base Class Library だけで動作します。 .NET SDK がインストールされていればすぐに始められます。

---

![Iterate collection C# diagram showing a list flowing into a foreach loop and then to the console](/images/iterate-collection-csharp.png "iterate collection c# diagram")

---

## Step 1: Set Up the Sample Object

まずは、名前のコレクションを返すオブジェクトを用意します。 `Signature` クラスが複数の署名を保持し、各署名が `Name` プロパティを持っていると想定してください。 メソッド `GetSignatureNames` はそれらの名前を `IEnumerable<string>` に抽出します。

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

**Why this matters:** `IEnumerable<string>` を返すことでメソッドの柔軟性が保たれます。 呼び出し側は列挙したり、クエリしたり、結果をコピーせずに変換したりできます。 後で **loop over items** する際にも扱いやすくなります。

---

## Step 2: Write the Foreach Loop to Display the String List

名前のソースができたので、実際に **iterate collection C#** してみましょう。 `foreach` 構文は列挙可能オブジェクトから自動的に要素を取り出すので、インデックス変数を管理する必要がありません。

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

1. **Instantiate** `Signature` – これで自分の名前を保持しているオブジェクトが手に入ります。  
2. **Retrieve** the collection via `GetSignatureNames()` – これが **get object names** のステップです。  
3. **Foreach loop example** – `foreach (var name in signatureNames)` が各文字列を自動的に走査します。  
4. **Display** each `name` with `Console.WriteLine` – コンソールアプリで **display string list** する古典的な方法です。

`signatureNames` が `IEnumerable<string>` を実装しているため、`foreach` ループは内部で列挙子を自動的に処理し、オフバイワンエラーや手動の境界チェックを心配する必要がありません。

---

## Step 3: Run the Program and Verify Output

プログラムをコンパイルして実行します（例: プロジェクトフォルダーで `dotnet run`）。 以下のように表示されるはずです：

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

何も出力されない場合は、`GetSignatureNames` が `null` を返していないか確認してください。 簡単な防御的ガードを入れるだけで頭痛の種を防げます：

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

これでコレクションが存在しない場合でもループは安全にスキップし、`NullReferenceException` を投げません。

---

## Step 4: Common Variations & Edge Cases

### 4.1 Looping Over a List of Complex Objects

単なる文字列ではなく、複数のプロパティを持つオブジェクトを扱うことも多いでしょう。その場合でも **loop over items** でき、表示内容を選択できます：

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

ここでは文字列補間を使って複数フィールドを結合しています。 依然として `foreach` ループですが、出力がリッチになります。

### 4.2 Early Exit with `break`

最初にマッチした名前だけが欲しい場合は、ループから抜け出します：

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

コレクションが非常に大きく、各イテレーションが CPU 集中型の場合は `Parallel.ForEach` で高速化できます：

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

`Console.WriteLine` 自体はスレッドセーフですが、出力順序は非決定的になることに注意してください。

---

## Step 5: Tips for Clean and Maintainable Loops

- **Prefer `foreach` over `for`** when you don’t need an index; it reduces off‑by‑one bugs.  
- **Use `IEnumerable<T>`** in method signatures to keep APIs flexible.  
- **Guard against null** collections with the null‑coalescing operator (`??`).  
- **Keep the loop body small**—if you find yourself writing many lines, extract a method.  
- **Avoid modifying the collection** while iterating; it throws an `InvalidOperationException`.

---

## Conclusion

今回の例では、**iterate collection C#** をクリーンな **foreach loop example** で実装し、**object names** を取得し、コンソールに **display string list** する方法を示しました。 オブジェクト定義、取得、イテレーションをすべて含む完全なプログラムはそのまま動作し、アイテムをループするあらゆるシナリオの土台となります。

ここからさらに踏み込むなら：

- ループ前に LINQ でフィルタリング (`signatureNames.Where(n => n.Contains("a"))`)  
- コンソールではなくファイルへ出力  
- 非同期ストリーム用に `IAsyncEnumerable<T>` を使用  

ぜひ試してみてください。 エッジケースやパフォーマンスに関する質問があれば下のコメントで教えてください。 Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}