---
category: general
date: 2026-10-07
description: เพิ่มสถานะกราฟิกใน PDF ด้วย Aspose.Pdf บน C# เพื่อแก้ไขความโปร่งใสของ
  PDF. ทำตามคู่มือขั้นตอนต่อขั้นตอนนี้เพื่อฝังสถานะกราฟิกที่กำหนดเองและควบคุมความทึบแสง.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- modify pdf transparency
language: th
lastmod: 2026-10-07
og_description: เพิ่มกราฟิกสเตต PDF ด้วย Aspose.Pdf ใน C#. เรียนรู้วิธีปรับเปลี่ยนความโปร่งใสของ
  PDF โดยการสร้างพจนานุกรมกราฟิกสเตตแบบกำหนดเอง.
og_image_alt: Screenshot showing the add graphics state pdf code editor in Visual
  Studio
og_title: เพิ่มสถานะกราฟิก PDF ด้วย Aspose.Pdf – ควบคุมความโปร่งใสของ PDF
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Add graphics state pdf using Aspose.Pdf in C# to modify PDF transparency.
    Follow this step‑by‑step guide to embed custom graphics states and control opacity.
  headline: Add graphics state pdf with Aspose.Pdf in C#
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: เพิ่มสถานะกราฟิก PDF ด้วย Aspose.Pdf ใน C#
url: /th/net/images-graphics/add-graphics-state-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่ม graphics state pdf ด้วย Aspose.Pdf ใน C#

หากคุณต้องการ **add graphics state pdf** ให้กับเอกสาร บทแนะนำนี้จะแสดงวิธีทำอย่างละเอียดด้วย Aspose.Pdf สำหรับ .NET. เมื่ออ่านจบคุณจะรู้วิธี **modify PDF transparency** เพื่อกำหนดค่าความทึบแบบกำหนดเองสำหรับการวาดใด ๆ

การทำงานกับ PDF graphics states ช่วยให้คุณควบคุมพารามิเตอร์ต่าง ๆ เช่น ความกว้างของเส้น, โหมดผสม, และที่สำคัญที่สุดสำหรับบทความนี้คือความโปร่งใสของเนื้อหา ขั้นตอนต่อไปเขียนสำหรับนักพัฒนาที่คุ้นเคยกับ C# และต้องการโซลูชันพร้อมรันโดยไม่ต้องค้นหาในเอกสาร SDK อย่างเป็นทางการ

## สิ่งที่คุณจะได้เรียน

* วิธีสร้าง graphics state dictionary ใหม่และใส่ค่า `CA`, `ca`, และ `BM`  
* วิธีแทรก dictionary นั้นลงใน resource `ExtGState` ของหน้าเพื่อให้ PDF รู้จัก  
* วิธีที่ค่า `ca` (stroke) และ `CA` (fill) มีผลต่อ **modify PDF transparency** สำหรับคำสั่งการวาดต่อไป  
* ข้อผิดพลาดทั่วไป เช่น การชนชื่อและความเข้ากันได้ของเวอร์ชัน, พร้อมเคล็ดลับการขยาย graphics state ในภายหลัง

**Prerequisites**

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.7+)  
* ไลเซนส์ Aspose.Pdf for .NET ที่ถูกต้อง (รุ่นทดลองฟรีใช้สำหรับทดสอบ)  
* Visual Studio 2022 หรือ IDE C# ใด ๆ ที่คุณชอบ  

---

## Step 1: Install Aspose.Pdf for .NET

เพิ่มแพคเกจ NuGet ไปยังโปรเจกต์ของคุณ:

```bash
dotnet add package Aspose.Pdf
```

แพคเกจนี้รวม namespace `Aspose.Pdf` ที่ให้คลาส `Document`, `DictionaryEditor`, และ `CosPdfDictionary` ที่ใช้ต่อไป

> **Pro tip:** หากคุณวางแผนประมวลผล PDF จำนวนมากเป็นชุด, ให้เปิด **License** ตั้งแต่ต้นใน `Program.cs` เพื่อหลีกเลี่ยงลายน้ำรุ่นทดลอง

```csharp
// Apply your license (optional for evaluation)
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Aspose.Pdf.lic");
```

## Step 2: Define input and output paths

คุณต้องระบุ SDK ให้ชี้ไปที่ไฟล์ PDF ที่มีอยู่ (`input.pdf`) และกำหนดตำแหน่งที่ไฟล์ที่แก้ไขแล้วจะบันทึก (`output.pdf`)

```csharp
// Define input and output PDF file paths
string inputPath = @"C:\MyPdfs\input.pdf";
string outputPath = @"C:\MyPdfs\output.pdf";
```

> **Why this matters:** การใช้ path แบบเต็มช่วยป้องกัน SDK ไม่ให้ค้นหาในโฟลเดอร์ทำงานผิดที่, ซึ่งเป็นสาเหตุทั่วไปของ `FileNotFoundException`

## Step 3: Open the PDF and locate the first page’s resources

Dictionary `ExtGState` อยู่ภายใน resource dictionary ของแต่ละหน้า เราจะแก้ไขหน้าแรกเพื่อความง่าย, แต่วิธีเดียวกันใช้ได้กับหน้าใดก็ได้

```csharp
using (var pdfDocument = new Aspose.Pdf.Document(inputPath))
{
    // Get the first page (pages are 1‑based)
    var firstPage = pdfDocument.Pages[1];

    // Access the page’s resource dictionary via DictionaryEditor
    var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

    // Retrieve (or create) the ExtGState entry
    var extGStateDict = resourcesEditor["ExtGState"]
        .ToCosPdfDictionary(); // Throws if ExtGState does not exist
```

**Edge case:** หากหน้าดังกล่าวไม่มี entry `ExtGState` คุณต้องสร้างมันขึ้นมา:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    var emptyDict = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor.Add("ExtGState", emptyDict);
    extGStateDict = emptyDict;
}
```

## Step 4: Build a new graphics state dictionary

Graphics state คือชุดของคู่ key/value ที่อธิบายพฤติกรรมของการวาด สำหรับความโปร่งใสเราต้องการสามคีย์:

| Key | Meaning | Typical value |
|-----|---------|---------------|
| `CA` | ความทึบของการเติม (0 = โปร่งใส, 1 = ทึบ) | `1` (เต็มที่) |
| `ca` | ความทึบของการวาดเส้น (สเกลเดียวกัน) | `0.5` (โปร่งใส 50 %) |
| `BM` | โหมดผสม (เช่น `Normal`, `Multiply`) | `Normal` |

```csharp
    // Create an empty dictionary that will hold the graphics state
    var newGraphicsState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Populate the dictionary with transparency and blend mode entries
    var graphicsStateEntries = new[]
    {
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "CA", new Aspose.Pdf.CosPdfNumber(1)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "ca", new Aspose.Pdf.CosPdfNumber(0.5)),
        new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
            "BM", new Aspose.Pdf.CosPdfName("Normal"))
    };

    foreach (var entry in graphicsStateEntries)
        newGraphicsState.Add(entry);
```

**Why these values?**  
`ca = 0.5` ทำให้เส้นใด ๆ (lines, borders) แสดงที่ความโปร่งใส 50 %, ส่วน `CA = 1` ทำให้รูปที่เติมเต็มยังคงทึบเต็มที่ ปรับตัวเลขทั้งสองเพื่อให้ได้ผล **modify PDF transparency** ที่ต้องการ

## Step 5: Insert the graphics state into the ExtGState dictionary

คุณต้องตั้งชื่อให้ state ใหม่ให้เป็นเอกลักษณ์ (เช่น `GS0`). หากชื่อนั้นมีอยู่แล้ว Aspose.Pdf จะเขียนทับ entry เดิม, ซึ่งอาจทำให้เนื้อหาอื่นที่อ้างอิงเสีย

```csharp
    // Add the new graphics state under a custom name
    const string stateName = "GS0";

    // Ensure we don’t clash with an existing entry
    if (extGStateDict.ContainsKey(stateName))
        extGStateDict.Remove(stateName);

    extGStateDict.Add(stateName, newGraphicsState);
```

ตอนนี้ resource ของหน้ารู้จัก `GS0` แล้ว. เพื่อใช้งานจริง คุณต้องอ้างอิง graphics state นี้ใน content stream ผ่าน operator `gs` (เช่น `GS0 gs`). Aspose.Pdf อนุญาตให้คุณแทรก PDF operators ดิบหากต้องการวาดรูปแบบกำหนดเอง

## Step 6: Save the modified PDF

```csharp
    // Persist the changes to a new file
    pdfDocument.Save(outputPath);
}
```

ไฟล์ `output.pdf` ที่ได้จะมีเนื้อหาเดียวกับต้นฉบับ, แต่คำสั่งการวาดใด ๆ ที่เลือก `GS0` จะเคารพการตั้งค่าความโปร่งใสที่คุณกำหนด

### Expected result

เปิด `output.pdf` ด้วย Adobe Acrobat หรือโปรแกรมดู PDF ใด ๆ หากคุณเพิ่มเส้นใหม่ที่ใช้ graphics state `GS0` (เช่น ผ่าน `pdfDocument.Pages[1].Contents.Add(...)`), เส้นนั้นจะปรากฏเป็นกึ่งโปร่งใสในขณะที่การเติมยังคงทึบ นี่แสดงว่าคุณได้ทำ **add graphics state pdf** และ **modify PDF transparency** สำเร็จแล้ว

---

## Full runnable example

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอก‑วางลงในแอปพลิเคชันคอนโซล มันรวมการโหลดไลเซนส์, การจัดการข้อผิดพลาด, และคอมเมนต์อธิบายแต่ละขั้นตอนที่ไม่ชัดเจน



## What Should You Learn Next?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [Add Transparency to PDF with Aspose PDF in C# – Step‑by‑Step Guide](/pdf/english/net/images-graphics/add-transparency-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Add Transparency to PDF using Aspose – Complete C# Guide](/pdf/english/net/programming-with-operators/add-transparency-to-pdf-using-aspose-complete-c-guide/)
- [How to Add an Image Stamp to a PDF Using Aspose.PDF for .NET: A Comprehensive Guide](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}