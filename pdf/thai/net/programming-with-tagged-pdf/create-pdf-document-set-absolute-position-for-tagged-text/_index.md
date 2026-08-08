---
category: general
date: 2026-03-24
description: สร้างเอกสาร PDF และเรียนรู้วิธีกำหนดตำแหน่งแน่นอนสำหรับข้อความที่มีแท็ก
  การสอนนี้จะแสดงวิธีเพิ่มองค์ประกอบ span, วิธีเพิ่มเนื้อหาที่มีแท็ก และการวางตำแหน่งข้อความบนหน้า.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: th
og_description: สร้างเอกสาร PDF และดูทันทีว่าตั้งตำแหน่งแบบสัมบูรณ์, เพิ่มองค์ประกอบ
  span, และจัดตำแหน่งข้อความบนหน้าอย่างไรด้วยเนื้อหา PDF ที่มีแท็ก
og_title: สร้างเอกสาร PDF – การจัดตำแหน่งแบบคงที่ของข้อความที่มีแท็ก
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: สร้างเอกสาร PDF – กำหนดตำแหน่งแน่นอนสำหรับข้อความที่มีแท็ก
url: /th/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้างเอกสาร PDF – ตั้งค่าตำแหน่งแน่นอนสำหรับข้อความที่มีแท็ก

เคยต้องการ **สร้างเอกสาร pdf** ที่มีข้อความที่เข้าถึงได้และมีแท็กซึ่งตั้งตำแหน่งตรงตามที่คุณต้องการหรือไม่? บางทีคุณอาจกำลังสร้าง PDF แบบฟอร์มที่ป้ายกำกับต้องอยู่ที่พิกัดที่แม่นยำ, หรือคุณกำลังสร้างใบรับรองและต้องการให้ชื่อจัดตำแหน่งให้ตรงกับภาพพื้นหลังอย่างสมบูรณ์แบบ.

ในคู่มือนี้เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์และสามารถรันได้ ซึ่งแสดง **วิธีเพิ่มเนื้อหาที่มีแท็ก**, **ตั้งค่าตำแหน่งแน่นอน**, และ **เพิ่มองค์ประกอบ span** เพื่อให้คุณ **วางข้อความบนหน้า** ได้โดยไม่ต้องเดา ไม่มีการอ้างอิงภายนอก—เพียงโค้ดที่คุณสามารถคัดลอก‑วางได้ พร้อมคำอธิบาย “ทำไม” ของแต่ละบรรทัด.

## ข้อกำหนดเบื้องต้น

- .NET 6+ (หรือ .NET Framework 4.6+) พร้อมคอมไพเลอร์ C#
- Aspose.Pdf for .NET (เวอร์ชันล่าสุด ณ เวลาที่เขียน, 23.12) ติดตั้งผ่าน NuGet
- ความคุ้นเคยพื้นฐานกับไวยากรณ์ C#

หากคุณมีทั้งหมดนี้แล้ว, มาเริ่มกันเลย.

---

## สร้างเอกสาร PDF – ตั้งค่าตำแหน่งแน่นอน

สิ่งแรกที่เราทำคือสร้างอินสแตนซ์ของ `Document` ว่างเปล่า วัตถุนี้แทนไฟล์ PDF ทั้งหมดและให้เราเข้าถึงต้นไม้ของเนื้อหาที่มีแท็กได้

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**ทำไมเรื่องนี้ถึงสำคัญ:**  
`Document` คือรากของโครงสร้าง PDF การสร้างมันก่อนทำให้เรามีผ้าใบสำหรับทั้งองค์ประกอบภาพ (หน้า, กราฟิก) และโครงสร้างเชิงตรรกะ (แท็ก) คำสั่ง `using` รับประกันว่าไฟล์จะถูกทำลายอย่างถูกต้อง ซึ่งป้องกันการรั่วของไฟล์แฮนด์เดิลบน Windows.

## เปิดใช้งานเนื้อหาที่มีแท็ก (วิธีเพิ่มแท็ก)

ก่อนที่เราจะใส่องค์ประกอบที่มีแท็กใด ๆ เอกสารต้องถูกทำเครื่องหมายว่า *มีแท็ก* Aspose.Pdf จะสร้างอ็อบเจกต์ `TaggedContent` โดยอัตโนมัติ แต่คุณยังต้องเปิดสวิตช์นี้

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**อะไรเกิดขึ้นภายใน?**  
การตั้งค่า `TaggedContent` เป็น `true` บอกผู้อ่าน PDF ว่าไฟล์นี้มีต้นไม้โครงสร้างเชิงตรรกะ ซึ่งสำคัญต่อโปรแกรมอ่านหน้าจอและทำให้เมธอด `SetPosition` ทำงานได้อย่างถูกต้องบนองค์ประกอบ span.

## ดึงองค์ประกอบรากของต้นไม้เนื้อหาที่มีแท็ก

องค์ประกอบรากเป็นจุดเริ่มต้นสำหรับแท็กโครงสร้างทั้งหมด (เช่น `<Document>`, `<Section>`, `<Span>`) คิดว่าเป็น “body” ที่มองไม่เห็นของ PDF.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**ทำไมเราต้องการราก:**  
แท็กทั้งหมดที่ตามมาต้องถูกแนบไว้ที่ใดที่หนึ่งในต้นไม้ มิฉะนั้นจะไม่ปรากฏในลำดับชั้นการเข้าถึง.

## เพิ่มองค์ประกอบ Span – บล็อกสร้างข้อความในบรรทัดเดียว

*span* คือสิ่งที่เทียบเท่ากับ HTML `<span>` ใน PDF—เหมาะสำหรับข้อความสั้น ๆ ที่คุณต้องการวางตำแหน่งอย่างแม่นยำ.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**หมายเหตุการออกแบบ:**  
หากคุณต้องการรูปแบบที่ซับซ้อนขึ้น (ตัวหนา, ตัวเอียง, ลิงก์) คุณสามารถห่อ span ด้วย `<Paragraph>` หรือใช้วัตถุ `TextFragment` ต่อไป สำหรับการกำหนดตำแหน่งแน่นอน span ธรรมดาจะเบาที่สุด.

## ตั้งค่าตำแหน่งแน่นอน – X=100, Y=200

ต่อไปคือส่วนที่สนุก: วาง span ที่ตำแหน่งที่แน่นอนบนหน้า ระบบพิกัดเริ่มจากมุมซ้ายล่าง (0,0) และใช้หน่วยเป็นพอยต์ (1 pt ≈ 1/72 in).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**ทำไมต้องใช้การกำหนดตำแหน่งแน่นอน?**  
เมื่อคุณต้องการการจัดวางที่พิกเซล‑พอร์เฟ็คท์—เช่น ใบรับรอง, ใบแจ้งหนี้, หรือแบบฟอร์ม—การไหลแบบสัมพันธ์ (เช่น ข้อความจากซ้ายไปขวา) ไม่เพียงพอ `SetPosition` ข้ามการไหลของข้อความปกติและตรึงองค์ประกอบไว้ที่ตำแหน่งที่คุณระบุ.

## เพิ่มข้อความลงใน Span

เมื่อ span ถูกวางตำแหน่งแล้ว เราจะใส่สตริงจริงลงไป

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**เคล็ดลับ:**  
หากคุณต้องการอักขระ Unicode หรือสคริปต์จากขวาไปซ้าย เพียงส่งสตริงนั้น; Aspose.Pdf จะจัดการการเข้ารหัสโดยอัตโนมัติ.

## แนบ Span ไปยังองค์ประกอบราก

สุดท้าย เราแนบ span ไปยังต้นไม้เชิงตรรกะของเอกสารเพื่อให้มันเป็นส่วนหนึ่งของ PDF สุดท้าย.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**ถ้าคุณลืมขั้นตอนนี้จะเป็นอย่างไร?**  
span จะอยู่ในหน่วยความจำแต่ไม่ถูกจัดเก็บลงไฟล์ ดังนั้นคุณจะไม่เห็นข้อความและต้นไม้การเข้าถึงจะไม่สมบูรณ์.

## ตัวอย่างสมบูรณ์ที่สามารถรันได้

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถวางในแอปคอนโซลได้ มันสร้าง PDF หนึ่งหน้า, เพิ่ม span ที่มีแท็กที่ตำแหน่ง (100, 200), และบันทึกไฟล์เป็น `TaggedPositioned.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:**  
เปิด `TaggedPositioned.pdf` ในโปรแกรมดูใด ๆ (Adobe Acrobat, Foxit ฯลฯ) คุณจะเห็นวลี **“Positioned tagged text”** อยู่ห่างจากขอบซ้าย 100 pt และจากขอบล่าง 200 pt ของหน้า หากคุณตรวจสอบแผง *Tags* จะพบองค์ประกอบ `<Span>` อยู่ภายใต้รากของเอกสาร ยืนยันว่าข้อความถูกแท็กอย่างถูกต้อง.

## คำถามทั่วไป & กรณีขอบ

### ถ้าฉันต้องการวางข้อความบนหน้าที่เฉพาะที่ไม่ใช่หน้าแรก?

เพิ่มหน้าที่คุณต้องการ (`var page = pdfDocument.Pages[3];`) ก่อนเรียก `SetPosition` Span จะถูกแนบโดยอัตโนมัติไปยังบริบทของหน้าที่ใช้งาน.

### ฉันสามารถตั้งค่าตำแหน่งเป็นนิ้วหรือเซนติเมตรได้หรือไม่?

`SetPosition` รับค่าหน่วยเป็นพอยต์ แปลงโดยใช้สูตร:  
- **นิ้ว → พอยต์:** `points = inches * 72`  
- **เซนติเมตร → พอยต์:** `points = cm * 28.3465`

### ฉันจะเปลี่ยนฟอนต์หรือสีของ span ได้อย่างไร?

หลังจากสร้าง span แล้ว คุณสามารถดึง `TextState` ของมันและแก้ไขได้:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### ถ้าเอกสารถูกแท็กไว้แล้วจะทำอย่างไร?

คุณยังสามารถสร้าง span ใหม่และแนบไปยังองค์ประกอบที่มีอยู่ (`rootElement`, `<Section>` เฉพาะ ฯลฯ) เพียงตรวจสอบให้คงลำดับโครงสร้างเชิงตรรกะ—โปรแกรมอ่านหน้าจอคาดหวังต้นไม้ที่มีโครงสร้างดี.

### วิธีนี้ทำงานกับการปฏิบัติตาม PDF/A หรือ PDF/UA หรือไม่?

ใช่. PDF ที่มีแท็กเป็นข้อกำหนดหลักสำหรับ PDF/UA หากต้องการ PDF/A ให้ตั้งค่า `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` หลังจากสร้างเนื้อหา.

## เคล็ดลับระดับมืออาชีพ & สิ่งที่ต้องระวัง

- **เคล็ดลับระดับมืออาชีพ:** ควรเพิ่มหน้าเสมอก่อนวางเนื้อหา หากไม่มีหน้า `SetPosition` จะล้มเหลวโดยไม่มีข้อความแจ้ง เพราะไม่มีที่ให้เรนเดอร์.
- **ระวังหน่วย:** การผสมพิกเซลจากการออกแบบ UI กับพอยต์ของ PDF จะทำให้ข้อความอยู่ผิดตำแหน่ง ตรวจสอบการแปลงของคุณสองครั้ง.
- **คำแนะนำด้านประสิทธิภาพ:** หากคุณสร้าง PDF จำนวนหลายพันไฟล์ ควรใช้ `Document` ตัวเดียวซ้ำและเรียก `pdfDocument.Pages.Clear()` ระหว่างการรันเพื่อหลีกเลี่ยงการจัดสรรหน่วยความจำมากเกินไป.
- **เตือนเรื่องการเข้าถึง:** การแท็กไม่ใช่แค่สิ่งที่ดีเท่านั้น; หลายกฎระเบียบ (Section 508, EN 301 549) กำหนดให้ทำเช่นนั้น การใช้ `CreateSpanElement` ทำให้ข้อความสามารถค้นพบโดยเทคโนโลยีช่วยเหลือได้.

## สรุป

เราเพิ่ง **สร้างเอกสาร pdf** ตั้งแต่ต้น, **ตั้งค่าตำแหน่งแน่นอน**, **เพิ่มองค์ประกอบ span**, และสาธิต **วิธีเพิ่มเนื้อหาที่มีแท็ก** เพื่อให้คุณ **วางข้อความบนหน้า** ด้วยความแม่นยำระดับพิกเซล ตัวอย่างเต็มพร้อมรันแล้วและคำอธิบายครอบคลุมทั้ง *วิธีทำ* และ *เหตุผล*—สิ่งที่นักพัฒนา (และผู้ช่วย AI) มองหาเมื่อจำเป็นต้องมีโซลูชันที่เชื่อถือได้.

ต่อไปคุณอาจสำรวจ:

- การเพิ่มรูปภาพไว้ด้านหลังข้อความที่วางเพื่อทำใบรับรองที่มีลายน้ำ.  
- การใช้ `CreateParagraphElement` สำหรับบล็อกหลายบรรทัดที่ยังต้องการการวางตำแหน่งแน่นอน.  
- การส่งออกเป็น PDF/UA เพื่อตอบสนองการตรวจสอบการเข้าถึงที่เข้มงวด.  

อย่าลังเลที่จะแก้ไขพิกัด, ฟอนต์ หรือสี—การทดลองคือวิธีที่เร็วที่สุดในการเชี่ยวชาญการสร้าง PDF ที่มีแท็ก หากคุณเจอปัญหาใด ๆ แคะแสดงความคิดเห็นด้านล่าง; โค้ดดิ้งให้สนุก!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}