---
category: general
date: 2026-01-15
description: เพิ่มหมายเลขบาเตสใน PDF ของคุณอย่างรวดเร็วด้วย Aspose.Pdf. เรียนรู้วิธีเพิ่มส่วนท้ายใน
  PDF, เพิ่มหมายเลขหน้าใน PDF, และเพิ่มการจัดหมายเลขหน้าที่กำหนดเอง.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: th
og_description: เพิ่มหมายเลขบาเตสให้ไฟล์ PDF ของคุณอย่างรวดเร็วด้วย Aspose.Pdf. เรียนรู้วิธีเพิ่มส่วนท้ายใน
  PDF, เพิ่มหมายเลขหน้าใน PDF, และเพิ่มการนับหน้าที่กำหนดเอง.
og_title: เพิ่มหมายเลข Bates ไปยัง PDF – การใส่หมายเลข Bates ใน PDF
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: เพิ่มหมายเลข Bates ลงใน PDF – การตั้งหมายเลข Bates PDF
url: /th/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มหมายเลข Bates ลงใน PDF – คู่มือฉบับสมบูรณ์

เคยต้องการ **add bates numbers** ลงใน PDF แต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว—ทีมกฎหมาย, ผู้ตรวจสอบ, และผู้ที่ต้องจัดการกับชุดเอกสารขนาดใหญ่ต่างเผชิญกับปัญหานี้ทุกวัน ข่าวดีคืออะไร? ด้วย Aspose.Pdf for .NET คุณสามารถใส่หมายเลขเหล่านั้นลงบนทุกหน้าได้ด้วยเพียงไม่กี่บรรทัดโค้ด.

ในบทแนะนำนี้ เราจะพาคุณผ่านขั้นตอนทั้งหมด: ตั้งแต่การนำเข้าไลบรารี Aspose.Pdf, การโหลดไฟล์ต้นฉบับของคุณ, การกำหนดค่า *BatesNumberingArtifact*, การแนบเป็นส่วนท้าย (footer), และสุดท้ายการบันทึกผลลัพธ์. เมื่อจบคุณจะรู้วิธี **add footer to pdf**, **add page numbers pdf**, และแม้กระทั่ง **add custom page numbering** สำหรับกรณีขอบที่ซับซ้อน.

## สิ่งที่คุณต้องการ

- .NET 6+ (หรือ .NET Framework 4.8 หากคุณยังใช้สแตกคลาสสิก)  
- อ้างอิงไปยังแพ็กเกจ NuGet **Aspose.Pdf** (`Install-Package Aspose.Pdf`)  
- ไฟล์ PDF ที่คุณต้องการใส่ตรา (เราจะเรียกว่า `source.pdf`)  

เท่านั้นแหละ—ไม่ต้องใช้เครื่องมือเพิ่มเติม, ไม่ต้องใช้โปรแกรมแก้ไข PDF ขนาดใหญ่. มาเริ่มกันเลย.

![ตัวอย่างการเพิ่มหมายเลข Bates](https://example.com/images/add-bates-numbers.png "ตัวอย่างการเพิ่มหมายเลข Bates")

## ขั้นตอนที่ 1: เพิ่มหมายเลข Bates – โหลดเอกสาร PDF

ก่อนอื่น เราต้องการอ็อบเจ็กต์ `Document` ที่เป็นตัวแทนของ PDF ที่กำลังจะทำการแก้ไข. คิดว่าเป็นการเปิดเอกสาร Word ก่อนที่คุณจะเริ่มพิมพ์.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **ทำไมเรื่องนี้สำคัญ:** การโหลดไฟล์ทำให้คุณเข้าถึงคอลเลกชัน `Pages` ของมัน, ซึ่งเป็นที่ที่เราจะแนบ Bates numbering artifact ในภายหลัง. หากไม่พบไฟล์, Aspose จะโยน `FileNotFoundException` ที่ชัดเจน, ดังนั้นตรวจสอบเส้นทางอีกครั้ง.

## ขั้นตอนที่ 2: กำหนดค่า Settings ของ bates numbering pdf

ตอนนี้เรากำหนด *วิธี* ที่หมายเลขควรแสดง. `BatesNumberingArtifact` ให้คุณตั้งค่า prefix, start number, digit padding, suffix, และ placement. นี่คือหัวใจของ **bates numbering pdf**.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **เคล็ดลับมือโปร:** หากคุณต้องการให้หมายเลขปรากฏในส่วนหัวแทน, ให้เปลี่ยน `BottomCenter` เป็น `TopCenter`. enum ของ placement ยังรองรับ `BottomLeft`, `BottomRight` เป็นต้น, ให้ความยืดหยุ่นสำหรับสไตล์ **add footer to pdf** ที่แตกต่างกัน.

## ขั้นตอนที่ 3: เพิ่ม page numbers pdf – แนบ Artifact ไปยังทุกหน้า

เมื่อ artifact พร้อม, เราจะวนลูปผ่านแต่ละหน้าและเพิ่มลงในคอลเลกชัน `Artifacts`. นี่คือขั้นตอนที่จริงๆ แล้ว **adds page numbers pdf**.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **อะไรกำลังเกิดขึ้นเบื้องหลัง?** คอลเลกชัน `Artifacts` จะถูกเรนเดอร์หลังจากเนื้อหาหลักของหน้า, ทำให้หมายเลข Bates อยู่บนข้อความที่มีอยู่แล้วแต่ใต้ annotation. หากคุณต้องการให้หมายเลขอยู่ด้านหลังเนื้อหา (หายาก), คุณจะใช้ `page.Artifacts.Insert(0, batesArtifact)`.

## ขั้นตอนที่ 4: เพิ่ม custom page numbering – บันทึก PDF ที่อัปเดต

สุดท้าย, เราจะเขียนเอกสารที่แก้ไขแล้วออกไปยังดิสก์. ไฟล์ผลลัพธ์จะมีหมายเลข Bates เป็นส่วนถาวรของแต่ละหน้า.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **เคล็ดลับการตรวจสอบ:** เปิด `bates_out.pdf` ด้วยโปรแกรมดูใดก็ได้. คุณควรเห็นข้อความเช่น `CASE-01000-A` อยู่กึ่งกลางด้านล่างของทุกหน้า. หากไม่มีหมายเลข, ตรวจสอบอีกครั้งว่า property `Placement` ตรงกับตำแหน่งที่คุณต้องการหรือไม่.

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน, นี่คือโปรแกรมที่สมบูรณ์และพร้อมรัน:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

- **File:** `bates_out.pdf` ในโฟลเดอร์เดียวกับ `source.pdf`  
- **Visual:** ข้อความกึ่งกลางด้านล่าง `CASE-01000-A`, `CASE-01001-A`, … สำหรับแต่ละหน้าถัดไป  
- **Behaviour:** หมายเลขถูกฝังอย่างถาวร; พวกมันยังคงอยู่หลังการพิมพ์, การแบน, และการแก้ไขต่อไป  

## ความแตกต่างทั่วไป & กรณีขอบ

| สถานการณ์ | วิธีปรับ |
|-----------|----------|
| **หมายเลขเริ่มต้นที่แตกต่าง** | เปลี่ยน `StartNumber` เป็นจำนวนเต็มใดก็ได้ (เช่น `StartNumber = 500`). |
| **ส่วนต่อท้ายเป็นตัวอักษรต่อโวลุ่ม** | ใช้ลูปเพื่อแก้ไข `Suffix` ต่อหน้า, หรือสร้างหลาย artifact ที่มีส่วนต่อท้ายต่างกัน. |
| **การจัดหมายเลขทางขวา** | ตั้งค่า `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **เอกสารขนาดใหญ่ (10k+ หน้า)** | พิจารณาแบ่งเป็นชุดหน้า หรือเพิ่มค่า `NumberDigits` เพื่อหลีกเลี่ยง overflow. |
| **ต้องการซ่อนหมายเลขในบางหน้า** | ข้ามหน้าดังกล่าวในลูป `foreach` (เช่น `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **ระวัง:** การใช้ `Prefix` หรือ `Suffix` ที่มีอักขระที่ไม่อนุญาตในชื่อไฟล์ (เช่น `*` หรือ `?`). Aspose จะยังฝังไว้, แต่อาจทำให้เกิดปัญหาเมื่อคุณดึงข้อความออกในภายหลัง.

## เคล็ดลับระดับมืออาชีพสำหรับการใช้งานใน Production

- **Cache the artifact** หากคุณกำลังประมวลผล PDF จำนวนมากต่อเนื่อง; การสร้างครั้งเดียวจะประหยัดหลายมิลลิวินาทีต่อไฟล์.  
- **Thread‑safety:** อินสแตนซ์ `BatesNumberingArtifact` ไม่ปลอดภัยต่อหลายเธรด, ดังนั้นให้แต่ละเธรดมีสำเนาของมันเอง.  
- **Performance:** สำหรับชุดงานขนาดใหญ่, ปิดการบีบอัด PDF (`pdfDocument.Compress = false`) ก่อนบันทึก, แล้วเปิดใหม่หากต้องการ.  
- **Testing:** ควรตรวจสอบภาพอย่างรวดเร็วบน PDF แรกที่สร้างขึ้นเพื่อให้แน่ใจว่าตำแหน่งตรงตามมาตรฐานของทีมกฎหมาย.  

## สรุป

ตอนนี้คุณมีสูตรครบวงจรสำหรับการ **add bates numbers** ใบ PDF ใดๆ ด้วย Aspose.Pdf, พร้อมตัวเลือกในการ **add footer to pdf**, **add page numbers pdf**, และ **add custom page numbering**. โค้ดเป็นอิสระเต็มรูปแบบ, ทำงานกับ .NET 6 และรุ่นต่อไป, และสามารถนำไปใช้ใน pipeline automation ที่มีอยู่ได้.

ต่อไปทำอะไร? ลองสลับการวาง `BottomCenter` เป็นสไตล์ส่วนหัว, ทดลองใช้ prefix แบบไดนามิก (เช่น ID ของคดีจากฐานข้อมูล), หรือรวมกับฟีเจอร์การดึงข้อความของ Aspose เพื่อสร้างดัชนีที่ค้นหาได้ของเอกสารที่เพิ่งเพิ่มหมายเลข. ไม่มีขีดจำกัด, และคุณเพิ่งได้เครื่องมือที่ทรงพลังสำหรับการควบคุมเอกสาร.

ขอให้เขียนโค้ดอย่างสนุกสนาน, และขอให้ PDF ของคุณมีหมายเลขที่สมบูรณ์แบบเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}