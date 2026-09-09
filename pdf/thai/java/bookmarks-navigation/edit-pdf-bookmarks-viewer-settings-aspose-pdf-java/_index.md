---
date: '2025-12-19'
description: เรียนรู้วิธีเปลี่ยนรูปแบบหน้าของ PDF, แก้ไขบุ๊กมาร์กของ PDF, และปรับแต่งการตั้งค่าผู้ชมด้วย
  Aspose.PDF สำหรับ Java. เชี่ยวชาญการนำทางและการตั้งค่ารูปแบบเพื่อประสบการณ์ผู้ใช้ที่ราบรื่นยิ่งขึ้น.
keywords:
- edit PDF bookmarks Java
- Aspose.PDF viewer settings
- configure PDF navigation Java
title: 'เปลี่ยนการจัดหน้า PDF ใน Java - แก้ไขบุ๊กมาร์กและการตั้งค่า'
url: /th/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# เปลี่ยนการจัดหน้า PDF ใน Java: แก้ไขบุ๊กมาร์กและการตั้งค่า

## บทนำ
การนำทางในเอกสาร PDF ที่ซับซ้อนอาจทำให้ยุ่งยาก โดยเฉพาะเมื่อการตั้งค่า **change PDF page layout** ไม่ได้กำหนดอย่างถูกต้องหรือบุ๊กมาร์กชี้ไปยังตำแหน่งที่ผิด ในบทเรียนนี้คุณจะได้เรียนรู้วิธี **change PDF page layout**, **edit PDF bookmarks**, และ **configure PDF viewer settings** ด้วย Aspose.PDF for Java เมื่อเสร็จแล้วคุณจะมีการควบคุมเต็มที่ต่อการนำทาง, ปลายทางของบุ๊กมาร์ก, และวิธีการแสดงเอกสารต่อผู้อ่าน

**สิ่งที่คุณจะได้เรียนรู้**
- วิธีแก้ไขบุ๊กมาร์ก PDF ที่มีอยู่ให้ชี้ไปที่จุดเริ่มต้นของหน้า  
- วิธีตั้งค่าปลายทางของบุ๊กมาร์กขณะสร้าง PDF  
- วิธีเปลี่ยนการตั้งค่าผู้ชม เช่น การจัดหน้า  
- เคล็ดลับปฏิบัติสำหรับการโหลดเอกสาร PDF ใน Java และการเพิ่มประสิทธิภาพ

### คำตอบอย่างรวดเร็ว
- **วิธีหลักในการเปลี่ยนการจัดหน้า PDF คืออะไร?** ใช้ `PdfContentEditor.changeViewerPreference()` พร้อม `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.  
- **ฉันสามารถแก้ไขปลายทางของบุ๊กมาร์กหลังจากสร้าง PDF แล้วได้หรือไม่?** ได้ – โหลดเอกสาร, เข้าถึงโครงร่าง, และตั้งค่า `ExplicitDestination` ใหม่.  
- **ต้องใช้ไลเซนส์สำหรับฟีเจอร์เหล่านี้หรือไม่?** การทดลองใช้ฟรีเพียงพอสำหรับการประเมิน; ไลเซนส์เต็มจะลบข้อจำกัดทั้งหมด.  
- **ต้องการ dependency ของ Maven ใด?** `com.aspose:aspose-pdf:25.3` (หรือเวอร์ชันใหม่กว่า).  
- **รองรับ Java 11 ขึ้นไปหรือไม่?** แน่นอน – Aspose.PDF รองรับ Java 8+.

## “change PDF page layout” คืออะไร?
การเปลี่ยนการจัดหน้า PDF ควบคุมวิธีการแสดงหน้าต่างผู้ชม—หน้าเดียว, ต่อเนื่อง, มุมมองสองหน้า ฯลฯ การปรับตั้งค่านี้ช่วยเพิ่มความอ่านง่าย โดยเฉพาะสำหรับรายงานหรือแคตาล็อกที่ยาว

## ทำไมต้องแก้ไขบุ๊กมาร์ก PDF และตั้งค่าปลายทางของบุ๊กมาร์ก?
บุ๊กมาร์กทำหน้าที่คล้ายสารบัญ. ปลายทางที่แม่นยำทำให้ผู้อ่านกระโดดตรงไปยังส่วนที่ต้องการ ลดความสับสนและปรับปรุงประสบการณ์ผู้ใช้โดยรวม.

## ข้อกำหนดเบื้องต้น
- **Libraries & Dependencies**: Aspose.PDF for Java v25.3 หรือใหม่กว่า.  
- **Environment**: JDK 8 หรือใหม่กว่า, เครื่องมือสร้าง Maven หรือ Gradle.  
- **Knowledge**: ความรู้พื้นฐานการเขียนโปรแกรม Java และความคุ้นเคยกับแนวคิด PDF.

## การตั้งค่า Aspose.PDF for Java
### การติดตั้ง Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### การติดตั้ง Gradle
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**License Acquisition**: เริ่มต้นด้วยการทดลองใช้ฟรีหรือขอไลเซนส์ชั่วคราวเพื่อเข้าถึงฟีเจอร์เต็ม. พิจารณาซื้อไลเซนส์ถาวรสำหรับการใช้งานในผลิตภัณฑ์.

### การเริ่มต้นพื้นฐาน
```java
import com.aspose.pdf.Document;

public class PDFSetup {
    public static void main(String[] args) {
        // Initialize document object
        Document pdfDocument = new Document("path/to/your/pdf");
        
        System.out.println("Aspose.PDF for Java initialized successfully.");
    }
}
```

## คู่มือการดำเนินการ
### วิธีเปลี่ยนการจัดหน้า PDF ใน Java
**Overview**: ปรับการตั้งค่าผู้ชมเพื่อแสดงหน้าตามที่คุณต้องการ.

#### การเริ่มต้น PdfContentEditor
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### การเปลี่ยนการตั้งค่าผู้ชม
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### การบันทึกเอกสารที่อัปเดต
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

### วิธีแก้ไขบุ๊กมาร์ก PDF
**Overview**: ปรับบุ๊กมาร์กที่มีอยู่ให้ชี้อย่างแม่นยำไปยังจุดเริ่มต้นของหน้าที่ระบุ.

#### การเข้าถึงบุ๊กมาร์ก
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### การตั้งค่าปลายทางใหม่
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### การบันทึกการเปลี่ยนแปลง
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

### วิธีตั้งปลายทางของบุ๊กมาร์กขณะสร้าง PDF
**Overview**: สร้างบุ๊กมาร์กที่นำผู้ใช้ตรงไปยังตำแหน่งที่ต้องการใน PDF ที่สร้างใหม่.

#### การสร้างและกำหนดค่าบุ๊กมาร์ก
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### การกำหนดปลายทางของบุ๊กมาร์ก
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### การเพิ่มและบันทึก PDF
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## การประยุกต์ใช้ในทางปฏิบัติ
1. **Digital Books** – ทำให้บุ๊กมาร์กแต่ละบทอยู่ที่ด้านบนของหน้าเพื่อประสบการณ์การอ่านที่ต่อเนื่อง.  
2. **Technical Manuals** – การนำทางที่แม่นยำช่วยวิศวกรค้นหาส่วนต่าง ๆ ได้อย่างรวดเร็ว, โดยเฉพาะใน PDF ขนาดใหญ่.  
3. **Product Catalogs** – การจัดหน้าแบบหน้าเดียวทำให้การเรียกดูแคตาล็อกบนแท็บเล็ตเป็นธรรมชาติมากขึ้น.

## การพิจารณาประสิทธิภาพ
- **Optimizing Resources**: เมื่อจัดการ PDF ขนาดใหญ่, ใช้ `Document.optimizeResources()` เพื่อลดการใช้หน่วยความจำ.  
- **Java Memory Management**: ปิดสตรีมอย่างชัดเจนและให้ garbage collector ทำการคืนวัตถุหลังการประมวลผล.

## ปัญหาทั่วไปและวิธีแก้
- **Bookmarks Not Updating**: ตรวจสอบว่าคุณกำลังแก้ไขดัชนีโครงร่างที่ถูกต้อง (`get_Item(1)` หมายถึงบุ๊กมาร์กระดับบนสุดแรก).  
- **Viewer Preference Not Applied**: ตรวจสอบว่าคุณเรียก `editor.save()` หลังจากเปลี่ยนการตั้งค่า; มิฉะนั้นการเปลี่ยนแปลงจะอยู่ในหน่วยความจำเท่านั้น.  
- **License Exceptions**: ไลเซนส์ทดลองอาจเพิ่มลายน้ำ; ควรได้รับไลเซนส์เต็มสำหรับการใช้งานจริง.

## คำถามที่พบบ่อย
**Q: วิธีที่ง่ายที่สุดในการโหลดเอกสาร PDF ใน Java คืออะไร?**  
A: ใช้ `new Document("path/to/file.pdf")`; Aspose.PDF จะตรวจจับรูปแบบไฟล์โดยอัตโนมัติ.

**Q: ฉันสามารถเปลี่ยนการจัดหน้าโดยไม่ใช้ PdfContentEditor ได้หรือไม่?**  
A: ได้, คุณสามารถตั้งค่าการแสดงผลโดยตรงบนอ็อบเจ็กต์ `Document` ผ่าน `pdfDocument.getViewerPreferences().setPageLayout(...)`.

**Q: การเปลี่ยนการจัดแสดงผลมีผลต่อการพิมพ์หรือไม่?**  
A: การจัดแสดงผลมีผลเฉพาะต่อการแสดงบนหน้าจอ; ไม่ส่งผลต่อผลลัพธ์การพิมพ์.

**Q: มีขีดจำกัดจำนวนบุ๊กมาร์กที่ฉันสามารถสร้างได้หรือไม่?**  
A: ไม่มีขีดจำกัดที่ชัดเจน, แต่โครงร่างที่ใหญ่เกินไปอาจส่งผลต่อประสิทธิภาพ; ควรจัดระเบียบให้ดี.

**Q: ฉันจะทำให้แน่ใจว่าปลายทางของบุ๊กมาร์กแม่นยำหลังจากเพิ่มหรือเอาหน้าออกได้อย่างไร?**  
A: คำนวณปลายทางใหม่โดยใช้ดัชนีหน้าปัจจุบันหลังจากการเปลี่ยนแปลงโครงสร้างใด ๆ.

## แหล่งข้อมูล
- **Documentation**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **Download**: [Latest Releases for Java](https://releases.aspose.com/pdf/java/)
- **Purchase**: [Buy Aspose.PDF License](https://purchase.aspose.com/buy)
- **Free Trial**: [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)
- **Temporary License**: [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**Last Updated:** 2025-12-19  
**Tested With:** Aspose.PDF for Java v25.3  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}