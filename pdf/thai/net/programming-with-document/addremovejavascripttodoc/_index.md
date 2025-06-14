---
"description": "เรียนรู้วิธีการเพิ่มและลบ JavaScript ลงในเอกสาร PDF โดยใช้ Aspose.PDF สำหรับ .NET คำแนะนำทีละขั้นตอนพร้อมบทช่วยสอนเกี่ยวกับโค้ดสำหรับการเขียนสคริปต์ในระดับเอกสาร"
"linktitle": "เพิ่มการลบ Javascript ลงในเอกสาร"
"second_title": "เอกสารอ้างอิง Aspose.PDF สำหรับ API ของ .NET"
"title": "เพิ่มการลบ Javascript ลงในเอกสาร PDF"
"url": "/th/net/programming-with-document/addremovejavascripttodoc/"
"weight": 30
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มการลบ Javascript ลงในเอกสาร PDF

## การแนะนำ

ในคู่มือนี้ เราจะแนะนำวิธีการใช้ Aspose.PDF สำหรับ .NET เพื่อแทรก JavaScript ลงในไฟล์ PDF และวิธีลบออกเมื่อจำเป็น เมื่ออ่านบทช่วยสอนนี้จบ คุณจะเข้าใจอย่างชัดเจนว่าจะจัดการ JavaScript ใน PDF ได้อย่างไรอย่างง่ายดาย

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกโค้ด มีบางสิ่งที่คุณจะต้องตั้งค่า:

1. Aspose.PDF สำหรับ .NET: คุณต้องมีไลบรารี Aspose.PDF สำหรับ .NET ติดตั้งอยู่ในโปรเจ็กต์ของคุณ หากคุณยังไม่มี ให้ดาวน์โหลดไลบรารีจาก [หน้าดาวน์โหลด Aspose.PDF สำหรับ .NET](https://releases-aspose.com/pdf/net/).
2. IDE หรือ Text Editor: คุณสามารถใช้ IDE ที่เข้ากันได้กับ .NET เช่น Visual Studio
3. ความรู้พื้นฐานเกี่ยวกับ C#: บทช่วยสอนนี้ถือว่าคุณคุ้นเคยกับ C# และคุ้นเคยกับการจัดการ PDF
4. ใบอนุญาต: ตรวจสอบให้แน่ใจว่าคุณได้สมัครใบอนุญาตที่ถูกต้องเพื่อหลีกเลี่ยงข้อจำกัด คุณสามารถขอใบอนุญาตชั่วคราวได้จาก [ที่นี่](https://purchase-aspose.com/temporary-license/).

## แพ็คเกจนำเข้า

หากต้องการเริ่มใช้ Aspose.PDF สำหรับ .NET คุณจะต้องนำเข้าเนมสเปซที่จำเป็นลงในโปรเจ็กต์ของคุณ ดังต่อไปนี้:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.Collections;
```

เนมสเปซทั้งสองนี้มีความจำเป็น `Aspose.Pdf` ช่วยให้คุณสามารถทำงานกับเอกสาร PDF ได้ `System.Collections` จะถูกใช้ในการจัดการคีย์ JavaScript

มาแบ่งกระบวนการทั้งหมดของการเพิ่มและลบ JavaScript จาก PDF ออกเป็นขั้นตอนที่ทำตามได้ง่าย

## ขั้นตอนที่ 1: เริ่มต้นเอกสาร PDF ใหม่

สิ่งแรกที่คุณต้องทำคือสร้างเอกสาร PDF ใหม่ เอกสารนี้จะทำหน้าที่เป็นพื้นที่ว่างสำหรับการเพิ่ม JavaScript

```csharp
Document doc = new Document();
doc.Pages.Add();
```

ที่นี่เราจะเริ่มต้นใหม่ `Document` วัตถุและเพิ่มหน้าว่างเข้าไป คิดว่านี่เป็นรากฐานของ PDF ของคุณ

## ขั้นตอนที่ 2: เพิ่ม JavaScript ลงใน PDF

ตอนนี้เรามีเอกสารแล้ว ถึงเวลาเพิ่ม JavaScript ลงไปบ้าง JavaScript ใน PDF สามารถใช้เพื่อเพิ่มพฤติกรรมที่กำหนดเองได้ เช่น การแจ้งเตือนหรือการตรวจสอบแบบฟอร์ม

```csharp
doc.JavaScript["func1"] = "function func1() { hello(); }";
doc.JavaScript["func2"] = "function func2() { hello(); }";
```

ในโค้ดตัวอย่างนี้ เราจะเพิ่มฟังก์ชัน JavaScript สองรายการ (`func1` และ `func2`) ไปยัง PDF ฟังก์ชันเหล่านี้สามารถทำงานต่างๆ ได้ ขึ้นอยู่กับความต้องการของคุณ ในที่นี้ เราจะเรียกใช้ฟังก์ชันตัวแทนที่เรียกว่า `hello()`-

## ขั้นตอนที่ 3: บันทึก PDF ด้วย JavaScript

เมื่อคุณเพิ่ม JavaScript ที่ต้องการแล้ว ก็ถึงเวลาบันทึก PDF

```csharp
doc.Save(dataDir + "AddJavascript.pdf");
```

นี้จะบันทึกเอกสารด้วย JavaScript ภายใต้ชื่อ `AddJavascript.pdf` ในไดเร็กทอรีที่ระบุ (`dataDir`-

## ขั้นตอนที่ 4: โหลดและดู JavaScript ใน PDF ที่มีอยู่

สมมติว่าคุณต้องการตรวจสอบหรือแก้ไขฟังก์ชัน JavaScript ใน PDF ที่มีอยู่ ขั้นตอนแรกคือโหลดไฟล์ PDF และเข้าถึงคีย์ JavaScript

```csharp
Document doc1 = new Document(dataDir + "AddJavascript.pdf");
IList keys = (System.Collections.IList)doc1.JavaScript.Keys;
```

เรากำลังโหลดสิ่งที่มีอยู่ `AddJavascript.pdf` และจัดเก็บคีย์ JavaScript ไว้ในรายการ `Keys` คุณสมบัติจะส่งคืนชื่อของฟังก์ชัน JavaScript ทั้งหมดที่แนบมากับเอกสาร

## ขั้นตอนที่ 5: แสดงฟังก์ชัน JavaScript

ต่อไปเราสามารถวนซ้ำผ่านฟังก์ชัน JavaScript เพื่อดูว่ามีอะไรบ้างในเอกสาร

```csharp
Console.WriteLine("=============================== ");
foreach (string key in keys)
{
    Console.WriteLine(key + " ==> " + doc1.JavaScript[key]);
}
```

การดำเนินการนี้จะพิมพ์ชื่อฟังก์ชัน JavaScript แต่ละรายการและโค้ดที่เกี่ยวข้องไปยังคอนโซล ซึ่งมีประโยชน์หากคุณต้องการตรวจสอบว่ามีฟังก์ชันใดบ้างในเอกสารในปัจจุบัน

## ขั้นตอนที่ 6: ลบ JavaScript ออกจาก PDF

ทีนี้ มาลองพูดว่าคุณต้องการลบฟังก์ชัน JavaScript เฉพาะ เช่น `func1`คุณสามารถทำได้ดังนี้:

```csharp
doc1.JavaScript.Remove("func1");
Console.WriteLine("Key 'func1' removed ");
```

การ `Remove` วิธีการใช้ชื่อของฟังก์ชัน JavaScript เป็นอาร์กิวเมนต์และลบออกจากเอกสาร

## ขั้นตอนที่ 7: ตรวจสอบการลบ JavaScript

หลังจากลบ JavaScript แล้ว คุณสามารถพิมพ์ฟังก์ชันที่เหลืออีกครั้งเพื่อยืนยันว่า `func1` ได้รับการลบเรียบร้อยแล้ว

```csharp
Console.WriteLine("=============================== ");
foreach (string key in keys)
{
    Console.WriteLine(key + " ==> " + doc1.JavaScript[key]);
}
Console.WriteLine("Javascript added/removed successfully.");
```

ส่วนสุดท้ายของโค้ดนี้จะช่วยให้แน่ใจว่าทุกอย่างอยู่ในที่ที่เหมาะสมและฟังก์ชัน JavaScript ได้รับการอัปเดตอย่างถูกต้อง

## บทสรุป

ขอแสดงความยินดี! คุณเพิ่งเรียนรู้วิธีการเพิ่มและลบ JavaScript จากเอกสาร PDF โดยใช้ Aspose.PDF สำหรับ .NET คุณลักษณะอันทรงพลังนี้สามารถใช้กับงานต่างๆ ได้มากมาย ตั้งแต่การเพิ่มข้อความแบบไดนามิกไปจนถึงการคำนวณหรือการตรวจสอบแบบกำหนดเอง การปรับแต่ง JavaScript ภายใน PDF จะช่วยปรับปรุงประสบการณ์ของผู้ใช้ได้อย่างมาก

## คำถามที่พบบ่อย

### ฉันสามารถเพิ่มฟังก์ชัน JavaScript หลายรายการลงใน PDF เดียวได้หรือไม่
แน่นอน! คุณสามารถเพิ่มฟังก์ชัน JavaScript ได้มากเท่าที่คุณต้องการโดยใช้ `doc.JavaScript` ของสะสม.

### จะเกิดอะไรขึ้นหากฉันพยายามลบฟังก์ชัน JavaScript ที่ไม่มีอยู่จริง?
ถ้าไม่มีฟังก์ชั่นนี้อยู่ `Remove` วิธีการนี้จะไม่เกิดข้อผิดพลาด แต่จะไม่ลบสิ่งใด ๆ เช่นกัน

### สามารถรัน JavaScript ได้ทันทีที่เปิด PDF หรือไม่
ใช่! คุณสามารถกำหนดค่า JavaScript ให้ทำงานเมื่อเกิดเหตุการณ์บางอย่าง เช่น การเปิดเอกสารหรือการคลิกปุ่ม

### ฉันสามารถแก้ไข JavaScript หลังจากเพิ่มลงใน PDF แล้วได้หรือไม่
ใช่ คุณสามารถโหลด PDF ที่มีอยู่ เข้าถึง JavaScript แก้ไขโค้ด และบันทึกเอกสารอีกครั้งได้

### การลบ JavaScript ออกไปจะส่งผลต่อเนื้อหา PDF ส่วนที่เหลือหรือไม่?
ไม่ การลบ JavaScript จะส่งผลต่อสคริปต์เท่านั้น เนื้อหาของ PDF ยังคงไม่เปลี่ยนแปลง

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}