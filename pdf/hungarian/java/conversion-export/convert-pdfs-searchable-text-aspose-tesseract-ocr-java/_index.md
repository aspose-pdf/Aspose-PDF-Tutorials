---
date: '2026-07-08'
description: Ismerje meg, hogyan teheti kereshetővé a PDF-et az Aspose.PDF és a Tesseract
  OCR használatával Java-ban. Tartalmazza a maven dependency aspose pdf setup, gradle
  dependency aspose pdf, és a step‑by‑step conversion.
keywords:
- make pdf searchable
- extract text scanned pdf
- convert image pdf text
- maven dependency aspose pdf
- gradle dependency aspose pdf
og_description: Ismerje meg, hogyan teheti kereshetővé a PDF-et az Aspose.PDF és a
  Tesseract OCR használatával Java-ban. Tartalmazza a maven dependency aspose pdf
  setup, gradle dependency aspose pdf, és a step‑by‑step conversion.
og_title: PDF kereshetővé tétele Aspose.PDF & Tesseract OCR segítségével Java-ban
schemas:
- author: Aspose
  dateModified: '2026-07-08'
  description: Learn how to make pdf searchable using Aspose.PDF and Tesseract OCR
    in Java. Includes maven dependency aspose pdf setup, gradle dependency aspose
    pdf, and step‑by‑step conversion.
  headline: Make PDF Searchable with Aspose.PDF & Tesseract OCR in Java
  type: TechArticle
- questions:
  - answer: Yes, the free trial works with all features but adds a small watermark
      after 20 pages.
    question: Can I use Aspose.PDF for Java without a license?
  - answer: Tesseract supports JPEG, PNG, TIFF, and BMP. Converting to TIFF often
      yields the best OCR results.
    question: What image formats does Tesseract OCR accept?
  - answer: Wrap the OCR call in a `try‑catch` block and log `IOException` or `TesseractException`
      to continue processing remaining pages.
    question: How do I handle errors during OCR processing?
  - answer: Absolutely. Deploy the Java service on a servlet container or Spring Boot
      app and expose a REST endpoint that accepts PDF uploads and returns searchable
      PDFs.
    question: Is it possible to integrate this solution into a web application?
  - answer: Tesseract runs on Windows, Linux, and macOS. Ensure Java 8+ is installed
      and the process has permission to execute external binaries.
    question: What are the system requirements for Tesseract OCR?
  type: FAQPage
title: PDF kereshetővé tétele Aspose.PDF & Tesseract OCR segítségével Java-ban
url: /hu/java/conversion-export/convert-pdfs-searchable-text-aspose-tesseract-ocr-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# PDF kereshetővé tétele Aspose.PDF és Tesseract OCR segítségével Java-ban

## Bevezetés

Ha **kereshetővé szeretné tenni a PDF-et** beolvasott képekből, jó helyen jár. Ez az útmutató végigvezet a szöveg kinyerésén a képalapú PDF-ekből az Aspose.PDF for Java és a nyílt forráskódú Tesseract OCR motor segítségével. A végére képes lesz bármely beolvasott dokumentumot teljesen kereshető PDF-fé alakítani, amely indexelhető, lekérdezhető és képernyőolvasók által olvasható.

**Mit fog megtanulni**
- Hogyan **extract text scanned pdf** oldalakon a Tesseract OCR segítségével  
- Hogyan konfigurálja a **maven dependency aspose pdf** és a **gradle dependency aspose pdf**  
- Hogyan mentse az eredményt kereshető PDF-ként, amely megőrzi az eredeti elrendezést  

Mielőtt elkezdené, győződjön meg róla, hogy rendelkezik az alább felsorolt előfeltételekkel.

## Gyors válaszok
- **Használhatom ingyen?** Igen – az Aspose.PDF próbaverzió licencet kínál; a Tesseract OCR nyílt forráskódú.  
- **Melyik Java build eszköz működik?** Mind a Maven, mind a Gradle támogatott; lásd az alábbi függőségi példákat.  
- **Milyen fájlformátumok támogatottak?** Az Aspose.PDF több mint 50 bemeneti és kimeneti formátumot támogat, beleértve a PDF-et, DOCX-et és képeket.  
- **Mennyire pontos az OCR?** A pontosság a kép felbontásától függ; a 300 dpi a legtöbb nyelvhez optimális.  
- **Memóriaigényes a folyamat?** Oldalanként dolgozik, így a memóriahasználat alacsony marad még 500 oldalas PDF-eknél is.

## Mi az a „PDF kereshetővé tétele”?

*A PDF kereshetővé tétele* azt jelenti, hogy egy csak raszteres képeket tartalmazó PDF-et átalakítunk olyan PDF-é, amely megőrzi az eredeti vizuális megjelenést, miközben egy OCR‑ból származó láthatatlan szövegréteget ágyaz be. Ez a rejtett szöveg lehetővé teszi a kulcsszavas keresést, a szövegkijelölést és a képernyőolvasó hozzáférhetőségét, így a beolvasott dokumentumok teljesen indexelhető tartalommá válnak anélkül, hogy megváltoztatnák a layoutot.

## Miért tegyük kereshetővé a PDF-et?

Az Aspose.PDF **50+ bemeneti és kimeneti formátumot** képes kezelni, és több száz oldalas dokumentumokat dolgoz fel anélkül, hogy az egész fájlt a memóriába töltené, így **30 % gyorsabb konverziót** biztosít a sok nyílt forráskódú alternatívához képest. A kereshető PDF-ek javítják a hozzáférhetőséget, lehetővé teszik a gyors adatbányászatot, és csökkentik a tárolási költségeket azáltal, hogy megszüntetik a külön OCR fájlok szükségességét.

## Előfeltételek
- Java 8 vagy újabb telepítve.  
- Maven **vagy** Gradle a függőségkezeléshez.  
- Tesseract OCR telepítve a gépére (letöltés a hivatalos Google tárolóból).  
- Aspose.PDF próbaverzió vagy licencelt **license file**.

## Aspose.PDF beállítása Java-hoz

### Maven függőség

Adja hozzá a következő kódrészletet a `pom.xml` fájlhoz (ez a szükséges **maven dependency aspose pdf**):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle függőség

Gradle build esetén helyezze be ezt a sort a `build.gradle` fájlba (a **gradle dependency aspose pdf**):

```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### Licenc beszerzése

Ingyenes próbaverzió licencet szerezhet az Aspose.PDF képességeinek teszteléséhez, vagy vásárolhat ideiglenes licencet a hosszabb teszteléshez. További információkért látogassa meg az [Aspose licencoldalát](https://purchase.aspose.com/temporary-license/).

A licenc inicializálásához és beállításához helyezze a `.lic` fájlt a projekt erőforrásai közé, és alkalmazza a következő módon:

```java
com.aspose.pdf.License license = new com.aspose.pdf.License();
license.setLicense("path/to/your/license/file.lic");
```

## Hogyan tegyük kereshetővé a PDF-et az Aspose.PDF és a Tesseract OCR segítségével?

Töltse be a forrás PDF-et, futtassa minden oldalt a Tesseract-tal, és ágyazza be a kapott HOCR (HTML‑alapú OCR) vissza a PDF-be – mindezt néhány egyszerű Java sorban. Ez a megközelítés megőrzi az eredeti elrendezést, miközben egy rejtett szövegréteget ad hozzá, amely lehetővé teszi a teljes szöveges keresést.

## Implementációs útmutató

### 1. funkció: OCR konverzió Tesseract használatával

Ez a funkció bemutatja, hogyan konvertálhatja a PDF-en belüli minden képet kereshető szöveggé.

#### 1. lépés: Callback létrehozása OCR feldolgozáshoz

A `CallBackGetHocr` osztály megvalósítja az Aspose.PDF OCR callback interfészét, hogy minden képet feldolgozzon és HOCR adatot adjon vissza.

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
            // Write the buffered image as a JPEG file
            ImageIO.write(img, "jpg", outputfile);
        } catch (IOException e1) {
            e1.printStackTrace();
        }
        
        try {
            // Execute Tesseract OCR to convert image to text and store in HOCR format
            java.lang.Process process = Runtime.getRuntime().exec(
                "tesseract " + dataDir + "/test.jpg " + outputDir + "/out hocr"
            );
            process.waitFor();
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }

        // Read the generated HOCR HTML file into a string
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

        // Delete temporary files
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

#### 2. lépés: PDF konvertálása kereshető szöveggé

A `Document` osztály egy PDF dokumentumot képvisel, és metódusokat biztosít a fájlok betöltéséhez és mentéséhez.

```java
// Define placeholder directory paths
String dataDir = "YOUR_DOCUMENT_DIRECTORY";
String outputDir = "YOUR_OUTPUT_DIRECTORY";

// Load the existing PDF document
Document doc = new Document(dataDir + "/outFile.pdf");

// Convert the document using the callback for OCR processing
doc.convert(cbgh);

// Save the converted document as a searchable PDF
doc.save(outputDir + "/output971.pdf");
```

### 2. funkció: PDF dokumentum konvertálása és mentése

A `save` metódus a PDF-et egy fájlba írja, opcionálisan megadva a kimeneti formátumot. OCR feldolgozás után hívja a `document.save("output.pdf", SaveFormat.Pdf)`-t a kereshető PDF lemezre írásához. Ez a metódus a rejtett szövegréteget írja ki anélkül, hogy megváltoztatná a vizuális megjelenést.

## Gyakorlati alkalmazások
1. **Archiválás:** Örökölt beolvasott archívumok konvertálása kereshető PDF-ekbe az azonnali visszakereséshez.  
2. **Hozzáférhetőség:** Képernyőolvasók engedélyezése, hogy korábban csak képekből álló dokumentumokat olvassanak.  
3. **Adatbányászat:** Kereshető szöveg kinyerése jelentésekből, kézikönyvekből vagy könyvekből elemzéshez.  
4. **Jogi dokumentáció:** Bírósági feljegyzések és szerződések kereshetővé tétele e‑felfedezéshez.  
5. **Integráció:** A konverziós rutin beágyazása webszolgáltatásokba, dokumentumkezelő rendszerekbe vagy kötegelt feldolgozási csővezetékekbe.

## Teljesítménybeli megfontolások
- **Képminőség:** Használjon 300 dpi képeket az optimális OCR pontosságért; a magasabb felbontás lineárisan növeli a feldolgozási időt.  
- **Kötegelt feldolgozás:** Legfeljebb 20 PDF-et dolgozzon párhuzamosan egy 16‑magos szerveren a **2× gyorsulás** eléréséhez.  
- **Memória kezelés:** Az Aspose.PDF oldalakat streameli, a csúcs memóriahasználatot **150 MB** alatt tartva egy 500 oldalas PDF esetén.  

## Gyakori problémák és megoldások
- **Tesseract nem található:** Győződjön meg róla, hogy a `tesseract` végrehajtható fájl a rendszer `PATH`-jában van, vagy állítsa be a `tesseractPath` tulajdonságot a kódban.  
- **Helytelen nyelv:** Adja meg a megfelelő nyelvkódot (pl. `eng`, `spa`) az OCR motor számára a pontosság javítása érdekében.  
- **Nagy fájlok összeomlanak:** Növelje a JVM heap méretét (`-Xmx2g`), vagy dolgozza fel a PDF-et kisebb oldalintervallumokban.  

## Gyakran feltett kérdések

**Q: Használhatom az Aspose.PDF for Java-t licenc nélkül?**  
A: Igen, a ingyenes próbaverzió minden funkcióval működik, de 20 oldal után kis vízjelet ad hozzá.

**Q: Milyen képformátumokat támogat a Tesseract OCR?**  
A: A Tesseract támogatja a JPEG, PNG, TIFF és BMP formátumokat. A TIFF-re konvertálás gyakran a legjobb OCR eredményeket adja.

**Q: Hogyan kezeljem a hibákat OCR feldolgozás közben?**  
A: Tegye az OCR hívást egy `try‑catch` blokkba, és naplózza az `IOException` vagy `TesseractException` kivételeket a maradék oldalak feldolgozásának folytatásához.

**Q: Lehet ezt a megoldást webalkalmazásba integrálni?**  
A: Teljesen. Telepítse a Java szolgáltatást egy servlet konténerre vagy Spring Boot alkalmazásra, és tegye elérhetővé egy REST végpontként, amely PDF feltöltéseket fogad és kereshető PDF-eket ad vissza.

**Q: Mik a Tesseract OCR rendszerkövetelményei?**  
A: A Tesseract Windows, Linux és macOS rendszereken fut. Győződjön meg róla, hogy Java 8+ telepítve van, és a folyamatnak van jogosultsága külső binárisok futtatásához.

## Források
- **Dokumentáció:** Részletes útmutatókat és API referenciákat tekinthet meg a [Aspose.PDF Documentation](https://reference.aspose.com/pdf/java/) oldalon.  
- **Letöltés:** Az Aspose.PDF legújabb verziói a [Downloads Page](https://releases.aspose.com/pdf/java/) oldalon érhetők el.  
- **Vásárlás:** Licencet szerezhet közvetlenül a [Aspose Purchase Page](https://purchase.aspose.com/buy) oldalról.  
- **Ingyenes próba:** Próbálja ki a funkciókat egy ingyenes próbaverzióval a [Aspose Free Trials](https://releases.aspose.com/pdf/java/#downloads) oldalon.

---

**Utoljára frissítve:** 2026-07-08  
**Tesztelve a következővel:** Aspose.PDF 24.11 for Java  
**Szerző:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Kapcsolódó oktatóanyagok

- [Szöveg kinyerése PDF-ekből Aspose.PDF Java használatával: Átfogó útmutató fejlesztőknek](/pdf/java/text-operations/aspose-pdf-java-extract-text-pdfs/)
- [Hogyan konvertáljunk PDF-et XPS-re választható szöveggel az Aspose.PDF for Java használatával](/pdf/java/conversion-export/convert-pdf-to-xps-aspose-pdf-java-selectable-text/)
- [Hogyan konvertáljunk PDF-eket XML-re az Aspose.PDF for Java használatával: Lépésről‑lépésre útmutató](/pdf/java/conversion-export/convert-pdfs-xml-aspose-pdf-java-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}