---
category: general
date: 2026-03-19
description: เพิ่มความโปร่งใสให้กับ PDF ด้วย Aspose.PDF สำหรับ C# เรียนรู้วิธีตั้งค่าความทึบแสง
  โหมดการผสม และ ExtGState ด้วยเพียงไม่กี่บรรทัดของโค้ด
draft: false
keywords:
- add transparency to pdf
- Aspose PDF transparency
- C# PDF graphics state
- PDF blend mode
- set PDF opacity
language: th
og_description: เพิ่มความโปร่งใสให้กับ PDF อย่างรวดเร็ว คู่มือนี้แสดงวิธีควบคุมความทึบและโหมดผสมโดยใช้
  Aspose.PDF ใน C#
og_title: เพิ่มความโปร่งใสให้กับ PDF ด้วย Aspose PDF – คู่มือ C# ฉบับเต็ม
tags:
- Aspose.PDF
- C#
title: เพิ่มความโปร่งใสให้กับ PDF ด้วย Aspose PDF ใน C# – คู่มือขั้นตอนโดยละเอียด
url: /th/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มความโปร่งใสให้กับ PDF ด้วย Aspose PDF ใน C# – บทเรียนเต็ม

เคยสงสัย **วิธีเพิ่มความโปร่งใสให้กับไฟล์ PDF** โดยไม่ต้องต่อสู้กับไวยากรณ์ระดับต่ำของ PDF หรือไม่? คุณไม่ได้เป็นคนเดียวที่ต้องการวิธีรวดเร็วในการทำให้รูปทรงหรือข้อความเป็นกึ่ง‑โปร่งใส—เช่นลายน้ำ, กราฟิกซ้อน, หรือเคล็ดลับ UI ที่ละเอียดภายในเอกสาร  

ในคู่มือนี้เราจะเดินผ่าน **ตัวอย่างที่สมบูรณ์และสามารถรันได้** ที่แสดงอย่างชัดเจนว่าตั้งค่าความทึบของการเติม, ความทึบของเส้นขอบ, และโหมดการผสมอย่างไรโดยใช้ Aspose.PDF สำหรับ .NET. เมื่อเสร็จสิ้นคุณจะได้ PDF ที่สี่เหลี่ยมผืนผ้าแสดงที่ความทึบ 50 % และคุณจะเข้าใจว่าพจนานุกรม ExtGState คือกุญแจสำคัญในการทำให้ได้ผลลัพธ์นี้

เราจะครอบคลุมทุกอย่างที่คุณต้องการ: แพ็คเกจ NuGet ที่จำเป็น, โค้ดตัวอย่าง, คำอธิบายแต่ละบรรทัด, และเคล็ดลับบางอย่างสำหรับกรณีขอบเช่นโปรแกรมอ่าน PDF รุ่นเก่า ไม่ต้องอ้างอิงภายนอก—เพียงโซลูชันที่พร้อมคัดลอก‑วางและรันได้ทันที

## สิ่งที่คุณต้องมี

- **Aspose.PDF for .NET** (เวอร์ชัน 23.12 หรือใหม่กว่า) ติดตั้งผ่าน NuGet: `Install-Package Aspose.PDF`.
- สภาพแวดล้อมการพัฒนา .NET (Visual Studio, Rider, หรือ `dotnet` CLI).
- PDF ตัวอย่างชื่อ `input.pdf` ที่วางไว้ในโฟลเดอร์ที่คุณควบคุม (บทเรียนใช้ `YOUR_DIRECTORY/` เป็นตัวแทน).

เท่านี้เอง ถ้าคุณมีทั้งหมดแล้ว ไปต่อกันเลย

## เพิ่มความโปร่งใสให้กับ PDF – ภาพรวม

หัวใจของการทำให้สิ่งใดสิ่งหนึ่งโปร่งใสใน PDF คือ **กราฟิกสเตต** (`ExtGState`). โดยการเพิ่มอ็อบเจกต์กราฟิกสเตตที่กำหนดเองลงในพจนานุกรมทรัพยากรของหน้า คุณสามารถกำหนดค่าได้ดังนี้

| Property | Meaning |
|----------|---------|
| `ca` | ความทึบของการเติม (0 = โปร่งใสเต็ม, 1 = ทึบเต็ม). |
| `CA` | ความทึบของเส้นขอบ (สเกลเดียวกัน). |
| `BM` | โหมดการผสม (เช่น `Normal`, `Multiply`). |

เราจะสร้างกราฟิกสเตตใหม่, แทรกลงในพจนานุกรม `ExtGState` ของหน้า, แล้วอ้างอิงมันเมื่อวาดต่อไป โค้ดสแนปด้านล่างทำสิ่งนั้นอย่างตรงไปตรงมา

![add transparency to pdf diagram](add_transparency_to_pdf.png){alt="เพิ่มความโปร่งใสให้กับ pdf"}

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และโหลด PDF

แรกสุดเราจะสร้างแอปคอนโซลง่าย ๆ (หรือโปรเจกต์ C# ใด ๆ) แล้วโหลด PDF ต้นฉบับ

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;          // For low‑level PDF operators
using Aspose.Pdf.Text;               // Optional, if you want to add text later
using Aspose.Pdf.XObjects;          // For image handling, not needed here

// Define the folder that contains the PDF file
string inputDir = @"YOUR_DIRECTORY/";

// Load the PDF document
using (var pdfDocument = new Document(Path.Combine(inputDir, "input.pdf")))
{
    // All subsequent steps go inside this using block
```

**ทำไมจึงสำคัญ:**  
`Document` คือจุดเริ่มต้นของการจัดการ PDF ใด ๆ ด้วย Aspose. การห่อหุ้มด้วย `using` รับประกันว่าทรัพยากรทั้งหมดจะถูกล้างอย่างถูกต้องเมื่อเราบันทึกไฟล์ต่อไป

## ขั้นตอนที่ 2: เข้าถึงหน้าแรกและทรัพยากรของมัน

เราต้องการพจนานุกรมทรัพยากรของหน้าแรก เพราะที่นั่นมีคอลเลกชัน `ExtGState`

```csharp
    // Grab the first page (pages are 1‑based in Aspose)
    Page firstPage = pdfDocument.Pages[1];

    // Helper to edit dictionaries (resources, etc.)
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);

    // Retrieve the existing ExtGState dictionary, or create a new one if missing
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

**คำอธิบาย:**  
หากหน้ามีรายการ `ExtGState` อยู่แล้ว เราจะใช้ต่อ; หากไม่มีเราจะสร้างพจนานุกรมใหม่ วิธีนี้ช่วยป้องกันข้อผิดพลาด null‑reference เมื่อทำงานกับ PDF ที่ไม่มีกราฟิกสเตตใด ๆ

## ขั้นตอนที่ 3: สร้างกราฟิกสเตตใหม่ด้วยความทึบที่ต้องการ

ต่อไปเรากำหนดค่าความโปร่งใสจริง ๆ

```csharp
    // Create an empty dictionary that will represent our new graphics state
    CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Stroke opacity – fully opaque (1.0)
    newGraphicsState.Add("CA", new CosPdfNumber(1));

    // Fill opacity – 50 % transparent (0.5)
    newGraphicsState.Add("ca", new CosPdfNumber(0.5));

    // Blend mode – Normal is the default, but you can experiment with Multiply, Screen, etc.
    newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**ทำไมต้องใช้คีย์เหล่านี้?**  
- `CA` ควบคุมความทึบของเส้นขอบ (เส้น, ขอบ).  
- `ca` ควบคุมความทึบของการเติม (รูปทรงทึบ, ข้อความ).  
- `BM` เลือกวิธีที่อ็อบเจกต์โปร่งใสผสมกับเนื้อหาที่อยู่ด้านล่าง การใช้ `"Normal"` ทำให้ผลลัพธ์คาดเดาได้ในหลายโปรแกรมอ่าน

## ขั้นตอนที่ 4: ลงทะเบียนกราฟิกสเตตในทรัพยากรของหน้า

เราตั้งชื่อกราฟิกสเตต (`GS0`) แล้วเพิ่มลงในพจนานุกรม `ExtGState`

```csharp
    // Add the graphics state to the ExtGState dictionary with a unique name
    extGStateDict.Add("GS0", newGraphicsState);
```

**เคล็ดลับ:**  
หากต้องการอ็อบเจกต์โปร่งใสหลายอันที่มีความทึบต่างกัน ให้สร้างรายการเพิ่มเติม (`GS1`, `GS2`, …) แล้วปรับค่า `ca`/`CA` ตามต้องการ

## ขั้นตอนที่ 5: วาดสี่เหลี่ยมโปร่งใสโดยใช้กราฟิกสเตตใหม่

เมื่อกราฟิกสเตตพร้อม เราสามารถวาดสิ่งที่ใช้มันได้ ด้านล่างเป็นการเพิ่มสี่เหลี่ยมสีน้ำเงินกึ่งโปร่งใสลงในหน้า

```csharp
    // Prepare a content stream for the page (adds to existing content)
    var canvas = new Aspose.Pdf.Drawing.Graphic(firstPage);

    // Set the graphics state we just created
    canvas.SetGraphicsState("GS0");

    // Choose a fill color (blue) and draw the rectangle
    canvas.SetColor(new Aspose.Pdf.Drawing.Color(0, 0, 255)); // RGB blue
    canvas.Rectangle(100, 500, 200, 100); // x, y, width, height

    // Close the canvas to flush commands
    canvas.Close();
```

**สิ่งที่คุณจะเห็น:**  
เมื่อเปิด PDF ที่ได้ สี่เหลี่ยมสีน้ำเงินจะแสดงที่ตำแหน่งที่กำหนด แต่เนื้อหาหน้าพื้นฐานยังคงมองเห็นได้ผ่านมัน เพราะความทึบของการเติมเป็น 0.5 หากคุณตรวจสอบ PDF ด้วยเครื่องมือเช่นฟีเจอร์ “Edit PDF” ของ Adobe Acrobat คุณจะเห็นอ็อบเจกต์ `ExtGState` (`GS0`) ถูกแนบกับสี่เหลี่ยมนั้น

## ขั้นตอนที่ 6: บันทึก PDF ที่อัปเดตแล้ว

สุดท้าย เขียนเอกสารที่แก้ไขกลับไปยังดิสก์

```csharp
    // Save the document with a new name so the original stays untouched
    pdfDocument.Save(Path.Combine(inputDir, "ExtGStateAdded.pdf"));
}
```

นี่คือขั้นตอนทั้งหมด รันแอปคอนโซล, เปิด `ExtGStateAdded.pdf`, และตรวจสอบการซ้อนทับที่โปร่งใส

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class AddTransparencyDemo
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF file
        string inputDir = @"YOUR_DIRECTORY/";

        // Step 2: Load the PDF document
        using (var pdfDocument = new Document(Path.Combine(inputDir, "input.pdf")))
        {
            // Step 3: Get the first page and its resource dictionary
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

            // Step 4: Create a new graphics state with opacity and blend mode settings
            CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            newGraphicsState.Add("CA", new CosPdfNumber(1));          // stroke opacity (fully opaque)
            newGraphicsState.Add("ca", new CosPdfNumber(0.5));       // fill opacity (50% transparent)
            newGraphicsState.Add("BM", new CosPdfName("Normal"));   // blend mode

            // Step 5: Add the new graphics state to the page resources
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 6: Draw a rectangle using the new graphics state
            var canvas = new Graphic(firstPage);
            canvas.SetGraphicsState("GS0");
            canvas.SetColor(new Color(0, 0, 255)); // blue fill
            canvas.Rectangle(100, 500, 200, 100);
            canvas.Close();

            // Step 7: Save the updated PDF document
            pdfDocument.Save(Path.Combine(inputDir, "ExtGStateAdded.pdf"));
        }

        Console.WriteLine("PDF with transparency created successfully.");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  
การเปิด `ExtGStateAdded.pdf` จะเห็นสี่เหลี่ยมสีน้ำเงินที่ตำแหน่ง (100, 500) มีความทึบการเติม 50 % ด้านล่างสี่เหลี่ยม ข้อความหรือรูปภาพที่มีอยู่เดิมยังคงมองเห็นได้

---

## คำถามที่พบบ่อย & กรณีขอบ

### ทำงานกับโปรแกรมอ่าน PDF รุ่นเก่าได้หรือไม่?
โปรแกรมอ่านสมัยใหม่ส่วนใหญ่ (Adobe Reader, Foxit, Chrome) รองรับคีย์ `ca`/`CA` พื้นฐาน โปรแกรมอ่านที่เก่ามากอาจละเลยคีย์เหล่านี้และแสดงรูปทรงเป็นทึบเต็ม

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}