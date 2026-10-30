---
category: general
date: 2026-08-14
description: วิธีตั้งค่าตัวเลือกการใส่หมายเลขบาเตสใน C# ด้วย GroupDocs. ทำตามบทแนะนำขั้นตอนต่อขั้นตอนนี้เพื่อเพิ่มคำนำหน้าที่กำหนดเองและตั้งค่าตัวเลขเริ่มต้นเมื่อแปลงไฟล์
  Word เป็น PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: th
lastmod: 2026-08-14
og_description: วิธีตั้งค่าตัวเลือกการใส่หมายเลขบาเตสใน C# อย่างรวดเร็ว คู่มือนี้จะแสดงวิธีเพิ่มคำนำหน้าที่กำหนดเองและตั้งค่าเลขเริ่มต้นเมื่อแปลงไฟล์
  Word เป็น PDF.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: วิธีตั้งค่าตัวเลือกการนับเลขบาเตสใน C# – สอนทีละขั้นตอน
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: วิธีตั้งค่าตัวเลือกการทำหมายเลขบาเตสใน C# – คู่มือฉบับสมบูรณ์
url: /th/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีตั้งค่าตัวเลือกการใส่หมายเลข Bates ใน C# – คู่มือฉบับสมบูรณ์

หากคุณต้องการ **วิธีตั้งค่าตัวเลือกการใส่หมายเลข Bates** ใน C# คู่มือนี้จะพาคุณผ่านขั้นตอนอย่างละเอียด คุณจะได้เรียนรู้วิธีกำหนดหมายเลขเริ่มต้น เพิ่มคำนำหน้า และนำหมายเลขไปใช้ขณะแปลงเอกสาร Word เป็น PDF ด้วย GroupDocs API  

การประมวลผลเอกสารมักต้องการตัวระบุที่ไม่ซ้ำกันบนแต่ละหน้าเพื่อวัตถุประสงค์ทางกฎหมายหรือการจัดเก็บเอกสาร เมื่อจบการสอนนี้คุณจะมีโค้ดสั้นที่สามารถนำไปใช้ซ้ำได้ในโปรเจกต์ .NET ใด ๆ ไม่ว่าจะเป็นเครื่องมือสนับสนุนการฟ้องร้องหรือเครื่องมือสร้างรายงานอัตโนมัติ ไม่ต้องใช้เครื่องมือภายนอก—เพียงแค่ไลบรารี GroupDocs.Conversion และโค้ด C# ไม่กี่บรรทัด  

## สิ่งที่คุณต้องเตรียม

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

* .NET 6.0 SDK หรือรุ่นที่ใหม่กว่า ติดตั้งแล้ว  
* Visual Studio 2022 (หรือ IDE ใด ๆ ที่รองรับ .NET)  
* ไลเซนส์ GroupDocs.Conversion ที่ใช้งานได้ (รุ่นทดลองฟรีใช้สำหรับการทดสอบ)  
* ตัวอย่างไฟล์ Word (`input.docx`) ที่ต้องการใส่หมายเลข  

ข้อกำหนดเหล่านี้ทำให้โค้ดทำงานได้โดยไม่ต้องตั้งค่าเพิ่มเติม  

## วิธีตั้งค่าตัวเลือกการใส่หมายเลข Bates – ภาพรวม

หัวใจของ **วิธีตั้งค่าตัวเลือกการใส่หมายเลข Bates** อยู่ในสามอ็อบเจกต์:

1. `Document` – โหลดไฟล์ต้นฉบับ  
2. `BatesNumberingOptions` – เก็บหมายเลขเริ่มต้น คำนำหน้า และรายละเอียดการจัดรูปแบบอื่น ๆ  
3. `AddBatesNumbering` – เมธอดที่แทรกหมายเลขลงในแต่ละหน้า  

การเข้าใจเหตุผลที่แต่ละส่วนมีอยู่ช่วยให้คุณปรับโซลูชันให้เข้ากับสถานการณ์ที่ซับซ้อนมากขึ้น เช่น ฟอนต์ที่กำหนดเองหรือการใส่หมายเลขหลายภาษา  

## ขั้นตอนที่ 1: ติดตั้งแพคเกจ NuGet ของ GroupDocs.Conversion

เปิดเทอร์มินัลในโฟลเดอร์โซลูชันของคุณและรัน:

```bash
dotnet add package GroupDocs.Conversion
```

**GroupDocs API** ให้คลาส `Document` และเมธอดส่วนขยาย `AddBatesNumbering` ที่จะใช้ต่อในบทเรียนนี้  

## ขั้นตอนที่ 2: โหลดเอกสารต้นฉบับ

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*ทำไมต้องทำขั้นตอนนี้?*  
การโหลดไฟล์จะสร้างการแสดงผลในหน่วยความจำที่เครื่องมือแปลงสามารถจัดการได้ หากไม่มีอินสแตนซ์ `Document` คุณจะไม่สามารถใส่หมายเลข Bates หรือทำการแปลงอื่น ๆ ได้  

## ขั้นตอนที่ 3: สร้างตัวเลือกการใส่หมายเลข Bates

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*ทำไมต้องทำขั้นตอนนี้?*  
`BatesNumberingOptions` รวมการตั้งค่าทั้งหมดที่คุณอาจต้องการเมื่อ **ตั้งค่าตัวเลือกการใส่หมายเลข Bates** การปรับ `StartNumber` และ `Prefix` ช่วยให้ผลลัพธ์สอดคล้องกับระบบจัดการคดีของคุณ คุณสมบัติ `Position` ควบคุมตำแหน่งการแสดงผล ซึ่งมักเป็นข้อกำหนดด้านการปฏิบัติตามกฎระเบียบ  

## ขั้นตอนที่ 4: นำหมายเลข Bates ไปใช้กับเอกสาร

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

เมธอด `AddBatesNumbering` จะวนผ่านแต่ละหน้าของ `Document` ที่โหลดแล้วและแทรกสตริงที่กำหนดไว้ เนื่องจากเมธอดทำงานบนการแสดงผลในหน่วยความจำ คุณจึงสามารถต่อขั้นตอนการประมวลผลเพิ่มเติม (เช่น การใส่ลายน้ำ) ก่อนบันทึกได้  

## ขั้นตอนที่ 5: แปลงและบันทึกผลลัพธ์เป็น PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*ทำไมต้องทำขั้นตอนนี้?*  
การบันทึกเป็น PDF เป็นรูปแบบสุดท้ายที่นิยมใช้สำหรับเอกสารทางกฎหมาย `PdfConvertOptions` ช่วยให้คุณปรับแต่งผลลัพธ์ได้ละเอียดขึ้น แต่ไม่จำเป็นสำหรับการใส่หมายเลขพื้นฐาน คำสั่ง `Save` จะเขียนไฟล์ PDF ที่มีหมายเลขครบถ้วนลงดิสก์  

## ตัวอย่างที่สมบูรณ์และสามารถรันได้

รวมทุกอย่างเข้าด้วยกัน นี่คือตัวอย่างแอปคอนโซลที่สมบูรณ์ สามารถคอมไพล์และรันได้:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง**  

เมื่อรันโปรแกรมจะสร้าง `output.pdf` ที่ทุกหน้าจะแสดงป้ายเช่น `CASE-1000`, `CASE-1001` ฯลฯ อยู่ที่ส่วนท้ายขวา เปิด PDF ด้วยโปรแกรมดูใด ๆ เพื่อยืนยันว่าตัวเลขปรากฏตามที่ต้องการ  

## ข้อผิดพลาดทั่วไปและแนวทางปฏิบัติที่ดีที่สุด

| ปัญหา | ทำไมถึงเกิด | วิธีหลีกเลี่ยง |
|-------|--------------|----------------|
| **Relative paths cause `FileNotFoundException`** | โฟลเดอร์ทำงานของแอปคอนโซลอาจแตกต่างจากของ Visual Studio | ใช้เส้นทางแบบ absolute หรือ `Path.Combine(AppContext.BaseDirectory, "input.docx")` |
| **Numbering overlaps existing footers** | หากเอกสารต้นฉบับมีเนื้อหาอยู่ในพื้นที่ส่วนท้ายที่เลือก ตัวเลขใหม่อาจถูกซ่อน | เลือก `Position` อื่น (เช่น `HeaderLeft`) หรือปรับเทมเพลตต้นฉบับ |
| **Large documents are slow** | การใส่หมายเลข Bates ต้องวนผ่านทุกหน้า การใช้หน่วยความจำเพิ่มขึ้นตามขนาดไฟล์ | แบ่งการประมวลผลเป็นชิ้นส่วนโดยใช้ `Document.Split` หากเกิน 500 หน้า |
| **License expiration** | รุ่นทดลองของ GroupDocs หมดอายุหลัง 30 วัน ทำให้เกิดข้อยกเว้นที่ `AddBatesNumbering` | ใส่คีย์ไลเซนส์ที่ใช้งานได้ก่อนโหลดเอกสาร: `License license = new License(); license.SetLicense("license.lic");` |

**เคล็ดลับ:** หากต้องการรูปแบบหมายเลขที่แตกต่างตามคดี (เช่น `2023-CASE-001`) ให้สร้างคำนำหน้าแบบไดนามิกก่อนสร้าง `BatesNumberingOptions`  

## การขยายโซลูชัน

วิธี **Bates numbering C#** เดียวกันทำงานกับรูปแบบแหล่งข้อมูลอื่น ๆ เช่น `.txt`, `.html` หรือแม้กระทั่งรูปภาพ เพียงเปลี่ยนส่วนต่อท้ายไฟล์เมื่อสร้างอ็อบเจกต์ `Document` แล้วเอนจินแปลงจะจัดการส่วนที่เหลือให้เอง  

คุณอาจผสาน **document conversion C#** กับ OCR สำหรับ PDF ที่สแกนไว้ได้เช่นกัน:

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## สรุป

ตอนนี้คุณรู้แล้วว่า **วิธีตั้งค่าตัวเลือกการใส่หมายเลข Bates** ใน C# ตั้งแต่ต้นจนจบ โดยการสร้างอ็อบเจกต์ `BatesNumberingOptions` ใช้งานกับ `AddBatesNumbering` แล้วบันทึกผลเป็น PDF คุณสามารถอัตโนมัติการผลิตเอกสารที่เป็นไปตามกฎหมายและมีตัวระบุเฉพาะ  

จากนี้คุณสามารถสำรวจหัวข้อที่เกี่ยวข้อง เช่น **C# PDF generation**, **document conversion C#**, หรือคุณลักษณะขั้นสูงของ **GroupDocs API** เช่น การใส่ลายน้ำและลายเซ็นดิจิทัล ทดลองใช้คำนำหน้า ตำแหน่ง และรูปแบบหมายเลขต่าง ๆ เพื่อให้เข้ากับกระบวนการทำงานของคุณ  

ขอให้สนุกกับการเขียนโค้ด!  

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้ในโปรเจกต์ของคุณเอง  

- [เพิ่มหมายเลข Bates PDF ใน C# – คู่มือฉบับสมบูรณ์](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)  
- [วิธีเพิ่มและปรับแต่งเลขหน้าใน PDF ด้วย Aspose.PDF สำหรับ .NET | คู่มือการจัดการเอกสาร](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)  
- [วิธีเพิ่มข้อความสแตมป์ที่ส่วนท้ายใน PDF ด้วย Aspose.PDF สำหรับ .NET: คู่มือแบบขั้นตอนต่อขั้นตอน](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}