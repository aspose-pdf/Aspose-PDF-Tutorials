---
"date": "2025-04-14"
"description": "เรียนรู้วิธีแปลงเอกสาร PDF ที่ใช้รูปภาพเป็นข้อความที่สามารถค้นหาได้โดยใช้ Aspose.PDF และ Tesseract OCR กับ Java คู่มือนี้ครอบคลุมถึงการตั้งค่า การใช้งาน และแอปพลิเคชันจริง"
"title": "วิธีการแปลงไฟล์ PDF เป็นข้อความที่ค้นหาได้โดยใช้ Aspose.PDF และ Tesseract OCR ใน Java"
"url": "/th/java/conversion-export/convert-pdfs-searchable-text-aspose-tesseract-ocr-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# วิธีการแปลงไฟล์ PDF เป็นข้อความที่ค้นหาได้โดยใช้ Aspose.PDF และ Tesseract OCR ใน Java

## การแนะนำ

คุณกำลังเผชิญกับความท้าทายในการแยกข้อความจากเอกสาร PDF ที่สแกนหรือจากรูปภาพหรือไม่ การแปลงไฟล์ที่ไม่สามารถค้นหาได้เหล่านี้ให้เป็นรูปแบบที่สามารถค้นหาได้นั้นสามารถปฏิวัติวงการการแยกข้อมูล การจัดเก็บถาวร และการเข้าถึงข้อมูลได้ บทช่วยสอนนี้จะแนะนำคุณเกี่ยวกับการใช้ Aspose.PDF สำหรับ Java ร่วมกับ Tesseract OCR เพื่อให้การแปลงนี้มีประสิทธิภาพ

**สิ่งที่คุณจะได้เรียนรู้:**
- แปลงรูปภาพ PDF เป็นข้อความโดยใช้ Tesseract OCR ใน Java
- นำฟีเจอร์อันทรงพลังของ Aspose.PDF มาใช้สำหรับการประมวลผลเอกสาร
- บันทึกเอกสารที่ประมวลผลแล้วเป็น PDF ที่สามารถค้นหาได้

ด้วยทักษะเหล่านี้ คุณสามารถปลดล็อกศักยภาพทั้งหมดของเอกสารของคุณได้ ก่อนที่จะเริ่มใช้งานจริง ให้แน่ใจว่าคุณเตรียมทุกอย่างพร้อมแล้ว

## ข้อกำหนดเบื้องต้น

หากต้องการปฏิบัติตามบทช่วยสอนนี้อย่างมีประสิทธิผล ต้องแน่ใจว่าคุณมี:
- ความเข้าใจพื้นฐานเกี่ยวกับการเขียนโปรแกรมภาษา Java
- ความคุ้นเคยกับ Maven หรือ Gradle สำหรับการจัดการการอ้างอิง
- ซอฟต์แวร์ Tesseract OCR เวอร์ชันที่ติดตั้ง (ดาวน์โหลดฟรีจาก Google)

นอกจากนี้ ให้ตั้งค่าสภาพแวดล้อมการพัฒนาของคุณเพื่อจัดการโปรเจ็กต์ Java และให้แน่ใจว่าสามารถเข้าถึงไลบรารี Aspose.PDF ได้

## การตั้งค่า Aspose.PDF สำหรับ Java

หากต้องการเริ่มใช้ Aspose.PDF ในโปรเจ็กต์ Java ของคุณ ให้เพิ่มเป็นส่วนที่ต้องมีผ่าน Maven หรือ Gradle:

**เมเวน:**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**เกรเดิ้ล:**

```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### การขอใบอนุญาต

คุณสามารถรับใบอนุญาตทดลองใช้งานฟรีเพื่อทดสอบความสามารถของ Aspose.PDF หรือซื้อใบอนุญาตชั่วคราวเพื่อการทดสอบแบบขยายเวลา เยี่ยมชม [หน้าการอนุญาตสิทธิ์ของ Aspose](https://purchase.aspose.com/temporary-license/) สำหรับรายละเอียดเพิ่มเติม

ในการเริ่มต้นและตั้งค่า Aspose.PDF ให้แน่ใจว่าคุณมีไฟล์ลิขสิทธิ์ของคุณพร้อมแล้ว และนำไปใช้ตามที่แสดง:

```java
com.aspose.pdf.License license = new com.aspose.pdf.License();
license.setLicense("path/to/your/license/file.lic");
```

## คู่มือการใช้งาน

### คุณสมบัติ 1: การแปลง OCR โดยใช้ Tesseract

ฟีเจอร์นี้สาธิตวิธีการแปลงรูปภาพใน PDF เป็นข้อความโดยใช้ Tesseract OCR

#### ขั้นตอนที่ 1: สร้างการโทรกลับสำหรับการประมวลผล OCR

ฟังก์ชั่นการโทรกลับ `CallBackGetHocr` ประมวลผลแต่ละภาพจาก PDF:

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.Document.CallBackGetHocr;
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.util.Scanner;

CallBackGetHocr cbgh = new CallBackGetHocr() {
    @Override
    public String invoke(BufferedImage img) {
        String dataDir = "YOUR_DOCUMENT_DIRECTORY";
        String outputDir = "YOUR_OUTPUT_DIRECTORY";

        File outputfile = new File(dataDir + "/test.jpg");
        try {
            // เขียนภาพบัฟเฟอร์เป็นไฟล์ JPEG
            ImageIO.write(img, "jpg", outputfile);
        } catch (IOException e1) {
            e1.printStackTrace();
        }
        
        try {
            // ดำเนินการ Tesseract OCR เพื่อแปลงรูปภาพเป็นข้อความและจัดเก็บในรูปแบบ HOCR
            java.lang.Process process = Runtime.getRuntime().exec(
                "tesseract " + dataDir + "/test.jpg " + outputDir + "/out hocr"
            );
            process.waitFor();
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }

        // อ่านไฟล์ HOCR HTML ที่ถูกสร้างขึ้นเป็นสตริง
        File file = new File(outputDir + "/out.html");
        StringBuilder fileContents = new StringBuilder((int) file.length());
        Scanner scanner = null;
        try {
            scanner = new Scanner(file);
            String lineSeparator = System.getProperty("line.separator");
            while (scanner.hasNextLine()) {
                fileContents.append(scanner.nextLine() + lineSeparator);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } finally {
            if (scanner != null)
                scanner.close();
        }

        // ลบไฟล์ชั่วคราว
        File fileOut = new File(outputDir + "/out.html");
        if (fileOut.exists()) {
            fileOut.delete();
        }
        File fileTest = new File(dataDir + "/test.jpg");
        if (fileTest.exists()) {
            fileTest.delete();
        }
        return fileContents.toString();
    }
};
```

#### ขั้นตอนที่ 2: แปลง PDF เป็นข้อความที่ค้นหาได้

โหลด PDF ที่ไม่สามารถค้นหาได้ที่มีอยู่และแปลงโดยใช้การโทรกลับ:

```java
// กำหนดเส้นทางไดเรกทอรีตัวแทน
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
String outputDir = "YOUR_OUTPUT_DIRECTORY";

// โหลดเอกสาร PDF ที่มีอยู่
Document doc = new Document(dataDir + "/outFile.pdf");

// แปลงเอกสารโดยใช้การโทรกลับสำหรับการประมวลผล OCR
doc.convert(cbgh);

// บันทึกเอกสารที่แปลงแล้วเป็น PDF ที่สามารถค้นหาได้
doc.save(outputDir + "/output971.pdf");
```

### คุณสมบัติที่ 2: การแปลงและบันทึกเอกสาร PDF

หลังจากใช้ OCR แล้วให้บันทึก PDF ของคุณในรูปแบบที่สามารถค้นหาได้

## การประยุกต์ใช้งานจริง

1. **การจัดเก็บถาวร:** แปลงเอกสารที่สแกนเก่าเป็นรูปแบบที่สามารถค้นหาได้เพื่อให้ค้นหาได้ง่ายขึ้น
2. **การเข้าถึง:** ปรับปรุงการเข้าถึงได้โดยทำให้ข้อความพร้อมใช้งานสำหรับโปรแกรมอ่านหน้าจอ
3. **การขุดข้อมูล:** ดึงข้อมูลข้อความจากรายงานหรือหนังสือที่อิงภาพเพื่อการวิเคราะห์
4. **เอกสารทางกฎหมาย:** แปลงบันทึกทางศาลและเอกสารทางกฎหมายเพื่อให้สามารถค้นหาได้ดีขึ้น
5. **การบูรณาการ:** ใช้กระบวนการแปลงในแอปพลิเคชันเว็บหรือระบบจัดการเอกสาร

## การพิจารณาประสิทธิภาพ

- **เพิ่มประสิทธิภาพคุณภาพของภาพ:** รูปภาพที่มีความละเอียดสูงกว่าจะให้ผลลัพธ์ OCR ที่แม่นยำยิ่งขึ้น แต่ต้องใช้พลังการประมวลผลมากขึ้น
- **การประมวลผลแบบแบตช์:** จัดการไฟล์หลายไฟล์เป็นชุดเพื่อปรับปรุงประสิทธิภาพ
- **การจัดการหน่วยความจำ:** ตรวจสอบการใช้งานหน่วยความจำ Java และกำหนดค่าขนาดฮีปให้เหมาะสมสำหรับเอกสารขนาดใหญ่

## บทสรุป

การแปลง PDF เป็นข้อความที่ค้นหาได้โดยใช้ Aspose.PDF และ Tesseract OCR เป็นวิธีที่มีประสิทธิภาพในการปลดล็อกข้อมูลอันมีค่าจากเอกสารที่เป็นรูปภาพ โดยปฏิบัติตามคู่มือนี้ คุณสามารถผสานฟังก์ชันนี้เข้ากับแอปพลิเคชันของคุณได้อย่างง่ายดาย สำรวจเพิ่มเติมโดยปรับแต่งโค้ดให้เหมาะกับกรณีการใช้งานเฉพาะหรือผสานเข้ากับระบบอื่น

พร้อมที่จะลองหรือยัง เริ่มนำเทคนิคเหล่านี้ไปใช้ในโครงการของคุณวันนี้!

## ส่วนคำถามที่พบบ่อย

**คำถามที่ 1: ฉันสามารถใช้ Aspose.PDF สำหรับ Java โดยไม่ต้องมีใบอนุญาตได้หรือไม่**
- A1: ใช่ คุณสามารถลองใช้ Aspose.PDF เวอร์ชันทดลองใช้งานฟรีซึ่งมีข้อจำกัดบางประการ หากต้องการฟังก์ชันครบถ้วน ควรพิจารณาซื้อใบอนุญาตชั่วคราวหรือถาวร

**คำถามที่ 2: Tesseract OCR รองรับรูปแบบภาพอะไรบ้าง**
- A2: Tesseract รองรับรูปแบบภาพต่างๆ เช่น JPEG, PNG, TIFF และ BMP โปรดตรวจสอบว่ารูปภาพของคุณอยู่ในรูปแบบเหล่านี้เพื่อให้ได้ผลลัพธ์ที่ดีที่สุด

**คำถามที่ 3: ฉันจะจัดการข้อผิดพลาดระหว่างกระบวนการ OCR ได้อย่างไร**
- A3: นำการจัดการข้อผิดพลาดที่แข็งแกร่งมาใช้โดยใช้บล็อก try-catch รอบโค้ดการดำเนินการ OCR เพื่อจัดการข้อยกเว้นอย่างมีประสิทธิภาพ

**คำถามที่ 4: สามารถรวมโซลูชั่นนี้เข้ากับแอปพลิเคชันเว็บได้หรือไม่**
- A4: แน่นอน! คุณสามารถปรับใช้ Aspose.PDF และ Tesseract ในสภาพแวดล้อมเซิร์ฟเวอร์ ช่วยให้คุณสามารถประมวลผลเอกสารผ่าน API หรือบูรณาการโดยตรงกับระบบแบ็กเอนด์ของคุณได้

**คำถามที่ 5: ข้อกำหนดของระบบสำหรับการรัน Tesseract OCR มีอะไรบ้าง**
- A5: Tesseract ต้องใช้การสนับสนุนระบบปฏิบัติการพื้นฐาน โปรดตรวจสอบให้แน่ใจว่าได้ติดตั้ง Java บนเครื่องของคุณแล้ว พร้อมทั้งสิทธิ์อนุญาตที่จำเป็นสำหรับการดำเนินการกระบวนการภายนอก เช่น Tesseract

## ทรัพยากร

- **เอกสารประกอบ:** สำรวจคำแนะนำโดยละเอียดและการอ้างอิง API ได้ที่ [เอกสาร Aspose.PDF](https://reference-aspose.com/pdf/java/).
- **ดาวน์โหลด:** เข้าถึงเวอร์ชันล่าสุดของ Aspose.PDF ผ่านทาง [หน้าดาวน์โหลด](https://releases-aspose.com/pdf/java/).
- **ซื้อ:** รับใบอนุญาตโดยตรงจาก [หน้าสั่งซื้อ Aspose](https://purchase-aspose.com/buy).
- **ทดลองใช้งานฟรี:** ทดลองใช้คุณสมบัติต่างๆ ด้วยการทดลองใช้ฟรีที่ [ทดลองใช้ Aspose ฟรี](https://releases-aspose.com/pdf/java/#downloads).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}