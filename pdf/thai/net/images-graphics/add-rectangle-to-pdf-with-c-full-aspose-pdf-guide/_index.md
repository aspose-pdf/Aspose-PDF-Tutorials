---
category: general
date: 2026-04-06
description: เพิ่มสี่เหลี่ยมผืนผ้าใน PDF อย่างรวดเร็วด้วย C# เรียนรู้การวาดสี่เหลี่ยมผืนผ้าใน
  PDF, โหลดเอกสาร PDF ด้วย C# และใช้ Aspose PDF วาดสี่เหลี่ยมผืนผ้าในบทแนะนำแบบขั้นตอนต่อขั้นตอนนี้.
draft: false
keywords:
- add rectangle to pdf
- draw rectangle on pdf
- draw shape in pdf
- load pdf document c#
- aspose pdf draw rectangle
language: th
og_description: เพิ่มสี่เหลี่ยมผืนผ้าใน PDF อย่างทันที คู่มือนี้แสดงวิธีวาดสี่เหลี่ยมผืนผ้าใน
  PDF, โหลดเอกสาร PDF ด้วย C#, และใช้ Aspose PDF วาดสี่เหลี่ยมผืนผ้าพร้อมตัวอย่างโค้ดที่ชัดเจน.
og_title: เพิ่มสี่เหลี่ยมผืนผ้าใน PDF ด้วย C# – บทเรียน Aspose PDF ฉบับสมบูรณ์
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: เพิ่มสี่เหลี่ยมผืนผ้าใน PDF ด้วย C# – คู่มือ Aspose PDF ฉบับเต็ม
url: /th/net/images-graphics/add-rectangle-to-pdf-with-c-full-aspose-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มสี่เหลี่ยมผืนผ้าใน PDF – คู่มือ Aspose PDF ฉบับสมบูรณ์

เคยต้องการ **add rectangle to PDF** แต่ไม่แน่ใจว่า API ใดทำงานได้? คุณไม่ได้เป็นคนเดียว; นักพัฒนาหลายคนเจอปัญหาเดียวกันเมื่อต้องอัตโนมัติรายงานหรือไฮไลท์ส่วนในเอกสาร ในคู่มือนี้เราจะอธิบายขั้นตอนที่แน่นอนเพื่อ **draw rectangle on PDF** ด้วย Aspose.PDF สำหรับ .NET และคุณจะได้เห็นตัวอย่างเต็มที่สามารถรันได้ซึ่งคุณสามารถนำไปใช้ในโปรเจคของคุณ

เราจะอธิบายวิธี **load PDF document C#**, ตรวจสอบว่ารูปร่างพอดีกับหน้า และพูดถึงข้อผิดพลาดทั่วไปบางอย่างเมื่อคุณพยายาม **draw shape in PDF**. เมื่อจบคุณจะมีโปรแกรมทำงานที่เพิ่มสี่เหลี่ยมสีเหลืองสดใสลงในหน้าแรกของ PDF ใด ๆ ที่คุณระบุ

## สิ่งที่คุณต้องการ

- .NET 6.0 หรือใหม่กว่า (โค้ดทำงานกับ .NET Framework 4.6+ ด้วย)
- Aspose.PDF for .NET NuGet package (เวอร์ชัน 23.11 หรือใหม่กว่า)
- ตัวอย่างไฟล์ PDF (`input.pdf`) ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้
- Visual Studio, VS Code หรือ IDE C# ใด ๆ ที่คุณชอบ

ไม่มีไฟล์การกำหนดค่าเพิ่มเติม, ไม่มี COM interop, เพียงไม่กี่คำสั่ง `using` และบรรทัดของตรรกะไม่กี่บรรทัด

## ขั้นตอนที่ 1: Load PDF Document C# – เตรียมไฟล์ให้พร้อม

สิ่งแรกที่คุณต้องทำคือเปิด PDF ที่มีอยู่เพื่อให้คุณมีพื้นผิวสำหรับวาด. Aspose.PDF ทำให้ขั้นตอนนี้เป็นบรรทัดเดียว

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color

// Step 1: Load the PDF document
var inputPath = @"C:\MyPdfs\input.pdf";
using var pdfDocument = new Document(inputPath);
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
`Document` แทนไฟล์ PDF ทั้งไฟล์. การใส่ไว้ในบล็อก `using` ทำให้แน่ใจว่า handle ของไฟล์จะถูกปล่อยทันทีที่เสร็จ, ป้องกันปัญหาไฟล์ล็อกบน Windows. หากลืมใช้ `using`, คุณอาจเจอข้อความ “cannot access the file because it is being used by another process” เมื่อพยายามบันทึก

## ขั้นตอนที่ 2: Access the Target Page and Verify Bounds – วาดรูปร่างใน PDF อย่างปลอดภัย

ก่อนที่คุณจะวางสี่เหลี่ยมบนหน้า, คุณต้องการอ็อบเจ็กต์หน้าและควรตรวจสอบว่าสี่เหลี่ยมพอดีกับมิติของหน้า. สิ่งนี้ป้องกันข้อยกเว้นขณะรันและทำให้ PDF ของคุณดูเป็นระเบียบ

```csharp
// Step 2: Get the first page (pages are 1‑based in Aspose)
Page firstPage = pdfDocument.Pages[1];

// Define rectangle bounds: lower‑left X/Y and upper‑right X/Y
var rectangleBounds = new Rectangle(50, 700, 200, 800);

// Verify the rectangle is inside the page limits
bool fits = rectangleBounds.LLX >= 0 &&
            rectangleBounds.URX <= firstPage.PageInfo.Width &&
            rectangleBounds.LLY >= 0 &&
            rectangleBounds.URY <= firstPage.PageInfo.Height;

if (!fits)
{
    throw new InvalidOperationException("Rectangle exceeds page dimensions.");
}
```

**คำอธิบาย:**  
คอนสตรัคเตอร์ `Rectangle` ต้องการตัวเลขสี่ค่า: X ซ้าย‑ล่าง, Y ซ้าย‑ล่าง, X ขวา‑บน, Y ขวา‑บน. ค่าต่าง ๆ นี้วัดเป็น points (1 pt ≈ 1/72 in). ขั้นตอนการตรวจสอบเป็นเครือข่ายความปลอดภัยเล็ก ๆ — มีประโยชน์โดยเฉพาะเมื่อคำนวณพิกัดแบบไดนามิก (เช่น จากขนาดภาพหรือความยาวข้อความ).

## ขั้นตอนที่ 3: Add Rectangle to PDF – แกนหลักของ “Add Rectangle to PDF”

ตอนนี้เป็นส่วนที่สนุก: การแทรกรูปร่างจริง ๆ. Aspose.PDF มีคลาส `RectangleShape` ที่คุณสามารถใส่ลงในคอลเลกชัน `Paragraphs` ของหน้า

```csharp
// Step 3: Add a yellow rectangle shape
var rectangleShape = new RectangleShape(rectangleBounds)
{
    FillColor = Color.Yellow,
    Border = new BorderInfo(BorderSide.All, 1.0f, Color.Black) // Optional: thin black border
};

firstPage.Paragraphs.Add(rectangleShape);
```

**ทำไมต้องใช้ `RectangleShape`?**  
มันเป็นกราฟิกเวกเตอร์, ดังนั้นสี่เหลี่ยมจะปรับขนาดได้อย่างเรียบบนอุปกรณ์ใดก็ได้. การเพิ่มลงใน `Paragraphs` ทำให้มันทำงานเหมือนองค์ประกอบเนื้อหาอื่น ๆ — ตั้งตำแหน่งสัมพันธ์กับหน้า, ไม่ใช่กับข้อความที่มีอยู่. หากต้องการเติมสีโปร่งใส, เพียงตั้งค่า `FillColor = Color.Transparent`.

> **เคล็ดลับ:** เปลี่ยน `FillColor` เป็น `Color.FromArgb(128, 255, 255, 0)` เพื่อให้เป็นสีเหลืองกึ่งโปร่งใสที่ทำให้ข้อความด้านล่างมองเห็นได้.

## ขั้นตอนที่ 4: Save the Updated PDF – สรุปวงจร “Add Rectangle to PDF”

เมื่อรูปร่างถูกวางไว้แล้ว, คุณเพียงบันทึกเอกสารเป็นไฟล์ใหม่ (หรือเขียนทับไฟล์เดิม, หากคุณต้องการ)

```csharp
// Step 4: Save the updated PDF
var outputPath = @"C:\MyPdfs\output.pdf";
pdfDocument.Save(outputPath);
```

เท่านี้! เปิด `output.pdf` แล้วคุณจะเห็นสี่เหลี่ยมสีเหลืองสดใสที่วางอย่างพอดีระหว่างพิกัดที่คุณกำหนด

## ตัวอย่างทำงานเต็มรูปแบบ – ทุกขั้นตอนในไฟล์เดียว

ด้านล่างเป็นโปรแกรมครบวงจรที่คุณสามารถคอมไพล์และรันได้ทันที. มันรวมการจัดการข้อผิดพลาดและคอมเมนต์ที่อธิบายแต่ละบรรทัด

```csharp
// ---------------------------------------------------------------
// AddRectangleToPdf.cs
// Demonstrates how to add rectangle to PDF using Aspose.PDF for .NET
// ---------------------------------------------------------------
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

class AddRectangleToPdf
{
    static void Main()
    {
        // ----- 1. Load the PDF document -----
        string inputPath = @"C:\MyPdfs\input.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        using var pdfDoc = new Document(inputPath);

        // ----- 2. Access first page and define rectangle bounds -----
        Page page = pdfDoc.Pages[1];
        var rect = new Rectangle(50, 700, 200, 800);

        // Verify rectangle fits the page
        bool fits = rect.LLX >= 0 && rect.URX <= page.PageInfo.Width &&
                    rect.LLY >= 0 && rect.URY <= page.PageInfo.Height;
        if (!fits)
        {
            Console.WriteLine("Rectangle exceeds page dimensions. Adjust coordinates.");
            return;
        }

        // ----- 3. Create and add rectangle shape -----
        var shape = new RectangleShape(rect)
        {
            FillColor = Color.Yellow,
            Border = new BorderInfo(BorderSide.All, 1.0f, Color.Black)
        };
        page.Paragraphs.Add(shape);

        // ----- 4. Save the modified PDF -----
        string outputPath = @"C:\MyPdfs\output.pdf";
        pdfDoc.Save(outputPath);
        Console.WriteLine($"Rectangle added successfully. Saved to {outputPath}");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  
เมื่อคุณเปิด `output.pdf`, หน้าแรกจะแสดงสี่เหลี่ยมสีเหลืองที่มุมล่างซ้ายเริ่มที่ (50 pt, 700 pt) และมุมบนขวาจบที่ (200 pt, 800 pt). สี่เหลี่ยมจะมีเส้นขอบสีดำบาง ๆ ทำให้มองเห็นชัดเจนบนพื้นหลังส่วนใหญ่

## คำถามทั่วไป & กรณีขอบ

### ถ้าฉันต้องการวาดสี่เหลี่ยมบนหน้าที่แตกต่าง?

เพียงเปลี่ยน `pdfDoc.Pages[1]` เป็นหมายเลขหน้าที่ต้องการ (`pdfDoc.Pages[3]` สำหรับหน้าที่สาม). จำไว้ว่า Aspose ใช้การจัดอันดับเริ่มจาก 1, ไม่ใช่ 0

### ฉันสามารถวาดสี่เหลี่ยมหลาย ๆ รูปในลูปได้หรือไม่?

ได้เลย. ใส่ตรรกะการสร้างสี่เหลี่ยมไว้ใน `foreach` ที่วนผ่านคอลเลกชันของพิกัด. แต่ต้องระวังประสิทธิภาพ; การเพิ่มรูปหลายพันรูปอาจทำให้ขนาดไฟล์เพิ่มขึ้นอย่างชัดเจน

### วิธีนี้แตกต่างจากการใช้ `Graphics` หรือ `System.Drawing` อย่างไร?

`System.Drawing` ทำงานกับภาพแรสเตอร์; ผลลัพธ์จะถูกฝังในบิตแมพ, ซึ่งอาจเบลอเมื่อซูม. `RectangleShape` เป็นเวกเตอร์, หมายความว่าจะคมชัดที่ระดับการซูมใด ๆ — เหมาะสำหรับ PDF ระดับมืออาชีพ

### ถ้า PDF มีการป้องกันด้วยรหัสผ่านจะทำอย่างไร?

โหลดเอกสารด้วยอ็อบเจ็กต์ `PdfLoadOptions` ที่รวมรหัสผ่าน:

```csharp
var loadOpts = new PdfLoadOptions { Password = "mySecret" };
using var pdfDoc = new Document(inputPath, loadOpts);
```

จากนั้นทำตามปกติ. สี่เหลี่ยมจะถูกเพิ่มเมื่อเอกสารถูกถอดรหัสในหน่วยความจำ

## ตัวอย่างภาพอ้างอิง

![ตัวอย่างการเพิ่มสี่เหลี่ยมผืนผ้าใน pdf พร้อมสี่เหลี่ยมสีเหลืองบนหน้าแรก](/images/add-rectangle-to-pdf-example.png)

*ข้อความแทนภาพ: “add rectangle to pdf example with yellow rectangle on first page”*

## สรุป & ขั้นตอนต่อไป

เราเพิ่งอธิบายวิธี **add rectangle to PDF** ด้วย Aspose.PDF สำหรับ .NET, ตั้งแต่การโหลดเอกสารจนถึงการบันทึกไฟล์ที่แก้ไข. สิ่งสำคัญที่ควรจำ:

1. โหลด PDF (`load pdf document c#`) พร้อมการจัดการทรัพยากรอย่างเหมาะสม.
2. กำหนดขอบเขตของสี่เหลี่ยมและตรวจสอบว่าพอดีกับหน้า.
3. ใช้ `RectangleShape` เพื่อ **draw rectangle on pdf** (หรือ **draw shape in pdf** อื่น ๆ ที่คุณอาจต้องการ).
4. บันทึกผลลัพธ์และเพลิดเพลินกับสี่เหลี่ยมเวกเตอร์ที่คมชัด

พร้อมสำหรับต่อหรือยัง? ลองเปลี่ยน `RectangleShape` เป็น `EllipseShape` หรือ `PolygonShape` เพื่อสร้างไฮไลท์แบบกำหนดเอง. หรือสำรวจความสามารถการสกัดข้อความของ Aspose เพื่อกำหนดตำแหน่งรูปร่างแบบไดนามิกตามตำแหน่งคีย์เวิร์ด. ไลบรารีนี้อุดมสมบูรณ์พอที่จะให้คุณสร้างเครื่องมือ anotations เต็มรูปแบบโดยไม่ต้องออกจาก C#.

หากคุณเจอปัญหาใด ๆ, ฝากคอมเมนต์ด้านล่าง—ยินดีช่วยเหลือ. และอย่าลืมกดดาวให้แพคเกจ Aspose.PDF บน NuGet หากคุณพบว่ามีประโยชน์. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}