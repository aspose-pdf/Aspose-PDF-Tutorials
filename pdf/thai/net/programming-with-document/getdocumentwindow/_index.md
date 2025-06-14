---
"description": "เรียนรู้วิธีใช้คุณลักษณะ GetDocumentWindow ของ Aspose.PDF สำหรับ .NET เพื่อรับข้อมูลเกี่ยวกับคุณสมบัติหน้าต่างเอกสาร PDF"
"linktitle": "รับหน้าต่างเอกสาร"
"second_title": "เอกสารอ้างอิง Aspose.PDF สำหรับ API ของ .NET"
"title": "รับหน้าต่างเอกสาร"
"url": "/th/net/programming-with-document/getdocumentwindow/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# รับหน้าต่างเอกสาร

# การแนะนำ

คุณกำลังทำงานกับ PDF และต้องการควบคุมเพิ่มเติมว่าไฟล์จะปรากฏอย่างไรเมื่อเปิดขึ้นมาหรือไม่ ไม่ว่าจะเป็นการซ่อนแถบเมนูหรือการปรับขนาดหน้าต่างให้พอดีกับหน้าแรก Aspose.PDF สำหรับ .NET มอบเครื่องมือทั้งหมดที่คุณต้องการเพื่อปรับแต่งลักษณะการทำงานของ PDF เมื่อเปิดในโปรแกรมดู ในบทช่วยสอนนี้ เราจะอธิบายวิธีการเรียกค้นและจัดการการตั้งค่าหน้าต่างเอกสารใน Aspose.PDF สำหรับ .NET


# ข้อกำหนดเบื้องต้น

ก่อนจะเริ่มบทช่วยสอนนี้ ให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นดังต่อไปนี้:

- Aspose.PDF สำหรับ .NET ติดตั้งอยู่บนสภาพแวดล้อมการพัฒนาของคุณ
  - [ดาวน์โหลด Aspose.PDF สำหรับ .NET](https://releases.aspose.com/pdf/net/)
- ใบอนุญาตที่ถูกต้องสำหรับ Aspose.PDF หรือคุณสามารถรับได้ [ทดลองใช้งานฟรี](https://releases.aspose.com/) หรือ [ใบอนุญาตชั่วคราว](https://purchase-aspose.com/temporary-license/).
- ความเข้าใจพื้นฐานเกี่ยวกับ .NET และ C#
- Visual Studio หรือ IDE อื่นที่เหมาะสม

# แพ็คเกจนำเข้า

ก่อนที่คุณจะเริ่มเขียนโค้ดใดๆ คุณจะต้องนำเข้าแพ็คเกจที่จำเป็น เปิดโปรเจ็กต์ของคุณ และเพิ่มเนมสเปซต่อไปนี้ที่ด้านบนของไฟล์ C#:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

สิ่งนี้จะทำให้คุณเข้าถึงคลาสและวิธีการทั้งหมดที่จำเป็นสำหรับการจัดการเอกสาร PDF โดยใช้ Aspose.PDF สำหรับ .NET

ตอนนี้มาดูขั้นตอนการดึงการตั้งค่าหน้าต่างเอกสารที่แตกต่างกัน สำหรับตัวอย่างนี้ เราจะใช้ไฟล์ PDF ตัวอย่างชื่อ `GetDocumentWindow-pdf`.

## ขั้นตอนที่ 1: ตั้งค่าเส้นทางไดเรกทอรีเอกสาร

ขั้นแรก เราต้องกำหนดเส้นทางไปยังไฟล์ PDF ของเรา สิ่งสำคัญคือคุณต้องมีเส้นทางไฟล์ที่ถูกต้องเพื่อหลีกเลี่ยงข้อผิดพลาดระหว่างการดำเนินการ

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

ที่นี่แทนที่ `"YOUR DOCUMENT DIRECTORY"` โดยมีไดเร็กทอรีจริงที่ไฟล์ PDF ของคุณตั้งอยู่ นี่คือไดเร็กทอรีการทำงานของคุณที่คุณจะโหลดเอกสาร PDF

## ขั้นตอนที่ 2: เปิดเอกสาร PDF

เมื่อกำหนดเส้นทางของไฟล์เรียบร้อยแล้ว ขั้นตอนต่อไปคือเปิดเอกสาร PDF โดยใช้ Aspose.PDF ซึ่งจะโหลดเอกสารเข้าสู่หน่วยความจำ ช่วยให้คุณสามารถเรียกค้นคุณสมบัติของเอกสารได้

```csharp
Document pdfDocument = new Document(dataDir + "GetDocumentWindow.pdf");
```

ด้วยโค้ดบรรทัดง่ายๆ นี้ คุณสามารถโหลดไฟล์ PDF ลงในไฟล์ได้สำเร็จ `pdfDocument` วัตถุซึ่งตอนนี้คุณจะสามารถเข้าถึงคุณสมบัติทั้งหมดได้

## ขั้นตอนที่ 3: ดึงสถานะการจัดกึ่งกลางหน้าต่าง

ต่อไปเรามาตรวจสอบว่าหน้าต่างเอกสารควรอยู่ตรงกลางเมื่อเปิดหรือไม่ ค่าเริ่มต้นคือ `false`-

```csharp
Console.WriteLine("CenterWindow : {0}", pdfDocument.CenterWindow);
```

หากผลลัพธ์ออกมาเป็น `true`หน้าต่างเอกสารจะเปิดขึ้นที่กึ่งกลางของหน้าจอ มิฉะนั้น จะเปิดที่ตำแหน่งเริ่มต้น

## ขั้นตอนที่ 4: ตรวจสอบทิศทางข้อความ

ลักษณะสำคัญอีกประการหนึ่งของลักษณะที่ปรากฏของ PDF คือทิศทางของข้อความ ซึ่งจะกำหนดว่าข้อความจะถูกอ่านจากซ้ายไปขวา (L2R) หรือขวาไปซ้าย (R2L) คุณสามารถเรียกข้อมูลนี้ได้โดยใช้โค้ดต่อไปนี้:

```csharp
Console.WriteLine("Direction : {0}", pdfDocument.Direction);
```

ผลลัพธ์ที่ได้จะเป็น `L2R` สำหรับข้อความจากซ้ายไปขวาและ `R2L` สำหรับข้อความจากขวาไปซ้าย การตั้งค่านี้มีประโยชน์อย่างยิ่งสำหรับเอกสารในภาษาเช่นอาหรับหรือฮีบรู

## ขั้นตอนที่ 5: แสดงชื่อเอกสารในหน้าต่าง

คุณสมบัติต่อไปนี้ช่วยให้คุณควบคุมว่าจะแสดงชื่อเอกสารหรือชื่อไฟล์บนแถบชื่อของหน้าต่างหรือไม่ โดยค่าเริ่มต้นจะตั้งค่าเป็น `false`หมายความว่าจะแสดงชื่อไฟล์

```csharp
Console.WriteLine("DisplayDocTitle : {0}", pdfDocument.DisplayDocTitle);
```

หากคุณต้องการให้แสดงชื่อเอกสารแทนชื่อไฟล์ คุณจะต้องเปิดใช้งานการตั้งค่านี้

## ขั้นตอนที่ 6: ปรับขนาดหน้าต่างให้พอดีกับหน้าแรก

บางครั้งคุณอาจต้องการให้หน้าต่างเอกสารปรับขนาดตัวเองโดยอัตโนมัติเพื่อให้พอดีกับหน้าแรกของ PDF เมื่อเปิดขึ้นมา ต่อไปนี้เป็นวิธีตรวจสอบว่าฟีเจอร์ดังกล่าวเปิดใช้งานอยู่หรือไม่:

```csharp
Console.WriteLine("FitWindow : {0}", pdfDocument.FitWindow);
```

โดยค่าเริ่มต้นจะถูกตั้งค่าเป็น `false`ซึ่งหมายความว่าขนาดของหน้าต่างจะคงเดิมไม่ว่าขนาดของหน้าแรกจะเป็นเท่าใดก็ตาม

## ขั้นตอนที่ 7: ซ่อนแถบเมนู

หากต้องการประสบการณ์การอ่านที่เน้นเฉพาะมากขึ้น คุณอาจต้องการซ่อนแถบเมนูของแอปพลิเคชันตัวแสดง คุณสามารถเรียกค้นการตั้งค่านี้โดยใช้บรรทัดต่อไปนี้:

```csharp
Console.WriteLine("HideMenuBar : {0}", pdfDocument.HideMenubar);
```

นี่จะกลับมา `true` หากแถบเมนูถูกซ่อนอยู่ และ `false` มิฉะนั้น.

## ขั้นตอนที่ 8: ซ่อนแถบเครื่องมือ

ในทำนองเดียวกัน คุณอาจต้องการซ่อนแถบเครื่องมือในโปรแกรมดู PDF เพื่อให้มีอินเทอร์เฟซผู้ใช้ที่สะอาดขึ้น การตั้งค่านี้สามารถเรียกใช้งานได้ดังนี้:

```csharp
Console.WriteLine("HideToolBar : {0}", pdfDocument.HideToolBar);
```

หากเปิดใช้งานการตั้งค่านี้ แถบเครื่องมือจะถูกซ่อนเมื่อเปิด PDF

## ขั้นตอนที่ 9: ซ่อนแถบเลื่อนและองค์ประกอบ UI

หากคุณต้องการแสดงเฉพาะเนื้อหาของหน้าโดยไม่มีองค์ประกอบ UI เพิ่มเติม เช่น แถบเลื่อน การตั้งค่านี้จะควบคุมพฤติกรรมดังกล่าว:

```csharp
Console.WriteLine("HideWindowUI : {0}", pdfDocument.HideWindowUI);
```

เมื่อตั้งค่าเป็น `true`โปรแกรมดู PDF จะซ่อนแถบเลื่อนและส่วนประกอบอินเทอร์เฟซผู้ใช้อื่นๆ โดยทิ้งไว้เฉพาะเนื้อหาของเอกสารเท่านั้น

## ขั้นตอนที่ 10: ตั้งค่าโหมดหน้าไม่เต็มหน้าจอ

คุณสามารถควบคุมลักษณะการปรากฏของเอกสารเมื่อออกจากโหมดเต็มหน้าจอโดยใช้ `NonFullScreenPageMode` คุณสมบัติ การตั้งค่านี้มีประโยชน์ในการกำหนดวิธีที่ผู้ใช้ควรโต้ตอบกับเอกสารในโหมดที่ไม่ใช่เต็มหน้าจอ

```csharp
Console.WriteLine("NonFullScreenPageMode : {0}", pdfDocument.NonFullScreenPageMode);
```

สามารถตั้งค่าเอาท์พุตเป็นโหมดต่างๆ ได้ เช่น ภาพขนาดย่อ โครงร่าง หรือแผงแนบ

## ขั้นตอนที่ 11: กำหนดเค้าโครงหน้า

การตั้งค่านี้ช่วยให้คุณควบคุมวิธีการจัดวางหน้าเอกสารได้ ตัวอย่างเช่น คุณสามารถเลือกมุมมองแบบหน้าเดียวหรือแบบคอลัมน์ต่อเนื่องได้

```csharp
Console.WriteLine("PageLayout : {0}", pdfDocument.PageLayout);
```

วิธีนี้ทำให้ผู้ใช้มีความยืดหยุ่นในการอ่านหรือดูเนื้อหาเอกสาร

## ขั้นตอนที่ 12: ระบุโหมดหน้า

สุดท้ายนี้ `PageMode` คุณสมบัติจะกำหนดว่าเอกสารควรแสดงอย่างไรเมื่อเปิด ตัวเลือกต่างๆ ได้แก่ การแสดงภาพขนาดย่อ การเข้าสู่โหมดเต็มหน้าจอ หรือการแสดงแผงสิ่งที่แนบมา

```csharp
Console.WriteLine("PageMode : {0}", pdfDocument.PageMode);
```

คุณสามารถตั้งค่าเป็นโหมดใดๆ ก็ได้ที่เหมาะกับวัตถุประสงค์ของ PDF ของคุณตามความต้องการ

## บทสรุป

ดังที่คุณจะเห็น Aspose.PDF สำหรับ .NET มีเครื่องมือที่ครอบคลุมสำหรับจัดการวิธีแสดงเอกสาร PDF ของคุณในโปรแกรมอ่าน PDF ต่างๆ ไม่ว่าคุณต้องการซ่อนแถบเครื่องมือ จัดกึ่งกลางหน้าต่าง หรือควบคุมทิศทางของข้อความ Aspose.PDF ก็มอบความยืดหยุ่นในการปรับปรุงประสบการณ์การดูของผู้ใช้

# คำถามที่พบบ่อย

### ฉันสามารถปรับแต่งระดับการซูมเริ่มต้นของ PDF ได้หรือไม่
ใช่ Aspose.PDF ช่วยให้คุณตั้งระดับการซูมเมื่อเปิดเอกสารได้

### ฉันจะล็อคขนาดหน้าต่างของ PDF ได้อย่างไร?
คุณสามารถตั้งค่าได้ `FitWindow` คุณสมบัติในการป้องกันไม่ให้หน้าต่างปรับขนาด

### Aspose.PDF รองรับโหมดการอ่านที่แตกต่างกันหรือไม่
ใช่ รองรับโหมดต่างๆ เช่น เต็มหน้าจอ, ภาพขนาดย่อ และไฟล์แนบ

### สามารถซ่อนแถบเลื่อนในโปรแกรมดู PDF ได้หรือไม่
แน่นอน คุณสามารถซ่อนแถบเลื่อนได้โดยการตั้งค่า `HideWindowUI` ทรัพย์สินที่จะ `true`-

### ฉันสามารถจัดหน้าต่างเอกสารให้ตรงกลางเมื่อเปิดได้หรือไม่
ใช่ คุณสามารถควบคุมสิ่งนี้ได้โดยตั้งค่า `CenterWindow` คุณสมบัติ.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}