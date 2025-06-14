---
"description": "เรียนรู้วิธีสร้างไฮเปอร์ลิงก์ภายในเครื่องในไฟล์ PDF โดยใช้ Aspose.PDF สำหรับ .NET ได้อย่างง่ายดายด้วยคู่มือทีละขั้นตอนของเรา"
"linktitle": "สร้างไฮเปอร์ลิงก์ท้องถิ่นในไฟล์ PDF"
"second_title": "เอกสารอ้างอิง Aspose.PDF สำหรับ API ของ .NET"
"title": "สร้างไฮเปอร์ลิงก์ท้องถิ่นในไฟล์ PDF"
"url": "/th/net/programming-with-links-and-actions/create-local-hyperlink/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# สร้างไฮเปอร์ลิงก์ท้องถิ่นในไฟล์ PDF

## การแนะนำ

ในคู่มือนี้ เราจะแนะนำคุณเกี่ยวกับขั้นตอนการสร้างไฮเปอร์ลิงก์ภายในไฟล์ PDF โดยใช้ Aspose.PDF สำหรับ .NET เราจะอธิบายแต่ละขั้นตอนอย่างชัดเจน เพื่อให้แน่ใจว่าแม้ว่าคุณจะเป็นมือใหม่ในโลกของการจัดการ PDF คุณก็จะสามารถทำตามได้อย่างง่ายดาย

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเริ่มเขียนโค้ด เรามาตรวจสอบก่อนว่าคุณมีทุกสิ่งที่คุณต้องการ:

1. Visual Studio: คุณจะต้องใช้สิ่งนี้เพื่อพัฒนาแอปพลิเคชัน .NET ดาวน์โหลดได้จาก [เว็บไซต์](https://visualstudio-microsoft.com/).
2. Aspose.PDF สำหรับ .NET: คุณสามารถดาวน์โหลดไลบรารีนี้ได้ผ่านทาง [ลิงค์ดาวน์โหลดที่นี่](https://releases.aspose.com/pdf/net/)มาพร้อมฟีเจอร์มากมายสำหรับการจัดการ PDF
3. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# เล็กน้อยจะช่วยได้ แต่ไม่ต้องกังวล เราจะอธิบายโค้ดทีละบรรทัด
4. .NET Framework: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET framework ไว้ในเครื่องของคุณแล้ว คุณสามารถตรวจสอบข้อกำหนดได้ในไฟล์ Aspose.PDF [เอกสารประกอบ](https://reference-aspose.com/pdf/net/).

เมื่อตั้งค่าข้อกำหนดเบื้องต้นเหล่านี้แล้ว คุณก็พร้อมที่จะเรียนรู้วิธีสร้างไฮเปอร์ลิงก์ภายในในเอกสาร PDF ของคุณแล้ว!

## แพ็คเกจนำเข้า

ตอนนี้คุณเตรียมพร้อมทุกอย่างแล้ว ถึงเวลาที่จะนำเข้าแพ็คเกจที่จำเป็นลงในโปรเจ็กต์ C# ของคุณ ไลบรารี Aspose.PDF มีคลาสทั้งหมดที่เราต้องการ วิธีดำเนินการมีดังนี้:

### เปิดโครงการของคุณ

เปิดโปรเจ็กต์ .NET ที่มีอยู่ของคุณหรือสร้างโปรเจ็กต์ใหม่ใน Visual Studio หากคุณกำลังเริ่มต้นใหม่ ให้เลือก "สร้างโปรเจ็กต์ใหม่" จากหน้าจอเริ่มต้น

### เพิ่มการอ้างอิงถึง Aspose.PDF

คลิกขวาที่ "Dependencies" ในโฟลเดอร์โปรเจ็กต์ของคุณใน Solution Explorer เลือก "Manage NuGet Packages" จากนั้นค้นหา `Aspose.PDF`ติดตั้งเวอร์ชันล่าสุดที่มีให้ใช้งาน ซึ่งจะมีเครื่องมือทั้งหมดที่คุณต้องการสำหรับการสร้างและจัดการ PDF

### นำเข้าเนมสเปซ

ที่ด้านบนของไฟล์ .cs ของคุณ เพิ่มการใช้คำสั่งสำหรับไลบรารี Aspose.PDF ดังนี้:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

ด้วยวิธีการนี้ คุณจะสามารถเข้าถึงคุณลักษณะต่างๆ ของห้องสมุดได้

มาแบ่งกระบวนการสร้างไฮเปอร์ลิงก์ในพื้นที่ออกเป็นขั้นตอนง่ายๆ กัน แต่ละขั้นตอนจะได้รับการอธิบายอย่างครอบคลุมเพื่อช่วยให้คุณเข้าใจเหตุผลเบื้องหลัง

## ขั้นตอนที่ 1: ตั้งค่าอินสแตนซ์เอกสาร

ในขั้นตอนนี้ คุณจะสร้างอินสแตนซ์ใหม่ของคลาสเอกสารซึ่งแสดงถึงไฟล์ PDF ที่คุณจะใช้งาน

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // ตั้งค่าไดเรกทอรีเอกสารของคุณ
Document doc = new Document(); // สร้างอินสแตนซ์เอกสาร
```
การ `dataDir` ตัวแปรคือตำแหน่งที่ PDF ที่คุณเพิ่งสร้างจะอยู่ในนั้น คุณจะต้องแทนที่ `"YOUR DOCUMENT DIRECTORY"` ด้วยเส้นทางจริงบนระบบของคุณ `Document` คลาสสร้างเอกสาร PDF ใหม่ซึ่งเราสามารถเพิ่มหน้าและลิงก์ได้

## ขั้นตอนที่ 2: เพิ่มหน้าลงในเอกสาร

ต่อไปคุณจะเพิ่มหน้าลงในเอกสาร PDF ของคุณ 

```csharp
Page page = doc.Pages.Add(); // เพิ่มหน้าเข้าในคอลเลคชันหน้า
```
การ `Pages.Add()` วิธีการนี้จะเพิ่มหน้าใหม่ลงในเอกสาร ซึ่งเนื้อหาทั้งหมดของคุณจะอยู่ตรงนี้

## ขั้นตอนที่ 3: สร้างส่วนข้อความ

ตอนนี้มาสร้างข้อความที่จะทำหน้าที่เป็นลิงก์ที่สามารถคลิกได้กัน

```csharp
Aspose.Pdf.Text.TextFragment text = new Aspose.Pdf.Text.TextFragment("link page number test to page 7");
```
การ `TextFragment` แสดงถึงข้อความส่วนหนึ่งใน PDF เรากำลังสร้างลิงก์เพื่อแจ้งให้ผู้ใช้ทราบว่าระบบจะนำพวกเขาไปยังหน้าที่ 7

## ขั้นตอนที่ 4: สร้างไฮเปอร์ลิงก์ท้องถิ่น

นี่คือจุดที่เวทมนตร์เกิดขึ้น! คุณต้องสร้างไฮเปอร์ลิงก์ภายในเครื่องที่จะบอกส่วนของข้อความว่าควรชี้ไปที่ใด

```csharp
Aspose.Pdf.LocalHyperlink link = new Aspose.Pdf.LocalHyperlink(); // สร้างไฮเปอร์ลิงก์ท้องถิ่น
link.TargetPageNumber = 7; // ตั้งค่าหน้าเป้าหมายสำหรับอินสแตนซ์ลิงก์
text.Hyperlink = link; // ตั้งค่าไฮเปอร์ลิงก์ TextFragment
```
การ `LocalHyperlink` คลาสคือสิ่งที่ช่วยให้เราสามารถชี้ไปยังหน้าอื่น ๆ ในเอกสารเดียวกันได้ โดยการตั้งค่า `TargetPageNumber` ถึง 7 คุณกำหนดไฮเปอร์ลิงก์ให้กระโดดไปที่เพจนั้นโดยเฉพาะเมื่อคลิก

## ขั้นตอนที่ 5: เพิ่มส่วนข้อความลงในหน้า

หลังจากตั้งค่าไฮเปอร์ลิงก์แล้ว ก็ถึงเวลาที่จะเพิ่มส่วนข้อความลงในเพจที่เราสร้างขึ้น

```csharp
page.Paragraphs.Add(text); // เพิ่มข้อความลงในคอลเลกชันย่อหน้าของหน้า
```
บรรทัดนี้จะเพิ่มข้อความที่คุณคลิกได้ลงในคอลเล็กชั่นย่อหน้าของหน้า

## ขั้นตอนที่ 6: สร้างข้อความส่วนอื่น (ทางเลือก)

มาเพิ่มไฮเปอร์ลิงก์อีกอันเพื่อนำทางกลับไปยังหน้า 1 กัน

```csharp
text = new TextFragment("link page number test to page 1"); // สร้าง TextFragment ใหม่
text.IsInNewPage = true; // เพิ่มไปยังหน้าใหม่
```
การสร้างใหม่ `TextFragment` สำหรับลิงค์ที่สองเราตั้งค่า `IsInNewPage` เป็นจริง แสดงว่าข้อความนี้จะไปที่หน้าใหม่

## ขั้นตอนที่ 7: ตั้งค่าไฮเปอร์ลิงก์ท้องถิ่นที่สอง

เช่นเดียวกับก่อนหน้านี้ คุณจะสร้างไฮเปอร์ลิงก์ภายในเครื่องอีกอันสำหรับหน้าที่ 1

```csharp
link = new LocalHyperlink(); // สร้างอินสแตนซ์ไฮเปอร์ลิงก์ท้องถิ่นอื่น
link.TargetPageNumber = 1; // ตั้งค่าหน้าเป้าหมายสำหรับไฮเปอร์ลิงก์ที่สอง
text.Hyperlink = link; // ตั้งค่าลิงก์สำหรับ TextFragment ที่สอง
```
ไฮเปอร์ลิงก์นี้กำหนดเป้าหมายไปที่หน้า 1 ช่วยให้ผู้ใช้สามารถย้อนกลับได้เมื่อไปถึงหน้าที่สอง

## ขั้นตอนที่ 8: เพิ่มส่วนข้อความที่สองลงในหน้าใหม่

ต่อไปเรามาเพิ่มข้อความนี้ลงในหน้ากัน

```csharp
page.Paragraphs.Add(text); // เพิ่มข้อความลงในคอลเลกชันย่อหน้าของวัตถุหน้า
```
คล้ายกับขั้นตอนที่ 5 บรรทัดนี้จะเพิ่มข้อความไฮเปอร์ลิงก์ใหม่ลงในหน้าที่สร้างขึ้นใหม่

## ขั้นตอนที่ 9: บันทึกเอกสาร

ในที่สุด ก็ถึงเวลาที่จะบันทึกการทำงานหนักของคุณแล้ว! 

```csharp
dataDir = dataDir + "CreateLocalHyperlink_out.pdf"; // ระบุชื่อไฟล์เอาท์พุต
doc.Save(dataDir); // บันทึกเอกสารอัพเดต
Console.WriteLine("\nLocal hyperlink created successfully.\nFile saved at " + dataDir);
```
นี่จะรวมเส้นทางไดเร็กทอรีของคุณกับชื่อไฟล์ `Save()` วิธีการนี้จะบันทึกเอกสารของคุณและข้อความยืนยันจะแจ้งให้คุณทราบว่าทุกอย่างเป็นไปอย่างราบรื่น!

## บทสรุป

การสร้างไฮเปอร์ลิงก์ภายในไฟล์ PDF โดยใช้ Aspose.PDF สำหรับ .NET ไม่ใช่แค่กลเม็ดเด็ดๆ เท่านั้น แต่ยังเป็นฟีเจอร์ที่มีประโยชน์จริงที่ช่วยเพิ่มการนำทางและประสบการณ์ของผู้ใช้ ตอนนี้คุณมีความรู้ที่จะชี้ให้ผู้อ่านของคุณไปยังข้อมูลที่ต้องการได้โดยตรง ลองนึกถึงการเปรียบเทียบเบื้องต้นของเราดูสิ—ไม่มีวิญญาณหลงทางที่ต้องท่องไปในหน้าที่ไม่รู้จบอีกต่อไป

## คำถามที่พบบ่อย

### Aspose.PDF สำหรับ .NET คืออะไร?
Aspose.PDF สำหรับ .NET เป็นไลบรารีที่ช่วยให้นักพัฒนาสามารถสร้าง จัดการ และแปลงเอกสาร PDF ด้วยโปรแกรมโดยใช้กรอบงาน .NET

### ฉันสามารถสร้างไฮเปอร์ลิงก์ไปยังหน้าเว็บภายนอกได้หรือไม่
ใช่ Aspose.PDF ยังรองรับการสร้างไฮเปอร์ลิงก์ไปยัง URL ภายนอก นอกเหนือจากไฮเปอร์ลิงก์ภายใน PDF ด้วย

### มีการทดลองใช้ Aspose.PDF ฟรีหรือไม่
แน่นอน! คุณสามารถเข้าถึงการทดลองใช้ฟรีได้จาก [เว็บไซต์](https://releases-aspose.com/).

### Aspose รองรับภาษาโปรแกรมอะไรบ้าง?
Aspose นำเสนอไลบรารีสำหรับภาษาการเขียนโปรแกรมต่าง ๆ รวมถึง Java, C++ และ Python เป็นต้น

### ฉันจะได้รับการสนับสนุนสำหรับผลิตภัณฑ์ Aspose ได้อย่างไร
คุณสามารถขอความช่วยเหลือได้ผ่าน [ฟอรั่ม Aspose](https://forum-aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}