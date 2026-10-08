---
category: general
date: 2026-03-01
description: วิธีทำลบข้อมูลใน PDF อย่างรวดเร็วด้วย Aspose.Pdf ใน C# เรียนรู้การซ่อนข้อความใน
  PDF, การลบเนื้อหาใน PDF, และการทำลบพื้นที่ใน PDF พร้อมตัวอย่างที่สมบูรณ์และสามารถรันได้
draft: false
keywords:
- how to redact pdf
- hide text pdf
- remove content pdf
- create pdf document c#
- redact area in pdf
language: th
og_description: วิธีทำการลบข้อมูลใน PDF ด้วย C# โดยใช้ Aspose.Pdf คู่มือนี้จะแสดงวิธีซ่อนข้อความใน
  PDF, ลบเนื้อหาใน PDF, และทำการลบข้อมูลในพื้นที่ของ PDF พร้อมโค้ดต้นฉบับเต็ม
og_title: วิธีทำการลบข้อมูลใน PDF ด้วย C# – ซ่อนข้อความใน PDF และลบเนื้อหา PDF
tags:
- Aspose.Pdf
- C#
- PDF Redaction
title: วิธีทำ Redact PDF ด้วย C# – ซ่อนข้อความ PDF และลบเนื้อหา PDF
url: /th/net/document-manipulation/how-to-redact-pdf-in-c-hide-text-pdf-remove-content-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำลบข้อมูล PDF ใน C# – ซ่อนข้อความ PDF & ลบเนื้อหา PDF

เคยสงสัย **how to redact pdf** ว่าไม่มีการใช้เวลาหลายชั่วโมงกับเครื่องมือของบุคคลที่สามหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการที่ต้องปฏิบัติตามข้อกำหนดอย่างเข้มงวด คุณต้องซ่อนข้อความ pdf, กำจัดข้อมูลที่เป็นความลับ, และยังคงรักษาเอกสารส่วนที่เหลือไว้ครบถ้วน.  

ข่าวดีคืออะไร? ด้วย Aspose.Pdf for .NET คุณสามารถทำทั้งหมดนี้ได้ในไม่กี่บรรทัด ในบทแนะนำนี้เราจะเดินผ่านการสร้างเอกสาร PDF ด้วย C#, กำหนดพื้นที่ทำลบข้อมูล, และสุดท้ายบันทึกสำเนาที่สะอาด หลังจากนี้คุณจะรู้วิธี remove content pdf, hide text pdf, และ redact area in pdf อย่างแม่นยำ—ทั้งหมดจากโค้ดที่คุณสามารถใส่ลงในโครงการ .NET ใดก็ได้.

## ข้อกำหนดเบื้องต้น & สิ่งที่คุณจะสร้าง

- **.NET 6+** (หรือ .NET Framework 4.6+ – API เหมือนเดิม)
- **Aspose.Pdf for .NET** NuGet package (`Aspose.Pdf`)
- ความเข้าใจพื้นฐานของไวยากรณ์ C# (ไม่ต้องการความซับซ้อน)

เราจะสร้างไฟล์ชื่อ `redacted.pdf` ที่มีสี่เหลี่ยมสีแดงครอบคลุมพิกัด (100, 100)‑(300, 200) ทุกอย่างที่อยู่ใต้สี่เหลี่ยมนั้นจะถูกลบอย่างถาวร ซึ่งเป็นสิ่งที่คุณต้องการเมื่อถูกขอให้ **hide text pdf** สำหรับ GDPR หรือเหตุผลทางกฎหมาย.

> **Pro tip:** หากคุณต้องการทำลบข้อมูลหลายพื้นที่ที่ไม่ต่อเนื่อง เพียงเพิ่มวัตถุ `RedactionAnnotation` เพิ่มเติมในหน้าเดียว – ไลบรารีจะจัดการทั้งหมดในหนึ่งรอบ.

## วิธีทำลบข้อมูล PDF – ขั้นตอนทีละขั้น

ด้านล่างแต่ละขั้นตอนคุณจะเห็นโค้ดสั้น ๆ คำอธิบายว่า *ทำไม* บรรทัดนั้นสำคัญ และเคล็ดลับเร็ว ๆ เพื่อหลีกเลี่ยงข้อผิดพลาดทั่วไป.

### 1. ตั้งค่าโครงการและเพิ่ม Aspose.Pdf

ขั้นแรก สร้างแอปคอนโซลใหม่ (หรือรวมเข้ากับบริการที่มีอยู่) และติดตั้งแพ็กเกจ NuGet:

```bash
dotnet new console -n PdfRedactionDemo
cd PdfRedactionDemo
dotnet add package Aspose.Pdf
```

> **ทำไม?** การติดตั้งแพ็กเกจจะดึงเอา assembly `Aspose.Pdf` ซึ่งประกอบด้วย `Document`, `RedactionAnnotation` และวัตถุ PDF ระดับต่ำทั้งหมดที่คุณต้องการ หากไม่มีคุณจะไม่สามารถ **remove content pdf** ได้โดยโปรแกรม.

### 2. สร้างเอกสาร PDF ในหน่วยความจำ

เราเริ่มด้วย PDF ว่างเปล่า – คิดว่าเป็นแผ่นกระดาษใหม่ที่คุณสามารถเขียนได้.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Redactions;

class Program
{
    static void Main()
    {
        // Step 2: Create a new PDF document in memory
        using var pdfDocument = new Document();

        // (Optional) Add a page with some sample text so you can see the redaction effect
        var page = pdfDocument.Pages.Add();
        page.Paragraphs.Add(new TextFragment("Sensitive data: 123‑45‑6789"));
```

**ทำไมเรื่องนี้สำคัญ:**  
- `using var` ทำให้แน่ใจว่าเอกสารถูกทำลายอย่างถูกต้อง ปล่อยทรัพยากรเนทีฟ  
- การเพิ่มหน้าที่มีข้อความมองเห็นได้ช่วยให้คุณตรวจสอบว่าการทำลบข้อมูลจริง ๆ *ลบ* เนื้อหา ไม่ใช่แค่ปกปิด

### 3. กำหนด Redaction Annotation (พื้นที่ “hide text pdf”)

ที่นี่เรากำหนดสี่เหลี่ยมที่จะถูกลบออกจากหน้า.

```csharp
        // Step 3: Define a redaction annotation covering the desired area
        var redactionRect = new Rectangle(100, 100, 300, 200);
        var redactionAnnotation = new RedactionAnnotation(redactionRect)
        {
            // Optional: set the fill color to a solid black for visual feedback
            FillColor = Color.Black,
            // Optional: set overlay text that will appear after redaction
            OverlayText = "REDACTED"
        };

        // Attach the annotation to the first page (index 1)
        pdfDocument.Pages[1].Annotations.Add(redactionAnnotation);
```

**ทำไม?** `RedactionAnnotation` บอก Aspose *ตำแหน่ง* ที่จะลบข้อมูล สี่เหลี่ยมใช้ระบบพิกัด PDF (จุดกำเนิดที่มุมล่างซ้าย) หากคุณคุ้นเคยกับพิกัด Windows GDI จำไว้ว่าแกน Y จะกลับด้าน

> **ข้อผิดพลาดทั่วไป:** ลืมเพิ่ม annotation ไปที่ `Pages[1].Annotations` Annotation จะมีอยู่ แต่ไม่มีการทำลบข้อมูลใด ๆ

### 4. เตรียม Resources (เช่น XObjects) – การใช้ขั้นสูง

หากคุณต้องการฝังรูปภาพหรือกราฟิกแบบกำหนดเองลงในพื้นที่ทำลบข้อมูล คุณสามารถโหลดล่วงหน้าเข้าไปในพจนานุกรม resources ของ annotation.

```csharp
        // Step 4: Access the annotation's resources dictionary (optional)
        var resources = redactionAnnotation.Resources;
        // Example: add an XObject later – omitted here for brevity
```

**ทำไมต้องรวมขั้นตอนนี้?** แม้คุณต้องการเพียงกล่องสีดำง่าย ๆ การเปิดเผยพจนานุกรม resources จะสื่อให้เอนจินรู้ว่าคุณ *อาจ* เพิ่มเนื้อหาเพิ่มเติมในภายหลัง เป็นการเรียกที่ไม่มีผลเสียและทำให้โค้ดยืดหยุ่นสำหรับการพัฒนาในอนาคต

### 5. ใช้การทำลบข้อมูลและบันทึก PDF

การเรียก `Redact()` จะลบเนื้อหาออกจริง ๆ จากนั้นเราบันทึกไฟล์.

```csharp
        // Step 5: Apply the redaction and save the PDF
        pdfDocument.Redact();   // This processes all redaction annotations
        pdfDocument.Save("redacted.pdf");

        Console.WriteLine("Redacted PDF saved as redacted.pdf");
    }
}
```

**ทำไมต้องเรียก `Redact()`?** การเพิ่ม annotation เพียงอย่างเดียวไม่ทำให้สตรีมพื้นฐานเปลี่ยนแปลง `Redact()` จะวนผ่านแต่ละ annotation, ลบวัตถุที่อยู่ภายในสี่เหลี่ยม, และอาจเพิ่มข้อความ overlay หากข้ามขั้นตอนนี้ข้อมูลต้นฉบับจะคงอยู่—ทำให้วัตถุประสงค์ของ **how to redact pdf** ไม่สำเร็จ

## ตัวอย่างทำงานเต็มรูปแบบ

คัดลอกและวางรายการทั้งหมดลงใน `Program.cs` แล้วรัน `dotnet run` คุณจะเห็น `redacted.pdf` ปรากฏในโฟลเดอร์โครงการ โดยสตริงที่เป็นข้อมูลสำคัญจะถูกแทนที่ด้วยกล่องสีดำที่มีป้าย “REDACTED”.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Redactions;
using Aspose.Pdf.Text;   // For TextFragment
using Aspose.Pdf.Drawing; // For Color

class Program
{
    static void Main()
    {
        // Create a new PDF document in memory
        using var pdfDocument = new Document();

        // Add a page with sample text (so we can see the effect)
        var page = pdfDocument.Pages.Add();
        page.Paragraphs.Add(new TextFragment("Sensitive data: 123‑45‑6789"));

        // Define a redaction annotation covering the desired area
        var redactionRect = new Rectangle(100, 100, 300, 200);
        var redactionAnnotation = new RedactionAnnotation(redactionRect)
        {
            FillColor = Color.Black,
            OverlayText = "REDACTED"
        };
        pdfDocument.Pages[1].Annotations.Add(redactionAnnotation);

        // (Optional) Access resources dictionary – useful for XObjects
        var resources = redactionAnnotation.Resources;

        // Apply redaction and save the PDF
        pdfDocument.Redact();
        pdfDocument.Save("redacted.pdf");

        Console.WriteLine("Redacted PDF saved as redacted.pdf");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** การเปิด `redacted.pdf` จะเห็นหน้าเดียวที่ข้อความ “Sensitive data: 123‑45‑6789” หายไปอย่างสมบูรณ์ ถูกแทนที่ด้วยสี่เหลี่ยมสีดำทึบที่มีคำว่า “REDACTED” อยู่ตรงกลาง ไม่มีสตรีมที่ซ่อนอยู่เหลืออยู่ ทำให้ผ่านการตรวจสอบการปฏิบัติตามข้อกำหนด

## คำถามที่พบบ่อย & กรณีขอบ

| Question | Answer |
|----------|--------|
| **ฉันสามารถทำลบข้อมูลหลายหน้าในครั้งเดียวได้หรือไม่?** | ได้ – เพียงวนลูปผ่าน `pdfDocument.Pages` แล้วเพิ่ม `RedactionAnnotation` ไปยังคอลเลกชัน `Annotations` ของแต่ละหน้า. |
| **ถ้าพื้นที่ทำลบข้อมูลทับกับรูปภาพที่มีอยู่จะเป็นอย่างไร?** | เอนจินทำลบข้อมูลจะลบ *ทั้งหมด* ของวัตถุที่ตัดกันกับสี่เหลี่ยม รวมถึงรูปภาพ, เวกเตอร์, และข้อความ. |
| **ฉันต้องเรียก `Redact()` หลังจากแต่ละ annotation ใหม่หรือไม่?** | ไม่. เรียกครั้งเดียวหลังจากที่คุณได้เพิ่ม *ทั้งหมด* annotation ที่ต้องการใช้. |
| **ฉันจะทำให้ PDF ต้นฉบับไม่เปลี่ยนแปลงได้อย่างไร?** | โหลดไฟล์ต้นฉบับเข้า `Document`, ทำสำเนา (`var clone = (Document)source.Clone();`), ใช้การทำลบข้อมูลกับสำเนา, แล้วบันทึกสำเนา. |
| **การทำลบข้อมูลสามารถย้อนกลับได้หรือไม่?** | ไม่. เมื่อ `Redact()` ทำงานแล้ว เนื้อหาเดิมจะถูกลบออกจากสตรีม PDF เก็บสำเนาสำรองไว้หากคุณอาจต้องการเวอร์ชันที่ไม่ได้ทำลบข้อมูลในภายหลัง. |

## หัวข้อที่เกี่ยวข้องที่คุณอาจสนใจต่อไป

- **Hide text pdf** โดยใช้เลเยอร์ PDF (`OptionalContentGroup`) เพื่อการซ่อนที่ย้อนกลับได้.  
- **Remove content pdf** โดยการลบหน้า หรือวัตถุเฉพาะผ่านโมเดลวัตถุ PDF ระดับต่ำ.  
- **Create PDF document C#** พร้อมตาราง, รูปภาพ, และลายเซ็นดิจิทัล.  
- **Redact area in PDF** ด้วยกราฟิก overlay แบบกำหนดเอง (เช่น โลโก้บริษัท).  

## สรุป

คุณมีคำตอบที่มั่นคงและพร้อมใช้งานในระดับผลิตภัณฑ์สำหรับ **how to redact pdf** ด้วย C# โดยการสร้าง `Document`, เพิ่ม `RedactionAnnotation`, เรียก `Redact()`, และบันทึกไฟล์ คุณสามารถ **hide text pdf**, **remove content pdf**, และ **redact area in pdf** ได้อย่างเชื่อถือโดยไม่ต้องใช้โปรแกรมของบุคคลที่สาม  

ลองใช้กับไฟล์ของคุณเอง ทดลองหลายสี่เหลี่ยม และอาจทำอัตโนมัติขั้นตอนสำหรับการทำลบข้อมูลเป็นชุด หากเจอปัญหาใด ๆ ฝากคอมเมนต์ด้านล่าง – โค้ดดิ้งสนุก!

![ตัวอย่างการทำลบข้อมูล pdf](redaction-example.png){: .align-center alt="ตัวอย่างการทำลบข้อมูล pdf"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}