---
date: '2026-05-28'
description: Erfahren Sie, wie Sie das Single Page View PDF einstellen, die Anzeigeeinstellungen
  ändern, Lesezeichen bearbeiten und PDF-Einstellungen mit Aspose.PDF für Java konfigurieren.
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
title: Single Page View PDF in Java – Layout ändern & Lesezeichen bearbeiten
url: /de/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/products-backtop-button >}}
# Einzelne Seitenansicht PDF in Java – Layout ändern & Lesezeichen bearbeiten

## Einleitung
Wenn Leser ein großes PDF öffnen, kann das Standard‑Viewer‑Layout kontinuierlich scrollen, sodass es schwer fällt, sich auf eine einzelne Seite zu konzentrieren. Durch das Konfigurieren der **single page view pdf**‑Einstellung zwingen Sie den Viewer, jeweils nur eine Seite anzuzeigen – ideal für Berichte, E‑Books und Kataloge. In diesem Tutorial lernen Sie außerdem, wie Sie vorhandene PDF‑Lesezeichen bearbeiten, Lesezeichenziele beim Erstellen eines Dokuments festlegen und weitere Viewer‑Einstellungen mit Aspose.PDF für Java anpassen. Am Ende haben Sie die volle Kontrolle über Navigation, Lesezeichen‑Genauigkeit und das Layout auf dem Bildschirm.

**Was Sie lernen werden**
- Wie man vorhandene PDF‑Lesezeichen bearbeitet, sodass sie auf den Beginn einer Seite zeigen.  
- Wie man Lesezeichenziele beim Erstellen eines PDFs festlegt.  
- Wie man Viewer‑Einstellungen wie das Einzelseiten‑Layout ändert.  
- Praktische Tipps zum Laden eines PDF‑Dokuments in Java und zur Leistungsoptimierung.

### Schnellantworten
- **Wie aktiviert man am besten die Einzelne‑Seiten‑Ansicht für PDFs?** Rufen Sie `PdfContentEditor.changeViewerPreference()` mit `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE` auf.  
- **Können Lesezeichenziele nach der PDF‑Erstellung bearbeitet werden?** Ja – laden Sie das Dokument, holen Sie das Outline und weisen Sie ein neues `ExplicitDestination` zu.  
- **Benötige ich eine Lizenz für diese Funktionen?** Eine kostenlose Testversion reicht für die Evaluation; eine Voll‑Lizenz entfernt alle Einschränkungen.  
- **Welche Maven‑Abhängigkeit ist erforderlich?** `com.aspose:aspose-pdf:25.3` (oder neuer).  
- **Ist das mit Java 11 und höher kompatibel?** Absolut – Aspose.PDF unterstützt Java 8+.

## Was ist „PDF-Seitenlayout ändern“?
Das Ändern des PDF‑Seitenlayouts steuert, wie Seiten in einem Viewer angezeigt werden – Einzelne Seite, kontinuierlich, Zwei‑Seiten‑Ansicht usw. Das Aktivieren von **single page view pdf** verbessert die Lesbarkeit langer Dokumente und stellt sicher, dass jede Seite isoliert dargestellt wird, was besonders auf Mobilgeräten und Tablets hilfreich ist.

## Warum PDF‑Lesezeichen bearbeiten und Lesezeichenziele festlegen?
Lesezeichen funktionieren wie ein dynamisches Inhaltsverzeichnis. Präzise Ziele ermöglichen es Lesern, direkt zum gewünschten Abschnitt zu springen, wodurch überflüssiges Scrollen entfällt und die Nutzerfrustration sinkt. Das führt zu einer flüssigeren Navigation und höherer Zufriedenheit bei technischen Handbüchern, Produktkatalogen und digitalen Büchern.

## Voraussetzungen
- **Bibliotheken & Abhängigkeiten**: Aspose.PDF für Java v25.3 oder neuer.  
- **Umgebung**: JDK 8 oder neuer, Maven‑ oder Gradle‑Build‑Tool.  
- **Kenntnisse**: Grundlegende Java‑Programmierung und Vertrautheit mit PDF‑Konzepten.

## Einrichtung von Aspose.PDF für Java
### Maven-Installation
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### Gradle-Installation
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**Lizenzbeschaffung**: Beginnen Sie mit einer kostenlosen Testversion oder beantragen Sie eine temporäre Lizenz für den vollen Funktionsumfang. Für den Produktionseinsatz empfiehlt sich der Kauf einer dauerhaften Lizenz.

### Grundlegende Initialisierung
Die Klasse `Document` ist das Kernobjekt von Aspose.PDF, das eine PDF‑Datei im Speicher repräsentiert. Nach dem Erstellen einer Instanz laufen alle Lese‑/Schreib‑Operationen über dieses Objekt.  
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

## Implementierungsleitfaden
### Wie man das PDF‑Seitenlayout in Java ändert
**Übersicht**: Passen Sie Viewer‑Einstellungen an, um Seiten nach Ihren Wünschen darzustellen.

#### Initialisierung von PdfContentEditor
`PdfContentEditor` ist eine Hilfsklasse, mit der Sie Viewer‑Einstellungen ändern können, ohne das gesamte Dokument neu zu schreiben.  
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### Ändern der Viewer-Einstellungen
Um **single page view pdf** zu aktivieren, rufen Sie `changeViewerPreference()` mit dem entsprechenden Enum‑Wert auf. Dieser Aufruf aktualisiert das interne Viewer‑Preference‑Dictionary des PDFs.  
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### Speichern des aktualisierten Dokuments
Nach dem Ändern der Einstellungen rufen Sie `save()` auf, um die Änderungen auf die Festplatte zu schreiben.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

## Wie man PDF‑Lesezeichen bearbeitet
**Antwort**: Um vorhandene Lesezeichen zu ändern, laden Sie das PDF mit `Document`, holen Sie die Outline‑Collection, finden das gewünschte `OutlineItem` und weisen ihm ein neues `ExplicitDestination` zu, das auf die korrekte Seite und Koordinaten zeigt. Nach dem Aktualisieren jedes Lesezeichens speichern Sie das Dokument, um die Änderungen zu übernehmen. So werden Benutzer exakt zu den gewünschten Abschnitten geleitet, ohne zusätzliches Scrollen.

#### Zugriff auf Lesezeichen
Die `OutlineItemCollection` repräsentiert den hierarchischen Lesezeichen‑Baum. Rufen Sie sie aus dem `Document`‑Objekt ab, um mit einzelnen Einträgen zu arbeiten.  
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### Festlegen eines neuen Ziels
Ein `ExplicitDestination` definiert die genaue Seite und Position, zu der ein Lesezeichen springen soll. Weisen Sie es der `Destination`‑Eigenschaft des Outline‑Items zu.  
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### Änderungen speichern
Persistieren Sie den aktualisierten Lesezeichen‑Baum, indem Sie `document.save()` aufrufen.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

## Wie man ein Lesezeichenziel beim Erstellen eines PDFs festlegt
**Antwort**: Beim Generieren eines PDFs können Sie Lesezeichen on‑the‑fly erstellen, indem Sie `OutlineItem`‑Objekte instanziieren, deren Titel setzen und ein `ExplicitDestination` definieren, das eine bestimmte Seite und Ansicht anvisiert. Fügen Sie jedes Lesezeichen vor dem Speichern zur Outline‑Collection des Dokuments hinzu, sodass die resultierende Datei einen sofort nutzbaren Navigationsbaum enthält.

#### Erstellen und Konfigurieren von Lesezeichen
`OutlineItem` stellt einen einzelnen Lesezeicheneintrag im PDF‑Outline dar. Beim Aufbau eines PDFs von Grund auf erstellen Sie ein neues `OutlineItem` und fügen es der Outline‑Collection des Dokuments hinzu.  
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### Definieren des Lesezeichenziels
Verwenden Sie `ExplicitDestination.createFitH(page, top)`, um die Ansicht an den oberen Rand der Zielseite zu positionieren.  
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### Hinzufügen und Speichern des PDFs
Zum Schluss fügen Sie das Lesezeichen dem Outline hinzu und speichern das Dokument.  
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## Praktische Anwendungen
1. **Digitale Bücher** – Stellen Sie sicher, dass jedes Kapitel‑Lesezeichen oben auf der Seite landet für ein nahtloses Leseerlebnis.  
2. **Technische Handbücher** – Präzise Navigation hilft Ingenieuren, Abschnitte schnell zu finden, besonders in großen PDFs.  
3. **Produktkataloge** – Das Einzel‑Seiten‑Layout macht das Durchblättern von Katalogen auf Tablets intuitiver.

## Leistungsüberlegungen
- **Ressourcenoptimierung**: Aspose.PDF kann PDFs bis zu 2 GB verarbeiten, ohne die gesamte Datei in den Speicher zu laden, dank seiner Streaming‑Architektur. Nutzen Sie `Document.optimizeResources()`, um den Speicherverbrauch weiter zu reduzieren.  
- **Java‑Speichermanagement**: Schließen Sie Streams explizit und lassen Sie den Garbage Collector Objekte nach der Verarbeitung freigeben, um Speicherlecks zu vermeiden.

## Häufige Probleme & Lösungen
- **Lesezeichen werden nicht aktualisiert**: Vergewissern Sie sich, dass Sie den richtigen Outline‑Index ändern (`get_Item(1)` bezieht sich auf das erste Lesezeichen der obersten Ebene).  
- **Viewer‑Einstellung wird nicht übernommen**: Stellen Sie sicher, dass Sie `editor.save()` nach dem Ändern der Einstellungen aufrufen; sonst bleiben die Änderungen nur im Speicher.  
- **Lizenz‑Ausnahmen**: Eine Testlizenz kann Wasserzeichen hinzufügen; für die Produktion benötigen Sie eine Voll‑Lizenz.

## Häufig gestellte Fragen
**F: Was ist der einfachste Weg, ein PDF‑Dokument in Java zu laden?**  
A: Verwenden Sie `new Document("path/to/file.pdf")`; Aspose.PDF erkennt das Dateiformat automatisch.

**F: Kann ich das Seitenlayout ändern, ohne PdfContentEditor zu benutzen?**  
A: Ja, Sie können Viewer‑Einstellungen direkt am `Document`‑Objekt über `pdfDocument.getViewerPreferences().setPageLayout(...)` setzen.

**F: Wirkt sich das Ändern des Viewer‑Layouts auf den Druck aus?**  
A: Das Viewer‑Layout beeinflusst nur die Anzeige auf dem Bildschirm; die Druckausgabe bleibt unverändert.

**F: Gibt es Beschränkungen für die Anzahl der erstellbaren Lesezeichen?**  
A: Es gibt kein festes Limit, aber sehr große Outline‑Bäume können die Leistung beeinträchtigen; halten Sie sie strukturiert.

**F: Wie stelle ich sicher, dass Lesezeichenziele nach dem Hinzufügen oder Entfernen von Seiten korrekt bleiben?**  
A: Berechnen Sie die Ziele nach strukturellen Änderungen erneut anhand der aktuellen Seitenindizes.

## Ressourcen
- **Dokumentation**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **Download**: [Latest Releases for Java](https://releases.aspose.com/pdf/java/)
- **Kauf**: [Buy Aspose.PDF License](https://purchase.aspose.com/buy)
- **Kostenlose Testversion**: [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)
- **Temporäre Lizenz**: [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**Zuletzt aktualisiert:** 2026-05-28  
**Getestet mit:** Aspose.PDF für Java v25.3  
**Autor:** Aspose

## Verwandte Tutorials

- [How to Change PDF Viewer Preferences Using Aspose.PDF for Java: A Comprehensive Guide](/pdf/java/printing-rendering/modify-pdf-viewer-preferences-aspose-pdf-java/)
- [How to Create PDF Bookmarks and Manage Navigation Using Aspose.PDF for Java](/pdf/java/bookmarks-navigation/create-manage-pdf-bookmarks-aspose-java/)
- [PDF Bookmarks and Navigation Tutorials for Aspose.PDF Java](/pdf/java/bookmarks-navigation/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}