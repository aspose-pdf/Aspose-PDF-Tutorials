---
title: เข้ารหัส PDF ด้วยการปิดการพิมพ์โดยใช้ Aspose.PDF for .NET
weight: 101
limit:
description: เรียนรู้วิธีเข้ารหัส PDF ด้วย AES‑256 และปิดการพิมพ์โดยใช้ Aspose.PDF for .NET.
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: เรียนรู้วิธีเข้ารหัส PDF ด้วย AES‑256 และปิดการพิมพ์โดยใช้ Aspose.PDF
    for .NET.
  headline: เข้ารหัส PDF ด้วยการปิดการพิมพ์โดยใช้ Aspose.PDF for .NET
  type: TechArticle
- description: เรียนรู้วิธีเข้ารหัส PDF ด้วย AES‑256 และปิดการพิมพ์โดยใช้ Aspose.PDF
    for .NET.
  name: เข้ารหัส PDF ด้วยการปิดการพิมพ์โดยใช้ Aspose.PDF for .NET
  steps:
  - name: กำหนดเส้นทางของ PDF ต้นฉบับ, ชื่อไฟล์ที่บันทึกผลลัพธ์ที่ได้รับการปกป้อง,
      และรหัสผ่านผู้ดูและเจ้าของ.
    text: กำหนดเส้นทางของ PDF ต้นฉบับ, ชื่อไฟล์ที่บันทึกผลลัพธ์ที่ได้รับการปกป้อง,
      และรหัสผ่านผู้ดูและเจ้าของ.
  - name: ตรวจสอบว่าไฟล์ต้นฉบับมีอยู่และยกเลิกการทำงานพร้อมแสดงข้อความข้อผิดพลาดหากไฟล์หายไป.
    text: ตรวจสอบว่าไฟล์ต้นฉบับมีอยู่และยกเลิกการทำงานพร้อมแสดงข้อความข้อผิดพลาดหากไฟล์หายไป.
  - name: เปิด PDF ต้นฉบับ, ตั้งค่าไม่มีสิทธิ์ใด ๆ, เข้ารหัสด้วย AES‑256 โดยใช้รหัสผ่านที่ระบุ,
      และบันทึกไฟล์ที่ได้รับการปกป้อง.
    text: เปิด PDF ต้นฉบับ, ตั้งค่าไม่มีสิทธิ์ใด ๆ, เข้ารหัสด้วย AES‑256 โดยใช้รหัสผ่านที่ระบุ,
      และบันทึกไฟล์ที่ได้รับการปกป้อง.
  - name: เปิด PDF ที่เข้ารหัสใหม่ด้วยรหัสผ่านผู้ดูและเขียนค่าสถานะ IsEncrypted ไปยังคอนโซลเพื่อยืนยันการปกป้อง.
    text: เปิด PDF ที่เข้ารหัสใหม่ด้วยรหัสผ่านผู้ดูและเขียนค่าสถานะ IsEncrypted ไปยังคอนโซลเพื่อยืนยันการปกป้อง.
  - name: พิมพ์ข้อความสุดท้ายที่ระบุว่าการเข้ารหัสเสร็จสมบูรณ์และชื่อไฟล์ผลลัพธ์.
    text: พิมพ์ข้อความสุดท้ายที่ระบุว่าการเข้ารหัสเสร็จสมบูรณ์และชื่อไฟล์ผลลัพธ์.
  type: HowTo
- questions:
  - answer: '`Permissions` เป็น enum แบบ flag; การกำหนดค่า `0` หมายความว่าไม่มีบิตสิทธิ์ใด
      ๆ ถูกตั้งค่า, ดังนั้น Aspose.Pdf จะไม่ให้สิทธิ์ PrintDocument และผู้ดูไม่สามารถพิมพ์
      PDF ได้.'
    question: ทำไมการตั้งค่า `Permissions rights = 0;` ถึงทำให้การพิมพ์ถูกปิดใช้งาน?
  - answer: ได้, ให้แทนที่ `CryptoAlgorithm.AESx256` ด้วย `CryptoAlgorithm.AESx128`
      (หรือค่า enum ที่รองรับอื่น) ในการเรียก `pdfDoc.Encrypt`; ส่วนอื่นของโค้ดยังคงเหมือนเดิม.
    question: ฉันสามารถใช้อัลกอริทึมการเข้ารหัสอื่น เช่น AES‑128 กับโค้ดเดียวกันได้หรือไม่?
  - answer: Aspose.Pdf จะยอมรับรหัสผ่านที่เหมือนกัน, แต่รหัสผ่านเจ้าของจะไม่ให้สิทธิพิเศษเพิ่มเติม;
      PDF ยังจะถูกเข้ารหัสอยู่, และสิทธิ์ที่คุณระบุ (ไม่มี) จะถูกนำไปใช้.
    question: จะเกิดอะไรขึ้นหากรหัสผ่านผู้ดูและรหัสผ่านหลัก (owner) เหมือนกัน?
  - answer: เปิดไฟล์ที่ได้รับการปกป้องด้วยรหัสผ่านผู้ดู (`new Document(securedFile,
      viewerPwd)`) แล้วลองพิมพ์จากโปรแกรมดู PDF; เนื่องจากไม่ได้ตั้งค่าสิทธิ์ `PrintDocument`,
      โปรแกรมดูจะปฏิเสธคำสั่งพิมพ์.
    question: ฉันจะยืนยันว่าการพิมพ์ถูกบล็อกจริงหลังจากการเข้ารหัสได้อย่างไร?
  - answer: โค้ดตรวจสอบ `File.Exists(sourceFile)` และเขียนข้อความข้อผิดพลาดไปยัง `Console.Error`
      ก่อนคืนค่า, ป้องกันไม่ให้ `Document` constructor โยน `FileNotFoundException`.
    question: ข้อผิดพลาดใดจะถูกโยนเมื่อ `original.pdf` ไม่มีอยู่, และควรจัดการอย่างไร?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: เข้ารหัส PDF และบล็อกการพิมพ์
og_description: ปกป้อง PDF ของคุณด้วยการเข้ารหัส AES‑256 และตรวจสอบว่าไม่สามารถพิมพ์ได้ — คู่มือขั้นตอนต่อขั้นตอน.
og_image_alt: ภาพหน้าจอแสดงโค้ด Aspose.PDF for .NET ที่เข้ารหัส PDF และปิดการพิมพ์.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# เข้ารหัส PDF ด้วยการปิดการพิมพ์โดยใช้ Aspose.PDF
บทแนะนำนี้แสดงวิธีเปิดไฟล์ PDF ที่มีอยู่ด้วย Aspose.PDF for .NET, ใช้การเข้ารหัส AES‑256 พร้อมไม่ให้สิทธิ์ใด ๆ — ซึ่งทำให้การพิมพ์ไม่ทำงาน — บันทึกเอกสารที่ได้รับการปกป้อง, และยืนยันการปกป้องโดยเปิดไฟล์ด้วยรหัสผ่านผู้ดู. ปฏิบัติตามโค้ดขั้นตอนต่อขั้นตอนเพื่อให้แน่ใจว่า PDF ของคุณไม่สามารถพิมพ์ได้หลังจากการเข้ารหัส.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-no-print" >}}


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

**Q: ทำไมการตั้งค่า `Permissions rights = 0;` ถึงทำให้การพิมพ์ถูกปิดใช้งาน?**  
A: `Permissions` เป็น enum แบบ flag; การกำหนดค่า `0` หมายความว่าไม่มีบิตสิทธิ์ใด ๆ ถูกตั้งค่า, ดังนั้น Aspose.Pdf จะไม่ให้สิทธิ์ PrintDocument และผู้ดูไม่สามารถพิมพ์ PDF ได้.

**Q: ฉันสามารถใช้อัลกอริทึมการเข้ารหัสอื่น เช่น AES‑128 กับโค้ดเดียวกันได้หรือไม่?**  
A: ได้, ให้แทนที่ `CryptoAlgorithm.AESx256` ด้วย `CryptoAlgorithm.AESx128` (หรือค่า enum ที่รองรับอื่น) ในการเรียก `pdfDoc.Encrypt`; ส่วนอื่นของโค้ดยังคงเหมือนเดิม.

**Q: จะเกิดอะไรขึ้นหากรหัสผ่านผู้ดูและรหัสผ่านหลัก (owner) เหมือนกัน?**  
A: Aspose.Pdf จะยอมรับรหัสผ่านที่เหมือนกัน, แต่รหัสผ่านเจ้าของจะไม่ให้สิทธิพิเศษเพิ่มเติม; PDF ยังจะถูกเข้ารหัสอยู่, และสิทธิ์ที่คุณระบุ (ไม่มี) จะถูกนำไปใช้.

**Q: ฉันจะยืนยันว่าการพิมพ์ถูกบล็อกจริงหลังจากการเข้ารหัสได้อย่างไร?**  
A: เปิดไฟล์ที่ได้รับการปกป้องด้วยรหัสผ่านผู้ดู (`new Document(securedFile, viewerPwd)`) แล้วลองพิมพ์จากโปรแกรมดู PDF; เนื่องจากไม่ได้ตั้งค่าสิทธิ์ `PrintDocument`, โปรแกรมดูจะปฏิเสธคำสั่งพิมพ์.

**Q: ข้อผิดพลาดใดจะถูกโยนเมื่อ `original.pdf` ไม่มีอยู่, และควรจัดการอย่างไร?**  
A: โค้ดตรวจสอบ `File.Exists(sourceFile)` และเขียนข้อความข้อผิดพลาดไปยัง `Console.Error` ก่อนคืนค่า, ป้องกันไม่ให้ `Document` constructor โยน `FileNotFoundException`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}