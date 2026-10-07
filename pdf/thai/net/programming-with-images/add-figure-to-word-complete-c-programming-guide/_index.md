---
category: general
date: 2026-04-12
description: เพิ่มรูปภาพลงใน Word อย่างรวดเร็วด้วย C# เรียนรู้วิธีกำหนดตำแหน่งรูปภาพใน
  Word, แทรกรูปภาพลงในไฟล์ docx, และเพิ่ม XML ที่กำหนดเองสำหรับการจัดวางขั้นสูง.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: th
og_description: เพิ่มรูปภาพใน Word อย่างรวดเร็วด้วย C# เรียนรู้วิธีจัดตำแหน่งรูปภาพใน
  Word, แทรกรูปภาพลงในไฟล์ docx, และเพิ่ม XML กำหนดเองสำหรับการจัดวางขั้นสูง.
og_title: เพิ่มรูปภาพใน Word – คู่มือการเขียนโปรแกรม C# ฉบับสมบูรณ์
tags:
- C#
- Word Automation
- Document Generation
title: เพิ่มรูปภาพลงใน Word – คู่มือการเขียนโปรแกรม C# อย่างครบถ้วน
url: /th/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มรูปภาพใน Word – คู่มือการเขียนโปรแกรม C# ฉบับสมบูรณ์

เคยต้อง **เพิ่มรูปภาพใน Word** แต่ไม่รู้จะเริ่มจากตรงไหนหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการอัตโนมัติของ Office สิ่งที่ขาดคือรูปภาพหรือแผนภูมิที่วางไว้ในตำแหน่งที่เหมาะสมซึ่งอยู่ภายใน custom XML part คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่า **วางรูปภาพใน Word อย่างไร**, แทรกรูปภาพลงในไฟล์ *.docx* และแม้กระทั่งปรับแต่ง custom XML ด้านล่างเพื่อให้รูปภาพทำงานเหมือนวัตถุ Word ธรรมดา

เราจะเดินผ่านตัวอย่างจริงโดยใช้ไลบรารี GemBox.Document (ใช้ฟรีสำหรับไฟล์ขนาดเล็ก, มีเวอร์ชันเชิงพาณิชย์สำหรับงานที่ใหญ่กว่า) เมื่อเสร็จคุณจะได้โปรแกรมที่ทำงานได้เองซึ่งวางรูปภาพที่พิกัด X = 50, Y = 200 ภายใน container ที่มีแท็กเนื้อหา ไม่ใช่การอ้างอิง “ดูเอกสาร” แบบคลุมเครือ—แต่เป็นโค้ดที่ชัดเจน, ทำไมถึงทำงาน, และเคล็ดลับที่คุณสามารถคัดลอกไปใช้ในโปรเจกต์ของคุณได้ทันที

## ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังคอมไพล์ได้กับ .NET Core 3.1)
- **GemBox.Document** NuGet package (`Install-Package GemBox.Document`)
- ไฟล์ Word เริ่มต้น (`input.docx`) ที่มี custom XML tag อยู่แล้วในตำแหน่งที่คุณต้องการให้รูปภาพปรากฏ
- ความรู้พื้นฐานของ C# (คุณจะเห็นว่าทำไมแต่ละบรรทัดจึงสำคัญ)

> **เคล็ดลับระดับมืออาชีพ:** หากคุณไม่มีเอกสารที่มีแท็กไว้ล่วงหน้า คุณสามารถสร้างได้ใน Word โดยใส่ *Content Control* → *XML Mapping Pane* → แมป custom XML part ไลบรารีจะถือคอนโทรลนั้นเป็น `TaggedContent`

## ขั้นตอนที่ 1 – โหลดเอกสารต้นฉบับ

สิ่งแรกที่เราทำคือเปิดไฟล์ *.docx* ที่มีอยู่ `Document` เป็นจุดเริ่มต้นสำหรับการทำงานทั้งหมดของ GemBox

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*ทำไมต้องทำเช่นนี้?* การโหลดไฟล์ทำให้เราสามารถเข้าถึงส่วนภายในของมัน รวมถึง custom XML containers หากไม่มีขั้นตอนนี้ เราจะไม่สามารถหาน็อด `TaggedContent` ที่จะเก็บรูปภาพของเราได้

## ขั้นตอนที่ 2 – เข้าถึง Tagged Content (Custom XML Container)

Custom XML จะถูกเก็บไว้ภายใน *content control* ใน Word GemBox จะเปิดให้เข้าถึงเป็น `TaggedContent`

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

หากเอกสารมีหลายส่วนที่มีแท็ก `TaggedContent` จะคืนค่า **แรก** ที่พบ คุณยังสามารถวนลูป `doc.TaggedContents` เพื่อเลือกแท็กตามชื่อได้อีกด้วย

## ขั้นตอนที่ 3 – สร้าง Figure Element

`FigureElement` แทนภาพ, แผนภูมิ หรือวัตถุภาพใด ๆ ที่ Word ถือเป็น *shape* เราจะสร้างมันภายใน container ที่มีแท็ก

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*ทำไมต้องสร้างรูปที่นี่?* การผูกรูปกับน็อด custom XML ทำให้ Word รู้ว่ารูปเป็นส่วนของส่วนตรรกะนั้น ซึ่งสำคัญสำหรับการแก้ไขภายหลังหรือเวิร์กโฟลว์ที่อิง content‑control

## ขั้นตอนที่ 4 – กำหนดตำแหน่งรูปอย่างแม่นยำ

Word ใช้หน่วย point (1 pt ≈ 1/72 in) สำหรับการกำหนดตำแหน่ง `PointF` struct ช่วยให้เราตั้งค่า X/Y ได้ง่าย

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **วิธีกำหนดตำแหน่ง shape word:** คุณสมบัติ `Position` รับค่า `PointF` โดยค่าตัวแรกคือการเลื่อนแนวนอน (ซ้าย) และค่าที่สองคือการเลื่อนแนวตั้ง (บน) เทียบกับขอบกระดาษ ปรับค่าตัวเลขเหล่านี้เพื่อทำการจัดตำแหน่งให้ละเอียดขึ้น

## ขั้นตอนที่ 5 – แทรกรูปลงในต้นไม้ Tagged Content

ตอนนี้เราจะผูกรูปเข้ากับ root element ของ custom XML tree ซึ่งจะทำให้ shape ปรากฏในเอกสาร Word

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

ในขั้นตอนนี้รูปยังไม่มีแหล่งที่มาของภาพ เราจะเพิ่ม PNG อย่างง่ายจากดิสก์

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## ขั้นตอนที่ 6 – บันทึกเอกสารที่แก้ไขแล้ว

สุดท้ายเราจะเขียนการเปลี่ยนแปลงกลับไปยังไฟล์ *.docx* ใหม่

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

เมื่อคุณเปิด `output.docx` ใน Word คุณจะเห็นภาพที่วางอยู่ที่พิกัด (50, 200) ภายในบล็อก custom‑XML ที่คุณระบุ

### ตัวอย่างทำงานเต็มรูปแบบ

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** การเปิด `output.docx` จะเห็น PNG อยู่ตรงตำแหน่งที่คุณกำหนดไว้ และซ้อนอยู่ภายใน custom XML part หากคุณเปิด XML ของเอกสาร (`.docx` → unzip → `word/document.xml`) จะพบ `<w:pict>` ที่มี `<v:shape>` พร้อมพิกัดที่ถูกต้อง

## คำถามที่พบบ่อย & กรณีขอบ

### ถ้าเอกสารมีหลายส่วนที่มีแท็กจะทำอย่างไร?

ใช้ `doc.TaggedContents` เพื่อวนลูปและเลือกตามชื่อแท็ก:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### วิธีเพิ่ม caption ให้รูปคืออะไร?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### ทำงานได้กับ Word 2010 ขึ้นไปหรือไม่?

ได้ครับ GemBox.Document รองรับมาตรฐาน Open XML ซึ่งเข้ากันได้กับ Word 2007 + (รวมถึง 2010, 2013, 2016, 2019, และ Microsoft 365)

### ถ้าต้องการหมุน shape จะทำอย่างไร?

```csharp
figure.Rotation = 45; // degrees
```

### วิธีเพิ่มกราฟิกแบบเวกเตอร์แทนภาพราสเตอร์คืออะไร?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## เคล็ดลับระดับมืออาชีพ & สิ่งที่ควรระวัง

- **เส้นทางไฟล์:** ใช้ `Path.Combine` เพื่อหลีกเลี่ยงการเขียนตัวคั่นแบบฮาร์ดโค้ด โดยเฉพาะบนแพลตฟอร์มที่ไม่ใช่ Windows
- **ขีดจำกัดไลเซนส์:** ไลเซนส์ฟรีของ GemBox จำกัดขนาดเอกสารที่ 20 KB หากไฟล์ใหญ่กว่านี้ต้องซื้อคีย์เชิงพาณิชย์
- **ประสิทธิภาพ:** การใช้ `Document` ตัวเดียวสำหรับการประมวลผลเป็นชุดช่วยลดการใช้หน่วยความจำอย่างมาก
- **Shape overflow:** หากขนาดของรูปเกินขอบกระดาษ Word จะตัดส่วนที่เกินออก ปรับ `figure.Width` และ `figure.Height` ให้เหมาะสม

## สรุป

ตอนนี้คุณรู้แล้วว่า **จะเพิ่มรูปภาพใน Word อย่างไร**, **กำหนดตำแหน่งรูปใน Word อย่างแม่นยำ**, และจัดการกับ custom XML ด้านล่างเพื่อให้ shape ทำงานเหมือนองค์ประกอบพื้นฐานของ Word ตัวอย่างเต็มที่สามารถรันได้แสดงทุกขั้นตอน—from การโหลดเอกสาร, การสร้าง `FigureElement`, การตั้งค่าพิกัด, การแนบภาพ, และการบันทึกไฟล์ *.docx* ที่อัปเดต

ต่อไปลองทดลอง **insert figure into docx** ด้วยการเพิ่มหลายรูป, ใช้ลูป, หรือสร้างแผนภูมิแบบไดนามิก คุณอาจสนใจ **how to add custom xml** เพื่อควบคุม content control ที่ซับซ้อนขึ้น หรือ **how to position shape word** ในตารางและส่วนหัวของเอกสาร ความเป็นไปได้ไม่มีที่สิ้นสุด และด้วยพื้นฐานที่ครอบคลุมนี้ คุณพร้อมที่จะทำอัตโนมัติเอกสาร Word อย่างมืออาชีพแล้ว

ขอให้สนุกกับการเขียนโค้ด และอย่าลังเลที่จะคอมเมนต์หากเจออุปสรรคใด ๆ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}