---
"description": "เรียนรู้วิธีการจัดเรียงเนื้อหากล่องลอยในไฟล์ PDF โดยใช้ Aspose.PDF สำหรับ .NET สร้างเอกสารที่สวยงามด้วยเลย์เอาต์ระดับมืออาชีพ"
"linktitle": "การจัดตำแหน่งข้อความสำหรับเนื้อหากล่องลอยในไฟล์ PDF"
"second_title": "เอกสารอ้างอิง Aspose.PDF สำหรับ API ของ .NET"
"title": "การจัดตำแหน่งข้อความสำหรับเนื้อหากล่องลอยในไฟล์ PDF"
"url": "/th/net/programming-with-text/text-alignment-for-floating-box-contents/"
"weight": 520
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การจัดตำแหน่งข้อความสำหรับเนื้อหากล่องลอยในไฟล์ PDF

## การแนะนำ

การสร้าง PDF ที่มีรูปลักษณ์สวยงามถือเป็นทักษะที่สำคัญในโลกดิจิทัลในปัจจุบัน ซึ่งทุกคนต่างก็ต้องการความสนใจ Aspose.PDF สำหรับ .NET ช่วยให้ภารกิจนี้ง่ายและยืดหยุ่นอย่างเหลือเชื่อ โดยเฉพาะอย่างยิ่งเมื่อต้องปรับแต่งเค้าโครงของเอกสาร ในบทช่วยสอนนี้ เราจะมาสำรวจวิธีการจัดวางเนื้อหาในกล่องลอยภายในไฟล์ PDF ของคุณ วิธีนี้จะทำให้เอกสารของคุณดูสวยงามและเป็นมืออาชีพจนโดดเด่นกว่าเอกสารอื่นๆ

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเริ่มบทช่วยสอน มีสิ่งสำคัญบางประการที่คุณจำเป็นต้องมี:

1. .NET Framework: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET Framework ที่เข้ากันได้บนเครื่องของคุณ เนื่องจากนี่คือที่ที่คุณจะรันโค้ดของคุณ
2. ไลบรารี Aspose.PDF: คุณต้องมีไลบรารี Aspose.PDF หากคุณยังไม่ได้ดาวน์โหลด คุณสามารถทำได้ [ที่นี่](https://releases-aspose.com/pdf/net/).
3. IDE: สภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE) เช่น Visual Studio จะมีประโยชน์สำหรับการเขียนโค้ดและการดีบัก
4. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# จะทำให้ติดตามและทำความเข้าใจชิ้นส่วนโค้ดได้ง่ายขึ้น

## แพ็คเกจนำเข้า

ในการเริ่มต้น คุณต้องนำเข้าแพ็คเกจที่จำเป็นลงในโปรเจ็กต์ C# ของคุณ โดยทำดังนี้:

1. เปิดโครงการของคุณ: เปิด IDE ของคุณ และเปิดโครงการที่คุณต้องการใช้งานฟังก์ชันกล่องลอย
2. ติดตั้ง Aspose.PDF สำหรับ .NET: ใช้ตัวจัดการแพ็คเกจ NuGet เพื่อติดตั้งแพ็คเกจ Aspose.PDF โดยทำดังนี้:
   - คลิกขวาที่โครงการของคุณใน Solution Explorer เลือก "จัดการแพ็คเกจ NuGet"
   - ค้นหา “Aspose.PDF” แล้วคลิก "ติดตั้ง"
   
```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

เมื่อคุณตั้งค่าแพ็คเกจเรียบร้อยแล้ว คุณก็พร้อมที่จะสร้างและจัดตำแหน่งกล่องลอยใน PDF ของคุณได้

ต่อไปมาดูขั้นตอนการเพิ่มและจัดตำแหน่งกล่องลอยในเอกสาร PDF กัน เราจะสร้างกล่องลอยหลายกล่องและจัดตำแหน่งเนื้อหาต่างกันเพื่อใช้ประกอบภาพ

## ขั้นตอนที่ 1: ตั้งค่าเอกสาร

ขั้นตอนแรกคือการเริ่มต้นเอกสาร PDF ใหม่และเพิ่มหน้าเข้าไป ซึ่งทำหน้าที่เป็นผืนผ้าใบสำหรับกล่องลอยของเรา

```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "YOUR DOCUMENT DIRECTORY";
Aspose.Pdf.Document doc = new Document();
doc.Pages.Add();
```

ในโค้ดตัวอย่างนี้ ให้แทนที่ `"YOUR DOCUMENT DIRECTORY"` ด้วยเส้นทางที่แท้จริงที่คุณต้องการบันทึกไฟล์ PDF ของคุณ

## ขั้นตอนที่ 2: สร้างกล่องลอยแรก

ต่อไปเราจะสร้างกล่องลอยตัวแรกและตั้งค่าการจัดตำแหน่ง ที่นี่ เนื้อหาจะถูกจัดตำแหน่งให้ชิดขวาล่างของกล่อง

```csharp
Aspose.Pdf.FloatingBox floatBox = new Aspose.Pdf.FloatingBox(100, 100);
floatBox.VerticalAlignment = VerticalAlignment.Bottom;
floatBox.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
floatBox.Paragraphs.Add(new TextFragment("FloatingBox_bottom"));
floatBox.Border = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, Aspose.Pdf.Color.Blue);
doc.Pages[1].Paragraphs.Add(floatBox);
```

- FloatingBox(100, 100): เป็นการเริ่มต้นด้วยกล่องลอยที่มีความกว้างและความสูงหน่วยละ 100 หน่วย
- การจัดแนวแนวตั้งและแนวนอน: เราจะกำหนดให้ข้อความจัดแนวชิดด้านล่างและด้านขวา
- TextFragment: แสดงข้อความที่คุณต้องการแสดงภายในกล่องลอย
- BorderInfo: จะสร้างขอบรอบ ๆ กล่องลอย เพื่อให้มองเห็นได้ชัดเจน

## ขั้นตอนที่ 3: เพิ่มกล่องลอยที่สอง

ตอนนี้เรามาสร้างกล่องลอยตัวที่สองที่วางเนื้อหาไว้ตรงกลางกัน

```csharp
Aspose.Pdf.FloatingBox floatBox1 = new Aspose.Pdf.FloatingBox(100, 100);
floatBox1.VerticalAlignment = VerticalAlignment.Center;
floatBox1.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
floatBox1.Paragraphs.Add(new TextFragment("FloatingBox_center"));
floatBox1.Border = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, Aspose.Pdf.Color.Blue);
doc.Pages[1].Paragraphs.Add(floatBox1);
```

เช่นเดียวกับกล่องแรก เราได้ตั้งค่าการจัดแนวแนวตั้งให้กึ่งกลางและการจัดแนวแนวนอนให้ชิดขวา วิธีนี้ช่วยให้ปรับเนื้อหาแบบไดนามิกได้และดึงดูดสายตาได้ดียิ่งขึ้น

## ขั้นตอนที่ 4: สร้างกล่องลอยตัวที่สาม

สำหรับกล่องลอยอันที่สามและอันสุดท้าย เราจะจัดตำแหน่งเนื้อหาให้อยู่มุมขวาบน

```csharp
Aspose.Pdf.FloatingBox floatBox2 = new Aspose.Pdf.FloatingBox(100, 100);
floatBox2.VerticalAlignment = VerticalAlignment.Top;
floatBox2.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
floatBox2.Paragraphs.Add(new TextFragment("FloatingBox_top"));
floatBox2.Border = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, Aspose.Pdf.Color.Blue);
doc.Pages[1].Paragraphs.Add(floatBox2);
```

กล่องนี้จะจัดตำแหน่งเนื้อหาที่ด้านบนขวา แสดงให้เห็นถึงความยืดหยุ่นที่คุณมีกับไลบรารี Aspose.PDF กล่องลอยแต่ละกล่องสามารถทำหน้าที่ที่แตกต่างกันได้ ขึ้นอยู่กับวิธีที่คุณต้องการสื่อสารข้อมูลในรูปแบบภาพ

## ขั้นตอนที่ 5: บันทึกเอกสาร

ในที่สุด ก็ถึงเวลาบันทึกเอกสารของคุณแล้ว คุณจะบันทึกเอกสารนั้นในตำแหน่งที่คุณระบุไว้ก่อนหน้านี้

```csharp
doc.Save(dataDir + "FloatingBox_alignment_review_out.pdf");
```

ไฟล์จะถูกบันทึกด้วยชื่อ `FloatingBox_alignment_review_out.pdf` ในไดเร็กทอรีที่ระบุ ตรวจสอบให้แน่ใจว่าได้เลือกตำแหน่งนี้เพื่อดูไฟล์ PDF ที่คุณสร้างขึ้น

## บทสรุป

การใช้ Aspose.PDF สำหรับ .NET เพื่อจัดการเค้าโครง PDF ช่วยให้คุณสามารถสร้างเอกสารที่เป็นมืออาชีพและดึงดูดสายตาได้อย่างมีประสิทธิภาพ ด้วยการทำความเข้าใจวิธีการจัดวางเนื้อหาในกล่องลอย คุณสามารถปรับปรุงประสบการณ์การใช้งานไฟล์ PDF ของคุณได้อย่างมาก ดังที่เราเห็นแล้วว่าเป็นเรื่องง่ายแต่ทรงพลังเพียงพอที่จะทำให้ PDF ของคุณโดดเด่น

## คำถามที่พบบ่อย

### กล่องลอยใน Aspose.PDF คืออะไร?  
กล่องลอยช่วยให้คุณวางตำแหน่งเนื้อหาได้อย่างยืดหยุ่นภายในเค้าโครง PDF

### ฉันสามารถเปลี่ยนสีขอบกล่องลอยได้ไหม  
ใช่ คุณสามารถระบุสีที่แตกต่างกันสำหรับเส้นขอบได้เมื่อสร้างกล่องลอย

### Aspose.PDF สำหรับ .NET ใช้ได้ฟรีหรือไม่?  
Aspose.PDF เสนอการทดลองใช้ฟรี แต่ต้องมีใบอนุญาตแบบชำระเงินจึงจะใช้ฟังก์ชันครบถ้วน

### ฉันสามารถเพิ่มรูปภาพลงในกล่องลอยได้หรือไม่?  
แน่นอน! คุณสามารถเพิ่มเนื้อหาประเภทต่างๆ รวมถึงรูปภาพลงในกล่องลอยได้

### ฉันสามารถหาข้อมูลเพิ่มเติมเกี่ยวกับ Aspose.PDF ได้จากที่ใด  
สามารถดูเอกสารรายละเอียดได้ [ที่นี่](https://reference-aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}