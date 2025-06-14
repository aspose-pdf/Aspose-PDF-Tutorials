---
"description": "เรียนรู้วิธีการส่งออกข้อมูลเวิร์กชีต Excel ไปยังตาราง PDF โดยใช้ Aspose.PDF สำหรับ .NET บทช่วยสอนแบบทีละขั้นตอนพร้อมตัวอย่างโค้ด ข้อกำหนดเบื้องต้น และเคล็ดลับที่เป็นประโยชน์"
"linktitle": "การส่งออกข้อมูลเวิร์กชีต Excel ไปยังตาราง"
"second_title": "เอกสารอ้างอิง Aspose.PDF สำหรับ API ของ .NET"
"title": "การส่งออกข้อมูลเวิร์กชีต Excel ไปยังตาราง"
"url": "/th/net/programming-with-tables/export-excel-worksheet-data-to-table/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การส่งออกข้อมูลเวิร์กชีต Excel ไปยังตาราง

## การแนะนำ

คุณเคยจำเป็นต้องส่งออกข้อมูลจากเวิร์กชีต Excel ไปยังไฟล์ PDF ที่จัดเรียงอย่างเรียบร้อยในรูปแบบตารางหรือไม่ ลองนึกภาพว่ามีข้อมูลจำนวนมากใน Excel แต่จำเป็นต้องแชร์เป็น PDF ที่ดูเป็นมืออาชีพ ดูสิ อาจฟังดูซับซ้อนใช่ไหม แต่ด้วย Aspose.PDF สำหรับ .NET คุณสามารถทำให้ภารกิจนี้กลายเป็นเรื่องง่ายได้ ในบทช่วยสอนนี้ เราจะแนะนำคุณเกี่ยวกับกระบวนการส่งออกข้อมูลเวิร์กชีต Excel ไปยังตารางภายในเอกสาร PDF โดยใช้ Aspose.PDF สำหรับ .NET เราจะอธิบายขั้นตอนต่างๆ ให้คุณทราบทีละขั้นตอน เพื่อให้แม้ว่าคุณจะเป็นมือใหม่ แต่คุณจะรู้สึกเหมือนเป็นผู้เชี่ยวชาญเมื่อทำเสร็จ

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกการเข้ารหัส เรามาตั้งค่าบางสิ่งบางอย่างกันก่อน:

1. Aspose.PDF สำหรับไลบรารี .NET – ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งเวอร์ชันล่าสุดแล้ว คุณสามารถ [ดาวน์โหลดได้ที่นี่](https://releases-aspose.com/pdf/net/).
2. Aspose.Cells สำหรับไลบรารี .NET – คุณจะต้องใช้สิ่งนี้เพื่อจัดการการทำงานของ Excel ดาวน์โหลดได้จาก [ที่นี่](https://releases-aspose.com/cells/net/).
3. สภาพแวดล้อมการพัฒนา .NET – เครื่องมือเช่น Visual Studio จะทำงานอย่างสมบูรณ์แบบสำหรับการเขียนโค้ด
4. ไฟล์ Excel – มีไฟล์ Excel ที่มีข้อมูลที่คุณต้องการส่งออกให้พร้อมใช้งาน

หากคุณไม่มีไลบรารี Aspose.PDF และ Aspose.Cells คุณสามารถเริ่มต้นด้วย [ทดลองใช้งานฟรี](https://releases-aspose.com/).

## แพ็คเกจนำเข้า

ในการเริ่มต้น ให้แน่ใจว่าคุณได้ติดตั้งไลบรารี Aspose.PDF และ Aspose.Cells ไว้ในโปรเจ็กต์ของคุณแล้ว คุณสามารถติดตั้งได้โดยใช้ตัวจัดการแพ็กเกจ NuGet ใน Visual Studio

วิธีการนำเข้าแพ็คเกจที่จำเป็นลงในโค้ด C# ของคุณมีดังนี้:

```csharp
using System.Data;
using System.IO;
using System.Linq;
```

ตอนนี้เมื่อกำหนดข้อกำหนดเบื้องต้นเรียบร้อยแล้ว มาดูขั้นตอนการส่งออกข้อมูลจากแผ่นงาน Excel ไปยังตารางในเอกสาร PDF กัน

## ขั้นตอนที่ 1: โหลดสมุดงาน Excel

ในการเริ่มต้น คุณต้องโหลดเวิร์กบุ๊ก Excel ของคุณลงในโปรแกรม ในขั้นตอนนี้ เราจะใช้ Aspose.Cells เพื่อเปิดไฟล์ Excel

```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "YOUR DOCUMENT DIRECTORY";

// โหลดสมุดงาน Excel
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(new FileStream(dataDir + "newBook1.xlsx", FileMode.Open));
```

คำอธิบาย: ที่นี่ เราจะระบุเส้นทางไดเร็กทอรีที่ไฟล์ Excel ของเราตั้งอยู่และโหลดเวิร์กบุ๊กโดยใช้ `Aspose.Cells.Workbook`. อย่าลืมปรับให้เหมาะสม `"YOUR DOCUMENT DIRECTORY"` เพื่อชี้ไปยังตำแหน่งไฟล์ของคุณ

## ขั้นตอนที่ 2: เข้าถึงแผ่นงานแรก

หลังจากโหลดเวิร์กบุ๊กแล้ว เราต้องเข้าถึงเวิร์กชีตแรกซึ่งจัดเก็บข้อมูลของเราไว้

```csharp
// การเข้าถึงเวิร์กชีตแรกในไฟล์ Excel
Aspose.Cells.Worksheet worksheet = workbook.Worksheets[0];
```

คำอธิบาย: ขั้นตอนนี้ตรงไปตรงมามาก—เราหยิบเวิร์กชีตแรกจากเวิร์กบุ๊กซึ่งมีข้อมูลที่จะส่งออก

## ขั้นตอนที่ 3: ส่งออกข้อมูลไปยัง DataTable

ตอนนี้ให้เราส่งออกข้อมูลจากแผ่นงาน Excel ไปยังวัตถุ DataTable ซึ่งจะทำหน้าที่เป็นตัวกลางในการถ่ายโอนข้อมูลไปยัง PDF

```csharp
// การส่งออกเนื้อหา 7 แถวและ 2 คอลัมน์เริ่มจากเซลล์ที่ 1 ไปยัง DataTable
DataTable dataTable = worksheet.Cells.ExportDataTable(0, 0, worksheet.Cells.MaxRow + 1, worksheet.Cells.MaxColumn + 1, true);
```

คำอธิบาย : `ExportDataTable` วิธีการนี้จะดึงข้อมูลโดยเริ่มจากเซลล์แรกของเวิร์กชีตและครอบคลุมทุกแถวและคอลัมน์ จากนั้นข้อมูลนี้จะถูกเก็บไว้ใน `DataTable` เพื่อใช้งานต่อไป.

## ขั้นตอนที่ 4: สร้างเอกสาร PDF ใหม่

ต่อไปเราต้องสร้างเอกสาร PDF ใหม่โดยใช้ Aspose.PDF

```csharp
// สร้างอินสแตนซ์เอกสาร
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();

// สร้างหน้าในอินสแตนซ์เอกสาร
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

คำอธิบาย: ที่นี่เราจะเริ่มต้นใหม่ `Aspose.Pdf.Document` และเพิ่มหน้าเข้าไป ในหน้านั้นจะมีตารางที่เราสร้างจากข้อมูล Excel ในภายหลัง

## ขั้นตอนที่ 5: สร้างวัตถุตารางใน PDF

เรามาเริ่มสร้างตารางภายในเอกสาร PDF กันเลย

```csharp
// สร้างวัตถุตาราง
Aspose.Pdf.Table table = new Aspose.Pdf.Table();

// เพิ่มวัตถุตารางลงในคอลเล็กชั่นย่อหน้าของหน้า
page.Paragraphs.Add(table);
```

คำอธิบาย : เราสร้าง `Aspose.Pdf.Table` วัตถุและเพิ่มลงในคอลเล็กชั่นย่อหน้าของหน้าซึ่งจะทำให้แน่ใจว่าตารางจะแสดงบนหน้า

## ขั้นตอนที่ 6: ตั้งค่าความกว้างและขอบของคอลัมน์

ตารางใน PDF ต้องมีความกว้างของคอลัมน์ที่กำหนดไว้ เราจะเพิ่มเส้นขอบเพื่อให้ตารางอ่านได้ง่ายขึ้นด้วย

```csharp
// กำหนดความกว้างของคอลัมน์ของตาราง
table.ColumnWidths = "40 100 100";

// ตั้งค่าเส้นขอบเซลล์เริ่มต้น
table.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

คำอธิบาย: เรากำหนดความกว้างของคอลัมน์ทั้งสามและให้เซลล์ทั้งหมดมีเส้นขอบเริ่มต้นที่มีความหนาเท่ากับ `0-1F`.

## ขั้นตอนที่ 7: นำเข้าข้อมูลจาก DataTable เข้าสู่ตาราง PDF

ตอนนี้ถึงเวลานำเข้าข้อมูลจาก DataTable เข้าสู่ตาราง PDF ของเราแล้ว

```csharp
// นำเข้าข้อมูลลงในวัตถุตารางจาก DataTable
table.ImportDataTable(dataTable, true, 0, 0, dataTable.Rows.Count + 1, dataTable.Columns.Count);
```

คำอธิบาย : `ImportDataTable` วิธีการถ่ายโอนข้อมูลทั้งหมดจาก `DataTable` ไปที่ตาราง PDF การดำเนินการนี้จะทำให้ตารางมีข้อมูลจากแผ่นงาน Excel ของคุณ

## ขั้นตอนที่ 8: จัดรูปแบบแถวส่วนหัว

มาปรับแต่งสไตล์แถวส่วนหัวของตารางโดยการเปลี่ยนสีพื้นหลัง แบบอักษร และการจัดตำแหน่ง

```csharp
// รับแถวแรกจากตาราง
Aspose.Pdf.Row headerRow = table.Rows[0];

// ตั้งค่ารูปแบบสำหรับแถวส่วนหัว
foreach (Aspose.Pdf.Cell cell in headerRow.Cells)
{
    cell.BackgroundColor = Color.Blue;
    cell.DefaultCellTextState.Font = Aspose.Pdf.Text.FontRepository.FindFont("Helvetica-Oblique");
    cell.DefaultCellTextState.ForegroundColor = Color.Yellow;
    cell.DefaultCellTextState.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Center;
}
```

คำอธิบาย: เราวนซ้ำผ่านเซลล์ทั้งหมดในแถวแรก (ส่วนหัว) และตั้งค่าสีพื้นหลังเป็นสีน้ำเงิน สีข้อความเป็นสีเหลือง และจัดตำแหน่งข้อความให้ตรงกลาง

## ขั้นตอนที่ 9: จัดแต่งทรงแถวที่เหลือ

เพื่อแยกความแตกต่างระหว่างส่วนหัวและแถวที่เหลือ เราจะเพิ่มรูปแบบที่แตกต่างกันให้กับแถวที่เหลือ

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++)
{
    foreach (Aspose.Pdf.Cell cell in table.Rows[i].Cells)
    {
        cell.BackgroundColor = Color.Gray;
        cell.DefaultCellTextState.ForegroundColor = Color.White;
    }
}
```

คำอธิบาย: สำหรับทุกแถว ยกเว้นส่วนหัว เราจะกำหนดพื้นหลังสีเทาและสีข้อความเป็นสีขาว

## ขั้นตอนที่ 10: บันทึกเอกสาร PDF

สุดท้ายให้บันทึกเอกสาร PDF พร้อมตาราง

```csharp
// บันทึกไฟล์ PDF
pdfDocument.Save(dataDir + "Exceldata_toPdf_table.pdf");
```

คำอธิบาย: เราบันทึก PDF ลงในไดเร็กทอรีที่ระบุ เท่านี้ข้อมูล Excel ของคุณก็อยู่ในตาราง PDF ที่มีรูปแบบสวยงามแล้ว

## บทสรุป

และแล้วคุณก็ทำได้! เพียงไม่กี่ขั้นตอน คุณก็ส่งออกข้อมูลจากเวิร์กชีต Excel ไปยังตารางภายใน PDF โดยใช้ Aspose.PDF สำหรับ .NET ได้แล้ว คุณสามารถปรับแต่งผลลัพธ์และรับรองว่าข้อมูลของคุณจะดูสะอาดและเป็นมืออาชีพได้ โดยการแบ่งกระบวนการและจัดรูปแบบไปทีละขั้นตอน ดังนั้น ครั้งต่อไปที่ใครสักคนส่งไฟล์ Excel ให้คุณและขอรายงาน PDF คุณจะรู้ทันทีว่าต้องทำอย่างไร

## คำถามที่พบบ่อย

### ฉันสามารถปรับแต่งตารางเพิ่มเติมได้ไหม
แน่นอน! คุณสามารถปรับเปลี่ยนสี แบบอักษร การจัดตำแหน่ง และแม้แต่เพิ่มเส้นขอบให้กับเซลล์ที่ต้องการได้

### Aspose.PDF สำหรับ .NET ฟรีหรือไม่?
มีการให้ทดลองใช้งานฟรี แต่หากต้องการใช้งานแบบขยายเวลา คุณจะต้องมีใบอนุญาต คุณสามารถ [ซื้อที่นี่](https://purchase-aspose.com/buy).

### ฉันสามารถส่งออกเฉพาะแถวและคอลัมน์ที่เจาะจงได้หรือไม่
ใช่ คุณสามารถปรับเปลี่ยนพารามิเตอร์ในได้ `ExportDataTable` วิธีการส่งออกช่วงที่เฉพาะเจาะจง

### วิธีนี้ใช้กับไฟล์ Excel ขนาดใหญ่ได้หรือไม่?
ใช่ Aspose.Cells ได้รับการออกแบบมาเพื่อจัดการกับไฟล์ Excel ขนาดใหญ่อย่างมีประสิทธิภาพ

### ฉันจะเพิ่มหน้าเพิ่มเติมใน PDF ได้อย่างไร?
คุณสามารถใช้ `pdfDocument.Pages.Add()` เพื่อเพิ่มหน้าได้มากเท่าที่คุณต้องการ

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}