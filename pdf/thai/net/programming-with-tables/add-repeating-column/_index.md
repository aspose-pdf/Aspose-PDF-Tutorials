---
"description": "เรียนรู้วิธีเพิ่มคอลัมน์ที่ซ้ำกันในเอกสาร PDF โดยใช้ Aspose.PDF สำหรับ .NET คำแนะนำทีละขั้นตอนพร้อมตัวอย่างและโค้ด เหมาะสำหรับนักพัฒนา"
"linktitle": "เพิ่มคอลัมน์ที่ซ้ำกันในเอกสาร PDF"
"second_title": "เอกสารอ้างอิง Aspose.PDF สำหรับ API ของ .NET"
"title": "เพิ่มคอลัมน์ที่ซ้ำกันในเอกสาร PDF"
"url": "/th/net/programming-with-tables/add-repeating-column/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เพิ่มคอลัมน์ที่ซ้ำกันในเอกสาร PDF

## การแนะนำ

หากคุณกำลังทำงานกับเอกสาร PDF และจำเป็นต้องเพิ่มคอลัมน์ที่ซ้ำกัน คุณมาถูกที่แล้ว! การใช้ Aspose.PDF สำหรับ .NET ช่วยให้คุณจัดการตารางและเนื้อหาภายใน PDF ได้อย่างง่ายดาย ไม่ว่าคุณจะกำลังสร้างรายงานแบบไดนามิก ใบแจ้งหนี้ หรือเอกสารที่มีโครงสร้างอื่น ๆ คอลัมน์ที่ซ้ำกันสามารถเปลี่ยนแปลงรูปแบบการจัดระเบียบข้อมูลได้ มาดูคำแนะนำทีละขั้นตอนเกี่ยวกับวิธีเพิ่มคอลัมน์ที่ซ้ำกันในเอกสาร PDF กัน

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเริ่มเขียนโค้ด เรามาตรวจสอบก่อนว่าคุณได้ตั้งค่าทุกอย่างเรียบร้อยแล้ว:

- Aspose.PDF สำหรับ .NET: คุณต้องติดตั้งไลบรารี Aspose.PDF สำหรับ .NET ไว้ในโปรเจ็กต์ของคุณ
- [ดาวน์โหลด Aspose.PDF สำหรับ .NET](https://releases.aspose.com/pdf/net/)
- [ทดลองใช้งานฟรี](https://releases.aspose.com/)
- สภาพแวดล้อมการพัฒนา: ตรวจสอบให้แน่ใจว่าคุณมี IDE ที่เข้ากันได้กับ .NET เช่น Visual Studio ติดตั้งอยู่
- ความเข้าใจพื้นฐานเกี่ยวกับ C#: แม้ว่าเราจะแยกทุกอย่างออก แต่ความเข้าใจพื้นฐานเกี่ยวกับ C# จะช่วยให้คุณทำตามได้อย่างราบรื่น
  
หากคุณยังไม่มี Aspose.PDF สำหรับ .NET คุณสามารถรับได้ [ใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/) เพื่อเริ่มสำรวจคุณสมบัติของมัน

## แพ็คเกจนำเข้า

ในการเริ่มต้น คุณต้องนำเข้าเนมสเปซที่จำเป็นจาก Aspose.PDF สำหรับ .NET โดยทำตามขั้นตอนต่อไปนี้:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

แพ็คเกจเหล่านี้มีคลาสและวิธีการที่จำเป็นสำหรับการทำงานกับเอกสาร PDF และจัดการตาราง

ตอนนี้เรามาแบ่งกระบวนการออกเป็นหลายขั้นตอนเพื่อเพิ่มคอลัมน์ที่ซ้ำกันในเอกสาร PDF ทำตามกัน!

## ขั้นตอนที่ 1: ตั้งค่าเส้นทางไปยังไดเรกทอรีเอกสารของคุณ

ก่อนที่เราจะสร้างหรือจัดการไฟล์ใดๆ เราจะต้องกำหนดเส้นทางที่จะบันทึกไฟล์ PDF ที่สร้างขึ้น ในโปรเจ็กต์ C# ของคุณ ให้ตั้งค่าเส้นทางไดเรกทอรีไปยังตำแหน่งที่จะจัดเก็บไฟล์ของคุณ:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "AddRepeatingColumn_out.pdf";
```

เส้นทางนี้ชี้ไปยังไดเรกทอรีที่ไฟล์ PDF เอาต์พุตจะถูกบันทึก แทนที่ `"YOUR DOCUMENT DIRECTORY"` ด้วยเส้นทางจริงบนเครื่องของคุณ

## ขั้นตอนที่ 2: สร้างเอกสาร PDF ใหม่

ในการเริ่มต้น ให้สร้างอินสแตนซ์ใหม่ `Document` วัตถุ ซึ่งจะทำหน้าที่เป็นคอนเทนเนอร์สำหรับหน้าและเนื้อหาทั้งหมดภายใน PDF

```csharp
Document doc = new Document();
Aspose.Pdf.Page page = doc.Pages.Add();
```

ที่นี่เราได้สร้างเอกสาร PDF ใหม่และเพิ่มหน้าว่างเข้าไป `doc.Pages.Add()` วิธีการแทรกหน้าใหม่ลงในเอกสาร

## ขั้นตอนที่ 3: สร้างตัวอย่างตารางด้านนอก

ขั้นต่อไป เราจะสร้างตารางภายนอก ตารางนี้จะครอบคลุมความกว้างทั้งหมดของเพจและทำหน้าที่เป็นคอนเทนเนอร์สำหรับตารางอื่นๆ รวมถึงตารางที่มีคอลัมน์ที่ซ้ำกัน

```csharp
Aspose.Pdf.Table outerTable = new Aspose.Pdf.Table();
outerTable.ColumnWidths = "100%";
outerTable.HorizontalAlignment = HorizontalAlignment.Left;
```

เราได้ตั้งค่าไว้ `ColumnWidths` คุณสมบัติเป็น "100%" หมายความว่าตารางจะยืดออกไปทั่วทั้งความกว้างของหน้า

## ขั้นตอนที่ 4: สร้างตารางภายใน

ตอนนี้เรามาสร้างตารางด้านในซึ่งจะมีคอลัมน์ที่ซ้ำกัน คุณสมบัติหลักที่นี่คือ `Broken`ซึ่งทำให้ตารางสามารถดำเนินต่อไปบนหน้าเดียวกันได้และ `ColumnAdjustment`ซึ่งจะปรับความกว้างของคอลัมน์ให้พอดีกับเนื้อหาโดยอัตโนมัติ

```csharp
Aspose.Pdf.Table mytable = new Aspose.Pdf.Table();
mytable.Broken = TableBroken.VerticalInSamePage;
mytable.ColumnAdjustment = ColumnAdjustment.AutoFitToContent;
```

ตารางด้านในจะซ้อนอยู่ภายในตารางด้านนอก

## ขั้นตอนที่ 5: เพิ่มตารางลงในหน้า

ตอนนี้เรามีตารางด้านนอกและด้านในพร้อมแล้ว เรามาเพิ่มตารางเหล่านี้ลงในเพจกันเถอะ ขั้นตอนนี้จะช่วยให้มั่นใจว่าตารางจะรวมอยู่ในโครงสร้างของเอกสาร

```csharp
page.Paragraphs.Add(outerTable);
var bodyRow = outerTable.Rows.Add();
var bodyCell = bodyRow.Cells.Add();
bodyCell.Paragraphs.Add(mytable);
mytable.RepeatingColumnsCount = 5;
```

ที่นี่เราได้เพิ่ม `outerTable` ไปที่หน้าแล้วภายในตารางด้านนอกเราซ้อน `mytable`นอกจากนี้เรายังตั้ง `RepeatingColumnsCount` ถึง 5 โดยระบุจำนวนคอลัมน์ที่จะทำซ้ำเมื่อเพิ่มข้อมูล

## ขั้นตอนที่ 6: เพิ่มแถวส่วนหัว

ตอนนี้ถึงเวลาเพิ่มส่วนหัวในตารางแล้ว แถวส่วนหัวจะให้บริบทกับข้อมูลและช่วยจัดโครงสร้างคอลัมน์ 

```csharp
Aspose.Pdf.Row row = mytable.Rows.Add();
row.Cells.Add("header 1");
row.Cells.Add("header 2");
row.Cells.Add("header 3");
row.Cells.Add("header 4");
row.Cells.Add("header 5");
row.Cells.Add("header 6");
row.Cells.Add("header 7");
row.Cells.Add("header 11");
row.Cells.Add("header 12");
row.Cells.Add("header 13");
row.Cells.Add("header 14");
row.Cells.Add("header 15");
row.Cells.Add("header 16");
row.Cells.Add("header 17");
```

คำสั่งสั้นๆ นี้จะเพิ่มแถวแรก (ซึ่งเราจะใช้เป็นส่วนหัว) และเติมด้วยเซลล์ที่มีข้อความ เช่น "ส่วนหัว 1" "ส่วนหัว 2" เป็นต้น

## ขั้นตอนที่ 7: เพิ่มแถวข้อมูล

ในที่สุด เราก็สามารถเพิ่มข้อมูลบางส่วนลงในตารางได้ ลูปนี้จะสร้างแถวและเติมเนื้อหาลงในเซลล์แบบไดนามิก:

```csharp
for (int RowCounter = 0; RowCounter <= 5; RowCounter++)
{
    Aspose.Pdf.Row row1 = mytable.Rows.Add();
    row1.Cells.Add("col " + RowCounter.ToString() + ", 1");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 2");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 3");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 4");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 5");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 6");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 7");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 11");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 12");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 13");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 14");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 15");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 16");
    row1.Cells.Add("col " + RowCounter.ToString() + ", 17");
}
```

ลูปจะวนซ้ำ 6 ครั้ง โดยเพิ่มแถวและเติมแต่ละเซลล์ด้วยข้อมูลคอลัมน์ที่สอดคล้องกัน (เช่น "คอลัมน์ 1, 1" "คอลัมน์ 2, 2" เป็นต้น)

## ขั้นตอนที่ 8: บันทึกเอกสาร

เมื่อเพิ่มแถวและคอลัมน์ทั้งหมดแล้ว ขั้นตอนสุดท้ายคือการบันทึกเอกสารไปยังเส้นทางไฟล์ที่ระบุ

```csharp
doc.Save(outFile);
```

เอกสารของคุณได้รับการบันทึกด้วยคอลัมน์ที่ทำซ้ำแล้ว!

## บทสรุป

เท่านี้คุณก็สร้างเอกสาร PDF ที่มีคอลัมน์ซ้ำกันได้โดยใช้ Aspose.PDF สำหรับ .NET ด้วยขั้นตอนง่ายๆ เหล่านี้ โดยใช้ประโยชน์จากความยืดหยุ่นของตารางที่ซ้อนกัน คุณสามารถสร้างเค้าโครงที่ซับซ้อนที่ทำให้ PDF ของคุณดูเป็นมืออาชีพและเป็นระเบียบ ลองใช้สิ่งนี้สำหรับโปรเจ็กต์ถัดไปของคุณและสำรวจศักยภาพทั้งหมดของ Aspose.PDF ในการจัดการความต้องการสร้าง PDF ของคุณ

## คำถามที่พบบ่อย

### Aspose.PDF สำหรับ .NET คืออะไร?
Aspose.PDF สำหรับ .NET เป็นไลบรารีอันทรงพลังที่ช่วยให้นักพัฒนาสามารถสร้าง แก้ไข และจัดการเอกสาร PDF ได้ด้วยโปรแกรม

### ฉันสามารถปรับจำนวนคอลัมน์ที่ทำซ้ำแบบไดนามิกได้หรือไม่
ใช่ คุณสามารถเปลี่ยนจำนวนคอลัมน์ที่ทำซ้ำได้โดยการแก้ไข `RepeatingColumnsCount` คุณสมบัติ.

### ฉันจะสมัครใบอนุญาตสำหรับ Aspose.PDF สำหรับ .NET ได้อย่างไร
คุณสามารถสมัครใบอนุญาตจากไฟล์หรือสตรีมได้โดยทำตามขั้นตอนต่อไปนี้ [เอกสารประกอบ](https://reference-aspose.com/pdf/net/).

### สามารถเพิ่มรูปภาพลงในเซลล์ตารางได้หรือไม่?
ใช่ Aspose.PDF สำหรับ .NET รองรับการเพิ่มเนื้อหาประเภทต่างๆ รวมทั้งรูปภาพลงในเซลล์ตาราง

### ฉันสามารถปรับแต่งเค้าโครงตารางเพิ่มเติมได้หรือไม่
แน่นอน! Aspose.PDF มีฟีเจอร์มากมายในการปรับแต่งรูปแบบตาราง รวมถึงขอบ การเติมช่องว่าง การจัดตำแหน่ง และอื่นๆ อีกมากมาย

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}