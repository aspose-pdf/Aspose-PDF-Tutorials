---
title: การเปรียบเทียบ PDF แบบ Side‑by‑Side โดยยกเว้นหมายเหตุด้วย Aspose.Pdf for .NET
weight: 101
limit:
description: คู่มือขั้นตอนต่อขั้นตอนสำหรับเปรียบเทียบ PDF และยกเว้นพื้นที่หมายเหตุโดยใช้ Aspose.Pdf for .NET
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: คู่มือขั้นตอนต่อขั้นตอนสำหรับเปรียบเทียบ PDF และยกเว้นพื้นที่หมายเหตุโดยใช้
    Aspose.Pdf for .NET
  headline: การเปรียบเทียบ PDF แบบ Side‑by‑Side โดยยกเว้นหมายเหตุด้วย Aspose.Pdf for
    .NET
  type: TechArticle
- description: คู่มือขั้นตอนต่อขั้นตอนสำหรับเปรียบเทียบ PDF และยกเว้นพื้นที่หมายเหตุโดยใช้
    Aspose.Pdf for .NET
  name: การเปรียบเทียบ PDF แบบ Side‑by‑Side โดยยกเว้นหมายเหตุด้วย Aspose.Pdf for .NET
  steps:
  - name: กำหนดเส้นทางไฟล์สำหรับ PDF หลัก, PDF รอง, และ PDF diff ที่เป็นผลลัพธ์
    text: กำหนดเส้นทางไฟล์สำหรับ PDF หลัก, PDF รอง, และ PDF diff ที่เป็นผลลัพธ์
  - name: ตรวจสอบว่าไฟล์ PDF อินพุตทั้งสองไฟล์มีอยู่และยกเลิกการทำงานพร้อมข้อความแสดงข้อผิดพลาดหากไฟล์ใดไฟล์หนึ่งหายไป
    text: ตรวจสอบว่าไฟล์ PDF อินพุตทั้งสองไฟล์มีอยู่และยกเลิกการทำงานพร้อมข้อความแสดงข้อผิดพลาดหากไฟล์ใดไฟล์หนึ่งหายไป
  - name: เปิดไฟล์ PDF สองไฟล์เป็นอ็อบเจ็กต์ Document (pdfA และ pdfB) ภายในบล็อก using
      เพื่อให้มีการปล่อยทรัพยากรโดยอัตโนมัติ
    text: เปิดไฟล์ PDF สองไฟล์เป็นอ็อบเจ็กต์ Document (pdfA และ pdfB) ภายในบล็อก using
      เพื่อให้มีการปล่อยทรัพยากรโดยอัตโนมัติ
  - name: รวบรวมสี่เหลี่ยมขอบเขตของหมายเหตุทั้งหมดใน pdfA และเก็บไว้ใน ignoredRectsA
    text: รวบรวมสี่เหลี่ยมขอบเขตของหมายเหตุทั้งหมดใน pdfA และเก็บไว้ใน ignoredRectsA
  - name: รวบรวมสี่เหลี่ยมขอบเขตของหมายเหตุทั้งหมดใน pdfB และเก็บไว้ใน ignoredRectsB
    text: รวบรวมสี่เหลี่ยมขอบเขตของหมายเหตุทั้งหมดใน pdfB และเก็บไว้ใน ignoredRectsB
  - name: สร้างอ็อบเจ็กต์ SideBySideComparisonOptions และกำหนดสี่เหลี่ยมหมายเหตุที่รวบรวมไว้ก่อนหน้านี้ให้กับ
      ExcludeAreas1 และ ExcludeAreas2 เพื่อให้พื้นที่เหล่านั้นถูกละเว้นระหว่างการเปรียบเทียบ
    text: สร้างอ็อบเจ็กต์ SideBySideComparisonOptions และกำหนดสี่เหลี่ยมหมายเหตุที่รวบรวมไว้ก่อนหน้านี้ให้กับ
      ExcludeAreas1 และ ExcludeAreas2 เพื่อให้พื้นที่เหล่านั้นถูกละเว้นระหว่างการเปรียบเทียบ
  - name: ดำเนินการเปรียบเทียบ PDF แบบ side‑by‑side โดยใช้ Document ทั้งสองอ็อบเจ็กต์และตัวเลือกที่กำหนดค่าไว้,
      แล้วบันทึกผลลัพธ์ลงใน outputPdf
    text: ดำเนินการเปรียบเทียบ PDF แบบ side‑by‑side โดยใช้ Document ทั้งสองอ็อบเจ็กต์และตัวเลือกที่กำหนดค่าไว้,
      แล้วบันทึกผลลัพธ์ลงใน outputPdf
  - name: ปล่อยอ็อบเจ็กต์ Document และออกจากบล็อก using
    text: ปล่อยอ็อบเจ็กต์ Document และออกจากบล็อก using
  - name: พิมพ์ข้อความยืนยันที่ระบุว่าการเปรียบเทียบเสร็จสมบูรณ์และบอกตำแหน่งที่บันทึกไฟล์
      diff PDF
    text: พิมพ์ข้อความยืนยันที่ระบุว่าการเปรียบเทียบเสร็จสมบูรณ์และบอกตำแหน่งที่บันทึกไฟล์
      diff PDF
  type: HowTo
- questions:
  - answer: ใช่. โค้ดจะไม่เพิ่มสี่เหลี่ยมใด ๆ ลงในรายการ `ignoredRects` ที่สอดคล้องกัน,
      ดังนั้น `ExcludeAreas1`/`ExcludeAreas2` จะได้รับอาเรย์ว่างและตัวเปรียบเทียบจะประมวลผลทั้งหน้า
    question: จะเกิดอะไรขึ้นหากหน้าของ PDF ไม่มีหมายเหตุ – การเปรียบเทียบจะยังทำงานได้หรือไม่?
  - answer: ตั้งค่า `ExcludeAreas1` (หรือ `ExcludeAreas2`) ให้เป็นสี่เหลี่ยมที่รวบรวมไว้และปล่อยให้คุณสมบัติอีกอันเป็นอาเรย์ว่าง;
      ตัวเปรียบเทียบจะละเว้นพื้นที่เฉพาะในเอกสารที่ระบุ
    question: ฉันสามารถยกเว้นหมายเหตุเฉพาะจากเอกสารหนึ่งได้หรือไม่ ในขณะที่ยังคงรักษาหมายเหตุของอีกเอกสารใน
      diff ไว้?
  - answer: สี่เหลี่ยมที่ทับกันจะถูกรวมเข้าด้วยกันภายในโดยตัวเปรียบเทียบ, ดังนั้นขอบเขตหมายเหตุที่ทับกันจะถูกละเว้นอย่างปลอดภัยโดยไม่นับซ้ำ
    question: สี่เหลี่ยมหมายเหตุที่ทับกันทำให้เกิดปัญหาใด ๆ กับ `ExcludeAreas` หรือไม่?
  - answer: ใช่, ตั้งค่า `compareOpts.ExcludeTables = true;` – ธงนี้ทำงานร่วมกับ `ExcludeAreas1`/`ExcludeAreas2`
      เพื่อยกเว้นพื้นที่ตารางด้วย
    question: มีวิธีใดที่จะยกเว้นตารางเพิ่มเติมจากหมายเหตุโดยใช้วัตถุตัวเลือกเดียวกันหรือไม่?
  - answer: โค้ดจะตรวจสอบ `if (a != null && a.Rect != null)` ก่อนเพิ่มลงในรายการ,
      ดังนั้นสี่เหลี่ยมที่เป็น null จะถูกข้ามไปโดยไม่มีการโยนข้อยกเว้น
    question: ถ้าคุณสมบัติ `Rect` ของหมายเหตุเป็น null จะเกิดข้อยกเว้นในโค้ดหรือไม่?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: เปรียบเทียบ PDF โดยไม่มีหมายเหตุ
og_description: ดำเนินการ diff PDF แบบ side‑by‑side ที่ข้ามเครื่องหมายหมายเหตุทั้งหมด
og_image_alt: คำแนะนำที่แสดงการเปรียบเทียบ PDF แบบ side‑by‑side ที่ยกเว้นพื้นที่หมายเหตุโดยใช้ Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# การเปรียบเทียบ PDF แบบ Side‑by‑Side โดยยกเว้นหมายเหตุด้วย Aspose.Pdf
บทแนะนำนี้แสดงวิธีเปรียบเทียบไฟล์ PDF สองไฟล์ด้วย Aspose.Pdf for .NET โดยไม่สนใจเนื้อหาหมายเหตุใด ๆ มันดึงกล่องขอบเขตของหมายเหตุทั้งหมดจากแต่ละเอกสาร, ส่งพื้นที่เหล่านั้นเข้าไปใน SideBySideComparisonOptions, แล้วดำเนินการเปรียบเทียบแบบ side‑by‑side ผลลัพธ์คือไฟล์ diff PDF ที่เน้นการเปลี่ยนแปลงที่ไม่ใช่หมายเหตุเท่านั้น

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: จะเกิดอะไรขึ้นหากหน้าของ PDF ไม่มีหมายเหตุ – การเปรียบเทียบจะยังทำงานได้หรือไม่?**  
A: ใช่. โค้ดจะไม่เพิ่มสี่เหลี่ยมใด ๆ ลงในรายการ `ignoredRects` ที่สอดคล้องกัน, ดังนั้น `ExcludeAreas1`/`ExcludeAreas2` จะได้รับอาเรย์ว่างและตัวเปรียบเทียบจะประมวลผลทั้งหน้า

**Q: ฉันสามารถยกเว้นหมายเหตุเฉพาะจากเอกสารหนึ่งได้หรือไม่ ในขณะที่ยังคงรักษาหมายเหตุของอีกเอกสารใน diff ไว้?**  
A: ตั้งค่า `ExcludeAreas1` (หรือ `ExcludeAreas2`) ให้เป็นสี่เหลี่ยมที่รวบรวมไว้และปล่อยให้คุณสมบัติอีกอันเป็นอาเรย์ว่าง; ตัวเปรียบเทียบจะละเว้นพื้นที่เฉพาะในเอกสารที่ระบุ

**Q: สี่เหลี่ยมหมายเหตุที่ทับกันทำให้เกิดปัญหาใด ๆ กับ `ExcludeAreas` หรือไม่?**  
A: สี่เหลี่ยมที่ทับกันจะถูกรวมเข้าด้วยกันภายในโดยตัวเปรียบเทียบ, ดังนั้นขอบเขตหมายเหตุที่ทับกันจะถูกละเว้นอย่างปลอดภัยโดยไม่นับซ้ำ

**Q: มีวิธีใดที่จะยกเว้นตารางเพิ่มเติมจากหมายเหตุโดยใช้วัตถุตัวเลือกเดียวกันหรือไม่?**  
A: ใช่, ตั้งค่า `compareOpts.ExcludeTables = true;` – ธงนี้ทำงานร่วมกับ `ExcludeAreas1`/`ExcludeAreas2` เพื่อยกเว้นพื้นที่ตารางด้วย

**Q: ถ้าคุณสมบัติ `Rect` ของหมายเหตุเป็น null จะเกิดข้อยกเว้นในโค้ดหรือไม่?**  
A: โค้ดจะตรวจสอบ `if (a != null && a.Rect != null)` ก่อนเพิ่มลงในรายการ, ดังนั้นสี่เหลี่ยมที่เป็น null จะถูกข้ามไปโดยไม่มีการโยนข้อยกเว้น

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}