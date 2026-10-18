---
date: '2026-07-03'
description: เรียนรู้วิธีเพิ่ม Aspose PDF Maven dependency และแปลง PDF เป็น XPS พร้อมข้อความที่เลือกได้โดยใช้
  Aspose.PDF for Java. คู่มือแบบ Step‑by‑step พร้อมข้อกำหนดเบื้องต้นและ FAQ.
keywords:
- aspose pdf maven dependency
- how to convert pdf to xps
- java convert pdf xps
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to add the Aspose PDF Maven dependency and convert PDF to
    XPS with selectable text using Aspose.PDF for Java. Step‑by‑step guide with prerequisites
    and FAQs.
  headline: Aspose PDF Maven Dependency – Convert PDF to XPS (Java)
  type: TechArticle
- description: Learn how to add the Aspose PDF Maven dependency and convert PDF to
    XPS with selectable text using Aspose.PDF for Java. Step‑by‑step guide with prerequisites
    and FAQs.
  name: Aspose PDF Maven Dependency – Convert PDF to XPS (Java)
  steps:
  - name: Load the PDF Document
    text: 'First, load your PDF document from its directory:'
  - name: Configure Save Options
    text: 'Create an instance of `XpsSaveOptions` to set up the XPS conversion options:'
  - name: Save as XPS File
    text: 'Finally, save the document in XPS format to your desired output directory:'
  type: HowTo
- questions:
  - answer: Yes—pass the password to the `Document` constructor or use `Document.open(String
      path, String password)` before conversion.
    question: Can I convert password‑protected PDFs?
  - answer: Absolutely. All vector shapes, images, and text are preserved, and the
      text remains selectable.
    question: Does the XPS retain vector graphics?
  - answer: The trial works without a license but adds a watermark to the output;
      a permanent license removes all restrictions.
    question: Is a license mandatory for the trial version?
  - answer: It processes files in a streaming manner, allowing conversion of PDFs
      with hundreds of pages without loading the entire document into memory.
    question: How does Aspose.PDF handle large files?
  - answer: The library runs on any OS with a compatible JDK, including Windows, Linux,
      and macOS.
    question: Which platforms are supported?
  type: FAQPage
title: การเพิ่ม Aspose PDF Maven Dependency – แปลง PDF เป็น XPS (Java)
url: /th/java/conversion-export/convert-pdf-to-xps-aspose-pdf-java-selectable-text/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Aspose PDF Maven Dependency – แปลง PDF เป็น XPS (Java)

## บทนำ

หากคุณต้องการ **เพิ่ม Aspose PDF Maven dependency** แล้วแปลงเอกสาร PDF เป็น XPS พร้อมคงข้อความให้สามารถเลือกได้ คุณมาถูกที่แล้ว คู่มือฉบับนี้จะพาคุณผ่านทุกขั้นตอน—ตั้งค่า Maven หรือ Gradle, โหลด PDF, ตั้งค่า XPS options, และสุดท้ายบันทึกไฟล์ XPS ที่ข้อความสามารถเลือกได้ หลังจากนี้คุณจะมีโค้ดสั้น ๆ ที่สามารถนำไปใช้ในโครงการ Java ใดก็ได้

## คำตอบสั้น
- **ต้องการ dependency อะไร?** `com.aspose:aspose-pdf` (Maven) หรืออาร์ติแฟคต์ที่เทียบเท่าใน Gradle.  
- **XPS สามารถคงข้อความที่เลือกได้หรือไม่?** ใช่—Aspose.PDF จะเก็บชั้นข้อความโดยอัตโนมัติ.  
- **ต้องการเวอร์ชัน Java ใด?** JDK 8 หรือใหม่กว่า.  
- **ต้องใช้ลิขสิทธิ์สำหรับการผลิตหรือไม่?** จำเป็นต้องมีลิขสิทธิ์ Aspose.PDF ที่ถูกต้องสำหรับการใช้งานไม่จำกัด.  
- **การแปลงใช้เวลานานเท่าไหร่?** โดยทั่วไปใช้เวลาน้อยกว่าวินาทีสำหรับไฟล์ที่มีน้อยกว่า 100 หน้า บนฮาร์ดแวร์มาตรฐาน.

## Aspose PDF Maven Dependency คืออะไร?
`aspose-pdf` Maven artifact ให้ API ของ Aspose.PDF for Java เต็มรูปแบบ ซึ่งช่วยให้สร้าง, แก้ไข, และแปลง PDF ได้โดยไม่ต้องใช้ซอฟต์แวร์ภายนอก การเพิ่ม dependency นี้ใน `pom.xml` หรือ `build.gradle` จะดึง **ไบนารีที่จำเป็นทั้งหมด** ทำให้คุณเริ่มเขียนโค้ดได้ทันทีโดยไม่ต้องจัดการ JAR ด้วยตนเอง.

## ทำไมต้องแปลง PDF เป็น XPS พร้อมข้อความที่เลือกได้?
Aspose.PDF รองรับ **รูปแบบเข้าและออกกว่า 50 ประเภท** และสามารถสร้างไฟล์ XPS ที่คงชั้นข้อความที่สามารถค้นหาและเลือกได้ สิ่งนี้สำคัญสำหรับกระบวนการทำงานที่ **ต้องการเอกสารระดับการเก็บรักษา**, ความแม่นยำของการจัดวาง, หรือการแก้ไขต่อใน **เครื่องมือที่รองรับ XPS** การแปลงเสร็จภายในน้อยกว่าวินาทีสำหรับ PDF ปกติที่ **20 หน้า** บน CPU สมัยใหม่.

## ข้อกำหนดเบื้องต้น

- **Java Development Kit (JDK) 8+** ติดตั้งแล้วและตั้งค่า `JAVA_HOME`.  
- **Maven 3.6+** หรือ **Gradle 6+** สำหรับ **การจัดการ dependency**.  
- มีความคุ้นเคยพื้นฐาน **กับการทำ I/O ของไฟล์ใน Java** และ **การจัดการข้อยกเว้น**.  

### ไลบรารีและ Dependency ที่จำเป็น

คุณจะต้องใช้ไลบรารี Aspose.PDF for Java รุ่น 25.3 หรือใหม่กว่า รวมเข้าด้วยกันโดยใช้เครื่องมือสร้างต่อไปนี้:

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

### การตั้งค่าสภาพแวดล้อม

ตรวจสอบให้แน่ใจว่า IDE หรือสภาพแวดล้อมการสร้างของคุณชี้ไปที่ JDK ที่ถูกต้องและเครือข่ายสามารถเข้าถึง Maven Central หรือรีโพ지ทอรีส่วนตัวของคุณได้.

## วิธีเพิ่ม Aspose PDF Maven dependency?

`aspose-pdf` คืออาร์ติแฟคต์ที่คุณเพิ่มในไฟล์การสร้างของโครงการของคุณ แล้วรีเฟรช dependency เพื่อให้ JAR ถูกดาวน์โหลดโดยอัตโนมัติ สำหรับ Maven ให้ใส่บล็อก `<dependency>` ภายใน `<dependencies>`; สำหรับ Gradle ให้วางบรรทัด `implementation` ภายในบล็อก `dependencies` หลังจากรีเฟรชแล้ว คลาสของ Aspose จะพร้อมใช้งานใน classpath และคุณสามารถเริ่มเขียนโค้ดโดยไม่ต้องจัดการ JAR ด้วยตนเอง.

## การตั้งค่า Aspose.PDF สำหรับ Java

### ขั้นตอนการติดตั้ง

1. **การตั้งค่า Maven/Gradle:** เพิ่ม dependency ตามที่แสดงข้างต้นและรัน `mvn clean install` หรือ `gradle build` เพื่อดึงไลบรารี.  
2. **การรับลิขสิทธิ์:**  
   - ดาวน์โหลด [ทดลองใช้ฟรี](https://releases.aspose.com/pdf/java/) หรือรับ [ลิขสิทธิ์ชั่วคราว](https://purchase.aspose.com/temporary-license/).  
   - วางไฟล์ลิขสิทธิ์ (`Aspose.Pdf.lic`) ในโฟลเดอร์ที่แอปพลิเคชันของคุณเข้าถึงได้และโหลดมันเมื่อเริ่มต้น.

### การเริ่มต้นพื้นฐาน

`License` ใช้ไฟล์ลิขสิทธิ์ของ Aspose เพื่อเปิดใช้งานฟังก์ชันเต็มรูปแบบ.  
โหลดลิขสิทธิ์ (หากคุณมี) และสร้างอ็อบเจ็กต์ `Document` เพื่อทำงานกับ PDF.  
`Document` แทนไฟล์ PDF และให้เมธอดสำหรับจัดการเนื้อหาของมัน.

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.License;

// Initialize a License object
License license = new License();

// Set the license file path
license.setLicense("path/to/Aspose.Total.Java.lic");
```  

## วิธีแปลง PDF เป็น XPS พร้อมข้อความที่เลือกได้?

`XpsSaveOptions` กำหนดค่าการบันทึก PDF เป็นเอกสาร XPS รวมถึงการคงข้อความ.  
โหลด PDF ต้นฉบับ, ตั้งค่า `XpsSaveOptions` เพื่อคงข้อความ, แล้วเรียก `save` ด้วยนามสกุล `.xps`. API จะฝังชั้นข้อความโดยอัตโนมัติ ทำให้ XPS ที่ได้สามารถค้นหาและคัดลอกได้เช่นเดียวกับ PDF ดั้งเดิม กระบวนการทั้งหมดโดยทั่วไปต้องใช้เพียงสามบรรทัดของโค้ดหลังจากตั้งค่าไลบรารี.

## คู่มือการใช้งาน

### แปลง PDF เป็น XPS

ฟีเจอร์นี้ช่วยให้คุณแปลงเอกสาร PDF เป็นไฟล์ XPS ด้วย Aspose.PDF for Java.

#### ขั้นตอนที่ 1: โหลดเอกสาร PDF

First, load your PDF document from its directory:

```java
import com.aspose.pdf.Document;

String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document pdfDocument = new Document(dataDir + "/input.pdf");
```  

#### ขั้นตอนที่ 2: ตั้งค่าการบันทึก

Create an instance of `XpsSaveOptions` to set up the XPS conversion options:

```java
import com.aspose.pdf.XpsSaveOptions;

XpsSaveOptions saveOptions = new XpsSaveOptions();
```  

#### ขั้นตอนที่ 3: บันทึกเป็นไฟล์ XPS

Finally, save the document in XPS format to your desired output directory:

```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
pdfDocument.save(outputDir + "/ConvertPDFtoXPS_out.xps\
```  

## ปัญหาทั่วไปและวิธีแก้

- **หน้าว่างในผลลัพธ์ XPS:** ตรวจสอบว่า PDF ไม่ใช้สตรีมที่เข้ารหัส; หากมี ให้ระบุรหัสผ่านเมื่อโหลด `Document`.  
- **ข้อผิดพลาดหน่วยความจำกับ PDF ขนาดใหญ่:** ใช้ `Document.optimizeResources()` ก่อนบันทึกเพื่อลดการใช้หน่วยความจำ.  
- **ฟอนต์หาย:** ติดตั้งฟอนต์ที่จำเป็นบนเซิร์ฟเวอร์หรือฝังฟอนต์ใน PDF ก่อนการแปลง.

## คำถามที่พบบ่อย

**Q: ฉันสามารถแปลง PDF ที่มีการป้องกันด้วยรหัสผ่านได้หรือไม่?**  
A: ใช่—ส่งรหัสผ่านไปยังคอนสตรัคเตอร์ของ `Document` หรือใช้ `Document.open(String path, String password)` ก่อนการแปลง.

**Q: XPS จะคงกราฟิกเวกเตอร์ไว้หรือไม่?**  
A: แน่นอน. รูปทรงเวกเตอร์, ภาพ, และข้อความทั้งหมดจะถูกคงไว้และข้อความยังคงสามารถเลือกได้.

**Q: จำเป็นต้องมีลิขสิทธิ์สำหรับเวอร์ชันทดลองหรือไม่?**  
A: เวอร์ชันทดลองทำงานได้โดยไม่มีลิขสิทธิ์แต่จะใส่ลายน้ำในผลลัพธ์; ลิขสิทธิ์ถาวรจะลบข้อจำกัดทั้งหมด.

**Q: Aspose.PDF จัดการไฟล์ขนาดใหญ่อย่างไร?**  
A: มันประมวลผลไฟล์แบบสตรีมมิ่ง ทำให้สามารถแปลง PDF ที่มีหลายร้อยหน้าได้โดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ.

**Q: แพลตฟอร์มใดบ้างที่รองรับ?**  
A: ไลบรารีทำงานบนระบบปฏิบัติการใด ๆ ที่มี JDK ที่เข้ากันได้ รวมถึง Windows, Linux, และ macOS.

---

**อัปเดตล่าสุด:** 2026-07-03  
**ทดสอบกับ:** Aspose.PDF for Java 25.3  
**ผู้เขียน:** Aspose  

{{< blocks/products/products-backtop-button >}}

## บทแนะนำที่เกี่ยวข้อง

- [แปลง PDF เป็น JPEG ด้วย Aspose.PDF for Java: คู่มือขั้นตอนโดยละเอียด](/pdf/java/conversion-export/convert-pdf-to-jpeg-aspose-java-tutorial/)
- [วิธีแปลง PDF เป็น Excel ด้วย Aspose.PDF for Java | คู่มือขั้นตอนโดยละเอียด](/pdf/java/conversion-export/convert-pdf-excel-aspose-java-tutorial/)
- [วิธีแปลงไฟล์ XPS เป็น PDF ด้วย Aspose.PDF ใน Java: คู่มือฉบับสมบูรณ์](/pdf/java/conversion-export/convert-xps-pdf-aspose-java-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}