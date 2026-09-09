---
category: general
date: 2026-09-08
description: เพิ่มความโปร่งใสให้กับ PDF ด้วย Aspose.PDF for .NET – เรียนรู้การตั้งค่าความทึบของเส้นและการเติมสี,
  โหมดผสม, และบันทึกผลลัพธ์ภายในไม่กี่นาที.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- aspose.pdf transparency
- pdf graphics state
- extgstate dictionary
- pdf opacity settings
language: th
lastmod: 2026-09-08
og_description: เพิ่มความโปร่งใสให้กับ PDF ด้วย Aspose.PDF สำหรับ .NET บทเรียนนี้แสดงวิธีการแก้ไขพจนานุกรม
  ExtGState ตั้งค่าความทึบแสงและโหมดการผสมสี แล้วบันทึกไฟล์ที่อัปเดต.
og_image_alt: Screenshot of a PDF page showing semi‑transparent shapes created with
  Aspose.PDF
og_title: เพิ่มความโปร่งใสให้กับ PDF ด้วย Aspose.PDF – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Add transparency to PDF with Aspose.PDF for .NET – learn to set stroke
    and fill opacity, blend mode, and save the result in minutes.
  headline: How to add transparency to PDF files using Aspose.PDF for .NET
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: วิธีเพิ่มความโปร่งใสให้ไฟล์ PDF ด้วย Aspose.PDF สำหรับ .NET
url: /th/net/images-graphics/how-to-add-transparency-to-pdf-files-using-aspose-pdf-for-ne/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเพิ่มความโปร่งใสให้ไฟล์ PDF ด้วย Aspose.PDF for .NET

หากคุณต้องการ **เพิ่มความโปร่งใสให้กับ PDF** เอกสาร คู่มือนี้จะแสดงให้คุณเห็นอย่างละเอียดว่า如何ปรับเปลี่ยน graphics state ด้วย Aspose.PDF for .NET คุณจะได้เรียนรู้การตั้งค่า stroke opacity, fill opacity, และ blend mode บนหน้าเดียว แล้วบันทึกผลลัพธ์เป็นไฟล์ใหม่

ความโปร่งใสเป็นความต้องการทั่วไปสำหรับลายน้ำ, กราฟิกซ้อน, หรือเอฟเฟกต์ภาพในรายงาน ในบทแนะนำนี้คุณจะได้เห็นโค้ดที่ทำงานได้เต็มรูปแบบ, เข้าใจเหตุผลที่แต่ละการเรียก API มีความสำคัญ, และรับเคล็ดลับการจัดการกรณีขอบเช่นรายการทรัพยากรที่หายไป

## สิ่งที่คุณต้องเตรียม

ก่อนเริ่มทำงาน, ตรวจสอบให้แน่ใจว่าคุณมี:

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานได้กับ .NET Framework 4.6+)
* ใบอนุญาต Aspose.PDF for .NET ที่ถูกต้อง (รุ่นทดลองใช้ฟรีสามารถใช้ทดสอบได้)
* ไฟล์ PDF อินพุตชื่อ `input.pdf` ที่วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโค้ด
* สภาพแวดล้อมการพัฒนา C# (Visual Studio, Rider หรือ VS Code)

ไม่จำเป็นต้องติดตั้งแพ็กเกจ NuGet เพิ่มเติมนอกจาก `Aspose.Pdf`.

## ภาพรวมของ PDF graphics state

PDF graphics state ถูกเก็บไว้ใน **dictionary ExtGState** ภายใน dictionary ของทรัพยากรของหน้าแต่ละหน้า แต่ละรายการกำหนดพารามิเตอร์การเรนเดอร์เช่น ความกว้างของเส้น, ความโปร่งใส, และ blend mode โดยการสร้างอ็อบเจ็กต์ graphics state ใหม่และเพิ่มลงใน dictionary `ExtGState` คุณสามารถใช้การตั้งค่าความโปร่งใสเดียวกันซ้ำได้หลายคำสั่งการวาด

การเข้าใจโครงสร้างนี้ช่วยให้คุณหลีกเลี่ยงข้อผิดพลาดทั่วไป, เช่น การพยายามตั้งค่า opacity โดยตรงบนอ็อบเจ็กต์ `Page` (ซึ่ง API ไม่รองรับ) แทนที่จะทำงานกับอ็อบเจ็กต์ COS ระดับต่ำที่แมพตรงกับสเปค PDF

## ขั้นตอนที่ 1: โหลดเอกสาร PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Cos;

// Load the source PDF
var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");
```

*ทำไมต้องทำขั้นตอนนี้?*  
`Document` เป็นจุดเริ่มต้นสำหรับการจัดการ PDF ใด ๆ การโหลดไฟล์จะสร้างการแสดงผลในหน่วยความจำที่คุณสามารถแก้ไขได้โดยไม่ต้องแตะไฟล์ต้นฉบับบนดิสก์

## ขั้นตอนที่ 2: รับหน้าแรกและตัวแก้ไข dictionary ของทรัพยากร

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor provides convenient access to the page’s resources
var resourceEditor = new DictionaryEditor(page.Resources);
```

*ทำไมต้องทำขั้นตอนนี้?*  
รายการ graphics‑state ทั้งหมดอยู่ภายใน resources ของหน้า `DictionaryEditor` ทำหน้าที่เป็นชั้นนามธรรมสำหรับการจัดการ dictionary COS ระดับต่ำ, ให้คุณอ่านหรือสร้างรายการเช่น `ExtGState`

## ขั้นตอนที่ 3: ดึง dictionary ExtGState จาก resources ของหน้า

```csharp
// The ExtGState entry may already exist; if not, create it
CosPdfDictionary extGStateDict;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGStateDict = (CosPdfDictionary)resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a new ExtGState dictionary and attach it to the page resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
    resourceEditor.Add("ExtGState", extGStateDict);
}
```

*ทำไมต้องทำขั้นตอนนี้?*  
PDF อาจไม่มี dictionary `ExtGState` อยู่เลย โค้ดข้างต้นจัดการกับกรณีที่มีและไม่มีอย่างปลอดภัย, ทำให้บทแนะนำทำงานได้กับ PDF ใด ๆ

## ขั้นตอนที่ 4: สร้าง dictionary graphics state ใหม่และกำหนดรายการของมัน

```csharp
// Create an empty dictionary that will hold our transparency settings
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Define the entries:
//   CA – stroke opacity (0 = fully transparent, 1 = opaque)
//   ca – fill opacity
//   BM – blend mode (Normal, Multiply, etc.)
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity = 100%
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity = 50%
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Standard blend mode
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

*ทำไมต้องทำขั้นตอนนี้?*  
`CA` และ `ca` เป็นโอเปอเรเตอร์ของ PDF ที่ควบคุมความโปร่งใสสำหรับการ stroke และการ fill (non‑stroking) การตั้งค่า `BM` เป็น `Normal` จะรักษาพฤติกรรมการผสมแบบเริ่มต้น, แต่คุณสามารถทดลองกับ `Multiply` หรือ `Screen` เพื่อเอฟเฟกต์ศิลปะ

## ขั้นตอนที่ 5: เพิ่ม graphics state ใหม่ลงใน dictionary ExtGState

```csharp
// Choose a unique name for the graphics state (e.g., GS0)
extGStateDict.Add("GS0", newGraphicsState);
```

*ทำไมต้องทำขั้นตอนนี้?*  
ชื่อ `GS0` จะกลายเป็นอ้างอิงที่คุณสามารถใช้ต่อใน content stream (`/GS0 gs`) การเพิ่มเข้าไปใน `ExtGState` ทำให้ PDF รู้จักพารามิเตอร์ความโปร่งใสใหม่

## ขั้นตอนที่ 6: ใช้ graphics state ใน content stream (ไม่บังคับ)

หากคุณต้องการเห็นผลทันที, คุณสามารถใส่คำสั่งวาดง่าย ๆ ที่ใช้สถานะใหม่ไว้ด้านหน้า:

```csharp
// Build a content stream that draws a semi‑transparent rectangle
var content = new PageContent();
content.Operators.Add(new Operator("q"));                     // Save graphics state
content.Operators.Add(new Operator("GS0", "gs"));            // Set our custom graphics state
content.Operators.Add(new Operator("0.2", "0.2", "0.8", "rg")); // Set fill color (light blue)
content.Operators.Add(new Operator("100", "500", "200", "100", "re")); // Rectangle
content.Operators.Add(new Operator("f"));                    // Fill
content.Operators.Add(new Operator("Q"));                     // Restore graphics state

// Insert the new content at the beginning of the page
page.Contents.Insert(0, content);
```

*ทำไมต้องทำขั้นตอนนี้?*  
ส่วนเสริมนี้แสดงให้เห็นว่า graphics state ที่คุณเพิ่ม (`GS0`) ถูกนำไปใช้จริงอย่างไร สี่เหลี่ยมจะปรากฏด้วยความโปร่งใสของ fill 50 % ในขณะที่เส้นขอบยังคงเต็มที่

## ขั้นตอนที่ 7: บันทึกเอกสาร PDF ที่แก้ไขแล้ว

```csharp
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
```

ไฟล์ผลลัพธ์ `output.pdf` จะมีรายการ `ExtGState` ใหม่และหากคุณเพิ่มส่วนเสริมเนื้อหาแล้ว จะมีสี่เหลี่ยมซ้อนที่มีความโปร่งใสกึ่งครึ่ง

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณเปิด `output.pdf` ด้วย Adobe Acrobat Reader หรือโปรแกรมดู PDF ใด ๆ คุณควรเห็น:

* เนื้อหาหน้าเดิมไม่เปลี่ยนแปลง
* หากคุณรันโค้ดวาดเสริม, จะมีสี่เหลี่ยมสีฟ้าอ่อนที่ fill มีความโปร่งใส 50 % ทำให้หน้าพื้นหลังมองเห็นได้ผ่านสี่เหลี่ยม

## รายการโค้ดเต็ม

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using Aspose.Pdf.Operators;
using System.Collections.Generic;

class AddTransparencyExample
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2. Get the first page and its resources
        var page = pdfDoc.Pages[1];
        var resourceEditor = new DictionaryEditor(page.Resources);

        // 3. Retrieve or create ExtGState dictionary
        CosPdfDictionary extGStateDict;
        if (resourceEditor.ContainsKey("ExtGState"))
            extGStateDict = (CosPdfDictionary)resourceEditor["ExtGState"].ToCosPdfDictionary();
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
            resourceEditor.Add("ExtGState", extGStateDict);
        }

        // 4. Create new graphics state with transparency settings
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);
        var graphicsStateEntries = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // Fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
        };
        foreach (var entry in graphicsStateEntries)
            newGraphicsState.Add(entry);

        // 5. Add the graphics state to ExtGState with a unique name
        extGStateDict.Add("GS0", newGraphicsState);

        // 6. (Optional) Draw a rectangle using the new state
        var content = new PageContent();
        content.Operators.Add(new Operator("q"));
        content.Operators.Add(new Operator("GS0", "gs"));
        content.Operators.Add(new Operator("0.2", "0.2", "0.8", "rg"));
        content.Operators.Add(new Operator("100", "500", "200", "100", "re"));
        content.Operators.Add(new Operator("f"));
        content.Operators.Add(new Operator("Q"));
        page.Contents.Insert(0, content);

        // 7. Save the updated PDF
        pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

คัดลอกโค้ดไปยังแอปพลิเคชันคอนโซล, แทนที่ `YOUR_DIRECTORY` ด้วยพาธโฟลเดอร์จริง, แล้วรัน โปรแกรมจะสร้าง `output.pdf` พร้อมการตั้งค่าความโปร่งใสที่เพิ่มเข้าไป

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| อาการ | สาเหตุ | วิธีแก้ |
|---------|-------|-----|
| `KeyNotFoundException` on `"ExtGState"` | หน้าไม่มีรายการ `ExtGState` | บทแนะนำได้สร้าง dictionary เมื่อไม่มีอยู่แล้ว; ตรวจสอบให้แน่ใจว่าคุณใช้บล็อกเงื่อนไขที่ให้มา |
| ความโปร่งใสไม่แสดงในตัวดู | คำสั่งวาดไม่เคยอ้างอิง `GS0` | เพิ่มโอเปอเรเตอร์ `gs` (`"GS0 gs"`) ก่อนการ stroke/fill ใด ๆ ตามที่แสดงในส่วนเสริม |
| PDF เสียหายหลังบันทึก | ผสมผสาน API ระดับสูง `Page` กับอ็อบเจ็กต์ COS ระดับต่ำอย่างไม่ถูกต้อง | ปฏิบัติตามรูปแบบการดึง `CosPdfDictionary` ผ่าน `DictionaryEditor` และหลีกเลี่ยงการแก้ไข dictionary เดียวกันสองครั้ง |
| Blend mode ไม่มีผล | ตัวดูไม่รองรับ blend mode ที่เลือก | ใช้ `Normal` เพื่อความเข้ากันได้กว้าง; ทดลอง `Multiply` เฉพาะในตัวดูที่ระบุว่ารองรับ |

## ขั้นตอนต่อไป

ตอนนี้คุณรู้วิธี **เพิ่มความโปร่งใสให้กับ PDF** แล้ว, คุณสามารถ:

* ใช้ graphics state เดียวกันกับหลายหน้าโดยวนลูป `pdfDoc.Pages`
* ผสานความโปร่งใสกับ clipping path เพื่อสร้างลายน้ำขั้นสูง
* สำรวจรายการ ExtGState อื่น ๆ เช่น `SM` (stroke adjustment) หรือ `CA`

## สิ่งที่คุณควรเรียนรู้ต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [How to Add and Align Text Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-text-stamp-aspose-pdf-dotnet/)
- [How to Add a Rotating Image Watermark to PDFs Using Aspose.PDF for .NET](/pdf/english/net/watermarks-backgrounds/add-rotating-image-watermark-aspose-pdf/)
- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET: A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}