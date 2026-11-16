---
category: general
date: 2026-11-16
description: วิธีตั้งค่าความโปร่งใสใน PDF ด้วย Aspose.Pdf โดยการแก้ไขทรัพยากร PDF
  และการโหลด PDF อย่างมีประสิทธิภาพ ตามคู่มือ C# ฉบับเต็มนี้
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set transparency
- edit pdf resources
- load pdf aspose
language: th
lastmod: 2026-11-16
og_description: วิธีตั้งค่าความโปร่งใสใน PDF ด้วย Aspose.Pdf เพื่อควบคุมความทึบของกราฟิกอย่างแม่นยำโดยตรงจาก
  C#
og_image_alt: C# code snippet that sets PDF transparency via Aspose.Pdf
og_title: ตั้งค่าความโปร่งใสของ PDF ด้วย Aspose.Pdf – คู่มือ C# ทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to set transparency in a PDF with Aspose.Pdf by editing PDF resources
    and loading the PDF efficiently. Follow this complete C# guide.
  headline: How to set transparency in a PDF using Aspose.Pdf
  type: TechArticle
- description: How to set transparency in a PDF with Aspose.Pdf by editing PDF resources
    and loading the PDF efficiently. Follow this complete C# guide.
  name: How to set transparency in a PDF using Aspose.Pdf
  steps:
  - name: '**Load the PDF** with Aspose.Pdf (`load pdf aspose`).'
    text: '**Load the PDF** with Aspose.Pdf (`load pdf aspose`).'
  - name: '**Access the first page’s resources** dictionary (`edit pdf resources`).'
    text: '**Access the first page’s resources** dictionary (`edit pdf resources`).'
  - name: '**Create a custom ExtGState** that contains the desired transparency values.'
    text: '**Create a custom ExtGState** that contains the desired transparency values.'
  - name: '**Insert the ExtGState** back into the page resources.'
    text: '**Insert the ExtGState** back into the page resources.'
  - name: '**Save the modified PDF**.'
    text: '**Save the modified PDF**.'
  type: HowTo
tags:
- PDF
- Aspose.Pdf
- C#
title: วิธีตั้งค่าความโปร่งใสใน PDF ด้วย Aspose.Pdf
url: /th/net/images-graphics/how-to-set-transparency-in-a-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีตั้งค่าความโปร่งใสใน PDF ด้วย Aspose.Pdf

หากคุณต้องการ **วิธีตั้งค่าความโปร่งใส** ในเอกสาร PDF บทแนะนำนี้จะแสดงขั้นตอนที่แน่นอนด้วย Aspose.Pdf สำหรับ .NET ไม่ว่าคุณจะกำลังสร้างเครื่องมือรายงานหรือเพิ่มลายน้ำ การควบคุมความทึบเป็นความต้องการทั่วไป เมื่อจบคู่มือคุณจะได้โปรแกรม C# ที่สามารถรันได้ซึ่งโหลด PDF แก้ไขทรัพยากรของมันและบันทึกผลลัพธ์กลับไปยังดิสก์

การทำงานกับ PDF มักหมายความว่าคุณต้อง **แก้ไขทรัพยากร PDF** เช่นพจนานุกรม ExtGState และคุณยังต้อง **โหลด PDF ด้วย Aspose** อย่างถูกต้องเพื่อหลีกเลี่ยงผลลัพธ์ที่เสียหาย คู่มือนี้ครอบคลุมทั้งสองประเด็นและอธิบายว่าทำไมแต่ละการดำเนินการจึงสำคัญ เพื่อให้คุณสามารถปรับรูปแบบนี้ให้เข้ากับเอกสารหลายหน้า หรือสถานะกราฟิกแบบกำหนดเองได้

## วิธีตั้งค่าความโปร่งใสใน PDF – ภาพรวม

ความโปร่งใสใน PDF ถูกกำหนดโดยอ็อบเจ็กต์ *ExtGState* (external graphics state) วัตถุนี้เก็บพารามิเตอร์เช่น ความทึบของเส้น (`CA`), ความทึบของการเติม (`ca`), และโหมดการผสม (`BM`). Aspose.Pdf ให้คุณจัดการพจนานุกรมเหล่านี้โดยตรง ทำให้คุณควบคุมได้ละเอียดโดยไม่ต้องพึ่งพา API ระดับสูง

ขั้นตอนโดยรวมคือ:

1. **โหลด PDF** ด้วย Aspose.Pdf (`load pdf aspose`).
2. **เข้าถึงพจนานุกรมทรัพยากรของหน้าแรก** (`edit pdf resources`).
3. **สร้าง ExtGState แบบกำหนดเอง** ที่มีค่าความโปร่งใสที่ต้องการ.
4. **แทรก ExtGState** กลับเข้าไปในทรัพยากรของหน้า.
5. **บันทึก PDF ที่แก้ไขแล้ว**.

แต่ละขั้นตอนถูกดำเนินการในเมธอด C# ที่กระชับ และซอร์สโค้ดเต็มจะปรากฏที่ส่วนท้ายของบทความ

## ขั้นตอนที่ 1: โหลด PDF ด้วย Aspose.Pdf (`load pdf aspose`)

ก่อนที่คุณจะสามารถแก้ไขอะไรได้ คุณต้องเปิดไฟล์โดยใช้คลาส `Document` ของ Aspose คำสั่ง `using` รับประกันว่าการจัดการไฟล์จะถูกปล่อยออกแม้เกิดข้อยกเว้น

```csharp
// Step 1: Load the PDF document
using (var pdfDocument = new Aspose.Pdf.Document("YOUR_DIRECTORY/input.pdf"))
{
    // All subsequent operations happen inside this block.
}
```

**ทำไมสิ่งนี้ถึงสำคัญ:**  
Aspose.Pdf จะทำการแยกโครงสร้าง PDF ไปเป็นโมเดลอ็อบเจ็กต์ การโหลดเอกสารเพียงครั้งเดียวและเก็บไว้ในหน่วยความจำช่วยหลีกเลี่ยงการทำ I/O ซ้ำและรับประกันว่าการเปลี่ยนแปลงใด ๆ ที่คุณทำจะถูกนำไปใช้กับอินสแตนซ์เดียวกัน

**เคล็ดลับ:** หาก PDF ต้นฉบับถูกป้องกันด้วยรหัสผ่าน ให้ส่งรหัสผ่านไปยังคอนสตรัคเตอร์ของ `Document`:

```csharp
var pdfDocument = new Aspose.Pdf.Document("input.pdf", new LoadOptions { Password = "mySecret" });
```

## ขั้นตอนที่ 2: เข้าถึงพจนานุกรมทรัพยากรของหน้า (`edit pdf resources`)

ทุกหน้าของ PDF มีพจนานุกรม *Resources* ที่เก็บฟอนต์, รูปภาพ, และสถานะกราฟิก เพื่อเพิ่ม ExtGState ใหม่ ให้ดึงพจนานุกรมนี้และรับพจนานุกรมย่อย `ExtGState` ที่มีอยู่ (หรือสร้างใหม่หากไม่มีอยู่)

```csharp
// Step 2: Access the first page's resources dictionary
var firstPage = pdfDocument.Pages[1];                     // Aspose uses 1‑based indexing
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);

// Ensure the ExtGState entry exists; if not, create an empty dictionary.
if (!resourcesEditor.ContainsKey("ExtGState"))
{
    resourcesEditor["ExtGState"] = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
}
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

**ทำไมสิ่งนี้ถึงสำคัญ:**  
พจนานุกรม `Resources` เป็นที่เดียวที่เรนเดอร์ PDF มองหาการกำหนดสถานะกราฟิก หากไม่มีรายการ `ExtGState` หน้า PDF จะละเลยการตั้งค่าความทึบใด ๆ ที่คุณอ้างอิงต่อมา

**กรณีขอบ:** PDF บางไฟล์มีพจนานุกรม `ExtGState` อยู่แล้วพร้อมหลายรายการ ในกรณีนั้นคุณสามารถใช้พจนานุกรมที่มีอยู่ซ้ำได้ตามที่แสดงข้างต้น เพื่อหลีกเลี่ยงการเขียนทับสถานะที่ไม่เกี่ยวข้อง

## ขั้นตอนที่ 3: กำหนดพารามิเตอร์ความโปร่งใส

ความโปร่งใสถูกควบคุมโดยสามคีย์:

| Key | ความหมาย | ช่วงทั่วไป |
|-----|----------|-----------|
| `CA` | ความทึบของเส้น | 0 (โปร่งใส) … 1 (ทึบ) |
| `ca` | ความทึบของการเติม | 0 … 1 |
| `BM` | โหมดการผสม | `"Normal"`, `"Multiply"`, เป็นต้น |

สร้าง `CosPdfDictionary` ใหม่และใส่ค่าที่ต้องการลงไป

```csharp
// Step 3: Create a new ExtGState dictionary with desired entries
var customExtGState = Aspose.Pdf.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var graphicsStateParameters = new[]
{
    // Stroke opacity = 1 (fully opaque)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("CA",
        new Aspose.Pdf.CosPdfNumber(1)),
    // Fill opacity = 0.5 (50% transparent)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("ca",
        new Aspose.Pdf.CosPdfNumber(0.5)),
    // Blend mode = Normal (standard source‑over composition)
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>("BM",
        new Aspose.Pdf.CosPdfName("Normal"))
};

foreach (var param in graphicsStateParameters)
    customExtGState.Add(param);
```

**ทำไมสิ่งนี้ถึงสำคัญ:**  
การตั้งค่า `ca` เป็น `0.5` ทำให้รูปทรงที่เติมใด ๆ (เช่นสี่เหลี่ยมหรือข้อความ) แสดงเป็นกึ่งโปร่งใส คุณสามารถปรับตัวเลขเหล่านี้เพื่อให้ได้เอฟเฟกต์ภาพที่ต้องการ โหมดการผสมกำหนดว่าคอนเทนต์โปร่งใสจะผสมกับกราฟิกพื้นหลังอย่างไร; `"Normal"` เป็นตัวเลือกที่พบบ่อยที่สุด

**เคล็ดลับพิเศษ:** หากคุณต้องการโหมดการผสมอื่น ให้เปลี่ยน `"Normal"` เป็น `"Multiply"` หรือ `"Screen"` เพื่อให้ได้เอฟเฟกต์ศิลปะ เช่น ทำให้เนื้อหาพื้นหลังมืดลงหรือสว่างขึ้น

## ขั้นตอนที่ 4: แทรก ExtGState แบบกำหนดเองลงในทรัพยากรของหน้า

ตอนนี้ผูกพจนานุกรมกับชื่อ (เช่น `GS0`) และเพิ่มลงในคอลเลกชัน `ExtGState` ของหน้า

```csharp
// Step 4: Add the custom ExtGState entry to the page resources
extGStateDict.Add("GS0", customExtGState);
```

**ทำไมสิ่งนี้ถึงสำคัญ:**  
ชื่อ (`GS0`) จะถูกอ้างอิงโดยตัวดำเนินการกราฟิกในสตรีมเนื้อหาในภายหลัง หากคุณตั้งใจใช้สถานะนี้บนหลายหน้า คุณสามารถใช้ชื่อเดียวกันซ้ำหรือสร้างชื่อเฉพาะหน้าต่าง ๆ (`GS1`, `GS2`, …).

**รูปแบบขั้นสูง:** เพื่อใช้สถานะนี้กับสตรีมเนื้อหาที่มีอยู่ คุณอาจใส่ตัวดำเนินการ PDF `q /GS0 gs` ไว้หน้าคำสั่งวาด Aspose.Pdf มี `PdfContentEditor` สำหรับจุดประสงค์นั้น แต่เกินขอบเขตของบทแนะนำพื้นฐานนี้

## ขั้นตอนที่ 5: บันทึก PDF ที่แก้ไขแล้ว

สุดท้าย ให้บันทึกการเปลี่ยนแปลงลงในไฟล์ใหม่ การเก็บไฟล์ต้นฉบับไว้ไม่เปลี่ยนแปลงทำให้เปรียบเทียบผลลัพธ์ก่อนและหลังได้ง่าย

```csharp
// Step 5: Save the modified PDF
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

**การตรวจสอบ:** เปิด `output.pdf` ด้วยโปรแกรมดู PDF ใด ๆ รูปทรงที่เติมและใช้สถานะกราฟิกแบบกำหนดเอง (เช่นสี่เหลี่ยมที่วาดด้วย `GS0`) จะปรากฏที่ความทึบ 50 % หากคุณไม่เห็นการเปลี่ยนแปลง ให้ตรวจสอบอีกครั้งว่าสตรีมเนื้อหาจริง ๆ อ้างอิง `GS0` หรือไม่ คุณสามารถแทรกสี่เหลี่ยมทดสอบโดยใช้ `PdfContentEditor` เป็นการตรวจสอบเสริมได้

## ตัวอย่างการทำงานเต็มรูปแบบ

การรวมทุกขั้นตอนเข้าด้วยกันจะได้โปรแกรมที่เป็นอิสระซึ่งคุณสามารถคัดลอกและวางลงในแอปพลิเคชันคอนโซลได้

```csharp
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Operators;

class Program
{
    static void Main()
    {
        // Load the PDF (load pdf aspose)
        using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
        {
            // Access first page resources (edit pdf resources)
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);
            if (!resourcesEditor.ContainsKey("ExtGState"))
                resourcesEditor["ExtGState"] = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // Create custom ExtGState with transparency
            var customExtGState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var parameters = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };
            foreach (var p in parameters) customExtGState.Add(p);
            extGStateDict.Add("GS0", customExtGState);

            // OPTIONAL: Apply the graphics state to a sample rectangle
            // This demonstrates that the transparency works.
            var canvas = new Aspose.Pdf.PageEditor(firstPage);
            canvas.AddRectangle(100, 500, 200, 600); // left, bottom, right, top
            // Set the graphics state before drawing
            canvas.ContentStream.Operators.Insert(0, new SetGraphicsState("GS0"));
            canvas.Save();

            // Save the modified PDF
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
        }

        System.Console.WriteLine("Transparency applied successfully.");
    }
}
```

**คำอธิบายของบล็อกเสริม:**  
`PageEditor` เพิ่มสี่เหลี่ยมง่าย ๆ ลงในหน้าและตั้งค่าสถานะกราฟิกเป็น `GS0` อย่างชัดเจน ขั้นตอนนี้มีประโยชน์สำหรับการทดสอบ; ในสถานการณ์จริงคุณจะมีเนื้อหาที่อ้างอิงสถานะนี้อยู่แล้ว

## ทั่วไป

## สิ่งที่คุณควรเรียนต่อไปคืออะไร?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบอื่นในโครงการของคุณ

- [วิธีเพิ่ม graphics state ใน pdf และควบคุมความโปร่งใสด้วย Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)
- [วิธีเพิ่มความโปร่งใสให้ PDF ด้วย Aspose.PDF ใน C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [วิธีเปลี่ยนความโปร่งใสของ PDF ด้วย Aspose.Pdf ใน C#](/pdf/english/net/programming-with-operators/how-to-change-pdf-transparency-using-aspose-pdf-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}