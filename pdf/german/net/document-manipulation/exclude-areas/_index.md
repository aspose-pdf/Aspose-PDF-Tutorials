---
title: PDFs vergleichen, während bestimmte Bereiche ignoriert werden, mit Aspose.Pdf für .NET
weight: 201
limit:
description: Lernen Sie, PDFs nebeneinander zu vergleichen und ausgewählte Regionen mit Aspose.Pdf für .NET zu ignorieren.
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Lernen Sie, PDFs nebeneinander zu vergleichen und ausgewählte Regionen
    mit Aspose.Pdf für .NET zu ignorieren.
  headline: PDFs vergleichen, während bestimmte Bereiche ignoriert werden, mit Aspose.Pdf
    für .NET
  type: TechArticle
- description: Lernen Sie, PDFs nebeneinander zu vergleichen und ausgewählte Regionen
    mit Aspose.Pdf für .NET zu ignorieren.
  name: PDFs vergleichen, während bestimmte Bereiche ignoriert werden, mit Aspose.Pdf
    für .NET
  steps:
  - name: Definieren Sie die Dateipfade für die beiden Quell‑PDFs und das Ausgabe‑Diff‑PDF.
    text: Definieren Sie die Dateipfade für die beiden Quell‑PDFs und das Ausgabe‑Diff‑PDF.
  - name: Überprüfen Sie, ob beide Quell‑PDF‑Dateien existieren, und brechen Sie mit
      einer Fehlermeldung ab, wenn eine fehlt.
    text: Überprüfen Sie, ob beide Quell‑PDF‑Dateien existieren, und brechen Sie mit
      einer Fehlermeldung ab, wenn eine fehlt.
  - name: Erstellen Sie ein Array, das den rechteckigen Bereich enthält, der im ersten
      PDF ignoriert werden soll.
    text: Erstellen Sie ein Array, das den rechteckigen Bereich enthält, der im ersten
      PDF ignoriert werden soll.
  - name: Erstellen Sie ein Array, das den rechteckigen Bereich enthält, der im zweiten
      PDF ignoriert werden soll.
    text: Erstellen Sie ein Array, das den rechteckigen Bereich enthält, der im zweiten
      PDF ignoriert werden soll.
  - name: Konfigurieren Sie den Nebeneinander‑Vergleich und weisen Sie die Ignorier‑Bereich‑Arrays
      den entsprechenden Eigenschaften zu.
    text: Konfigurieren Sie den Nebeneinander‑Vergleich und weisen Sie die Ignorier‑Bereich‑Arrays
      den entsprechenden Eigenschaften zu.
  - name: Laden Sie beide PDFs und führen Sie den Nebeneinander‑Vergleich aus, wobei
      die Diff‑Datei am angegebenen Pfad erstellt wird.
    text: Laden Sie beide PDFs und führen Sie den Nebeneinander‑Vergleich aus, wobei
      die Diff‑Datei am angegebenen Pfad erstellt wird.
  - name: Geben Sie eine Bestätigungsnachricht aus, die angibt, dass der Vergleich
      abgeschlossen ist und wo das Diff‑PDF gespeichert wurde.
    text: Geben Sie eine Bestätigungsnachricht aus, die angibt, dass der Vergleich
      abgeschlossen ist und wo das Diff‑PDF gespeichert wurde.
  type: HowTo
- questions:
  - answer: Die Koordinaten sind in Punkten (1/72 Zoll) angegeben, wobei der Ursprung
      in der linken unteren Ecke der Seite liegt; die ersten beiden Zahlen sind das
      linke untere X/Y und die letzten beiden das rechte obere X/Y.
    question: Welches Koordinatensystem verwenden die `Rectangle`‑Werte beim Definieren
      von Ignorierzonen?
  - answer: Ja – übergeben Sie mehrere `Aspose.Pdf.Rectangle`‑Objekte im `ExcludeAreas1`‑
      (oder `ExcludeAreas2`‑)Array; jedes Rechteck wird beim Vergleich unabhängig
      ausgeschlossen.
    question: Kann ich mehr als einen rechteckigen Bereich im selben Dokument ignorieren?
  - answer: Nein. `ExcludeAreas1` gilt für das erste PDF und `ExcludeAreas2` für das
      zweite, sodass Sie für jedes Dokument unterschiedliche Koordinaten angeben können.
    question: Müssen die Ignorier‑Rechtecke in beiden PDFs identisch sein?
  - answer: Aspose.Pdf ignoriert Rechtecke, die vollständig außerhalb der Seite liegen,
      stillschweigend; sie haben keinen Einfluss auf das Vergleichsergebnis.
    question: Was passiert, wenn ein Rechteck außerhalb der Seitenränder definiert
      wird?
  - answer: Die `ExcludeAreas`‑Arrays gelten pro Seite, daher müssen Sie das gleiche
      `Rectangle` zu jeder Seitensammlung hinzufügen (z. B. über eine Schleife durch
      `pdf.Pages` und das Zuweisen des Arrays), bevor Sie `SideBySidePdfComparer.Compare`
      aufrufen.
    question: Wie kann ich denselben Bereich auf jeder Seite eines PDFs ausschließen?
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: Regionen beim Vergleich von PDFs ignorieren
og_description: Sehen Sie, wie Sie ausgewählte Bereiche in einem Nebeneinander‑PDF‑Vergleich überspringen und ein sauberes Diff‑PDF erhalten.
og_image_alt: Leitfaden zum Nebeneinander‑PDF‑Vergleich mit ausgeschlossenen rechteckigen Regionen unter Verwendung von Aspose.Pdf für .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDFs vergleichen, während bestimmte Bereiche ignoriert werden, mit Aspose.Pdf für .NET
Dieses Tutorial demonstriert, wie man zwei PDF‑Dokumente nebeneinander mit Aspose.Pdf für .NET vergleicht, wobei festgelegte rechteckige Regionen von der Analyse ausgeschlossen werden. Durch das Definieren von Ausschlussbereichen in jeder Datei hebt das erzeugte Diff‑PDF nur die wesentlichen Änderungen hervor, was das Fokussieren auf relevante Unterschiede erleichtert.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


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

**Q: Welches Koordinatensystem verwenden die `Rectangle`‑Werte beim Definieren von Ignorierzonen?**  
A: Die Koordinaten sind in Punkten (1/72 Zoll) angegeben, wobei der Ursprung in der linken unteren Ecke der Seite liegt; die ersten beiden Zahlen sind das linke untere X/Y und die letzten beiden das rechte obere X/Y.

**Q: Kann ich mehr als einen rechteckigen Bereich im selben Dokument ignorieren?**  
A: Ja – übergeben Sie mehrere `Aspose.Pdf.Rectangle`‑Objekte im `ExcludeAreas1`‑ (oder `ExcludeAreas2`‑)Array; jedes Rechteck wird beim Vergleich unabhängig ausgeschlossen.

**Q: Müssen die Ignorier‑Rechtecke in beiden PDFs identisch sein?**  
A: Nein. `ExcludeAreas1` gilt für das erste PDF und `ExcludeAreas2` für das zweite, sodass Sie für jedes Dokument unterschiedliche Koordinaten angeben können.

**Q: Was passiert, wenn ein Rechteck außerhalb der Seitenränder definiert wird?**  
A: Aspose.Pdf ignoriert Rechtecke, die vollständig außerhalb der Seite liegen, stillschweigend; sie haben keinen Einfluss auf das Vergleichsergebnis.

**Q: Wie kann ich denselben Bereich auf jeder Seite eines PDFs ausschließen?**  
A: Die `ExcludeAreas`‑Arrays gelten pro Seite, daher müssen Sie das gleiche `Rectangle` zu jeder Seitensammlung hinzufügen (z. B. über eine Schleife durch `pdf.Pages` und das Zuweisen des Arrays), bevor Sie `SideBySidePdfComparer.Compare` aufrufen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}