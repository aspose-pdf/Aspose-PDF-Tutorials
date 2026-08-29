---
category: general
date: 2026-08-20
description: สร้างสถานะกราฟิกแบบกำหนดเองใน PDF ด้วย Aspose.Pdf เรียนรู้วิธีแก้ไขทรัพยากร
  PDF และเพิ่มความโปร่งใสให้ PDF เพียงไม่กี่ขั้นตอน.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: th
lastmod: 2026-08-20
og_description: สร้างสถานะกราฟิกแบบกำหนดเองใน PDF ด้วย Aspose.Pdf. บทเรียนนี้แสดงวิธีแก้ไขทรัพยากร
  PDF และเพิ่มความโปร่งใสให้ PDF อย่างรวดเร็ว.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: สร้างสถานะกราฟิกแบบกำหนดเองใน PDF – คู่มือ Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: สร้างสถานะกราฟิกแบบกำหนดเองใน PDF ด้วย Aspose.Pdf
url: /th/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างกราฟิกสเตตส์แบบกำหนดเองใน PDF ด้วย Aspose.Pdf

หากคุณต้องการ **สร้างกราฟิกสเตตส์แบบกำหนดเอง** ใน PDF คู่มือนี้จะแสดงให้คุณเห็นอย่างละเอียดว่าทำอย่างไรด้วย Aspose.Pdf สำหรับ .NET เมื่อจบบทเรียนคุณจะสามารถ **แก้ไขทรัพยากร PDF**, แทรกพจนานุกรมกราฟิก‑สเตตส์ใหม่, และ **เพิ่มเนื้อหา PDF ที่มีความโปร่งใส** ได้โดยไม่ต้องออกจากโปรเจกต์ C# ของคุณ

คุณจะได้เห็นตัวอย่างที่ทำงานได้เต็มรูปแบบ, คำอธิบายว่าทำไมแต่ละบรรทัดจึงสำคัญ, และเคล็ดลับสำหรับการจัดการเอกสารหลายหน้า หรือโหมดผสมต่าง ๆ ไม่ต้องใช้เครื่องมือภายนอก—เพียงแค่ไลบรารี Aspose.Pdf และสภาพแวดล้อมการพัฒนา .NET เบื้องต้น

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานได้กับ .NET Framework 4.7+)
* สำเนาไลเซนส์ของ **Aspose.Pdf for .NET** (รุ่นทดลองฟรีใช้สำหรับทดสอบได้)
* ไฟล์ PDF อินพุตชื่อ `input.pdf` ที่วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโค้ดได้
* Visual Studio 2022 หรือ IDE ใด ๆ ที่รองรับการพัฒนา C#

บทเรียนนี้สมมติว่าคุณคุ้นเคยกับไวยากรณ์พื้นฐานของ C# และแนวคิดของหน้า PDF

## ขั้นตอนที่ 1: โหลด PDF ต้นฉบับและเข้าถึงหน้าแรก

การดำเนินการแรกคือเปิดไฟล์ PDF และดึงหน้าที่คุณต้องการแก้ไขทรัพยากร Aspose.Pdf แสดงแต่ละหน้าเป็นอ็อบเจกต์ `Page` และทุกหน้ามีพจนานุกรม **resource dictionary** ที่เก็บกราฟิกสเตตส์, ฟอนต์, XObjects และอื่น ๆ

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*ทำไมจึงสำคัญ:* คลาส `Document` โหลดไฟล์เข้าสู่หน่วยความจำ, และ `Pages[1]` ให้คุณเข้าถึงพจนานุกรมทรัพยากรของหน้าแรกโดยตรง ซึ่งเป็นที่ที่กราฟิกสเตตส์อาศัยอยู่

## ขั้นตอนที่ 2: เปิดพจนานุกรมทรัพยากรเพื่อแก้ไข

Aspose.Pdf มีตัวช่วย `DictionaryEditor` ที่ทำให้คุณจัดการพจนานุกรมทรัพยากรเหมือนกับ `Dictionary` ของ .NET ปกติ ทำให้การอ่าน, เพิ่ม หรือแทนที่รายการเช่น `ExtGState` เป็นเรื่องง่าย

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*ทำไมจึงสำคัญ:* `DictionaryEditor` แยกความซับซ้อนของวัตถุ COS ระดับต่ำออก, ให้คุณทำงานกับคู่คีย์/ค่าแบบที่คุ้นเคยในขณะยังคงรักษาความสอดคล้องของ PDF ไว้

## ขั้นตอนที่ 3: ดึง (หรือสร้าง) พจนานุกรม ExtGState

รายการ **ExtGState** เก็บอ็อบเจกต์กราฟิกสเตตส์ภายนอกทั้งหมดของหน้า หากพจนานุกรมไม่มีอยู่, Aspose.Pdf จะสร้างพจนานุกรมเปล่าสำหรับคุณ

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*ทำไมจึงสำคัญ:* หากไม่มีรายการ `ExtGState` จะทำให้เกิด `KeyNotFoundException` ในภายหลัง การตรวจสอบนี้ทำให้โค้ดทำงานกับ PDF ที่ไม่เคยกำหนดกราฟิกสเตตส์แบบกำหนดเองมาก่อน—เป็นส่วนสำคัญของความทนทานในการ **แก้ไขทรัพยากร PDF**

## ขั้นตอนที่ 4: สร้างพจนานุกรมกราฟิกสเตตส์แบบกำหนดเอง

กราฟิกสเตตส์อธิบายวิธีการเรนเดอร์การวาดรูป เพื่อ **เพิ่มเนื้อหา PDF ที่มีความโปร่งใส** คุณต้องตั้งค่ารายการ `ca` (ความทึบของการเติม) และ `CA` (ความทึบของการขีด) และอาจเพิ่มโหมดผสม (`BM`) โค้ดต่อไปนี้สร้างพจนานุกรมใหม่พร้อมพารามิเตอร์เหล่านั้น

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*ทำไมจึงสำคัญ:* รายการ `ca` และ `CA` ควบคุมความโปร่งใสสำหรับการเติมและการขีดตามลำดับ การตั้งค่า `BM` ให้คุณทดลองเอฟเฟกต์การผสมต่าง ๆ ซึ่งมีประโยชน์เมื่อคุณต่อไป **เพิ่มเนื้อหา PDF ที่มีความโปร่งใส** เช่น รูปร่างหรือภาพที่กึ่งโปร่งใส

## ขั้นตอนที่ 5: ลงทะเบียนกราฟิกสเตตส์ใหม่ภายใต้ชื่อที่ไม่ซ้ำกัน

กราฟิกสเตตส์แต่ละตัวในพจนานุกรม `ExtGState` ต้องมีชื่อที่ไม่ซ้ำกัน (เช่น `GS0`, `GS1`). คุณสามารถเลือกชื่อใดก็ได้ที่ไม่ชนกับรายการที่มีอยู่

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*ทำไมจึงสำคัญ:* การใส่พจนานุกรมใหม่ภายใต้ `GS0` ทำให้สเตตส์สามารถอ้างอิงได้จากสตรีมเนื้อหาของหน้า บล็อกเงื่อนไขทำให้แน่ใจว่ามีรายการ `ExtGState` แม้สำหรับ PDF ที่เริ่มต้นโดยไม่มีรายการนี้—เป็นการป้องกันเพิ่มเติมในการ **แก้ไขทรัพยากร PDF**

## ขั้นตอนที่ 6: ใช้กราฟิกสเตตส์แบบกำหนดเองในเนื้อหาของหน้า (ไม่บังคับ)

ขั้นตอนก่อนหน้านี้เพียง *กำหนด* กราฟิกสเตตส์เท่านั้น เพื่อให้เห็นผลจริงคุณต้องอ้างอิงสเตตส์นี้ในสตรีมเนื้อหาของหน้า ตัวอย่างสั้น ๆ ด้านล่างวาดสี่เหลี่ยมกึ่งโปร่งใสโดยใช้สเตตส์ที่สร้างขึ้น

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*ทำไมจึงสำคัญ:* ตัวดำเนินการ `SetExtGState` (`gs`) บอกเรนเดอร์ของ PDF ให้ใช้พารามิเตอร์ที่กำหนดใน `GS0` สี่เหลี่ยมจะปรากฏด้วยความทึบการเติม 50 % ในขณะที่เส้นขอบยังคงเต็มความทึบ

## ขั้นตอนที่ 7: บันทึก PDF ที่แก้ไขแล้ว

สุดท้ายให้เขียนการเปลี่ยนแปลงกลับไปยังดิสก์ คุณสามารถเขียนทับไฟล์ต้นฉบับหรือสร้างไฟล์ใหม่ได้

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

เมื่อคุณเปิด `output_with_custom_gs.pdf` ในโปรแกรมดู PDF คุณควรเห็นสี่เหลี่ยมกึ่งโปร่งใสบนหน้าแรก ซึ่งยืนยันว่าคุณได้ **สร้างกราฟิกสเตตส์แบบกำหนดเอง**, **แก้ไขทรัพยากร PDF**, และ **เพิ่มเนื้อหา PDF ที่มีความโปร่งใส** อย่างสำเร็จ

## ความแปรผันทั่วไปและกรณีขอบ

| สถานการณ์ | สิ่งที่ต้องปรับ |
|-----------|----------------|
| **หลายหน้าต้องการสเตตส์เดียวกัน** | ลงทะเบียนกราฟิกสเตตส์ครั้งเดียว (ขั้นตอน 1‑5) แล้วอ้างอิง `GS0` ในสตรีมเนื้อหาของหน้าใดก็ได้ |
| **ความทึบต่างกันตามองค์ประกอบ** | กำหนดสเตตส์เพิ่มเติม (`GS1`, `GS2`, …) ด้วยค่า `ca`/`CA` ที่ต่างกันและสลับใช้โดย `SetExtGState` |
| **โหมดผสมไม่ใช่ Normal** | แทนที่ `"Normal"` ด้วย `"Multiply"`, `"Screen"` หรือโหมดผสมมาตรฐานของ PDF ใด ๆ ในรายการ `BM` |
| **ชื่อชนกัน** | ก่อนเพิ่มให้ตรวจสอบ `extGStateDict.ContainsKey(yourName)` แล้วเลือกส่วนต่อท้ายที่ไม่ซ้ำ |
| **PDF มีพจนานุกรม ExtGState อยู่แล้ว** | โค้ดในขั้นตอน 3 จะใช้พจนานุกรมที่มีอยู่แล้ว ดังนั้นไม่ต้องทำการจัดการเพิ่มเติม |

**เคล็ดลับมืออาชีพ:** เมื่อทำงานกับ PDF ขนาดใหญ่ ให้ห่อการใช้ `Document` ด้วยบล็อก `using` (ตามตัวอย่าง) เพื่อปล่อยทรัพยากรเนทีฟโดยเร็ว นอกจากนี้ควรพิจารณาเปิดใช้งานคุณสมบัติ `PdfCompliance` ของ Aspose.Pdf หากต้องการรับประกันการสอดคล้องตามมาตรฐาน PDF/A หรือ PDF/X หลังจากแก้ไขทรัพยากร

## ตัวอย่างทำงานเต็มรูปแบบ

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Load the PDF you want to edit
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Step 1: Get the first page
            Page firstPage = pdfDocument.Pages[1];

            // Step 2: Open the page resources for editing
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 3: Retrieve or create the ExtGState dictionary
            var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
                ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
                : new CosPdfDictionary(pdfDocument);

            // Step 4: Build a custom graphics state (50 % fill opacity, 100 % stroke opacity)
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var param in graphicsStateParams)
                newGraphicsState.Add(param);

            // Step 5: Register the graphics state under the name GS0
            const string graphicsStateName = "GS0";
            extGStateDict.Add(graphicsStateName, newGraphics


## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบต่าง ๆ ในโปรเจกต์ของคุณเอง

- [วิธีสร้าง PDF ด้วย Aspose – เพิ่มฟิลด์ฟอร์มและหน้า](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [วิธีสร้างตารางแบบกำหนดเองใน PDF ด้วย Aspose.PDF .NET](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [สร้างตรา PDF แบบกำหนดเอง Aspose Pdf Net](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}