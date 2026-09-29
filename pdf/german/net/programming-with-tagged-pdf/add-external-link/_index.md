---
title: Tagged External Link mit Tooltip zu PDF hinzufügen mit Aspose.Pdf für .NET
weight: 440
limit:
description: Erfahren Sie, wie Sie einen getaggten externen Hyperlink mit Anzeigetext und Tooltip zu einem PDF mit Aspose.Pdf für .NET hinzufügen.
keywords: [Aspose.Pdf for .NET, add external link pdf, tagged pdf hyperlink, pdf tooltip title, pdf logical structure, c# pdf hyperlink]
url: /net/programming-with-tagged-pdf/add-external-link/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Erfahren Sie, wie Sie einen getaggten externen Hyperlink mit Anzeigetext
    und Tooltip zu einem PDF mit Aspose.Pdf für .NET hinzufügen.
  headline: Tagged External Link mit Tooltip zu PDF hinzufügen mit Aspose.Pdf für
    .NET
  type: TechArticle
- description: Erfahren Sie, wie Sie einen getaggten externen Hyperlink mit Anzeigetext
    und Tooltip zu einem PDF mit Aspose.Pdf für .NET hinzufügen.
  name: Tagged External Link mit Tooltip zu PDF hinzufügen mit Aspose.Pdf für .NET
  steps:
  - name: Definieren Sie die Pfade für das Quell‑PDF und die Ergebnisdatei.
    text: Definieren Sie die Pfade für das Quell‑PDF und die Ergebnisdatei.
  - name: Überprüfen Sie, ob das Quell‑PDF existiert, und brechen Sie ab, wenn es
      nicht gefunden werden kann.
    text: Überprüfen Sie, ob das Quell‑PDF existiert, und brechen Sie ab, wenn es
      nicht gefunden werden kann.
  - name: Öffnen Sie das PDF‑Dokument innerhalb eines using‑Blocks, um eine ordnungsgemäße
      Freigabe sicherzustellen.
    text: Öffnen Sie das PDF‑Dokument innerhalb eines using‑Blocks, um eine ordnungsgemäße
      Freigabe sicherzustellen.
  - name: Holen Sie den Tagged‑Content‑Manager für das geöffnete Dokument.
    text: Holen Sie den Tagged‑Content‑Manager für das geöffnete Dokument.
  - name: Setzen Sie die Dokumentensprache auf Englisch (US) und geben Sie dem PDF
      einen Titel, der vom Dateinamen abgeleitet ist.
    text: Setzen Sie die Dokumentensprache auf Englisch (US) und geben Sie dem PDF
      einen Titel, der vom Dateinamen abgeleitet ist.
  - name: Rufen Sie das Wurzelelement des logischen Strukturbaums ab, zu dem neue
      Elemente hinzugefügt werden.
    text: Rufen Sie das Wurzelelement des logischen Strukturbaums ab, zu dem neue
      Elemente hinzugefügt werden.
  - name: Erstellen Sie ein Link‑Element, setzen Sie dessen angezeigten Text, Ziel‑URL
      und Tooltip‑Titel und fügen Sie es dann in die Dokumentstruktur ein.
    text: Erstellen Sie ein Link‑Element, setzen Sie dessen angezeigten Text, Ziel‑URL
      und Tooltip‑Titel und fügen Sie es dann in die Dokumentstruktur ein.
  - name: Speichern Sie das aktualisierte PDF in der angegebenen Ergebnisdatei.
    text: Speichern Sie das aktualisierte PDF in der angegebenen Ergebnisdatei.
  - name: Geben Sie eine Bestätigungsnachricht aus, die angibt, wo das modifizierte
      PDF gespeichert wurde.
    text: Geben Sie eine Bestätigungsnachricht aus, die angibt, wo das modifizierte
      PDF gespeichert wurde.
  type: HowTo
- questions:
  - answer: '`pdfDoc.TaggedContent` gibt den vorhandenen getaggten Inhalt zurück,
      wenn das Dokument bereits getaggt ist; es erstellt keinen doppelten Baum.'
    question: Was passiert, wenn das Quell‑PDF bereits getaggt ist – erzeugt der Aufruf
      von `pdfDoc.TaggedContent` einen neuen Tag‑Baum oder wird der vorhandene wiederverwendet?
  - answer: Ja – finden Sie das gewünschte `StructureElement` (z. B. ein `Div` oder
      `Paragraph` auf einer Seite) über den logischen Strukturbaum und rufen Sie `AppendChild(externalLink)`
      für dieses Element auf.
    question: Kann ich den Hyperlink auf einer bestimmten Seite platzieren, anstatt
      ihn an das Wurzelelement anzuhängen?
  - answer: Der Tooltip wird nur angezeigt, wenn `externalLink.Title` vor `pdfDoc.Save`
      gesetzt wird; ein Setzen nach dem Speichern hat keine Wirkung auf das bereits
      geschriebene PDF.
    question: Ist die `Title`‑Eigenschaft von `LinkElement` erforderlich, damit der
      Tooltip erscheint, und kann sie nach dem Aufruf von `Save` gesetzt werden?
  - answer: Weisen Sie `externalLink.Hyperlink` ein `FileSpecification` zu (z. B.
      `new FileSpecification(\"file:///C:/Docs/manual.pdf\")`), anstatt `WebHyperlink`
      zu verwenden.
    question: Wie erstelle ich einen Link zu einer lokalen Datei anstelle einer Web‑URL?
  type: FAQPage
images:
- /net/programming-with-tagged-pdf/add-external-link/og-image.png
og_title: Einen Tagged External Link mit Tooltip in ein PDF einfügen
og_description: Betten Sie einen barrierefreien Hyperlink mit sichtbarem Text und Tooltip in Ihr PDF ein, indem Sie Aspose.Pdf für .NET verwenden.
og_image_alt: Leitfaden, der zeigt, wie man einen getaggten externen Hyperlink mit Tooltip zu einem PDF mit Aspose.Pdf für .NET hinzufügt
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tagged External Link mit Tooltip zu PDF hinzufügen mit Aspose.Pdf für .NET
Dieses Tutorial zeigt, wie man ein vorhandenes PDF mit Aspose.Pdf für .NET öffnet, einen getaggten externen Hyperlink erstellt, der sichtbaren Anzeigetext und einen Tooltip‑Titel enthält, den Link in die logische Struktur des Dokuments einfügt und die aktualisierte Datei speichert. Wenn Sie die Schritte befolgen, erzeugen Sie ein barrierefreies PDF, bei dem der Link Teil der Tag‑Hierarchie ist und den Lesern zusätzlichen Kontext bietet.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-tagged-pdf/add-external-link" >}}


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

**Q: Was passiert, wenn das Quell‑PDF bereits getaggt ist – erzeugt der Aufruf von `pdfDoc.TaggedContent` einen neuen Tag‑Baum oder wird der vorhandene wiederverwendet?**  
A: `pdfDoc.TaggedContent` gibt den vorhandenen getaggten Inhalt zurück, wenn das Dokument bereits getaggt ist; es erstellt keinen doppelten Baum.

**Q: Kann ich den Hyperlink auf einer bestimmten Seite platzieren, anstatt ihn an das Wurzelelement anzuhängen?**  
A: Ja – finden Sie das gewünschte `StructureElement` (z. B. ein `Div` oder `Paragraph` auf einer Seite) über den logischen Strukturbaum und rufen Sie `AppendChild(externalLink)` für dieses Element auf.

**Q: Ist die `Title`‑Eigenschaft von `LinkElement` erforderlich, damit der Tooltip erscheint, und kann sie nach dem Aufruf von `Save` gesetzt werden?**  
A: Der Tooltip wird nur angezeigt, wenn `externalLink.Title` vor `pdfDoc.Save` gesetzt wird; ein Setzen nach dem Speichern hat keine Wirkung auf das bereits geschriebene PDF.

**Q: Wie erstelle ich einen Link zu einer lokalen Datei anstelle einer Web‑URL?**  
A: Weisen Sie `externalLink.Hyperlink` ein `FileSpecification` zu (z. B. `new FileSpecification(\"file:///C:/Docs/manual.pdf\")`), anstatt `WebHyperlink` zu verwenden.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}