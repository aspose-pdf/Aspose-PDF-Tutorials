---
"description": "เรียนรู้วิธีซ่อนหมายเลขหน้าในสารบัญโดยใช้ Aspose.PDF สำหรับ .NET ทำตามคำแนะนำโดยละเอียดนี้พร้อมตัวอย่างโค้ดเพื่อสร้าง PDF แบบมืออาชีพ"
"linktitle": "ซ่อนหมายเลขหน้าในสารบัญ"
"second_title": "เอกสารอ้างอิง Aspose.PDF สำหรับ API ของ .NET"
"title": "ซ่อนหมายเลขหน้าในสารบัญ"
"url": "/th/net/programming-with-document/hidepagenumbersintoc/"
"weight": 220
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ซ่อนหมายเลขหน้าในสารบัญ

## การแนะนำ

เมื่อคุณทำงานกับ PDF บางครั้งคุณอาจต้องการสร้างสารบัญ (TOC) แต่ต้องการให้ทุกอย่างดูสวยงามด้วยการซ่อนหมายเลขหน้า บางทีเอกสารอาจไหลลื่นขึ้นหากไม่มีหมายเลขหน้า หรือบางทีอาจเป็นเพราะความสวยงามก็ได้ ไม่ว่าเหตุผลของคุณจะเป็นอย่างไร หากคุณกำลังทำงานกับ Aspose.PDF สำหรับ .NET บทช่วยสอนนี้จะแสดงให้คุณเห็นอย่างชัดเจนว่าต้องซ่อนหมายเลขหน้าในสารบัญอย่างไร

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มต้น มีบางสิ่งที่คุณต้องมี นี่คือรายการตรวจสอบอย่างรวดเร็ว:

- ติดตั้ง Visual Studio แล้ว: คุณจะต้องมี Visual Studio เวอร์ชันที่ใช้งานได้เพื่อเขียนโค้ด
- ไลบรารี Aspose.PDF สำหรับ .NET: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารี Aspose.PDF สำหรับ .NET แล้ว
  - ลิงค์ดาวน์โหลด: [Aspose.PDF สำหรับ .NET](https://releases.aspose.com/pdf/net/)
- ใบอนุญาตชั่วคราว: หากคุณกำลังทดสอบคุณสมบัติต่างๆ การมีใบอนุญาตชั่วคราวก็จะเป็นประโยชน์
  - ใบอนุญาตชั่วคราว: [รับได้ที่นี่](https://purchase.aspose.com/temporary-license/)

## แพ็คเกจนำเข้า

ก่อนจะเริ่มเขียนโค้ด ให้แน่ใจว่าคุณได้นำเข้าเนมสเปซต่อไปนี้ในโปรเจ็กต์ C# ของคุณแล้ว ซึ่งเนมสเปซเหล่านี้จะมีคลาสและวิธีการที่จำเป็นสำหรับการทำงานกับเอกสาร PDF และการสร้างสารบัญ (TOC)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

ตอนนี้สภาพแวดล้อมของคุณพร้อมแล้วและแพ็กเกจก็นำเข้าแล้ว มาดูขั้นตอนต่างๆ ของกระบวนการกัน เราจะอธิบายทุกส่วนของโค้ดเพื่อให้แน่ใจว่ามีความชัดเจน คุณจึงทำตามได้ง่าย

## ขั้นตอนที่ 1: เริ่มต้นเอกสาร PDF ของคุณ

สิ่งแรกที่เราต้องทำคือสร้างเอกสาร PDF ใหม่และเพิ่มหน้าสำหรับสารบัญ (TOC)


```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "HiddenPageNumbers_out.pdf";
Document doc = new Document();
Page tocPage = doc.Pages.Add();
```

- dataDir: นี่คือไดเร็กทอรีที่ไฟล์เอาต์พุตของคุณจะถูกบันทึก
- Document(): เริ่มต้นเอกสาร PDF ใหม่
- Pages.Add(): เพิ่มหน้าว่างใหม่ลงในเอกสาร ซึ่งภายหลังจะเก็บ TOC ของคุณไว้

## ขั้นตอนที่ 2: ตั้งค่าข้อมูล TOC และชื่อเรื่อง

ต่อไปเราจะกำหนดข้อมูล TOC รวมถึงกำหนดชื่อเรื่องที่จะปรากฏที่ด้านบนของ TOC

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocPage.TocInfo = tocInfo;
```

- TocInfo: อ็อบเจ็กต์นี้เก็บข้อมูลทั้งหมดเกี่ยวกับ TOC
- TextFragment: แสดงข้อความในหัวข้อ TOC ในที่นี้เราตั้งค่าเป็น "สารบัญ"
- FontStyle: เรากำหนดสไตล์ของชื่อ TOC โดยตั้งขนาดเป็น 20 และทำตัวหนา
- tocPage.TocInfo: เรากำหนดข้อมูล TOC ให้กับหน้าที่จะแสดง TOC

## ขั้นตอนที่ 3: ซ่อนหมายเลขหน้าใน TOC

ตอนนี้มาถึงส่วนสนุก ๆ แล้ว! เราจะกำหนดค่า TOC เพื่อซ่อนหมายเลขหน้าในที่นี้

```csharp
tocInfo.IsShowPageNumbers = false;
tocInfo.FormatArrayLength = 4;
```

- IsShowPageNumbers: นี่คือสวิตช์วิเศษที่ซ่อนหมายเลขหน้า ตั้งค่าเป็น `false`และหมายเลขหน้าจะไม่ปรากฏใน TOC
- FormatArrayLength: เราตั้งค่านี้เป็น 4 ซึ่งระบุว่าเราต้องการกำหนดการจัดรูปแบบให้กับหัวข้อ TOC สี่ระดับ

## ขั้นตอนที่ 4: ปรับแต่งรูปแบบ TOC

เพื่อเพิ่มรูปแบบให้กับ TOC ของคุณ เราจะกำหนดการจัดรูปแบบสำหรับหัวเรื่องในระดับต่างๆ กัน

```csharp
tocInfo.FormatArray[0].Margin.Right = 0;
tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
tocInfo.FormatArray[1].Margin.Left = 30;
tocInfo.FormatArray[1].TextState.Underline = true;
tocInfo.FormatArray[1].TextState.FontSize = 10;
tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;
tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;
```

- FormatArray: อาร์เรย์นี้ควบคุมการจัดรูปแบบของรายการ TOC โดยดัชนีแต่ละรายการจะแสดงระดับหัวเรื่องที่แตกต่างกัน
- ระยะขอบและรูปแบบข้อความ: เราตั้งค่าระยะขอบและใช้รูปแบบตัวอักษรเช่น ตัวหนา ตัวเอียง และขีดเส้นใต้ ให้กับระดับหัวเรื่องแต่ละระดับ

## ขั้นตอนที่ 5: เพิ่มหัวข้อลงในเอกสาร

สุดท้ายนี้ เรามาเพิ่มหัวข้อจริง ๆ ที่จะเป็นส่วนหนึ่งของ TOC กัน

```csharp
Page page = doc.Pages.Add();
for (int Level = 1; Level != 5; Level++)
{ 
    Heading heading2 = new Heading(Level); 
    TextSegment segment2 = new TextSegment(); 
    heading2.TocPage = tocPage; 
    heading2.Segments.Add(segment2); 
    heading2.IsAutoSequence = true; 
    segment2.Text = "this is heading of level " + Level; 
    heading2.IsInList = true; 
    page.Paragraphs.Add(heading2); 
}
```

- ส่วนหัวและส่วนข้อความ: แสดงถึงส่วนหัวที่จะปรากฏใน TOC ของคุณ แต่ละระดับจะมีส่วนหัวของตัวเอง
- IsAutoSequence: กำหนดหมายเลขหัวเรื่องโดยอัตโนมัติ
- IsInList: ทำให้แน่ใจว่าหัวข้อแต่ละหัวข้อปรากฏใน TOC

## ขั้นตอนที่ 6: บันทึกเอกสาร

เมื่อทุกอย่างพร้อมแล้ว ให้บันทึกเอกสาร PDF ลงในไฟล์เอาต์พุตที่คุณระบุ

```csharp
doc.Save(outFile);
```

และเสร็จเรียบร้อย! คุณได้สร้าง PDF พร้อมสารบัญสำเร็จแล้ว และหมายเลขหน้าก็ถูกซ่อนไว้!

## บทสรุป

การสร้างสารบัญใน PDF และการซ่อนหมายเลขหน้าอาจดูยุ่งยาก แต่ด้วย Aspose.PDF สำหรับ .NET จะทำให้ทุกอย่างง่ายดายขึ้น ด้วยการทำตามคำแนะนำทีละขั้นตอนนี้ คุณจะได้เรียนรู้วิธีปรับแต่งรูปแบบ TOC ซ่อนหมายเลขหน้า และใช้รูปแบบต่างๆ กับหัวเรื่องของคุณ ตอนนี้คุณสามารถสร้าง PDF แบบมืออาชีพที่ปรับแต่งตามความต้องการของคุณได้

## คำถามที่พบบ่อย

### ฉันสามารถแสดงหมายเลขหน้าสำหรับหัวเรื่องเฉพาะใน TOC ได้หรือไม่
ไม่ Aspose.PDF จะซ่อนหรือแสดงหมายเลขหน้าสำหรับ TOC ทั้งหมด คุณไม่สามารถซ่อนหมายเลขหน้าสำหรับรายการเฉพาะเจาะจงได้

### สามารถเพิ่มระดับให้กับ TOC ได้อีกหรือไม่?
ใช่ คุณสามารถเพิ่มได้ `FormatArrayLength` เพื่อกำหนดระดับหัวข้อ TOC ให้มากขึ้น

### ฉันจะเปลี่ยนแบบอักษรสำหรับรายการ TOC ทั้งหมดได้อย่างไร
คุณสามารถเปลี่ยนแบบอักษรได้โดยการแก้ไข `TextState.Font` ทรัพย์สินของแต่ละระดับใน `FormatArray`-

### ฉันสามารถแทรกไฮเปอร์ลิงก์ลงใน TOC ได้หรือไม่?
ใช่ คุณสามารถเชื่อมโยงรายการ TOC แต่ละรายการกับส่วนเฉพาะในเอกสารโดยใช้ `Heading.TocPage` คุณสมบัติ.

### ฉันต้องมีใบอนุญาตสำหรับ Aspose.PDF หรือไม่?
ใช่ ต้องมีใบอนุญาตที่ถูกต้องสำหรับการใช้ในการผลิต คุณสามารถขอใบอนุญาตชั่วคราวได้ [ที่นี่](https://purchase.aspose.com/temporary-license/) เพื่อทดสอบคุณสมบัติ

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}