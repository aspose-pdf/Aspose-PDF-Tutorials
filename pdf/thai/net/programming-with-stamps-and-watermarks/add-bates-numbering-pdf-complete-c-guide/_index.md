---
category: general
date: 2026-03-22
description: เพิ่มหมายเลข Bates ให้ไฟล์ PDF อย่างรวดเร็วด้วย Aspose.Pdf. เรียนรู้วิธีเพิ่ม
  Bates, เพิ่มหมายเลขหน้าแบบต่อเนื่อง, เพิ่มส่วนท้าย PDF ที่กำหนดเอง, และเพิ่มอาร์ติแฟคท์ลงใน
  PDF ภายในไม่กี่นาที.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: th
og_description: เพิ่มหมายเลข Bates ให้ไฟล์ PDF ด้วย Aspose.Pdf คู่มือนี้แสดงวิธีเพิ่ม
  Bates, เพิ่มหมายเลขหน้าตามลำดับ, เพิ่มส่วนท้ายที่กำหนดเองใน PDF, และเพิ่มอาร์ติแฟกต์ใน
  PDF.
og_title: เพิ่มหมายเลข Bates ให้กับ PDF – คำแนะนำ C# ทีละขั้นตอน
tags:
- Aspose.Pdf
- C#
- PDF automation
title: เพิ่มหมายเลข Bates ใน PDF – คู่มือ C# ฉบับสมบูรณ์
url: /th/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มหมายเลข Bates PDF – คู่มือ C# ฉบับสมบูรณ์

เคยต้องการ **add bates numbering pdf** ให้กับชุดเอกสารทางกฎหมายหลายไฟล์แต่ไม่แน่ใจว่าจะเริ่มอย่างไรหรือไม่? คุณไม่ได้เป็นคนแรก—นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อต้องสร้างเครื่องมือจัดการคดี ข่าวดีคือ? ด้วย Aspose.Pdf คุณสามารถ **add bates**, **add sequential page numbers**, และแม้กระทั่ง **add custom footer pdf** ได้ในไม่กี่บรรทัดของโค้ด.  

ในบทแนะนำนี้เราจะพาคุณผ่านกระบวนการทั้งหมด ตั้งแต่การติดตั้งไลบรารีจนถึงการบันทึกไฟล์สุดท้าย และเราจะใส่เคล็ดลับเกี่ยวกับวิธี **add artifact to pdf** ไฟล์โดยไม่ทำลายเนื้อหาที่มีอยู่ ตอนจบคุณจะได้โค้ดสั้นที่พร้อมใช้งานซึ่งสามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้.

## สิ่งที่คุณต้องการ

- .NET 6+ (โค้ดทำงานบน .NET Core และ .NET Framework ได้เช่นกัน)  
- ใบอนุญาต Aspose.Pdf for .NET ที่ถูกต้อง (คุณสามารถเริ่มต้นด้วยการทดลองใช้ฟรี)  
- ไฟล์ PDF อินพุต (`input.pdf`) ที่วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงได้  
- Visual Studio, Rider หรือเครื่องมือแก้ไข C# ใดก็ได้ที่คุณชอบ  

แค่นั้น—ไม่มีแพ็กเกจ NuGet เพิ่มเติมนอกจาก Aspose.Pdf.

## ขั้นตอนที่ 1: ติดตั้ง Aspose.Pdf ผ่าน NuGet

สิ่งแรกที่ต้องทำ—มาติดตั้งไลบรารีบนเครื่องของคุณ เปิดเทอร์มินัลในโฟลเดอร์โปรเจกต์ของคุณและรัน:

```bash
dotnet add package Aspose.Pdf
```

หรือ หากคุณใช้ Package Manager Console ของ Visual Studio:

```powershell
Install-Package Aspose.Pdf
```

*Pro tip:* หลังการติดตั้ง ตรวจสอบให้แน่ใจว่าโฟลเดอร์ `Aspose.Pdf` ปรากฏภายใต้ `Dependencies → Packages` ใน Solution Explorer ของคุณ.

## ขั้นตอนที่ 2: โหลดเอกสาร PDF ต้นฉบับ

ตอนนี้เราจะสร้างอ็อบเจ็กต์ `Document` ที่แทน PDF ที่เราต้องการใส่สแตมป์ การใช้คำสั่ง `using` ทำให้แน่ใจว่าการจัดการไฟล์จะถูกปล่อยอัตโนมัติ.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

ทำไมต้องใช้ `using var`? มันรับประกันการทำลายออบเจ็กต์แม้เกิดข้อยกเว้น ช่วยป้องกันปัญหาไฟล์ล็อกเมื่อต้องการเขียนทับไฟล์เดียวกันในภายหลัง.

## ขั้นตอนที่ 3: สร้างและกำหนดค่า Bates Numbering Artifact

หมายเลข Bates เป็นแค่ artifact ข้อความที่อยู่ในโครงสร้างเชิงตรรกะของ PDF คุณสามารถถือว่ามันเป็น **custom footer pdf** เพราะมันปรากฏบนทุกหน้าโดยไม่เป็นส่วนหนึ่งของสตรีมเนื้อหาของหน้า.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### ทำไมการตั้งค่าเหล่านี้ถึงสำคัญ

- **Prefix**: มีประโยชน์สำหรับแยกประเภทเอกสาร (เช่น “INV‑” สำหรับใบแจ้งหนี้).  
- **Start**: กำหนดหมายเลขแรก; คุณสามารถดึงค่าจากฐานข้อมูลหากต้องการความต่อเนื่องระหว่างไฟล์.  
- **Format**: `"0000"` บังคับให้แสดงเป็นสี่หลัก เพื่อให้การจัดแนวคงที่เมื่อจำนวนเพิ่มขึ้น.  
- **X/Y**: พิกัดวัดจากมุมซ้าย‑ล่าง, ดังนั้น `Y = 20` จะวางข้อความอยู่เหนือขอบหน้ากระดาษเล็กน้อย ปรับ `X` หากต้องการให้หมายเลขจัดชิดซ้ายหรือกึ่งกลาง.

หากคุณต้องการ **add sequential page numbers** แทนหมายเลข Bates เพียงลบ `Prefix` ออกและปรับ `Format` เป็น `"###"` หรือรูปแบบใดก็ได้ที่คุณต้องการ.

## ขั้นตอนที่ 4: ใส่ Artifact ไปยังทุกหน้า

Aspose.Pdf ให้คุณแนบ artifact ไปยังเอกสารทั้งหมดด้วยการเรียกครั้งเดียว นี่เป็นวิธีที่มีประสิทธิภาพที่สุดในการ **add artifact to pdf** โดยไม่ต้องวนลูปผ่านแต่ละหน้าเอง.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

เบื้องหลัง Aspose จะเพิ่ม artifact ไปยังพจนานุกรมของแต่ละหน้า ซึ่งหมายความว่าการตั้งหมายเลขจะเป็นส่วนหนึ่งของโครงสร้างเชิงตรรกะของ PDF—เหมาะสำหรับการสกัดหรือค้นหาในภายหลัง.

## ขั้นตอนที่ 5: บันทึก PDF ที่อัปเดต

สุดท้ายให้เขียนการเปลี่ยนแปลงกลับไปยังดิสก์ คุณสามารถเขียนทับไฟล์เดิมหรือบันทึกเป็นไฟล์ใหม่; วิธีหลังปลอดภัยกว่าในระหว่างการพัฒนา.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

เมื่อคุณเปิด `output.pdf` ในโปรแกรมดูไฟล์ คุณจะเห็น “INV‑1000”, “INV‑1001”, … ที่มุมล่าง‑ขวาของแต่ละหน้า.

### ตรวจสอบผลลัพธ์

เปิด PDF ใน Adobe Acrobat หรือโปรแกรมดูไฟล์ใดก็ได้และมองหาตัวเลข หากต้องการยืนยันโดยโปรแกรม คุณสามารถอ่าน artifact กลับมาได้:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

## กรณีขอบและคำถามทั่วไป

### ถ้า PDF ของฉันมี Footer อยู่แล้วจะทำอย่างไร?

การเพิ่ม artifact จะไม่เขียนทับ footer ที่มีอยู่เพราะ artifacts อยู่ในชั้นแยก อย่างไรก็ตาม หากการทับซ้อนกันเป็นปัญหา ให้ปรับพิกัด `Y` หรือเพิ่มค่า offset ของ `X` เพื่อย้ายหมายเลข Bates ออกไป.

### สามารถใช้ฟอนต์หรือสีอื่นได้หรือไม่?

ได้เลย `BatesNumberingArtifact` สืบทอดจาก `Artifact` ดังนั้นคุณสามารถตั้งค่า `Font`, `FontColor` และแม้กระทั่ง `Opacity` ตัวอย่าง:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### จะรีเซ็ตตัวนับสำหรับเอกสารใหม่อย่างไร?

เพียงเปลี่ยนค่า `Start` ก่อนเรียก `AddArtifact` หากคุณสร้าง PDF จำนวนมากในลูป ให้เก็บตัวนับที่ทำงานต่อเนื่องในตรรกะของแอปพลิเคชัน.

### วิธีนี้เข้ากันได้กับ PDF ที่เข้ารหัสหรือไม่?

Aspose.Pdf สามารถเปิด PDF ที่เข้ารหัสได้หากคุณใส่รหัสผ่าน:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

หลังจากถอดรหัส ขั้นตอนการเพิ่ม artifact จะทำงานได้อย่างไม่มีปัญหา.

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่สมบูรณ์พร้อมรัน ให้วางลงในแอปคอนโซล ปรับเส้นทางไฟล์ แล้วกด **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** คอนโซลจะแสดงข้อความ “Bates numbering added successfully!” และ `output.pdf` จะมีป้ายลำดับเช่น `INV‑1000`, `INV‑1001` ฯลฯ อยู่ที่มุมล่าง‑ขวาของแต่ละหน้า.

## สรุปสั้น

- **เป้าหมายหลัก:** **add bates numbering pdf** ด้วย Aspose.Pdf.  
- เราได้อธิบาย **how to add bates**, **add sequential page numbers**, และ **add custom footer pdf** ผ่าน artifact เดียว.  
- บทแนะนำแสดงวิธี **add artifact to pdf**, จัดการกรณีขอบ และตรวจสอบผลลัพธ์.  

## ขั้นตอนต่อไป?

- **Dynamic prefixes:** ดึงค่าจากฐานข้อมูลเพื่อสร้าง “CASE‑2023‑001”, “CASE‑2023‑002”, …  
- **Conditional placement:** ใช้การตรวจจับขนาดหน้า (`page.MediaBox`) เพื่อจัดศูนย์หมายเลขบนหน้ากว้าง.  
- **Combine with watermarks:** เพิ่มโลโก้กึ่งโปร่งใสพร้อมหมายเลข Bates เพื่อการสร้างแบรนด์.  

ลองทดลองได้เลย—อาจจะค้นพบวิธีที่ฉลาดกว่าในการประมวลผลไฟล์หลายพันไฟล์พร้อมกัน หากเจอปัญหา แค่คอมเมนต์หรือดูเอกสารอย่างเป็นทางการของ Aspose (มันชัดเจนมาก) ขอให้เขียนโค้ดสนุก!  

![add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "Screenshot showing add bates numbering pdf in a PDF viewer")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}