---
date: '2026-05-28'
description: Lär dig hur du ställer in PDF med enkel sidvy, ändrar visarinställningar,
  redigerar bokmärken och konfigurerar PDF-inställningar med Aspose.PDF för Java.
keywords:
- single page view pdf
- aspose pdf maven dependency
- change pdf viewer preference
- configure pdf viewer settings
- set pdf bookmark destination
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  headline: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  type: TechArticle
- description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  name: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  steps:
  - name: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
    text: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
  - name: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
    text: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
  - name: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
    text: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
  type: HowTo
- questions:
  - answer: Use `new Document("path/to/file.pdf")`; Aspose.PDF automatically detects
      the file format.
    question: What is the easiest way to load a PDF document in Java?
  - answer: Yes, you can set viewer preferences directly on the `Document` object
      via `pdfDocument.getViewerPreferences().setPageLayout(...)`.
    question: Can I change the page layout without using PdfContentEditor?
  - answer: Viewer layout only influences on‑screen display; it does not alter the
      printed output.
    question: Does changing the viewer layout affect printing?
  - answer: No explicit limit, but extremely large outline trees may impact performance;
      keep them organized.
    question: Are there limits on the number of bookmarks I can create?
  - answer: Re‑calculate destinations using the current page indices after any structural
      changes.
    question: How do I ensure bookmark destinations are accurate after adding or removing
      pages?
  type: FAQPage
title: PDF med enkel sidvy i Java – Ändra layout och redigera bokmärken
url: /sv/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/products-backtop-button >}}
# Ensidig PDF-visning i Java – Ändra layout och redigera bokmärken

## Introduktion
När läsare öppnar en stor PDF kan standardvisarens layout rulla kontinuerligt, vilket gör det svårt att fokusera på en enskild sida. Genom att konfigurera inställningen **single page view pdf** tvingar du visaren att visa en sida åt gången, vilket är idealiskt för rapporter, e‑böcker och kataloger. I den här handledningen kommer du också att lära dig hur du redigerar befintliga PDF‑bokmärken, sätter bokmärkesdestinationer medan du skapar ett dokument och finjusterar andra visarinställningar med Aspose.PDF för Java. I slutet har du full kontroll över navigering, bokmärkesnoggrannhet och skärm‑layout.

**Vad du kommer att lära dig**
- Hur man redigerar befintliga PDF‑bokmärken så att de pekar på början av en sida.  
- Hur man sätter bokmärkesdestinationer medan man skapar en PDF.  
- Hur man ändrar visarinställningar såsom en‑sidig layout.  
- Praktiska tips för att ladda ett PDF‑dokument i Java och optimera prestanda.

### Snabba svar
- **Vad är det primära sättet att aktivera ensidig PDF‑visning?** Anropa `PdfContentEditor.changeViewerPreference()` med `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.  
- **Kan bokmärkesdestinationer redigeras efter att en PDF har genererats?** Ja – ladda dokumentet, hämta outline och tilldela en ny `ExplicitDestination`.  
- **Behöver jag en licens för dessa funktioner?** En gratis provversion fungerar för utvärdering; en full licens tar bort alla begränsningar.  
- **Vilket Maven‑beroende krävs?** `com.aspose:aspose-pdf:25.3` (or later).  
- **Är detta kompatibelt med Java 11 och senare?** Absolut – Aspose.PDF stödjer Java 8+.

## Vad är “change PDF page layout”?
Att ändra PDF‑sidlayout styr hur sidor visas i en visare—ensidig, kontinuerlig, två‑sidig vy osv. Att aktivera **single page view pdf** förbättrar läsbarheten för långa dokument och säkerställer att varje sida presenteras isolerat, vilket är särskilt hjälpsamt på mobila enheter och surfplattor.

## Varför redigera PDF‑bokmärken och sätta bokmärkesdestinationer?
Bokmärken fungerar som en dynamisk innehållsförteckning. Exakta destinationer låter läsare hoppa direkt till den avsedda sektionen, vilket eliminerar extra rullning och minskar användarfrustration. Detta leder till en smidigare navigeringsupplevelse och högre tillfredsställelse för tekniska manualer, produktkataloger och digitala böcker.

## Förutsättningar
- **Bibliotek & beroenden**: Aspose.PDF för Java v25.3 eller senare.  
- **Miljö**: JDK 8 eller nyare, Maven‑ eller Gradle‑byggverktyg.  
- **Kunskap**: Grundläggande Java‑programmering och bekantskap med PDF‑koncept.

## Installera Aspose.PDF för Java
### Maven‑installation
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### Gradle‑installation
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**Licensanskaffning**: Starta med en gratis provversion eller begär en tillfällig licens för fullständig funktionstillgång. Överväg att köpa en permanent licens för produktionsbruk.

### Grundläggande initialisering
`Document`‑klassen är Aspose.PDF:s kärnobjekt som representerar en PDF‑fil i minnet. Efter att en instans har skapats flödar alla läs‑/skriv‑operationer genom detta objekt.  
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

## Implementeringsguide
### Hur man ändrar PDF‑sidlayout i Java
**Översikt**: Justera visarinställningarna för att visa sidor på det sätt du önskar.

#### Initiering av PdfContentEditor
`PdfContentEditor` är en verktygsklass som låter dig ändra visarinställningar utan att skriva om hela dokumentet.  
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### Ändra visarinställningar
För att aktivera **single page view pdf**, anropa `changeViewerPreference()` med rätt enum‑värde. Detta anrop uppdaterar PDF:ens interna visarinställnings‑ordbok.  
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### Spara uppdaterat dokument
Efter att ha ändrat inställningarna, anropa `save()` för att skriva tillbaka ändringarna till disk.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

## Hur man redigerar PDF‑bokmärken
**Svar**: För att modifiera befintliga bokmärken, ladda PDF‑en med `Document`, hämta dess outline‑samling, lokalisera önskat `OutlineItem` och tilldela en ny `ExplicitDestination` som pekar på rätt sida och koordinater. Efter att ha uppdaterat varje bokmärke, spara dokumentet för att bevara ändringarna. Detta säkerställer att användare leds exakt till de avsedda sektionerna utan extra rullning.

#### Åtkomst till bokmärken
`OutlineItemCollection` representerar det hierarkiska bokmärkesträdet. Hämta den från `Document`‑objektet för att arbeta med enskilda poster.  
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### Ställa in en ny destination
En `ExplicitDestination` definierar den exakta sidan och platsen ett bokmärke ska hoppa till. Tilldela den till `Destination`‑egenskapen för outline‑objektet.  
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### Spara ändringar
Bevara det uppdaterade bokmärkesträdet genom att anropa `document.save()`.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

## Hur man sätter bokmärkesdestination vid skapande av en PDF
**Svar**: När du genererar en PDF kan du skapa bokmärken i farten genom att instansiera `OutlineItem`‑objekt, sätta deras titlar och definiera en `ExplicitDestination` som riktar sig mot en specifik sida och visningsläge. Lägg till varje bokmärke i dokumentets outline‑samling innan du sparar, så att den resulterande filen innehåller ett färdigt navigeringsträd.

#### Skapa och konfigurera bokmärke
`OutlineItem` representerar en enskild bokmärkespost i PDF‑outline. När du bygger en PDF från grunden, instansiera ett nytt `OutlineItem` och lägg till det i dokumentets outline‑samling.  
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### Definiera bokmärkesdestination
Använd `ExplicitDestination.createFitH(page, top)` för att placera vyn högst upp på målsidan.  
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### Lägga till och spara PDF‑en
Slutligen, lägg till bokmärket i outline och spara dokumentet.  
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## Praktiska tillämpningar
1. **Digitala böcker** – Säkerställ att varje kapitels bokmärke landar högst upp på sidan för en sömlös läsupplevelse.  
2. **Tekniska manualer** – Precisionsnavigering hjälper ingenjörer att snabbt hitta sektioner, särskilt i stora PDF‑er.  
3. **Produktkataloger** – Ensidig layout gör bläddring av kataloger på surfplattor mer intuitiv.

## Prestandaöverväganden
- **Optimera resurser**: Aspose.PDF kan bearbeta PDF‑filer upp till 2 GB utan att ladda hela filen i minnet, tack vare sin streaming‑arkitektur. Använd `Document.optimizeResources()` för att ytterligare minska minnesavtrycket.  
- **Java‑minneshantering**: Stäng explicit strömmar och låt skräpsamlaren återta objekt efter bearbetning för att undvika minnesläckor.

## Vanliga problem & lösningar
- **Bokmärken uppdateras inte**: Verifiera att du modifierar rätt outline‑index (`get_Item(1)` refererar till det första top‑nivå bokmärket).  
- **Visarinställning tillämpas inte**: Säkerställ att du anropar `editor.save()` efter att ha ändrat inställningarna; annars förblir ändringarna bara i minnet.  
- **Licensundantag**: En provlicens kan lägga till vattenstämplar; skaffa en full licens för produktion.

## Vanliga frågor
**Q: Vad är det enklaste sättet att ladda ett PDF‑dokument i Java?**  
A: Använd `new Document("path/to/file.pdf")`; Aspose.PDF upptäcker automatiskt filformatet.

**Q: Kan jag ändra sidlayout utan att använda PdfContentEditor?**  
A: Ja, du kan sätta visarinställningar direkt på `Document`‑objektet via `pdfDocument.getViewerPreferences().setPageLayout(...)`.

**Q: Påverkar ändring av visarlayout utskrift?**  
A: Visarlayout påverkar endast skärmvisning; den ändrar inte utskriftsresultatet.

**Q: Finns det begränsningar för hur många bokmärken jag kan skapa?**  
A: Ingen explicit begränsning, men extremt stora outline‑träd kan påverka prestanda; håll dem organiserade.

**Q: Hur säkerställer jag att bokmärkesdestinationer är korrekta efter att ha lagt till eller tagit bort sidor?**  
A: Beräkna om destinationerna med de aktuella sidindexen efter eventuella strukturella förändringar.

## Resurser
- **Dokumentation**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **Nedladdning**: [Latest Releases for Java](https://releases.aspose.com/pdf/java/)
- **Köp**: [Köp Aspose.PDF-licens](https://purchase.aspose.com/buy)
- **Prova Aspose.PDF gratis**: [Prova Aspose.PDF gratis](https://releases.aspose.com/pdf/java/)
- **Begär tillfällig licens**: [Begär tillfällig licens](https://purchase.aspose.com/temporary-license)

---

**Senast uppdaterad:** 2026-05-28  
**Testat med:** Aspose.PDF för Java v25.3  
**Författare:** Aspose

## Relaterade handledningar

- [Hur man ändrar PDF‑visarinställningar med Aspose.PDF för Java: En omfattande guide](/pdf/java/printing-rendering/modify-pdf-viewer-preferences-aspose-pdf-java/)
- [Hur man skapar PDF‑bokmärken och hanterar navigation med Aspose.PDF för Java](/pdf/java/bookmarks-navigation/create-manage-pdf-bookmarks-aspose-java/)
- [PDF‑bokmärken och navigationshandledningar för Aspose.PDF Java](/pdf/java/bookmarks-navigation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}