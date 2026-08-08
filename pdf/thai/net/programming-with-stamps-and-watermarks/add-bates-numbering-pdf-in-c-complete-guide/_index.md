---
category: general
date: 2026-05-27
description: เพิ่มหมายเลข Bates ให้ไฟล์ PDF ด้วย Aspose.Pdf ใน C#. เรียนรู้วิธีเพิ่มหมายเลข
  Bates อย่างรวดเร็ว ปรับแต่งรูปแบบ และทำให้การแท็กเอกสารทางกฎหมายเป็นอัตโนมัติ
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: th
og_description: เพิ่มหมายเลข Bates ให้กับ PDF ด้วย Aspose.Pdf ใน C#. คู่มือนี้แสดงวิธีเพิ่มหมายเลข
  Bates, ตั้งค่าคำนำหน้า, และบันทึกผลลัพธ์.
og_title: เพิ่มการใส่หมายเลข Bates ใน PDF ด้วย C# – คู่มือแบบทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: เพิ่มหมายเลขบาเตสใน PDF ด้วย C# – คู่มือเต็ม
url: /th/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่ม Bates Numbering PDF ใน C# – คู่มือฉบับสมบูรณ์

เคยสงสัยไหมว่า **วิธีเพิ่ม Bates numbering** ลงใน PDF โดยไม่ต้องเสียเวลาหลายชั่วโมงกับเครื่องมือแบบแมนนวล? คุณไม่ได้เป็นคนเดียว—ทีมกฎหมาย, ผู้ตรวจสอบ, และผู้เชี่ยวชาญด้าน e‑discovery ต่างก็ต้องการวิธีที่เชื่อถือได้ในการ **เพิ่ม Bates numbering PDF** อย่างอัตโนมัติ  

ในบทแนะนำนี้ เราจะพาคุณผ่านโซลูชันสั้น ๆ แบบครบวงจรโดยใช้ Aspose.Pdf for .NET เพื่อให้คุณสามารถใส่หมายเลข Bates ลงในเอกสารใดก็ได้ด้วยเพียงไม่กี่บรรทัดของโค้ด C#.

## สิ่งที่คุณจะได้เรียนรู้

- วิธีเปิด PDF ที่มีอยู่ด้วย Aspose.Pdf  
- วิธีสร้าง BatesNumberingArtifact และปรับแต่งรูปแบบให้ละเอียด  
- วิธีแนบ Artifact ไปยังทุกหน้า (หรือเฉพาะหน้าแรก)  
- วิธีบันทึกไฟล์ที่อัปเดตและตรวจสอบผลลัพธ์  

ไม่จำเป็นต้องมีประสบการณ์กับ Aspose มาก่อน—เพียงความเข้าใจพื้นฐานของ C# และ .NET เท่านั้น เมื่อเสร็จคุณจะมีโค้ดส่วนนำกลับมาใช้ใหม่ที่สามารถคัดลอก‑วางไปยังโปรเจกต์ใดก็ได้

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.7+ ด้วย)  
- แพคเกจ NuGet Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)  
- ไฟล์ PDF ต้นฉบับที่คุณต้องการใส่แท็ก (วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้)

> **เคล็ดลับ:** หากคุณยังไม่มีลิขสิทธิ์ Aspose มีคีย์ชั่วคราวฟรีที่ลบลายน้ำการประเมินผลออก

## ขั้นตอนที่ 1 – เปิดเอกสาร PDF ต้นฉบับ  

ก่อนอื่นเราต้องการอ็อบเจ็กต์ `Document` ที่แทนไฟล์บนดิสก์ คิดว่าเป็นการโหลดผืนผ้าใบเปล่าที่เราจะวาดหมายเลข Bates ลงไปต่อไป

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**ทำไมเรื่องนี้ถึงสำคัญ:** การเปิดเอกสารภายในบล็อก `using` ทำให้ทรัพยากรที่ไม่ได้จัดการถูกปล่อยออกอย่างรวดเร็ว ซึ่งสำคัญอย่างยิ่งสำหรับ PDF ขนาดใหญ่

## ขั้นตอนที่ 2 – สร้าง BatesNumberingArtifact  

*BatesNumberingArtifact* คือวิธีของ Aspose ที่อธิบายว่าตัวเลขควรแสดงอย่างไร คุณสามารถตั้งค่า prefix, starting number, increment, และแม้กระทั่งรูปแบบสตริงที่กำหนดเองได้

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**ทำไมคุณอาจต้องเปลี่ยนค่าต่าง ๆ เหล่านี้:**  
- **Prefix** มีประโยชน์สำหรับรหัสคดี (“CASE‑”, “DOC‑”)  
- **StartNumber** ให้คุณต่อจากชุดหมายเลขก่อนหน้า  
- **Increment** สามารถตั้งเป็น 2 หากต้องการหมายเลขคี่/คู่  
- **Format** รองรับรูปแบบคอมโพสิตของ .NET; `{0:D5}` รับประกันห้าหลักพร้อมศูนย์นำหน้า

## ขั้นตอนที่ 3 – แนบ Artifact ไปยังหน้าที่ต้องการ  

คุณสามารถเพิ่ม artifact ไปยังหน้าเดียว, ช่วงหน้า, หรือทั้งเอกสาร สำหรับกระบวนการทำงานด้านกฎหมายส่วนใหญ่ เราแนบมันไปยัง *ทุก* หน้า แต่ตัวอย่างด้านล่างแสดงกรณีที่น้อยที่สุด—การเพิ่มไปยังหน้าแรก

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

หากคุณต้องการครอบคลุมทุกหน้า ให้วนลูปผ่านหน้าเหล่านั้น:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**ทำไมขั้นตอนนี้ถึงสำคัญ:** Artifacts จะถูกเรนเดอร์ *หลัง* เนื้อหาหน้า ดังนั้นหมายเลขจะแสดงบนข้อความที่มีอยู่โดยไม่เปลี่ยนแปลงเลย์เอาต์เดิม

## ขั้นตอนที่ 4 – บันทึก PDF ที่แก้ไขแล้ว  

สุดท้ายให้เขียนการเปลี่ยนแปลงกลับไปยังดิสก์ คุณสามารถเขียนทับไฟล์ต้นฉบับหรือสร้างไฟล์ใหม่—ที่นี่เราจะสร้างสำเนาใหม่ชื่อ `bates.pdf`

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

เมื่อคุณเปิด `bates.pdf` คุณจะเห็น “ABC01000” (หรือรูปแบบที่คุณเลือก) ปรากฏในตำแหน่งเริ่มต้น—โดยทั่วไปที่มุมล่าง‑ขวา

## ตัวอย่างทำงานเต็มรูปแบบ  

รวมทั้งหมดเข้าด้วยกัน นี่คือโปรแกรมเต็มที่คุณสามารถคอมไพล์และรันได้:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณรันโปรแกรม คอนโซลจะแสดง:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

การเปิด `bates.pdf` จะเห็นคำนำหน้า “ABC” ตามด้วยลำดับห้าหลักที่เติมศูนย์นำหน้าบนทุกหน้า—ตรงกับที่คุณสั่งให้โค้ดทำ

## คำถามทั่วไปและกรณีขอบ

### ฉันสามารถวางหมายเลข Bates ไว้ที่อื่นได้หรือไม่?

ได้ ใช้ property `Location` ของ `BatesNumberingArtifact` (เช่น `Location = new Position(10, 10)`) เพื่อวางหมายเลขที่พิกัด X/Y ที่กำหนดเอง คุณยังสามารถตั้งค่า `HorizontalAlignment` และ `VerticalAlignment` เพื่อควบคุมเพิ่มเติมได้

### ถ้า PDF ของฉันมีหลายพันหน้า จะทำอย่างไร?

Aspose.Pdf สตรีมหน้าต่างอย่างมีประสิทธิภาพ แต่หากเจอข้อจำกัดของหน่วยความจำ การประมวลผลเป็นชุดยังคงเป็นแนวคิดที่ดี คลาส `Document` ยังรองรับ `PdfConverter` สำหรับการบันทึกแบบเพิ่มส่วน

### ฉันจะเปลี่ยนฟอนต์หรือสีได้อย่างไร?

Wrap the artifact in a `TextState` object:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### ฉันต้องมีลิขสิทธิ์สำหรับการใช้งานในผลิตภัณฑ์หรือไม่?

เวอร์ชันที่มีลิขสิทธิ์จะลบลายน้ำการประเมินและเปิดประสิทธิภาพเต็มที่ รุ่นทดลองฟรีก็ใช้ได้ดีสำหรับการทดสอบและพิสูจน์แนวคิด

## การตรวจสอบ – ตรวจสอบภาพอย่างรวดเร็ว  

หากคุณต้องการการตรวจสอบอัตโนมัติ Aspose สามารถดึงข้อความของหน้าและยืนยันการมีอยู่ของคำนำหน้า:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

การรันโค้ดนี้หลังจากขั้นตอนบันทึกจะพิมพ์ `Bates number verified.` หากทุกอย่างทำงานได้อย่างราบรื่น

## สรุป  

ตอนนี้คุณรู้แล้วว่า **วิธีเพิ่ม Bates numbering PDF** ด้วย Aspose.Pdf ใน C# ตั้งแต่การเปิดเอกสาร การกำหนดค่า artifact การแนบไปยังหน้า และการบันทึกผลลัพธ์ กระบวนการนี้ตรงไปตรงมาและสามารถสคริปต์ได้เต็มที่  

ขั้นตอนต่อไป? ลองทดลองกับ:

- ค่า `Prefix` ที่แตกต่างกันสำหรับชุดคดีหลายชุด  
- `Location` และ `TextState` ที่กำหนดเองสำหรับการสร้างแบรนด์  
- เพิ่มคำนำหน้าตามหน้าที่เฉพาะ (เช่น “VOL‑1‑”, “VOL‑2‑”) โดยปรับ `StartNumber` ในแต่ละรอบของลูป  

การปรับแต่งเหล่านี้ทำให้คุณสามารถปรับโซลูชันให้เหมาะกับกระบวนการทำงานด้านกฎหมายหรือการจัดเก็บเอกสารได้เกือบทุกประเภท  

มีคำถามเพิ่มเติมเกี่ยวกับ **วิธีเพิ่ม Bates numbering** สำหรับ PDF หลายภาษา หรือไฟล์ที่เข้ารหัสหรือไม่? แสดงความคิดเห็นด้านล่าง แล้วขอให้เขียนโค้ดอย่างสนุกสนาน!

## บทแนะนำที่เกี่ยวข้อง

- [วิธีเพิ่มและปรับแต่งเลขหน้าใน PDF ด้วย Aspose.PDF for .NET | คู่มือการจัดการเอกสาร](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [วิธีเพิ่มหัวเรื่องต่าง ๆ ใน PDF ด้วย Aspose.PDF for .NET: คู่มือขั้นตอนต่อขั้นตอน](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [วิธีเพิ่มข้อความสแตมป์เป็นส่วนท้ายใน PDF ด้วย Aspose.PDF for .NET: คู่มือขั้นตอนต่อขั้นตอน](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}