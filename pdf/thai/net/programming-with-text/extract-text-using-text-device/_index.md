---
"description": "เรียนรู้วิธีแยกข้อความจากเอกสาร PDF โดยใช้ Text Device ใน Aspose.PDF สำหรับ .NET"
"linktitle": "การแยกข้อความโดยใช้ Text Device"
"second_title": "เอกสารอ้างอิง Aspose.PDF สำหรับ API ของ .NET"
"title": "การแยกข้อความโดยใช้ Text Device"
"url": "/th/net/programming-with-text/extract-text-using-text-device/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การแยกข้อความโดยใช้ Text Device

## การแนะนำ

การแยกข้อความจาก PDF อาจเป็นเรื่องยุ่งยาก โดยเฉพาะเมื่อต้องจัดการกับเอกสารที่มีรูปแบบต่างๆ ฟอนต์ฝังไว้ หรือเค้าโครงที่ซับซ้อน แต่ด้วย Aspose.PDF สำหรับ .NET กระบวนการนี้จะกลายเป็นเรื่องง่ายดาย! ไม่ว่าคุณต้องการแปลงหน้าของ PDF เป็นข้อความธรรมดาเพื่อวิเคราะห์เพิ่มเติมหรือเพียงแค่ต้องการแยกส่วนเฉพาะ Aspose.PDF ก็ช่วยคุณได้ ในบทช่วยสอนนี้ เราจะอธิบายทีละขั้นตอนถึงวิธีแยกข้อความจาก PDF โดยใช้คลาส TextDevice ใน Aspose.PDF นอกจากนี้ เรายังให้คำอธิบายที่ชัดเจนด้วย ดังนั้น คุณจึงสามารถนำวิธีการเดียวกันไปใช้กับโปรเจ็กต์ของคุณเองได้อย่างง่ายดาย

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มต้นเขียนโค้ด ให้แน่ใจว่าคุณมีทุกอย่างพร้อมแล้ว ต่อไปนี้คือสิ่งที่คุณต้องมี:

1. Aspose.PDF สำหรับ .NET: ดาวน์โหลดเวอร์ชันล่าสุดจาก [หน้าดาวน์โหลด Aspose.PDF สำหรับ .NET](https://releases-aspose.com/pdf/net/).
2. สภาพแวดล้อมการพัฒนา: Visual Studio หรือสภาพแวดล้อมการพัฒนา C# อื่นๆ
3. .NET Framework: ตรวจสอบให้แน่ใจว่าโครงการของคุณกำหนดเป้าหมายเป็น .NET Framework 4.x หรือสูงกว่า
4. อินพุตไฟล์ PDF: ไฟล์ PDF ที่คุณจะใช้สำหรับการแยกข้อความ วางไฟล์นี้ไว้ในไดเร็กทอรีบนเครื่องของคุณ (เราจะเรียกไฟล์นี้ว่า `YOUR DOCUMENT DIRECTORY`-

## แพ็คเกจนำเข้า

ที่ด้านบนของโค้ดของคุณ คุณจะต้องนำเข้าเนมสเปซที่จำเป็นสำหรับการทำงานกับ Aspose.PDF:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Devices;
using System;
using System.Text;
```

## ขั้นตอนที่ 1: โหลดเอกสาร PDF ของคุณ

ก่อนที่จะแยกข้อความ เราจะต้องโหลดเอกสาร PDF ลงในหน่วยความจำ ในขั้นตอนนี้ คุณจะเปิด PDF โดยใช้ Aspose.PDF `Document` คลาสนี้จะช่วยให้คุณสามารถเข้าถึงหน้าและเนื้อหาทั้งหมดภายในไฟล์ได้

```csharp
// กำหนดเส้นทางไปยังเอกสาร PDF ของคุณ
string dataDir = "YOUR DOCUMENT DIRECTORY";

// โหลดเอกสาร PDF
Document pdfDocument = new Document(dataDir + "input.pdf");
```

ที่นี่เราใช้ `Document pdfDocument = new Document(dataDir + "input.pdf");` เพื่อโหลดไฟล์ PDF `dataDir` ตัวแปรจะเก็บเส้นทางไดเรกทอรีของไฟล์ PDF ของคุณ ซึ่งจะทำให้เราเข้าถึงเอกสารทั้งหมดได้ ทำให้เราวนซ้ำหน้าต่างๆ และแยกเนื้อหาออกมาได้

## ขั้นตอนที่ 2: ตั้งค่าตัวสร้างสตริงสำหรับการจัดเก็บข้อความ

ตอนนี้เมื่อโหลดเอกสารเสร็จแล้ว เราต้องหาวิธีจัดเก็บข้อความที่แยกออกมา สำหรับสิ่งนี้ เราจะใช้ `StringBuilder` ซึ่งช่วยให้สามารถเรียงสตริงได้อย่างมีประสิทธิภาพ

```csharp
// StringBuilder เพื่อเก็บข้อความที่แยกออกมา
StringBuilder builder = new StringBuilder();
```

เราเริ่มต้น `StringBuilder` อินสแตนซ์ที่จะรวบรวมข้อความที่แยกออกมาจากแต่ละหน้า เป็นวิธีที่มีประสิทธิภาพมากกว่าในการจัดการสตริงขนาดใหญ่เมื่อเทียบกับการต่อสตริงปกติในลูป

## ขั้นตอนที่ 3: วนซ้ำหน้า PDF

ต่อไป เราจะวนซ้ำผ่านแต่ละหน้าของเอกสาร PDF เพื่อแยกข้อความออกมา เราจะประมวลผลแต่ละหน้าทีละหน้าโดยใช้ `TextDevice` คลาสซึ่งรับผิดชอบการแปลงเนื้อหา PDF เป็นรูปแบบข้อความ

```csharp
// วนซ้ำผ่านหน้าทั้งหมดใน PDF
foreach (Page pdfPage in pdfDocument.Pages)
{
    // ประมวลผลแต่ละหน้าสำหรับการดึงข้อความ
}
```

ลูปนี้จะผ่านทุกหน้าของ PDF (`pdfDocument.Pages`). สำหรับแต่ละหน้าเราจะแยกข้อความและเพิ่มลงใน `StringBuilder`-

## ขั้นตอนที่ 4: ดึงข้อความจากแต่ละหน้า

ตอนนี้เราตั้งค่ากระบวนการแยกข้อความสำหรับแต่ละหน้าแล้ว ที่นี่เราจะสร้าง `TextDevice` วัตถุและใช้ในการประมวลผลหน้า PDF `TextDevice` แยกข้อความดิบหรือจัดรูปแบบตามตัวเลือกการแยกที่เราตั้งค่าไว้

```csharp
using (MemoryStream textStream = new MemoryStream())
{
    // สร้างอุปกรณ์ข้อความสำหรับการแยกข้อความ
    TextDevice textDevice = new TextDevice();
    
    // ตั้งค่าตัวเลือกการแยกข้อความเป็นโหมด 'บริสุทธิ์'
    TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);
    textDevice.ExtractionOptions = textExtOptions;

    // ดึงข้อความจากหน้าปัจจุบันและบันทึกลงในสตรีมหน่วยความจำ
    textDevice.Process(pdfPage, textStream);

    // แปลงสตรีมหน่วยความจำเป็นข้อความ
    string extractedText = Encoding.Unicode.GetString(textStream.ToArray());

    // ผนวกข้อความที่แยกออกมาไปยัง StringBuilder
    builder.Append(extractedText);
}
```

- `TextDevice textDevice = new TextDevice();`: เดอะ `TextDevice` คลาสนี้ใช้เพื่อแยกข้อความจาก PDF
- `TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);`:ตัวเลือกนี้จะแยกข้อความดิบโดยไม่คงการจัดรูปแบบใดๆ เช่น แบบอักษรหรือตำแหน่ง คุณยังสามารถใช้ `TextFormattingMode.Raw` หากคุณต้องการควบคุมการจัดรูปแบบเพิ่มเติม
- `textDevice.Process(pdfPage, textStream);`:กระบวนการนี้จะประมวลผลแต่ละหน้าของ PDF และจัดเก็บข้อความที่แยกออกมาใน `MemoryStream`-
- สุดท้ายเราแปลงข้อความจาก `MemoryStream` เป็นสตริงแล้วผนวกเข้า `StringBuilder`-

## ขั้นตอนที่ 5: บันทึกข้อความที่แยกออกมาลงในไฟล์

หลังจากประมวลผลหน้าทั้งหมดแล้ว ข้อความจะถูกเก็บไว้ใน `StringBuilder`ขั้นตอนสุดท้ายคือการบันทึกข้อความที่แยกออกมาลงในไฟล์

```csharp
// กำหนดเส้นทางเอาท์พุตสำหรับไฟล์ข้อความ
dataDir = dataDir + "input_Text_Extracted_out.txt";

// บันทึกข้อความที่แยกออกมาลงในไฟล์
File.WriteAllText(dataDir, builder.ToString());

Console.WriteLine("\nText extracted successfully from PDF document.\nFile saved at " + dataDir);
```

- `File.WriteAllText(dataDir, builder.ToString());`:นี่คือการเขียนเนื้อหาทั้งหมดของ `StringBuilder` ลงในไฟล์ข้อความ
- เส้นทางสำหรับไฟล์เอาท์พุตจะถูกตั้งค่าโดยการผนวกชื่อไฟล์ (`"input_Text_Extracted_out.txt"`) ถึง `dataDir` เส้นทาง.

## บทสรุป

การแยกข้อความจาก PDF โดยใช้ Aspose.PDF สำหรับ .NET เป็นกระบวนการที่เรียบง่ายและมีประสิทธิภาพ โดยทำตามขั้นตอนที่ระบุไว้ในคู่มือนี้ คุณสามารถเปิดเอกสาร PDF วนซ้ำหน้าต่างๆ และแยกข้อความลงในไฟล์ข้อความได้อย่างง่ายดาย ซึ่งมีประโยชน์อย่างยิ่งสำหรับการประมวลผลข้อมูล PDF จำนวนมาก การวิเคราะห์ข้อความ หรือการแปลงเอกสารเพื่อการจัดการเพิ่มเติม

ด้วย Aspose.PDF คุณจะไม่ถูกจำกัดอยู่แค่การแยกข้อความเท่านั้น แต่คุณสามารถจัดการคำอธิบายประกอบ ปรับแต่งรูปภาพ หรือแม้แต่แปลง PDF เป็นรูปแบบอื่น เช่น HTML หรือ Word ความยืดหยุ่นและประสิทธิภาพของไลบรารีนี้ทำให้เป็นเครื่องมืออันล้ำค่าสำหรับการจัดการ PDF ในแอปพลิเคชัน .NET

## คำถามที่พบบ่อย

### Aspose.PDF สามารถดึงข้อความจาก PDF ที่ใช้รูปภาพได้หรือไม่
ไม่ Aspose.PDF ถูกออกแบบมาเพื่อแยกข้อความจาก PDF ที่เน้นเนื้อหา สำหรับ PDF ที่เน้นรูปภาพ จำเป็นต้องใช้เทคโนโลยี OCR

### Aspose.PDF ยังคงรูปแบบเดิมไว้เมื่อแยกข้อความหรือไม่
ตามค่าเริ่มต้น ข้อความจะถูกแยกออกโดยไม่จัดรูปแบบ แต่คุณสามารถปรับเปลี่ยนตัวเลือกการแยกออกได้หากคุณต้องการคงการจัดรูปแบบบางอย่างไว้

### ฉันสามารถแยกข้อความจากช่วงหน้าเฉพาะได้หรือไม่
ใช่ คุณสามารถปรับเปลี่ยนโค้ดเพื่อวนซ้ำในช่วงหน้าที่กำหนดแทนที่จะวนซ้ำทุกหน้าได้

### โหมดการแยกข้อความใน Aspose.PDF คืออะไร
Aspose.PDF มีสองโหมด: Raw และ Pure โหมด Raw จะพยายามรักษาเค้าโครงเดิมเอาไว้ ในขณะที่โหมด Pure จะแยกเฉพาะข้อความโดยไม่จัดรูปแบบ

### Aspose.PDF สำหรับ .NET เข้ากันได้กับ .NET Core หรือไม่
ใช่ Aspose.PDF สำหรับ .NET เข้ากันได้อย่างสมบูรณ์กับ .NET Core และ .NET Framework

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}