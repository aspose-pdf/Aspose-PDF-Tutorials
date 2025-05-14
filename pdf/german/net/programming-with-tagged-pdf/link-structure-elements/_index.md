---
"description": "Erfahren Sie, wie Sie mit Aspose.PDF für .NET Linkstrukturelemente in einer PDF-Datei erstellen. Schritt-für-Schritt-Anleitung zum Hinzufügen barrierefreier Links, Bilder und zur Konformitätsvalidierung."
"linktitle": "Linkstrukturelemente"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Linkstrukturelemente"
"url": "/de/net/programming-with-tagged-pdf/link-structure-elements/"
"weight": 120
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Linkstrukturelemente

## Einführung

Das Erstellen und Verwalten von Linkstrukturelementen in PDF-Dateien kann für Dokumente, die Barrierefreiheit und eine reibungslose Navigation erfordern, entscheidend sein. In diesem Tutorial zeigen wir Ihnen, wie Sie dies mit Aspose.PDF für .NET tun. Falls Sie mit Aspose.PDF oder der PDF-Bearbeitung im Allgemeinen noch nicht vertraut sind, keine Sorge. Ich erkläre jeden Schritt detailliert, damit Sie ihn problemlos nachvollziehen können!

## Voraussetzungen  

Bevor wir uns in die Programmierung stürzen, sollten wir zunächst ein paar Dinge klären. Dies sind die Grundvoraussetzungen für eine reibungslose Entwicklung.

1. Aspose.PDF für .NET: Sie können die neueste Version herunterladen [Hier](https://releases.aspose.com/pdf/net/).
2. .NET-Entwicklungsumgebung: Ob Visual Studio oder eine andere .NET-kompatible IDE, installieren und bereithalten.
3. Aspose-Lizenz: Sie können die kostenlose Testversion von Aspose.PDF verwenden [Hier](https://releases.aspose.com/) oder erwerben Sie eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).
4. Grundkenntnisse in C#: Wir werden mit einigem C#-Code arbeiten, daher wird das Verständnis der Grundlagen die Dinge wesentlich einfacher machen.

## Pakete importieren

Bevor Sie den Code für die Linkstrukturelemente schreiben, müssen Sie einige Pakete importieren. Referenzieren Sie zunächst die erforderlichen Aspose.PDF-Bibliotheken in Ihrem Projekt:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Diese Importe ermöglichen es uns, mit PDF-Dokumenten zu arbeiten, Tags hinzuzufügen und Strukturelemente zu verwalten.

Wir erstellen jetzt ein PDF-Dokument mit verschiedenen Arten von Linkstrukturen und jeder Schritt wird aufgeschlüsselt, damit Sie den Vorgang gründlich verstehen.

## Schritt 1: Initialisieren des Dokuments  

Beginnen wir mit der Erstellung eines neuen PDF-Dokuments und der Einrichtung getaggter Inhalte für die Barrierefreiheit.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "LinkStructureElements_Output.pdf";
string logFile = dataDir + "46035_log.xml";
string imgFile = dataDir + "google-icon-512.png";

// Erstellen Sie ein neues PDF-Dokument
Document document = new Document(); 

// Abrufen der TaggedContent-Schnittstelle
ITaggedContent taggedContent = document.TaggedContent;
```
  
Hier initialisieren wir die `Document` Objekt, das unsere PDF-Datei darstellt. Wir rufen auch die `TaggedContent` Schnittstelle, die es uns ermöglicht, Strukturelemente wie Absätze, Links und Bilder hinzuzufügen.

## Schritt 2: Titel und Sprache festlegen  

Jedes PDF sollte einen Titel und eine Spracheinstellung haben, insbesondere wenn Sie die Einhaltung der PDF/UA-Standards anstreben.

```csharp
// Legen Sie den Dokumenttitel und die Sprache fest
taggedContent.SetTitle("Link Elements Example");
taggedContent.SetLanguage("en-US");
```
  
Dieser Schritt stellt sicher, dass Ihr PDF einen aussagekräftigen Titel hat und stellt die Sprache auf Englisch ein (`en-US`). Dies ist für die Barrierefreiheit von entscheidender Bedeutung und stellt sicher, dass Bildschirmleseprogramme oder andere unterstützende Technologien Ihr Dokument richtig interpretieren können.

## Schritt 3: Absätze erstellen und anhängen  

In diesem Schritt fügen wir Absätze hinzu, die unsere Linkelemente enthalten.

```csharp
// Erstellen Sie das Stammelement
StructureElement rootElement = taggedContent.RootElement;

// Erstellen Sie einen Absatz und fügen Sie ihn dem Stammelement hinzu
ParagraphElement p1 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p1);
```
  
Wir erstellen ein Stammstrukturelement, das im Wesentlichen der Container der obersten Ebene für alle anderen Elemente ist. Anschließend erstellen wir einen Absatz (`p1`) und hängen Sie es an das Stammelement an.

## Schritt 4: Einen einfachen Link hinzufügen  

Fügen wir nun einen einfachen Hyperlink hinzu, der auf Google verweist.

```csharp
// Erstellen Sie ein Link-Element und fügen Sie es dem Absatz hinzu
LinkElement link1 = taggedContent.CreateLinkElement();
p1.AppendChild(link1);

// Hyperlink und Text für den Link festlegen
link1.Hyperlink = new WebHyperlink("http://google.com");
link1.SetText("Google");
link1.AlternateDescriptions = "Link to Google";
```
  
In diesem Schritt haben wir ein Linkelement erstellt, dessen Hyperlink auf „http://google.com“ gesetzt und den Text („Google“) für den Link angegeben. Um die Zugänglichkeit zu gewährleisten, haben wir außerdem eine alternative Beschreibung hinzugefügt.

## Schritt 5: Hinzufügen eines Links mit Spans  

Wir können auch Links mit unterschiedlichen Textabschnitten erstellen.

```csharp
// Einen weiteren Absatz erstellen
ParagraphElement p2 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p2);

// Erstellen eines Links mit einem Span-Element
LinkElement link2 = taggedContent.CreateLinkElement();
p2.AppendChild(link2);
link2.Hyperlink = new WebHyperlink("http://google.com");

SpanElement span2 = taggedContent.CreateSpanElement();
span2.SetText("Google");
link2.AppendChild(span2);

link2.AlternateDescriptions = "Link to Google";
```
  
Hier haben wir ein Span-Element verwendet, um einen Teil des Textes in den Link einzuschließen. Dadurch konnten wir anpassen, wie bestimmte Teile des Links angezeigt werden.

## Schritt 6: Mehrzeiliger Link  

Was ist, wenn Ihr Linktext zu lang ist? Kein Problem, Sie können ihn auf mehrere Zeilen verteilen.

```csharp
ParagraphElement p4 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p4);

LinkElement link4 = taggedContent.CreateLinkElement();
p4.AppendChild(link4);
link4.Hyperlink = new WebHyperlink("http://google.com");
link4.SetText("The multiline link: Google Google Google Google Google...");
link4.AlternateDescriptions = "Link to Google (multiline)";
```
  
In diesem Fall haben wir einen mehrzeiligen Link erstellt, indem wir einfach einen langen Textwert festgelegt haben. Der Text wird dann automatisch über mehrere Zeilen umbrochen.

## Schritt 7: Fügen Sie dem Link ein Bild hinzu  

Schließlich können Sie einem Link auch Bilder hinzufügen.

```csharp
// Erstellen Sie einen neuen Absatz und ein Linkelement
ParagraphElement p5 = taggedContent.CreateParagraphElement();
rootElement.AppendChild(p5);

LinkElement link5 = taggedContent.CreateLinkElement();
p5.AppendChild(link5);
link5.Hyperlink = new WebHyperlink("http://google.com");

// Fügen Sie dem Link ein Bild hinzu
FigureElement figure5 = taggedContent.CreateFigureElement();
figure5.SetImage(imgFile, 1200);
figure5.AlternativeText = "Google icon";
link5.AppendChild(figure5);

link5.AlternateDescriptions = "Link to Google";
```
  
Dieser Schritt zeigt, wie Sie Ihre Links mit einem Bild optimieren können. In diesem Fall haben wir dem Link ein Google-Symbol hinzugefügt. Zusätzlich haben wir die Barrierefreiheit durch die Verwendung eines alternativen Bildtextes sichergestellt.

## Schritt 8: PDF auf Konformität validieren  

Wenn Sie die Konformität mit PDF/UA (einem Zugänglichkeitsstandard) anstreben, empfiehlt es sich, Ihr Dokument zu validieren.

```csharp
// Speichern Sie das PDF-Dokument
document.Save(outFile);

// Validieren Sie das Dokument auf PDF/UA-Konformität
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```
  
Wir haben das Dokument gespeichert und anhand des PDF/UA-Standards validiert, wodurch sichergestellt wird, dass das PDF die Anforderungen an die Barrierefreiheit erfüllt.

## Abschluss  

In diesem Tutorial haben wir die Erstellung strukturierter PDF-Dokumente mit Aspose.PDF für .NET erläutert. Vom Hinzufügen einfacher Hyperlinks bis hin zu komplexeren Strukturen wie Spannen, mehrzeiligen Links und sogar Bildern bietet diese Anleitung eine solide Grundlage für die Bearbeitung von Linkelementen in Ihren PDFs. Dank der PDF/UA-Konformität sind Sie nun in der Lage, barrierefreie und navigierbare PDFs zu erstellen.

## Häufig gestellte Fragen

### Kann ich komplexere Strukturen wie Tabellen in Links einfügen?  
Nein, Links dienen in erster Linie Text und Bildern, Sie können jedoch auch komplexe Elemente in der Nähe einbetten.

### Ist die PDF/UA-Validierung obligatorisch?  
Nicht immer, aber es wird dringend empfohlen, wenn Ihnen die Zugänglichkeit wichtig ist.

### Was passiert, wenn der Bilddateipfad falsch ist?  
Das Bild wird im Dokument nicht angezeigt und beim Rendern kann ein Fehler auftreten.

### Kann ich den Text innerhalb des Links formatieren?  
Ja, Sie können mithilfe der Span-Elemente Textstile anwenden.

### Ist es möglich, interne Dokumentlinks zu erstellen?  
Auf jeden Fall! Sie können auf bestimmte Abschnitte innerhalb desselben Dokuments verlinken.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}