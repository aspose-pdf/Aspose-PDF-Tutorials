---
category: general
date: 2026-11-12
description: เรียนรู้วิธีเปลี่ยนความทึบของ PDF ด้วย Aspose.Pdf, เพิ่มความโปร่งใส,
  ตั้งค่าโหมดผสม, และบันทึก PDF ที่แก้ไขใน C#
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: th
lastmod: 2026-11-12
og_description: เปลี่ยนความโปร่งใสของ PDF ด้วย Aspose.Pdf, เรียนรู้วิธีเพิ่มความโปร่งใส,
  ตั้งค่าโหมดผสม, และบันทึกไฟล์ PDF ที่แก้ไขใน C#
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: เปลี่ยนความทึบของ PDF ด้วย Aspose.Pdf – เพิ่มความโปร่งใสและบันทึก
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: เปลี่ยนความทึบของ PDF ด้วย Aspose.Pdf และบันทึกไฟล์
url: /th/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เปลี่ยนความทึบของ PDF ด้วย Aspose.Pdf และบันทึกไฟล์

หากคุณต้องการ **เปลี่ยนความทึบของ PDF** ในเอกสาร, Aspose.Pdf มี API ที่ใช้งานง่ายเพื่อปรับความโปร่งใสของเส้นขอบและการเติมสี. บทเรียนนี้จะแสดงอย่างชัดเจน **วิธีเพิ่มความโปร่งใส**, **วิธีตั้งค่าโหมดผสม**, และ **บันทึกไฟล์ PDF ที่แก้ไข** ด้วยเพียงไม่กี่บรรทัดของโค้ด C#.

คุณจะได้เดินผ่านทุกขั้นตอน—ตั้งแต่การโหลด PDF ที่มีอยู่ไปจนถึงการกำหนดกราฟิกสเตตใหม่และบันทึกการเปลี่ยนแปลง. เมื่อจบคู่มือนี้คุณจะสามารถ:

* ลดการมองเห็นของกราฟิกเวกเตอร์หรือรูปภาพ
* ใช้โหมดผสมแบบกำหนดเองเช่น *Normal* หรือ *Multiply*
* ส่งออกไฟล์ที่อัปเดตโดยไม่สูญเสียเนื้อหาอื่นใด

ข้อกำหนดเบื้องต้นเพียงอย่างเดียวคือสภาพแวดล้อมการพัฒนา .NET ที่ทำงานได้และการอ้างอิงถึงไลบรารี Aspose.Pdf (เวอร์ชัน 23.9 หรือใหม่กว่า). ไม่จำเป็นต้องใช้เครื่องมือภายนอก.

## ข้อกำหนดเบื้องต้น

| ข้อกำหนด | เหตุผลที่สำคัญ |
|-------------|----------------|
| .NET 6.0 SDK หรือใหม่กว่า | รับประกันความเข้ากันได้กับ API ของ Aspose.Pdf เวอร์ชันล่าสุด |
| แพคเกจ NuGet Aspose.Pdf สำหรับ .NET | จัดเตรียมคลาส `Document`, `CosPdfDictionary` และคลาสที่เกี่ยวข้องที่ใช้ในโค้ด |
| ไฟล์ PDF เพื่อแก้ไข (เช่น `input.pdf`) | ทำหน้าที่เป็นแหล่งข้อมูลสำหรับการเปลี่ยนความทึบ |

Install the NuGet package with:

```bash
dotnet add package Aspose.Pdf
```

## เปลี่ยนความทึบของ PDF ด้วย Aspose.Pdf

### ขั้นตอนที่ 1: โหลดเอกสาร PDF

เริ่มต้นด้วยการสร้างอินสแตนซ์ `Document` ที่ชี้ไปยังไฟล์ต้นทางของคุณ. ตัวสร้างจะอ่าน PDF ทั้งหมดเข้าสู่หน่วยความจำ, ทำให้คุณสามารถจัดการกับอ็อบเจ็กต์ภายในได้.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **ทำไมต้องทำขั้นตอนนี้?** การโหลดไฟล์จะสร้างโมเดลอ็อบเจ็กต์ที่สามารถจัดการได้. การเปลี่ยนแปลงทั้งหมดต่อมาจะทำงานบนการแสดงผลในหน่วยความจำนี้, ทำให้ไฟล์ต้นฉบับยังคงไม่ถูกแก้ไขจนกว่าคุณจะบันทึกอย่างชัดเจน.

### ขั้นตอนที่ 2: เข้าถึงทรัพยากรของหน้าที่หนึ่ง

แต่ละหน้าของ PDF จะเก็บ *resource dictionary* ที่บรรจุอ็อบเจ็กต์เช่น ฟอนต์, รูปภาพ, และกราฟิกสเตต. คุณจำเป็นต้องแก้ไขพจนานุกรมนี้เพื่อใส่รายการ `ExtGState` ใหม่.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **เคล็ดลับ:** หาก PDF ของคุณมีหลายหน้าและต้องการความทึบเดียวกัน, ให้ทำซ้ำขั้นตอนนี้สำหรับแต่ละหน้า หรือใช้ `ExtGState` เดียวกันระหว่างหลายหน้า.

### ขั้นตอนที่ 3: ตรวจสอบให้แน่ใจว่ามีพจนานุกรม ExtGState อยู่

พจนานุกรม `ExtGState` จะเก็บกราฟิกสเตตแบบกำหนดเอง. หากไม่มี, โค้ดจะสร้างขึ้นโดยอัตโนมัติ.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **ทำไมต้องทำขั้นตอนนี้?** หากไม่มีคอนเทนเนอร์ `ExtGState`, การอ้างอิงกราฟิกสเตตใหม่ใด ๆ จะล้มเหลว, ทำให้ PDF ไม่รับการตั้งค่าความทึบของคุณ.

### ขั้นตอนที่ 4: กำหนดกราฟิกสเตตใหม่ (ExtGState)

กราฟิกสเตตกำหนดพฤติกรรมของการวาด. พจนานุกรมต่อไปนี้ตั้งค่าความทึบของเส้น (`CA`), ความทึบของการเติม (`ca`), และโหมดผสม (`BM`).

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **วิธีตั้งค่าความทึบของการเติม:** รายการ `ca` ควบคุมความทึบของรูปทรงที่เติม (ข้อความ, เส้นทาง). ปรับค่าตัวเลขระหว่าง `0` (โปร่งใสเต็ม) และ `1` (ทึบเต็ม) ให้ตรงกับความต้องการออกแบบของคุณ.

> **วิธีตั้งค่าโหมดผสม:** รายการ `BM` เลือกอัลกอริทึมการผสม. ค่าที่พบบ่อยได้แก่ `Normal`, `Multiply`, `Screen`, และ `Overlay`. เลือกค่าที่ตรงกับเจตนาภาพของคุณ.

### ขั้นตอนที่ 5: ลงทะเบียนกราฟิกสเตตในพจนานุกรมทรัพยากร

ตั้งชื่อให้สเตตใหม่ (เช่น `GS0`) และเพิ่มลงในพจนานุกรม `ExtGState`. ชื่อนี้จะถูกอ้างอิงต่อไปในสตรีมเนื้อหาของหน้า.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **เคล็ดลับระดับมืออาชีพ:** ใช้รูปแบบการตั้งชื่อเช่น `GS0`, `GS1`, … เมื่อคุณสร้างหลายสเตต. จะช่วยป้องกันการชนชื่อและทำให้การดีบักง่ายขึ้น.

### ขั้นตอนที่ 6: ใช้กราฟิกสเตตกับเนื้อหาของหน้า

เพื่อให้เห็นผลของความทึบ, แทรกตัวดำเนินการ `/GS0 gs` ก่อนคำสั่งวาดที่คุณต้องการให้มีผล. ตัวอย่างด้านล่างวาดสี่เหลี่ยมที่มีความทึบกึ่งโปร่งใส.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **ทำไมต้องใช้ตัวดำเนินการ `q` และ `Q`?** พวกมันทำการ push และ pop สแต็กของกราฟิกสเตต, ทำให้การเปลี่ยนความทึบส่งผลเฉพาะสี่เหลี่ยมและไม่กระทบส่วนอื่นของหน้า.

### ขั้นตอนที่ 7: บันทึก PDF ที่แก้ไขแล้ว

สุดท้าย, เขียนเอกสารที่อัปเดตลงดิสก์. เมธอด `Save` จะเขียนทับไฟล์เป้าหมายหรือสร้างไฟล์ใหม่หากไม่มี.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **วิธีบันทึก PDF ที่แก้ไข:** การเรียก `Save` จะเขียนการแก้ไขทั้งหมดในหน่วยความจำ, รวมถึง `ExtGState` ใหม่, ไปยังพาธที่ระบุ. คุณยังสามารถสตรีมผลลัพธ์ไปยัง `MemoryStream` สำหรับการตอบสนองเว็บได้.

## ตัวอย่างการทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเดียวที่ทำงานอิสระซึ่งรวมทุกขั้นตอนที่อธิบายไว้ข้างต้น. คัดลอกไปยังแอปพลิเคชันคอนโซลและรันเพื่อยืนยันการเปลี่ยนความทึบ.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Operators;

class ChangePdfOpacityDemo
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get first page and its resources
        var page = pdfDoc.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3. Ensure ExtGState dictionary exists
        var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                             ?? new CosPdfDictionary(pdfDoc);
        resourcesEditor["Ext


## สิ่งที่คุณควรเรียนต่อไป

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งข้อมูลรวมตัวอย่างโค้ดที่ทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการดำเนินการทางเลือกในโครงการของคุณ.

- [วิธีบันทึก PDF ที่แก้ไขด้วย Aspose.Pdf และเพิ่มความโปร่งใส](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [วิธีเพิ่มความโปร่งใสให้ PDF ด้วย Aspose.PDF ใน C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [วิธีเพิ่มกราฟิกสเตต PDF และควบคุมความโปร่งใสด้วย Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}