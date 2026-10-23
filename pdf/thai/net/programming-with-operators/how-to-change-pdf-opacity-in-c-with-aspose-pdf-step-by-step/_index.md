---
category: general
date: 2026-10-23
description: วิธีเปลี่ยนความทึบของ PDF ด้วย Aspose.Pdf ใน C# เรียนรู้การแก้ไข ExtGState
  ตั้งค่าความทึบของเส้นขอบ/การเติมสี และใช้โหมดผสมในไม่กี่บรรทัดของโค้ด.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change PDF opacity
- Aspose.Pdf opacity
- PDF graphics state
- ExtGState dictionary
- C# PDF manipulation
- PDF blend mode
language: th
lastmod: 2026-10-23
og_description: วิธีเปลี่ยนความโปร่งใสของ PDF ด้วย Aspose.Pdf ใน C#. ปฏิบัติตามคำแนะนำสั้น
  ๆ นี้เพื่อปรับความโปร่งใสของเส้นและการเติมสี ตั้งค่าโหมดการผสม และบันทึกเอกสารที่อัปเดต.
og_image_alt: Screenshot of a PDF page with semi‑transparent graphics created by Aspose.Pdf
  in C#
og_title: วิธีเปลี่ยนความทึบของ PDF ใน C# – บทเรียน Aspose.Pdf อย่างครบถ้วน
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  headline: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  type: TechArticle
- description: How to change PDF opacity using Aspose.Pdf in C#. Learn to edit ExtGState,
    set stroke/fill opacity, and apply blend modes in just a few lines of code.
  name: How to change PDF opacity in C# with Aspose.Pdf – step‑by‑step guide
  steps:
  - name: Load the PDF document
    text: '```csharp using Aspose.Pdf;'
  - name: Get the first page and its resource dictionary
    text: '```csharp // Step 2: Get the first page and its resource dictionary var
      firstPage = pdfDocument.Pages[1]; var resourcesEditor = new DictionaryEditor(firstPage.Resources);
      ```'
  - name: Retrieve (or create) the ExtGState dictionary
    text: '```csharp // Step 3: Retrieve the ExtGState dictionary from the page resources
      // If ExtGState does not exist, create an empty one. CosPdfDictionary extGStateDict;
      if (resourcesEditor.ContainsKey("ExtGState")) { extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
      } else { extGStateDic'
  - name: Create a new graphics state dictionary and define opacity entries
    text: '```csharp // Step 4: Create a new graphics state dictionary and define
      its entries var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
      var graphicsStateEntries = new[] { new KeyValuePair<string, ICosPdfPrimitive>("CA",
      new CosPdfNumber(1.0)), // Stroke opacity (fully opaque)'
  - name: Add the new graphics state to the ExtGState dictionary
    text: '```csharp // Step 5: Add the new graphics state to the ExtGState dictionary
      (named "GS0") extGStateDict.Add("GS0", graphicsStateDict); ```'
  - name: Save the updated PDF document
    text: '```csharp // Step 6: Save the updated PDF document pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
      } ```'
  type: HowTo
tags:
- PDF
- C#
- Aspose.Pdf
- Opacity
- GraphicsState
title: วิธีเปลี่ยนความทึบของ PDF ใน C# ด้วย Aspose.Pdf – คู่มือขั้นตอนโดยละเอียด
url: /th/net/programming-with-operators/how-to-change-pdf-opacity-in-c-with-aspose-pdf-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการเปลี่ยนความทึบของ PDF ใน C# ด้วย Aspose.Pdf – คู่มือขั้นตอนต่อขั้นตอน

หากคุณต้องการ **วิธีการเปลี่ยนความทึบของ PDF** สำหรับองค์ประกอบเฉพาะ คู่มือฉบับนี้จะแสดงวิธีแก้ไขที่สมบูรณ์และสามารถรันได้ คุณจะได้เห็นวิธีแก้ไขพจนานุกรม ExtGState ตั้งค่าความทึบของเส้นและการเติมสี และเลือกโหมดการผสมสี — ทั้งหมดด้วยไม่กี่บรรทัดของโค้ด C# ที่ชัดเจน

การเปลี่ยนความทึบของ PDF มีประโยชน์เมื่อคุณต้องการลายน้ำ, กราฟิกซ้อน, หรือเอฟเฟ็กต์ภาพที่ละเอียดอ่อนโดยไม่ต้องสร้างเอกสารใหม่ทั้งหมด คู่มือสมมติว่าคุณมีสภาพแวดล้อม C# พื้นฐานและไลบรารี Aspose.Pdf for .NET ติดตั้งแล้ว

![วิธีการเปลี่ยนความทึบของ PDF โดยใช้ Aspose.Pdf ใน C#](https://example.com/og-image.png)

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.7+)
* สำเนาแบบมีลิขสิทธิ์ของ **Aspose.Pdf for .NET** (รุ่นทดลองฟรีใช้สำหรับทดสอบได้)
* ไฟล์ PDF อินพุตที่อยู่ในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโค้ดได้
* Visual Studio 2022 หรือโปรแกรมแก้ไข C# ใด ๆ ที่คุณชอบ

ไม่มีแพ็กเกจ NuGet เพิ่มเติมที่จำเป็น — Aspose.Pdf มีทุกประเภทที่ใช้ในบทเรียนนี้แล้ว

## ทำความเข้าใจสถานะกราฟิกของ PDF

หน้า PDF จะเก็บพารามิเตอร์การวาดในอ็อบเจ็กต์ **graphics state** พจนานุกรม **ExtGState** จะบรรจุรายการเช่น:

* **CA** – ความทึบของเส้น (0 = โปร่งใส, 1 = ทึบ)
* **ca** – ความทึบของการเติมสี
* **BM** – โหมดการผสมสี (เช่น *Normal*, *Multiply*, *Screen*)

โดยการสร้างพจนานุกรมสถานะกราฟิกใหม่และเพิ่มลงในคอลเลกชัน ExtGState ของหน้า คุณสามารถอ้างอิงสถานะนี้ในสตรีมเนื้อหาได้ในภายหลัง วิธีนี้ช่วยหลีกเลี่ยงการเขียนทับเนื้อหาทั้งหมดของหน้าและทำงานกับ PDF ใด ๆ ที่มีอยู่

## วิธีการเปลี่ยนความทึบของ PDF ด้วย Aspose.Pdf

ขั้นตอนหกขั้นตอนต่อไปนี้ครอบคลุมกระบวนการทั้งหมด — ตั้งแต่การโหลดเอกสารจนถึงการบันทึกไฟล์ที่แก้ไขแล้ว แต่ละขั้นตอนรวมโค้ดที่ต้องใช้และคำอธิบายว่าทำไมขั้นตอนนั้นสำคัญ

### ขั้นตอนที่ 1: โหลดเอกสาร PDF

```csharp
using Aspose.Pdf;

// Step 1: Load the PDF document
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here
}
```

**ทำไมขั้นตอนนี้สำคัญ** – การเปิดไฟล์ด้วย `Aspose.Pdf.Document` ให้คุณเข้าถึงโครงสร้างภายในของ PDF อย่างเต็มที่ รวมถึงทรัพยากรของหน้า ที่พจนานุกรม **ExtGState** อยู่

### ขั้นตอนที่ 2: ดึงหน้าแรกและพจนานุกรมทรัพยากรของมัน

```csharp
// Step 2: Get the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

**ทำไมขั้นตอนนี้สำคัญ** – ทุกหน้ามีพจนานุกรม *Resources* ที่จัดกลุ่มฟอนต์, รูปภาพ, และสถานะกราฟิก `DictionaryEditor` ให้การเข้าถึงแบบอ่าน/เขียนที่สะดวกต่อคอลเลกชันนั้น

### ขั้นตอนที่ 3: ดึง (หรือสร้าง) พจนานุกรม ExtGState

```csharp
// Step 3: Retrieve the ExtGState dictionary from the page resources
// If ExtGState does not exist, create an empty one.
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

**ทำไมขั้นตอนนี้สำคัญ** – PDF บางไฟล์อาจมีรายการ **ExtGState** อยู่แล้ว; บางไฟล์อาจไม่มี เงื่อนไขนี้ทำให้บทเรียนทำงานได้กับทั้งสองกรณี ทำให้ทนทานต่อไฟล์จริง

### ขั้นตอนที่ 4: สร้างพจนานุกรมสถานะกราฟิกใหม่และกำหนดรายการความทึบ

```csharp
// Step 4: Create a new graphics state dictionary and define its entries
var graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var entry in graphicsStateEntries)
    graphicsStateDict.Add(entry);
```

**ทำไมขั้นตอนนี้สำคัญ** – รายการสำคัญสามรายการควบคุมวิธีการแสดงผลของคำสั่งวาด:

* `CA = 1.0` ทำให้เส้นขอบเต็มที่มองเห็นได้
* `ca = 0.5` ทำให้รูปที่เติมสีเป็นกึ่งโปร่งใส
* `BM = Normal` ใช้โหมดการผสมสีเริ่มต้น; คุณสามารถเปลี่ยน `"Normal"` เป็น `"Multiply"` หรือ `"Screen"` เพื่อสร้างเอฟเฟ็กต์ศิลป์ได้

### ขั้นตอนที่ 5: เพิ่มสถานะกราฟิกใหม่ลงในพจนานุกรม ExtGState

```csharp
// Step 5: Add the new graphics state to the ExtGState dictionary (named "GS0")
extGStateDict.Add("GS0", graphicsStateDict);
```

**ทำไมขั้นตอนนี้สำคัญ** – การตั้งชื่อรายการเป็น `"GS0"` จะสร้างอ้างอิงที่คุณสามารถใช้ในสตรีมเนื้อหา (`/GS0 gs`) ได้ หากต้องการระดับความทึบหลายระดับ ให้เพิ่มรายการเพิ่มเติม (`"GS1"`, `"GS2"` ฯลฯ) พร้อมค่า `CA`/`ca` ที่แตกต่างกัน

### ขั้นตอนที่ 6: บันทึกเอกสาร PDF ที่อัปเดต

```csharp
// Step 6: Save the updated PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**ทำไมขั้นตอนนี้สำคัญ** – การบันทึกการเปลี่ยนแปลงจะเขียนพจนานุกรม **ExtGState** ที่แก้ไขแล้วกลับไปยังไฟล์ PDF ผลลัพธ์จึงมีสถานะกราฟิกที่สามารถนำกลับมาใช้ซ้ำได้โดยคำสั่งวาดใด ๆ

## การใช้สถานะกราฟิกใหม่กับเนื้อหาของหน้า

ขั้นตอนข้างต้นเพียงสร้างสถานะกราฟิก; คุณยังต้องอ้างอิงมันในสตรีมเนื้อหาของหน้า ด้านล่างเป็นตัวอย่างสั้น ๆ ที่วาดสี่เหลี่ยมกึ่งโปร่งใสโดยใช้สถานะที่เพิ่มไว้เมื่อคราวก่อน:

```csharp
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    var page = pdfDocument.Pages[1];
    var content = new PageContentEditor(page);
    // Begin the graphics state GS0
    content.InsertContent(0, "q /GS0 gs\n"); // Save graphics state and apply GS0
    // Draw a rectangle (100,100) to (300,300)
    content.InsertContent(0, "0.2 0.6 0.8 rg\n"); // Set fill color (light blue)
    content.InsertContent(0, "100 100 200 200 re\n");
    content.InsertContent(0, "f\n"); // Fill rectangle with current fill opacity
    // Restore graphics state
    content.InsertContent(0, "Q\n");
    pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
}
```

**Explanation** – ตัวดำเนินการ `q` บันทึกสถานะกราฟิกปัจจุบัน, `/GS0 gs` ใช้การตั้งค่าความทึบ, วาดสี่เหลี่ยม, แล้ว `Q` คืนสถานะเดิม คุณสามารถวางโค้ดนี้ได้ทุกตำแหน่งบนหน้า ก่อนหรือหลังเนื้อหาที่มีอยู่แล้ว ขึ้นกับการจัดลำดับชั้นภาพที่ต้องการ

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| อาการ | สาเหตุ | วิธีแก้ |
|---------|-------|-----|
| ความทึบไม่เปลี่ยนแปลง | หน้าไม่มีรายการ ExtGState หรือเนื้อหาไม่ได้อ้างอิงสถานะใหม่ | ตรวจสอบว่า `ExtGState` มีอยู่และสตรีมเนื้อหามี `/GS0 gs` (หรือชื่อที่คุณตั้ง) |
| โหมดการผสมสีไม่มีผล | ใช้สีสเปซหรือเวอร์ชัน PDF ที่ไม่รองรับ | ตรวจสอบว่าเวอร์ชัน PDF อย่างน้อยเป็น 1.4 (ต้องการความโปร่งใส) และไม่ผสมสีสปอตกับโหมดการผสม |
| เอกสารไม่เปิดในโปรแกรมอ่านเก่า | PDF 1.3 หรือเก่ากว่าไม่รองรับความโปร่งใส | ตั้งค่า `pdfDocument.Version = 1.4;` ก่อนบันทึก หรืออัปเกรดเวอร์ชัน PDF อย่างชัดเจน |

## การทดสอบผลลัพธ์

เปิด `output.pdf` ด้วย Adobe Acrobat Reader, Foxit, หรือโปรแกรมอ่าน PDF สมัยใหม่ใด ๆ คุณควรเห็นสี่เหลี่ยมที่แสดงความทึบการเติม 50 % ขณะที่ขอบยังคงทึบเต็ม ใช้เมนู *Edit → Preferences → Accessibility* เพื่อสลับ “Use high‑contrast colors” และยืนยันว่าเอฟเฟ็กต์กึ่งโปร่งใสยังคงอยู่

หากต้องการตรวจสอบแบบโปรแกรมมิ่ง Aspose.Pdf ให้คุณอ่านพจนานุกรมสถานะกราฟิกกลับมาได้:

```csharp
var gs = pdfDocument.Pages[1].Resources["ExtGState"]["GS0"].ToCosPdfDictionary();
var fillOpacity = ((CosPdfNumber)gs["ca"]).Value; // Should be 0.5
```

## การขยายเทคนิค

* **หลายระดับความทึบ** – เพิ่มรายการเพิ่มเติม (`"GS1"`, `"GS2"`) พร้อมค่า `ca` ที่ต่างกันและอ้างอิงตามต้องการ
* **โหมดการผสมสีต่าง ๆ** – แทนที่ `"Normal"` ด้วย `"Multiply"` หรือ `"Screen"` เพื่อสร้างการซ้อนทับเชิงศิลป์
* **ใช้กับรูปภาพ** – ใช้สถานะกราฟิกเดียวกันก่อนตัวดำเนินการ `Do` ที่วาด XObject รูปภาพ

การปรับเปลี่ยนเหล่านี้ช่วยให้คุณสร้างลายน้ำ, ไฮไลท์ส่วนต่าง ๆ, หรือออกแบบกราฟิกซับซ้อนโดยไม่ต้องแปลง PDF เป็นภาพ raster

## สรุป

คุณได้เรียนรู้ **วิธีการเปลี่ยนความทึบของ PDF** ใน C# ด้วย Aspose.Pdf แล้ว โดยการสร้างสถานะกราฟิกแบบกำหนดเอง, เพิ่มลงในพจนานุกรม ExtGState ของหน้า, และเรียกใช้สถานะนั้นในสตรีมเนื้อหา คุณจะได้การควบคุมระดับละเอียดของความโปร่งใสของเส้นและการเติมสี รวมถึงโหมดการผสมสี ตัวอย่างเต็มพร้อมคัดลอก, รัน, และปรับใช้กับสถานการณ์การจัดการ PDF ใด ๆ ที่คุณเจอ

พร้อมรับความท้าทายต่อไปหรือยัง? ลองผสานเทคนิคนี้กับ **Aspose.Pdf opacity** บนรูปภาพ, หรือสำรวจเอฟเฟ็กต์ **PDF blend mode** เพื่อสร้างโอเวอร์เลย์ระดับมืออาชีพ ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ต่อ‑ขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณเอง

- [Change PDF Opacity with Aspose.PDF – Complete C# Guide](/pdf/english/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-complete-c-guide/)
- [Change opacity PDF in C# with Aspose.Pdf – step‑by‑step guide](/pdf/english/net/programming-with-pdf-pages/change-opacity-pdf-in-c-with-aspose-pdf-step-by-step-guide/)
- [How to change PDF transparency in C# using Aspose.Pdf](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-in-c-using-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}