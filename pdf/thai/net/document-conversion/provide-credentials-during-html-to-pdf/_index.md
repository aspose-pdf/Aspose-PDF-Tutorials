---
"description": "เรียนรู้วิธีแปลง HTML เป็น PDF โดยใช้ Aspose.PDF สำหรับ .NET ด้วยคู่มือทีละขั้นตอนนี้ เหมาะสำหรับนักพัฒนาที่ต้องการปรับปรุงกระบวนการสร้างเอกสาร"
"linktitle": "ระบุข้อมูลประจำตัวระหว่างการแปลง HTML เป็น PDF"
"second_title": "เอกสารอ้างอิง Aspose.PDF สำหรับ API ของ .NET"
"title": "ระบุข้อมูลประจำตัวระหว่างการแปลง HTML เป็น PDF"
"url": "/th/net/document-conversion/provide-credentials-during-html-to-pdf/"
"weight": 240
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ระบุข้อมูลประจำตัวระหว่างการแปลง HTML เป็น PDF

## การแนะนำ

ในโลกของการพัฒนาซอฟต์แวร์ การแปลง HTML เป็น PDF ถือเป็นข้อกำหนดทั่วไป ไม่ว่าคุณจะสร้างรายงาน ใบแจ้งหนี้ หรือเอกสารอื่นใด การมีไลบรารีที่เชื่อถือได้ในการจัดการงานนี้จะช่วยประหยัดเวลาและความพยายามของคุณได้มาก ลองใช้ Aspose.PDF สำหรับ .NET ซึ่งเป็นไลบรารีอันทรงพลังที่ช่วยให้ผู้พัฒนาสามารถสร้าง จัดการ และแปลงเอกสาร PDF ได้อย่างง่ายดาย ในบทช่วยสอนนี้ เราจะแนะนำคุณเกี่ยวกับขั้นตอนการใช้ Aspose.PDF เพื่อแปลง HTML เป็น PDF พร้อมทั้งให้ข้อมูลประจำตัวสำหรับการเข้าถึงที่ปลอดภัย ดังนั้น สวมหมวกแห่งการเขียนโค้ดของคุณแล้วเริ่มกันเลย!

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มต้น มีบางสิ่งที่คุณต้องมี:

1. Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio ไว้ในเครื่องของคุณแล้ว นี่จะเป็นสภาพแวดล้อมการพัฒนาของเรา
2. Aspose.PDF สำหรับ .NET: คุณสามารถดาวน์โหลดไลบรารีได้จาก [เว็บไซต์](https://releases.aspose.com/pdf/net/)หากคุณต้องการทดลองใช้ก่อน คุณยังสามารถรับ [ทดลองใช้งานฟรี](https://releases-aspose.com/).
3. ความรู้พื้นฐานเกี่ยวกับ C#: ความคุ้นเคยกับการเขียนโปรแกรม C# จะช่วยให้คุณเข้าใจตัวอย่างต่างๆ ได้ดีขึ้น
4. การเข้าถึงอินเทอร์เน็ต: เนื่องจากเราจะดึงเนื้อหา HTML จาก URL โปรดตรวจสอบว่าคุณมีการเชื่อมต่ออินเทอร์เน็ตที่ใช้งานได้

## แพ็คเกจนำเข้า

หากต้องการเริ่มต้นใช้งาน Aspose.PDF คุณต้องนำเข้าแพ็คเกจที่จำเป็นลงในโปรเจ็กต์ของคุณ โดยคุณสามารถทำได้ดังนี้:

1. เปิดโครงการ Visual Studio ของคุณ
2. คลิกขวาที่โครงการของคุณใน Solution Explorer และเลือก "จัดการแพ็คเกจ NuGet"
3. ค้นหา "Aspose.PDF" และติดตั้งเวอร์ชันล่าสุด

```csharp
using System.IO;
using Aspose.Pdf;
using System;
using System.Net;
```
ตอนนี้เราได้ตั้งค่าทุกอย่างเรียบร้อยแล้ว เรามาแบ่งขั้นตอนการแปลง HTML เป็น PDF พร้อมข้อมูลประจำตัวออกเป็นขั้นตอนที่สามารถจัดการได้กัน

## ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีเอกสารของคุณ

ก่อนที่เราจะแปลง HTML เป็น PDF เราจะต้องระบุตำแหน่งที่จะบันทึกไฟล์ PDF เอาต์พุต โดยกำหนดเส้นทางไปยังไดเร็กทอรีเอกสาร

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

แทนที่ `"YOUR DOCUMENT DIRECTORY"` ด้วยเส้นทางที่คุณต้องการบันทึกไฟล์ PDF ของคุณ ซึ่งอาจเป็นโฟลเดอร์บนเดสก์ท็อปหรือตำแหน่งอื่นในระบบของคุณก็ได้

## ขั้นตอนที่ 2: สร้างคำขอเว็บ

ต่อไปเราต้องสร้างคำขอเพื่อดึงเนื้อหา HTML จาก URL เฉพาะ นี่คือจุดที่เราจะใช้ `WebRequest` ระดับ.

```csharp
WebRequest request = WebRequest.Create("http://อ้างอิง: www.signchart.com/Report/PrintBook.asp?ProjectGuid=6FB9DBB0-");
```

ที่นี่ เรากำลังสร้างคำขอไปยัง URL ที่มี HTML ที่เราต้องการแปลง อย่าลืมแทนที่ URL ด้วย URL ที่คุณต้องการใช้

## ขั้นตอนที่ 3: ตั้งค่าข้อมูลประจำตัว (ถ้าจำเป็น)

หากเซิร์ฟเวอร์ต้องการข้อมูลประจำตัวเพื่อเข้าถึงเนื้อหา เราจะต้องตั้งค่า ซึ่งทำได้โดยใช้ `CredentialCache-DefaultCredentials`.

```csharp
request.Credentials = CredentialCache.DefaultCredentials;
```

บรรทัดนี้จะช่วยให้แน่ใจว่าคำขอใช้ข้อมูลประจำตัวเริ่มต้นของผู้ใช้ปัจจุบัน หากคุณจำเป็นต้องระบุข้อมูลประจำตัวเฉพาะ คุณสามารถสร้างใหม่ได้ `NetworkCredential` วัตถุ.

## ขั้นตอนที่ 4: รับการตอบสนอง

ตอนนี้เราได้ตั้งค่าคำขอเรียบร้อยแล้ว ถึงเวลารับการตอบกลับจากเซิร์ฟเวอร์

```csharp
HttpWebResponse response = (HttpWebResponse)request.GetResponse();
```

บรรทัดนี้จะส่งคำขอและรอให้เซิร์ฟเวอร์ตอบสนอง หากทุกอย่างเป็นไปด้วยดี เราจะได้รับเนื้อหา HTML ที่เราต้องการ

## ขั้นตอนที่ 5: อ่านสตรีมการตอบกลับ

เมื่อเราได้รับการตอบกลับแล้ว เราจำเป็นต้องอ่านเนื้อหาที่ส่งกลับมาโดยเซิร์ฟเวอร์ ซึ่งทำได้โดยใช้ `StreamReader`-

```csharp
Stream dataStream = response.GetResponseStream();
StreamReader reader = new StreamReader(dataStream);
string responseFromServer = reader.ReadToEnd();
reader.Close();
dataStream.Close();
response.Close();
```

ที่นี่ เรากำลังอ่านเนื้อหาทั้งหมดของสตรีมการตอบสนองลงในตัวแปรสตริงที่เรียกว่า `responseFromServer`อย่าลืมปิดเครื่องอ่านและสตรีมเพื่อปลดปล่อยทรัพยากร

## ขั้นตอนที่ 6: แปลง HTML เป็น PDF

ตอนนี้มาถึงส่วนที่น่าตื่นเต้นแล้ว! เราจะแปลงเนื้อหา HTML เป็นเอกสาร PDF โดยใช้ Aspose.PDF

```csharp
MemoryStream stream = new MemoryStream(System.Text.Encoding.UTF8.GetBytes(responseFromServer));
HtmlLoadOptions options = new HtmlLoadOptions("http://My.signchart.com/");
options.ExternalResourcesCredentials = CredentialCache.DefaultCredentials;

Document pdfDocument = new Document(stream, options);
```

ในขั้นตอนนี้เราจะสร้าง `MemoryStream` จากเนื้อหา HTML และการตั้งค่า `HtmlLoadOptions`สิ่งนี้ช่วยให้เราสามารถระบุ URL ฐานสำหรับรีซอร์สภายนอกใดๆ (เช่น รูปภาพหรือสไตล์ชีต) ที่ HTML อาจอ้างอิงได้

## ขั้นตอนที่ 7: บันทึกเอกสาร PDF

สุดท้ายเราจะต้องบันทึกเอกสาร PDF ที่สร้างขึ้นไปยังไดเร็กทอรีที่ระบุ

```csharp
pdfDocument.Save(dataDir + "ProvideCredentialsDuringHTMLToPDF_out.pdf");
```

บรรทัดนี้จะบันทึกไฟล์ PDF ด้วยชื่อ `ProvideCredentialsDuringHTMLToPDF_out.pdf` ในไดเร็กทอรีที่เราระบุไว้ก่อนหน้านี้

## บทสรุป

และแล้วคุณก็ทำได้! คุณได้แปลง HTML เป็น PDF สำเร็จแล้วโดยใช้ Aspose.PDF สำหรับ .NET พร้อมทั้งให้ข้อมูลประจำตัวสำหรับการเข้าถึงที่ปลอดภัย ไลบรารีอันทรงพลังนี้ทำให้การจัดการเอกสาร PDF เป็นเรื่องง่าย และด้วยโค้ดเพียงไม่กี่บรรทัด คุณก็สามารถสร้าง PDF ที่ดูเป็นมืออาชีพจากเนื้อหา HTML ได้ 

## คำถามที่พบบ่อย

### Aspose.PDF สำหรับ .NET คืออะไร?
Aspose.PDF สำหรับ .NET เป็นไลบรารีที่ช่วยให้นักพัฒนาสามารถสร้าง จัดการ และแปลงเอกสาร PDF ในแอปพลิเคชัน .NET ได้

### ฉันจะติดตั้ง Aspose.PDF ได้อย่างไร?
คุณสามารถติดตั้ง Aspose.PDF ผ่านตัวจัดการแพ็กเกจ NuGet ใน Visual Studio หรือดาวน์โหลดจาก [เว็บไซต์](https://releases-aspose.com/pdf/net/).

### ฉันสามารถใช้ Aspose.PDF ได้ฟรีหรือไม่?
ใช่ Aspose นำเสนอเวอร์ชันทดลองใช้งานฟรีที่คุณสามารถใช้ประเมินไลบรารีก่อนการซื้อ

### ฉันสามารถสร้างเอกสารประเภทใดได้บ้างโดยใช้ Aspose.PDF?
คุณสามารถสร้างเอกสารต่างๆ มากมาย รวมถึงรายงาน ใบแจ้งหนี้ และแบบฟอร์มด้วย Aspose.PDF

### ฉันสามารถค้นหาการสนับสนุนสำหรับ Aspose.PDF ได้ที่ไหน
คุณสามารถค้นหาการสนับสนุนและถามคำถามได้ที่ [ฟอรั่มสนับสนุน Aspose](https://forum-aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}