---
"date": "2025-04-11"
"description": "เรียนรู้วิธีการเพิ่มและปรับแต่ง TOC พร้อมด้วยหมายเลขหน้าในเอกสาร PDF ของคุณอย่างมีประสิทธิภาพโดยใช้ Aspose.PDF สำหรับ .NET เพื่อเพิ่มประสิทธิภาพการนำทางเอกสาร"
"title": "วิธีการเพิ่มสารบัญพร้อมหมายเลขหน้าในไฟล์ PDF โดยใช้ Aspose.PDF .NET"
"url": "/th/net/bookmarks-navigation/add-toc-page-numbers-aspose-pdf-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# วิธีการเพิ่มสารบัญพร้อมหมายเลขหน้าในไฟล์ PDF โดยใช้ Aspose.PDF .NET

## การแนะนำ

ในยุคดิจิทัลทุกวันนี้ การจัดการเอกสารยาวๆ อย่างมีประสิทธิภาพถือเป็นสิ่งสำคัญ ไม่ว่าคุณจะจัดการกับรายงาน คู่มือ หรือเอกสารวิชาการ การมีสารบัญ (TOC) ที่จัดระบบอย่างดีจะช่วยเพิ่มการใช้งานได้อย่างมาก คู่มือนี้สาธิตวิธีการเพิ่มและปรับแต่งสารบัญพร้อมหมายเลขหน้าในไฟล์ PDF โดยใช้ Aspose.PDF สำหรับ .NET ซึ่งเป็นไลบรารีอันทรงพลังที่ออกแบบมาสำหรับการจัดการ PDF ในแอปพลิเคชัน .NET

**สิ่งที่คุณจะได้เรียนรู้:**
- การตั้งค่า Aspose.PDF สำหรับ .NET
- การโหลดเอกสาร PDF ที่มีอยู่ลงในแอปพลิเคชันของคุณ
- การสร้างและปรับแต่ง TOC ด้วยหมายเลขหน้า
- การบันทึกไฟล์ PDF ที่ถูกแก้ไข

พร้อมที่จะปรับปรุงการจัดการเอกสารของคุณหรือยัง มาเริ่มกันเลย!

### ข้อกำหนดเบื้องต้น

ก่อนที่จะดำเนินการต่อ ให้แน่ใจว่าคุณมี:
- **ห้องสมุดและแหล่งอ้างอิง**:Aspose.PDF สำหรับ .NET รวมอยู่ในโครงการของคุณ
- **การตั้งค่าสภาพแวดล้อม**:สภาพแวดล้อมการพัฒนา .NET (เช่น Visual Studio)
- **ข้อกำหนดเบื้องต้นของความรู้**:ความเข้าใจพื้นฐานเกี่ยวกับ C# และการจัดการไฟล์ในแอปพลิเคชัน .NET

### การตั้งค่า Aspose.PDF สำหรับ .NET

#### การติดตั้ง
ในการเริ่มต้น ให้เพิ่มไลบรารี Aspose.PDF ลงในโปรเจ็กต์ของคุณโดยใช้วิธีใดวิธีหนึ่งต่อไปนี้:

**.NET CLI:**
```bash
dotnet add package Aspose.PDF
```

**ตัวจัดการแพ็กเกจ:**
```powershell
Install-Package Aspose.PDF
```

**UI ตัวจัดการแพ็กเกจ NuGet:**
ค้นหา "Aspose.PDF" และติดตั้งเวอร์ชันล่าสุด

#### การขอใบอนุญาต
คุณสามารถเริ่มต้นด้วยการทดลองใช้ฟรีเพื่อสำรวจความสามารถของ Aspose.PDF หากต้องการใช้งานแบบขยายเวลา โปรดพิจารณาซื้อใบอนุญาตชั่วคราวหรือซื้อใบอนุญาตหนึ่งใบ เยี่ยมชม [การซื้อ Aspose](https://purchase.aspose.com/buy) เพื่อดูรายละเอียดเพิ่มเติมในการซื้อใบอนุญาต

### คู่มือการใช้งาน

เมื่อตั้งค่าทุกอย่างเสร็จเรียบร้อยแล้ว ให้เพิ่ม TOC แบบกำหนดเองพร้อมหมายเลขหน้าลงในเอกสาร PDF ของคุณ

#### โหลดและแก้ไขเอกสาร PDF
ขั้นแรก ให้โหลดเอกสาร PDF ที่มีอยู่แล้วลงในแอปพลิเคชันของคุณ จากนั้นเราจะแทรกหน้าใหม่ที่จุดเริ่มต้นของเอกสารนี้สำหรับ TOC ของเรา

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string inFile = "YOUR_DOCUMENT_DIRECTORY/42824.pdf";
string outFile = "YOUR_OUTPUT_DIRECTORY/42824_out.pdf";

// โหลดเอกสาร PDF
document doc = new Document(inFile);

// แทรกหน้าใหม่ในตอนต้นของ TOC
Aspose.Pdf.Page tocPage = doc.Pages.Insert(1);
```

#### การสร้างและกำหนดค่าข้อมูลสารบัญ
ขั้นตอนต่อไป ให้กำหนดค่า TOC ของคุณโดยตั้งชื่อเรื่อง ขนาดตัวอักษร รูปแบบ และคำนำหน้าหมายเลขหน้า

```csharp
// ตั้งค่าข้อมูล TOC
tocInfo tocInfo = new TocInfo();
textFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20; // ขนาดตัวอักษรสำหรับหัวข้อ TOC
title.TextState.FontStyle = FontStyles.Bold; // สไตล์ตัวหนาเพื่อเน้นย้ำ
tocInfo.Title = title;
tocInfo.PageNumbersPrefix = "P"; // ใส่หมายเลขหน้านำหน้าด้วย 'P'
tocPage.TocInfo = tocInfo; // กำหนดข้อมูล TOC ให้กับหน้าใหม่
```

#### เพิ่มรายการลงในสารบัญ
ตอนนี้ให้เพิ่มรายการลงใน TOC สำหรับแต่ละหน้าในเอกสารของคุณ

```csharp
for (int i = 1; i < doc.Pages.Count; i++) {
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
textSegment segment2 = new textSegment();

    // เชื่อมโยงหัวข้อกับหน้า TOC
    heading2.TocPage = tocPage;

    // เพิ่มส่วนข้อความลงในหัวเรื่อง
    heading2.Segments.Add(segment2); 

    // ตั้งค่าหน้าปลายทางและตำแหน่งสำหรับแต่ละรายการ
    heading2.DestinationPage = doc.Pages[i + 1];
    heading2.Top = doc.Pages[i + 1].Rect.Height; 
    segment2.Text = "P" + i.ToString(); // ข้อความที่กำหนดเองโดยมีคำนำหน้า 'P'

    // เพิ่มหัวข้อลงในหน้า TOC
    tocPage.Paragraphs.Add(heading2);
}
```

#### บันทึกเอกสาร PDF ที่แก้ไขแล้ว
สุดท้าย ให้บันทึกเอกสารที่คุณแก้ไขโดยใช้ TOC ที่เพิ่มเข้ามาใหม่

```csharp
doc.Save(outFile);
```

### การประยุกต์ใช้งานจริง

การเพิ่ม TOC ที่กำหนดเองสามารถปรับปรุงการนำทางเอกสารได้อย่างมีนัยสำคัญในสถานการณ์ต่างๆ:
1. **บทความวิชาการ**:เข้าถึงส่วนต่างๆ ของเอกสารวิจัยยาวๆ ได้อย่างรวดเร็ว
2. **คู่มือการใช้งาน**:ปรับปรุงประสบการณ์ผู้ใช้ด้วยการให้สามารถข้ามไปยังคำแนะนำหรือหัวข้อที่เจาะจงได้อย่างรวดเร็ว
3. **รายงานและข้อเสนอ**:ช่วยให้สามารถอ้างอิงได้อย่างง่ายดายในระหว่างการนำเสนอหรือการทบทวน

### การพิจารณาประสิทธิภาพ

เมื่อทำงานกับไฟล์ PDF ขนาดใหญ่ ควรพิจารณาสิ่งต่อไปนี้เพื่อประสิทธิภาพสูงสุด:
- **การจัดการหน่วยความจำที่มีประสิทธิภาพ**:กำจัดสิ่งของทันทีหลังใช้งานเพื่อประหยัดทรัพยากร
- **การประมวลผลแบบแบตช์**:จัดการเอกสารหลายฉบับเป็นชุดหากเป็นไปได้เพื่อปรับปรุงกระบวนการทำงาน
- **การดำเนินการแบบอะซิงโครนัส**:ใช้การทำงานแบบอะซิงโครนัสในกรณีที่เหมาะสมเพื่อหลีกเลี่ยงการบล็อกการทำงาน

### บทสรุป

ในบทช่วยสอนนี้ คุณจะได้เรียนรู้วิธีปรับปรุงเอกสาร PDF ของคุณโดยการเพิ่มสารบัญแบบกำหนดเองพร้อมหมายเลขหน้าโดยใช้ Aspose.PDF สำหรับ .NET ความสามารถนี้ไม่เพียงแต่ช่วยปรับปรุงการนำทางเอกสารเท่านั้น แต่ยังปรับปรุงประสบการณ์โดยรวมของผู้ใช้ด้วย

หากต้องการสำรวจความสามารถของ Aspose.PDF สำหรับ .NET เพิ่มเติม โปรดพิจารณาเจาะลึกคุณลักษณะและการบูรณาการที่ซับซ้อนมากขึ้นเมื่อคุณคุ้นเคยกับพื้นฐานแล้ว

### ส่วนคำถามที่พบบ่อย

**1. ฉันสามารถปรับแต่งลักษณะของ TOC เพิ่มเติมได้หรือไม่**
ใช่ คุณสามารถปรับเปลี่ยนรูปแบบของแบบอักษร สี และแม้กระทั่งใช้รูปแบบการกำหนดหมายเลขแบบกำหนดเองเพื่อปรับแต่งลักษณะของ TOC ได้

**2. จะเกิดอะไรขึ้นหาก PDF ของฉันมีบุ๊กมาร์กอยู่แล้ว?**
โค้ดที่ให้มาเน้นไปที่การเพิ่ม TOC แต่คุณสามารถรวมเข้ากับบุ๊กมาร์กที่มีอยู่ได้โดยการแก้ไขการตั้งค่าปลายทางตามนั้น

**3. ฉันจะจัดการไฟล์ PDF ที่เข้ารหัสหรือป้องกันด้วยรหัสผ่านได้อย่างไร**
ก่อนที่จะประมวลผลไฟล์ดังกล่าว ให้ใช้กระบวนการถอดรหัสของ Aspose.PDF เพื่อปลดล็อกเพื่อแก้ไข

**4. แนวทางนี้เหมาะสำหรับการประมวลผลเอกสารหลายชุดเป็นชุดหรือไม่**
แน่นอน! คุณสามารถวนซ้ำผ่านไดเร็กทอรีของ PDF และใช้ตรรกะเดียวกันกับแต่ละไฟล์ได้อย่างมีประสิทธิภาพ

**5. ฉันสามารถรวมฟังก์ชันนี้เข้ากับแอปพลิเคชั่นเว็บได้หรือไม่**
ใช่ Aspose.PDF สำหรับ .NET ทำงานได้ดีในสภาพแวดล้อมเว็บ เช่น ASP.NET โดยช่วยให้คุณประมวลผล PDF ได้แบบทันที

### ทรัพยากร
- **เอกสารประกอบ**- [Aspose.PDF สำหรับเอกสาร .NET](https://reference.aspose.com/pdf/net/)
- **ดาวน์โหลด**- [เวอร์ชันล่าสุดของ Aspose.PDF สำหรับ .NET](https://releases.aspose.com/pdf/net/)
- **ซื้อ**- [ซื้อใบอนุญาต](https://purchase.aspose.com/buy)
- **ทดลองใช้งานฟรี**- [เริ่มต้นด้วยการทดลองใช้ฟรี](https://releases.aspose.com/pdf/net/)
- **ใบอนุญาตชั่วคราว**- [รับใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/)
- **ฟอรั่มสนับสนุน**- [เข้าร่วมชุมชน Aspose](https://forum.aspose.com/c/pdf/10)

เราหวังว่าคู่มือนี้จะเป็นประโยชน์ในการปรับปรุงความสามารถในการจัดการเอกสาร PDF ของคุณ ขอให้สนุกกับการเขียนโค้ด!


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}