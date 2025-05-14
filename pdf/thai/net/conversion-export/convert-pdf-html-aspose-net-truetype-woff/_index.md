---
"date": "2025-04-10"
"description": "เรียนรู้วิธีแปลงไฟล์ PDF เป็น HTML โดยใช้ Aspose.PDF สำหรับ .NET โดยยังคงรักษาฟอนต์ในรูปแบบ TrueType (TTF) และ Web Open Font Format (WOFF) คำแนะนำทีละขั้นตอนพร้อมตัวอย่างโค้ด"
"title": "แปลง PDF เป็น HTML ด้วย Aspose.PDF สำหรับ .NET และรักษาฟอนต์ในรูปแบบ TTF และ WOFF"
"url": "/th/net/conversion-export/convert-pdf-html-aspose-net-truetype-woff/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# แปลง PDF เป็น HTML ด้วย Aspose.PDF สำหรับ .NET: รักษาแบบอักษรในรูปแบบ TTF และ WOFF

## การแนะนำ
กำลังดิ้นรนเพื่อรักษาเค้าโครงเดิมและความสมบูรณ์ของแบบอักษรของเอกสาร PDF ของคุณเมื่อแปลงเป็น HTML หรือไม่ การแปลง PDF ในขณะที่รักษาแบบอักษรไว้อาจเป็นเรื่องท้าทาย แต่ก็ไม่จำเป็นต้องเป็นเช่นนั้น **Aspose.PDF สำหรับ .NET**คุณสามารถแปลงไฟล์ PDF เป็นรูปแบบ HTML ได้อย่างง่ายดาย โดยยังคงรักษาแบบอักษรไว้ในรูปแบบ TrueType (TTF) หรือ Web Open Font Format (WOFF) คู่มือนี้จะแนะนำคุณทีละขั้นตอนในกระบวนการ

ในบทช่วยสอนนี้เราจะครอบคลุม:
- วิธีการบันทึกแบบอักษรเป็น TTF เมื่อแปลง PDF เป็น HTML
- การกำหนดค่าการแปลงของคุณเพื่อบันทึกแบบอักษรเป็น WOFF
- บันทึกแบบอักษรในทุกรูปแบบระหว่างการแปลง

เมื่ออ่านบทความนี้จบ คุณจะเข้าใจอย่างครอบคลุมเกี่ยวกับการใช้ Aspose.PDF สำหรับ .NET เพื่อจัดการการแปลงฟอนต์อย่างมีประสิทธิภาพ มาเจาะลึกข้อกำหนดเบื้องต้นที่จำเป็นก่อนเริ่มต้นกันเลย

## ข้อกำหนดเบื้องต้น
ก่อนที่จะดำเนินการแปลงไฟล์ PDF เป็น HTML ด้วย Aspose.PDF โปรดตรวจสอบให้แน่ใจว่าคุณปฏิบัติตามข้อกำหนดเหล่านี้:

### ไลบรารีและการอ้างอิงที่จำเป็น
- **Aspose.PDF สำหรับ .NET**:ไลบรารีนี้มีความจำเป็นสำหรับการประมวลผลไฟล์ PDF ในแอปพลิเคชัน .NET
- **.NET Framework หรือ .NET Core/5+**: ตรวจสอบให้แน่ใจว่าสภาพแวดล้อมการพัฒนาของคุณรองรับกรอบงานเหล่านี้

### ข้อกำหนดการตั้งค่าสภาพแวดล้อม
ตรวจสอบให้แน่ใจว่าสภาพแวดล้อมการพัฒนาของคุณ (เช่น Visual Studio) ได้รับการตั้งค่าให้ทำงานกับไลบรารี Aspose.PDF คุณจะต้องมี:
- โครงการที่สร้างขึ้นใน .NET Framework หรือ .NET Core/5+
- การเข้าถึงตัวจัดการแพ็คเกจ NuGet เพื่อติดตั้งไลบรารี

### ข้อกำหนดเบื้องต้นของความรู้
ความเข้าใจพื้นฐานเกี่ยวกับ C# และความคุ้นเคยกับการจัดการไฟล์ใน .NET จะเป็นประโยชน์

## การตั้งค่า Aspose.PDF สำหรับ .NET
ในการเริ่มต้น คุณต้องติดตั้งไลบรารี Aspose.PDF ซึ่งคุณสามารถทำได้ผ่านตัวจัดการแพ็คเกจต่างๆ:

**.NET CLI:**
```bash
dotnet add package Aspose.PDF
```

**คอนโซลตัวจัดการแพ็คเกจ:**
```powershell
Install-Package Aspose.PDF
```

**UI ตัวจัดการแพ็กเกจ NuGet:**
ค้นหา "Aspose.PDF" และติดตั้งเวอร์ชันล่าสุด

### การขอใบอนุญาต
คุณสามารถขอรับใบอนุญาตชั่วคราวหรือซื้อใบอนุญาตฉบับเต็มจาก Aspose ได้ การทดลองใช้ฟรีช่วยให้คุณสำรวจฟีเจอร์ทั้งหมดได้โดยไม่มีข้อจำกัด จึงเหมาะอย่างยิ่งสำหรับการประเมินเบื้องต้น ต่อไปนี้เป็นวิธีตั้งค่าสภาพแวดล้อมของคุณด้วยใบอนุญาต:
1. ขอคำร้อง [ใบอนุญาตชั่วคราว](https://purchase-aspose.com/temporary-license/).
2. ใช้ใบอนุญาตในแอปพลิเคชันของคุณโดยใช้ตัวอย่างโค้ดต่อไปนี้ก่อนที่จะดำเนินการใด ๆ:

```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to your License File");
```

## คู่มือการใช้งาน
มาแบ่งการใช้งานออกเป็นสามคุณสมบัติหลัก: บันทึกฟอนต์เป็น TTF, WOFF และรูปแบบอื่นๆ

### บันทึกแบบอักษรเป็น TTF
**ภาพรวม**
ฟีเจอร์นี้ช่วยให้คุณบันทึกแบบอักษรจากเอกสาร PDF ในรูปแบบ TrueType (TTF) ได้ในขณะแปลงเป็น HTML ซึ่งจะทำให้มั่นใจได้ว่าแบบอักษรของคุณจะคงความสมบูรณ์ในระหว่างการแปลง

#### การดำเนินการแบบทีละขั้นตอน
1. **เริ่มต้นเอกสารและตัวเลือก:**
   เริ่มต้นด้วยการโหลดเอกสาร PDF ของคุณโดยใช้ Aspose.PDF `Document` ชั้นเรียนและการตั้งค่า `HtmlSaveOptions`-

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   string outFile = Path.GetFullPath(dataDir + "/36192_out.html");
   Document doc = new Document(dataDir + "/input.pdf");

   HtmlSaveOptions saveOptions = new HtmlSaveOptions();
   ```

2. **กำหนดค่าตัวเลือกการบันทึก:**
   ตั้งค่าตัวเลือกที่จำเป็นเพื่อรักษาเค้าโครงและระบุโหมดการบันทึกแบบอักษร

   ```csharp
   saveOptions.FixedLayout = true; // รักษาเค้าโครง PDF ดั้งเดิมไว้
   saveOptions.SplitIntoPages = false; // อย่าแยกไฟล์ออกเป็นหลายไฟล์ HTML
   saveOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.AlwaysSaveAsTTF;
   ```

3. **เตรียมไดเรกทอรีผลลัพธ์:**
   ตรวจสอบให้แน่ใจว่าไดเร็กทอรีเอาต์พุตพร้อมที่จะจัดเก็บไฟล์ฟอนต์ที่เชื่อมโยง

   ```csharp
   string linkedFilesFolder = Path.GetDirectoryName(outFile) + "/36192_files";
   if (Directory.Exists(linkedFilesFolder))
   {
       Directory.Delete(linkedFilesFolder, true); // ล้างไฟล์ที่มีอยู่
   }
   ```

4. **บันทึกเอกสาร:**
   สุดท้ายให้บันทึกเอกสารของคุณด้วยตัวเลือกที่ระบุ

   ```csharp
doc.Save(outFile, saveOptions);
```

### Save Fonts as WOFF
**Overview**
Configuring Aspose.PDF to save fonts in Web Open Font Format (WOFF) is beneficial for web optimization, reducing font file sizes while maintaining quality.

#### Step-by-Step Implementation
1. **Configure Save Options:**
   Initialize `HtmlSaveOptions` and set the font saving mode to WOFF.

   ```csharp
   HtmlSaveOptions woffSaveOptions = new HtmlSaveOptions();
   woffSaveOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.AlwaysSaveAsWOFF;
   ```

2. **ใช้ตัวเลือกการบันทึก:**
   ใช้ตัวเลือกเหล่านี้เมื่อบันทึกเอกสารของคุณ เช่นเดียวกับวิธี TTF

### บันทึกแบบอักษรในทุกรูปแบบ
**ภาพรวม**
เพื่อให้แน่ใจว่ามีความเข้ากันได้และความยืดหยุ่นสูงสุด คุณอาจต้องการบันทึกแบบอักษรในรูปแบบทั้งหมดที่มีในระหว่างการแปลง

#### การดำเนินการแบบทีละขั้นตอน
1. **เริ่มต้นเอกสารและตัวเลือก:**
   โหลดเอกสาร PDF และกำหนดค่า `HtmlSaveOptions`-

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   Document doc = new Document(dataDir + "/input.pdf");
   HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
   ```

2. **กำหนดค่าตัวเลือกการบันทึก:**
   ตั้งค่าตัวเลือกเพื่อบันทึกรูปแบบฟอนต์ทั้งหมดและรักษาเค้าโครงไว้

   ```csharp
   htmlOptions.FixedLayout = true;
   htmlOptions.RasterImagesSavingMode = HtmlSaveOptions.RasterImagesSavingModes.AsExternalPngFilesReferencedViaSvg;
   htmlOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.SaveInAllFormats;
   ```

3. **บันทึกเอกสาร:**
   บันทึกเอกสารของคุณด้วยการตั้งค่าเหล่านี้

   ```csharp
doc.Save(dataDir + "/ThreeSetFonts_out.html", htmlOptions);
```

## Practical Applications
Converting PDFs to HTML with font preservation has numerous real-world applications:
1. **Web Publishing**: Ensure that documents retain their original styling when published online.
2. **Content Portability**: Easily move content between desktop and web environments without loss of formatting.
3. **Document Archiving**: Maintain document integrity during long-term storage or migration.

Integration possibilities include embedding these conversions into CMS systems, automated reporting tools, or digital libraries for seamless font management across platforms.

## Performance Considerations
When using Aspose.PDF for .NET, consider the following tips to optimize performance:
- **Memory Management**: Dispose of objects properly and utilize `using` statements where applicable.
- **Batch Processing**: Process documents in batches if dealing with large volumes to prevent memory overflow.
- **Resource Optimization**: Configure options like image compression and font subsetting to reduce file sizes.

## Conclusion
We've explored how to convert PDFs to HTML while preserving fonts using Aspose.PDF for .NET. Whether saving fonts as TTF, WOFF, or all formats, these techniques ensure your documents maintain their original design and readability in web environments. 

For further exploration, consider diving into Aspose's extensive documentation or experimenting with additional conversion features offered by the library.

## FAQ Section
1. **What are the benefits of converting PDFs to HTML using Aspose.PDF?**
   - Maintains document layout and font integrity.
   - Facilitates web publishing and content portability.
2. **Can I convert large PDF files efficiently with Aspose.PDF?**
   - Yes, by optimizing memory usage and processing in batches.
3. **How do I handle licensing for Aspose.PDF?**
   - Obtain a temporary or full license from the [Aspose website](https://purchase.aspose.com/buy).
4. **Is it possible to customize font settings during conversion?**
   - Yes, through various `HtmlSaveOptions`.
5. **What are some common issues when converting PDFs and how can I address them?**
   - Common issues include missing fonts or layout discrepancies. Adjusting save options and ensuring proper licensing can help mitigate these problems.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}