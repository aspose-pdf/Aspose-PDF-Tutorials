---
date: '2026-07-03'
description: Erfahren Sie, wie Sie die Aspose PDF Maven-Abhängigkeit hinzufügen und
  PDF mit auswählbarem Text mithilfe von Aspose.PDF für Java nach XPS konvertieren.
  Schritt‑für‑Schritt-Anleitung mit Voraussetzungen und FAQs.
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
title: Aspose PDF Maven-Abhängigkeit – PDF nach XPS konvertieren (Java)
url: /de/java/conversion-export/convert-pdf-to-xps-aspose-pdf-java-selectable-text/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Aspose PDF Maven-Abhängigkeit – PDF nach XPS konvertieren (Java)

## Einleitung

Wenn Sie die **Aspose PDF Maven-Abhängigkeit hinzufügen** und anschließend PDF-Dokumente in XPS konvertieren möchten, wobei der Text auswählbar bleibt, sind Sie hier genau richtig. Dieses Tutorial führt Sie durch jeden Schritt – von der Konfiguration von Maven oder Gradle über das Laden einer PDF, das Konfigurieren der XPS-Optionen bis hin zum Speichern einer XPS-Datei mit auswählbarem Text. Am Ende haben Sie einen wiederverwendbaren Code‑Snippet, den Sie in jedes Java‑Projekt einbinden können.

## Schnelle Antworten
- **Welche Abhängigkeit benötige ich?** `com.aspose:aspose-pdf` (Maven) oder das entsprechende Gradle‑Artefakt.  
- **Kann das XPS auswählbaren Text behalten?** Ja – Aspose.PDF bewahrt Textschichten automatisch.  
- **Welche Java-Version wird benötigt?** JDK 8 oder neuer.  
- **Benötige ich eine Lizenz für die Produktion?** Eine gültige Aspose.PDF‑Lizenz ist für uneingeschränkte Nutzung erforderlich.  
- **Wie lange dauert die Konvertierung?** In der Regel weniger als eine Sekunde für Dateien mit weniger als 100 Seiten auf Standard‑Hardware.

## Was ist die Aspose PDF Maven-Abhängigkeit?
Das Maven‑Artefakt `aspose-pdf` stellt die vollständige Aspose.PDF für Java‑API bereit und ermöglicht das Erstellen, Manipulieren und Konvertieren von PDFs ohne externe Software. Durch das Hinzufügen dieser Abhängigkeit zu Ihrer `pom.xml` oder `build.gradle` werden alle erforderlichen Binärdateien eingebunden, sodass Sie sofort mit dem Coden beginnen können, ohne JAR‑Dateien manuell verwalten zu müssen.

## Warum PDF zu XPS mit auswählbarem Text konvertieren?
Aspose.PDF unterstützt **mehr als 50 Eingabe‑ und Ausgabeformate** und kann XPS‑Dateien erzeugen, die eine durchsuchbare, auswählbare Textebene behalten. Das ist entscheidend für Workflows, die archivwürdige Dokumente, exakte Layout‑Treue oder nachgelagerte Bearbeitung in XPS‑fähigen Tools erfordern. Konvertierungen werden in weniger als einer Sekunde für typische 20‑Seiten‑PDFs auf einer modernen CPU abgeschlossen.

## Voraussetzungen

- **Java Development Kit (JDK) 8+** installiert und `JAVA_HOME` konfiguriert.  
- **Maven 3.6+** oder **Gradle 6+** für das Abhängigkeitsmanagement.  
- Grundlegende Kenntnisse in Java‑Datei‑I/O und Ausnahmebehandlung.  

### Erforderliche Bibliotheken und Abhängigkeiten

Sie benötigen die Aspose.PDF für Java‑Bibliothek in Version 25.3 oder höher. Binden Sie sie mit einem der folgenden Build‑Tools ein:

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

### Umgebung einrichten

Stellen Sie sicher, dass Ihre IDE oder Ihre Build‑Umgebung auf das richtige JDK zeigt und dass das Netzwerk Maven Central oder Ihr privates Repository erreichen kann.

## Wie fügt man die Aspose PDF Maven-Abhängigkeit hinzu?

`aspose-pdf` ist das Artefakt, das Sie zu Ihrer Projekt‑Build‑Datei hinzufügen und anschließend die Abhängigkeiten aktualisieren, damit die JARs automatisch heruntergeladen werden. Für Maven fügen Sie den `<dependency>`‑Block innerhalb von `<dependencies>` ein; für Gradle platzieren Sie die `implementation`‑Zeile im `dependencies`‑Block. Nach dem Aktualisieren stehen die Aspose‑Klassen im Klassenpfad zur Verfügung, und Sie können ohne manuelle JAR‑Verwaltung mit dem Coden beginnen.

## Einrichtung von Aspose.PDF für Java

### Installationsschritte

1. **Maven/Gradle‑Einrichtung:** Fügen Sie die Abhängigkeit wie oben gezeigt hinzu und führen Sie `mvn clean install` oder `gradle build` aus, um die Bibliothek zu beziehen.  
2. **Lizenzbeschaffung:**  
   - Laden Sie eine [kostenlose Testversion](https://releases.aspose.com/pdf/java/) herunter oder erhalten Sie eine [temporäre Lizenz](https://purchase.aspose.com/temporary-license/).  
   - Legen Sie die Lizenzdatei (`Aspose.Pdf.lic`) in einen für Ihre Anwendung zugänglichen Ordner und laden Sie sie beim Start.

### Grundlegende Initialisierung

`License` wendet eine Aspose‑Lizenzdatei an, um die volle Funktionalität freizuschalten.  
Laden Sie die Lizenz (falls vorhanden) und erstellen Sie ein `Document`‑Objekt, um mit PDFs zu arbeiten.  
`Document` repräsentiert eine PDF‑Datei und bietet Methoden zur Manipulation ihres Inhalts.

```java
import com.aspose.pdf.Document;
import com.aspose.pdf.License;

// Initialize a License object
License license = new License();

// Set the license file path
license.setLicense("path/to/Aspose.Total.Java.lic");
```  

## Wie konvertiert man PDF zu XPS mit auswählbarem Text?

`XpsSaveOptions` konfiguriert die Einstellungen zum Speichern einer PDF als XPS‑Dokument, einschließlich der Text‑Erhaltung.  
Laden Sie die Quell‑PDF, konfigurieren Sie `XpsSaveOptions` zur Text‑Erhaltung und rufen Sie `save` mit der `.xps`‑Erweiterung auf. Die API bettet automatisch eine Textebene ein, sodass das resultierende XPS wie das ursprüngliche PDF durchsucht und kopiert werden kann. Dieser gesamte Vorgang erfordert in der Regel nur drei Code‑Zeilen, nachdem die Bibliothek eingerichtet ist.

## Implementierungsleitfaden

### PDF zu XPS konvertieren

Diese Funktion ermöglicht es Ihnen, ein PDF‑Dokument mit Aspose.PDF für Java in eine XPS‑Datei zu konvertieren.

#### Schritt 1: PDF-Dokument laden

Laden Sie zunächst Ihr PDF‑Dokument aus dem entsprechenden Verzeichnis:

```java
import com.aspose.pdf.Document;

String dataDir = "YOUR_DOCUMENT_DIRECTORY";
Document pdfDocument = new Document(dataDir + "/input.pdf");
```  

#### Schritt 2: Speicheroptionen konfigurieren

Erstellen Sie eine Instanz von `XpsSaveOptions`, um die XPS‑Konvertierungsoptionen festzulegen:

```java
import com.aspose.pdf.XpsSaveOptions;

XpsSaveOptions saveOptions = new XpsSaveOptions();
```  

#### Schritt 3: Als XPS-Datei speichern

Speichern Sie schließlich das Dokument im XPS‑Format in Ihrem gewünschten Ausgabeverzeichnis:

```java
String outputDir = "YOUR_OUTPUT_DIRECTORY";
pdfDocument.save(outputDir + "/ConvertPDFtoXPS_out.xps\
```  

## Häufige Probleme und Lösungen

- **Leere Seiten in der XPS‑Ausgabe:** Stellen Sie sicher, dass das PDF keine verschlüsselten Streams verwendet; falls doch, geben Sie das Passwort beim Laden des `Document` an.  
- **Speicherfehler bei großen PDFs:** Verwenden Sie `Document.optimizeResources()` vor dem Speichern, um den Speicherverbrauch zu reduzieren.  
- **Fehlende Schriftarten:** Installieren Sie die benötigten Schriftarten auf dem Server oder betten Sie sie vor der Konvertierung in das PDF ein.

## Häufig gestellte Fragen

**F: Kann ich passwortgeschützte PDFs konvertieren?**  
A: Ja – übergeben Sie das Passwort dem `Document`‑Konstruktor oder verwenden Sie `Document.open(String path, String password)` vor der Konvertierung.

**F: Behält das XPS Vektorgrafiken bei?**  
A: Absolut. Alle Vektorformen, Bilder und Texte werden erhalten, und der Text bleibt auswählbar.

**F: Ist eine Lizenz für die Testversion zwingend erforderlich?**  
A: Die Testversion funktioniert ohne Lizenz, fügt jedoch ein Wasserzeichen zum Ergebnis hinzu; eine permanente Lizenz entfernt alle Einschränkungen.

**F: Wie geht Aspose.PDF mit großen Dateien um?**  
A: Es verarbeitet Dateien streaming‑basiert, sodass PDFs mit Hunderten von Seiten konvertiert werden können, ohne das gesamte Dokument in den Speicher zu laden.

**F: Welche Plattformen werden unterstützt?**  
A: Die Bibliothek läuft auf jedem Betriebssystem mit einem kompatiblen JDK, einschließlich Windows, Linux und macOS.

---

**Last Updated:** 2026-07-03  
**Tested With:** Aspose.PDF for Java 25.3  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Verwandte Tutorials

- [PDF zu JPEG mit Aspose.PDF für Java konvertieren: Schritt‑für‑Schritt‑Anleitung](/pdf/java/conversion-export/convert-pdf-to-jpeg-aspose-java-tutorial/)
- [Wie man PDF zu Excel mit Aspose.PDF für Java konvertiert | Schritt‑für‑Schritt‑Anleitung](/pdf/java/conversion-export/convert-pdf-excel-aspose-java-tutorial/)
- [Wie man XPS‑Dateien mit Aspose.PDF in Java zu PDF konvertiert: Eine vollständige Anleitung](/pdf/java/conversion-export/convert-xps-pdf-aspose-java-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}