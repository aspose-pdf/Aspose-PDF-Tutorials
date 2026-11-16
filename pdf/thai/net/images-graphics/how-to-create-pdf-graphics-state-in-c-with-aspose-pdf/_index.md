---
category: general
date: 2026-11-16
description: เรียนรู้วิธีสร้างสถานะกราฟิก PDF ใน C# ด้วย Aspose.Pdf คู่มือนี้ครอบคลุมความโปร่งใส
  โหมดผสม และตัวอย่างโค้ดเต็ม
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: th
lastmod: 2026-11-16
og_description: สร้างสถานะกราฟิก PDF ใน C# ด้วย Aspose.Pdf. ทำตามบทแนะนำฉบับเต็มนี้เพื่อกำหนดความทึบและโหมดผสมโดยโปรแกรม.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: สร้างสถานะกราฟิก PDF ใน C# – คู่มือ Aspose.Pdf ทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: วิธีสร้างสถานะกราฟิก PDF ใน C# ด้วย Aspose.Pdf
url: /th/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้าง PDF graphics state ใน C# ด้วย Aspose.Pdf

หากคุณต้องการ **create PDF graphics state** ในโครงการ .NET นี้ การสอนนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าต้องทำอย่างไรด้วย Aspose.Pdf ไม่ว่าคุณต้องการควบคุมความโปร่งใส, เปลี่ยนโหมดการผสม, หรือใช้ graphics state ที่กำหนดเองซ้ำหลายหน้า ขั้นตอนด้านล่างจะให้โซลูชันที่สมบูรณ์พร้อมใช้งาน

ในคู่มือนี้คุณจะได้เรียนรู้วิธีเข้าถึง resources ของหน้า, เพิ่มรายการ **ExtGState**, และบันทึกการเปลี่ยนแปลงลงในไฟล์ใหม่ ตัวอย่างทำงานกับ Aspose.Pdf 23.12 (หรือใหม่กว่า) และมุ่งเป้าไปที่ .NET 6+ แต่แนวคิดสามารถใช้กับเวอร์ชันก่อนหน้าได้เช่นกัน

## ข้อกำหนดเบื้องต้น

* Visual Studio 2022 (หรือ IDE C# ใดก็ได้) พร้อมติดตั้ง .NET 6 SDK  
* ใบอนุญาต Aspose.Pdf for .NET หรือคีย์ประเมินผลชั่วคราว  
* ไฟล์ PDF ชื่อ `input.pdf` ที่วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโค้ดได้  

ไม่จำเป็นต้องติดตั้งแพ็กเกจ NuGet เพิ่มเติมนอกจาก `Aspose.Pdf`.

## สิ่งที่การสอนนี้ครอบคลุม

* โหลดเอกสาร PDF ที่มีอยู่แล้ว  
* ไปยังพจนานุกรม resources ของหน้าแรก  
* สร้างพจนานุกรม graphics state ใหม่ที่กำหนดความโปร่งใสของเส้น (`CA`), ความโปร่งใสของการเติม (`ca`), และโหมดการผสม (`BM`)  
* เพิ่ม graphics state ใหม่เข้าไปในคอลเลกชัน **ExtGState** ด้วยชื่อที่กำหนดเอง (`GS0`)  
* บันทึก PDF ที่อัปเดตเพื่อให้คำสั่งการวาดต่อไปสามารถอ้างอิงสถานะใหม่ได้  

เมื่อจบการสอนคุณจะสามารถสร้างอ็อบเจ็กต์ **create PDF graphics state** อย่างโปรแกรมเมติกและใช้ซ้ำได้ในทุกการดำเนินการวาด

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และนำเข้า namespace

สร้างแอปพลิเคชันคอนโซลใหม่ (หรือรวมโค้ดเข้าในโปรเจกต์ที่มีอยู่) เพิ่มการอ้างอิง Aspose.Pdf และรวม namespace ที่จำเป็น:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **Pro tip:** หากคุณใช้เวอร์ชันประเมินฟรี ให้เพิ่ม `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` ก่อนโหลดเอกสารเพื่อหลีกเลี่ยงข้อความลายน้ำ

## ขั้นตอนที่ 2: โหลดเอกสาร PDF

การเปิดไฟล์ทำได้อย่างง่ายดาย คลาส `Document` แทนเอกสาร PDF ทั้งหมดและให้คุณเข้าถึงหน้าและ resources ของมัน

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

การวางโค้ดภายในบล็อก `using` รับประกันว่าการจัดการไฟล์จะถูกปล่อยหลังจากดำเนินการเสร็จ ซึ่งเป็นสิ่งสำคัญสำหรับ **C# PDF manipulation** ในบริการผลิต

## ขั้นตอนที่ 3: ดึงพจนานุกรม resources ของหน้าแรก

ทุกหน้าของ PDF มีพจนานุกรม *Resources* ที่เก็บฟอนต์, รูปภาพ, และ graphics state เราต้องการ `DictionaryEditor` เพื่อแก้ไขโครงสร้างนั้น

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

หาก PDF มีรายการ `ExtGState` อยู่แล้ว `resourcesEditor["ExtGState"]` จะคืนค่ามัน; มิฉะนั้น Aspose.Pdf จะสร้างพจนานุกรมเปล่าสำหรับเราเมื่อเราเพิ่มรายการแรก

## ขั้นตอนที่ 4: เข้าถึงหรือสร้างพจนานุกรม ExtGState

พจนานุกรม **ExtGState** เก็บอ็อบเจ็กต์ graphics state ที่มีชื่อ เราจะดึงอ็อบเจ็กต์ที่มีอยู่หรือสร้างคอนเทนเนอร์ใหม่

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

เมื่อ `ExtGState` ไม่มีอยู่ `resourcesEditor["ExtGState"]` จะคืนพจนานุกรมเปล่าใหม่โดยอัตโนมัติ ทำให้โค้ดทำงานกับ PDF ใดก็ได้

## ขั้นตอนที่ 5: สร้างพจนานุกรม graphics state ใหม่

graphics state คือ `CosPdfDictionary` ที่มีคีย์เฉพาะ:

* `CA` – ความโปร่งใสของเส้น (0‑1)  
* `ca` – ความโปร่งใสของการเติม (0‑1)  
* `BM` – โหมดการผสม (`Normal`, `Multiply`, เป็นต้น)

เราจะสร้างพจนานุกรมเปล่า เติมค่าลงไป แล้วเพิ่มลงใน `ExtGState`

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

คุณสามารถเปลี่ยน `0.5` เป็นค่าใดก็ได้ระหว่าง `0` ถึง `1` เพื่อปรับความโปร่งใสของการเติม, หรือเปลี่ยน `"Normal"` เป็น `"Multiply"` เพื่อใช้ **PDF blend mode** ที่แตกต่าง ความยืดหยุ่นนี้เป็นเหตุผลที่การสร้าง graphics state ที่กำหนดเองเป็นเทคนิคที่ทรงพลังในการจัดการ **Aspose.Pdf graphics state**

## ขั้นตอนที่ 6: ลงทะเบียน graphics state ด้วยชื่อ

PDF content streams อ้างอิง graphics state ด้วยชื่อ ที่นี่เราใช้ `GS0` แต่ชื่อใดที่ไม่ซ้ำก็ได้

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

หากต้องการหลายสถานะ ให้ทำขั้นตอนการสร้างซ้ำด้วยพารามิเตอร์ต่างกันและเพิ่มเป็น `GS1`, `GS2` เป็นต้น รูปแบบนี้ขยายได้ดีสำหรับเอกสารซับซ้อนที่ต้องการความโปร่งใสหรือการตั้งค่า blend ที่แตกต่างกันในแต่ละเลเยอร์

## ขั้นตอนที่ 7: บันทึก PDF ที่แก้ไขแล้ว

สุดท้ายให้เขียนเอกสารที่อัปเดตลงในไฟล์ใหม่ การรักษาไฟล์ต้นฉบับไว้ไม่เปลี่ยนแปลงช่วยให้การดีบักง่ายขึ้น

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

หลังจากรันเสร็จ `output.pdf` จะมีรายการ `ExtGState` ชื่อ `GS0` ตัวดำเนินการวาดต่อไปสามารถอ้างอิงมันด้วยตัวดำเนินการ `gs` (เช่น `GS0 gs` ในสตรีมเนื้อหา)  

> **Why this matters:** การสร้าง graphics state ที่ใช้ซ้ำได้ช่วยหลีกเลี่ยงการตั้งค่าความโปร่งใสและ blend ซ้ำสำหรับแต่ละคำสั่งวาด ซึ่งทำให้ประสิทธิภาพและการบำรุงรักษาดีขึ้น

## การใช้ graphics state ใหม่ในสตรีมเนื้อหา (ทางเลือก)

หากคุณต้องการเห็นผลทันที คุณสามารถเพิ่มสี่เหลี่ยมง่าย ๆ ที่ใช้สถานะที่เราสร้างขึ้น

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

สี่เหลี่ยมจะถูกวาดด้วยความโปร่งใสของการเติม 50 % ในขณะที่เส้นขอบยังคงเต็มที่ตามที่กำหนดในพจนานุกรม **create PDF graphics state**

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| `ExtGState` entry not found | PDF บางไฟล์ไม่มีพจนานุกรมนี้เลย | `DictionaryEditor` จะสร้างโดยอัตโนมัติเมื่อคุณเพิ่มรายการแรก ดังนั้นไม่จำเป็นต้องตรวจสอบเพิ่มเติม |
| Opacity values > 1 or < 0 | สเปค PDF จำกัดความโปร่งใสในช่วง `[0,1]` | จำกัดค่าก่อนสร้าง `CosPdfNumber` |
| Blend mode typo | ชื่อ Blend mode ของ PDF แยกแยะตัวพิมพ์ใหญ่‑เล็ก | ใช้ชื่อที่ตรงกันเช่น `"Normal"`, `"Multiply"`, `"Screen"` |
| License watermark | เวอร์ชันประเมินเพิ่มลายน้ำบนหน้าแรก | ใช้ไฟล์ใบอนุญาตที่ถูกต้องก่อนเปิดเอกสาร |

การจัดการกับกรณีขอบเหล่านี้ทำให้การใช้งาน **create PDF graphics state** ของคุณทำงานอย่างเชื่อถือได้กับแหล่ง PDF ต่าง ๆ

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นโปรแกรมที่สมบูรณ์แบบซึ่งคุณสามารถคัดลอก, วาง, และรันได้ แทนที่ `YOUR_DIRECTORY` ด้วยเส้นทางโฟลเดอร์จริงบนเครื่องของคุณ



## คุณควรเรียนรู้อะไรต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโครงการของคุณ

- [สร้าง graphics state แบบกำหนดเองใน PDF ด้วย Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [เพิ่ม graphics state ไปยัง PDF ด้วย Aspose.PDF for .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [วิธีสร้าง graphics state ว่างใน PDF ด้วย C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}