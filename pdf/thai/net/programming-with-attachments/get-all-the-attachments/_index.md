---
"description": "เรียนรู้วิธีแยกไฟล์แนบทั้งหมดจากไฟล์ PDF โดยใช้ Aspose.PDF สำหรับ .NET ในบทช่วยสอนทีละขั้นตอนนี้"
"linktitle": "รับสิ่งที่แนบมาทั้งหมดในไฟล์ PDF"
"second_title": "เอกสารอ้างอิง Aspose.PDF สำหรับ API ของ .NET"
"title": "รับสิ่งที่แนบมาทั้งหมดในไฟล์ PDF"
"url": "/th/net/programming-with-attachments/get-all-the-attachments/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# รับสิ่งที่แนบมาทั้งหมดในไฟล์ PDF

## การแนะนำ

ในยุคดิจิทัล PDF กลายมาเป็นสิ่งสำคัญสำหรับการแชร์เอกสาร PDF มีความยืดหยุ่น ปลอดภัย และสามารถบรรจุข้อมูลได้มากมาย รวมถึงไฟล์แนบ คุณเคยสงสัยไหมว่าจะดึงข้อมูลที่ซ่อนอยู่ทั้งหมดจากไฟล์ PDF ได้อย่างไร คุณโชคดีแล้ว ในบทช่วยสอนนี้ เราจะเจาะลึกการใช้ Aspose.PDF สำหรับ .NET เพื่อรับไฟล์แนบทั้งหมดในไฟล์ PDF ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น คู่มือนี้จะแนะนำคุณทีละขั้นตอน

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มต้นใช้งานโค้ด เรามาตรวจสอบก่อนว่าคุณมีทุกสิ่งที่จำเป็นสำหรับการเริ่มต้น:

1. Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio ไว้ในเครื่องของคุณแล้ว ซึ่งเป็น IDE หลักสำหรับการพัฒนา .NET
2. Aspose.PDF สำหรับ .NET: คุณจะต้องดาวน์โหลดและติดตั้งไลบรารี Aspose.PDF คุณสามารถค้นหาได้ [ที่นี่](https://releases-aspose.com/pdf/net/).
3. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# จะช่วยให้คุณเข้าใจชิ้นส่วนโค้ดได้ดีขึ้น

## แพ็คเกจนำเข้า

ในการเริ่มต้น คุณจะต้องนำเข้าแพ็คเกจที่จำเป็นลงในโปรเจ็กต์ C# ของคุณ โดยทำดังนี้:

### สร้างโครงการใหม่

เปิด Visual Studio และสร้างโปรเจ็กต์ C# ใหม่ เลือกแอปพลิเคชันคอนโซลเพื่อความเรียบง่าย

### เพิ่มการอ้างอิง Aspose.PDF

1. คลิกขวาที่โครงการของคุณใน Solution Explorer
2. เลือก “จัดการแพ็คเกจ NuGet”
3. ค้นหา “Aspose.PDF” และติดตั้งเวอร์ชันล่าสุด

### นำเข้าเนมสเปซ

ที่ด้านบนของไฟล์ C# ของคุณ นำเข้าเนมสเปซ Aspose.PDF

```csharp
using System.IO;
using Aspose.Pdf;
using System;
```

ตอนนี้เราได้ตั้งค่าสภาพแวดล้อมเรียบร้อยแล้ว มาดูขั้นตอนสำคัญของการแยกไฟล์แนบจากไฟล์ PDF กัน

## ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีเอกสารของคุณ

ขั้นแรก คุณต้องระบุเส้นทางไปยังไดเร็กทอรีเอกสารของคุณ นี่คือที่ที่ไฟล์ PDF ของคุณจะอยู่

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

แทนที่ `YOUR DOCUMENT DIRECTORY` ด้วยเส้นทางจริงที่จัดเก็บไฟล์ PDF ของคุณ ซึ่งเป็นสิ่งสำคัญเนื่องจากโปรแกรมจำเป็นต้องทราบว่าจะต้องค้นหาไฟล์ที่ใด

## ขั้นตอนที่ 2: เปิดเอกสาร PDF

ต่อไปเราจะเปิดเอกสาร PDF โดยใช้ไลบรารี Aspose.PDF นี่คือจุดเริ่มต้นของความมหัศจรรย์!

```csharp
Document pdfDocument = new Document(dataDir + "GetAlltheAttachments.pdf");
```

ที่นี่เราสร้างใหม่ `Document` วัตถุและส่งผ่านเส้นทางของไฟล์ PDF ตรวจสอบให้แน่ใจว่าชื่อไฟล์ตรงกันทุกประการ รวมถึงนามสกุลด้วย

## ขั้นตอนที่ 3: เข้าถึงคอลเลกชันไฟล์ที่ฝังไว้

ตอนนี้เราเปิดเอกสารแล้ว ให้เข้าไปที่คอลเลกชันไฟล์ที่ฝังไว้ นี่คือที่ที่ไฟล์แนบทั้งหมดถูกเก็บไว้

```csharp
EmbeddedFileCollection embeddedFiles = pdfDocument.EmbeddedFiles;
```

ด้วยบรรทัดนี้ เราจะดึงไฟล์ที่ฝังไว้ทั้งหมดลงในคอลเล็กชั่นที่เราสามารถวนซ้ำได้อย่างง่ายดาย

## ขั้นตอนที่ 4: นับไฟล์ที่ฝังไว้

การทราบจำนวนไฟล์แนบที่คุณกำลังจัดการนั้นเป็นเรื่องที่ดีเสมอ มาพิมพ์จำนวนไฟล์ที่ฝังไว้ทั้งหมดกัน

```csharp
Console.WriteLine("Total files : {0}", embeddedFiles.Count);
```

นี่จะช่วยให้คุณดูภาพรวมได้อย่างรวดเร็วว่า PDF ของคุณมีไฟล์แนบจำนวนเท่าไร

## ขั้นตอนที่ 5: วนรอบสิ่งที่แนบมา

ตอนนี้มาถึงส่วนสนุก ๆ แล้ว! เราจะวนซ้ำผ่านข้อมูลจำเพาะของไฟล์แต่ละไฟล์ในคอลเลกชันไฟล์ที่ฝังไว้และแยกรายละเอียดออกมา

```csharp
int count = 1;

foreach (FileSpecification fileSpecification in embeddedFiles)
{
    Console.WriteLine("Name: {0}", fileSpecification.Name);
    Console.WriteLine("Description: {0}", fileSpecification.Description);
    Console.WriteLine("Mime Type: {0}", fileSpecification.MIMEType);
```

ในลูปนี้ เราจะพิมพ์ชื่อ คำอธิบาย และประเภท MIME ของไฟล์แนบแต่ละรายการ เพื่อให้คุณเห็นภาพชัดเจนว่าไฟล์ PDF ของคุณมีเนื้อหาอะไรบ้าง

## ขั้นตอนที่ 6: ตรวจสอบพารามิเตอร์เพิ่มเติม

สิ่งที่แนบมาบางรายการอาจมีพารามิเตอร์เพิ่มเติม ลองตรวจสอบว่ามีพารามิเตอร์เหล่านี้หรือไม่ แล้วพิมพ์ออกมา

```csharp
if (fileSpecification.Params != null)
{
    Console.WriteLine("CheckSum: {0}", fileSpecification.Params.CheckSum);
    Console.WriteLine("Creation Date: {0}", fileSpecification.Params.CreationDate);
    Console.WriteLine("Modification Date: {0}", fileSpecification.Params.ModDate);
    Console.WriteLine("Size: {0}", fileSpecification.Params.Size);
}
```

ขั้นตอนนี้จะช่วยให้คุณไม่พลาดรายละเอียดสำคัญใดๆ เกี่ยวกับสิ่งที่แนบมา

## ขั้นตอนที่ 7: แตกไฟล์และบันทึกสิ่งที่แนบมา

สุดท้ายนี้ เรามาแยกเนื้อหาจากไฟล์แนบแต่ละไฟล์แล้วบันทึกลงในไฟล์ นี่คือผลลัพธ์จากการทำงานหนักของคุณ!

```csharp
byte[] fileContent = new byte[fileSpecification.Contents.Length];
fileSpecification.Contents.Read(fileContent, 0, fileContent.Length);
FileStream fileStream = new FileStream(dataDir + count + "_out" + ".txt", FileMode.Create);
fileStream.Write(fileContent, 0, fileContent.Length);
fileStream.Close();
count += 1;
```

ในโค้ดนี้ เราจะอ่านเนื้อหาของไฟล์แนบแต่ละรายการลงในอาร์เรย์ไบต์ จากนั้นจึงเขียนลงในไฟล์ใหม่ ไฟล์ต่างๆ จะถูกตั้งชื่อตามลำดับ (เช่น `1_out.txt`- `2_out.txt`ฯลฯ).

## บทสรุป

และแล้วคุณก็ทำได้! คุณได้แยกไฟล์แนบทั้งหมดออกจากไฟล์ PDF สำเร็จแล้วโดยใช้ Aspose.PDF สำหรับ .NET ไลบรารีอันทรงพลังนี้ทำให้การจัดการเอกสาร PDF และการเข้าถึงสมบัติที่ซ่อนอยู่เป็นเรื่องง่าย ไม่ว่าคุณจะทำงานในโปรเจ็กต์ส่วนตัวหรือแอปพลิเคชันระดับมืออาชีพ การรู้วิธีแยกไฟล์แนบก็มีประโยชน์อย่างยิ่ง

## คำถามที่พบบ่อย

### Aspose.PDF สำหรับ .NET คืออะไร?
Aspose.PDF สำหรับ .NET เป็นไลบรารีที่ช่วยให้นักพัฒนาสามารถสร้าง จัดการ และแปลงเอกสาร PDF ได้ด้วยโปรแกรม

### ฉันสามารถใช้ Aspose.PDF ได้ฟรีหรือไม่?
ใช่ Aspose นำเสนอเวอร์ชันทดลองใช้งานฟรีที่คุณสามารถใช้สำรวจฟีเจอร์ต่างๆ ของไลบรารีได้ ลองดูสิ [ที่นี่](https://releases-aspose.com/).

### ฉันจะได้รับการสนับสนุนสำหรับ Aspose.PDF ได้อย่างไร
คุณสามารถรับการสนับสนุนผ่านฟอรั่ม Aspose ได้ [ที่นี่](https://forum-aspose.com/c/pdf/10).

### มีใบอนุญาตชั่วคราวให้ใช้หรือไม่?
ใช่ คุณสามารถขอรับใบอนุญาตชั่วคราวสำหรับ Aspose.PDF ได้ [ที่นี่](https://purchase-aspose.com/temporary-license/).

### ฉันสามารถหาเอกสารได้ที่ไหน
เอกสารประกอบสำหรับ Aspose.PDF สำหรับ .NET สามารถพบได้ [ที่นี่](https://reference-aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}