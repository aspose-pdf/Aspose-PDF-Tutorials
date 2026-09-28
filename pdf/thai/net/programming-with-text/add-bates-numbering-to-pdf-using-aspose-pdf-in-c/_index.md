---
category: general
date: 2026-09-27
description: เพิ่มการใส่หมายเลขบาเตสลงใน PDF ด้วย Aspose.PDF ใน C#. เรียนรู้วิธีโหลดเอกสาร
  PDF, ตั้งค่าตัวเลือกการใส่หมายเลขบาเตส, และบันทึกไฟล์ที่อัปเดต.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: th
lastmod: 2026-09-27
og_description: เพิ่มการใส่หมายเลขบาเตสลงใน PDF ด้วย Aspose.PDF ใน C#. บทเรียนนี้จะแสดงวิธีโหลดเอกสาร
  PDF, กำหนดค่าการใส่หมายเลขบาเตส, และบันทึกผลลัพธ์.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: เพิ่มการใส่หมายเลขบาเตสใน PDF ด้วย Aspose.PDF – คู่มือ C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: เพิ่มการใส่หมายเลขบาเตสลงใน PDF ด้วย Aspose.PDF ใน C#
url: /th/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มหมายเลขบาเตสลงใน PDF ด้วย Aspose.PDF ใน C#

หากคุณต้องการ **เพิ่มหมายเลขบาเตส** ลงในไฟล์ PDF คำแนะนำนี้จะแสดงวิธีแก้ไขที่สมบูรณ์และพร้อมใช้งาน คุณจะได้เห็นวิธี **โหลดเอกสาร PDF**, ตั้งค่าตัวเลือกการใส่หมายเลขบาเตส, และบันทึกไฟล์ที่มีหมายเลขกลับไปยังดิสก์—ทั้งหมดด้วย Aspose.PDF สำหรับ .NET

การใส่หมายเลขบาเตสเป็นเรื่องทั่วไปในกระบวนการทำงานด้านกฎหมาย, การบังคับใช้กฎหมาย, และการจัดเก็บเอกสาร. เมื่อจบบทเรียนนี้คุณจะสามารถฝังตัวระบุแบบต่อเนื่องบนทุกหน้า, ปรับแต่งคำนำหน้า, และเริ่มนับจากหมายเลขใดก็ได้ที่คุณต้องการ

## สิ่งที่คุณจะได้เรียนรู้

* วิธี **โหลดเอกสาร PDF** เข้าไปในอ็อบเจ็กต์ `Aspose.Pdf.Document`.
* ขั้นตอนที่แน่นอน **วิธีเพิ่มหมายเลขบาเตส** ด้วย `BatesNumberingOptions`.
* วิธีบันทึกไฟล์ที่แก้ไขแล้วโดยคงรูปแบบและคุณภาพเดิม.

ไม่ต้องใช้เครื่องมือภายนอก—เพียงแพ็กเกจ Aspose.PDF NuGet และสภาพแวดล้อมการพัฒนา .NET (Visual Studio, VS Code, หรือ Rider).

---

## ขั้นตอนที่ 1: ติดตั้ง Aspose.PDF สำหรับ .NET

เปิดโฟลเดอร์โปรเจกต์ของคุณในเทอร์มินัลและรัน:

```bash
dotnet add package Aspose.PDF
```

แพ็กเกจนี้รวมเนมสเปซ `Aspose.Pdf` ซึ่งให้คลาสทั้งหมดที่ใช้ในบทเรียนนี้ หลังการติดตั้ง ให้รีโหลดโปรเจกต์เพื่อให้ IDE ตรวจจับการอ้างอิงใหม่.

## ขั้นตอนที่ 2: โหลดเอกสาร PDF

การโหลดไฟล์ต้นฉบับเป็นขั้นตอนแรก เนื่องจากเครื่องมือใส่หมายเลขบาเตสทำงานบนอินสแตนซ์ `Document` ที่มีอยู่.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**ทำไมเรื่องนี้สำคัญ:** คลาส `Document` จะวิเคราะห์โครงสร้าง PDF ให้คุณเข้าถึงหน้า, คำอธิบายประกอบ, และเมตาดาต้า หากไม่ได้โหลดไฟล์ก่อน คุณจะไม่สามารถใส่หมายเลขใด ๆ ได้.

## ขั้นตอนที่ 3: ตั้งค่าตัวเลือกการใส่หมายเลขบาเตส

สร้างอ็อบเจ็กต์ `BatesNumberingOptions` และตั้งค่าคำนำหน้าที่ต้องการ, หมายเลขเริ่มต้น, และพารามิเตอร์การจัดรูปแบบเพิ่มเติม (ถ้ามี).

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**ทำไมเรื่องนี้สำคัญ:** `BatesNumberingOptions` บอก Aspose.PDF ว่าจะสร้างป้ายกำกับสำหรับแต่ละหน้าอย่างไร `Prefix` ช่วยให้คุณจัดกลุ่มคดีที่เกี่ยวข้อง, ส่วน `StartNumber` ทำให้คุณต่อเนื่องลำดับจากชุดก่อนหน้า.

## ขั้นตอนที่ 4: บันทึก PDF พร้อมหมายเลขบาเตสที่ใส่แล้ว

ส่งอ็อบเจ็กต์ตัวเลือกไปยังเมธอด `Save`. Aspose.PDF จะเขียนหมายเลขลงบนแต่ละหน้าโดยตรง.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**ทำไมเรื่องนี้สำคัญ:** การโอเวอร์โหลด `Save(string, BatesNumberingOptions)` จะรวมขั้นตอนการเรนเดอร์กับกระบวนการใส่หมายเลข, ทำให้ไฟล์ผลลัพธ์มีตัวระบุที่มองเห็นได้.

## ตัวอย่างเต็ม – รวมทุกอย่างไว้ด้วยกัน

ด้านล่างเป็นโปรแกรมเดียวที่ทำงานอิสระซึ่งคุณสามารถคัดลอก, วาง, และรันได้ มันแสดง **วิธีเพิ่มหมายเลขบาเตส** ตั้งแต่ต้นจนจบ.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมจะสร้างไฟล์ `output.pdf` ที่แต่ละหน้าจะแสดงป้ายกำกับคล้ายกับ:

```
CASE01-1
CASE01-2
CASE01-3
...
```

โดยปกติหมายเลขจะปรากฏที่ส่วนท้ายของหน้า, แต่คุณสามารถย้ายตำแหน่งได้โดยปรับคุณสมบัติ `Margin` ใน `BatesNumberingOptions`.

## กรณีขอบและการปรับเปลี่ยนทั่วไป

| Situation | What to adjust |
|-----------|----------------|
| **คำนำหน้าต่างกันต่อแต่ละชุด** | เปลี่ยน `Prefix` ก่อนเรียก `Save`. คุณสามารถวนลูปหลายเอกสารที่มีคำนำหน้าแตกต่างกัน. |
| **ต่อหมายเลขจากไฟล์ก่อนหน้า** | ตั้งค่า `StartNumber` เป็นหมายเลขที่ใช้ล่าสุด + 1. |
| **วางหมายเลขในส่วนหัว** | ใช้ `batesOptions.Margin = new Margin(20, 0, 0, 0);` (margin ด้านบน) หรือปรับแต่ง `batesOptions.Position`. |
| **ฟอนต์หรือสีที่กำหนดเอง** | กำหนดคุณสมบัติ `Font`, `FontSize`, และ `Color` ตามที่แสดงในส่วนคอมเมนต์. |
| **PDF ขนาดใหญ่ (1000+ หน้า)** | การทำงานนี้ใช้หน่วยความจำอย่างมีประสิทธิภาพ; อย่างไรก็ตามคุณอาจต้องเปิดใช้งาน `doc.OptimizeResources()` ก่อนบันทึกเพื่อลดขนาดไฟล์. |

**เคล็ดลับ:** หากกระบวนการทำงานของคุณต้องการรูปแบบการใส่หมายเลขที่แตกต่างกันต่อเอกสาร, ให้ห่อหุ้มตรรกะไว้ในเมธอดช่วยเหลือ:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## สรุป

ตอนนี้คุณรู้ **วิธีเพิ่มหมายเลขบาเตส** ให้กับ PDF ใด ๆ ด้วย Aspose.PDF ใน C# แล้ว บทเรียนนี้ครอบคลุมการโหลดเอกสาร PDF, การตั้งค่าตัวเลือกการใส่หมายเลข, และการบันทึกไฟล์สุดท้าย—ทั้งหมดในโปรแกรมเดียวที่สามารถรันได้.

จากนี้คุณสามารถสำรวจหัวข้อที่เกี่ยวข้องเช่น **การเพิ่มลายน้ำ**, **การรวมหลาย PDF**, หรือ **การสกัดข้อความ** ด้วย Aspose.PDF ทดลองใช้ฟอนต์, สี, และตำแหน่งต่าง ๆ เพื่อให้ตรงกับมาตรฐานการจัดรูปแบบขององค์กรของคุณ.

พร้อมที่จะทำอัตโนมัติขั้นตอนการทำงานของเอกสารทางกฎหมายของคุณหรือยัง? เพิ่มโค้ดนี้เข้าไปใน pipeline การสร้างของคุณ, รันกับชุดไฟล์หลายไฟล์, และให้ Aspose.PDF จัดการงานหนักให้. ขอให้เขียนโค้ดอย่างสนุก!

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดที่ทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโปรเจกต์ของคุณ.

- [สร้างเอกสาร PDF C# – เพิ่มหมายเลขบาเตส](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [เพิ่มหมายเลขบาเตส PDF – คู่มือขั้นตอนต่อขั้นตอนในการใส่หมายเลขหน้า PDF](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [บทเรียน Aspose PDF – แทรกหน้าว่างและอัปเดตหมายเลขบาเตส](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}