---
date: '2026-04-21'
description: เรียนรู้วิธีส่งออก PDF เป็น TIFF ด้วย Aspose.PDF for Java ลดขนาดไฟล์
  TIFF และแปลงหน้าของ PDF เป็น TIFF พร้อมตัวอย่างการใช้งานจริง
keywords:
- export pdf as tiff
- reduce tiff file size
- convert pdf to tiff java
- convert pdf page tiff
- generate tiff from pdf
title: 'ส่งออก PDF เป็น TIFF ใน Java: คู่มือฉบับสมบูรณ์โดยใช้ Aspose.PDF'
url: /th/java/conversion-export/convert-pdf-to-tiff-aspose-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# ส่งออก PDF เป็น TIFF ใน Java

## บทนำ
คุณกำลังมองหา **export PDF as TIFF** หรือไม่? ไม่ว่าคุณจะต้องการสำหรับการเก็บถาวร, การแชร์, หรือการดึงภาพคุณภาพสูงจาก PDF, การเชี่ยวชาญการแปลงนี้สามารถช่วยประหยัดเวลาและความพยายามของคุณได้. ด้วย **Aspose.PDF for Java**, คุณสามารถแปลง PDF ทั้งไฟล์หรือเฉพาะหน้าที่เลือกเป็นภาพ TIFF, ควบคุมความละเอียด, การบีบอัด, และแม้กระทั่ง **reduce TIFF file size**. ในบทแนะนำนี้, เราจะพาคุณผ่านทุกอย่างที่คุณต้องรู้—ตั้งแต่การตั้งค่าไปจนถึงการเขียนโค้ด—เพื่อให้คุณมั่นใจในการ **convert PDF to TIFF Java**.

**สิ่งที่คุณจะได้เรียนรู้**
- วิธีตั้งค่า Aspose.PDF for Java ในโปรเจกต์ของคุณ  
- วิธี **convert PDF page TIFF** (หน้าเดียวหรือช่วง)  
- เคล็ดลับเพื่อ **reduce TIFF file size** และปรับปรุงประสิทธิภาพ  

มาดูข้อกำหนดเบื้องต้นที่จำเป็นสำหรับกระบวนการแปลงนี้กัน

## คำตอบอย่างรวดเร็ว
- **ไลบรารีหลักคืออะไร?** Aspose.PDF for Java  
- **ฉันสามารถส่งออก PDF เป็น TIFF ด้วยบรรทัดโค้ดเดียวได้หรือไม่?** Yes, using `TiffDevice.process()`  
- **การตั้งค่าใดที่ลดขนาดไฟล์?** CCITT4 compression with lower DPI  
- **สามารถแปลงเฉพาะหน้าที่ต้องการได้หรือไม่?** Absolutely – use the overloaded `process()` method  
- **ต้องการไลเซนส์สำหรับการผลิตหรือไม่?** Yes, a paid license removes evaluation limits  

## ข้อกำหนดเบื้องต้น
ก่อนจะดำดิ่งสู่การทำงาน, โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้พร้อม:
- **Java Development Kit (JDK)** – เวอร์ชันล่าสุดใดก็ได้ (แนะนำ 8+)  
- **IDE** – IntelliJ IDEA, Eclipse หรือโปรแกรมแก้ไข Java ที่คุณชื่นชอบ  
- **Aspose.PDF for Java** library – เพิ่มผ่าน Maven หรือ Gradle (ดูส่วนต่อไป)

## การตั้งค่า Aspose.PDF for Java
เพื่อเริ่มต้น, ให้เพิ่มไลบรารี Aspose.PDF for Java ในโปรเจกต์ของคุณโดยใช้ Maven หรือ Gradle:

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### การรับไลเซนส์
Aspose.PDF มีการให้ทดลองใช้ฟรี, ไลเซนส์ชั่วคราวสำหรับการประเมิน, และตัวเลือกการซื้อเพื่อการเข้าถึงเต็มรูปแบบ:
- **ทดลองใช้ฟรี:** ดาวน์โหลดจาก [หน้าเผยแพร่](https://releases.aspose.com/pdf/java/) เพื่อทดลองฟีเจอร์.  
- **ไลเซนส์ชั่วคราว:** รับไลเซนส์ชั่วคราวโดยเยี่ยมชม [ลิงก์](https://purchase.aspose.com/temporary-license/) นี้.  
- **ซื้อ:** สำหรับฟีเจอร์เต็ม, ซื้อไลเซนส์ของคุณที่นี่: [หน้าซื้อ Aspose](https://purchase.aspose.com/buy).

เมื่อคุณได้ตั้งค่าไลบรารีและไลเซนส์อย่างเหมาะสมแล้ว, เราสามารถดำเนินการต่อไปยังการแปลง PDF‑to‑TIFF ได้.

## คู่มือการใช้งาน

### แปลงทุกหน้าของ PDF เป็นภาพ TIFF เดียว
#### ทำไมต้องแปลงทุกหน้า?
การสร้าง TIFF แบบหลายหน้าเป็นทางเลือกที่เหมาะสำหรับการเก็บถาวรหรือเมื่อไฟล์เดียวทำให้การประมวลผลต่อไปง่ายขึ้น.

#### คำแนะนำทีละขั้นตอน
**1. เปิดเอกสาร PDF**  
```java
Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```

**2. สร้าง Output Stream สำหรับภาพ TIFF**  
```java
java.io.OutputStream imageStream = new java.io.FileOutputStream("YOUR_OUTPUT_DIRECTORY/Converted_Image.tiff");
```

**3. Set Up Resolution and TiffSettings**  
```java
Resolution resolution = new Resolution(300);
TiffSettings tiffSettings = new TiffSettings();
tiffSettings.setCompression(CompressionType.CCITT4);
tiffSettings.setDepth(ColorDepth.Format8bpp);
tiffSettings.setSkipBlankPages(true);
```
- **Resolution:** 300 DPI ให้คุณภาพพร้อมพิมพ์. ลด DPI (เช่น 150) เพื่อ **reduce TIFF file size**.  
- **Compression:** CCITT4 เหมาะสำหรับเอกสารขาว‑ดำและช่วยลดขนาดไฟล์.  
- **Color Depth:** 8 bpp ให้สมดุลระหว่างรายละเอียดและขนาด.

**4. เริ่มต้น TiffDevice**  
```java
TiffDevice tiffDevice = new TiffDevice(resolution, tiffSettings);
```

**5. แปลงและบันทึกภาพ TIFF**  
```java
tiffDevice.process(pdfDocument, imageStream);
imageStream.close();
```
`process()` method ทำการเรนเดอร์ทุกหน้าเป็น TIFF แบบหลายหน้าเดียว. การปิด stream จะทำให้ข้อมูลทั้งหมดถูกเขียนลงดิสก์.

### แปลงหน้า PDF เฉพาะเป็น TIFF
#### เมื่อใดที่คุณอาจต้องการสิ่งนี้?
บางครั้งคุณอาจต้องการเฉพาะภาพย่อหรือหน้าเดียวเพื่อการแสดงตัวอย่าง.

#### คำแนะนำทีละขั้นตอน
**1. เปิดเอกสาร PDF**  
```java
Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```

**2. สร้าง Output Stream สำหรับภาพ TIFF ของหน้าที่ระบุ**  
```java
java.io.OutputStream imageStream = new java.io.FileOutputStream("YOUR_OUTPUT_DIRECTORY/Converted_Image_Page_1.tiff");
```

**3. ใช้ Resolution และ TiffSettings เดิม** (การตั้งค่านี้เหมือนกับตัวอย่างการแปลงทุกหน้า).

**4. เริ่มต้น TiffDevice**  
```java
TiffDevice tiffDevice = new TiffDevice(resolution, tiffSettings);
```

**5. แปลงเฉพาะหน้าที่ต้องการ**  
```java
tiffDevice.process(pdfDocument, 1, 1, imageStream); // Converts only the first page.
imageStream.close();
```
`process()` method ที่มีการ overload ให้คุณระบุหน้าเริ่มต้นและหน้าสิ้นสุด, ทำให้สามารถทำ **convert pdf page tiff** ได้.

## การประยุกต์ใช้งานจริง
- **Archiving:** เก็บ PDF ทางกฎหมายหรือประวัติศาสตร์เป็น TIFF เพื่อการเก็บรักษาระยะยาว.  
- **Image Processing:** ดึง TIFF ความละเอียดสูงสำหรับ OCR หรือกระบวนการคอมพิวเตอร์วิชัน.  
- **Document Sharing:** ให้ภาพสแนปช็อตหน้าเดียวที่แสดงผลสม่ำเสมอบนทุกแพลตฟอร์ม.

## การพิจารณาประสิทธิภาพ
- **Memory Management:** PDF ขนาดใหญ่สามารถใช้หน่วยความจำ heap มาก. ประมวลผลหน้าเป็นชุดหรือเพิ่ม flag `-Xmx` ของ JVM หากจำเป็น.  
- **Resolution vs. Size:** DPI สูงให้ภาพคมชัดแต่ไฟล์ใหญ่ขึ้น. ปรับ DPI ให้สอดคล้องกับเป้าหมาย **reduce tiff file size** ของคุณ.  
- **Compression Choice:** สำหรับ PDF สี, พิจารณาใช้การบีบอัด JPEG2000 แทน CCITT4 เพื่อให้ขนาดไฟล์จัดการได้.

## ข้อผิดพลาดทั่วไปและการแก้ไขปัญหา
- **Blank Pages Appear:** ตรวจสอบให้แน่ใจว่าได้ตั้งค่า `tiffSettings.setSkipBlankPages(true)`, หรือยืนยันว่า PDF ต้นฉบับมีเนื้อหาในหน้านั้นจริง.  
- **Out‑Of‑Memory Errors:** แบ่ง PDF เป็นส่วนย่อยหรือใช้ `Document.optimizeResources()` ก่อนการแปลง.  
- **Unexpected Colors:** หากต้องการ TIFF แบบระดับสีเทา, ตั้งค่า `tiffSettings.setDepth(ColorDepth.Format8bpp)` และเลือก `CompressionType` ที่เหมาะสม.

## คำถามที่พบบ่อย

**Q: ความแตกต่างระหว่าง CCITT4 กับประเภทการบีบอัดอื่นคืออะไร?**  
A: CCITT4 ถูกปรับให้เหมาะกับภาพขาว‑ดำ, ให้ไฟล์ขนาดเล็กลงโดยไม่สูญเสียความชัดของข้อความ—เหมาะสำหรับเอกสารสแกน.

**Q: ฉันสามารถแปลง PDF ที่มีเนื้อหาผสม (ข้อความ + รูปภาพ) เป็น TIFF ได้หรือไม่?**  
A: ได้, Aspose.PDF จัดการทั้งชั้นข้อความและภาพ, รักษาความเที่ยงตรงของภาพ.

**Q: ฉันจะจัดการกับ PDF ขนาดใหญ่มากโดยไม่ทำให้หน่วยความจำหมดได้อย่างไร?**  
A: ประมวลผลเอกสารเป็นช่วงหน้า, เพิ่ม heap ของ JVM (`-Xmx`), หรือเรียก `Document.optimizeResources()` เพื่อลดการใช้หน่วยความจำ.

**Q: สามารถแปลงช่วงหน้าต่าง ๆ แทนการแปลงหน้าเดียวได้หรือไม่?**  
A: แน่นอน. ใช้ `tiffDevice.process(pdfDocument, startPage, endPage, imageStream);` โดยที่ `startPage` และ `endPage` กำหนดช่วงหน้า.

**Q: ไฟล์ TIFF ที่ได้มีขนาดใหญ่เกินไป—ฉันทำอย่างไรได้บ้าง?**  
A: ลด DPI, เปลี่ยนไปใช้การบีบอัดที่เข้มข้นกว่า (เช่น JPEG2000 สำหรับสี), หรือ ลดความลึกสี.

## แหล่งข้อมูล
- [เอกสาร Aspose.PDF](https://reference.aspose.com/pdf/java/)
- [ดาวน์โหลด Aspose.PDF for Java](https://releases.aspose.com/pdf/java/)
- [ซื้อไลเซนส์](https://purchase.aspose.com/buy)
- [เวอร์ชันทดลองใช้ฟรี](https://releases.aspose.com/pdf/java/)
- [สมัครไลเซนส์ชั่วคราว](https://purchase.aspose.com/temporary-license/)
- [ฟอรั่มสนับสนุน Aspose](https://forum.aspose.com/c/pdf/10)

โดยทำตามบทแนะนำนี้, คุณควรพร้อมที่จะ **export PDF as TIFF** อย่างมีประสิทธิภาพโดยใช้ Aspose.PDF for Java. ขอให้สนุกกับการเขียนโค้ด!

---

**อัปเดตล่าสุด:** 2026-04-21  
**ทดสอบด้วย:** Aspose.PDF 25.3 for Java  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}