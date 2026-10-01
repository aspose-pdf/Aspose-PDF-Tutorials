---
category: general
date: 2026-04-25
description: تكرار مجموعة في C# بسرعة باستخدام مثال واضح لحلقة foreach. تعلم كيفية
  الحصول على أسماء الكائنات وعرض قائمة السلاسل في بضع خطوات فقط.
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: ar
og_description: تكرار مجموعة في C# باستخدام مثال حلقة foreach. اكتشف كيفية الحصول
  على أسماء الكائنات وعرض قائمة السلاسل النصية بكفاءة.
og_title: تكرار مجموعة C# – حلقة خطوة بخطوة عبر العناصر
tags:
- C#
- collections
- loops
title: تكرار مجموعة C# – دليل بسيط للمرور عبر العناصر
url: /ar/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Iterate Collection C# – How to Loop Over Items with a Foreach Loop Example

هل احتجت يوماً إلى **iterate collection C#** لكن لم تكن متأكدًا أي بنية تمنحك أنظف كود؟ لست وحدك. في كثير من المشاريع ننتهي بكتابة حلقات `for` مطولة فقط لطباعة بعض السلاسل—مما يضيع الوقت ويقلل من قابلية القراءة. الخبر السار؟ حلقة `foreach` واحدة يمكنها استخراج كل اسم من كائن وعرض **display string list** في ثوانٍ.

في هذا الدرس سنستعرض مثالًا كاملاً قابلاً للتنفيذ يوضح كيفية **get object names**، التكرار على العناصر، وإخراجها إلى وحدة التحكم. بنهاية الدرس ستحصل على مقتطف مستقل يمكنك إدراجه في أي تطبيق .NET 6+ Console، بالإضافة إلى مجموعة من النصائح للحالات الخاصة والأداء.

> **نصيحة احترافية:** إذا كنت تتعامل مع مجموعات كبيرة، فكر في استخدام `Parallel.ForEach`—لكن هذا موضوع ليوم آخر.

---

## What You’ll Learn

- كيفية استرجاع مجموعة من الأسماء من كائن (`GetSignatureNames` في مثالنا)
- الصياغة والفروق الدقيقة في **foreach loop example** في C#
- طرق **display string list** في وحدة التحكم، بما في ذلك حيل التنسيق
- الأخطاء الشائعة عند التكرار على العناصر (مجموعات `null`، نتائج فارغة)
- برنامج كامل جاهز للنسخ واللصق يمكنك تشغيله فورًا

لا تحتاج إلى مكتبات خارجية؛ فقط مكتبة الفئة الأساسية التي تأتي مع .NET. إذا كان لديك .NET SDK مثبتًا، فأنت جاهز للانطلاق.

---

![مخطط Iterate collection C# يُظهر قائمة تتدفق إلى حلقة foreach ثم إلى وحدة التحكم](/images/iterate-collection-csharp.png "مخطط iterate collection c#")

---

## Step 1: Set Up the Sample Object

أولاً وقبل كل شيء—نحتاج إلى كائن يمكنه إرجاع مجموعة من الأسماء. تخيل أن لديك فئة `Signature` تحتوي على عدة توقيعات؛ كل توقيع له خاصية `Name`. الطريقة `GetSignatureNames` تستخرج هذه الأسماء إلى `IEnumerable<string>`.

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

**لماذا هذا مهم:** بإرجاع `IEnumerable<string>` نحافظ على مرونة الطريقة—يمكن للمتصلين تعداد النتيجة، أو استعلامها، أو تحويلها دون نسخ القائمة الأساسية. كما يسهل ذلك **loop over items** لاحقًا.

---

## Step 2: Write the Foreach Loop to Display the String List

الآن بعد أن أصبح لدينا مصدر للأسماء، لنقم فعليًا **iterate collection C#**. بنية `foreach` تسحب كل عنصر من القابل للتعداد تلقائيًا، لذا لا نحتاج إلى إدارة متغيّر فهرس.

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

**شرح الكود:**

1. **Instantiate** `Signature` – الآن لديك كائن يعرف أسمائه الخاصة.
2. **Retrieve** the collection via `GetSignatureNames()` – هذه هي خطوة **get object names**.
3. **Foreach loop example** – `foreach (var name in signatureNames)` يتكرر تلقائيًا على كل سلسلة.
4. **Display** each `name` with `Console.WriteLine` – الطريقة الكلاسيكية لـ **display string list** في تطبيق Console.

نظرًا لأن `signatureNames` يطبق `IEnumerable<string>`، فإن حلقة `foreach` تعمل مباشرةً، متعاملًا مع المُعدِّد خلف الكواليس. لا داعي للقلق بشأن أخطاء الفهرسة أو فحص الحدود يدويًا.

---

## Step 3: Run the Program and Verify Output

قم بترجمة البرنامج وتنفيذه (مثلاً `dotnet run` من مجلد المشروع). يجب أن ترى:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

إذا لم يُطبع شيء، تحقق من أن `GetSignatureNames` لا تُعيد `null`. يمكن لحارس دفاعي سريع أن يوفر عليك المتاعب:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

الآن سيتعامل الحلقة بأناقة مع مجموعة مفقودة وتُظهر لا شيء بدلاً من رمي `NullReferenceException`.

---

## Step 4: Common Variations & Edge Cases

### 4.1 Looping Over a List of Complex Objects

غالبًا ما لن تتعامل مع سلاسل نصية بسيطة بل مع كائنات تحتوي على عدة خصائص. في هذه الحالة لا يزال بإمكانك **loop over items** وتقرر ما الذي ستعرضه:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

هنا نستخدم الاستبدال داخل السلسلة لدمج الحقول—ما زالت حلقة `foreach`، لكن الناتج أغنى.

### 4.2 Early Exit with `break`

إذا كنت تحتاج فقط إلى الاسم الأول المطابق، يمكنك الخروج من الحلقة باستخدام `break`:

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

عندما تكون المجموعة ضخمة وكل تكرار يستهلك موارد المعالج، يمكن لـ `Parallel.ForEach` تسريع العملية:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

تذكر أن `Console.WriteLine` نفسه آمن للمتعدد الخيوط لكن ترتيب الإخراج سيكون غير محدد.

---

## Step 5: Tips for Clean and Maintainable Loops

- **Prefer `foreach` over `for`** عندما لا تحتاج إلى فهرس؛ يقلل ذلك من أخطاء الفهرسة.
- **Use `IEnumerable<T>`** في توقيعات الطرق للحفاظ على مرونة الـ APIs.
- **Guard against null** باستخدام عامل الدمج الصفري (`??`).
- **Keep the loop body small**—إذا وجدت نفسك تكتب عدة أسطر، استخرجها إلى طريقة منفصلة.
- **Avoid modifying the collection** أثناء التكرار؛ سيؤدي ذلك إلى رمي `InvalidOperationException`.

---

## Conclusion

لقد عرضنا للتو كيفية **iterate collection C#** باستخدام مثال **foreach loop example** نظيف، استرجاع **object names**، و**display string list** في وحدة التحكم. البرنامج الكامل—تعريف الكائن، الاسترجاع، والتكرار—يعمل كما هو، مما يمنحك أساسًا قويًا لأي سيناريو تحتاج فيه إلى التكرار على العناصر.

من هنا يمكنك استكشاف:

- الترشيح باستخدام LINQ قبل التكرار (`signatureNames.Where(n => n.Contains("a"))`)
- كتابة الناتج إلى ملف بدلاً من وحدة التحكم
- استخدام `IAsyncEnumerable<T>` للتيارات غير المتزامنة

جرّب ذلك، وسترى مدى مرونة بنية `foreach`. لديك أسئلة حول الحالات الخاصة أو الأداء؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}