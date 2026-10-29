---
category: general
date: 2026-10-13
description: เรียนรู้วิธีตั้งค่าความโปร่งใสในไฟล์ PDF ด้วย Aspose.Pdf สำหรับ C# และดูวิธีบันทึก
  PDF ที่แก้ไขแล้วพร้อมเปลี่ยนค่า fill alpha.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- save modified pdf
- change fill alpha
- set fill opacity
- edit pdf resources
language: th
lastmod: 2026-10-13
og_description: วิธีตั้งค่าความโปร่งใสใน PDF ด้วย Aspose.Pdf สำหรับ C# ปฏิบัติตามคำแนะนำนี้เพื่อแก้ไขทรัพยากร
  PDF, เปลี่ยนค่า fill alpha, และบันทึกไฟล์ PDF ที่แก้ไขแล้ว.
og_image_alt: Screenshot of a PDF page showing transparent graphics applied with Aspose.Pdf
  in C#
og_title: วิธีตั้งค่าความโปร่งใสใน PDF ด้วย Aspose.Pdf C# – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  headline: How to set transparency in a PDF with Aspose.Pdf C#
  type: TechArticle
- description: Learn how to set transparency in a PDF with Aspose.Pdf for C#. Also
    see how to save modified PDF and change fill alpha.
  name: How to set transparency in a PDF with Aspose.Pdf C#
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf; using System.Collections.Generic;'
  - name: Edit PDF resources to add a graphics state
    text: '```csharp // Get the first page (pages are 1‑based) Page firstPage = pdfDocument.Pages[1];'
  - name: Change fill alpha and set fill opacity
    text: '```csharp // Create an empty graphics state dictionary CosPdfDictionary
      newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Register the new state under the name "GS0" extGStateDict.Add("GS0",
      newGraphicsState); ```'
  - name: (Optional) Apply the graphics state in a content stream
    text: 'If you want to draw a rectangle using the new fill opacity, add the following
      after the previous steps:'
  - name: Save modified PDF
    text: '```csharp // Persist the changes to a new file pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      ```'
  - name: Next steps
    text: '* Explore other blend modes (`Multiply`, `Screen`, etc.) by changing the
      `BM` entry. * Adjust stroke alpha (`CA`) to create semi‑transparent outlines.
      * Combine multiple graphics states to build a library of reusable visual effects.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: วิธีตั้งค่าความโปร่งใสใน PDF ด้วย Aspose.Pdf C#
url: /th/net/images-graphics/how-to-set-transparency-in-a-pdf-with-aspose-pdf-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีตั้งค่าความโปร่งใสใน PDF ด้วย Aspose.Pdf C#

หากคุณต้องการตั้งค่าความโปร่งใสใน PDF ด้วย C# บทแนะนำนี้จะแสดงขั้นตอนที่แน่นอน คุณจะได้เรียนรู้วิธีบันทึกไฟล์ PDF ที่แก้ไขแล้วและเปลี่ยนค่า fill alpha โดยไม่ต้องออกจากสภาพแวดล้อมของ Aspose.Pdf

คู่มือจะพาคุณผ่านการโหลดเอกสาร, การแก้ไขทรัพยากร PDF, การสร้าง graphics state ที่กำหนดค่า fill opacity, และการบันทึกการเปลี่ยนแปลง ไม่จำเป็นต้องใช้เครื่องมือภายนอก; ทุกอย่างทำงานภายในโครงการ .NET มาตรฐาน

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า ที่ติดตั้งแล้ว  
* ใบอนุญาต Aspose.Pdf for .NET ที่ถูกต้อง (หรือคีย์ทดลองฟรี)  
* ไฟล์ PDF อินพุตที่อยู่ในไดเรกทอรีที่ทราบตำแหน่ง  

คุณสามารถเพิ่มแพคเกจ Aspose.Pdf ผ่าน NuGet ได้ดังนี้:

```bash
dotnet add package Aspose.Pdf
```

## วิธีตั้งค่าความโปร่งใสใน PDF

ส่วนนี้ประกอบด้วยการทำงานหลักของโค้ด แต่ละขั้นตอนอธิบาย **ทำไม** โค้ดจึงจำเป็น, ไม่ใช่แค่ **ทำอะไร**

### ขั้นตอน 1: โหลดเอกสาร PDF

```csharp
using Aspose.Pdf;
using System.Collections.Generic;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*ทำไมต้องทำขั้นตอนนี้?*  
`Document` แทนไฟล์ PDF ทั้งหมดในหน่วยความจำ การเปิดไฟล์ทำให้คุณเข้าถึงหน้า, ทรัพยากร, และอ็อบเจกต์ระดับต่ำที่คุณจะทำการแก้ไข

### ขั้นตอน 2: แก้ไขทรัพยากร PDF เพื่อเพิ่ม graphics state

```csharp
// Get the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Create an editor for the page's resource dictionary
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

// Retrieve the ExtGState dictionary; it holds graphics state objects
CosPdfDictionary extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
```

*ทำไมต้องทำขั้นตอนนี้?*  
หน้า PDF เก็บอ็อบเจกต์ที่ใช้ซ้ำได้—ฟอนต์, รูปภาพ, และ graphics state—ใน resource dictionary รายการ `ExtGState` มีการตั้งค่าความโปร่งใส การแก้ไข dictionary นี้ทำให้คุณสามารถเพิ่มสถานะใหม่ที่หน้าจะอ้างอิงได้

### ขั้นตอน 3: เปลี่ยนค่า fill alpha และตั้งค่า fill opacity

```csharp
// Create an empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Define the graphics state entries
var graphicsStateEntries = new[]
{
    // Stroke alpha (CA) – fully opaque
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    // Fill alpha (ca) – 50 % transparent
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    // Blend mode (BM) – normal composition
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

// Populate the new graphics state
foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*ทำไมต้องทำขั้นตอนนี้?*  
`ca` ควบคุม **fill opacity**, ส่วน `CA` ควบคุม **stroke opacity** การตั้งค่า `ca` เป็น `0.5` ทำให้รูปทรงที่เติมสีมีความโปร่งใส 50 % รายการ `BM` เลือกโหมดผสม; `"Normal"` เป็นตัวเลือกที่ใช้บ่อยที่สุดสำหรับความโปร่งใสมาตรฐาน

### ขั้นตอน 4: เพิ่ม graphics state ใหม่ลงใน dictionary ExtGState

```csharp
// Register the new state under the name "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

*ทำไมต้องทำขั้นตอนนี้?*  
การตั้งชื่อ graphics state (`"GS0"`) ทำให้ content stream บนหน้าอ้างอิงได้ด้วย operator `gs` หลังจากลงทะเบียนนี้ หน้า PDF จะสามารถใช้ความโปร่งใสที่คุณกำหนดได้

### ขั้นตอน 5: (ทางเลือก) ใช้ graphics state ใน content stream

หากคุณต้องการวาดสี่เหลี่ยมโดยใช้ fill opacity ใหม่ ให้เพิ่มโค้ดต่อไปนี้หลังจากขั้นตอนก่อนหน้า:

```csharp
// Create a content stream that uses the new graphics state
string cs = @"
q               % Save graphics state
/GS0 gs         % Apply the graphics state defined earlier
0 0 200 100 re  % Define a rectangle (x, y, width, height)
0.2 0.6 0.8 rg  % Set fill color (RGB)
f               % Fill the rectangle using the current graphics state
Q               % Restore graphics state
";

firstPage.Contents.Add(new Aspose.Pdf.Operator.GsContent(cs));
```

*ทำไมต้องทำขั้นตอนนี้?*  
operator `q`/`Q` จะบันทึกและคืนค่า graphics state, ทำให้ความโปร่งใสส่งผลเฉพาะคำสั่งการวาดที่ต้องการเท่านั้น operator `gs` จะสลับไปยัง graphics state ที่ชื่อ `"GS0"`

### ขั้นตอน 6: บันทึก PDF ที่แก้ไขแล้ว

```csharp
// Persist the changes to a new file
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*ทำไมต้องทำขั้นตอนนี้?*  
การบันทึกจะเขียน resource dictionary ที่อัปเดตและ content stream ใหม่ใด ๆ ลงดิสก์ ไฟล์ที่ได้ (`output.pdf`) จะมีสี่เหลี่ยมโปร่งใสที่กำหนดในขั้นตอนก่อนหน้า

## ตัวอย่างที่สามารถรันได้เต็มรูปแบบ

เมื่อนำส่วนต่าง ๆ มารวมกัน นี่คือโปรแกรมเต็มรูปแบบที่คุณสามารถคอมไพล์และรันได้:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class SetTransparencyDemo
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Access the first page and its resources
        Page firstPage = pdfDocument.Pages[1];
        var resourceEditor = new DictionaryEditor(firstPage.Resources);
        var extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();

        // Create a new graphics state with 50 % fill opacity
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke alpha
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill alpha
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // Register the graphics state as "GS0"
        extGStateDict.Add("GS0", newGraphicsState);

        // Optional: draw a rectangle using the new transparency
        string cs = @"
q
/GS0 gs
0 0 200 100 re
0.2 0.6 0.8 rg
f
Q
";
        firstPage.Contents.Add(new GsContent(cs));

        // Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

**ผลลัพธ์ที่คาดหวัง** – `output.pdf` แสดงสี่เหลี่ยมที่เติมด้วยสีม่วงอ่อนที่มีความโปร่งใส 50 % ทำให้เนื้อหาเบื้องหลังใด ๆ สามารถมองเห็นได้บางส่วน

## คำถามทั่วไปและกรณีขอบ

* **ฉันสามารถเปลี่ยน stroke opacity แทน fill opacity ได้หรือไม่?**  
  ตั้งค่าของ `CA` (ตัวอักษรพิมพ์ใหญ่) เป็นตัวเลขระหว่าง `0` (โปร่งใสเต็ม) ถึง `1` (ทึบเต็ม) ตัวอย่างได้ตั้งค่า `CA` เป็น `1` ซึ่งหมายความว่าเส้นขอบยังคงทึบ  

* **ถ้าหน้ายังไม่มี dictionary ExtGState จะทำอย่างไร?**  
  `resourceEditor["ExtGState"]` จะสร้าง dictionary ว่างโดยอัตโนมัติ การเพิ่ม `"GS0"` จะทำงานเช่นเดียวกัน  

* **graphics state สามารถใช้ซ้ำได้หลายหน้าหรือไม่?**  
  ได้. เมื่อคุณเพิ่มรายการลงใน resource dictionary ของเอกสาร หน้าใด ๆ ที่อ้างอิง `"GS0"` จะสืบทอดการตั้งค่าความโปร่งใสเดียวกัน  

* **วิธีนี้แตกต่างจากการใช้ `Graphics` API ระดับสูงอย่างไร?**  
  การแก้ไข resource dictionary ระดับต่ำให้คุณควบคุมภายใน PDF อย่างแม่นยำและทำให้ไฟล์มีขนาดเล็กลง เนื่องจากหลีกเลี่ยงการฝังอ็อบเจกต์เพิ่มเติม  

## สรุป

ตอนนี้คุณรู้ **วิธีตั้งค่าความโปร่งใสใน PDF** ด้วย Aspose.Pdf สำหรับ C# แล้ว บทแนะนำได้ครอบคลุมการแก้ไขทรัพยากร PDF, การเปลี่ยนค่า fill alpha, การตั้งค่า fill opacity, และการบันทึก PDF ที่แก้ไขแล้ว ด้วยพื้นฐานนี้คุณสามารถทดลองใช้โหมดผสมต่าง ๆ, ใส่ความโปร่งใสกับข้อความ, หรือสร้าง graphics state ที่ใช้ซ้ำได้สำหรับเอกสารที่ซับซ้อน

### ขั้นตอนต่อไป

* สำรวจโหมดผสมอื่น ๆ (`Multiply`, `Screen`, ฯลฯ) โดยเปลี่ยนค่า `BM`  
* ปรับค่า stroke alpha (`CA`) เพื่อสร้างขอบเส้นกึ่งโปร่งใส  
* รวมหลาย graphics state เพื่อสร้างไลบรารีของเอฟเฟกต์ภาพที่ใช้ซ้ำได้  

อย่าลังเลที่จะแบ่งปันผลลัพธ์ของคุณหรือถามคำถามในคอมเมนต์ ขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโครงการของคุณ

- [How to Customize PDFs with Aspose.PDF for .NET&#58; Set Page Margins and Draw Lines](/pdf/english/net/document-manipulation/customize-pdfs-aspose-pdf-set-margins-draw-lines/)
- [How to Set Image Size in a PDF Using Aspose-PDF for .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [How to Set PDF Permissions Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/security-permissions/set-pdf-privileges-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}