---
category: general
date: 2026-10-04
description: เรียนรู้วิธีเปลี่ยนความโปร่งใสของ PDF ด้วย Aspose.Pdf ใน C# คู่มือขั้นตอนนี้เพิ่มสถานะกราฟิกแบบกำหนดเองเพื่อปรับความทึบและโหมดการผสมสี
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF transparency
- Aspose.Pdf graphics state
- PDF opacity C#
- ExtGState dictionary
- blend mode PDF
language: th
lastmod: 2026-10-04
og_description: เปลี่ยนความโปร่งใสของ PDF ใน C# ด้วย Aspose.Pdf. ทำตามบทแนะนำสั้น
  ๆ นี้เพื่อปรับความทึบแสง, โหมดการผสม, และสถานะกราฟิกใน PDF ของคุณ.
og_image_alt: Screenshot of a PDF page before and after changing transparency with
  Aspose.Pdf
og_title: เปลี่ยนความโปร่งใสของ PDF ด้วย Aspose.Pdf – คู่มือ C# ฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to change PDF transparency with Aspose.Pdf in C#. This step‑by‑step
    guide adds a custom graphics state to adjust opacity and blend mode.
  headline: How to change PDF transparency using Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- graphics state
title: วิธีเปลี่ยนความโปร่งใสของ PDF ด้วย Aspose.Pdf ใน C#
url: /th/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการเปลี่ยนความโปร่งใสของ PDF ด้วย Aspose.Pdf ใน C#

หากคุณต้องการ **เปลี่ยนความโปร่งใสของ PDF** ในโครงการ .NET คู่มือนี้จะแสดงให้คุณเห็นขั้นตอนการทำด้วย Aspose.Pdf อย่างละเอียด เมื่อจบการสอนคุณจะได้ PDF ที่วัตถุที่เลือกใช้ค่าความโปร่งใสและโหมดการผสมสีที่กำหนดเอง โดยไม่ต้องใช้เครื่องมือภายนอกใด ๆ

การทำงานกับความโปร่งใสของ PDF เป็นความต้องการทั่วไปสำหรับลายน้ำ, กราฟิกโอเวอร์เลย์, หรือเอฟเฟกต์ภาพที่ละเอียดอ่อน ขั้นตอนต่อไปนี้ครอบคลุมทุกอย่างที่คุณต้องการ—ตั้งแต่การโหลดเอกสารไปจนถึงการแก้ไข **ExtGState dictionary**, การสร้างกราฟิกสเตทใหม่, และการบันทึกผลลัพธ์

## ข้อกำหนดเบื้องต้น

* **Aspose.Pdf for .NET** (เวอร์ชัน 23.12 หรือใหม่กว่า) คุณสามารถติดตั้งผ่าน NuGet:

```bash
dotnet add package Aspose.Pdf
```

* สภาพแวดล้อมการพัฒนา .NET (Visual Studio, VS Code หรือ `dotnet` CLI).
* ไฟล์ PDF อินพุตที่อยู่ในไดเรกทอรีที่ทราบ (ตัวอย่างใช้ `input.pdf`).

ไม่จำเป็นต้องใช้ไลบรารีเพิ่มเติม

## ขั้นตอนที่ 1: โหลดเอกสาร PDF

การดำเนินการแรกคือการเปิด PDF ที่มีอยู่ การใช้บล็อก `using` จะรับประกันว่าการจัดการไฟล์จะถูกปล่อยอัตโนมัติ

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;

// ...

using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

*ทำไมสิ่งนี้สำคัญ*: การโหลดเอกสารสร้างการแสดงผลในหน่วยความจำที่คุณสามารถแก้ไขได้ คลาส `Document` ยังให้คุณเข้าถึงวัตถุ COS ระดับต่ำ ซึ่งจำเป็นสำหรับการเปลี่ยนความโปร่งใสของ PDF

## ขั้นตอนที่ 2: เข้าถึงทรัพยากรของหน้าแรก

กราฟิกสเตทจะถูกเก็บไว้ในพจนานุกรมทรัพยากรของหน้า เราจะดึงหน้าแรกและห่อหุ้มทรัพยากรของมันด้วย `DictionaryEditor` เพื่อให้เราสามารถแก้ไขได้อย่างสะดวก

```csharp
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*คำอธิบาย*: `DictionaryEditor` ทำหน้าที่เป็นชั้นนามธรรมสำหรับการจัดการพจนานุกรม COS ทำให้คุณสามารถอ่านและเขียนรายการเช่น `ExtGState` ได้โดยไม่ต้องจัดการกับไวยากรณ์ PDF ดิบ

## ขั้นตอนที่ 3: รับ (หรือสร้าง) พจนานุกรม ExtGState

พจนานุกรม **ExtGState** เก็บวัตถุกราฟิกสเตทที่มีชื่อ หากมีอยู่แล้วเราจะใช้ซ้ำ; หากไม่มีเราจะสร้างใหม่

```csharp
CosPdfDictionary extGStateDict;

// Try to fetch an existing ExtGState entry
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a fresh ExtGState dictionary and add it to the resources
    extGStateDict = new CosPdfDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*ทำไมต้องทำขั้นตอนนี้*: หากไม่มีรายการ `ExtGState` เอนจิน PDF จะไม่มีที่ใดให้ค้นหาการตั้งค่าความโปร่งใสที่กำหนดเอง การเพิ่มพจนานุกรมทำให้หน้าตระหนักถึงกราฟิกสเตทใหม่ที่คุณกำหนด

## ขั้นตอนที่ 4: กำหนดกราฟิกสเตทใหม่ด้วยความโปร่งใสและโหมดการผสมสี

กราฟิกสเตทคือชุดของพารามิเตอร์การเรนเดอร์ PDF ที่นี่เราตั้งค่า:

* **CA** – ความโปร่งใสของเส้นขอบ (1 = ทึบเต็ม)
* **ca** – ความโปร่งใสของการเติม (0.5 = โปร่งใส 50 %)
* **BM** – โหมดการผสมสี (`Normal` เป็นค่าเริ่มต้น, แต่คุณสามารถทดลองกับ `Multiply`, `Screen`, ฯลฯ)

```csharp
// Create an empty dictionary that will become the new graphics state
var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Prepare the entries
var graphicsStateEntries = new KeyValuePair<string, ICosPdfPrimitive>[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

// Populate the dictionary
foreach (var entry in graphicsStateEntries)
{
    graphicsState.Add(entry);
}
```

*ข้อมูลเชิงลึก*: ค่า `CosPdfNumber` เป็นตัวเลขทศนิยมระหว่าง 0 ถึง 1 การเปลี่ยนแปลงค่าจะทำให้คุณปรับความโปร่งใสของเส้นและการเติมได้อย่างละเอียด โหมดการผสมสีกำหนดว่าคอนเทนต์โปร่งใสจะโต้ตอบกับกราฟิกพื้นฐานอย่างไร

## ขั้นตอนที่ 5: ลงทะเบียนกราฟิกสเตทใน ExtGState

เราให้สเตทใหม่ชื่อ (`GS0`). ภายหลังเมื่อคุณวาดวัตถุ คุณจะอ้างอิงชื่อนี้ในสตรีมคอนเทนต์

```csharp
extGStateDict.Add("GS0", graphicsState); // "GS0" becomes the identifier you’ll use later
```

*แนวทางปฏิบัติที่ดีที่สุด*: ใช้รูปแบบการตั้งชื่อที่ชัดเจน (`GS0`, `GS_Watermark` ฯลฯ) เพื่อให้คุณจัดการหลายสเตทได้โดยไม่สับสน

## ขั้นตอนที่ 6: ใช้กราฟิกสเตทกับเนื้อหาของหน้า (ตัวเลือก)

หากคุณต้องการใช้ความโปร่งใสใหม่กับองค์ประกอบที่มีอยู่ในหน้า คุณต้องแก้ไขสตรีมคอนเทนต์ของหน้า ด้านล่างเป็นตัวอย่างง่าย ๆ ที่เพิ่มสี่เหลี่ยมกึ่งโปร่งใสบนหน้า

```csharp
// Build a content stream that sets the graphics state and draws a rectangle
var contentBuilder = new Aspose.Pdf.Operators.ContentBuilder(pdfDocument);
contentBuilder.SetGraphicsState("GS0");
contentBuilder.SetFillColor(Color.FromRgb(255, 0, 0)); // red fill
contentBuilder.Rectangle(100, 500, 200, 100); // x, y, width, height
contentBuilder.FillPath();

firstPage.Contents.Add(contentBuilder);
```

*ทำไมจึงทำงาน*: ตัวดำเนินการ `SetGraphicsState` บอกตัวแปลความ PDF ให้ใช้พารามิเตอร์ที่กำหนดใน `GS0` สำหรับคำสั่งการวาดต่อไปทั้งหมด ดังนั้นสี่เหลี่ยมจะแสดงความโปร่งใสการเติม 50 % ในขณะที่เส้นขอบยังคงทึบเต็ม

## ขั้นตอนที่ 7: บันทึก PDF ที่แก้ไขแล้ว

สุดท้ายให้เขียนการเปลี่ยนแปลงกลับไปยังดิสก์

```csharp
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

ไฟล์ `output.pdf` ที่ได้จะมีกราฟิกสเตทใหม่และคอนเทนต์ใด ๆ ที่อ้างอิง `GS0` จะเรนเดอร์ด้วยความโปร่งใสที่กำหนด

---

![แผนภาพแสดงการเปลี่ยนความโปร่งใสของ PDF](/images/pdf-transparency-before-after.png "หน้า PDF ก่อนและหลังการใช้กราฟิกสเตทที่กำหนดเอง")
*ข้อความแทนภาพ (สำหรับ SEO และการเข้าถึง):* **ตัวอย่างการเปลี่ยนความโปร่งใสของ PDF – หน้าเดิม vs. หน้าแก้ไข**

## ตัวอย่างทำงานเต็มรูปแบบ

เมื่อนำทุกอย่างมารวมกัน นี่คือตัวอย่างโปรแกรมเดียวที่สามารถรันได้ซึ่งเปลี่ยนความโปร่งใสของ PDF และเพิ่มสี่เหลี่ยมกึ่งโปร่งใส

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Tools;
using System.Collections.Generic;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Drawing;

class ChangePdfTransparency
{
    static void Main()
    {
        // Load the source PDF
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Ensure ExtGState dictionary exists
            CosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            else
            {
                extGStateDict = new CosPdfDictionary(pdfDocument);
                resourcesEditor["ExtGState"] = extGStateDict;
            }

            // Create a new graphics state (opacity + blend mode)
            var graphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var e in entries) graphicsState.Add(e);

            // Register the graphics state as GS0
            extGStateDict.Add("GS0", graphicsState);

            // OPTIONAL: draw a semi‑transparent rectangle using GS0
            var builder = new ContentBuilder(pdfDocument);
            builder.SetGraphicsState("GS0");
            builder.SetFillColor(Color.FromRgb(255, 0, 0)); // red
            builder.Rectangle(100, 500, 200, 100);
            builder.FillPath();
            firstPage.Contents.Add(builder);

            // Save the result
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        Console.WriteLine("PDF transparency changed and saved to output.pdf");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

* ไฟล์ `output.pdf` ถูกสร้างในโฟลเดอร์ที่ระบุ
* หากคุณเปิด PDF คุณจะเห็นสี่เหลี่ยมสีแดงที่การเติมเป็นโปร่งใส 50 % ในขณะที่ขอบยังคงทึบเต็ม
* วัตถุอื่น ๆ ที่อ้างอิง `GS0` (เช่น ลายน้ำ) จะสืบทอดความโปร่งใสและโหมดการผสมสีเดียวกัน

## คำถามทั่วไปและการจัดการกรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| **ฉันสามารถเปลี่ยนความโปร่งใสของเส้นขอบเท่านั้นได้หรือไม่?** | ตั้งค่า `CA` เป็นค่าที่ต้องการและให้ `ca` คงเป็น `1` |
| **โหมดการผสมสีที่รองรับมีอะไรบ้าง?** | รองรับโหมดการผสมสีมาตรฐานของ PDF ทั้งหมด (`Normal`, `Multiply`, `Screen`, `Overlay` ฯลฯ) ผ่านรายการ `BM` |
| **ฉันต้องทำความสะอาดพจนานุกรมหลังการใช้งานหรือไม่?** | ไม่จำเป็น วัตถุ `CosPdfDictionary` จะถูกจัดการโดย Aspose.Pdf และจะถูกเขียนลงไฟล์เมื่อคุณเรียก `Save` |
| **วิธีการทำงานกับ PDF ที่เข้ารหัสเป็นอย่างไร?** | โหลดเอกสารด้วยรหัสผ่านที่ถูกต้อง (`new Document(path, password)`). การจัดการกราฟิกสเตททำงานเช่นเดียวกันเมื่อเอกสารถูกถอดรหัสในหน่วยความจำ |
| **สามารถใช้กราฟิกสเตทเดียวกันกับหลายหน้าได้หรือไม่?** | ได้ เพิ่มรายการ `GS0` ลงในพจนานุกรม `ExtGState` ของแต่ละหน้า หรือสร้างพจนานุกรมที่ใช้ร่วมกันในทรัพยากรระดับเอกสารและอ้างอิงจากแต่ละหน้า |

## เคล็ดลับและแนวทางปฏิบัติที่ดีที่สุด

* **เคล็ดลับมืออาชีพ:** ให้ชื่อกราฟิกสเตทสั้นแต่บ่งบอกความหมาย (`GS_Watermark`, `GS_Overlay`). นี้ช่วยหลีกเลี่ยงการชนชื่อและทำให้การดีบักง่ายขึ้น
* **ระวัง:** การเขียนทับรายการ `ExtGState` ที่มีอยู่โดยบังเอิญ ควรตรวจสอบ `resourcesEditor.ContainsKey("ExtGState")` ก่อนสร้างพจนานุกรมใหม่เสมอ
* **หมายเหตุด้านประสิทธิภาพ:** การแก้ไขวัตถุ COS ระดับต่ำทำได้เร็ว แต่หากต้องประมวลผลหลายพันหน้า ควรทำเป็นชุดเพื่อลดความกดดันของหน่วยความจำ

## ขั้นตอนต่อไป

ตอนนี้คุณรู้วิธี **เปลี่ยนความโปร่งใสของ PDF** แล้ว คุณสามารถสำรวจหัวข้อที่เกี่ยวข้องเช่น:

* การเพิ่ม **ลายน้ำ** ด้วยความโปร่งใสที่กำหนดเอง (`PDF opacity C#`).
* การใช้ **โหมดการผสมสีที่ต่างกัน** เพื่อสร้างเอฟเฟกต์ศิลปะ (`blend mode PDF`).
* การสร้าง **ไลบรารีกราฟิกสเตท** ที่นำกลับมาใช้ได้สำหรับการสร้างเอกสารขนาดใหญ่ (`Aspose.Pdf graphics state`).

ทดลองปรับค่า `ca` และ `CA` ต่าง ๆ หรือแทนที่สี่เหลี่ยมสีแดงด้วยรูปภาพหรือข้อความโอเวอร์เลย์ หลักการเดียวกันยังคงใช้ได้—เพียงอ้างอิงกราฟิกสเตท `GS0` ก่อนวาดคอนเทนต์ใหม่

---

*คุณได้เรียนรู้วิธีเปลี่ยนความโปร่งใสของ PDF ด้วย Aspose.Pdf ใน C# แล้ว ใช้เทคนิคเหล่านี้เพื่อปรับปรุงรายงาน, ใบแจ้งหนี้, หรือผลลัพธ์ใด ๆ ที่ใช้ PDF ที่ต้องการความละเอียดด้านภาพ*

## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณ

- [เปลี่ยนความโปร่งใสของ PDF ด้วย Aspose.PDF – คู่มือ C# ฉบับสมบูรณ์](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [เปลี่ยนความโปร่งใสของ PDF ใน C# – คู่มือ Aspose ฉบับสมบูรณ์](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-in-c-complete-aspose-guide/)
- [เพิ่มความโปร่งใสให้ PDF ด้วย Aspose – คู่มือ C# ฉบับสมบูรณ์](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}