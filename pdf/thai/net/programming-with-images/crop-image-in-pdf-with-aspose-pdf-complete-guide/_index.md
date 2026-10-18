---
category: general
date: 2026-06-08
description: ตัดรูปภาพใน PDF ด้วย Aspose.PDF ใน C#. เรียนรู้วิธีสร้าง PDF ที่มีรูปภาพ,
  บันทึก PDF ที่มีรูปภาพ, และเพิ่มรูปภาพลงใน PDF เพียงไม่กี่บรรทัด.
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: th
og_description: ตัดภาพใน PDF ด้วย Aspose.PDF ใน C#. บทแนะนำนี้แสดงวิธีสร้าง PDF พร้อมภาพ,
  บันทึก PDF พร้อมภาพ, และเพิ่มภาพลงใน PDF อย่างรวดเร็ว.
og_title: ตัดรูปภาพใน PDF ด้วย Aspose.PDF – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: การตัดรูปภาพใน PDF ด้วย Aspose.PDF – คู่มือฉบับสมบูรณ์
url: /th/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ครอบตัดรูปภาพใน PDF ด้วย Aspose.PDF – คู่มือเต็ม

เคยสงสัยไหมว่าจะแก้ **crop image in PDF** อย่างไรโดยไม่ต้องเปิดโปรแกรมแก้ไขกราฟิก? คุณไม่ได้เป็นคนเดียวที่คิดเช่นนั้น ในรายงานหลาย ๆ ฉบับ ใบแจ้งหนี้ หรือ e‑book คุณอาจต้องการเพียงส่วนหนึ่งของรูปภาพ—อาจเป็นมุมโลโก้หรือส่วนของแผนภูมิ—and you want it straight inside the PDF.  

คู่มือนี้จะแสดงให้คุณเห็นอย่างชัดเจน: เราจะ **create PDF with image**, **add image to PDF**, แล้ว **crop image in PDF** ด้วยไลบรารี Aspose.PDF สำหรับ C#. เมื่อเสร็จคุณจะรู้วิธี **save PDF with image** เพื่อที่คุณจะสามารถส่งไฟล์ให้ใครก็ได้.

---

## สิ่งที่คุณต้องการ

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ทำงานกับ .NET Framework 4.6+ ด้วยเช่นกัน)  
- สำเนา **Aspose.PDF for .NET** ที่มีลิขสิทธิ์หรือเวอร์ชันทดลอง (ติดตั้งผ่าน NuGet `Install-Package Aspose.PDF`)  
- ไฟล์รูปภาพ (JPEG/PNG) บนดิสก์ – เราจะเรียกมันว่า `image.jpg`  
- IDE ใดก็ได้ที่คุณชอบ (Visual Studio, Rider, VS Code)

เท่านี้แค่นั้น ไม่ต้องใช้บริการเพิ่มเติมหรือเครื่องมือภายนอก.

---

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และการนำเข้า

แรกเริ่ม ให้สร้างแอปคอนโซลและนำเข้า namespace ที่เราจะใช้ คำสั่ง `using` จะทำให้โค้ดเป็นระเบียบและทำให้ขั้นตอนต่อไปอ่านง่ายขึ้น.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Pro tip:** หากคุณใช้ Visual Studio ให้คลิกขวาที่โปรเจกต์ → *Manage NuGet Packages* → ค้นหา “Aspose.PDF” แล้วติดตั้ง ไลบรารีจะจัดการการวางภาพและการครอปภายในโดยอัตโนมัติ ดังนั้นคุณไม่จำเป็นต้องใช้ไลบรารีภาพจากบุคคลที่สาม.

---

## ขั้นตอนที่ 2: สร้าง PDF พร้อมรูปภาพ

ตอนนี้เราจะ **create pdf with image** จริง ๆ โค้ดสั้นด้านล่างจะสร้าง `Document` ใหม่, เพิ่มหน้าเปล่า, และเตรียมสตรีมรูปภาพ.

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

การรันโค้ดนี้จะให้ไฟล์ PDF ที่มีรูปภาพเต็มขนาดตามที่คุณระบุ เป็นการตรวจสอบเบื้องต้นที่ดีก่อนที่คุณจะเริ่มตัด.

---

## ขั้นตอนที่ 3: วิธีเพิ่มรูปภาพลงใน PDF (และเตรียมการครอป)

หากคุณรู้พื้นที่ที่ต้องการอย่างแม่นยำแล้ว คุณสามารถข้ามขั้นตอนขนาดเต็มและไปที่ส่วน **how to add image to pdf** ได้โดยตรง เมธอด `AddImage` รับพารามิเตอร์สามค่า:

1. **Image stream** – ไบต์ดิบของรูปภาพของคุณ.  
2. **Placement rectangle** – ตำแหน่งบนหน้าเพจที่รูปภาพจะอยู่.  
3. **Crop rectangle** – ส่วนของรูปภาพที่คุณต้องการให้แสดงผลจริง.  

ด้านล่างเป็นเวอร์ชันกระชับที่ทำการวาง **และ** การครอปในคำเรียกเดียว.

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Why this works:** Aspose.PDF ภายในจะแมป `crop rectangle` ไปยังมิติพิกเซลของภาพ แล้วเรนเดอร์เฉพาะส่วนนั้นภายในพื้นที่ `placement` ไม่ต้องประมวลผลบิตแมพเพิ่มเติม ซึ่งหมายความว่าไฟล์ PDF จะมีขนาดเล็ก

---

## ขั้นตอนที่ 4: วิธีครอปรูปภาพใน PDF – ตัวเลือกขั้นสูง

บางครั้งการครอปเป็นสี่ส่วนอาจไม่พอ คุณอาจต้องการสี่เหลี่ยมกำหนดเองหรืออยากรักษาอัตราส่วนของภาพ นี่คือวิธีที่ยืดหยุ่นมากขึ้น:

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**การจัดการกรณีพิเศษ:**  
- **Null streams** – ควรห่อ `FileStream` ด้วยบล็อก `using` เสมอ ตามที่แสดง เพื่อหลีกเลี่ยงการรั่วไหล.  
- **Large images** – หากภาพต้นทางมีขนาดใหญ่ ควรพิจารณาย่อสี่เหลี่ยม `placement` ลง; Aspose จะทำการลดความละเอียดโดยอัตโนมัติ.  
- **Transparent PNGs** – ไลบรารีเคารพช่องอัลฟา ดังนั้นพื้นที่ที่ครอปจะคงความโปร่งใส.

---

## ขั้นตอนที่ 5: บันทึก PDF พร้อมรูปภาพ (และตรวจสอบ)

สุดท้าย เราจะ **save pdf with image** เมธอด `Save` จะเขียนเอกสารลงดิสก์ คุณยังสามารถสตรีมกลับไปยังไคลเอนต์เว็บได้หากคุณกำลังสร้าง API.

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

เมื่อคุณเปิด `output.pdf` คุณควรเห็นเฉพาะส่วนที่ครอปของ `image.jpg` ที่วางไว้ตามที่คุณกำหนด หากรูปภาพดูบิดเบี้ยว ให้ปรับความกว้าง/ความสูงของสี่เหลี่ยม `placement` ให้ตรงกับอัตราส่วนของสี่เหลี่ยม `crop`.

---

## คำถามที่พบบ่อย & ปัญหาที่อาจเจอ

| Question | Answer |
|----------|--------|
| **ฉันสามารถครอปหลายรูปบนหน้าเดียวได้หรือไม่?** | ได้เลย เรียก `page.AddImage` สำหรับแต่ละรูปพร้อมสี่เหลี่ยม placement และ crop ของมันเอง. |
| **ถ้ารูปของฉันอยู่ในรูปแบบอื่น (เช่น BMP) จะทำอย่างไร?** | Aspose.PDF รองรับ JPEG, PNG, BMP, GIF, และ TIFF โดยตรง เพียงเปลี่ยนนามสกุลไฟล์. |
| **ฉันต้องการลิขสิทธิ์สำหรับการใช้งานในโปรดักชันหรือไม่?** | รุ่นทดลองทำงานได้สูงสุด 5 หน้า สำหรับการใช้งานจริงควรซื้อไลเซนส์เพื่อเอาวอเตอร์มาร์คออก. |
| **ฉันจะหมุนรูปที่ครอปได้อย่างไร?** | หลังจากเพิ่มรูปแล้ว ให้ดึงอ็อบเจกต์ `Image` แล้วตั้งค่า `Rotate` (`Rotate = RotationAngle.Rotate90`). |
| **มีวิธีครอปโดยใช้เปอร์เซ็นต์แทนการใช้จุดแบบคงที่หรือไม่?** | มี — คำนวณขนาดสี่เหลี่ยมโดยอิงจาก `image.Width * 0.25` เป็นต้น แล้วแปลงเป็นจุดตามที่แสดงในขั้นตอน 4. |

---

## ตัวอย่างทำงานเต็ม (พร้อมคัดลอก‑วาง)

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

รันโปรแกรม เปิด `output.pdf` แล้วคุณจะเห็นเพียงสี่ส่วนบน‑ซ้ายของ `image.jpg` ที่แสดงที่มุมบน‑ซ้ายของหน้า เปลี่ยนค่าของสี่เหลี่ยม `crop` เพื่อทดลองกับส่วนต่าง ๆ.

---

## สรุป

เราได้อธิบายขั้นตอนทั้งหมดของการ **crop image in pdf** ด้วย Aspose.PDF สำหรับ C# ตั้งแต่เริ่มจากเอกสารใหม่ เรา **create pdf with image**, แสดง **how to add image to pdf**, ใช้สี่เหลี่ยม **how to crop image pdf** ที่กำหนดเอง และสุดท้าย **save pdf with image**.  

ตอนนี้คุณสามารถฝังรูปที่ครอปอย่างแม่นยำลงใน PDF ใด ๆ ที่คุณสร้าง—เหมาะสำหรับใบแจ้งหนี้, โบรชัวร์การตลาด, หรือรายงานอัตโนมัติ ขั้นต่อไป ลองเพิ่มคำบรรยายข้อความ (`TextFragment`) หรือวาดรูปทรงรอบรูปที่ครอปเพื่อเน้นให้ชัดเจนยิ่งขึ้น.  

มีสถานการณ์อื่นที่คุณสนใจไหม? แสดงความคิดเห็นได้เลย และขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ.

- [วิธีตั้งขนาดรูปภาพใน PDF ด้วย Aspose.PDF for .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [วิธีเพิ่มสแตมป์รูปภาพลงใน PDF ด้วย Aspose.PDF for .NET&#58; คู่มือฉบับสมบูรณ์](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [วิธีดึงข้อมูลรูปภาพจาก PDF ด้วย Aspose.PDF for .NET](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}