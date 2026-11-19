---
category: general
date: 2026-11-19
description: เรียนรู้วิธีตั้งค่าความโปร่งแสงและวิธีเปลี่ยนโหมดผสมในไฟล์ PDF ด้วย Aspose.Pdf
  คู่มือ C# ทีละขั้นตอนสำหรับกราฟิกโปร่งแสง
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set opacity
- how to change blend
- Aspose.Pdf graphics state
- PDF transparency C#
- modify PDF resources
language: th
lastmod: 2026-11-19
og_description: วิธีตั้งค่าความทึบและวิธีเปลี่ยนโหมดผสมใน PDF ด้วย Aspose.Pdf. ทำตามบทเรียน
  C# ฉบับเต็มนี้เพื่อทำให้กราฟิกเป็นโปร่งใส.
og_image_alt: Code editor showing C# example that sets PDF opacity and blend mode
og_title: วิธีตั้งค่าความโปร่งใสและเปลี่ยนโหมดการผสมในไฟล์ PDF ด้วย Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to set opacity and how to change blend mode in a PDF using
    Aspose.Pdf. Step‑by‑step C# guide for transparent graphics.
  headline: How to set opacity in a PDF and how to change blend mode with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
- Transparency
title: วิธีตั้งค่าความทึบใน PDF และวิธีเปลี่ยนโหมดการผสมด้วย Aspose.Pdf
url: /th/net/images-graphics/how-to-set-opacity-in-a-pdf-and-how-to-change-blend-mode-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีตั้งค่าความทึบแสงและวิธีเปลี่ยนโหมดการผสมใน PDF ด้วย Aspose.Pdf

หากคุณต้องการ **วิธีตั้งค่าความทึบแสง** สำหรับวัตถุภายใน PDF คู่มือนี้จะแสดงขั้นตอนที่แน่นอน นอกจากนี้ยังครอบคลุม **วิธีเปลี่ยนโหมดการผสม** เพื่อให้สถานะกราฟิกใหม่ผสมอย่างถูกต้องกับเนื้อหาของหน้า

ในบทแนะนำนี้คุณจะได้:

* โหลด PDF ที่มีอยู่ด้วย Aspose.Pdf
* เข้าถึงพจนานุกรมทรัพยากรของหน้า
* สร้างพจนานุกรมสถานะกราฟิกใหม่ที่กำหนดความทึบของเส้นขอบ, ความทึบของการเติมสี, และโหมดการผสม
* เพิ่มสถานะกราฟิกลงในคอลเลกชัน `ExtGState`
* บันทึก PDF ที่อัปเดตแล้ว

ไม่ต้องใช้เครื่องมือภายนอก—เพียงแค่ไลบรารี Aspose.Pdf for .NET และสภาพแวดล้อมการพัฒนา .NET

## ข้อกำหนดเบื้องต้น

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.6+)
* แพ็กเกจ NuGet ของ Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)
* ไฟล์ PDF ชื่อ `input.pdf` อยู่ในโฟลเดอร์ที่สามารถเขียนได้ (เปลี่ยน `YOUR_DIRECTORY` เป็นเส้นทางจริงของคุณ)

## ขั้นตอนที่ 1: ติดตั้ง Aspose.Pdf และตั้งค่าโปรเจกต์

สร้างโปรเจกต์คอนโซลใหม่และเพิ่มการอ้างอิง Aspose.Pdf:

```bash
dotnet new console -n PdfOpacityDemo
cd PdfOpacityDemo
dotnet add package Aspose.Pdf
```

ไฟล์โปรเจกต์ตอนนี้รวมแอสเซมบลี Aspose.Pdf ซึ่งให้คลาส `Document`, `DictionaryEditor` และ `CosPdfDictionary` ที่จะใช้ต่อไป

## ขั้นตอนที่ 2: โหลดเอกสาร PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Engine;
using Aspose.Pdf.Engine.Data;

// Load the existing PDF
Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

**ทำไมขั้นตอนนี้สำคัญ:** การโหลดเอกสารจะสร้างตัวแทนในหน่วยความจำที่คุณสามารถแก้ไขได้ หากข้ามขั้นตอนนี้ พจนานุกรมทรัพยากรจะไม่สามารถเข้าถึงได้

## ขั้นตอนที่ 3: รับหน้าแรกและพจนานุกรมทรัพยากรของมัน

```csharp
// Retrieve the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];

// Open the page’s resource dictionary for editing
DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);
```

**คำอธิบาย:** พจนานุกรม `Resources` มีวัตถุต่าง ๆ เช่น ฟอนต์, รูปภาพ, และคอลเลกชัน `ExtGState` การแก้ไขพจนานุกรมนี้ทำให้คุณสามารถแทรกสถานะกราฟิกใหม่ที่ควบคุมความทึบและการผสมได้

## ขั้นตอนที่ 4: เข้าถึง (หรือสร้าง) พจนานุกรม ExtGState

```csharp
// Try to get the existing ExtGState dictionary; create it if missing
CosPdfDictionary extGStateDict = null;
if (resourceEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create an empty ExtGState dictionary and add it to resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourceEditor["ExtGState"] = extGStateDict;
}
```

**ทำไมต้องทำขั้นตอนนี้:** รายการ `ExtGState` เก็บอ็อบเจ็กต์สถานะกราฟิก หากไม่มีคุณต้องสร้างก่อนที่จะเพิ่มรายการใหม่

## ขั้นตอนที่ 5: สร้างสถานะกราฟิกใหม่พร้อมความทึบและโหมดการผสม

```csharp
// Create a new empty graphics state dictionary
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Set stroke opacity (CA) – 1 = fully opaque, 0 = fully transparent
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Set fill opacity (ca) – 0.5 = 50 % transparent fill
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Set blend mode (BM) – "Normal" is the default; other options: Multiply, Screen, Overlay, etc.
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

**วิธีที่วิธีนี้แก้ปัญหา:**  
* `CA` ควบคุมความทึบของเส้นที่วาด (เช่น เส้น)  
* `ca` ควบคุมความทึบของรูปที่เติมสี (เช่น สี่เหลี่ยม)  
* `BM` กำหนดวิธีการผสานกราฟิกใหม่กับเนื้อหาหน้าที่มีอยู่ การเปลี่ยนโหมดการผสมคือ **วิธีเปลี่ยนโหมดการผสม** สำหรับ PDF อย่างแท้จริง

## ขั้นตอนที่ 6: ลงทะเบียนสถานะกราฟิกในคอลเลกชัน ExtGState

```csharp
// Use a unique key for the new graphics state (e.g., GS0)
extGStateDict.Add("GS0", newGraphicsState);
```

ตอนนี้หน้าจะอ้างอิงสถานะกราฟิกนี้ด้วยชื่อ `/GS0` เนื้อหาใด ๆ ที่ตั้งค่า `/GS0 gs` จะใช้ความทึบและโหมดการผสมที่กำหนดไว้

## ขั้นตอนที่ 7: ใช้สถานะกราฟิกกับเนื้อหาที่มีอยู่ (ไม่บังคับ)

หากต้องการแก้ไขคำสั่งการวาดที่มีอยู่ คุณสามารถใส่ตัวดำเนินการสถานะกราฟิกไว้หน้าสตรีมเนื้อหาของหน้า:

```csharp
// Retrieve the content stream as a string
string pageContent = firstPage.Contents[1].ToString();

// Prepend the graphics state operator
string modifiedContent = "GS0 gs\n" + pageContent;

// Replace the original content
firstPage.Contents[1].Replace(modifiedContent);
```

**หมายเหตุ:** ขั้นตอนนี้เป็นทางเลือก หากคุณเพิ่มคำสั่งการวาดใหม่ในภายหลัง เพียงเริ่มสตรีมด้วย `GS0 gs`

## ขั้นตอนที่ 8: บันทึก PDF ที่แก้ไขแล้ว

```csharp
pdfDocument.Save(@"YOUR_DIRECTORY\out.pdf");
```

ไฟล์ `out.pdf` ที่ได้จะมีสถานะกราฟิกที่ความทึบของการเติมสีเป็น 50 % และโหมดการผสมเป็น `Normal` เนื้อหาใด ๆ ที่ใช้ `/GS0 gs` จะเรนเดอร์ด้วยความโปร่งใสที่ระบุ

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงใน `Program.cs` แล้วรันได้:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Engine;
using Aspose.Pdf.Engine.Data;

class Program
{
    static void Main()
    {
        // 1. Load the PDF document
        Document pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get the first page and its resource dictionary
        Page firstPage = pdfDocument.Pages[1];
        DictionaryEditor resourceEditor = new DictionaryEditor(firstPage.Resources);

        // 3. Access or create the ExtGState dictionary
        CosPdfDictionary extGStateDict;
        if (resourceEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourceEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourceEditor["ExtGState"] = extGStateDict;
        }

        // 4. Define a new graphics state with opacity and blend mode
        CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity (fully opaque)
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity (50 % transparent)
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode (Normal)

        // 5. Add the graphics state to ExtGState collection
        extGStateDict.Add("GS0", newGraphicsState);

        // 6. (Optional) Apply the graphics state to existing page content
        if (firstPage.Contents.Count > 0)
        {
            string original = firstPage.Contents[1].ToString();
            string withGs = "GS0 gs\n" + original;
            firstPage.Contents[1].Replace(withGs);
        }

        // 7. Save the updated PDF
        pdfDocument.Save(@"YOUR_DIRECTORY\out.pdf");

        Console.WriteLine("PDF updated successfully – opacity set and blend mode changed.");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมจะแสดงผล:

```
PDF updated successfully – opacity set and blend mode changed.
```

เมื่อคุณเปิด `out.pdf` ในโปรแกรมอ่าน PDF ใด ๆ รูปร่างที่ใช้สถานะกราฟิกที่กำหนดใหม่จะปรากฏด้วยความโปร่งใสของการเติมสี 50 % ขณะที่เส้นขอบยังคงทึบเต็มที่ โหมดการผสม `Normal` ทำให้กราฟิกถูกผสานโดยไม่มีเอฟเฟกต์พิเศษ คุณสามารถเปลี่ยน `"Normal"` เป็น `"Multiply"` หรือ `"Screen"` เพื่อดู **วิธีเปลี่ยนโหมดการผสม** สำหรับผลลัพธ์ที่แตกต่างกัน

## คำถามที่พบบ่อยและกรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| **ฉันสามารถตั้งค่าความทึบต่าง ๆ สำหรับหลายวัตถุได้หรือไม่?** | ได้ คุณสามารถสร้างสถานะกราฟิกเพิ่มเติม (เช่น `GS1`, `GS2`) พร้อมค่ `ca`/`CA` ที่แตกต่างกันและอ้างอิงชื่อที่เหมาะสมก่อนวาดแต่ละวัตถุ |
| **ถ้า PDF มีรายการ `ExtGState` ชื่อ `GS0` อยู่แล้วจะทำอย่างไร?** | เลือกคีย์ที่ไม่ซ้ำ (`GS1`, `MyOpacityState` ฯลฯ) หรือเขียนทับรายการเดิมหากไม่ต้องการคำนิยามเก่า |
| **โหมดการผสมจำกัดแค่ `Normal` หรือไม่?** | ไม่ มีชื่อที่ใช้ได้รวมถึง `Multiply`, `Screen`, `Overlay`, `Darken`, `Lighten`, `ColorDodge`, `ColorBurn`, `HardLight`, `SoftLight`, `Difference`, `Exclusion`, และ `Hue`, `Saturation`, `Color`, `Luminosity` |
| **วิธีนี้ทำงานกับ PDF ที่เข้ารหัสหรือไม่?** | Aspose.Pdf สามารถเปิด PDF ที่เข้ารหัสได้หากคุณระบุรหัสผ่านผ่าน `Document(string, LoadOptions)` การจัดการสถานะกราฟิกทำงานเช่นเดียวกันหลังจากถอดรหัส |
| **การเปลี่ยนแปลงจะส่งผลต่อทุกหน้าไหม?** | ตัวอย่างนี้แก้ไขเฉพาะหน้าแรก หากต้องการให้ทุกหน้ามีผล ให้วนลูปผ่าน `pdfDocument.Pages` และทำซ้ำขั้นตอนที่ 2‑6 สำหรับแต่ละหน้า |

## เคล็ดลับระดับมืออาชีพ

* **ใช้สถานะกราฟิกซ้ำ:** เพิ่มสถานะกราฟิกเพียงครั้งเดียวแล้วอ้างอิงบนหลายหน้า จะช่วยลดขนาดไฟล์
* **ประสิทธิภาพ:** การแก้ไข PDF ขนาดใหญ่ในหน่วยความจำอาจใช้ทรัพยากรสูง ใช้ `pdfDocument.Save(..., SaveOptions)` พร้อมการอัปเดตแบบเพิ่มส่วนถ้าต้องการเปลี่ยนแปลงเล็กน้อยเท่านั้น
* **ทดสอบโหมดการผสม:** โปรแกรมอ่าน PDF ทั้งหมดไม่ได้แสดงโหมดการผสมเดียวกันอย่างแม่นยำ ทดสอบผลลัพธ์ใน Adobe Acrobat Reader และโปรแกรมอ่านอื่น (เช่น Foxit) เพื่อยืนยันความสอดคล้องของภาพ

## สรุป

คุณได้เรียนรู้ **วิธีตั้งค่าความทึบแสง** และ **วิธีเปลี่ยนโหมดการผสม** ใน PDF ด้วย Aspose.Pdf for .NET แล้ว การแก้ไขพจนานุกรม `ExtGState` ทำให้คุณควบคุมความโปร่งใสและการผสานได้อย่างละเอียด ช่วยสร้างกราฟิก PDF ระดับมืออาชีพโดยไม่ต้องใช้เครื่องมือภายนอก

ต่อไปคุณอาจสนใจสำรวจ:

* การเพิ่มรูปภาพที่มีพื้นหลังโปร่งใส (**วิธีตั้งค่าความทึบแสง** บนรูปภาพ)
* การสร้างสตรีมเนื้อหาที่สามารถใช้ซ้ำได้และอ้างอิงสถานะกราฟิกใหม่
* การใช้โหมดการผสมอื่น ๆ (**วิธีเปลี่ยนโหมดการผสม** ไปเป็น `Multiply` หรือ `Screen`) เพื่อสร้างเอฟเฟกต์เชิงศิลป์

ขอให้เขียนโค้ดอย่างสนุกและทำให้ PDF ของคุณดูมีชีวิตชีวามากขึ้น!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบต่าง ๆ ในโปรเจกต์ของคุณ

- [How to Change Opacity in PDF with Aspose.PDF – Complete Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-change-opacity-in-pdf-with-aspose-pdf-complete-guide/)
- [How to change opacity in a PDF with Aspose.Pdf for .NET](/pdf/english/net/images-graphics/how-to-change-opacity-in-a-pdf-with-aspose-pdf-for-net/)
- [How to change PDF transparency using Aspose.Pdf in C#](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}