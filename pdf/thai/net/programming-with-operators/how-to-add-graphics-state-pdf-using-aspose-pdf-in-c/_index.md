---
category: general
date: 2026-09-28
description: เรียนรู้วิธีเพิ่มกราฟิกสเตต PDF ด้วย Aspose.PDF ใน C# คู่มือขั้นตอนต่อขั้นตอนนี้จะแสดงวิธีตั้งค่าความทึบแสงและโหมดผสมสำหรับหน้า
  PDF
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add graphics state pdf
- Aspose PDF graphics state
- PDF opacity settings
- modify PDF resources
- Aspose.Pdf DictionaryEditor
language: th
lastmod: 2026-09-28
og_description: เพิ่มสถานะกราฟิก PDF โดยใช้ Aspose.PDF ใน C# ทำตามคำแนะนำนี้เพื่อเปลี่ยนความทึบของเส้น/การเติมและโหมดการผสมบนหน้า
  PDF ใด ๆ.
og_image_alt: Screenshot of a PDF page after adding graphics state pdf with opacity
  settings
og_title: เพิ่มสถานะกราฟิก PDF ด้วย Aspose.PDF – คู่มือ C# ฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-09-28'
  description: Learn how to add graphics state pdf with Aspose.PDF in C#. This step‑by‑step
    guide shows you how to set opacity and blend mode for PDF pages.
  headline: How to add graphics state pdf using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: วิธีเพิ่มสถานะกราฟิก PDF ด้วย Aspose.PDF ใน C#
url: /th/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเพิ่ม graphics state pdf ด้วย Aspose.PDF ใน C#

หากคุณต้องการ **add graphics state pdf** เพื่อควบคุมความทึบแสงหรือโหมดการผสมสี คู่มือนี้จะแสดงให้คุณเห็นขั้นตอนอย่างละเอียด ด้วย Aspose.PDF คุณสามารถแก้ไข resource dictionary ของหน้าและแทรก graphics state ที่กำหนดเองได้เพียงไม่กี่บรรทัดของโค้ด

คุณจะได้เรียนรู้วิธีโหลด PDF, สร้าง graphics state dictionary ใหม่, ตั้งค่า stroke opacity, fill opacity, และ blend mode, แล้วบันทึกเอกสารที่แก้ไขแล้ว ไม่ต้องใช้เครื่องมือภายนอก—เพียงแค่ไลบรารี Aspose.PDF for .NET

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มทำงาน ให้แน่ใจว่าคุณมี:

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Core 3.1 และ .NET Framework 4.7+)
* ไลเซนส์ที่ถูกต้องสำหรับ **Aspose.PDF for .NET** (รุ่นทดลองฟรีใช้สำหรับการประเมิน)
* ไฟล์ PDF อินพุต (`input.pdf`) ที่วางไว้ในโฟลเดอร์ที่รู้จัก
* Visual Studio 2022 หรือโปรแกรมแก้ไข C# ใด ๆ ที่คุณชอบ

> **เคล็ดลับ:** เก็บไฟล์ PDF ของคุณไว้ไน่นอกโฟลเดอร์โปรเจกต์เพื่อหลีกเลี่ยงการคอมมิตไฟล์ไบนารีขนาดใหญ่โดยบังเอิญ

## ขั้นตอนที่ 1: ติดตั้งแพคเกจ NuGet ของ Aspose.PDF

เปิดเทอร์มินัลในไดเรกทอรีโปรเจกต์ของคุณและรัน:

```bash
dotnet add package Aspose.Pdf
```

แพคเกจนี้มี namespace `Aspose.Pdf` ซึ่งให้คลาส `Document`, `DictionaryEditor`, และ `CosPdfDictionary` ที่จะใช้ต่อไป

## ขั้นตอนที่ 2: โหลดเอกสาร PDF

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Path to the source PDF
string pdfPath = @"C:\MyPdfs\input.pdf";

// The `using` statement ensures the document is disposed automatically
using var pdfDocument = new Document(pdfPath);
```

*ทำไมขั้นตอนนี้สำคัญ*: การโหลด PDF จะสร้างการแสดงผลในหน่วยความจำที่คุณสามารถจัดการได้ วัตถุ `Document` ให้คุณเข้าถึงหน้า, resources, และวัตถุ COS ระดับต่ำที่จำเป็นสำหรับ **add graphics state pdf**

## ขั้นตอนที่ 3: เข้าถึง resources ของหน้าแรก

```csharp
// Get the first page (pages are 1‑based in Aspose.PDF)
Page firstPage = pdfDocument.Pages[1];

// Create a DictionaryEditor to work with the page’s resource dictionary
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

Dictionary `Resources` เก็บอ็อบเจกต์เช่นฟอนต์, รูปภาพ, และรายการ **ExtGState** การแก้ไขมันเป็นวิธีเดียวที่ปลอดภัยในการ **modify PDF resources**

## ขั้นตอนที่ 4: ดึง (หรือสร้าง) ExtGState dictionary

```csharp
// Try to get the existing ExtGState dictionary; if it does not exist, create one
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*ทำไมขั้นตอนนี้สำคัญ*: รายการ `ExtGState` เก็บ graphics state objects หาก PDF มีอยู่แล้วเราจะใช้ซ้ำ; หากไม่มีเราจะสร้าง dictionary ใหม่เพื่อให้การ **add graphics state pdf** ไม่ล้มเหลว

## ขั้นตอนที่ 5: สร้าง graphics state dictionary ใหม่

```csharp
// Create an empty dictionary that will hold our graphics state parameters
CosPdfDictionary graphicsStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1.0 means fully opaque strokes
graphicsStateDict.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes filled shapes 50 % transparent
graphicsStateDict.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default PDF blend mode
graphicsStateDict.Add("BM", new CosPdfName("Normal"));
```

คีย์ `CA`, `ca`, และ `BM` ถูกกำหนดโดยสเปค PDF การตั้งค่าพวกนี้ทำให้คุณควบคุม **PDF opacity settings** และพฤติกรรมการผสมสีสำหรับคำสั่งการวาดต่อไป

## ขั้นตอนที่ 6: ลงทะเบียน graphics state ใหม่ใน ExtGState

```csharp
// Choose a unique name for the graphics state, e.g., GS0
extGStateDict.Add("GS0", graphicsStateDict);
```

ตอนนี้ resource dictionary ของหน้ามีรายการใหม่ชื่อ `GS0` เมื่อคุณอ้างอิง `GS0` ใน content stream, ตัวดู PDF จะใช้ความทึบแสงและ blend mode ที่คุณกำหนด

## ขั้นตอนที่ 7: (ทางเลือก) ใช้ graphics state กับเนื้อหาเดิม

หากต้องการแก้ไขคำสั่งการวาดที่มีอยู่แล้ว คุณต้องแก้ไข content stream ของหน้า ตัวอย่างง่าย ๆ ด้านล่างจะ prepend ตัวดำเนินการ `gs` เพื่อกำหนด graphics state ก่อนการวาดใด ๆ เกิดขึ้น:

```csharp
// Retrieve the page’s content stream as a string
string originalContent = firstPage.Contents[1].ToString();

// Prepend the graphics state operator
string updatedContent = "GS0 gs\n" + originalContent;

// Replace the page content with the updated stream
firstPage.Contents[1].Replace(updatedContent);
```

> **หมายเหตุ:** การจัดการ content stream โดยตรงอาจทำให้เกิดความละเอียดอ่อน ควรทดสอบบนสำเนา PDF ก่อนเสมอ

## ขั้นตอนที่ 8: บันทึก PDF ที่แก้ไขแล้ว

```csharp
string outputPath = @"C:\MyPdfs\output.pdf";
pdfDocument.Save(outputPath);
```

หลังจากบันทึกแล้ว เปิด `output.pdf` ด้วยโปรแกรมดู PDF ใด ๆ รูปทรงที่เติมสีหลังจากตัวดำเนินการ `GS0 gs` จะปรากฏด้วยความทึบแสง 50 % ส่วนเส้นขอบยังคงทึบเต็มที่ แสดงว่าคุณได้ **add graphics state pdf** สำเร็จแล้ว

### ผลลัพธ์ที่คาดหวัง

| ก่อน | หลัง (พร้อม GS0) |
|--------|------------------|
| ![Before PDF page](placeholder-before.png){.img-fluid alt="หน้าต้นฉบับ PDF"} | ![After PDF page](placeholder-after.png){.img-fluid alt="หน้าตัว PDF หลังจากเพิ่ม graphics state pdf พร้อมการตั้งค่าความทึบแสง"} |

คอลัมน์ “หลัง” แสดงการเติมสีแบบกึ่งโปร่งใสในขณะที่เส้นขอบยังคงทึบเต็มตามที่กำหนดใน graphics state dictionary

## คำถามที่พบบ่อย & กรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| **ฉันสามารถเพิ่มหลาย graphics states ได้หรือไม่?** | ได้ เพียงเพิ่มรายการเพิ่มเติม (`GS1`, `GS2`, …) ไปยัง `extGStateDict` แล้วอ้างอิงชื่อที่ต้องการใน content stream |
| **ถ้า PDF มีชื่อ `GS0` อยู่แล้วจะทำอย่างไร?** | เลือกตัวระบุที่ไม่ซ้ำ (เช่น `GS_custom1`) คุณสามารถตรวจสอบ `extGStateDict.Keys` ก่อนเพิ่มได้ |
| **วิธีนี้ทำงานกับ PDF ที่เข้ารหัสหรือไม่?** | PDF ต้องเปิดด้วยรหัสผ่านที่ถูกต้อง ใช้ `new Document(pdfPath, new LoadOptions { Password = "secret" })` |
| **Blend mode จำกัดแค่ “Normal” หรือไม่?** | ไม่ สเปค PDF รองรับหลาย blend mode (`Multiply`, `Screen`, `Overlay`, ฯลฯ) แทนที่ `"Normal"` ด้วยชื่อที่รองรับ |
| **การเปลี่ยนแปลงนี้จะส่งผลต่อหน้าที่อื่นหรือไม่?** | มีผลเฉพาะหน้าที่คุณแก้ไข resources หากต้องการใช้สถานะเดียวกันหลายหน้า ให้ทำซ้ำขั้นตอน 3‑6 สำหรับแต่ละหน้า หรือแก้ไข resources ระดับเอกสารโดยรวม |

## สรุป

คุณได้เรียนรู้วิธี **add graphics state pdf** ด้วย Aspose.PDF for .NET ตั้งค่าความทึบของเส้นและเติมสี เลือก blend mode และ (ตามต้องการ) ใช้สถานะนี้กับเนื้อหาเดิม เทคนิคนี้ให้คุณควบคุมการเรนเดอร์ PDF อย่างละเอียดโดยไม่ต้องแปลงไฟล์เป็นรูปภาพ

ต่อไปคุณอาจสำรวจ:

* **PDF opacity settings** สำหรับรูปภาพและบล็อกข้อความ
* การใช้ **Aspose.Pdf DictionaryEditor** เพื่อแทนที่ฟอนต์หรือฝัง ICC profile แบบกำหนดเอง
* การรวมหลาย graphics states เพื่อสร้างเอฟเฟกต์ภาพที่ซับซ้อน

อย่ากลัวทดลองค่าความทึบต่าง ๆ, blend mode ต่าง ๆ, และขอบเขตของ resource การจัดการ PDF ระดับล่างเหล่านี้จะเปิดประตูสู่การสร้างเอกสารและการลบข้อมูลอย่างชาญฉลาด

---


## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [How to Add Stamp to PDF with Aspose.Pdf – Step‑by‑Step Guide](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-stamp-to-pdf-with-aspose-pdf-step-by-step-guide/)
- [How to Add Images to PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/images-graphics/add-images-to-pdfs-aspose-pdf-net/)
- [How to Remove Graphics from PDFs Using Aspose.PDF .NET&#58; A Complete Guide](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}