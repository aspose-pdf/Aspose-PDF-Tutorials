---
category: general
date: 2026-10-01
description: เพิ่ม ExtGState PDF แบบกำหนดเองโดยใช้ Aspose.PDF เพื่อกำหนดความโปร่งใสของ
  PDF อย่างรวดเร็ว ทำตามคู่มือนี้เพื่อเรียนรู้วิธีตั้งค่าความโปร่งใสของ PDF ด้วยกราฟิกสเตตแบบกำหนดเอง.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom extgstate pdf
- how to set transparency pdf
- Aspose.PDF graphics state
- PDF opacity settings
- PDF blend mode tutorial
language: th
lastmod: 2026-10-01
og_description: เพิ่ม ExtGState แบบกำหนดเองใน PDF และเรียนรู้วิธีตั้งค่าความโปร่งใสของ
  PDF ด้วยไม่กี่บรรทัดของ C# คู่มือนี้ครอบคลุมทุกขั้นตอนตั้งแต่การโหลดไฟล์จนถึงการบันทึกผลลัพธ์
og_image_alt: Screenshot of a PDF page showing transparent graphics after adding a
  custom ExtGState
og_title: เพิ่ม ExtGState ที่กำหนดเองใน PDF – บทเรียนเต็ม Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add custom ExtGState PDF using Aspose.PDF to set transparency PDF quickly.
    Follow this guide to learn how to set transparency PDF with a custom graphics
    state.
  headline: Add custom ExtGState PDF with Aspose.PDF – step‑by‑step guide
  type: TechArticle
tags:
- PDF
- Aspose.PDF
- C#
- GraphicsState
title: เพิ่ม ExtGState แบบกำหนดเองใน PDF ด้วย Aspose.PDF – คู่มือขั้นตอนโดยละเอียด
url: /th/net/images-graphics/add-custom-extgstate-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่ม ExtGState PDF แบบกำหนดเองด้วย Aspose.PDF – คู่มือขั้นตอนต่อขั้นตอน

หากคุณต้องการ **เพิ่ม ExtGState PDF แบบกำหนดเอง** เพื่อควบคุมความโปร่งใสและโหมดการผสมสี คู่มือฉบับนี้จะแสดงให้คุณเห็นอย่างละเอียด คุณจะได้เห็นตัวอย่างที่ทำงานได้เต็มรูปแบบซึ่งสาธิต **วิธีตั้งค่าความโปร่งใส PDF** ด้วย Aspose.PDF สำหรับ .NET

ในส่วนต่อไปนี้ เราจะครอบคลุมแพ็กเกจ NuGet ที่จำเป็น การอธิบายโค้ดทีละบรรทัด และเคล็ดลับในการจัดการกรณีขอบเช่นหลายหน้า หรือโหมดการผสมสีที่กำหนดเอง เมื่อเสร็จสิ้นคุณจะสามารถแก้ไข PDF ใด ๆ ที่มีอยู่และใช้กราฟิกสเตตแบบโปร่งใสได้โดยไม่ต้องออกจาก IDE ของคุณ

## Prerequisites

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานได้กับ .NET Framework 4.7+)
- Visual Studio 2022 (หรือโปรแกรมแก้ไข C# ใด ๆ ที่คุณชอบ)
- แพ็กเกจ **Aspose.PDF for .NET** NuGet (เวอร์ชัน 23.12 หรือใหม่กว่า)
- ไฟล์ PDF ตัวอย่างชื่อ `input.pdf` ที่วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโปรเจกต์ได้

> **Pro tip:** ใช้โฟลเดอร์ “Resources” แยกเฉพาะในโซลูชันของคุณเพื่อเก็บไฟล์ PDF เข้าและออกไว้ด้วยกัน วิธีนี้จะช่วยหลีกเลี่ยงข้อผิดพลาดที่เกี่ยวกับเส้นทางเมื่อโค้ดทำงาน

## Install Aspose.PDF

เปิดคอนโซล NuGet Package Manager แล้วรัน:

```bash
dotnet add package Aspose.PDF
```

แพ็กเกจนี้จะให้คลาส `Aspose.Pdf.Document`, `CosPdfDictionary` และคลาสที่เกี่ยวข้องที่ใช้ในตัวอย่างโค้ด

## Step 1 – Load the PDF document

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;

// Load the source PDF
using var pdfDocument = new Document("Resources/input.pdf");
```

**ทำไมขั้นตอนนี้สำคัญ:**  
`Document` แทนไฟล์ PDF ทั้งหมดในหน่วยความจำ การเปิดไฟล์ด้วยบล็อก `using` จะรับประกันว่าทรัพยากรที่ไม่ได้จัดการทั้งหมดจะถูกปล่อยหลังจากเราประมวลผลเสร็จ

## Step 2 – Access the first page’s resource dictionary

```csharp
// Get the first page (pages are 1‑based in Aspose.PDF)
Page firstPage = pdfDocument.Pages[1];

// The resource dictionary holds objects like fonts, XObjects, and ExtGState entries
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**คำอธิบาย:**  
แต่ละหน้าของ PDF มีพจนานุกรม *Resources* ที่จัดกลุ่มอ็อบเจ็กต์ที่สามารถนำกลับมาใช้ใหม่ได้ การแก้ไขพจนานุกรมนี้ทำให้เราสามารถแทรกกราฟิกสเตตใหม่ที่หน้าจะอ้างอิงต่อไป

## Step 3 – Retrieve (or create) the ExtGState dictionary

```csharp
// Try to get the existing ExtGState dictionary; create one if it does not exist
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", extGStateDict);
}
```

**ทำไมต้องตรวจสอบก่อน:**  
PDF บางไฟล์อาจมีรายการ `ExtGState` อยู่แล้ว การเพิ่มรายการซ้ำอาจเขียนทับสเตตที่มีอยู่และทำให้เนื้อหาอื่นเสียหาย โค้ดเชิงป้องกันนี้ช่วยรักษารายการเดิมไว้ไม่ให้เปลี่ยนแปลง

## Step 4 – Build a custom graphics state

```csharp
// Create an empty dictionary that will become our custom graphics state
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // CA – stroke opacity (range 0‑1)
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
    // ca – fill opacity (range 0‑1)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // BM – blend mode (Normal, Multiply, Screen, etc.)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Add each entry to the dictionary
foreach (var entry in graphicsStateEntries)
{
    newGraphicsState.Add(entry);
}
```

**แต่ละคีย์ทำอะไร:**

| คีย์ | ความหมาย | ค่าที่ใช้บ่อย |
|-----|---------|----------------|
| `CA` | ความโปร่งใสของเส้นขอบ | `0.0` (โปร่งใสเต็ม) → `1.0` (ทึบเต็ม) |
| `ca` | ความโปร่งใสของการเติม | ช่วงเดียวกับ `CA` |
| `BM` | โหมดการผสมสี | `Normal`, `Multiply`, `Screen`, `Overlay`, เป็นต้น |

โดยการตั้งค่า `ca` เป็น `0.5` เราจะทำให้รูปทรงที่เติมสีมีความโปร่งใส 50 % ในขณะที่ `CA` ยังคงเป็นค่าทึบเต็มสำหรับเส้นขอบ การเปลี่ยนค่า `BM` จะทำให้คุณทดลองเอฟเฟกต์การผสมสีแบบ Photoshop

## Step 5 – Register the custom graphics state under a unique name

```csharp
// Choose a unique name for the new state, e.g., "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

**รูปแบบการตั้งชื่อ:**  
สเปค PDF แนะนำให้ใช้ตัวระบุสั้น ๆ เป็นตัวพิมพ์ใหญ่ การใช้ `GS0` (Graphics State 0) ทำให้ชื่อสั้นและง่ายต่อการอ้างอิงจากสตรีมเนื้อหา

## Step 6 – Apply the custom graphics state in a content stream (optional)

หากคุณต้องการวาดสี่เหลี่ยมโปร่งใสบนหน้าที่หนึ่ง คุณสามารถเพิ่มออพเรเตอร์ต่อไปนี้ไว้ด้านหน้า:

```csharp
// Build the content stream that uses the new graphics state
var content = new Operator[]
{
    new Operator("q"),                 // Save graphics state
    new Operator("GS0", "gs"),         // Set our custom ExtGState
    new Operator("0.5 0.5 1 rg"),      // Set fill color (light blue)
    new Operator("100 500 200 100 re"),// Rectangle (x, y, width, height)
    new Operator("f"),                 // Fill the rectangle using the fill opacity
    new Operator("Q")                  // Restore graphics state
};

// Add the operators to the page's content
firstPage.Contents.Add(content);
```

**ทำไมขั้นตอนนี้เป็นทางเลือก:**  
ขั้นตอนก่อนหน้านี้เพียง *กำหนด* กราฟิกสเตตเท่านั้น เพื่อให้เห็นผลต้องอ้างอิงสเตตจากสตรีมเนื้อหาของหน้า โค้ดส่วนนี้แสดงการใช้งานจริง แต่คุณก็สามารถนำสเตตไปใช้กับคำสั่งวาดที่มีอยู่ใน PDF ของคุณได้เช่นกัน

## Step 7 – Save the modified PDF

```csharp
// Persist the changes to a new file
pdfDocument.Save("Resources/output.pdf");
```

เมื่อคุณเปิด `output.pdf` คุณจะสังเกตเห็นสี่เหลี่ยมที่แสดงด้วยความโปร่งใสการเติม 50 % ในขณะที่เส้นขอบยังคงทึบเต็ม—ผลลัพธ์ที่ได้จาก **วิธีตั้งค่าความโปร่งใส PDF** ด้วย ExtGState ที่กำหนดเอง

## Handling Multiple Pages

หากต้องการเอฟเฟ็กต์ความโปร่งใสเดียวกันบนทุกหน้า ให้วนลูปผ่าน `pdfDocument.Pages` และทำซ้ำ **Step 2**‑**Step 5** สำหรับพจนานุกรมของแต่ละหน้า ระวังไม่ให้เพิ่มกราฟิกสเตตซ้ำหลายครั้งต่อหน้า; การใช้พจนานุกรมเดียวกันข้ามหลายหน้าไม่ได้รับอนุญาตตามสเปค PDF

```csharp
foreach (Page page in pdfDocument.Pages)
{
    var editor = new DictionaryEditor(page.Resources);
    // Ensure ExtGState exists, then add GS0 as shown earlier
    // (code omitted for brevity)
}
```

## Common pitfalls and how to avoid them

| อาการ | สาเหตุ | วิธีแก้ |
|---------|-------|-----|
| ความโปร่งใสไม่เปลี่ยน | ค่า `ca` หรือ `CA` อยู่นอกช่วง 0‑1 | ใช้ค่าทศนิยมระหว่าง `0.0` ถึง `1.0` |
| เนื้อหาหายไป | กราฟิกสเตตไม่ได้ถูกใช้ (`gs` operator ขาด) | แทรก `GS0 gs` ก่อนคำสั่งวาด |
| PDF เปิดไม่ขึ้น | คีย์ซ้ำในพจนานุกรม `ExtGState` | ตรวจสอบ `extGStateDict.ContainsKey("GS0")` ก่อนเพิ่ม |
| โหมดการผสมสีถูกละเลย | ตัวดู PDF ไม่รองรับโหมดที่ระบุ | ใช้โหมดมาตรฐานเช่น `Normal`, `Multiply` |

## Full runnable example

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF
        using var pdfDocument = new Document("Resources/input.pdf");

        // Work with the first page
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        else
        {
            extGStateDict = new CosPdfDictionary(pdfDocument);
            resourcesEditor.Add("ExtGState", extGStateDict);
        }

        // Create custom graphics state
        CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var entries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var e in entries) newGraphicsState.Add(e);

        // Register under a unique name
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a transparent rectangle
        var ops = new Operator[]
        {
            new Operator("q"),
            new Operator("GS0", "gs"),
            new Operator("0.5 0.5 1 rg"),
            new Operator("100 500 200 100 re"),
            new Operator("f"),
            new Operator("Q")
        };
        firstPage.Contents.Add(ops);

        // Save result
        pdfDocument.Save("Resources/output.pdf");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  
เมื่อเปิด `output.pdf` จะเห็นสี่เหลี่ยมสีฟ้าอ่อนที่ตำแหน่ง (100, 500) มีความโปร่งใสการเติม 50 % เส้นขอบของสี่เหลี่ยมยังคงทึบเต็มเพราะ `CA` ถูกตั้งเป็น `1.0`

## Conclusion

คุณได้เรียนรู้วิธี **เพิ่ม ExtGState PDF แบบกำหนดเอง** ด้วย Aspose.PDF และควบคุมความโปร่งใสและโหมดการผสมสีอย่างแม่นยำ—ตอบคำถามทั่วไป **วิธีตั้งค่าความโปร่งใส PDF** คู่มือได้ครอบคลุมการโหลดเอกสาร, การแก้ไขพจนานุกรมทรัพยากร, การกำหนดกราฟิกสเตต, การนำไปใช้, และการบันทึกผลลัพธ์

ต่อไปคุณอาจสำรวจ:

- การใช้โหมดการผสมสีต่าง ๆ (`Multiply`, `Screen`) เพื่อสร้างเอฟเฟกต์เชิงสร้างสรรค์
- การนำ ExtGState เดียวกันไปใช้กับ Image XObjects เพื่อโลโก้ที่มีความโปร่งใสระดับกลาง
- การทำอัตโนมัติสำหรับการแก้ไข PDF จำนวนมากในบริการพื้นหลัง

อย่าลังเลที่จะทดลองปรับค่าต่าง ๆ, เปลี่ยนชื่อกราฟิกสเตต, หรือ

## What Should You Learn Next?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [เพิ่มความโปร่งใสให้ PDF ด้วย Aspose – คู่มือ C# ฉบับสมบูรณ์](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [วิธีเพิ่มตราประทับหน้าใน PDF ด้วย Aspose.PDF for Java (คู่มือ 2023)](/pdf/english/java/watermarks-backgrounds/add-page-stamp-aspose-pdf-java/)
- [วิธีเพิ่มตราประทับข้อความใน PDF ด้วย Aspose.PDF for Java: คู่มือฉบับสมบูรณ์](/pdf/english/java/document-manipulation/aspose-pdf-java-add-text-stamp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}