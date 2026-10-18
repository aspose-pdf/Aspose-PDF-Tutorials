---
title: Passe den Hintergrund, die Ränder und das Padding von Tabellenzellen in PDFs mit Aspose.Pdf für .NET an
weight: 101
limit:
description: Erfahren Sie, wie Sie ein PDF mit einer zweispaltigen Tabelle erstellen und benutzerdefinierte Hintergrundfarben, Ränder und Padding auf jede Zelle anwenden, wobei Sie Aspose.Pdf für .NET verwenden.
keywords: [Aspose.Pdf for .NET, style table cells pdf, pdf table cell background, pdf table cell border, pdf cell padding, Aspose PDF table styling]
url: /net/tables-lists/style-table-cells/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Erfahren Sie, wie Sie ein PDF mit einer zweispaltigen Tabelle erstellen
    und benutzerdefinierte Hintergrundfarben, Ränder und Padding auf jede Zelle anwenden,
    wobei Sie Aspose.Pdf für .NET verwenden.
  headline: Passe den Hintergrund, die Ränder und das Padding von Tabellenzellen in
    PDFs mit Aspose.Pdf für .NET an
  type: TechArticle
- description: Erfahren Sie, wie Sie ein PDF mit einer zweispaltigen Tabelle erstellen
    und benutzerdefinierte Hintergrundfarben, Ränder und Padding auf jede Zelle anwenden,
    wobei Sie Aspose.Pdf für .NET verwenden.
  name: Passe den Hintergrund, die Ränder und das Padding von Tabellenzellen in PDFs
    mit Aspose.Pdf für .NET an
  steps:
  - name: Erstelle ein neues leeres PDF‑Dokument innerhalb eines using‑Blocks.
    text: Erstelle ein neues leeres PDF‑Dokument innerhalb eines using‑Blocks.
  - name: Füge dem PDF‑Dokument eine leere Seite hinzu.
    text: Füge dem PDF‑Dokument eine leere Seite hinzu.
  - name: Instanziiere ein Table‑Objekt mit zwei 200‑Punkt‑Spalten, einem dünnen schwarzen
      äußeren Rand und einem Standard‑Cell‑Padding von 5 Punkten.
    text: Instanziiere ein Table‑Objekt mit zwei 200‑Punkt‑Spalten, einem dünnen schwarzen
      äußeren Rand und einem Standard‑Cell‑Padding von 5 Punkten.
  - name: Füge der Tabelle die erste Zeile hinzu.
    text: Füge der Tabelle die erste Zeile hinzu.
  - name: Erstelle die erste Zelle, füge den Text "First cell" ein, setze einen hellgelben
      Hintergrund, einen roten 2‑Punkt‑Rand und einen 4‑Punkt‑Margin.
    text: Erstelle die erste Zelle, füge den Text "First cell" ein, setze einen hellgelben
      Hintergrund, einen roten 2‑Punkt‑Rand und einen 4‑Punkt‑Margin.
  - name: Erstelle die zweite Zelle, füge den Text "Second cell" hinzu, gib ihr einen
      hellgrünen Hintergrund, einen blauen 2‑Punkt‑Rand und einen 4‑Punkt‑Margin.
    text: Erstelle die zweite Zelle, füge den Text "Second cell" hinzu, gib ihr einen
      hellgrünen Hintergrund, einen blauen 2‑Punkt‑Rand und einen 4‑Punkt‑Margin.
  - name: Füge der Tabelle die zweite Zeile hinzu.
    text: Füge der Tabelle die zweite Zeile hinzu.
  - name: Erstelle die dritte Zelle, füge "Third cell" ein, setze einen hellcyanfarbenen
      Hintergrund, einen dunkelgrauen 2‑Punkt‑Rand und einen 4‑Punkt‑Margin.
    text: Erstelle die dritte Zelle, füge "Third cell" ein, setze einen hellcyanfarbenen
      Hintergrund, einen dunkelgrauen 2‑Punkt‑Rand und einen 4‑Punkt‑Margin.
  - name: Erstelle die vierte Zelle, füge "Fourth cell" hinzu, gib ihr einen hellrosa
      Hintergrund, einen violetten 2‑Punkt‑Rand und einen 4‑Punkt‑Margin.
    text: Erstelle die vierte Zelle, füge "Fourth cell" hinzu, gib ihr einen hellrosa
      Hintergrund, einen violetten 2‑Punkt‑Rand und einen 4‑Punkt‑Margin.
  - name: Füge die vollständig formatierte Tabelle der Seite hinzu, damit sie im PDF
      sichtbar wird.
    text: Füge die vollständig formatierte Tabelle der Seite hinzu, damit sie im PDF
      sichtbar wird.
  - name: Speichere das PDF‑Dokument in einer Datei und schließe den using‑Block.
    text: Speichere das PDF‑Dokument in einer Datei und schließe den using‑Block.
  - name: Gib eine Bestätigungsnachricht in der Konsole aus.
    text: Gib eine Bestätigungsnachricht in der Konsole aus.
  type: HowTo
- questions:
  - answer: '`DefaultCellPadding` liefert ein Basis‑Padding für jede Zelle, aber wenn
      Sie einen `Margin` zuweisen (z. B. `cellA1.Margin = new MarginInfo(...)`), überschreiben
      die Margin‑Werte das Standard‑Padding für diese spezielle Zelle.'
    question: Wirkt das auf dem `Table` gesetzte `DefaultCellPadding` auf Zellen,
      die ebenfalls einen `Margin` definiert haben?
  - answer: Ohne `Table.Border` wird das äußere Rechteck um die gesamte Tabelle weggelassen;
      nur die einzelnen Zellränder, die Sie setzen (z. B. `cellA2.Border`), sind sichtbar.
    question: Wie sieht das PDF aus, wenn ich die `Border`‑Eigenschaft vom `Table`‑Objekt
      entferne?
  - answer: Ja, erstellen Sie ein `BorderInfo` mit einer bestimmten `BorderSide` (z. B.
      `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) und weisen Sie
      es der `Border`‑Eigenschaft der Zelle zu.
    question: Kann ich einer Zelle für jede Seite eine unterschiedliche Randbreite
      zuweisen?
  - answer: Instanziieren Sie ein neues `Row` mit `Row newRow = dataTable.Rows.Add();`
      und fügen Sie dann Zellen zu `newRow.Cells` hinzu, genau wie bei den vorherigen
      Zeilen.
    question: Wie füge ich nach dem gezeigten Code eine dritte Zeile zur Tabelle hinzu?
  type: FAQPage
images:
- /net/tables-lists/style-table-cells/og-image.png
og_title: PDF‑Tabellenzellen formatieren – Hintergrund, Rand, Padding
og_description: Formatieren Sie Tabellenzellen in einem PDF schnell mit benutzerdefinierten Farben, Rändern und Abständen, indem Sie Aspose.Pdf für .NET verwenden.
og_image_alt: Leitfaden, der zeigt, wie man die Hintergrundfarbe, den Rand und das Padding von Tabellenzellen in einem PDF mit Aspose.Pdf für .NET gestaltet
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Passe den Hintergrund, die Ränder und das Padding von Tabellenzellen in PDFs mit Aspose.Pdf für .NET an
In diesem Tutorial sehen Sie, wie man ein PDF‑Dokument erzeugt, eine zweispaltige Tabelle hinzufügt und das Aussehen jeder Zelle präzise steuert. Durch das Festlegen von Hintergrundfarben, das Definieren von Rändern und das Anpassen des Paddings können Tabellendaten hervorgehoben und professionell dargestellt werden. Das Beispiel verwendet die Aspose.Pdf Document‑ und Table‑Klassen, um jede Styling‑Option zu demonstrieren.

---

{{< tutorial-widget sourcePath="pdf/net/tables-lists/style-table-cells" >}}


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

**Q: Wirkt das auf dem `Table` gesetzte `DefaultCellPadding` auf Zellen, die ebenfalls einen `Margin` definiert haben?**  
A: `DefaultCellPadding` liefert ein Basis‑Padding für jede Zelle, aber wenn Sie einen `Margin` zuweisen (z. B. `cellA1.Margin = new MarginInfo(...)`), überschreiben die Margin‑Werte das Standard‑Padding für diese spezielle Zelle.

**Q: Wie sieht das PDF aus, wenn ich die `Border`‑Eigenschaft vom `Table`‑Objekt entferne?**  
A: Ohne `Table.Border` wird das äußere Rechteck um die gesamte Tabelle weggelassen; nur die einzelnen Zellränder, die Sie setzen (z. B. `cellA2.Border`), sind sichtbar.

**Q: Kann ich einer Zelle für jede Seite eine unterschiedliche Randbreite zuweisen?**  
A: Ja, erstellen Sie ein `BorderInfo` mit einer bestimmten `BorderSide` (z. B. `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) und weisen Sie es der `Border`‑Eigenschaft der Zelle zu.

**Q: Wie füge ich nach dem gezeigten Code eine dritte Zeile zur Tabelle hinzu?**  
A: Instanziieren Sie ein neues `Row` mit `Row newRow = dataTable.Rows.Add();` und fügen Sie dann Zellen zu `newRow.Cells` hinzu, genau wie bei den vorherigen Zeilen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}