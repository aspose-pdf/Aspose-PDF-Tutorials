---
title: Side‑by‑Side‑PDF‑Vergleich ohne Anmerkungen mit Aspose.Pdf für .NET
weight: 101
limit:
description: Schritt‑für‑Schritt‑Anleitung zum Vergleich von PDFs und zum Ausschließen von Annotationsbereichen mit Aspose.Pdf für .NET.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Schritt‑für‑Schritt‑Anleitung zum Vergleich von PDFs und zum Ausschließen
    von Annotationsbereichen mit Aspose.Pdf für .NET.
  headline: Side‑by‑Side‑PDF‑Vergleich ohne Anmerkungen mit Aspose.Pdf für .NET
  type: TechArticle
- description: Schritt‑für‑Schritt‑Anleitung zum Vergleich von PDFs und zum Ausschließen
    von Annotationsbereichen mit Aspose.Pdf für .NET.
  name: Side‑by‑Side‑PDF‑Vergleich ohne Anmerkungen mit Aspose.Pdf für .NET
  steps:
  - name: Definieren Sie die Dateipfade für das primäre PDF, das sekundäre PDF und
      das Ausgabediff‑PDF.
    text: Definieren Sie die Dateipfade für das primäre PDF, das sekundäre PDF und
      das Ausgabediff‑PDF.
  - name: Überprüfen Sie, ob beide Eingabe‑PDF‑Dateien existieren, und brechen Sie
      mit einer Fehlermeldung ab, falls eine fehlt.
    text: Überprüfen Sie, ob beide Eingabe‑PDF‑Dateien existieren, und brechen Sie
      mit einer Fehlermeldung ab, falls eine fehlt.
  - name: Öffnen Sie die beiden PDF‑Dateien als Document‑Objekte (pdfA und pdfB) innerhalb
      eines using‑Blocks, damit sie automatisch freigegeben werden.
    text: Öffnen Sie die beiden PDF‑Dateien als Document‑Objekte (pdfA und pdfB) innerhalb
      eines using‑Blocks, damit sie automatisch freigegeben werden.
  - name: Sammeln Sie die Begrenzungsrechtecke jeder Annotation in pdfA und speichern
      Sie sie in ignoredRectsA.
    text: Sammeln Sie die Begrenzungsrechtecke jeder Annotation in pdfA und speichern
      Sie sie in ignoredRectsA.
  - name: Sammeln Sie die Begrenzungsrechtecke jeder Annotation in pdfB und speichern
      Sie sie in ignoredRectsB.
    text: Sammeln Sie die Begrenzungsrechtecke jeder Annotation in pdfB und speichern
      Sie sie in ignoredRectsB.
  - name: Erstellen Sie ein SideBySideComparisonOptions‑Objekt und weisen Sie die
      zuvor gesammelten Annotationsrechtecke ExcludeAreas1 bzw. ExcludeAreas2 zu,
      damit diese Bereiche beim Vergleich ignoriert werden.
    text: Erstellen Sie ein SideBySideComparisonOptions‑Objekt und weisen Sie die
      zuvor gesammelten Annotationsrechtecke ExcludeAreas1 bzw. ExcludeAreas2 zu,
      damit diese Bereiche beim Vergleich ignoriert werden.
  - name: Führen Sie den Side‑by‑Side‑PDF‑Vergleich mit den beiden Document‑Objekten
      und den konfigurierten Optionen aus und schreiben Sie das Ergebnis in outputPdf.
    text: Führen Sie den Side‑by‑Side‑PDF‑Vergleich mit den beiden Document‑Objekten
      und den konfigurierten Optionen aus und schreiben Sie das Ergebnis in outputPdf.
  - name: Geben Sie die Document‑Objekte frei und verlassen Sie den using‑Block.
    text: Geben Sie die Document‑Objekte frei und verlassen Sie den using‑Block.
  - name: Geben Sie eine Bestätigungsnachricht aus, die anzeigt, dass der Vergleich
      abgeschlossen ist und wo das Diff‑PDF gespeichert wurde.
    text: Geben Sie eine Bestätigungsnachricht aus, die anzeigt, dass der Vergleich
      abgeschlossen ist und wo das Diff‑PDF gespeichert wurde.
  type: HowTo
- questions:
  - answer: Ja. Der Code fügt einfach keine Rechtecke zur entsprechenden `ignoredRects`‑Liste
      hinzu, sodass `ExcludeAreas1`/`ExcludeAreas2` ein leeres Array erhalten und
      der Vergleich die gesamte Seite verarbeitet.
    question: Was passiert, wenn eine PDF‑Seite keine Anmerkungen hat – funktioniert
      der Vergleich trotzdem?
  - answer: Setzen Sie `ExcludeAreas1` (oder `ExcludeAreas2`) auf die gesammelten
      Rechtecke und lassen Sie die andere Eigenschaft als leeres Array; der Vergleich
      ignoriert dann nur die Bereiche im angegebenen Dokument.
    question: Kann ich nur die Anmerkungen eines Dokuments ausschließen und die Anmerkungen
      des anderen Dokuments im Diff beibehalten?
  - answer: Überlappende Rechtecke werden vom Vergleich intern zusammengeführt, sodass
      überlappende Annotationsgrenzen sicher ausgeschlossen werden, ohne doppelt gezählt
      zu werden.
    question: Verursachen überlappende Annotationsrechtecke Probleme mit `ExcludeAreas`?
  - answer: Ja, setzen Sie `compareOpts.ExcludeTables = true;` – dieses Flag funktioniert
      zusammen mit `ExcludeAreas1`/`ExcludeAreas2`, um Tabellenbereiche ebenfalls
      zu ignorieren.
    question: Gibt es eine Möglichkeit, zusätzlich zu Anmerkungen Tabellen mit demselben
      Optionsobjekt auszuschließen?
  - answer: Der Code prüft `if (a != null && a.Rect != null)` bevor er das Element
      zur Liste hinzufügt, sodass null‑Rechtecke einfach übersprungen werden und keine
      Ausnahme ausgelöst wird.
    question: Was passiert, wenn die `Rect`‑Eigenschaft einer Anmerkung null ist –
      wirft der Code eine Ausnahme?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: PDFs ohne Anmerkungen vergleichen
og_description: Führen Sie ein Side‑by‑Side‑PDF‑Diff aus, das alle Annotationsmarkierungen überspringt.
og_image_alt: Leitfaden, der einen Side‑by‑Side‑PDF‑Vergleich zeigt, der Annotationsbereiche mit Aspose.Pdf für .NET ausschließt
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Side‑by‑Side‑PDF‑Vergleich ohne Anmerkungen mit Aspose.Pdf für .NET
Dieses Tutorial zeigt, wie man zwei PDF‑Dateien mit Aspose.Pdf für .NET vergleicht, wobei jeglicher Annotationsinhalt ignoriert wird. Es extrahiert die Begrenzungsrahmen aller Anmerkungen aus jedem Dokument, übergibt diese Regionen an SideBySideComparisonOptions und führt anschließend einen Side‑by‑Side‑Vergleich durch. Das Ergebnis ist ein Diff‑PDF, das nur die Änderungen ohne Anmerkungen hervorhebt.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


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

**Q: Was passiert, wenn eine PDF‑Seite keine Anmerkungen hat – funktioniert der Vergleich trotzdem?**  
A: Ja. Der Code fügt einfach keine Rechtecke zur entsprechenden `ignoredRects`‑Liste hinzu, sodass `ExcludeAreas1`/`ExcludeAreas2` ein leeres Array erhalten und der Vergleich die gesamte Seite verarbeitet.

**Q: Kann ich nur die Anmerkungen eines Dokuments ausschließen und die Anmerkungen des anderen Dokuments im Diff beibehalten?**  
A: Setzen Sie `ExcludeAreas1` (oder `ExcludeAreas2`) auf die gesammelten Rechtecke und lassen Sie die andere Eigenschaft als leeres Array; der Vergleich ignoriert dann nur die Bereiche im angegebenen Dokument.

**Q: Verursachen überlappende Annotationsrechtecke Probleme mit `ExcludeAreas`?**  
A: Überlappende Rechtecke werden vom Vergleich intern zusammengeführt, sodass überlappende Annotationsgrenzen sicher ausgeschlossen werden, ohne doppelt gezählt zu werden.

**Q: Gibt es eine Möglichkeit, zusätzlich zu Anmerkungen Tabellen mit demselben Optionsobjekt auszuschließen?**  
A: Ja, setzen Sie `compareOpts.ExcludeTables = true;` – dieses Flag funktioniert zusammen mit `ExcludeAreas1`/`ExcludeAreas2`, um Tabellenbereiche ebenfalls zu ignorieren.

**Q: Was passiert, wenn die `Rect`‑Eigenschaft einer Anmerkung null ist – wirft der Code eine Ausnahme?**  
A: Der Code prüft `if (a != null && a.Rect != null)` bevor er das Element zur Liste hinzufügt, sodass null‑Rechtecke einfach übersprungen werden und keine Ausnahme ausgelöst wird.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}