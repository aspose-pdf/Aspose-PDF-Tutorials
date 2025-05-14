---
"date": "2025-04-10"
"description": "เรียนรู้การแปลง PDF เป็น HTML โดยใช้ Aspose.PDF สำหรับ .NET เพิ่มการเข้าถึงและการมีส่วนร่วมของเอกสารด้วยตัวเลือกที่ปรับแต่งได้"
"title": "การแปลง PDF เป็น HTML ด้วย Aspose.PDF .NET คู่มือฉบับสมบูรณ์"
"url": "/th/net/conversion-export/aspose-pdf-net-pdf-to-html-conversion/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# การแปลง PDF เป็น HTML ด้วย Aspose.PDF .NET

**คู่มือที่ครอบคลุมเกี่ยวกับการเชี่ยวชาญการเข้าถึงเอกสารและการมีส่วนร่วมผ่านการแปลง**

## การแนะนำ

การแปลงไฟล์ PDF เป็นรูปแบบ HTML สามารถเพิ่มการเข้าถึงเอกสาร ปรับปรุงการมีส่วนร่วมของผู้ใช้ และทำให้เนื้อหาของคุณแชร์ได้ง่ายบนแพลตฟอร์มต่างๆ คู่มือนี้อธิบายวิธีการแปลง PDF เป็น HTML แบบทีละขั้นตอนโดยใช้ Aspose.PDF สำหรับ .NET พร้อมตัวเลือกที่ปรับแต่งได้หลายรายการ

**สิ่งที่คุณจะได้เรียนรู้:**
- สิ่งสำคัญของการแปลง PDF เป็น HTML
- วิธีปรับแต่งการแปลงด้วยคุณสมบัติเฉพาะ
- การประยุกต์ใช้งานจริงและแนวทางปฏิบัติที่ดีที่สุด

ในบทช่วยสอนนี้ เราจะสำรวจฟีเจอร์ต่างๆ เช่น การแปลงพื้นฐาน การจัดการฟอนต์ การสร้าง HTML หลายหน้า การจัดการ SVG การจัดเก็บรูปภาพ ความโปร่งใสของข้อความ การเรนเดอร์เลเยอร์ การปรับเค้าโครง และอื่นๆ อีกมากมาย

### ข้อกำหนดเบื้องต้น (H2)
ก่อนจะเริ่มใช้งานจริง ให้แน่ใจว่าคุณได้ครอบคลุมข้อกำหนดเบื้องต้นต่อไปนี้:

- **ห้องสมุดที่จำเป็น:** คุณต้องติดตั้ง Aspose.PDF สำหรับ .NET ไลบรารีนี้มีอยู่ใน NuGet
- **การตั้งค่าสภาพแวดล้อม:** สภาพแวดล้อมการพัฒนาที่มีการตั้งค่า .NET Core หรือ .NET Framework ถือเป็นสิ่งจำเป็น
- **ข้อกำหนดเบื้องต้นของความรู้:** ความเข้าใจพื้นฐานเกี่ยวกับ C# และความคุ้นเคยกับโครงสร้างเอกสาร PDF จะเป็นประโยชน์

## การตั้งค่า Aspose.PDF สำหรับ .NET (H2)
ในการเริ่มต้น คุณต้องติดตั้งไลบรารี Aspose.PDF ในโปรเจ็กต์ของคุณ คุณสามารถทำได้โดยใช้หนึ่งในวิธีต่อไปนี้:

**การใช้ .NET CLI:**
```bash
dotnet add package Aspose.PDF
```

**การใช้คอนโซลตัวจัดการแพ็คเกจ:**
```powershell
Install-Package Aspose.PDF
```

**UI ตัวจัดการแพ็กเกจ NuGet:** ค้นหา "Aspose.PDF" และติดตั้งเวอร์ชันล่าสุด

### การขอใบอนุญาต
คุณสามารถรับใบอนุญาตชั่วคราวเพื่อสำรวจฟีเจอร์ทั้งหมดโดยไม่มีข้อจำกัด หรืออีกทางหนึ่ง คุณสามารถซื้อใบอนุญาตเต็มรูปแบบได้หากคุณต้องการการเข้าถึงในระยะยาว เยี่ยมชม [หน้าการซื้อของ Aspose](https://purchase.aspose.com/buy) หรือ [หน้าใบอนุญาตชั่วคราว](https://purchase.aspose.com/temporary-license/) สำหรับรายละเอียดเพิ่มเติม

### การเริ่มต้นขั้นพื้นฐาน
เริ่มต้น Aspose.PDF ในโปรเจ็กต์ของคุณโดยสร้างอินสแตนซ์ใหม่ของคลาส Document และโหลดไฟล์ PDF ดังแสดงด้านล่าง:

```csharp
string dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document pdfDocument = new Document(dataDir + "/PDFToHTML.pdf");
```

## คู่มือการใช้งาน (H2)
มาดูรายละเอียดฟีเจอร์ต่างๆ ที่คุณสามารถใช้งานด้วย Aspose.PDF สำหรับ .NET กัน

### การแปลง PDF เป็น HTML ขั้นพื้นฐาน
**ภาพรวม:** แปลงเอกสาร PDF เป็นไฟล์ HTML ได้อย่างง่ายดาย

#### ขั้นตอน:
1. **โหลดเอกสารต้นฉบับ:**
   ```csharp
   using Aspose.Pdf;
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   Document pdfDocument = new Document(dataDir + "/PDFToHTML.pdf");
   ```
2. **บันทึกเป็น HTML:**
   ```csharp
   pdfDocument.Save(dataDir + "/output_out.html", SaveFormat.Html);
   ```

### ไม่รวมทรัพยากรแบบอักษรจากการแปลง
**ภาพรวม:** ปรับแต่งการแปลงของคุณโดยการยกเว้นแบบอักษรเฉพาะ

#### ขั้นตอน:
1. **เริ่มต้น HtmlSaveOptions ด้วยการยกเว้น:**

   ```csharp
   HtmlSaveOptions htmlOptions = new HtmlSaveOptions
   {
       ExplicitListOfSavedPages = new[] { 1 },
       FixedLayout = true,
       CompressSvgGraphicsIfAny = false,
       SaveTransparentTexts = true,
       SaveShadowedTextsAsTransparentTexts = true,
       ExcludeFontNameList = new[] { "ArialMT", "SymbolMT" },
       DefaultFontName = "Comic Sans MS",
       UseZOrder = true,
       LettersPositioningMethod = HtmlSaveOptions.LettersPositioningMethods.UseEmUnitsAndCompensationOfRoundingErrorsInCss,
       PartsEmbeddingMode = HtmlSaveOptions.PartsEmbeddingModes.NoEmbedding,
       RasterImagesSavingMode = HtmlSaveOptions.RasterImagesSavingModes.AsEmbeddedPartsOfPngPageBackground,
       SplitIntoPages = false
   };
   ```
2. **แปลงและบันทึก:**

   ```csharp
   Document pdfDocument = new Document(dataDir + "/PDFToHTML.pdf");
   pdfDocument.Save(dataDir + "/ExcludeFontResources_out.html", htmlOptions);
   ```

### แปลง PDF เป็น HTML หลายหน้า
**ภาพรวม:** แบ่ง PDF หน้าเดียวออกเป็นหน้า HTML หลาย ๆ หน้า

#### ขั้นตอน:
1. **ตั้งค่าตัวเลือกการแยก:**

   ```csharp
   HtmlSaveOptions options = new HtmlSaveOptions();
   options.SplitIntoPages = true;
   ```
2. **ดำเนินการแปลง:**

   ```csharp
   Document pdfDocument = new Document(dataDir + "/PDFToHTML.pdf");
   pdfDocument.Save(dataDir + "/MultiPageHTML_out.html", options);
   ```

### บันทึกไฟล์ SVG ในระหว่างการแปลง
**ภาพรวม:** จัดการกราฟิก SVG โดยบันทึกไว้ในโฟลเดอร์ที่ระบุ

#### ขั้นตอน:
1. **ระบุโฟลเดอร์พิเศษสำหรับ SVG:**

   ```csharp
   HtmlSaveOptions svgOptions = new HtmlSaveOptions();
   svgOptions.SpecialFolderForSvgImages = dataDir;
   ```
2. **ดำเนินการแปลง:**

   ```csharp
   Document doc = new Document(dataDir + "/PDFToHTML.pdf");
   doc.Save(dataDir + "/SaveSVGFiles_out.html", svgOptions);
   ```

### บีบอัดรูปภาพ SVG ในระหว่างการแปลง
**ภาพรวม:** เพิ่มประสิทธิภาพการแปลงของคุณด้วยการบีบอัดภาพ SVG

#### ขั้นตอน:
1. **เปิดใช้งานการบีบอัด SVG:**

   ```csharp
   HtmlSaveOptions options = new HtmlSaveOptions();
   options.CompressSvgGraphicsIfAny = true;
   ```
2. **ดำเนินการกระบวนการ:**

   ```csharp
   Document doc = new Document(dataDir + "/PDFToHTML.pdf");
   doc.Save(dataDir + "/CompressSVGImages_out.html", options);
   ```

### ระบุโฟลเดอร์รูปภาพระหว่างการแปลง
**ภาพรวม:** จัดระเบียบรูปภาพโดยบันทึกไว้ในโฟลเดอร์แยกต่างหาก

#### ขั้นตอน:
1. **ตั้งค่าโฟลเดอร์พิเศษสำหรับรูปภาพ:**

   ```csharp
   HtmlSaveOptions imageOptions = new HtmlSaveOptions();
   imageOptions.SpecialFolderForAllImages = dataDir;
   ```
2. **ดำเนินการแปลง:**

   ```csharp
   Document doc = new Document(dataDir + "/PDFToHTML.pdf");
   doc.Save(dataDir + "/SpecifyingImageFolder_out.html", imageOptions);
   ```

### สร้างไฟล์ถัดไปจาก PDF เป็น HTML
**ภาพรวม:** สร้างไฟล์ HTML แยกต่างหากสำหรับแต่ละหน้าของ PDF

#### ขั้นตอน:
1. **กำหนดค่าตัวเลือกการแยกและมาร์กอัป:**

   ```csharp
   HtmlSaveOptions options = new HtmlSaveOptions();
   options.HtmlMarkupGenerationMode = HtmlSaveOptions.HtmlMarkupGenerationModes.WriteOnlyBodyContent;
   options.SplitIntoPages = true;
   ```
2. **ดำเนินการแปลง:**

   ```csharp
   Document doc = new Document(dataDir + "/PDFToHTML.pdf");
   doc.Save(dataDir + "/CreateSubsequentFiles_out.html", options);
   ```

### การแสดงข้อความโปร่งใสในระหว่างการแปลง
**ภาพรวม:** ให้แน่ใจว่าการแสดงผลข้อความโปร่งใสในผลลัพธ์ HTML ของคุณ

#### ขั้นตอน:
1. **ตั้งค่าตัวเลือกความโปร่งใส:**

   ```csharp
   HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
   htmlOptions.SaveShadowedTextsAsTransparentTexts = true;
   htmlOptions.SaveTransparentTexts = true;
   ```
2. **ดำเนินการแปลง:**

   ```csharp
   Document doc = new Document(dataDir + "/PDFToHTML.pdf");
   doc.Save(dataDir + "/TransparentTextRendering_out.html", htmlOptions);
   ```

### การเรนเดอร์เลเยอร์ระหว่างการแปลง
**ภาพรวม:** เรนเดอร์เอกสาร PDF แยกชั้นเป็น HTML

#### ขั้นตอน:
1. **เปิดใช้งานการเรนเดอร์เลเยอร์:**

   ```csharp
   HtmlSaveOptions layerOptions = new HtmlSaveOptions();
   layerOptions.RenderLayersSeparately = true;
   ```
2. **ดำเนินการแปลง:**

   ```csharp
   Document doc = new Document(dataDir + "/PDFToHTML.pdf");
   doc.Save(dataDir + "/LayerRendering_out.html", layerOptions);
   ```

### ปรับปรุงเค้าโครงด้วยการตั้งค่าแบบกำหนดเอง
**ภาพรวม:** ปรับการตั้งค่าเค้าโครงเพื่อให้ได้ผลลัพธ์ HTML ที่เหมาะสมยิ่งขึ้น

#### ขั้นตอน:
1. **ปรับแต่งตัวเลือกเค้าโครง:**

   ```csharp
   HtmlSaveOptions layoutOptions = new HtmlSaveOptions();
   layoutOptions.PageSetup.AnyPage.Margin.Bottom = 10;
   layoutOptions.PageSetup.AnyPage.Margin.Top = 10;
   ```
2. **ดำเนินการแปลง:**

   ```csharp
   Document doc = new Document(dataDir + "/PDFToHTML.pdf");
   doc.Save(dataDir + "/CustomLayout_out.html", layoutOptions);
   ```

## บทสรุป
หากทำตามคำแนะนำนี้ คุณจะสามารถแปลงเอกสาร PDF เป็น HTML ได้อย่างมีประสิทธิภาพโดยใช้ Aspose.PDF สำหรับ .NET ด้วยตัวเลือกที่ปรับแต่งได้ คุณสามารถปรับแต่งกระบวนการแปลงให้ตรงตามข้อกำหนดเฉพาะได้ ช่วยเพิ่มการเข้าถึงและการมีส่วนร่วมกับเอกสาร


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}