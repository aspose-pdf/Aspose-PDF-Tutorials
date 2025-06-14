---
"description": "เรียนรู้วิธีค้นหาข้อความและเพิ่มไฮเปอร์ลิงก์ใน PDF โดยใช้ Aspose.PDF สำหรับ .NET ด้วยบทช่วยสอนทีละขั้นตอนของเรา"
"linktitle": "ค้นหาข้อความและเพิ่มไฮเปอร์ลิงก์"
"second_title": "เอกสารอ้างอิง Aspose.PDF สำหรับ API ของ .NET"
"title": "ค้นหาข้อความและเพิ่มไฮเปอร์ลิงก์"
"url": "/th/net/programming-with-text/search-text-and-add-hyperlink/"
"weight": 450
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ค้นหาข้อความและเพิ่มไฮเปอร์ลิงก์

## การแนะนำ

คุณกำลังมองหาวิธีที่จะไม่เพียงแต่จัดการ PDF แต่ยังปรับปรุง PDF ด้วยการแทรกไฮเปอร์ลิงก์หรือไม่? ใช่แล้ว คุณมาถูกที่แล้ว! ด้วยไลบรารี Aspose.PDF สำหรับ .NET ที่มีประสิทธิภาพ คุณสามารถค้นหารูปแบบข้อความในเอกสาร PDF และเพิ่มไฮเปอร์ลิงก์ได้อย่างราบรื่น ลองนึกภาพว่ามีเอกสารที่ไม่เพียงแต่ถ่ายทอดข้อมูลเท่านั้น แต่ยังเชื่อมโยงผู้อ่านกับแหล่งข้อมูลที่เกี่ยวข้องได้ด้วยการคลิกลิงก์ ฟังดูดีใช่ไหม? ในบทช่วยสอนนี้ เราจะแนะนำคุณทีละขั้นตอนเกี่ยวกับวิธีการค้นหาข้อความโดยใช้นิพจน์ทั่วไปและเพิ่มไฮเปอร์ลิงก์ใน PDF ของคุณ ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น คุณจะพบว่ากระบวนการนี้ง่ายและคุ้มค่า

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกรายละเอียด เรามาตรวจสอบกันก่อนว่าคุณมีทุกอย่างที่จำเป็นในการปฏิบัติตาม นี่คือรายการตรวจสอบที่มีประโยชน์:

- .NET Framework: คุณควรติดตั้ง .NET framework ไว้ในเครื่องของคุณ (เวอร์ชัน 4.0 ขึ้นไป)
- Aspose.PDF สำหรับไลบรารี .NET: อย่าลืมดาวน์โหลดและเพิ่มการอ้างอิงไปยังไลบรารี Aspose.PDF ในโปรเจ็กต์ของคุณ คุณสามารถค้นหาได้ [ที่นี่](https://releases-aspose.com/pdf/net/).
- IDE: คุณจะต้องมีสภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE) เช่น Visual Studio เพื่อเขียนและรันโค้ด
- ไฟล์ PDF ตัวอย่าง: ดาวน์โหลดไฟล์ PDF ตัวอย่างที่คุณสามารถทดสอบโค้ดได้ คุณสามารถสร้าง PDF ง่ายๆ หรือใช้เอกสารที่มีอยู่ของคุณก็ได้

เมื่อคุณได้ทำเครื่องหมายทุกอย่างในรายการนี้เรียบร้อยแล้ว เราก็พร้อมที่จะเริ่มดำเนินการ!

## แพ็คเกจนำเข้า

ขั้นตอนแรกในการเดินทางของเราคือการนำเข้าแพ็คเกจที่จำเป็น นี่คือขั้นตอนที่เราแจ้งให้โครงการของเราทราบว่าเราจะใช้เครื่องมือใด คุณสามารถทำได้ดังนี้:

ในไฟล์ C# ของคุณ เริ่มต้นด้วยการรวมเนมสเปซต่อไปนี้ไว้ที่ด้านบน:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System;
```

เมื่อคุณนำเข้าเนมสเปซเหล่านี้ คุณจะให้โปรแกรมของคุณเข้าถึงฟีเจอร์เจ๋งๆ ทั้งหมดที่ Aspose.PDF นำเสนอ

ตอนนี้เราก็พร้อมแล้ว ถึงเวลาลงมือทำจริง เราจะอธิบายทีละขั้นตอน ดังนั้นโปรดติดตามอย่างใกล้ชิด!

### ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีเอกสารของคุณ

ขั้นแรก คุณจะต้องระบุตำแหน่งจัดเก็บไฟล์ PDF ของคุณ แก้ไข `dataDir` ตัวแปรที่จะชี้ไปยังไดเร็กทอรีของเอกสารของคุณ คุณสามารถทำได้ดังนี้:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

อย่าลืมเปลี่ยน `"YOUR DOCUMENT DIRECTORY"` พร้อมเส้นทางจริงไปยังเอกสารของคุณ

### ขั้นตอนที่ 2: สร้าง TextFragmentAbsorber

ต่อไปเราจะต้องมีเครื่องมือในการค้นหาข้อความที่เราต้องการลิงก์ ป้อน `TextFragmentAbsorber`เจ้าตัวน้อยนี้จะช่วยเราค้นหารูปแบบข้อความเฉพาะใน PDF ของเรา

```csharp
TextFragmentAbsorber absorber = new TextFragmentAbsorber("\\d{4}-\\d{4}");
```

ที่นี่เรากำลังมองหารูปแบบที่เฉพาะเจาะจง: สี่หลัก เครื่องหมายขีดกลาง ตามด้วยสี่หลักอีก (เช่น หมายเลขโทรศัพท์หรือปี)

### ขั้นตอนที่ 3: เปิดใช้งานการค้นหาด้วยนิพจน์ทั่วไป

เรากำลังใช้นิพจน์ทั่วไปเพื่อค้นหารูปแบบข้อความของเราอยู่แล้ว แต่เราต้องแน่ใจว่า `absorber` รู้ว่ามีการเปิดใช้งานแล้ว ซึ่งเป็นสิ่งสำคัญเพื่อให้ค้นหาได้อย่างถูกต้อง

```csharp
absorber.TextSearchOptions = new TextSearchOptions(true);
```

### ขั้นตอนที่ 4: เริ่มต้นใช้งาน PdfContentEditor

ตอนนี้เรามีตัวดูดซับพร้อมแล้ว เราต้อง `PdfContentEditor` เพื่อทำงานกับไฟล์ PDF ของเรา คลาสนี้ช่วยให้เราผูกเข้ากับ PDF และจัดการไฟล์ได้

```csharp
PdfContentEditor editor = new PdfContentEditor();
```

### ขั้นตอนที่ 5: ผูกไฟล์ PDF ต้นฉบับของคุณ

เมื่อตัวแก้ไขเนื้อหาของเราพร้อมแล้ว ก็ถึงเวลาที่จะผูกเข้ากับไฟล์ PDF จริงที่เราต้องการใช้งาน

```csharp
editor.BindPdf(dataDir + "SearchRegularExpressionPage.pdf");
```

อย่าลืมเปลี่ยน `"SearchRegularExpressionPage.pdf"` พร้อมชื่อไฟล์ PDF ของคุณ

### ขั้นตอนที่ 6: ยอมรับตัวดูดซับสำหรับหน้า

เราต้องแจ้งให้บรรณาธิการทราบว่าเราต้องการค้นหาในหน้าใดหน้าหนึ่งของเอกสาร ในกรณีนี้ เราจะไปที่หน้า 1

```csharp
editor.Document.Pages[1].Accept(absorber);
```

### ขั้นตอนที่ 7: เตรียมการวนซ้ำผ่านชิ้นส่วนข้อความ

ตอนนี้ เราพร้อมที่จะวนซ้ำผ่านข้อความทั้งหมดที่พบโดยตัวดูดซับของเราแล้ว เราจะปรับแต่งรูปลักษณ์ของข้อความและตั้งค่าไฮเปอร์ลิงก์ของเรา

```csharp
int[] dashArray = { };
String[] LEArray = { };
Color blue = Color.Blue;
```

ที่นี่ เรากำลังตั้งค่าพารามิเตอร์บางอย่าง เช่น สีของไฮเปอร์ลิงก์ของเรา

### ขั้นตอนที่ 8: วนซ้ำผ่านแต่ละส่วนของข้อความ

สำหรับข้อความทุกส่วนที่ตรงกับการค้นหา เราจะเปลี่ยนสีและสร้างไฮเปอร์ลิงก์ มีลักษณะดังนี้:

```csharp
foreach (TextFragment textFragment in absorber.TextFragments)
{
    textFragment.TextState.ForegroundColor = Aspose.Pdf.Color.Blue;
    Rectangle rect = new Rectangle((int)textFragment.Rectangle.LLX,
        (int)Math.Round(textFragment.Rectangle.LLY), (int)Math.Round(textFragment.Rectangle.Width + 2),
        (int)Math.Round(textFragment.Rectangle.Height + 1));
    Enum[] actionName = new Enum[2] { Aspose.Pdf.Annotations.PredefinedAction.Document_AttachFile, Aspose.Pdf.Annotations.PredefinedAction.Document_ExtractPages };
    
    editor.CreateWebLink(rect, "http://www.aspose.com", 1, สีน้ำเงิน, actionName);
    editor.CreateLine(rect, "", (float)textFragment.Rectangle.LLX + 1, (float)textFragment.Rectangle.LLY - 1,
        (float)textFragment.Rectangle.URX, (float)textFragment.Rectangle.LLY - 1, 1, 1, blue, "S", dashArray, LEArray);
}
```

### ขั้นตอนที่ 9: บันทึก PDF ที่แก้ไขแล้ว

เกือบจะเสร็จแล้ว! ตอนนี้ถึงเวลาบันทึกการเปลี่ยนแปลงของเราลงในไฟล์ PDF ใหม่

```csharp
dataDir = dataDir + "SearchTextAndAddHyperlink_out.pdf";
editor.Save(dataDir);
```

### ขั้นตอนที่ 10: ปิดตัวแก้ไข

สุดท้ายอย่าลืมปิดเอกสารของคุณเพื่อปล่อยทรัพยากร!

```csharp
editor.Close();
Console.WriteLine("\nText replaced and hyperlink added successfully based on a regular expression.\nFile saved at " + dataDir);
```

ตอนนี้คุณได้สร้าง PDF ที่มีไฮเปอร์ลิงก์ที่สร้างขึ้นแบบไดนามิกตามผลการค้นหาแล้ว เจ๋งดีใช่ไหมล่ะ?

## บทสรุป

และแล้วคุณก็ทำได้! ด้วยการทำตามขั้นตอนเหล่านี้ คุณจะได้เรียนรู้วิธีค้นหาใน PDF และเพิ่มไฮเปอร์ลิงก์โดยใช้ไลบรารี Aspose.PDF สำหรับ .NET ซึ่งสามารถเปิดโลกแห่งความเป็นไปได้ โดยเฉพาะอย่างยิ่งหากคุณกำลังทำงานกับเอกสารที่ต้องมีปฏิสัมพันธ์ ลองจินตนาการถึงการเพิ่มลิงก์ไปยังแหล่งข้อมูลที่เกี่ยวข้อง เว็บไซต์อ้างอิง หรือแม้แต่หน้าภายใน โดยใช้โค้ดเพียงไม่กี่บรรทัด!
## คำถามที่พบบ่อย

### Aspose.PDF สำหรับ .NET คืออะไร?  
Aspose.PDF สำหรับ .NET เป็นไลบรารีที่ช่วยให้นักพัฒนาสามารถสร้าง จัดการ และจัดการเอกสาร PDF ในแอปพลิเคชัน .NET ได้

### ฉันสามารถดาวน์โหลด Aspose.PDF สำหรับ .NET ได้อย่างไร  
คุณสามารถดาวน์โหลดห้องสมุดได้ [ที่นี่](https://releases-aspose.com/pdf/net/).

### ฉันสามารถทดลองใช้ Aspose.PDF ฟรีได้หรือไม่?  
แน่นอน! คุณสามารถทดลองใช้งานฟรีได้ [ที่นี่](https://releases-aspose.com/).

### มีการสนับสนุนสำหรับผลิตภัณฑ์ Aspose หรือไม่  
ใช่ คุณสามารถค้นหาการสนับสนุนและการสนทนาของชุมชนได้ [ที่นี่](https://forum-aspose.com/c/pdf/10).

### ฉันจะขอใบอนุญาตชั่วคราวสำหรับ Aspose.PDF ได้อย่างไร  
คุณสามารถขอใบอนุญาตชั่วคราวได้ [ที่นี่](https://purchase-aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}