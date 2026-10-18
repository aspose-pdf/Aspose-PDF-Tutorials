---
category: general
date: 2026-08-04
description: เพิ่มกราฟิกสเตต PDF โดยใช้ Aspose.Pdf เพื่อควบคุมความทึบแสงและโหมดการผสมสี
  ปฏิบัติตามบทแนะนำฉบับเต็มนี้เพื่อแก้ไขทรัพยากร PDF อย่างปลอดภัย.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- Aspose.Pdf
- PDF opacity
- PDF blend mode
- ExtGState dictionary
language: th
lastmod: 2026-08-04
og_description: เพิ่มกราฟิกสเตทใน PDF ด้วย Aspose.Pdf เพื่อกำหนดความโปร่งแสงและโหมดผสม
  คำแนะนำนี้แสดงโค้ดเต็ม อธิบายแต่ละขั้นตอน และครอบคลุมข้อผิดพลาดทั่วไป
og_image_alt: Screenshot of a PDF page showing modified graphics state after using
  add graphics state pdf
og_title: เพิ่มสถานะกราฟิก PDF ด้วย Aspose.Pdf – คู่มือการเขียนโปรแกรมเต็ม
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Add graphics state pdf using Aspose.Pdf to control opacity and blend
    mode. Follow this complete tutorial for modifying PDF resources safely.
  headline: Add graphics state pdf with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: Add graphics state pdf using Aspose.Pdf to control opacity and blend
    mode. Follow this complete tutorial for modifying PDF resources safely.
  name: Add graphics state pdf with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: Locate (or create) the `ExtGState` dictionary.
    text: Locate (or create) the `ExtGState` dictionary.
  - name: Build a new graphics‑state dictionary with the desired entries.
    text: Build a new graphics‑state dictionary with the desired entries.
  - name: Reference the new state from drawing commands (outside the scope of this
      tutorial).
    text: Reference the new state from drawing commands (outside the scope of this
      tutorial).
  type: HowTo
tags:
- PDF
- Aspose
- C#
- Graphics state
title: เพิ่มสถานะกราฟิกใน PDF ด้วย Aspose.Pdf – คู่มือแบบทีละขั้นตอน
url: /th/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่ม graphics state pdf ด้วย Aspose.Pdf – คู่มือขั้นตอนโดยละเอียด

หากคุณต้องการ **add graphics state pdf** เพื่อควบคุมความทึบแสงหรือโหมดการผสมสี บทแนะนำนี้จะแสดงวิธีแก้ไขที่สมบูรณ์พร้อมใช้งานในระดับการผลิต คุณจะได้เรียนรู้วิธีแก้ไขพจนานุกรม ExtGState ของหน้า PDF ด้วย Aspose.Pdf และจะได้เห็นโค้ดที่สามารถคัดลอกไปใช้ในโปรเจคของคุณได้โดยตรง

คู่มือครอบคลุมทุกอย่างตั้งแต่การตั้งค่าโปรเจคจนถึงการจัดการกรณีขอบเขตเช่นการไม่มีรายการ ExtGState เมื่อเสร็จสิ้นคุณจะได้ PDF ที่หน้าแรกแสดงผลด้วย graphics state ที่คุณกำหนดไว้

## ข้อกำหนดเบื้องต้น

* ติดตั้ง .NET 6.0 SDK หรือรุ่นที่ใหม่กว่า
* เวอร์ชันล่าสุดของแพ็กเกจ NuGet **Aspose.Pdf** (เช่น 23.12 หรือใหม่กว่า)
* ไฟล์ PDF อินพุตที่อยู่ในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโค้ดได้
* สภาพแวดล้อมการพัฒนา เช่น Visual Studio 2022 หรือ VS Code

## ภาพรวมของกระบวนการ graphics state

graphics state ของ PDF ควบคุมวิธีการแสดงผลของการวาด  
คุณสมบัติสองอย่างเป็นที่นิยมที่สุดสำหรับเอฟเฟกต์ภาพ:

* **Opacity** – รายการ `ca` (เติม) และ `CA` (เส้นขอบ)
* **Blend mode** – รายการ `BM`

ค่าต่าง ๆ นี้อยู่ใน **ExtGState dictionary** ที่แนบกับพจนานุกรมทรัพยากรของหน้า  
การเพิ่ม graphics state ใหม่ประกอบด้วยสามขั้นตอน:

1. ค้นหา (หรือสร้าง) พจนานุกรม `ExtGState`
2. สร้างพจนานุกรม graphics‑state ใหม่พร้อมรายการที่ต้องการ
3. อ้างอิงสถานะใหม่จากคำสั่งการวาด (อยู่นอกขอบเขตของบทแนะนำนี้)

## ขั้นตอนที่ 1: สร้างโปรเจคคอนโซล .NET ใหม่

```bash
dotnet new console -n PdfGraphicsStateDemo
cd PdfGraphicsStateDemo
dotnet add package Aspose.Pdf
```

คำสั่ง `dotnet add package` จะดึงไลบรารี **Aspose.Pdf** ซึ่งให้ API ที่ใช้ตลอดคู่มือ

## ขั้นตอนที่ 2: โหลด PDF และเข้าถึงหน้าแรก

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.IO;

// Load the source PDF
using var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

// PDF pages are 1‑based; page 1 is the first page
Page firstPage = pdfDoc.Pages[1];
```

*ทำไมจึงสำคัญ*: โมเดลอ็อบเจ็กต์ของ PDF ใช้การจัดอันดับเริ่มจาก 1 ดังนั้นการเรียก `Pages[0]` จะทำให้เกิดข้อยกเว้น การโหลดเอกสารภายในบล็อก `using` จะทำให้การจัดการไฟล์ถูกปล่อยอัตโนมัติ

## ขั้นตอนที่ 3: ตรวจสอบว่ามีพจนานุกรม ExtGState อยู่

```csharp
// The page’s Resources dictionary holds many sub‑dictionaries (Font, XObject, etc.)
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);

// Try to get the existing ExtGState dictionary; create one if it is missing
CosCosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create an empty ExtGState dictionary and attach it to the page resources
    extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

**เคล็ดลับ**: ตรวจสอบการมีอยู่ของ `ExtGState` เสมอ บาง PDF ถูกสร้างโดยไม่มีมัน และการพยายามแก้ไขรายการที่ไม่มีอยู่จะทำให้เกิด `KeyNotFoundException`

## ขั้นตอนที่ 4: สร้าง graphics state ใหม่

```csharp
// Create a fresh dictionary for the new graphics state
CosCosPdfDictionary newGraphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Stroke opacity (CA) – 1.0 means fully opaque
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes the fill 50 % transparent
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing operation
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

*ทำไมต้องมีรายการเหล่านี้*:
- `CA` มีผลต่อเส้นและขอบ (stroke)
- `ca` มีผลต่อรูปแบบที่เติมและข้อความ
- `BM` กำหนดวิธีการผสมสีต้นทางกับสีปลายทาง; `"Normal"` จะรักษาลักษณะเดิมไว้พร้อมกับคำนึงถึงความทึบแสง

## ขั้นตอนที่ 5: แทรก graphics state ลงในพจนานุกรม ExtGState

```csharp
// Choose a unique name for the graphics state; "GS0" is common for the first entry
extGStateDict.Add("GS0", newGraphicsState);
```

หากคุณต้องการหลายสถานะ ให้เพิ่มเลขต่อท้าย (`GS1`, `GS2`, …) และอ้างอิงชื่อที่ถูกต้องในภายหลังใน content stream ของคุณ

## ขั้นตอนที่ 6: บันทึก PDF ที่แก้ไขแล้ว

```csharp
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
Console.WriteLine("PDF saved with new graphics state.");
```

ไฟล์ที่ได้ (`output.pdf`) มีเนื้อหาภาพเดียวกับต้นฉบับ แต่คำสั่งการวาดใด ๆ ที่อ้างอิง `/GS0` ต่อมาจะถูกแสดงด้วย **PDF opacity** 0.5 และ **PDF blend mode** `Normal`

## ตัวอย่างที่สามารถรันได้เต็มรูปแบบ

คัดลอกโปรแกรมต่อไปนี้ไปยังไฟล์ `Program.cs` ของโปรเจคที่สร้างในขั้นตอน 1 ปรับค่า `YOUR_DIRECTORY` ให้ตรงกับสภาพแวดล้อมของคุณ

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.IO;

namespace PdfGraphicsStateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the PDF document
            using var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

            // 2️⃣ Access the first page's resources
            Page firstPage = pdfDoc.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // 3️⃣ Retrieve or create ExtGState dictionary
            CosCosPdfDictionary extGStateDict;
            if (resourcesEditor.ContainsKey("ExtGState"))
            {
                extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
            }
            else
            {
                extGStateDict = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
                resourcesEditor["ExtGState"] = extGStateDict;
            }

            // 4️⃣ Define a new graphics state (opacity & blend mode)
            var newGraphicsState = CosCosPdfDictionary.CreateEmptyDictionary(pdfDoc);
            newGraphicsState.Add("CA", new CosPdfNumber(1));           // stroke opacity
            newGraphicsState.Add("ca", new CosPdfNumber(0.5));         // fill opacity
            newGraphicsState.Add("BM", new CosPdfName("Normal"));     // blend mode

            // 5️⃣ Add the graphics state to the ExtGState dictionary
            extGStateDict.Add("GS0", newGraphicsState);

            // 6️⃣ Save the modified PDF
            pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
            Console.WriteLine("PDF saved with new graphics state.");
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เปิด `output.pdf` ด้วยโปรแกรมดูใดก็ได้ หากคุณเพิ่มคำสั่งการวาดที่อ้างอิง `/GS0` ต่อมา (เช่น ผ่าน content stream หรือการเรียก API ของ Aspose.Pdf อื่น) การเติมสีจะปรากฏที่ความทึบ 50 % ในขณะที่เส้นขอบยังคงทึบเต็มที่ โหมดการผสมสีจะคงเป็น `"Normal"` ซึ่งเหมาะกับสถานการณ์การคอมโพสท์ส่วนใหญ่

## การจัดการกับความแปรผันทั่วไป

| สถานการณ์ | สิ่งที่ต้องเปลี่ยน | เหตุผล |
|-----------|----------------|--------|
| **หลายหน้าต้องการสถานะเดียวกัน** | วนลูป `pdfDoc.Pages` และทำซ้ำขั้นตอน 3‑5 สำหรับแต่ละหน้า หรือสร้าง ExtGState dictionary เดียวในทรัพยากรระดับเอกสารและอ้างอิงจากทุกหน้า | ป้องกันการซ้ำซ้อนของพจนานุกรมและทำให้ขนาดไฟล์เล็กลง |
| **ค่าความทึบแตกต่างตามหน้า** | ใช้ชื่อที่แตกต่าง (`GS0`, `GS1`, …) และปรับ `ca`/`CA` ให้เหมาะสมก่อนเพิ่มลงใน ExtGState ของแต่ละหน้า | ให้การควบคุมการเรนเดอร์อย่างละเอียด |
| **ExtGState มีคีย์ชื่อ “GS0” อยู่แล้ว** | เลือกชื่อคีย์อื่น (`GS1`, `MyState`, …) และอัปเดต content stream ที่อ้างอิงถึงคีย์นั้น | ป้องกันการเขียนทับ graphics state ที่มีอยู่โดยไม่ได้ตั้งใจ |
| **PDF ถูกสร้างโดยไม่มีพจนานุกรม ExtGState** | โค้ดในขั้นตอน 3 จะสร้างพจนานุกรมให้แล้ว ดังนั้นไม่ต้องทำงานเพิ่มเติม | รับประกันว่าการดำเนินการจะสำเร็จสำหรับ PDF ใด ๆ ก็ตาม |

## เคล็ดลับและแนวทางปฏิบัติที่ดีที่สุด

* **Validate the PDF after modification** – ใช้ `pdfDoc.Validate()` (มีใน Aspose.Pdf รุ่นใหม่) เพื่อจับปัญหาโครงสร้างตั้งแต่ต้น
* **Keep the graphics‑state dictionary small** – รวมเฉพาะรายการที่ต้องการ; คีย์เพิ่มเติมจะทำให้ไฟล์ใหญ่ขึ้นโดยไม่มีประโยชน์
* **เมื่อเพิ่ม content stream ที่ใช้สถานะใหม่**, ให้ใส่ `/GS0 gs` ไว้หน้าตัวดำเนินการการวาด ตัวอย่าง: `contentStream.Append("/GS0 gs 100 100 m 200 200 l S");`
* **Dispose of large PDFs promptly** – คำสั่ง `using` ในตัวอย่างทำให้การจัดการไฟล์ถูกปล่อยทันที ซึ่งสำคัญในสถานการณ์บริการเว็บ

## สรุป

ตอนนี้คุณรู้วิธี **add graphics state pdf** ด้วย Aspose.Pdf, ปรับ **PDF opacity**, ตั้งค่า **PDF blend mode**, และทำงานกับ **ExtGState dictionary** อย่างปลอดภัย ตัวอย่างโค้ดเต็มพร้อมใช้งานในโปรเจค .NET ใด ๆ และเคล็ดลับที่แนบมาช่วยให้คุณหลีกเลี่ยงข้อผิดพลาดทั่วไป

ต่อไปสำรวจวิธีนำ graphics state ที่สร้างใหม่ไปใช้กับข้อความ, รูปภาพ, หรือรูปเวกเตอร์ คุณอาจตรวจสอบรายการ ExtGState อื่น ๆ เช่น `SM` (การปรับเส้น) หรือค่า `CA` มากกว่า 1 สำหรับเอฟเฟกต์พิเศษ ขอให้สนุกกับการทำงานกับ PDF!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโปรเจคของคุณ

- [วิธีเพิ่ม Page Stamps ใน PDF ด้วย Aspose.PDF สำหรับ .NET: คู่มือเต็ม](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [เพิ่ม Image Stamps ใน PDF ด้วย Aspose.PDF สำหรับ .NET: คู่มือขั้นตอนโดยละเอียด](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)
- [วิธีลบ Graphics จาก PDF ด้วย Aspose.PDF .NET: คู่มือเต็ม](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}