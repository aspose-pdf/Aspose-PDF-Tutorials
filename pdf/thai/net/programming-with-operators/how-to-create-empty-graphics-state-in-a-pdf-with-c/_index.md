---
category: general
date: 2026-08-17
description: สร้างสถานะกราฟิกว่างใน PDF ด้วย C# และ Aspose.Pdf. ทำตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อแก้ไขทรัพยากร
  ExtGState อย่างปลอดภัย.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty graphics state
- Aspose PDF graphics state
- C# modify PDF resources
- add ExtGState dictionary
- PDF page resources editing
language: th
lastmod: 2026-08-17
og_description: สร้างสถานะกราฟิกเปล่าใน PDF ด้วย C#. บทเรียนนี้แสดงวิธีแก้ไขทรัพยากร
  ExtGState ด้วย Aspose.Pdf เพื่อการแก้ไข PDF ที่น่าเชื่อถือ.
og_image_alt: Screenshot of C# code that adds an empty graphics state to a PDF document
og_title: สร้างสถานะกราฟิกเปล่าใน PDF ด้วย C# – คู่มือแบบขั้นตอนต่อขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Create empty graphics state in a PDF using C# and Aspose.Pdf. Follow
    this step‑by‑step guide to edit ExtGState resources safely.
  headline: How to create empty graphics state in a PDF with C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: วิธีสร้างสถานะกราฟิกว่างใน PDF ด้วย C#
url: /th/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้างกราฟิกสเตตว่างใน PDF ด้วย C#

หากคุณต้องการ **create empty graphics state** ใน PDF คำแนะนำนี้จะแสดงให้คุณเห็นขั้นตอนที่ทำได้โดยใช้ C# และ Aspose.Pdf คุณจะได้เห็นตัวอย่างที่ทำงานได้เต็มรูปแบบซึ่งเพิ่มรายการใหม่ลงในพจนานุกรม ExtGState ของหน้าโดยไม่กระทบเนื้อหาที่มีอยู่

การทำงานกับกราฟิกสเตตของ PDF เป็นความต้องการทั่วไปเมื่อคุณต้องการควบคุมความโปร่งใส, โหมดผสม, หรือพารามิเตอร์การเรนเดอร์อื่น ๆ ในระดับวัตถุ โค้ดด้านล่างจะแสดงแนวทางที่แนะนำ, อธิบายว่าทำไมแต่ละขั้นตอนจึงสำคัญ, และครอบคลุมการเปลี่ยนแปลงทั่วไปที่คุณอาจพบ

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (ตัวอย่างสามารถคอมไพล์กับ .NET Core ได้เช่นกัน).
* ใบอนุญาต Aspose.Pdf for .NET (หรือคีย์ประเมินผลชั่วคราว).
* โฟลเดอร์ที่มีไฟล์ `input.pdf` ที่คุณต้องการแก้ไข.
* ความคุ้นเคยพื้นฐานกับไวยากรณ์ C# และแนวคิด PDF เช่น พจนานุกรม resources.

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และนำเข้า namespaces

สร้างแอปพลิเคชันคอนโซลใหม่หรือรวมโค้ดเข้าในโปรเจกต์ที่มีอยู่แล้ว เพิ่มแพคเกจ NuGet ของ Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

จากนั้นนำเข้า namespaces ที่จำเป็น:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
```

การนำเข้าดังกล่าวทำให้คุณเข้าถึงคลาส `Document`, `DictionaryEditor` และคลาส primitive ของ PDF ที่จำเป็นสำหรับการสร้างรายการ **create empty graphics state**

## ขั้นตอนที่ 2: กำหนดโฟลเดอร์ที่เก็บไฟล์ PDF

แทนที่เส้นทางด้วยตำแหน่งที่ตั้งของไฟล์ PDF ของคุณเอง การเก็บไดเรกทอรีในตัวแปรทำให้โค้ดสามารถนำกลับมาใช้ใหม่และง่ายต่อการทดสอบ.

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfSamples\";
```

## ขั้นตอนที่ 3: โหลดเอกสาร PDF ต้นฉบับ

การเปิดเอกสารภายในคำสั่ง `using` ทำให้แน่ใจว่าการจัดการไฟล์จะถูกปล่อยอัตโนมัติหลังจากบันทึกการเปลี่ยนแปลง.

```csharp
// Step 2: Load the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // All subsequent operations happen inside this using block
```

## ขั้นตอนที่ 4: เข้าถึงหน้าแรกและพจนานุกรม Resources ของมัน

```csharp
    // Step 3: Get the first page and its Resources dictionary
    var firstPage = pdfDocument.Pages[1];
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
    var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

- `Pages[1]` ดึงหน้าที่หนึ่ง (เลขหน้าของ PDF เริ่มที่ 1).
- `DictionaryEditor` ให้วิธีที่สะดวกในการอ่านและแก้ไขพจนานุกรมของ PDF.
- รายการ `ExtGState` เก็บวัตถุ graphics‑state ทั้งหมดสำหรับหน้า หากคีย์ไม่มีอยู่ Aspose.Pdf จะสร้างพจนานุกรมว่างโดยอัตโนมัติ.

## ขั้นตอนที่ 5: สร้างพจนานุกรม graphics‑state ว่างใหม่

กราฟิกสเตตที่คุณเพิ่มสามารถเป็นว่างหรือมีพารามิเตอร์ล่วงหน้า เช่น ความทึบ (`CA`, `ca`) หรือโหมดผสม (`BM`). ในบทแนะนำนี้เราจะสร้าง **empty graphics state** แล้วตั้งค่าบางค่าเพื่อแสดงวิธีการทำงานของพจนานุกรม.

```csharp
    // Step 4: Create a new empty graphics‑state dictionary and set its parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // Stroke opacity
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };
    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

- `CosPdfDictionary.CreateEmptyDictionary` สร้างคอนเทนเนอร์ที่ว่างเปล่าซึ่งคุณสามารถเติมด้วยคีย์ graphics‑state ใด ๆ.
- การเพิ่ม `CA`, `ca`, และ `BM` เป็นตัวเลือก; คุณสามารถละเว้นได้หากต้องการสเตตว่างจริง ๆ โค้ดแสดงวิธีเพิ่มรายการเมื่อคุณต้องการควบคุมการเรนเดอร์ในภายหลัง.

## ขั้นตอนที่ 6: แทรกกราฟิกสเตตใหม่ลงในพจนานุกรม ExtGState

```csharp
    // Step 5: Add the new graphics state to the page's ExtGState dictionary (e.g., name it "GS0")
    extGStateDict.Add("GS0", newGraphicsState);
```

การตั้งชื่อรายการเป็น `"GS0"` สอดคล้องกับแนวปฏิบัติทั่วไปที่ใส่คำนำหน้า “GS” ให้กับชื่อกราฟิกสเตต คุณสามารถเลือกชื่อ PDF ที่ถูกต้องใด ๆ ที่ไม่ซ้ำกับคีย์ที่มีอยู่.

## ขั้นตอนที่ 7: บันทึกเอกสาร PDF ที่แก้ไขแล้ว

```csharp
    // Step 6: Save the modified PDF document
    pdfDocument.Save(dataDir + "output.pdf");
}
```

คำสั่ง `Save` จะเขียนไฟล์ที่อัปเดตไปยัง `output.pdf`. การเปิดไฟล์นี้ในโปรแกรมดู PDF จะยืนยันว่ากราฟิกสเตตใหม่มีอยู่; คุณสามารถอ้างอิงมันต่อไปด้วยโอเปอเรเตอร์ `gs` ในสตรีมเนื้อหา.

### รายการซอร์สเต็มรูปแบบ

เมื่อรวมทุกอย่างเข้าด้วยกัน โปรแกรมเต็มรูปแบบจะเป็นดังนี้:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Define the folder that contains the PDF files
        string dataDir = @"C:\PdfSamples\";

        // Load the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Get the first page and its Resources dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create a new empty graphics‑state dictionary and set its parameters
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters)
                newGraphicsState.Add(p);

            // Add the new graphics state to the page's ExtGState dictionary (name it "GS0")
            extGStateDict.Add("GS0", newGraphicsState);

            // Save the modified PDF document
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("Empty graphics state created and saved to output.pdf");
    }
}
```

การรันโปรแกรมจะแสดงบรรทัดยืนยันและสร้างไฟล์ `output.pdf` พร้อมกราฟิกสเตตที่เพิ่มใหม่.

## ทำไมวิธีนี้ถึงทำงานได้ดีที่สุด

- **การแก้ไขพจนานุกรมโดยตรง** – การใช้ `DictionaryEditor` ช่วยหลีกเลี่ยงการต้องพาร์สสตรีมเนื้อหาทั้งหมด คุณจะแก้ไขเฉพาะ resources ที่ต้องการเท่านั้น.
- **PDF primitives ที่กำหนดประเภท** – `CosPdfNumber`, `CosPdfName`, และ `CosPdfDictionary` รับประกันว่า PDF ที่สร้างขึ้นสอดคล้องกับสเปค PDF 1.7.
- **ความปลอดภัย** – บล็อก `using` จะทำลายอ็อบเจ็กต์ `Document` ป้องกันการล็อกไฟล์ที่อาจทำให้การสร้างต่อไปเสียหาย.
- **ความสามารถขยาย** – เมื่อกราฟิกสเตตว่างมีอยู่แล้ว คุณสามารถอ้างอิงจากโอเปอเรเตอร์เนื้อหาใด ๆ (`gs`) เพื่อเปลี่ยนความทึบ, โหมดผสม, หรือพารามิเตอร์อื่น ๆ สำหรับคำสั่งวาดที่เลือก.

## การเปลี่ยนแปลงทั่วไปและกรณีขอบ

| สถานการณ์ | การปรับแต่งที่แนะนำ |
|-----------|-------------------|
| **หลายหน้า** | วนลูปผ่าน `pdfDocument.Pages` และทำการแทรกพจนานุกรมซ้ำสำหรับแต่ละหน้าที่คุณต้องการแก้ไข. |
| **ไม่มีรายการ ExtGState อยู่แล้ว** | `resourcesEditor["ExtGState"]` จะสร้างพจนานุกรมว่างโดยอัตโนมัติหากไม่มีอยู่ ไม่จำเป็นต้องเขียนโค้ดเพิ่มเติม. |
| **ชื่อ graphics‑state ที่แตกต่าง** | แทนที่ `"GS0"` ด้วยชื่อที่สอดคล้องกับแนวปฏิบัติของคุณ เช่น `"MyTransparentState"`. |
| **เพิ่มเฉพาะสเตตว่าง** | ละเว้นอาร์เรย์ `parameters` และลูป `foreach`; พจนานุกรมจะคงเป็นว่าง. |
| **ทำงานกับ PDF ที่เข้ารหัส** | ระบุรหัสผ่านเมื่อสร้าง `new Document(path, password)` ก่อนแก้ไข resources. |

## การตรวจสอบผลลัพธ์

คุณสามารถตรวจสอบว่ากราฟิกสเตตถูกเพิ่มโดยการตรวจสอบ PDF ด้วยโปรแกรมดูระดับต่ำเช่น **PDF‑Tron** หรือ **iText Sharp** ค้นหารายการที่คล้ายกับ:

```
/ExtGState << /GS0 << /CA 1 /ca 0.5 /BM /Normal >> >>
```

หากรายการปรากฏ การดำเนินการ **create empty graphics state** สำเร็จ.

## สรุป

ตอนนี้คุณรู้วิธี **create empty graphics state** ใน PDF ด้วย C# และ Aspose.Pdf แล้ว บทแนะนำได้ครอบคลุมทุกขั้นตอน—from การโหลดเอกสารจนถึงการแก้ไขพจนานุกรม `ExtGState` และการบันทึกผลลัพธ์—พร้อมอธิบายเหตุผลของแต่ละการกระทำ.  

จากนี้คุณสามารถ:

* ใช้กราฟิกสเตตใหม่ในสตรีมเนื้อหา (`gs /GS0`).
* ทดลองใช้คีย์เพิ่มเติมเช่น `/SM` (การปรับเส้น) หรือ `/OPM` (โหมดพิมพ์ซ้อน).
* นำเทคนิคเดียวกันไปใช้กับประเภท resource อื่น ๆ เช่น `/XObject` หรือ `/ColorSpace`.

ขอให้สนุกกับการทำงานกับ PDF และอย่าลังเลที่จะสำรวจสถานการณ์ **Aspose PDF graphics state** อื่น ๆ เช่น การเปลี่ยนความทึบแบบไดนามิกหรือโหมดผสมแบบกำหนดเอง!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโครงการของคุณ.

- [วิธีสร้างเส้นประใน PDF ด้วย Aspose.PDF for .NET: คู่มือขั้นตอนต่อขั้นตอน](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [วิธีลบกราฟิกจาก PDF ด้วย Aspose.PDF .NET: คู่มือเต็ม](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [สร้างและเติมสี่เหลี่ยมใน PDF ด้วย Aspose.PDF for .NET: คู่มือขั้นตอนต่อขั้นตอน](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}