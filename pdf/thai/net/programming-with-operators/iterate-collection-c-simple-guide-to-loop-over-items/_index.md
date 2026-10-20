---
category: general
date: 2026-04-25
description: วนซ้ำคอลเลกชันใน C# อย่างรวดเร็วด้วยตัวอย่างลูป foreach ที่ชัดเจน เรียนรู้วิธีดึงชื่อวัตถุและแสดงรายการสตริงในไม่กี่ขั้นตอน
draft: false
keywords:
- iterate collection c#
- loop over items
- foreach loop example
- get object names
- display string list
language: th
og_description: วนคอลเลกชันใน C# ด้วยตัวอย่างการใช้ foreach loop. ค้นหาวิธีดึงชื่อวัตถุและแสดงรายการสตริงอย่างมีประสิทธิภาพ.
og_title: วนซ้ำคอลเลกชัน C# – ขั้นตอนต่อขั้นตอนการวนลูปผ่านรายการ
tags:
- C#
- collections
- loops
title: วนซ้ำคอลเลกชัน C# – คู่มือง่ายสำหรับการวนลูปผ่านรายการ
url: /th/net/programming-with-operators/iterate-collection-c-simple-guide-to-loop-over-items/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วนซ้ำคอลเลกชัน C# – วิธีวนรายการด้วยตัวอย่างลูป foreach

เคยต้องการ **iterate collection C#** แต่ไม่แน่ใจว่าโครงสร้างใดให้โค้ดที่สะอาดที่สุด? คุณไม่ได้อยู่คนเดียว ในหลายโครงการเรามักเขียนลูป `for` ที่ยืดยาวเพียงเพื่อพิมพ์สตริงไม่กี่ตัว—เสียเวลาและทำให้อ่านยาก ข่าวดีคือ? ลูป `foreach` เพียงหนึ่งลูปสามารถดึงชื่อทุกอย่างจากอ็อบเจ็กต์และ **display string list** ได้ในไม่กี่วินาที

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งแสดงวิธี **get object names**, วนลูปรายการ, และแสดงผลออกที่คอนโซล. เมื่อจบคุณจะได้สแนปช็อตที่สามารถนำไปวางในแอปคอนโซล .NET 6+ ใดก็ได้ พร้อมเคล็ดลับสำหรับกรณีขอบและประสิทธิภาพ

> **Pro tip:** หากคุณทำงานกับคอลเลกชันขนาดใหญ่ ควรพิจารณาใช้ `Parallel.ForEach`—แต่เรื่องนี้เป็นหัวข้อสำหรับวันอื่น

---

## สิ่งที่คุณจะได้เรียนรู้

- วิธีดึงคอลเลกชันของชื่อจากอ็อบเจ็กต์ (`GetSignatureNames` ในตัวอย่างของเรา)
- ไวยากรณ์และรายละเอียดของ **foreach loop example** ใน C#
- วิธี **display string list** ในคอนโซล รวมถึงเทคนิคการจัดรูปแบบ
- ข้อผิดพลาดทั่วไปเมื่อวนรายการ (คอลเลกชันเป็น null, ผลลัพธ์ว่างเปล่า)
- โปรแกรมเต็มพร้อมคัดลอก‑วางที่คุณสามารถรันได้ทันที

ไม่ต้องใช้ไลบรารีภายนอก; เพียงแค่ Base Class Library ที่มาพร้อมกับ .NET. หากคุณได้ติดตั้ง .NET SDK แล้ว คุณก็พร้อมใช้งาน

![แผนภาพ Iterate collection C# แสดงรายการที่ไหลเข้าสู่ลูป foreach แล้วไปยังคอนโซล](/images/iterate-collection-csharp.png "แผนภาพ iterate collection c# diagram")

---

## ขั้นตอนที่ 1: ตั้งค่าอ็อบเจ็กต์ตัวอย่าง

ก่อนอื่นเราต้องมีอ็อบเจ็กต์ที่สามารถคืนคอลเลกชันของชื่อได้ ลองนึกว่าคุณมีคลาส `Signature` ที่เก็บลายเซ็นหลายรายการ; แต่ละลายเซ็นมีคุณสมบัติ `Name`. เมธอด `GetSignatureNames` จะดึงชื่อเหล่านั้นออกเป็น `IEnumerable<string>`.

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

## ขั้นตอนที่ 2: เขียนลูป Foreach เพื่อแสดงรายการสตริง

ตอนนี้เรามีแหล่งชื่อแล้ว, มา **iterate collection C#** กันจริง ๆ. โครงสร้าง `foreach` จะดึงแต่ละองค์ประกอบจาก enumerable อัตโนมัติ, ดังนั้นเราไม่ต้องจัดการตัวแปรดัชนี.

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

**คำอธิบายของโค้ด:**

1. **Instantiate** `Signature` – ตอนนี้คุณมีอ็อบเจ็กต์ที่รู้จักชื่อของตนเอง.
2. **Retrieve** คอลเลกชันผ่าน `GetSignatureNames()` – นี่คือขั้นตอน **get object names**.
3. **Foreach loop example** – `foreach (var name in signatureNames)` จะวนซ้ำอัตโนมัติบนแต่ละสตริง.
4. **Display** แต่ละ `name` ด้วย `Console.WriteLine` – วิธีคลาสสิกในการ **display string list** ในแอปคอนโซล.

เนื่องจาก `signatureNames` implements `IEnumerable<string>`, the `foreach` loop works out of the box, handling the enumerator behind the scenes. No need to worry about off‑by‑one errors or manual bounds checking.

---

## ขั้นตอนที่ 3: รันโปรแกรมและตรวจสอบผลลัพธ์

คอมไพล์และรันโปรแกรม (เช่น `dotnet run` จากโฟลเดอร์โปรเจกต์). คุณควรเห็น:

```
Alice Johnson
Bob Smith
Charlie Davis

Press any key to exit...
```

หากไม่มีอะไรแสดง, ตรวจสอบให้แน่ใจว่า `GetSignatureNames` ไม่ได้คืนค่า `null`. การป้องกันอย่างรวดเร็วสามารถช่วยหลีกเลี่ยงปัญหาได้:

```csharp
var signatureNames = signature.GetSignatureNames() ?? Enumerable.Empty<string>();
```

ตอนนี้ลูปจะจัดการคอลเลกชันที่หายไปอย่างอ่อนโยนและแค่ไม่แสดงอะไรเลยแทนที่จะโยน `NullReferenceException`.

---

## ขั้นตอนที่ 4: ความแปรผันทั่วไปและกรณีขอบ

### 4.1 การวนลูปผ่านรายการของอ็อบเจ็กต์ซับซ้อน

บ่อยครั้งคุณอาจไม่ได้ทำงานกับสตริงธรรมดาแต่กับอ็อบเจ็กต์ที่มีหลายคุณสมบัติ. ในกรณีนั้นคุณยังสามารถ **loop over items** และตัดสินใจว่าจะใส่อะไรแสดง:

```csharp
foreach (var sig in signature.GetAllSignatures())
{
    Console.WriteLine($"{sig.Id}: {sig.Name}");
}
```

ที่นี่เราใช้ string interpolation เพื่อรวมฟิลด์—ยังคงเป็นลูป `foreach` เพียงแต่ผลลัพธ์มีความหลากหลายมากขึ้น.

### 4.2 การออกจากลูปล่วงหน้าด้วย `break`

หากคุณต้องการเฉพาะชื่อแรกที่ตรงกัน, ให้ `break` ออกจากลูป:

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

### 4.3 การวนลูปแบบขนาน (ขั้นสูง)

เมื่อคอลเลกชันใหญ่และแต่ละรอบต้องใช้ CPU มาก, `Parallel.ForEach` สามารถเร่งความเร็วได้:

```csharp
System.Threading.Tasks.Parallel.ForEach(signatureNames, name =>
{
    // Simulate work
    Console.WriteLine(name);
});
```

จำไว้ว่า `Console.WriteLine` เองเป็น thread‑safe แต่ลำดับการแสดงผลจะไม่แน่นอน.

---

## ขั้นตอนที่ 5: เคล็ดลับสำหรับลูปที่สะอาดและดูแลได้ง่าย

- **Prefer `foreach` over `for`** เมื่อคุณไม่ต้องการดัชนี; จะลดบั๊ก off‑by‑one
- **Use `IEnumerable<T>`** ในลายเซ็นของเมธอดเพื่อให้ API ยืดหยุ่น
- **Guard against null** คอลเลกชันด้วยตัวดำเนินการ null‑coalescing (`??`)
- **Keep the loop body small**—หากคุณพบว่าตัวเองเขียนหลายบรรทัด ให้แยกเป็นเมธอด
- **Avoid modifying the collection** ขณะวนลูป; จะทำให้เกิด `InvalidOperationException`

---

## สรุป

เราได้สาธิตวิธี **iterate collection C#** ด้วย **foreach loop example** ที่สะอาด, ดึง **object names**, และ **display string list** ในคอนโซล. โปรแกรมเต็ม—การกำหนดอ็อบเจ็กต์, การดึงข้อมูล, และการวนลูป—ทำงานได้ทันที, ให้พื้นฐานที่มั่นคงสำหรับทุกสถานการณ์ที่ต้องวนรายการ

ต่อจากนี้คุณอาจสำรวจ:

- การกรองด้วย LINQ ก่อนวนลูป (`signatureNames.Where(n => n.Contains("a"))`)
- การเขียนผลลัพธ์ไปยังไฟล์แทนคอนโซล
- การใช้ `IAsyncEnumerable<T>` สำหรับสตรีมแบบอะซิงโครนัส

ลองทำดูและคุณจะเห็นว่า `foreach` มีความยืดหยุ่นแค่ไหน. มีคำถามเกี่ยวกับกรณีขอบหรือประสิทธิภาพ? แสดงความคิดเห็นด้านล่างและขอให้เขียนโค้ดอย่างสนุกสนาน!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}