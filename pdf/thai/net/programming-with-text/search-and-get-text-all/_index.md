---
"description": "เรียนรู้วิธีค้นหาและรับข้อความจากทุกหน้าของเอกสาร PDF โดยใช้ Aspose.PDF สำหรับ .NET"
"linktitle": "ค้นหาและรับข้อความทั้งหมด"
"second_title": "เอกสารอ้างอิง Aspose.PDF สำหรับ API ของ .NET"
"title": "ค้นหาและรับข้อความทั้งหมด"
"url": "/th/net/programming-with-text/search-and-get-text-all/"
"weight": 420
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ค้นหาและรับข้อความทั้งหมด

## การแนะนำ

คุณเคยจำเป็นต้องแยกข้อความเฉพาะจาก PDF แต่พบว่าทำได้ยากหรือไม่ บางครั้ง PDF อาจดูเหมือนคอนเทนเนอร์ที่ถูกล็อค ทำให้ยากต่อการรับข้อมูลที่คุณต้องการ แต่ข่าวดีก็คือ ด้วย Aspose.PDF สำหรับ .NET คุณสามารถค้นหาและเรียกค้นข้อความจาก PDF ได้อย่างง่ายดาย ไลบรารีอันทรงพลังนี้มอบทุกสิ่งที่คุณต้องการเพื่อทำงานกับ PDF ในแอปพลิเคชัน .NET ของคุณ ทำให้การแยกข้อความเป็นเรื่องง่าย ในบทช่วยสอนนี้ เราจะแนะนำคุณเกี่ยวกับกระบวนการค้นหาและแยกข้อความจากไฟล์ PDF โดยใช้ Aspose.PDF สำหรับ .NET ไม่ว่าคุณจะกำลังสร้างเครื่องมือวิเคราะห์ข้อความหรือต้องการเพียงแค่ทำให้การแยกข้อมูลจากรายงาน PDF เป็นไปโดยอัตโนมัติ คุณมาถูกที่แล้ว!

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเริ่มเขียนโค้ด เรามาตรวจสอบก่อนว่าคุณได้ตั้งค่าทุกอย่างเรียบร้อยแล้ว:

1. Aspose.PDF สำหรับ .NET: คุณจะต้องดาวน์โหลดและติดตั้ง Aspose.PDF สำหรับ .NET คุณสามารถรับได้จากหน้าดาวน์โหลด [ที่นี่](https://releases-aspose.com/pdf/net/).
2. สภาพแวดล้อม .NET: ตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่า .NET Framework หรือ .NET Core บนเครื่องพัฒนาของคุณแล้ว
3. ความรู้พื้นฐานเกี่ยวกับ C##: ขอแนะนำให้มีความคุ้นเคยกับ C# และการทำงานกับโปรเจ็กต์ .NET
4. เอกสาร PDF: ไฟล์ PDF ตัวอย่างที่เราจะแยกข้อความออกมา ในตัวอย่างนี้ เราจะใช้ `SearchAndGetTextFromAll-pdf`.

## แพ็คเกจนำเข้า

ก่อนที่จะเขียนโค้ดใดๆ คุณต้องนำเข้าเนมสเปซที่จำเป็นลงในโปรเจ็กต์ของคุณเพื่อทำงานกับ Aspose.PDF

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
```

เนมสเปซเหล่านี้ให้สิทธิ์ในการเข้าถึงโมเดลวัตถุเอกสารของ PDF และช่วยให้เราจัดการข้อความภายในไฟล์ได้

มาแบ่งขั้นตอนออกเป็นขั้นตอนง่าย ๆ เพื่อให้คุณทำตามได้อย่างง่ายดาย

## ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีเอกสาร

ขั้นแรก คุณต้องระบุเส้นทางไปยังไดเร็กทอรีที่ไฟล์ PDF ของคุณตั้งอยู่ วิธีนี้จะช่วยให้แอปพลิเคชันค้นหาไฟล์ที่คุณจะแยกข้อความออกมาได้

```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

- การ `dataDir` ตัวแปรควรชี้ไปที่ไดเร็กทอรีที่คุณ `SearchAndGetTextFromAll.pdf` ไฟล์ถูกเก็บไว้แล้ว
- แทนที่ `"YOUR DOCUMENT DIRECTORY"` ด้วยเส้นทางจริงบนเครื่องของคุณ

## ขั้นตอนที่ 2: เปิดเอกสาร PDF

ต่อไปเราจะเปิดเอกสาร PDF โดยใช้ Aspose.PDF `Document` วัตถุ.

```csharp
// เปิดเอกสาร
Document pdfDocument = new Document(dataDir + "SearchAndGetTextFromAll.pdf");
```

- เราสร้างอินสแตนซ์ใหม่ของ `Document` คลาสโดยการส่งเส้นทางไฟล์แบบเต็มของ PDF
- การดำเนินการนี้จะโหลด PDF เข้าไปในหน่วยความจำ ทำให้พร้อมสำหรับการประมวลผล

## ขั้นตอนที่ 3: สร้าง Text Absorber

การ `TextFragmentAbsorber` วัตถุใช้เพื่อค้นหาข้อความเฉพาะภายใน PDF ในกรณีนี้ เราจะค้นหาคำว่า "ข้อความ"

```csharp
// สร้างวัตถุ TextAbsorber เพื่อค้นหาอินสแตนซ์ทั้งหมดของวลีการค้นหาอินพุต
TextFragmentAbsorber textFragmentAbsorber = new TextFragmentAbsorber("text");
```

- การ `TextFragmentAbsorber` จะถูกเริ่มต้นด้วยสตริง `"text"`ซึ่งหมายความว่าระบบจะค้นหาคำว่า “ข้อความ” ที่เกิดขึ้นในเอกสาร PDF

## ขั้นตอนที่ 4: ยอมรับตัวดูดซับสำหรับทุกหน้า

ตอนนี้เราจะสั่งให้เอกสาร PDF ยอมรับตัวดูดซับและค้นหาข้อความในทุกหน้า

```csharp
// รับตัวดูดซับสำหรับทุกหน้า
pdfDocument.Pages.Accept(textFragmentAbsorber);
```

- การ `Accept` วิธีการนี้ใช้กับหน้าเอกสารทั้งหมด ซึ่งจะค้นหาข้อความที่ระบุในทุกหน้า

## ขั้นตอนที่ 5: แยกชิ้นส่วนข้อความ

เมื่อตัวดูดซับสแกนเอกสารแล้ว เราจะดึงชิ้นส่วนข้อความที่แยกออกมาได้

```csharp
// รับชิ้นส่วนข้อความที่แยกออกมา
TextFragmentCollection textFragmentCollection = textFragmentAbsorber.TextFragments;
```

- การ `TextFragments` ทรัพย์สินของ `TextFragmentAbsorber` ส่งคืนคอลเลกชันของส่วนข้อความทั้งหมดที่ตรงกับเงื่อนไขการค้นหา

## ขั้นตอนที่ 6: วนซ้ำผ่านชิ้นส่วนข้อความ

ตอนนี้เรามีคอลเลกชันของชิ้นส่วนข้อความแล้ว เราจะวนซ้ำผ่านชิ้นส่วนเหล่านั้นและแยกรายละเอียดออกมา

```csharp
// วนผ่านชิ้นส่วน
foreach (TextFragment textFragment in textFragmentCollection)
{
    Console.WriteLine("Text : {0} ", textFragment.Text);
    Console.WriteLine("Position : {0} ", textFragment.Position);
    Console.WriteLine("XIndent : {0} ", textFragment.Position.XIndent);
    Console.WriteLine("YIndent : {0} ", textFragment.Position.YIndent);
    Console.WriteLine("Font - Name : {0}", textFragment.TextState.Font.FontName);
    Console.WriteLine("Font - IsAccessible : {0} ", textFragment.TextState.Font.IsAccessible);
    Console.WriteLine("Font - IsEmbedded : {0} ", textFragment.TextState.Font.IsEmbedded);
    Console.WriteLine("Font - IsSubset : {0} ", textFragment.TextState.Font.IsSubset);
    Console.WriteLine("Font Size : {0} ", textFragment.TextState.FontSize);
    Console.WriteLine("Foreground Color : {0} ", textFragment.TextState.ForegroundColor);
}
```

- การ `foreach` ลูปวนซ้ำผ่านแต่ละ `TextFragment` ในคอลเลคชั่น
- เราจะพิมพ์คุณสมบัติต่างๆ ของแต่ละส่วน เช่น ข้อความจริง ตำแหน่งบนหน้า รายละเอียดแบบอักษร และขนาดแบบอักษร
- การ `XIndent` และ `YIndent` คุณสมบัติให้พิกัดที่แน่นอนของชิ้นส่วนข้อความภายใน PDF

## บทสรุป

และแล้วคุณก็จะได้มัน! ด้วยโค้ดเพียงไม่กี่บรรทัด เราก็สามารถค้นหาและแยกข้อความจาก PDF ได้สำเร็จโดยใช้ Aspose.PDF สำหรับ .NET ความยืดหยุ่นของ Aspose.PDF ช่วยให้คุณสามารถจัดการ PDF ได้หลายวิธี ทำให้เป็นตัวเลือกที่ยอดเยี่ยมสำหรับนักพัฒนาที่ต้องการโซลูชัน PDF ที่แข็งแกร่งในสภาพแวดล้อม .NET คุณสามารถขยายตัวอย่างนี้เพื่อค้นหาคำอื่นๆ แยกรายละเอียดเพิ่มเติม หรือแม้แต่จัดการเนื้อหา PDF ตามความต้องการของคุณได้อย่างง่ายดาย หวังว่าคู่มือนี้จะช่วยให้คุณมีแนวทางที่ชัดเจนและตรงไปตรงมาในการทำงานกับ PDF ลองทำดูกับ PDF ของคุณเองสิ!

## คำถามที่พบบ่อย

### ฉันสามารถค้นหาหลายคำในครั้งเดียวได้ไหม?  
ใช่ คุณสามารถปรับเปลี่ยนได้ `TextFragmentAbsorber` เพื่อค้นหาหลายวลีโดยปรับสตริงการค้นหาให้เหมาะสม

### จะเกิดอะไรขึ้นถ้าข้อความมีระยะหลายบรรทัด?  
Aspose.PDF จะยังคงจดจำและแยกข้อความออกมาได้แม้ว่าจะมีหลายบรรทัดก็ตาม คุณสามารถจัดการส่วนต่างๆ เหล่านี้ได้ทีละส่วน

### ฉันจะบันทึกข้อความที่แยกออกมาลงในไฟล์ได้อย่างไร?  
คุณสามารถเขียนข้อความที่แยกออกมาลงในไฟล์โดยใช้การดำเนินการ I/O ของไฟล์ C# มาตรฐาน เช่น `StreamWriter`-

### Aspose.PDF รองรับการแยกข้อความจาก PDF ที่สแกนหรือไม่  
Aspose.PDF ไม่รองรับ OCR สำหรับ PDF ที่สแกน คุณจะต้องใช้เครื่องมือ OCR เพื่อจดจำข้อความ

### ฉันจะจัดการไฟล์ PDF ที่เข้ารหัสได้อย่างไร  
หาก PDF ของคุณได้รับการป้องกันด้วยรหัสผ่าน คุณสามารถปลดล็อคได้โดยใช้ Aspose.PDF โดยระบุรหัสผ่านเมื่อโหลดเอกสาร

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}