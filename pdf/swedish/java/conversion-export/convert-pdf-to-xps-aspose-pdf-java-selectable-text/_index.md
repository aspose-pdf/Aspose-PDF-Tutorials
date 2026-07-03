---
date: '2026-07-03'
description: Lär dig hur du lägger till Aspose PDF Maven-beroendet och konverterar
  PDF till XPS med markerbar text med hjälp av Aspose.PDF for Java. Steg-för-steg-guide
  med förutsättningar och vanliga frågor.
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
title: Aspose PDF Maven-beroende – Konvertera PDF till XPS (Java)
url: /sv/java/conversion-export/convert-pdf-to-xps-aspose-pdf-java-selectable-text/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Aspose PDF Maven‑beroende – Konvertera PDF till XPS (Java)

## Introduktion

Om du behöver **lägga till Aspose PDF Maven‑beroendet** och sedan konvertera PDF‑dokument till XPS samtidigt som du behåller texten markerbar, är du på rätt plats. Denna handledning guidar dig genom varje steg—från att konfigurera Maven eller Gradle, till att läsa in en PDF, konfigurera XPS‑alternativ och slutligen spara en XPS‑fil med markerbar text. I slutet har du ett återanvändbart kodsnutt som du kan lägga in i vilket Java‑projekt som helst.

## Snabba svar
- **Vilket beroende behöver jag?** `com.aspose:aspose-pdf` (Maven) eller motsvarande Gradle‑artefakt.  
- **Kan XPS behålla markerbar text?** Ja—Aspose.PDF bevarar automatiskt textlager.  
- **Vilken Java‑version krävs?** JDK 8 eller nyare.  
- **Behöver jag en licens för produktion?** En giltig Aspose.PDF‑licens krävs för obegränsad användning.  
- **Hur lång tid tar konverteringen?** Vanligtvis under en sekund för filer under 100 sidor på standardhårdvara.

## Vad är Aspose PDF Maven‑beroende?
`aspose-pdf`‑Maven‑artefakten tillhandahåller hela Aspose.PDF för Java‑API:et, vilket möjliggör skapande, manipulation och konvertering av PDF utan extern programvara. Genom att lägga till detta beroende i din `pom.xml` eller `build.gradle` hämtas alla nödvändiga binärer, så att du kan börja koda omedelbart utan manuell JAR‑hantering.

## Varför konvertera PDF till XPS med markerbar text?
Aspose.PDF stödjer **50+ in‑ och utdataformat** och kan generera XPS‑filer som behåller ett sökbart, markerbart textlager. Detta är avgörande för arbetsflöden som kräver arkivkvalitet, exakt layout‑fidelitet eller efterföljande redigering i XPS‑medvetna verktyg. Konverteringar slutförs på under en sekund för typiska 20‑sidiga PDF‑filer på en modern CPU.

## Förutsättningar

- **Java Development Kit (JDK) 8+** installerat och `JAVA_HOME` konfigurerat.  
- **Maven 3.6+** eller **Gradle 6+** för beroendehantering.  
- Grundläggande kunskap om Java‑fil‑I/O och undantagshantering.  

### Nödvändiga bibliotek och beroenden

Du behöver Aspose.PDF för Java‑biblioteket version 25.3 eller senare. Inkludera det med ett av följande byggverktyg:

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

### Miljöinställning

Se till att din IDE eller byggmiljö pekar på rätt JDK och att nätverket kan nå Maven Central eller ditt privata arkiv.

## Hur lägger man till Aspose PDF Maven‑beroende?

`aspose-pdf` är artefakten du lägger till i ditt projekts byggfil, och sedan uppdaterar du beroendena så att JAR‑filerna hämtas automatiskt. För Maven, infoga `<dependency>`‑blocket inom `<dependencies>`; för Gradle, placera `implementation`‑raden i `dependencies`‑blocket. Efter uppdateringen blir Aspose‑klasserna tillgängliga på classpath, och du kan börja koda utan manuell JAR‑hantering.

## Konfigurera Aspose.PDF för Java

### Installationssteg

1. **Maven/Gradle‑setup:** Lägg till beroendet som visat ovan och kör `mvn clean install` eller `gradle build` för att hämta biblioteket.  
2. **Licensanskaffning:**  
   - Ladda ner en [free trial](https://releases.aspose.com/pdf/java/) eller skaffa en [temporary license](https://purchase.aspose.com/temporary-license/).  
   - Placera licensfilen (`Aspose.Pdf.lic`) i en mapp som är åtkomlig för din applikation och läs in den vid start.

### Grundläggande initiering

`License` applicerar en Aspose‑licensfil för att låsa upp full funktionalitet.  
Läs in licensen (om du har en) och skapa ett `Document`‑objekt för att arbeta med PDF‑filer.  
`Document` representerar en PDF‑fil och tillhandahåller metoder för att manipulera dess innehåll.

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.License;

// Initialize a License object
License license = new License();

// Set the license file path
license.setLicense("path/to/Aspose.Total.Java.lic");
```  

## Hur konverterar man PDF till XPS med markerbar text?

`XpsSaveOptions` konfigurerar inställningarna för att spara en PDF som ett XPS‑dokument, inklusive bevarande av text. Läs in käll‑PDF‑filen, konfigurera `XpsSaveOptions` för att bevara text och anropa `save` med filändelsen `.xps`. API‑et bäddar automatiskt in ett textlager, så den resulterande XPS‑filen kan sökas och kopieras precis som original‑PDF‑filen. Hela processen kräver vanligtvis bara tre kodrader efter att biblioteket är konfigurerat.

## Implementeringsguide

### Konvertera PDF till XPS

Denna funktion gör det möjligt att konvertera ett PDF‑dokument till en XPS‑fil med hjälp av Aspose.PDF för Java.

#### Steg 1: Läs in PDF‑dokumentet

Först läser du in ditt PDF‑dokument från dess katalog:

```java
import com.aspose.pdf.Document;

String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document pdfDocument = new Document(dataDir + "/input.pdf");
```  

#### Steg 2: Konfigurera sparalternativ

Skapa en instans av `XpsSaveOptions` för att ställa in XPS‑konverteringsalternativen:

```java
import com.aspose.pdf.XpsSaveOptions;

XpsSaveOptions saveOptions = new XpsSaveOptions();
```  

#### Steg 3: Spara som XPS‑fil

Slutligen sparar du dokumentet i XPS‑format till önskad utdatamapp:

```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
pdfDocument.save(outputDir + "/ConvertPDFtoXPS_out.xps\
```  

## Vanliga problem och lösningar

- **Tomma sidor i XPS‑utdata:** Säkerställ att PDF‑filen inte använder krypterade strömmar; om den gör det, ange lösenordet när du laddar `Document`.  
- **Minnesfel på stora PDF‑filer:** Använd `Document.optimizeResources()` före sparning för att minska minnesfotavtrycket.  
- **Saknade teckensnitt:** Installera de nödvändiga teckensnitten på servern eller bädda in dem i PDF‑filen innan konvertering.

## Vanliga frågor

**Q: Kan jag konvertera lösenordsskyddade PDF‑filer?**  
A: Ja—ange lösenordet till `Document`‑konstruktorn eller använd `Document.open(String path, String password)` innan konvertering.

**Q: Behåller XPS vektorgrafik?**  
A: Absolut. Alla vektorformer, bilder och text bevaras, och texten förblir markerbar.

**Q: Är en licens obligatorisk för provversionen?**  
A: Provversionen fungerar utan licens men lägger till ett vattenmärke i utdata; en permanent licens tar bort alla begränsningar.

**Q: Hur hanterar Aspose.PDF stora filer?**  
A: Det bearbetar filer i ett strömningsläge, vilket möjliggör konvertering av PDF‑filer med hundratals sidor utan att hela dokumentet laddas in i minnet.

**Q: Vilka plattformar stöds?**  
A: Biblioteket körs på alla OS med en kompatibel JDK, inklusive Windows, Linux och macOS.

---

**Senast uppdaterad:** 2026-07-03  
**Testat med:** Aspose.PDF for Java 25.3  
**Författare:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Relaterade handledningar

- [Konvertera PDF till JPEG med Aspose.PDF för Java: Steg‑för‑steg‑guide](/pdf/java/conversion-export/convert-pdf-to-jpeg-aspose-java-tutorial/)
- [Hur man konverterar PDF till Excel med Aspose.PDF för Java | Steg‑för‑steg‑guide](/pdf/java/conversion-export/convert-pdf-excel-aspose-java-tutorial/)
- [Hur man konverterar XPS‑filer till PDF med Aspose.PDF i Java: En komplett guide](/pdf/java/conversion-export/convert-xps-pdf-aspose-java-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}