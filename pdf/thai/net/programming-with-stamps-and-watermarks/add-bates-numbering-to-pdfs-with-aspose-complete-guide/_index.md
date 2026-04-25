---
category: general
date: 2026-04-25
description: เพิ่มการใส่หมายเลขบาเตสให้กับไฟล์ PDF อย่างรวดเร็วด้วย Aspose.Pdf. เรียนรู้วิธีเพิ่มหมายเลขหน้า
  PDF, ปรับขนาดฟอนต์อัตโนมัติ, และเพิ่มลายน้ำข้อความใน C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: th
og_description: เพิ่มการใส่หมายเลขบาเตสในไฟล์ PDF ด้วย Aspose.Pdf คู่มือนี้จะแสดงวิธีการเพิ่มเลขหน้าใน
  PDF ปรับขนาดฟอนต์อัตโนมัติ และเพิ่มลายน้ำข้อความในตัวอย่างเดียวที่สามารถรันได้
og_title: เพิ่มหมายเลข Bates ให้กับ PDF – บทเรียนเต็ม Aspose.C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: เพิ่มหมายเลข Bates ให้กับไฟล์ PDF ด้วย Aspose – คู่มือฉบับสมบูรณ์
url: /th/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มหมายเลข Bates ให้กับ PDF ด้วย Aspose – คู่มือเต็ม

เคยต้องการ **add bates numbering** ให้กับ PDF แต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—ทีมกฎหมาย, ผู้ตรวจสอบ, และนักพัฒนาต่างก็เจอปัญหานี้ทุกวัน ข่าวดีคือ? ด้วย Aspose.Pdf for .NET คุณสามารถใส่สแตมป์หมายเลข Bates, ปรับขนาดฟอนต์อัตโนมัติ, และแม้กระทั่งทำให้สแตมป์เป็นลายน้ำข้อความที่ละเอียดอ่อน—ทั้งหมดในไม่กี่บรรทัดของ C#.

ในบทแนะนำนี้ เราจะพาคุณผ่านขั้นตอนที่แม่นยำเพื่อ **add page numbers pdf**, ปรับฟอนต์ให้ไม่ล้น, และตอบคำถาม “how to add bates” อย่างครบถ้วน เมื่อเสร็จคุณจะมีแอปคอนโซลที่พร้อมรันซึ่งสร้าง PDF ที่มีหมายเลขอย่างมืออาชีพ และคุณจะเห็นวิธีขยายเป็นโซลูชันลายน้ำเต็มรูปแบบ

## ข้อกำหนดเบื้องต้น

* **Aspose.Pdf for .NET** (แพ็กเกจ NuGet ล่าสุด ณ เดือนเมษายน 2026).  
* .NET 6.0 SDK หรือใหม่กว่า – API ทำงานเช่นเดียวกันบน .NET Framework, แต่ .NET 6 ให้ประสิทธิภาพที่ดีที่สุด.  
* ตัวอย่าง PDF ชื่อ `input.pdf` ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้ (เช่น `C:\Docs\`).  

ไม่ต้องกำหนดค่าพิเศษใด ๆ; ไลบรารีเป็นแบบ self‑contained.

---

## ขั้นตอนที่ 1 – โหลดเอกสาร PDF ต้นฉบับ

สิ่งแรกที่เราทำคือเปิดไฟล์ที่ต้องการใส่หมายเลข. คลาส `Document` ของ Aspose แทนเอกสาร PDF ทั้งหมด, และการโหลดนั้นง่ายเพียงส่งพาธไปยังคอนสตรัคเตอร์.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*ทำไมจึงสำคัญ*: การโหลดเอกสารทำให้คุณเข้าถึงคอลเลกชัน `Pages` ซึ่งเป็นที่ที่เราจะแนบสแตมป์ Bates ต่อไป หากไม่พบไฟล์ Aspose จะโยน `FileNotFoundException` ที่ชัดเจน, ทำให้คุณรู้ว่าผิดพลาดตรงไหน.

---

## ขั้นตอนที่ 2 – สร้าง Text Stamp สำหรับหมายเลข Bates

ตอนนี้เราจะสร้างองค์ประกอบภาพที่จะแสดงบนแต่ละหน้า. คลาส `TextStamp` ให้คุณฝังสตริงใดก็ได้, และเราจะใช้ตัวแทน `{page}-{total}` เพื่อให้ Aspose แทนที่โทเคนเหล่านั้นโดยอัตโนมัติ.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*จุดสำคัญ*:

* **auto adjust font size** – การตั้งค่า `AutoAdjustFontSizeToFitStampRectangle` เป็น `true` รับประกันว่าข้อความจะไม่ล้นออกนอกสี่เหลี่ยม, ซึ่งเหมาะสำหรับหมายเลขหน้าที่มีความยาวเปลี่ยนแปลงได้.
* **add text watermark** – โดยลดค่า `Opacity` เราเปลี่ยนหมายเลข Bates ให้เป็นลายน้ำอ่อน ๆ, ตอบสนองความต้องการ “add text watermark” โดยไม่ต้องทำขั้นตอนแยก.
* **how to add bates** – โทเคน `{page}` และ `{total}` คือสูตรลับ; Aspose แทนที่พวกมันในขณะรัน, ทำให้คุณไม่ต้องคำนวณอะไรเอง.

---

## ขั้นตอนที่ 3 – ใส่สแตมป์ลงทุกหน้า

ข้อผิดพลาดทั่วไปคือการสแตมป์เฉพาะหน้าแรก. เพื่อ **add page numbers pdf** อย่างแท้จริง, เราต้องวนลูปผ่านคอลเลกชัน `Pages` ทั้งหมด.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

ทำไมต้องคลอน? เมธอด `AddStamp` สร้างสำเนาภายใน, แต่การใช้อินสแตนซ์ใหม่สำหรับแต่ละรอบช่วยหลีกเลี่ยงผลข้างเคียงโดยบังเอิญหากคุณแก้ไขคุณสมบัติของสแตมป์ในภายหลัง (เช่นเปลี่ยนสีสำหรับหน้าที่กำหนด).

---

## ขั้นตอนที่ 4 – บันทึก PDF ที่อัปเดต

เมื่อสแตมป์ถูกใส่แล้ว การบันทึกการเปลี่ยนแปลงเป็นเรื่องง่าย. คุณสามารถเขียนทับไฟล์ต้นฉบับหรือบันทึกไปยังตำแหน่งใหม่—ที่นี่เราจะบันทึกไฟล์ใหม่ชื่อ `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

หากคุณเปิด `output.pdf` คุณจะเห็นแต่ละหน้ามีป้าย “Bates: 1‑10”, “Bates: 2‑10”, … ที่มุมล่าง‑ขวา, ด้วยความทึบแสงอ่อนที่ทำหน้าที่เป็น **add text watermark**.

---

## ตัวอย่างทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน, นี่คือโปรแกรมคอนโซลแบบ self‑contained ที่คุณสามารถคัดลอก‑วางลงใน Visual Studio ได้.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Expected result**: เปิด `output.pdf` ด้วยโปรแกรมดูใดก็ได้; แต่ละหน้าจะแสดงบรรทัดเช่น “Bates: 3‑12” ที่มุมล่าง‑ขวา, ขนาดพอดีกับสี่เหลี่ยมและแสดงด้วยความทึบ 40 %. สิ่งนี้ตอบสนองความต้องการการติดตามทางกฎหมายและลายน้ำภาพ.

---

## ความแปรผันทั่วไป & กรณีขอบ

| สถานการณ์ | สิ่งที่ต้องเปลี่ยน | เหตุผล |
|-----------|----------------|-----|
| **Different placement** | ปรับ `HorizontalAlignment` / `VerticalAlignment` หรือกำหนด `XIndent`/`YIndent` | บางบริษัทอาจต้องการวางที่ด้านบน‑ซ้ายหรือกึ่งกลาง. |
| **Custom prefix** | แทนที่ `"Bates: "` ด้วย `"Doc‑ID: "` หรือสตริงใดก็ได้ | คุณอาจใช้รูปแบบการตั้งชื่อที่แตกต่าง. |
| **Multiple stamps** | สร้าง `TextStamp` ตัวที่สอง (เช่น สำหรับประกาศความลับ) แล้วเพิ่มหลังจากตัวแรก | การรวม **add bates numbering** กับความต้องการ **add text watermark** อื่น ๆ เป็นเรื่องง่าย. |
| **Large page counts** | เพิ่มขนาดฟอนต์เริ่มต้น (เช่น `14`) – การปรับอัตโนมัติจะทำให้ลดลงเมื่อจำเป็น | เมื่อมีหน้ามากกว่า 999 หน้า สตริงจะยาวขึ้น; การปรับอัตโนมัติช่วยป้องกันการตัด. |
| **Encrypted PDFs** | เรียก `pdfDocument.Decrypt("password")` ก่อนทำสแตมป์ | คุณไม่สามารถแก้ไขไฟล์ที่เข้ารหัสได้โดยไม่มีรหัสผ่าน. |

---

## เคล็ดลับระดับมืออาชีพ & สิ่งที่ควรระวัง

* **Pro tip:** ตั้งค่า `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)` หากคุณสังเกตว่าข้อความชิดขอบหน้า.  
* **Watch out for:** สี่เหลี่ยมขนาดเล็กมาก (ขนาดเริ่มต้นคือ 100 × 30 pt). หากต้องการพื้นที่ใหญ่ขึ้น, ตั้งค่า `batesStamp.Width` และ `batesStamp.Height` ด้วยตนเอง.  
* **Performance note:** การสแตมป์หลายพันหน้าอาจใช้เวลาสองสามวินาที, แต่ Aspose สตรีมหน้าต่างอย่างมีประสิทธิภาพ—ไม่จำเป็นต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ.  

---

## สรุป

เราได้สาธิตวิธี **add bates numbering** ให้กับ PDF ด้วย Aspose.Pdf, พร้อมกับ **add page numbers pdf**, เปิดใช้งาน **auto adjust font size**, และสร้าง **add text watermark** ในกระบวนการเดียวที่ต่อเนื่อง ตัวอย่างที่ทำงานได้เต็มรูปแบบข้างต้นให้พื้นฐานที่มั่นคงซึ่งคุณสามารถปรับใช้กับกระบวนการทำงานเอกสารทางกฎหมายหรือระบบรายงานภายในใด ๆ

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? ลองผสานวิธีนี้กับ API การรวม PDF ของ Aspose เพื่อประมวลผลหลายไฟล์เป็นชุด, หรือสำรวจคลาส `TextFragment` เพื่อสร้างลายน้ำที่หลากหลายกว่า (สี, หมุน, หรือหลายบรรทัด). ความเป็นไปได้ไม่มีที่สิ้นสุด, และโค้ดที่คุณมีตอนนี้เป็นฐานที่เชื่อถือได้.

หากคุณพบว่าคู่มือนี้เป็นประโยชน์, อย่าลังเลที่จะแสดงความคิดเห็น, ให้ดาวน์โหลด repository, หรือแบ่งปันการปรับเปลี่ยนของคุณเอง. โค้ดดิ้งอย่างสนุกสนาน, และขอให้ PDF ของคุณมีหมายเลขที่สมบูรณ์แบบเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}