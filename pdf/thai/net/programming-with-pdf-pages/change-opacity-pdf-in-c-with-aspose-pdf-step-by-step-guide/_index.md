---
category: general
date: 2026-08-11
description: เปลี่ยนความทึบของ PDF ด้วย Aspose.Pdf ใน C#. เรียนรู้วิธีเพิ่มความโปร่งใสให้กับหน้า
  PDF ตั้งค่า graphic state และบันทึกผลลัพธ์อย่างรวดเร็ว.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change opacity PDF
- how to add transparency
- add pdf transparency
language: th
lastmod: 2026-08-11
og_description: เปลี่ยนความทึบของ PDF ด้วย Aspose.Pdf ใน C#. ตามคำแนะนำนี้เพื่อดูวิธีเพิ่มความโปร่งใสให้กับเอกสาร
  PDF ใด ๆ ปรับแต่งสถานะกราฟิก และส่งออกผลลัพธ์
og_image_alt: Screenshot illustrating change opacity PDF example in C# code
og_title: เปลี่ยนความทึบของ PDF ใน C# – คู่มือ Aspose.Pdf ฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  headline: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: Change opacity PDF using Aspose.Pdf in C#. Learn how to add transparency
    to PDF pages, set graphic state, and save the result quickly.
  name: Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
    text: '**Missing ExtGState dictionary** – Some PDFs do not contain an `ExtGState`
      entry by default. In that case, create one:'
  - name: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
    text: '**Incorrect resource name** – The name you use in `SetGraphicsState` must
      match exactly the key you added (`GS0`). A typo results in the default, fully
      opaque rendering.'
  - name: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
    text: '**Overriding existing graphics states** – Adding a new entry does not replace
      existing ones. If you reuse a name that already exists, you may unintentionally
      alter other page elements that reference it.'
  - name: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
    text: '**Viewer compatibility** – Older PDF viewers (pre‑1.4) may ignore transparency.
      Ensure your target audience uses a modern viewer such as Adobe Reader DC or
      Chrome’s built‑in PDF viewer.'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: เปลี่ยนความทึบของ PDF ใน C# ด้วย Aspose.Pdf – คู่มือขั้นตอนโดยละเอียด
url: /th/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เปลี่ยนความทึบของ PDF ด้วย C# และ Aspose.Pdf – คู่มือขั้นตอนโดยละเอียด

หากคุณต้องการ **เปลี่ยนความทึบของไฟล์ PDF** อย่างอัตโนมัติ คู่มือนี้จะแสดงวิธีทำอย่างละเอียด ด้วย Aspose.Pdf for .NET คุณสามารถควบคุมความโปร่งใสของวัตถุกราฟิก ข้อความ และรูปภาพได้โดยไม่ต้องออกจากโค้ด C# ของคุณ

ในส่วนต่อไปนี้ คุณจะได้เรียนรู้ **วิธีเพิ่มความโปร่งใส** ให้กับหน้า PDF ความหมายของอ็อบเจ็กต์ graphics state ที่อยู่เบื้องหลัง และวิธีบันทึกเอกสารที่แก้ไขแล้ว คู่มือนี้ยังครอบคลุมข้อผิดพลาดทั่วไปเมื่อคุณ **เพิ่มความโปร่งใสให้ PDF** และให้เคล็ดลับสำหรับสถานการณ์จริง

## สิ่งที่คุณจะทำสำเร็จ

เมื่อจบคู่มือนี้ คุณจะสามารถ:

* โหลดเอกสาร PDF ที่มีอยู่
* สร้าง graphics state dictionary ใหม่ที่กำหนดค่าความทึบ
* แทรก graphics state ลงใน resource dictionary ของหน้า
* บันทึกเอกสารพร้อมเอฟเฟกต์ **เปลี่ยนความทึบของ PDF** ที่อัปเดตแล้ว

ไม่ต้องใช้เครื่องมือภายนอก—เพียงแค่ไลบรารี Aspose.Pdf for .NET (เวอร์ชัน 23.10 หรือใหม่กว่า) และสภาพแวดล้อมการพัฒนา .NET

## ข้อกำหนดเบื้องต้น

* .NET 6.0 (หรือ .NET Framework 4.7.2+) ที่ติดตั้งแล้ว
* Visual Studio 2022 หรือ IDE ที่รองรับ C#
* การอ้างอิงไปยังแพ็กเกจ NuGet `Aspose.Pdf`
* ไฟล์ PDF อินพุต (`input.pdf`) อยู่ในไดเรกทอรีที่สามารถเขียนได้

> **เคล็ดลับมืออาชีพ:** เมื่อทดสอบการเปลี่ยนความทึบ ให้ใช้ PDF ที่มีกราฟิกเวกเตอร์หรือข้อความอยู่แล้ว; รูปภาพแบบแรสเตอร์จะไม่สนใจพารามิเตอร์ `ca` และ `CA` เว้นแต่จะถูกวางไว้ใน transparency group

## เปลี่ยนความทึบของ PDF ด้วย Aspose.Pdf

หัวใจของวิธีแก้คือการแก้ไข dictionary **ExtGState** (external graphics state) ของหน้า Dictionary นี้เก็บพารามิเตอร์เช่น **ca** (stroke opacity) และ **CA** (fill opacity) โดยการเพิ่มรายการใหม่คุณสามารถอ้างอิงมันใน stream ของเนื้อหาได้ต่อไป

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;

class ChangeOpacityPdfExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        using (var document = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 2: Access the first page and its resource dictionary
            var page = document.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();

            // Step 3: Create a new graphics state dictionary with desired opacity values
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
            var parameters = new[]
            {
                // Fill opacity (CA) – 1.0 means fully opaque
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                // Stroke opacity (ca) – 0.5 makes lines semi‑transparent
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                // Blend mode (BM) – Normal is the default blend mode
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters) newGraphicsState.Add(p);

            // Step 4: Add the new graphics state to the ExtGState dictionary
            // “GS0” is the identifier you will reference later in the content stream
            extGState.Add("GS0", newGraphicsState);

            // Optional: Demonstrate usage by drawing a semi‑transparent rectangle
            // This part shows how the new graphics state affects drawing commands.
            var canvas = new Aspose.Pdf.Drawing.Graphic(page);
            canvas.SetGraphicsState("GS0"); // Apply the opacity settings
            canvas.Rectangle(100, 500, 200, 600);
            canvas.FillColor = Color.FromRgb(255, 0, 0); // Red fill
            canvas.StrokeColor = Color.FromRgb(0, 0, 255); // Blue border
            canvas.Draw();

            // Step 5: Save the modified PDF
            document.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF saved with changed opacity.");
    }
}
```

### ทำไมวิธีนี้ถึงได้ผล

* **ExtGState** เป็นทรัพยากร PDF ที่เก็บพารามิเตอร์กราฟิกที่ใช้ซ้ำได้ การเพิ่มรายการกำหนดเอง (`GS0`) จะสร้างการกำหนดค่าความโปร่งใสที่ใช้ซ้ำได้
* คีย์ **ca** ควบคุมความทึบของการวาดเส้น (stroke) เช่น เส้นและขอบ คีย์ **CA** ควบคุมการเติม (fill) เช่น รูปร่างสีและข้อความ การตั้งค่า `ca = 0.5` ทำให้เส้นโปร่งใส 50 % ในขณะที่ `CA = 1` ทำให้การเติมเต็มทึบเต็มที่
* การเรียก `SetGraphicsState("GS0")` บอก Aspose.Pdf ให้ใส่ตัวดำเนินการ `/GS0 gs` ลงใน content stream เพื่อเปิดใช้การตั้งค่าความโปร่งใสใหม่สำหรับคำสั่งการวาดต่อไป

## วิธีเพิ่มความโปร่งใสให้กับเนื้อหาที่มีอยู่

หากหน้ามีข้อความหรือรูปภาพอยู่แล้วและคุณต้องการทำให้พวกมันกึ่งโปร่งใสโดยไม่ต้องวาดใหม่ คุณสามารถแทรกตัวดำเนินการ **gs** ก่อนเนื้อหาที่มีอยู่ ตัวอย่างโค้ดต่อไปนี้แสดงวิธี prepend ตัวดำเนินการลงใน content stream ของหน้า

```csharp
// Retrieve the existing content stream
var content = page.Contents[1];
var originalBytes = content.ToByteArray();

// Build the new content with the graphics state applied
var gsOperator = System.Text.Encoding.ASCII.GetBytes("/GS0 gs\n");
var newBytes = new List<byte>(gsOperator);
newBytes.AddRange(originalBytes);

// Replace the page content
page.Contents[1].Replace(newBytes.ToArray());
```

### กรณีขอบและข้อควรพิจารณา

| สถานการณ์ | วิธีจัดการที่แนะนำ |
|-----------|----------------------|
| **หลายหน้า** | วนลูปผ่าน `document.Pages` และทำซ้ำขั้นตอนที่ 2‑4 สำหรับแต่ละหน้าที่ต้องการเปลี่ยน |
| **ความทึบต่างกันตามองค์ประกอบ** | สร้าง ExtGState เพิ่มเติม (`GS1`, `GS2`, …) พร้อมค่า `ca`/`CA` ที่แตกต่างและนำไปใช้ตามต้องการ |
| **PDF ที่มีรายการ ExtGState อยู่แล้ว** | ใช้ `dictEditor["ExtGState"]` อย่างปลอดภัย; หากคีย์ไม่มีอยู่ ให้สร้าง `CosPdfDictionary` ใหม่และกำหนดให้กับ `page.Resources` |
| **Transparency groups** | สำหรับการคอมโพสท์ที่ซับซ้อน (เช่น ภาพซ้อนกัน) ให้ตั้งค่า dictionary `/Group` ด้วย `S /Transparency` และ `CS /DeviceRGB` ซึ่งอยู่เหนือระดับพื้นฐานของ **เปลี่ยนความทึบของ PDF** แต่บางกรณีอาจจำเป็นสำหรับเลย์เอาต์ขั้นสูง |

## เพิ่มความโปร่งใสให้กับกราฟิกเวกเตอร์ใน PDF

นอกจากสี่เหลี่ยมแล้ว คุณสามารถใช้ graphics state เดียวกันกับการวาดเวกเตอร์ใด ๆ — เส้น, โค้ง, หรือแม้แต่ข้อความ ตัวอย่างสั้นต่อไปนี้เขียนข้อความกึ่งโปร่งใส:

```csharp
var textFragment = new TextFragment("Transparent text")
{
    Position = new Position(100, 400),
    TextState = { FontSize = 36, ForegroundColor = Color.Black }
};
page.Paragraphs.Add(textFragment);

// Apply the graphics state to the text fragment
textFragment.TextState.GraphicsState = "GS0";
```

คุณสมบัติ `GraphicsState` ของ `TextState` บอกเอนจิน PDF ให้เรนเดอร์ข้อความโดยใช้ความโปร่งใสที่กำหนดใน `GS0` นี่เป็นวิธีที่ตรงที่สุดในการ **เพิ่มความโปร่งใสให้กับ PDF** สำหรับเนื้อหาข้อความ

## ข้อผิดพลาดทั่วไปเมื่อคุณเปลี่ยนความทึบของ PDF

1. **ไม่มี ExtGState dictionary** – PDF บางไฟล์ไม่มีรายการ `ExtGState` โดยค่าเริ่มต้น ในกรณีนั้นให้สร้างใหม่:
   ```csharp
   if (!dictEditor.ContainsKey("ExtGState"))
       dictEditor.Add("ExtGState", new CosPdfDictionary(document));
   ```
2. **ชื่อทรัพยากรไม่ตรง** – ชื่อที่ใช้ใน `SetGraphicsState` ต้องตรงกับคีย์ที่คุณเพิ่ม (`GS0`) อย่างแม่นยำ การพิมพ์ผิดจะทำให้ PDF แสดงผลแบบทึบเต็มที่ตามค่าเริ่มต้น
3. **การเขียนทับ graphics state ที่มีอยู่** – การเพิ่มรายการใหม่ไม่ได้แทนที่รายการเดิม หากใช้ชื่อที่ซ้ำกับที่มีอยู่อยู่แล้ว คุณอาจทำให้ส่วนอื่นของหน้าเปลี่ยนแปลงโดยไม่ได้ตั้งใจ
4. **ความเข้ากันได้ของโปรแกรมอ่าน** – โปรแกรมอ่าน PDF รุ่นเก่า (ก่อน 1.4) อาจละเลยความโปร่งใส ตรวจสอบให้ผู้ใช้เป้าหมายใช้โปรแกรมอ่านสมัยใหม่ เช่น Adobe Reader DC หรือ viewer ของ Chrome

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่สมบูรณ์และเป็นอิสระ คุณสามารถคัดลอก วาง และรันได้ รวมถึง `using` directives, การจัดการข้อผิดพลาด, และคอมเมนต์ทั้งหมด



## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีโค้ดตัวอย่างทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [How to Add a Text Stamp to PDF Using Aspose.PDF .NET: Comprehensive Guide](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET: A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds Guide](/pdf/english/net/watermarks-backgrounds/implement-page-stamps-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}