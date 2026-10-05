---
title: Überschrift, Sprache und Titel zu einem PDF hinzufügen mit Aspose.PDF for .NET
weight: 110
limit:
description: Erstellen Sie ein PDF, setzen Sie dessen Sprache und Titel und fügen Sie mit Aspose.PDF for .NET eine Überschrift der Ebene 1 hinzu.
keywords: [Aspose.PDF for .NET, add heading pdf .net, set pdf language, pdf document title, ITaggedContent example, StructureElement pdf]
url: /net/programming-with-headings/add-heading/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Erstellen Sie ein PDF, setzen Sie dessen Sprache und Titel und fügen
    Sie mit Aspose.PDF for .NET eine Überschrift der Ebene 1 hinzu.
  headline: Überschrift, Sprache und Titel zu einem PDF hinzufügen mit Aspose.PDF
    for .NET
  type: TechArticle
- description: Erstellen Sie ein PDF, setzen Sie dessen Sprache und Titel und fügen
    Sie mit Aspose.PDF for .NET eine Überschrift der Ebene 1 hinzu.
  name: Überschrift, Sprache und Titel zu einem PDF hinzufügen mit Aspose.PDF for
    .NET
  steps:
  - name: Definieren Sie den Ausgabedateinamen für das erzeugte PDF.
    text: Definieren Sie den Ausgabedateinamen für das erzeugte PDF.
  - name: Erstellen Sie eine neue leere PDF‑Dokumentinstanz (`pdfDoc`) innerhalb eines
      `using`‑Blocks.
    text: Erstellen Sie eine neue leere PDF‑Dokumentinstanz (`pdfDoc`) innerhalb eines
      `using`‑Blocks.
  - name: Holen Sie sich die `ITaggedContent`‑Schnittstelle, um mit getaggten PDF‑Strukturen
      zu arbeiten.
    text: Holen Sie sich die `ITaggedContent`‑Schnittstelle, um mit getaggten PDF‑Strukturen
      zu arbeiten.
  - name: Setzen Sie die Standardsprache des Dokuments auf Englisch (US) und weisen
      Sie ein Titel‑Metadatum zu.
    text: Setzen Sie die Standardsprache des Dokuments auf Englisch (US) und weisen
      Sie ein Titel‑Metadatum zu.
  - name: Rufen Sie das Wurzelelement des logischen Strukturbaums ab.
    text: Rufen Sie das Wurzelelement des logischen Strukturbaums ab.
  - name: Erstellen Sie ein Header‑Element der Ebene 1, setzen Sie dessen angezeigten
      Text und geben Sie dessen Sprache an.
    text: Erstellen Sie ein Header‑Element der Ebene 1, setzen Sie dessen angezeigten
      Text und geben Sie dessen Sprache an.
  - name: Fügen Sie das Header‑Element dem Wurzelelement hinzu, sodass die Überschrift
      im PDF erscheint.
    text: Fügen Sie das Header‑Element dem Wurzelelement hinzu, sodass die Überschrift
      im PDF erscheint.
  - name: Speichern Sie das PDF in der angegebenen Datei und schließen Sie den Dokument‑Geltungsbereich.
    text: Speichern Sie das PDF in der angegebenen Datei und schließen Sie den Dokument‑Geltungsbereich.
  - name: Geben Sie eine Bestätigungsnachricht in der Konsole aus.
    text: Geben Sie eine Bestätigungsnachricht in der Konsole aus.
  type: HowTo
- questions:
  - answer: '`SetLanguage` definiert die Standardsprache für die gesamte logische
      Struktur des Dokuments; jedes Element, dem keine eigene Sprache zugewiesen ist,
      erbt "en-US".'
    question: Welche Auswirkung hat der Aufruf von `tagContent.SetLanguage("en-US")`
      auf das PDF?
  - answer: Das Setzen von `header.Language` ist optional; die Überschrift erbt die
      Standardsprache des Dokuments, sofern Sie keinen anderen Wert zuweisen, wie
      im Beispiel gezeigt.
    question: Muss ich `header.Language` setzen, wenn ich bereits `SetLanguage` für
      das Dokument aufgerufen habe?
  - answer: Verwenden Sie `tagContent.CreateHeaderElement(2)`, um eine Überschrift
      der Ebene 2 zu erstellen; das numerische Argument gibt die Überschriftenebene
      an, die im Strukturbaum des PDFs wiedergegeben wird.
    question: Wie kann ich eine Überschrift der Ebene 2 anstelle einer Ebene 1 erstellen?
  - answer: '`SetTitle` schreibt die übergebene Zeichenkette in das Titel‑Metadatenfeld
      des PDF‑Dokuments, das in PDF‑Readern angezeigt und für Suche oder Indexierung
      verwendet werden kann.'
    question: Was bewirkt `tagContent.SetTitle("PDF Example with Header")`?
  - answer: Das Überschrift‑Element wird nicht zum logischen Strukturbaum hinzugefügt,
      sodass es nicht im PDF‑Ausgabe erscheint und von Hilfsmitteln zur Barrierefreiheit
      nicht als Überschrift erkannt wird.
    question: Was passiert, wenn ich `rootElement.AppendChild(header)` weglasse?
  type: FAQPage
images:
- /net/programming-with-headings/add-heading/og-image.png
og_title: Überschrift einfügen und Sprache in einem PDF festlegen
og_description: Lernen Sie, ein PDF zu erstellen, dessen Sprache und Titel festzulegen und anschließend mit wenigen Zeilen .NET‑Code eine Überschrift der Ebene 1 hinzuzufügen.
og_image_alt: Leitfaden, der zeigt, wie man mit Aspose.PDF for .NET einer PDF‑Datei eine Überschrift, Sprache und Titel hinzufügt
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Überschrift, Sprache und Titel zu einem PDF hinzufügen mit Aspose.PDF
Dieses Tutorial führt Sie Schritt für Schritt durch das Erstellen eines neuen PDF‑Dokuments mit Aspose.PDF for .NET, das Zuweisen einer Standardsprache und eines Dokumenttitels sowie das Einfügen einer Überschrift der Ebene 1. Sie sehen, wie Sie mit den Klassen Document, ITaggedContent, StructureElement und HeaderElement arbeiten, um ein korrekt getaggtes PDF zu erzeugen, das für Hilfsmittel zur Barrierefreiheit geeignet ist.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-headings/add-heading" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Welche Auswirkung hat der Aufruf von `tagContent.SetLanguage("en-US")` auf das PDF?**  
A: `SetLanguage` definiert die Standardsprache für die gesamte logische Struktur des Dokuments; jedes Element, dem keine eigene Sprache zugewiesen ist, erbt "en-US".

**Q: Muss ich `header.Language` setzen, wenn ich bereits `SetLanguage` für das Dokument aufgerufen habe?**  
A: Das Setzen von `header.Language` ist optional; die Überschrift erbt die Standardsprache des Dokuments, sofern Sie keinen anderen Wert zuweisen, wie im Beispiel gezeigt.

**Q: Wie kann ich eine Überschrift der Ebene 2 anstelle einer Ebene 1 erstellen?**  
A: Verwenden Sie `tagContent.CreateHeaderElement(2)`, um eine Überschrift der Ebene 2 zu erstellen; das numerische Argument gibt die Überschriftenebene an, die im Strukturbaum des PDFs wiedergegeben wird.

**Q: Was bewirkt `tagContent.SetTitle("PDF Example with Header")`?**  
A: `SetTitle` schreibt die übergebene Zeichenkette in das Titel‑Metadatenfeld des PDF‑Dokuments, das in PDF‑Readern angezeigt und für Suche oder Indexierung verwendet werden kann.

**Q: Was passiert, wenn ich `rootElement.AppendChild(header)` weglasse?**  
A: Das Überschrift‑Element wird nicht zum logischen Strukturbaum hinzugefügt, sodass es nicht im PDF‑Ausgabe erscheint und von Hilfsmitteln zur Barrierefreiheit nicht als Überschrift erkannt wird.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}