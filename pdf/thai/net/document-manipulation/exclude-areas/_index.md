---
title: เปรียบเทียบ PDF โดยละเว้นพื้นที่เฉพาะด้วย Aspose.Pdf for .NET
weight: 201
limit:
description: เรียนรู้การเปรียบเทียบ PDF เคียงข้างและละเว้นพื้นที่ที่เลือกโดยใช้ Aspose.Pdf for .NET.
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: เรียนรู้การเปรียบเทียบ PDF เคียงข้างและละเว้นพื้นที่ที่เลือกโดยใช้
    Aspose.Pdf for .NET.
  headline: เปรียบเทียบ PDF โดยละเว้นพื้นที่เฉพาะด้วย Aspose.Pdf for .NET
  type: TechArticle
- description: เรียนรู้การเปรียบเทียบ PDF เคียงข้างและละเว้นพื้นที่ที่เลือกโดยใช้
    Aspose.Pdf for .NET.
  name: เปรียบเทียบ PDF โดยละเว้นพื้นที่เฉพาะด้วย Aspose.Pdf for .NET
  steps:
  - name: กำหนดเส้นทางไฟล์สำหรับ PDF ต้นฉบับสองไฟล์และไฟล์ diff PDF ที่จะส่งออก.
    text: กำหนดเส้นทางไฟล์สำหรับ PDF ต้นฉบับสองไฟล์และไฟล์ diff PDF ที่จะส่งออก.
  - name: ตรวจสอบว่าไฟล์ PDF ต้นฉบับทั้งสองไฟล์มีอยู่และยกเลิกการทำงานพร้อมแสดงข้อความข้อผิดพลาดหากไฟล์ใดไฟล์หนึ่งหายไป.
    text: ตรวจสอบว่าไฟล์ PDF ต้นฉบับทั้งสองไฟล์มีอยู่และยกเลิกการทำงานพร้อมแสดงข้อความข้อผิดพลาดหากไฟล์ใดไฟล์หนึ่งหายไป.
  - name: สร้างอาร์เรย์ที่บรรจุพื้นที่สี่เหลี่ยมที่ต้องละเว้นใน PDF แรก.
    text: สร้างอาร์เรย์ที่บรรจุพื้นที่สี่เหลี่ยมที่ต้องละเว้นใน PDF แรก.
  - name: สร้างอาร์เรย์ที่บรรจุพื้นที่สี่เหลี่ยมที่ต้องละเว้นใน PDF ที่สอง.
    text: สร้างอาร์เรย์ที่บรรจุพื้นที่สี่เหลี่ยมที่ต้องละเว้นใน PDF ที่สอง.
  - name: กำหนดค่าการเปรียบเทียบเคียงข้างกันโดยกำหนดอาร์เรย์พื้นที่ละเว้นให้กับคุณสมบัติที่เหมาะสม.
    text: กำหนดค่าการเปรียบเทียบเคียงข้างกันโดยกำหนดอาร์เรย์พื้นที่ละเว้นให้กับคุณสมบัติที่เหมาะสม.
  - name: โหลด PDF ทั้งสองไฟล์และดำเนินการเปรียบเทียบเคียงข้างกัน เพื่อสร้างไฟล์ diff
      ที่ตำแหน่งที่ระบุ.
    text: โหลด PDF ทั้งสองไฟล์และดำเนินการเปรียบเทียบเคียงข้างกัน เพื่อสร้างไฟล์ diff
      ที่ตำแหน่งที่ระบุ.
  - name: พิมพ์ข้อความยืนยันที่ระบุว่าการเปรียบเทียบเสร็จสิ้นและไฟล์ diff PDF ถูกบันทึกไว้ที่ใด.
    text: พิมพ์ข้อความยืนยันที่ระบุว่าการเปรียบเทียบเสร็จสิ้นและไฟล์ diff PDF ถูกบันทึกไว้ที่ใด.
  type: HowTo
- questions:
  - answer: พิกัดอยู่ในหน่วย points (1/72 นิ้ว) โดยจุดเริ่มต้นที่มุมซ้ายล่างของหน้า
      ดังนั้นสองตัวแรกคือ X/Y ของมุมซ้ายล่างและสองตัวสุดท้ายคือ X/Y ของมุมขวาบน.
    question: ค่าพิกัดของ `Rectangle` ใช้ระบบพิกัดใดเมื่อกำหนดโซนที่ต้องละเว้น?
  - answer: ได้ – ใส่หลายอ็อบเจกต์ `Aspose.Pdf.Rectangle` ลงในอาร์เรย์ `ExcludeAreas1`
      (หรือ `ExcludeAreas2`); แต่ละสี่เหลี่ยมจะถูกละเว้นอย่างอิสระระหว่างการเปรียบเทียบ.
    question: ฉันสามารถละเว้นพื้นที่สี่เหลี่ยมมากกว่าหนึ่งพื้นที่ในเอกสารเดียวกันได้หรือไม่?
  - answer: ไม่. `ExcludeAreas1` ใช้กับ PDF แรกและ `ExcludeAreas2` ใช้กับ PDF ที่สอง
      ดังนั้นคุณสามารถระบุพิกัดที่แตกต่างกันสำหรับแต่ละเอกสารได้.
    question: สี่เหลี่ยมที่ละเว้นต้องเหมือนกันในทั้งสอง PDF หรือไม่?
  - answer: Aspose.Pdf จะละเว้นสี่เหลี่ยมที่อยู่นอกหน้าทั้งหมดโดยไม่มีการแจ้งเตือน;
      พวกมันไม่มีผลต่อผลลัพธ์การเปรียบเทียบ.
    question: จะเกิดอะไรขึ้นหากสี่เหลี่ยมถูกกำหนดอยู่นอกขอบเขตของหน้า?
  - answer: อาร์เรย์ `ExcludeAreas` จะใช้ต่อหน้า ดังนั้นคุณต้องเพิ่ม `Rectangle` เดียวกันลงในคอลเลกชันของแต่ละหน้า
      (เช่น วนลูปผ่าน `pdf.Pages` และกำหนดอาร์เรย์) ก่อนเรียก `SideBySidePdfComparer.Compare`.
    question: ฉันจะละเว้นพื้นที่เดียวกันบนทุกหน้าของ PDF ได้อย่างไร?
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: ละเว้นพื้นที่เมื่อเปรียบเทียบ PDF
og_description: ดูวิธีข้ามพื้นที่ที่เลือกในการเปรียบเทียบ PDF เคียงข้างและรับไฟล์ diff PDF ที่สะอาด.
og_image_alt: คู่มือแสดงการเปรียบเทียบ PDF เคียงข้างพร้อมพื้นที่สี่เหลี่ยมที่ถูกยกเว้นโดยใช้ Aspose.Pdf for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เปรียบเทียบ PDF โดยละเว้นพื้นที่เฉพาะด้วย Aspose.Pdf
บทแนะนำนี้แสดงวิธีเปรียบเทียบเอกสาร PDF สองไฟล์เคียงข้างด้วย Aspose.Pdf for .NET โดยละเว้นพื้นที่สี่เหลี่ยมที่กำหนดไว้จากการวิเคราะห์ โดยการกำหนดพื้นที่ที่ต้องยกเว้นในแต่ละไฟล์ ไฟล์ diff PDF ที่สร้างขึ้นจะเน้นเฉพาะการเปลี่ยนแปลงที่สำคัญ ทำให้ง่ายต่อการมุ่งเน้นความแตกต่างที่เกี่ยวข้อง.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


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

**Q: ค่าพิกัดของ `Rectangle` ใช้ระบบพิกัดใดเมื่อกำหนดโซนที่ต้องละเว้น?**  
A: พิกัดอยู่ในหน่วย points (1/72 นิ้ว) โดยจุดเริ่มต้นที่มุมซ้ายล่างของหน้า ดังนั้นสองตัวแรกคือ X/Y ของมุมซ้ายล่างและสองตัวสุดท้ายคือ X/Y ของมุมขวาบน.

**Q: ฉันสามารถละเว้นพื้นที่สี่เหลี่ยมมากกว่าหนึ่งพื้นที่ในเอกสารเดียวกันได้หรือไม่?**  
A: ได้ – ใส่หลายอ็อบเจกต์ `Aspose.Pdf.Rectangle` ลงในอาร์เรย์ `ExcludeAreas1` (หรือ `ExcludeAreas2`); แต่ละสี่เหลี่ยมจะถูกละเว้นอย่างอิสระระหว่างการเปรียบเทียบ.

**Q: สี่เหลี่ยมที่ละเว้นต้องเหมือนกันในทั้งสอง PDF หรือไม่?**  
A: ไม่. `ExcludeAreas1` ใช้กับ PDF แรกและ `ExcludeAreas2` ใช้กับ PDF ที่สอง ดังนั้นคุณสามารถระบุพิกัดที่แตกต่างกันสำหรับแต่ละเอกสารได้.

**Q: จะเกิดอะไรขึ้นหากสี่เหลี่ยมถูกกำหนดอยู่นอกขอบเขตของหน้า?**  
A: Aspose.Pdf จะละเว้นสี่เหลี่ยมที่อยู่นอกหน้าทั้งหมดโดยไม่มีการแจ้งเตือน; พวกมันไม่มีผลต่อผลลัพธ์การเปรียบเทียบ.

**Q: ฉันจะละเว้นพื้นที่เดียวกันบนทุกหน้าของ PDF ได้อย่างไร?**  
A: อาร์เรย์ `ExcludeAreas` จะใช้ต่อหน้า ดังนั้นคุณต้องเพิ่ม `Rectangle` เดียวกันลงในคอลเลกชันของแต่ละหน้า (เช่น วนลูปผ่าน `pdf.Pages` และกำหนดอาร์เรย์) ก่อนเรียก `SideBySidePdfComparer.Compare`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}