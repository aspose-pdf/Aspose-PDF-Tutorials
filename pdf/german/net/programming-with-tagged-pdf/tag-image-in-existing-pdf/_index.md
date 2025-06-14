---
"description": "Erfahren Sie, wie Sie mit Aspose.PDF für .NET Bilder in vorhandenen PDFs taggen. Schritt-für-Schritt-Anleitung zur Verbesserung der Barrierefreiheit mit PDF/UA-Konformität."
"linktitle": "Bild in vorhandenem PDF taggen"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Bild in vorhandenem PDF taggen"
"url": "/de/net/programming-with-tagged-pdf/tag-image-in-existing-pdf/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Bild in vorhandenem PDF taggen

## Einführung

In diesem Tutorial zeigen wir Ihnen, wie Sie mit Aspose.PDF für .NET ein Bild in einer vorhandenen PDF-Datei taggen. Am Ende dieser Anleitung können Sie alternativen Text für Bilder festlegen, Layoutattribute anpassen und sicherstellen, dass Ihre PDF-Datei den Barrierefreiheitsstandards entspricht.

## Voraussetzungen

Bevor wir loslegen, gehen wir durch, was Sie für den Anfang brauchen:

- Aspose.PDF für .NET: Stellen Sie sicher, dass Sie die neueste Version von Aspose.PDF für .NET heruntergeladen und installiert haben. [Hier herunterladen](https://releases.aspose.com/pdf/net/).
- .NET Framework: Stellen Sie sicher, dass Sie eine .NET-Entwicklungsumgebung wie Visual Studio eingerichtet haben.
- Grundlegendes Verständnis der PDF-Struktur: Vertrautheit mit PDF-Strukturelementen wie Absätzen, Bereichen, Tabellen und Bildern.
- Eine gültige Lizenz: Sie können entweder eine Lizenz kaufen [Hier](https://purchase.aspose.com/buy) oder verwenden Sie eine temporäre [Hier](https://purchase.aspose.com/temporary-license/).

## Pakete importieren

Um mit dem Programmieren zu beginnen, müssen Sie die erforderlichen Namespaces aus Aspose.PDF für .NET importieren. Diese ermöglichen Ihnen den Zugriff auf die notwendigen Klassen und Methoden zur Bearbeitung des PDF-Dokuments.

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Nachdem wir nun die Bühne bereitet haben, wollen wir den Vorgang des Taggens eines Bildes in mehrere Schritte unterteilen.

## Schritt 1: Laden Sie das vorhandene PDF-Dokument

Laden Sie zunächst die PDF-Datei hoch, mit der Sie arbeiten möchten. Dies kann eine beliebige PDF-Datei mit einem Bild sein, das Sie taggen möchten.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "TH.pdf";
string outFile = dataDir + "TH_out.pdf";
string logFile = dataDir + "TH_out.xml";

// Öffnen Sie das Dokument
Document document = new Document(inFile);
```

- Ersetzen `"YOUR DOCUMENT DIRECTORY"` durch den tatsächlichen Pfad zu Ihrer Datei.
- Der `Document` Mit der Klasse können Sie eine vorhandene PDF-Datei laden. Sie ändern diese PDF-Datei, um das Bild zu taggen.

## Schritt 2: Zugriff auf getaggten Inhalt und Stammstrukturelement

Nachdem Sie die PDF-Datei geöffnet haben, müssen Sie im nächsten Schritt auf den getaggten Inhalt zugreifen und das Stammstrukturelement identifizieren. Dies ist wichtig, da Sie so durch die Elemente in der PDF-Datei navigieren und Änderungen vornehmen können.

```csharp
// Getaggten Inhalt und Stammstrukturelement abrufen
ITaggedContent taggedContent = document.TaggedContent;
StructureElement rootElement = taggedContent.RootElement;
```

- `TaggedContent` bietet Zugriff auf die strukturierten Elemente im PDF.
- Der `RootElement` ist das oberste Strukturelement, von dem aus Sie zu anderen Elementen wie Absätzen, Tabellen und Bildern gelangen können.

## Schritt 3: Legen Sie den Titel für das getaggte PDF-Dokument fest

Durch das Hinzufügen eines Titels zum getaggten PDF-Dokument wird sichergestellt, dass Ihr Dokument ordnungsgemäß beschriftet ist, was für die Zugänglichkeit und die PDF/UA-Konformität hilfreich ist.

```csharp
// Titel für das getaggte PDF-Dokument festlegen
taggedContent.SetTitle("Document with images");
```

- Durch das Festlegen eines Titels für Ihr mit Tags versehenes PDF wird die Zugänglichkeit verbessert und die Dokumentübersichtlichkeit für Bildschirmleseprogramme und unterstützende Technologien verbessert.

## Schritt 4: Suchen und markieren Sie das Bild

Suchen wir nun das Bildelement (genannt a `FigureElement` in Aspose.PDF), legen Sie einen alternativen Text dafür fest und konfigurieren Sie seine Layoutattribute.

```csharp
// Durchlaufen Sie alle Abbildungselemente (Bilder) und legen Sie alternative Text- und Layoutattribute fest
foreach (FigureElement figureElement in rootElement.FindElements<FigureElement>(true))
{
    // Alternativtext für die Abbildung festlegen
    figureElement.AlternativeText = "Figure alternative text (technique 2)";
    
    // BBox-Attribut (Begrenzungsrahmen) erstellen und festlegen
    StructureAttribute bboxAttribute = new StructureAttribute(AttributeKey.BBox);
    bboxAttribute.SetRectangleValue(new Aspose.Pdf.Rectangle(0.0, 0.0, 100.0, 100.0));
    
    // Legen Sie die Layoutattribute für die Abbildung fest
    StructureAttributes figureLayoutAttributes = figureElement.Attributes.GetAttributes(AttributeOwnerStandard.Layout);
    figureLayoutAttributes.SetAttribute(bboxAttribute);
}
```

- Dieser Code durchläuft alle `FigureElement` Objekte in der Wurzelstruktur, die Bilder darstellen.
- Es legt den alternativen Text für die Barrierefreiheit fest (Bildschirmleseprogramme verwenden diesen zur Beschreibung des Bildes).
- Der Begrenzungsrahmen (`BBox`) gibt die Koordinaten für das Layout des Bildes an und stellt sicher, dass es im Dokument richtig angezeigt wird.

## Schritt 5: Span-Elemente innerhalb der Tabelle ändern

In manchen Fällen müssen Sie Span-Elemente innerhalb einer Tabelle ändern. Hier zeigen wir Ihnen, wie Sie ein `SpanElement` und verschieben Sie es in einen Absatz.

```csharp
// Suchen Sie nach den Tabellen-, Spann- und Absatzelementen
TableElement tableElement = rootElement.FindElements<TableElement>(true)[0];
SpanElement spanElement = tableElement.FindElements<SpanElement>(true)[0];
TableTDElement firstTdElement = tableElement.FindElements<TableTDElement>(true)[0];
ParagraphElement paragraph = firstTdElement.FindElements<ParagraphElement>(true)[0];

// Verschieben Sie das Span-Element in den Absatz
spanElement.ChangeParentElement(paragraph);
```

- Hier finden wir die `TableElement`, `SpanElement`, Und `ParagraphElement` innerhalb der PDF-Datei.
- Verwenden des `ChangeParentElement` Methode verschieben wir den Bereich in den Absatz, um eine ordnungsgemäße Kennzeichnung und Struktur sicherzustellen.

## Schritt 6: Speichern Sie das Dokument und validieren Sie die PDF/UA-Konformität

Sobald alle Änderungen vorgenommen wurden, besteht der letzte Schritt darin, das aktualisierte PDF zu speichern und zu prüfen, ob es den PDF/UA-Standards entspricht.

```csharp
// Speichern Sie das aktualisierte PDF-Dokument
document.Save(outFile);

// Validieren Sie die PDF/UA-Konformität
document = new Document(outFile);
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

- Der `Validate` Die Methode prüft das PDF-Dokument anhand der PDF/UA-Standards und protokolliert die Ergebnisse.
- Durch die Gewährleistung der Konformität können Sie die Zugänglichkeit verbessern und gesetzliche Anforderungen für die Veröffentlichung von Dokumenten erfüllen.

## Abschluss

In diesem Tutorial haben wir Ihnen gezeigt, wie Sie Bilder in einem vorhandenen PDF mit Aspose.PDF für .NET taggen. Durch das Festlegen von Alternativtext, das Anpassen von Layoutattributen und die Validierung des Dokuments auf PDF/UA-Konformität stellen Sie sicher, dass Ihre PDFs barrierefrei sind und modernen Standards entsprechen. Aspose.PDF erleichtert die Arbeit mit strukturierten Elementen und gibt Ihnen die Kontrolle über das Layout und die Barrierefreiheit Ihres Dokuments.

## Häufig gestellte Fragen

### Wofür wird Aspose.PDF für .NET verwendet?
Aspose.PDF für .NET ist eine leistungsstarke Bibliothek zum programmgesteuerten Erstellen, Bearbeiten und Bearbeiten von PDF-Dokumenten in einer .NET-Umgebung.

### Wie stelle ich die PDF/UA-Konformität sicher?
Sie können Aspose.PDF's verwenden `Validate` Methode zum Überprüfen der PDF/UA-Konformität nach Änderungen am Dokument.

### Was ist Alternativtext in PDFs?
Alternativtext ist eine Beschreibung, die Bildern in PDF-Dateien hinzugefügt wird, um die Zugänglichkeit zu verbessern, insbesondere für Benutzer, die auf Bildschirmleseprogramme angewiesen sind.

### Kann ich mit Aspose.PDF Tabellen und Bereiche in einer PDF-Datei bearbeiten?
Ja, mit Aspose.PDF können Sie Tabellen, Bereiche und andere strukturierte Elemente in einem PDF-Dokument bearbeiten.

### Wo kann ich Aspose.PDF für .NET herunterladen?
Sie können die neueste Version von Aspose.PDF für .NET herunterladen [Hier](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}