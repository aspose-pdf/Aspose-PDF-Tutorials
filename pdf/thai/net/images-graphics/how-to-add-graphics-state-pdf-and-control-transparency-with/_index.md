---
category: general
date: 2026-09-05
description: เรียนรู้วิธีเพิ่มสถานะกราฟิกใน PDF ด้วย Aspose.PDF เพื่อกำหนดความโปร่งใส
  คู่มือแบบขั้นตอนนี้ยังแสดงวิธีเพิ่มความโปร่งใสให้กับ PDF และแก้ไขความโปร่งใสของ
  PDF อย่างมีประสิทธิภาพ
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- how to add transparency pdf
- modify pdf transparency
language: th
lastmod: 2026-09-05
og_description: เพิ่มสถานะกราฟิก PDF ด้วย Aspose.PDF. ทำตามคู่มือนี้เพื่อเรียนรู้วิธีเพิ่มความโปร่งใสให้
  PDF และแก้ไขความโปร่งใสของ PDF ด้วยไม่กี่บรรทัดของโค้ด C#
og_image_alt: Screenshot of C# code that adds graphics state pdf to a PDF document
og_title: เพิ่มสถานะกราฟิกใน PDF ด้วย Aspose.PDF – ควบคุมความโปร่งใสใน C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to add graphics state pdf using Aspose.PDF to set transparency.
    This step‑by‑step guide also shows how to add transparency pdf and modify pdf
    transparency efficiently.
  headline: How to add graphics state pdf and control transparency with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- PDF graphics state
- PDF transparency
- C# PDF manipulation
title: วิธีเพิ่มสถานะกราฟิกใน PDF และควบคุมความโปร่งใสด้วย Aspose.PDF
url: /th/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเพิ่ม graphics state pdf และควบคุมความโปร่งใสด้วย Aspose.PDF

หากคุณต้องการ **add graphics state pdf** ให้กับเอกสารที่มีอยู่ คู่มือนี้จะแสดงขั้นตอนที่ชัดเจน คุณจะได้เห็นวิธีเพิ่ม transparency pdf ด้วย Aspose.PDF for .NET และวิธีแก้ไขความโปร่งใสของ pdf โดยไม่ทำลายโครงสร้างเดิม

ในส่วนต่อไปนี้ เราจะเดินผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบ อธิบายว่าทำไมแต่ละบรรทัดจึงสำคัญ และพูดถึงข้อผิดพลาดทั่วไป เมื่อเสร็จสิ้นคุณจะสามารถฝัง graphics states ที่กำหนดเอง—เช่นค่า alpha ของเส้นขอบและการเติมสี—ลงในหน้า PDF ใดก็ได้

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานได้กับ .NET Framework 4.7+)
* ใบอนุญาต Aspose.PDF for .NET ที่ถูกต้องหรือคีย์ประเมินผลชั่วคราว
* Visual Studio 2022 (หรือโปรแกรมแก้ไข C# ใด ๆ ที่คุณชอบ)
* ไฟล์ PDF เข้า (`input.pdf`) ที่คุณมีสิทธิ์แก้ไข

ไม่จำเป็นต้องใช้แพ็คเกจ NuGet เพิ่มเติมนอกจาก `Aspose.Pdf`

## ขั้นตอนที่ 1: โหลดเอกสาร PDF

การดำเนินการแรกคือการเปิดไฟล์ PDF ต้นฉบับ Aspose.PDF จะห่อไฟล์ไว้ในอ็อบเจ็กต์ `Document` ซึ่งให้คุณเข้าถึงหน้า, แหล่งข้อมูล, และโครงสร้าง PDF ระดับต่ำ

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Generator;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Text;
using Aspose.Pdf.Xmp;

string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Open the document inside a using block so resources are released automatically.
using (var doc = new Document(inputPath))
{
    // The rest of the code lives inside this block.
}
```

**ทำไมจึงสำคัญ:** การเปิดไฟล์ด้วยคำสั่ง `using` รับประกันว่าตัวจัดการไฟล์จะถูกปิดแม้เกิดข้อยกเว้น `Document` ยังโหลดตาราง cross‑reference ทำให้เราสามารถแก้ไขดิกชันนารีระดับต่ำในภายหลังได้

## ขั้นตอนที่ 2: เข้าถึงดิกชันนารีทรัพยากรของหน้าที่หนึ่ง

ทุกหน้าของ PDF มีดิกชันนารี *Resources* ที่เก็บฟอนต์, XObjects, และ graphics states (`ExtGState`). เพื่อแทรก graphics state ใหม่ เราต้องดึงดิกชันนารีนี้ก่อน

```csharp
// Inside the using block
Page page = doc.Pages[1];                     // Get the first page (pages are 1‑based)
var dictEditor = new DictionaryEditor(page.Resources);
var extGState = dictEditor["ExtGState"].ToCosPdfDictionary();
```

**ทำไมจึงสำคัญ:** `ExtGState` เป็นคีย์ที่เก็บอ็อบเจ็กต์ graphics state หากหน้ายังไม่มีรายการ `ExtGState` Aspose.PDF จะสร้างดิกชันนารีเปล่าโดยอัตโนมัติ ทำให้โค้ดทำงานได้ในทั้งสองกรณี

## ขั้นตอนที่ 3: สร้างดิกชันนารี graphics state ใหม่

ดิกชันนารี graphics state กำหนดพฤติกรรมของการวาด สำหรับความโปร่งใสเราต้องการ `CA` (stroke alpha), `ca` (fill alpha) และอาจรวมถึงโหมดผสม (`BM`). โค้ดด้านล่างสร้างดิกชันนารีนั้น

```csharp
// Create an empty COS dictionary that will become our new graphics state.
CosPdfDictionary newGs = CosPdfDictionary.CreateEmptyDictionary(doc);

// Define the entries we want: 1.0 stroke opacity, 0.5 fill opacity, Normal blend mode.
var entries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke alpha (fully opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // fill alpha (50 % transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // blend mode
};

foreach (var entry in entries)
{
    newGs.Add(entry);
}
```

**ทำไมจึงสำคัญ:**  
* `CA` ควบคุมความทึบของเส้นที่วาด (เส้น, ขอบ)  
* `ca` ควบคุมความทึบของวัตถุที่เติมสี (รูปร่าง, ข้อความ)  
* `BM` เลือกโหมดผสม; “Normal” เป็นค่าที่ใช้บ่อยที่สุดและทำงานกับโปรแกรมอ่าน PDF ทุกตัว

### กรณีขอบ: ไม่มีรายการ `ExtGState`

หาก `page.Resources` ไม่มีดิกชันนารี `ExtGState` `dictEditor["ExtGState"]` จะคืนค่า `null` ในสถานการณ์นั้นคุณสามารถสร้างมันด้วยตนเองได้:

```csharp
if (extGState == null)
{
    extGState = CosPdfDictionary.CreateEmptyDictionary(doc);
    dictEditor["ExtGState"] = extGState;
}
```

การใส่การตรวจสอบนี้ทำให้บทเรียนมีความทนทานต่อ PDF ที่ไม่เคยใช้ graphics state แบบกำหนดเองมาก่อน

## ขั้นตอนที่ 4: เพิ่ม graphics state ใหม่ลงในดิกชันนารีทรัพยากร

ตอนนี้เราจะผูกดิกชันนารีที่สร้างใหม่กับชื่อ (เช่น `GS0`). สตรีมเนื้อหา สามารถอ้างอิงชื่อนี้เพื่อใช้ความโปร่งใสที่กำหนดไว้

```csharp
// Register the new graphics state under the name "GS0"
extGState.Add("GS0", newGs);
```

**ทำไมจึงสำคัญ:** ตัวดำเนินการเนื้อหา PDF เช่น `gs` จะสลับไปยัง graphics state ที่ตั้งชื่อไว้ โดยการเพิ่ม `GS0` คุณทำให้สตรีมเนื้อหาในภายหลังสามารถใช้ ` /GS0 gs ` เพื่อเปิดใช้งานการตั้งค่าความโปร่งใส

## ขั้นตอนที่ 5: (ทางเลือก) ใช้ graphics state กับเนื้อหาที่มีอยู่

หากคุณต้องการให้องค์ประกอบที่มีอยู่ในหน้าปัจจุบันกลายเป็นโปร่งใส คุณสามารถใส่ตัวดำเนินการ `gs` ไว้หน้าสตรีมเนื้อหาของหน้าได้ ขั้นตอนนี้เป็นทางเลือกเพราะหลายกรณีต้องการ graphics state เพียงสำหรับวัตถุที่เพิ่มใหม่

```csharp
// Prepend "GS0" graphics state to the page’s content
page.Contents.Insert(0, new OperatorGraphicsState("GS0"));
```

**ทำไมจึงสำคัญ:** หากไม่มีบรรทัดนี้ หน้า PDF จะคงลักษณะเดิมไว้ การเพิ่มตัวดำเนินการทำให้ทุกอย่างที่วาดหลังจากนั้นสืบทอดค่าความทึบใหม่

## ขั้นตอนที่ 6: บันทึก PDF ที่แก้ไขแล้ว

สุดท้ายให้บันทึกเอกสารที่อัปเดตลงดิสก์ คุณสามารถเขียนทับไฟล์ต้นฉบับหรือบันทึกไปยังตำแหน่งใหม่ได้

```csharp
string outputPath = @"YOUR_DIRECTORY\output.pdf";
doc.Save(outputPath);
```

**ทำไมจึงสำคัญ:** `doc.Save` จะทำการซีเรียลไลซ์ตาราง cross‑reference ที่แก้ไข, ดิกชันนารีทรัพยากร, และสตรีมเนื้อหาใหม่ใด ๆ สร้าง PDF ที่ถูกต้องซึ่งโปรแกรมอ่านใด ๆ ก็สามารถเปิดได้

## ตัวอย่างทำงานเต็มรูปแบบ

เมื่อรวมส่วนต่าง ๆ เข้าด้วยกัน นี่คือโปรแกรมที่ทำงานได้เองซึ่งคุณสามารถคัดลอก, วาง, และรันได้

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Xmp;
using Aspose.Pdf.Text;
using Aspose.Pdf.Generator;
using Aspose.Pdf.Cos;

class AddGraphicsStateExample
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        using (var doc = new Document(inputPath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Access the first page's resource dictionary
            // -----------------------------------------------------------------
            Page page = doc.Pages[1];
            var dictEditor = new DictionaryEditor(page.Resources);
            var extGState = dictEditor["ExtGState"]?.ToCosPdfDictionary();

            // Ensure ExtGState exists
            if (extGState == null)
            {
                extGState = CosPdfDictionary.CreateEmptyDictionary(doc);
                dictEditor["ExtGState"] = extGState;
            }

            // -----------------------------------------------------------------
            // 3️⃣ Create a new graphics state (transparency settings)
            // -----------------------------------------------------------------
            CosPdfDictionary newGs = CosPdfDictionary.CreateEmptyDictionary(doc);
            var entries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // stroke opacity
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),   // fill opacity
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var entry in entries) newGs.Add(entry);

            // -----------------------------------------------------------------
            // 4️⃣ Register the graphics state as "GS0"
            // -----------------------------------------------------------------
            extGState.Add("GS0", newGs);

            // -----------------------------------------------------------------
            // 5️⃣ (Optional) Apply the graphics state to existing content
            // -----------------------------------------------------------------
            page.Contents.Insert(0, new OperatorGraphicsState("GS0"));

            // -----------------------------------------------------------------
            // 6️⃣ Save the modified PDF
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath);
            Console.WriteLine($"PDF saved with new graphics state at: {outputPath}");
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

หลังจากรันโปรแกรม เปิด `output.pdf` ด้วย Adobe Acrobat Reader หรือโปรแกรมอ่าน PDF ใด ๆ รูปร่างที่เติมสี (เช่น สี่เหลี่ยมสี) บนหน้าที่หนึ่งควรแสดงที่ **ความทึบ 50 %** ในขณะที่เส้นขอบยังคงเต็มทึบ หากคุณเพิ่มตัวดำเนินการ `gs` ทางเลือก *ทั้งหมด* ของเนื้อหาที่มีอยู่บนหน้านั้นจะสืบทอดความโปร่งใสเดียวกัน

## คำถามทั่วไปและการแก้ไขปัญหา

| คำถาม | คำตอบ |
|----------|--------|
| **ฉันสามารถเพิ่ม graphics state มากกว่าหนึ่งรายการได้หรือไม่?** | ได้. สร้างดิกชันนารีเพิ่มเติม (เช่น `GS1`, `GS2`) แล้วอ้างอิงด้วยตัวดำเนินการ `gs` ที่แตกต่างกัน |
| **ถ้า PDF มีชื่อเช่น `GS0` อยู่แล้วจะทำอย่างไร?** | เลือกชื่อที่ไม่ซ้ำกัน (เช่น `MyGS`) หรือเช็คคีย์ที่มีอยู่ด้วย `extGState.Keys` |
| **วิธีนี้ทำงานกับ PDF ที่เข้ารหัสหรือไม่?** | ต้องเปิดเอกสารด้วยรหัสผ่านที่ถูกต้อง ใช้ `new Document(inputPath, new LoadOptions { Password = "pwd" })`. |
| **การเปลี่ยนแปลงนี้จะส่งผลต่อหน้าต่าง ๆ หรือไม่?** | ไม่. graphics state จะถูกเพิ่มไปยังทรัพยากรของหน้าที่คุณแก้ไข หากต้องการส่งผลต่อทุกหน้า ให้ทำซ้ำขั้นตอนสำหรับแต่ละหน้า หรือเพิ่มดิกชันนารีไปยังทรัพยากรระดับ *document* |
| **มีผลต่อประสิทธิภาพหรือไม่?** | การเพิ่ม graphics state เพียงหนึ่งรายการไม่มีผลต่อประสิทธิภาพอย่างมีนัยสำคัญ PDF ขนาดใหญ่ที่มีหลายหน้าอาจต้องใช้ลูป แต่การดำเนินการยังคงเป็น O(number of pages). |

## เคล็ดลับระดับมืออาชีพ

* **Reuse graphics states:** หากต้องการความโปร่งใสเดียวกันบนหลายหน้า ให้เพิ่มดิกชันนารีไปยังทรัพยากรระดับ *document* (`doc.Resources`) แล้วอ้างอิงจากแต่ละหน้า วิธีนี้ช่วยลดขนาดไฟล์
* **Blend modes:** ทดลองค่า `BM` อื่น ๆ เช่น `Multiply`, `Screen`, หรือ `Overlay` เพื่อสร้างเอฟเฟกต์ที่สร้างสรรค์ ไม่ใช่ทุกโปรแกรมอ่านจะสนับสนุนทุกโหมดผสม ดังนั้นควรทดสอบกับผู้ใช้เป้าหมายของคุณ
* **Testing:** ควรเปรียบเทียบ PDF ต้นฉบับและที่แก้ไขข้างกันเสมอ ใช้เครื่องมือเปรียบเทียบที่สามารถแสดงผล PDF (เช่น `DiffPDF`) เพื่อตรวจสอบว่ามีการเปลี่ยนแปลงตามที่ตั้งใจเท่านั้น

## ขั้นตอนต่อไป

เมื่อคุณรู้แล้วว่า **วิธีเพิ่ม transparency pdf** และ **แก้ไขความโปร่งใสของ pdf** คุณสามารถสำรวจหัวข้อที่เกี่ยวข้องต่อไปนี้:

* **Add graphics state pdf** สำหรับเอฟเฟกต์ overprint และ halftone
* **Embedding images with custom opacity** ด้วย `ImageFragment` และ graphics state
* **Batch processing** หลายไฟล์ PDF ในโฟลเดอร์พร้อมการประมวลผลแบบขนานเพื่อเพิ่มประสิทธิภาพ
* **Using Aspose.PDF’s high‑level API** (`PdfSaveOptions`, `PdfPageEditor`) สำหรับเวิร์กโฟลว์ที่ซับซ้อนมากขึ้น

อย่าลังเลที่จะทดลองค่าตัวแปร alpha ต่าง ๆ

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดที่ทำงานได้เต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโครงการของคุณ

- [เพิ่มความโปร่งใสให้ PDF ด้วย Aspose – คู่มือ C# ฉบับสมบูรณ์](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [วิธีเพิ่มตราข้อความลงใน PDF ด้วย Aspose.PDF .NET&#58; คู่มือครบวงจร](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)
- [วิธีเพิ่มรูปภาพลงใน PDF ด้วย Aspose.PDF for .NET&#58; คู่มือทีละขั้นตอน](/pdf/english/net/images-graphics/add-images-to-pdfs-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}