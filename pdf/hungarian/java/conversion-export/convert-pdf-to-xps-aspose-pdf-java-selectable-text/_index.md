---
date: '2026-07-03'
description: Ismerje meg, hogyan adhatja hozzá az Aspose PDF Maven függőséget, és
  konvertálhatja a PDF-et XPS-re választható szöveggel az Aspose.PDF for Java segítségével.
  Lépésről‑lépésre útmutató előkövetelményekkel és GYIK‑kel.
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
title: Aspose PDF Maven függőség – PDF konvertálása XPS-re (Java)
url: /hu/java/conversion-export/convert-pdf-to-xps-aspose-pdf-java-selectable-text/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Aspose PDF Maven függőség – PDF konvertálása XPS-re (Java)

## Bevezetés

Ha **hozzá szeretné adni az Aspose PDF Maven függőséget**, és aztán PDF dokumentumokat XPS-re szeretne konvertálni úgy, hogy a szöveg kiválasztható maradjon, jó helyen jár. Ez az útmutató minden lépésen végigvezet – a Maven vagy Gradle beállításától, a PDF betöltéséig, az XPS beállítások konfigurálásáig, és végül egy kiválasztható szöveget tartalmazó XPS fájl mentéséig. A végére egy újrahasználható kódrészletet kap, amelyet bármely Java projektbe beilleszthet.

## Gyors válaszok
- **Milyen függőségre van szükségem?** `com.aspose:aspose-pdf` (Maven) vagy a megfelelő Gradle artefaktum.  
- **Meg tudja őrizni az XPS a kiválasztható szöveget?** Igen – az Aspose.PDF automatikusan megőrzi a szövegrétegeket.  
- **Melyik Java verzió szükséges?** JDK 8 vagy újabb.  
- **Szükség van licencre a termeléshez?** Érvényes Aspose.PDF licenc szükséges a korlátlan használathoz.  
- **Mennyi időt vesz igénybe a konvertálás?** Általában egy másodpercnél kevesebb idő alatt, ha a fájlok 100 oldal alatt vannak standard hardveren.

## Mi az Aspose PDF Maven függőség?
`aspose-pdf` Maven artefaktum biztosítja a teljes Aspose.PDF for Java API-t, lehetővé téve a PDF létrehozását, manipulálását és konvertálását külső szoftver nélkül. Ennek a függőségnek a hozzáadásával a `pom.xml` vagy `build.gradle` fájlhoz az összes szükséges bináris letöltődik, így azonnal elkezdhet kódolni manuális JAR kezelés nélkül.

## Miért konvertáljuk a PDF-et XPS-re kiválasztható szöveggel?
Az Aspose.PDF **50+ bemeneti és kimeneti formátumot** támogat, és képes XPS fájlokat generálni, amelyek megőrzik a kereshető, kiválasztható szövegréteget. Ez elengedhetetlen olyan munkafolyamatokhoz, amelyek archiválási szintű dokumentumokat, pontos elrendezésmegőrzést vagy XPS‑t támogató eszközökben történő további szerkesztést igényelnek. A konvertálás egy modern CPU-n tipikus 20‑oldalas PDF-ek esetén egy másodpercnél kevesebb idő alatt befejeződik.

## Előfeltételek

- **Java Development Kit (JDK) 8+** telepítve és a `JAVA_HOME` beállítva.  
- **Maven 3.6+** vagy **Gradle 6+** a függőségkezeléshez.  
- Alapvető ismeretek a Java fájl I/O és a kivételkezelés terén.  

### Szükséges könyvtárak és függőségek

Szüksége lesz az Aspose.PDF for Java könyvtár 25.3 vagy újabb verziójára. A következő építőeszközök egyikével adja hozzá:

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

### Környezet beállítása

Győződjön meg arról, hogy az IDE vagy az építési környezet a megfelelő JDK-re mutat, és a hálózat eléri a Maven Central-t vagy a privát tárolóját.

## Hogyan adja hozzá az Aspose PDF Maven függőséget?

`aspose-pdf` az az artefakt, amelyet a projekt építőfájljához **hozzáad**, majd **frissíti** a függőségeket, hogy a JAR-ok automatikusan letöltődjenek. Maven esetén helyezze be a `<dependency>` blokkot a `<dependencies>` belsejébe; **Gradle** esetén a `implementation` sort a `dependencies` blokkba. A frissítés után az Aspose osztályok elérhetővé válnak az osztályúton, és manuális JAR kezelése nélkül kezdhet el kódolni.

## Az Aspose.PDF for Java beállítása

### Telepítési lépések

1. **Maven/Gradle beállítás:** Adja hozzá a függőséget a fentiek szerint, és futtassa a `mvn clean install` vagy `gradle build` parancsot a könyvtár letöltéséhez.  
2. **Licenc beszerzése:**  
   - Töltsön le egy [ingyenes próbaverziót](https://releases.aspose.com/pdf/java/) vagy szerezzen be egy [ideiglenes licencet](https://purchase.aspose.com/temporary-license/).  
   - Helyezze a licencfájlt (`Aspose.Pdf.lic`) egy az alkalmazás számára elérhető mappába, és töltse be indításkor.

### Alap inicializálás

`License` egy Aspose licencfájlt alkalmaz a teljes funkcionalitás feloldásához.  
Töltse be a licencet (ha van), és hozzon létre egy `Document` objektumot a PDF-ekkel való munkához.  
`Document` egy PDF fájlt képvisel, és módszereket biztosít a tartalom manipulálásához.

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.License;

// Initialize a License object
License license = new License();

// Set the license file path
license.setLicense("path/to/Aspose.Total.Java.lic");
```  

## Hogyan konvertáljuk a PDF-et XPS-re kiválasztható szöveggel?

`XpsSaveOptions` konfigurálja a beállításokat a PDF XPS dokumentummá mentéséhez, beleértve a szöveg megőrzését.  
Töltse be a forrás PDF-et, konfigurálja a `XpsSaveOptions`-t a szöveg megőrzésére, és hívja meg a `save`-et a `.xps` kiterjesztéssel. Az API automatikusan beágyaz egy szövegréteget, így a kapott XPS kereshető és másolható, mint az eredeti PDF. Ez a teljes **folyamat** általában csak három kódsort igényel a könyvtár beállítása után.

## Implementációs útmutató

### PDF konvertálása XPS-re

Ez a funkció lehetővé teszi, hogy **konvertálja** a PDF dokumentumot XPS fájlra az Aspose.PDF for Java használatával.

#### 1. lépés: PDF dokumentum betöltése

Először töltse be a PDF dokumentumot a könyvtárából:

```java
import com.aspose.pdf.Document;

String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document pdfDocument = new Document(dataDir + "/input.pdf");
```  

#### 2. lépés: Mentési beállítások konfigurálása

Hozzon létre egy `XpsSaveOptions` példányt az XPS konvertálási beállítások konfigurálásához:

```java
import com.aspose.pdf.XpsSaveOptions;

XpsSaveOptions saveOptions = new XpsSaveOptions();
```  

#### 3. lépés: Mentés XPS fájlként

Végül mentse a dokumentumot XPS formátumban a kívánt kimeneti könyvtárba:

```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
pdfDocument.save(outputDir + "/ConvertPDFtoXPS_out.xps\
```  

## Gyakori problémák és megoldások

- **Üres oldalak az XPS kimenetben:** Győződjön meg arról, hogy a PDF nem használ titkosított adatfolyamokat; ha igen, adja meg a jelszót a `Document` betöltésekor.  
- **Memória hibák nagy PDF-eknél:** Használja a `Document.optimizeResources()`-t a mentés előtt a memóriahasználat csökkentéséhez.  
- **Hiányzó betűtípusok:** Telepítse a szükséges betűtípusokat a szerveren, vagy ágyazza be őket a PDF-be a konvertálás előtt.

## Gyakran ismételt kérdések

**K: Konvertálhatok jelszóval védett PDF-eket?**  
A: Igen – adja meg a jelszót a `Document` konstruktorának, vagy használja a `Document.open(String path, String password)` metódust a konvertálás előtt.

**K: Az XPS megőrzi a vektorgrafikákat?**  
A: Természetesen. Minden vektor alakzat, kép és szöveg megmarad, és a szöveg továbbra is kiválasztható.

**K: Kötelező licenc a próbaverzióhoz?**  
A: A próbaverzió licenc nélkül is működik, de vízjelet ad a kimenethez; egy állandó licenc eltávolítja az összes korlátozást.

**K: Hogyan kezeli az Aspose.PDF a nagy fájlokat?**  
A: Fájlokat streaming módon dolgozza fel, lehetővé téve a több száz oldalas PDF-ek konvertálását anélkül, hogy az egész dokumentumot memóriába kellene tölteni.

**K: Mely platformok támogatottak?**  
A: A könyvtár bármely, kompatibilis JDK-val rendelkező operációs rendszeren fut, beleértve a Windows, Linux és macOS rendszereket.

---

**Last Updated:** 2026-07-03  
**Tested With:** Aspose.PDF for Java 25.3  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Kapcsolódó útmutatók

- [PDF konvertálása JPEG-re az Aspose.PDF for Java segítségével: Lépésről‑lépésre útmutató](/pdf/java/conversion-export/convert-pdf-to-jpeg-aspose-java-tutorial/)
- [Hogyan konvertáljunk PDF-et Excelbe az Aspose.PDF for Java használatával | Lépésről‑lépésre útmutató](/pdf/java/conversion-export/convert-pdf-excel-aspose-java-tutorial/)
- [Hogyan konvertáljunk XPS fájlokat PDF-re az Aspose.PDF Java-ban: Teljes útmutató](/pdf/java/conversion-export/convert-xps-pdf-aspose-java-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}