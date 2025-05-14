---
"date": "2025-04-11"
"description": "เรียนรู้วิธีการเพิ่มวันที่และเวลาหรือคำอธิบายประกอบลงในเอกสาร PDF อย่างมีประสิทธิภาพโดยใช้ Aspose.PDF สำหรับ .NET ปรับปรุงการจัดการเอกสารด้วยขั้นตอนที่ทำตามได้ง่ายเหล่านี้"
"title": "เพิ่มวันที่และเวลาลงใน PDF โดยใช้ Aspose.PDF สำหรับ .NET"
"url": "/th/net/document-manipulation/aspose-pdf-net-date-time-stamps-annotations/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# เพิ่มวันที่และเวลาลงใน PDF โดยใช้ Aspose.PDF สำหรับ .NET

## การแนะนำ

ในยุคดิจิทัลทุกวันนี้ การจัดการเอกสารอย่างมีประสิทธิภาพถือเป็นสิ่งสำคัญสำหรับธุรกิจและบุคคล การเพิ่มวันที่และเวลาหรือคำอธิบายประกอบลงใน PDF ของคุณสามารถปรับปรุงความสมบูรณ์และการจัดระเบียบข้อมูลได้ บทช่วยสอนนี้สาธิตวิธีการผสานรวมคุณลักษณะเหล่านี้โดยใช้ Aspose.PDF สำหรับ .NET

**ประเด็นสำคัญ:**
- เพิ่มวันที่และเวลาปัจจุบันเป็นแสตมป์ข้อความบนหน้า PDF ที่ระบุ
- สร้างคำอธิบายข้อความอิสระในตำแหน่งที่ต้องการในเอกสาร
- ปฏิบัติตามแนวทางปฏิบัติที่ดีที่สุดเพื่อประสิทธิภาพสูงสุดด้วย Aspose.PDF สำหรับ .NET

## ข้อกำหนดเบื้องต้น
ก่อนที่จะเริ่มต้น ให้แน่ใจว่าคุณมี:

### ไลบรารีและเวอร์ชันที่จำเป็น
- **Aspose.PDF สำหรับ .NET**:ไลบรารีที่แข็งแกร่งสำหรับการจัดการ PDF โดยไม่ต้องใช้ Adobe Acrobat ใช้เวอร์ชัน 21.x ขึ้นไป

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
- สภาพแวดล้อมการพัฒนาที่มี .NET Framework 4.5+ หรือ .NET Core 2.0+
- Visual Studio หรือ IDE อื่นที่รองรับการเขียนโปรแกรม C#

### ข้อกำหนดเบื้องต้นของความรู้
- ความเข้าใจพื้นฐานเกี่ยวกับโครงสร้างโครงการ C# และ .NET
- ความคุ้นเคยกับการจัดการไฟล์ในโครงสร้างไดเร็กทอรี

## การตั้งค่า Aspose.PDF สำหรับ .NET
ติดตั้ง Aspose.PDF โดยใช้หนึ่งในวิธีต่อไปนี้:

**การใช้ .NET CLI:**
```bash
dotnet add package Aspose.PDF
```

**การใช้ตัวจัดการแพ็คเกจ:**
```powershell
Install-Package Aspose.PDF
```

**ผ่านทาง UI ของตัวจัดการแพ็คเกจ NuGet:**
- เปิดตัวจัดการแพ็คเกจ NuGet ใน IDE ของคุณ
- ค้นหา "Aspose.PDF" และติดตั้งเวอร์ชันล่าสุด

### ขั้นตอนการรับใบอนุญาต
วิธีใช้งาน Aspose.PDF ให้เต็มประสิทธิภาพ:
1. **ทดลองใช้งานฟรี:** ดาวน์โหลดใบอนุญาตชั่วคราวเพื่อสำรวจคุณสมบัติทั้งหมด
2. **ใบอนุญาตชั่วคราว:** ขอใบอนุญาตประเมินผลแบบขยายเวลาหากจำเป็น
3. **ซื้อ:** ซื้อใบอนุญาตสำหรับการใช้งานระยะยาวจากเว็บไซต์ Aspose

เริ่มต้นใบอนุญาตของคุณในรหัส:
```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to License File");
```

## คู่มือการใช้งาน
มาเพิ่มวันที่และเวลาลงใน PDF กัน

### คุณสมบัติ 1: เพิ่มแสตมป์วันที่และเวลาลงใน PDF
คุณลักษณะนี้จะเพิ่มวันที่และเวลาปัจจุบันเป็นตราประทับข้อความบนหน้าแรกของเอกสาร PDF ที่ระบุ

#### การดำเนินการแบบทีละขั้นตอน

##### 1. เปิดเอกสาร PDF ที่มีอยู่
โหลดเอกสารเป้าหมายของคุณ:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/AddTextStamp.pdf");
```

##### 2. รับวันที่และเวลาปัจจุบันเป็นสตริง
รูปแบบวันที่และเวลาปัจจุบัน:
```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

##### 3. สร้างแสตมป์ข้อความพร้อมวันที่และเวลาปัจจุบัน
สร้าง `TextStamp` อินสแตนซ์ที่ใช้สตริงที่จัดรูปแบบ:
```csharp
TextStamp textStamp = new TextStamp(annotationText);
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

##### 4. เพิ่มตราประทับข้อความลงในหน้าแรก
เพิ่มตราประทับบนหน้าแรกของเอกสารของคุณ:
```csharp
document.Pages[1].AddStamp(textStamp);
```

##### 5. สร้างและเพิ่ม FreeTextAnnotation (ทางเลือก)
สำหรับคำอธิบายประกอบที่ซับซ้อนมากขึ้น ให้สร้าง `FreeTextAnnotation`-
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(document.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance)
{
    Name = "Stamp",
    Contents = textStamp.Value
};
textAnnotation.Border = new Border(textAnnotation) { Width = 0 };
document.Pages[1].Annotations.Add(textAnnotation);
```

##### 6. บันทึกเอกสารที่แก้ไข
บันทึกการเปลี่ยนแปลงของคุณ:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/AddDateTimeStamp_out.pdf";
document.Save(outputDir);
```

### คุณสมบัติที่ 2: เพิ่มคำอธิบาย FreeText บน PDF
เพิ่มคำอธิบายข้อความอิสระในตำแหน่งใดก็ได้ตามต้องการภายในเอกสาร PDF

#### การดำเนินการแบบทีละขั้นตอน

##### 1. เปิดเอกสาร PDF ที่มีอยู่
โหลดเอกสารเป้าหมายของคุณ:
```csharp
document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/Sample.pdf");
```

##### 2. กำหนดพื้นที่สี่เหลี่ยมผืนผ้าสำหรับคำอธิบายประกอบ
ระบุตำแหน่งที่จะวางคำอธิบายบนหน้า:
```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(100, 400, 200, 450);
```

##### 3. สร้าง FreeTextAnnotation พร้อมระบุลักษณะและตำแหน่ง
เริ่มต้นคำอธิบายของคุณด้วยการตั้งค่าข้อความและลักษณะที่ต้องการ:
```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 12, System.Drawing.Color.Blue);
FreeTextAnnotation freeTextAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], rect, default_appearance)
{
    Contents = "This is a sample annotation",
    Title = "Sample Annotation"
};
```

##### 4. ตั้งค่ารูปแบบขอบและเพิ่มคำอธิบาย
ตรวจสอบให้แน่ใจว่ารูปแบบขอบตรงกับความต้องการของคุณ (มองไม่เห็นในกรณีนี้):
```csharp
freeTextAnnotation.Border = new Border(freeTextAnnotation) { Width = 0 };
pdfDocument.Pages[1].Annotations.Add(freeTextAnnotation);
```

##### 5. บันทึกเอกสารที่แก้ไข
บันทึกเอกสารของคุณด้วยคำอธิบายประกอบที่เพิ่มใหม่:
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY/FreeTextAnnotation_out.pdf";
document.Save(outputDir);
```

## การประยุกต์ใช้งานจริง
การเพิ่มตราประทับวันที่และคำอธิบายลงใน PDF มีประโยชน์ในหลายอุตสาหกรรม:
- **เอกสารทางกฎหมาย**:รับประกันความสอดคล้องโดยการประทับเวลาการเปลี่ยนแปลง
- **บทความวิชาการ**:อำนวยความสะดวกในการแก้ไขร่วมกันด้วยคำอธิบายประกอบ
- **บันทึกทางการเงิน**:รักษาเส้นทางการตรวจสอบที่แม่นยำพร้อมรายงานที่มีการประทับเวลา
- **เอกสารทางเทคนิค**:ไฮไลท์การอัปเดตหรือหมายเหตุสำคัญในคู่มือ

## การพิจารณาประสิทธิภาพ
เพื่อประสิทธิภาพสูงสุดเมื่อใช้ Aspose.PDF สำหรับ .NET:
- **การประมวลผลแบบแบตช์**ประมวลผล PDF หลายไฟล์เป็นชุดเพื่อลดค่าใช้จ่าย
- **การจัดการหน่วยความจำ**: ใช้ `Dispose` วิธีการเพิ่มทรัพยากรหน่วยความจำหลังจากประมวลผลเอกสารแต่ละฉบับ
- **แบบอักษรและรูปภาพที่ได้รับการเพิ่มประสิทธิภาพ**จำกัดประเภทแบบอักษรและความละเอียดของภาพเพื่อลดขนาดไฟล์

## บทสรุป
การรวม Aspose.PDF สำหรับ .NET ช่วยให้คุณสามารถเพิ่มคุณลักษณะการประทับวันที่และคำอธิบายประกอบลงในเอกสาร PDF ซึ่งช่วยเพิ่มการใช้งาน เครื่องมือเหล่านี้ช่วยปรับปรุงความสมบูรณ์ของข้อมูลและปรับปรุงการจัดการเอกสารให้มีประสิทธิภาพมากขึ้น

ทดลองใช้การกำหนดค่าที่แตกต่างกันและสำรวจคุณลักษณะเพิ่มเติมที่ Aspose.PDF จัดทำขึ้นเพื่อตอบสนองความต้องการเฉพาะของคุณ

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}