---
category: general
date: 2026-09-24
description: เรียนรู้วิธีเปลี่ยนความโปร่งใสของ PDF ใน C# ด้วย Aspose.Pdf คู่มือแบบขั้นตอนนี้ครอบคลุมความทึบของ
  PDF โหมดการผสมและการแก้ไขสถานะกราฟิก
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity
- C# PDF manipulation
- blend mode PDF
- modify PDF resources
language: th
lastmod: 2026-09-24
og_description: เปลี่ยนความโปร่งใสของ PDF ใน C# ด้วย Aspose.Pdf. ทำตามคำแนะนำนี้เพื่อแก้ไขความทึบของ
  PDF, โหมดการผสม, และสถานะกราฟิกสำหรับผลลัพธ์เอกสารระดับมืออาชีพ.
og_image_alt: Screenshot showing C# code that changes PDF transparency
og_title: เปลี่ยนความโปร่งใสของ PDF ใน C# – คู่มือ Aspose.Pdf ฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to change PDF transparency in C# with Aspose.Pdf. This step‑by‑step
    guide covers PDF opacity, blend mode and graphics state editing.
  headline: How to change PDF transparency in C# using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- C#
- Aspose.Pdf
- Transparency
title: วิธีเปลี่ยนความโปร่งใสของ PDF ใน C# ด้วย Aspose.Pdf
url: /th/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการเปลี่ยนความโปร่งใสของ PDF ใน C# ด้วย Aspose.Pdf

หากคุณต้องการ **เปลี่ยนความโปร่งใสของ PDF** ในโครงการ .NET คู่มือนี้จะแสดงให้คุณเห็นขั้นตอนการทำอย่างละเอียดด้วย Aspose.Pdf คุณจะได้เห็นตัวอย่างที่สมบูรณ์และสามารถรันได้ซึ่งปรับเปลี่ยนความทึบของ PDF, ตั้งค่า blend mode, และอัปเดตพจนานุกรม graphics state ของหน้า

การเปลี่ยนความโปร่งใสของ PDF เป็นความต้องการที่พบบ่อยเมื่อคุณต้องการลายน้ำ, กราฟิกซ้อน, หรือเอฟเฟกต์ภาพแบบกำหนดเอง ในบทเรียนนี้คุณจะได้เรียนรู้การแก้ไข **Aspose.Pdf graphics state**, ปรับ **PDF opacity**, และทำงานกับการตั้งค่า **blend mode PDF** — ทั้งหมดโดยใช้โค้ด C# ที่เรียบง่าย

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า ติดตั้งแล้ว  
* ใบอนุญาต Aspose.Pdf for .NET (หรือคีย์ประเมินผลชั่วคราว)  
* ไฟล์ PDF ชื่อ `input.pdf` อยู่ในโฟลเดอร์ที่คุณสามารถอ้างอิงเป็น `YOUR_DIRECTORY`  
* ความคุ้นเคยพื้นฐานกับ C# และ Visual Studio (IDE ใดก็ได้ทำงานได้)

ไม่จำเป็นต้องใช้แพคเกจ NuGet เพิ่มเติมนอกจาก `Aspose.Pdf` โค้ดสามารถทำงานได้บน Windows, Linux หรือ macOS เนื่องจาก Aspose.Pdf รองรับหลายแพลตฟอร์ม

## การเปลี่ยนความโปร่งใสของ PDF – ขั้นตอนที่ 1: เปิดเอกสาร PDF

ขั้นตอนแรกคือการโหลด PDF ต้นฉบับ การใช้บล็อก `using` จะรับประกันว่าการจัดการไฟล์จะถูกปล่อยออกโดยอัตโนมัติ

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.Collections.Generic;

string inputPath  = @"YOUR_DIRECTORY\input.pdf";
string outputPath = @"YOUR_DIRECTORY\output.pdf";

using (var document = new Document(inputPath))
{
    // The document is now ready for manipulation.
```

การเปิดเอกสารเป็นพื้นฐานสำหรับงาน **C# PDF manipulation** ใด ๆ หากไม่พบไฟล์ Aspose.Pdf จะโยน `FileNotFoundException` ดังนั้นตรวจสอบเส้นทางให้แน่ใจก่อนรันโค้ด

## เข้าถึงทรัพยากรของหน้าโดยใช้ Aspose.Pdf graphics state

ต่อไปให้ดึงหน้าที่หนึ่งและพจนานุกรมทรัพยากรของมัน พจนานุกรมทรัพยากรเก็บอ็อบเจ็กต์เช่นฟอนต์, รูปภาพ, และรายการ **ExtGState** ที่ควบคุมพารามิเตอร์กราฟิก

```csharp
    // Step 2: Get the first page of the document
    var page = document.Pages[1];

    // Step 3: Access the page's resource dictionary for editing
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

คลาส `DictionaryEditor` ให้ตัวห่อที่สะดวกสำหรับการอ่านและเขียนพจนานุกรม PDF ที่นี่เรามุ่งเน้นที่พจนานุกรม **ExtGState** เนื่องจากมันเก็บการตั้งค่าความโปร่งใส

## สร้างและกำหนดค่า graphics state ใหม่สำหรับความทึบของ PDF

ตอนนี้เราจะสร้างพจนานุกรม graphics state ใหม่ พจนานุกรมนี้จะเก็บพารามิเตอร์ที่กำหนดความทึบของเส้น (`CA`), ความทึบของการเติม (`ca`), และ blend mode (`BM`)

```csharp
    // Step 4: Retrieve the existing ExtGState dictionary (graphics states)
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();

    // Step 5: Create a new empty graphics state dictionary
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);

    // Step 6: Define graphics state parameters (stroke opacity, fill opacity, blend mode)
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),            // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),          // Fill opacity (50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))       // Blend mode PDF (standard normal blending)
    };

    // Step 7: Add each parameter to the new graphics state dictionary
    foreach (var param in parameters)
        newGraphicsState.Add(param);
```

* **`CA`** ควบคุมความทึบของการวาดเส้น (เส้น, เส้นขอบ).  
* **`ca`** ควบคุมความทึบของการเติม (รูปทรงที่เติม, ข้อความ).  
* **`BM`** เลือก blend mode; `"Normal"` เป็นค่าเริ่มต้น, แต่คุณสามารถใช้ `"Multiply"` หรือ `"Screen"` สำหรับเอฟเฟกต์ศิลปะ

การตั้งค่าเหล่านี้เป็นหัวใจของการจัดการ **PDF opacity** ปรับค่าตัวเลขให้เหมาะกับการออกแบบของคุณ — `0` หมายถึงโปร่งใสเต็มที่, `1` หมายถึงทึบเต็มที่

## แทรก graphics state และบันทึกเอกสาร

หลังจากสร้าง state ใหม่แล้ว เราเพิ่มมันเข้าไปในพจนานุกรม **ExtGState** ที่มีอยู่โดยใช้ชื่อที่ไม่ซ้ำ (`GS0`). สุดท้ายเราบันทึก PDF ที่แก้ไขแล้ว

```csharp
    // Step 8: Insert the new graphics state into the ExtGState dictionary with a name
    extGState.Add("GS0", newGraphicsState);

    // Step 9: Save the modified PDF document
    document.Save(outputPath);
}
```

เมื่อเปิด PDF ในโปรแกรมดู, เนื้อหาใด ๆ ที่อ้างอิง `GS0` จะถูกแสดงด้วยความโปร่งใสที่กำหนด คุณสามารถนำ graphics state นี้ไปใช้กับอ็อบเจ็กต์เฉพาะในภายหลังโดยใช้ property `GraphicsState` ของคำสั่งวาด (เช่น `page.Contents.Add(new TextFragment(...){ GraphicsState = "GS0" })`).

## ตรวจสอบผลลัพธ์

เปิด `output.pdf` ด้วย Adobe Acrobat Reader, Foxit หรือโปรแกรมดู PDF ใด ๆ ที่รองรับความโปร่งใส คุณควรเห็นองค์ประกอบการเติมของหน้าที่หนึ่งแสดงที่ความทึบ 50 % ในขณะที่เส้นยังคงทึบเต็มที่ หากคุณไม่เห็นการเปลี่ยนแปลง ให้ตรวจสอบว่าหน้านั้นใช้ graphics state ใหม่จริงหรือไม่ — หากไม่, คุณสามารถกำหนด `GS0` ให้กับอ็อบเจ็กต์ที่ต้องการได้โดยตรง

![ตัวอย่างโค้ด C# ที่เปลี่ยนความโปร่งใสของ PDF](path/to/image.png){: .img-responsive alt="ตัวอย่างโค้ด C# ที่เปลี่ยนความโปร่งใสของ PDF"}

*ภาพด้านบนแสดงซอร์สโค้ด C# ทั้งหมดที่เปลี่ยนความโปร่งใสของ PDF.*

## การปรับเปลี่ยนทั่วไปและกรณีขอบ

| สถานการณ์ | วิธีปรับโค้ด |
|-----------|-----------------------|
| **หลายหน้า** | วนลูปผ่าน `document.Pages` และทำซ้ำขั้นตอนที่ 2‑8 สำหรับแต่ละหน้า. |
| **Blend mode ต่าง** | แทนที่ `"Normal"` ด้วย `"Multiply"`, `"Screen"` หรือชื่อ blend ใด ๆ ตามมาตรฐาน PDF. |
| **ความทึบของการเติมสูงขึ้น** | เปลี่ยน `new CosPdfNumber(0.5)` เป็นค่ารหว่าง `0` ถึง `1`. |
| **ไม่มี ExtGState ที่มีอยู่** | หาก `resourcesEditor["ExtGState"]` คืนค่า `null` ให้สร้างพจนานุกรมใหม่: `var extGState = CosPdfDictionary.CreateEmptyDictionary(document); resourcesEditor["ExtGState"] = extGState;` |

การปรับเปลี่ยนเหล่านี้แสดงให้เห็นถึงความยืดหยุ่นของการ **modify PDF resources** ด้วย Aspose.Pdf โดยการปรับพารามิเตอร์ คุณสามารถสร้างลายน้ำ, การซ้อนทับแบบกึ่งโปร่งใส, หรือองค์ประกอบ UI ที่กำหนดเองภายใน PDF

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในโครงการ Console App ใหม่ได้ มันประกอบด้วย `using` directives ที่จำเป็นทั้งหมด, การจัดการข้อผิดพลาด, และคอมเมนต์



## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดที่ทำงานได้ครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโครงการของคุณ

- [เปลี่ยนความทึบของ PDF ด้วย Aspose.PDF – คู่มือ C# ฉบับสมบูรณ์](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [เปลี่ยนความทึบของ PDF ใน C# – คู่มือ Aspose ฉบับสมบูรณ์](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [เพิ่มความโปร่งใสให้ PDF ด้วย Aspose – คู่มือ C# ฉบับสมบูรณ์](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}