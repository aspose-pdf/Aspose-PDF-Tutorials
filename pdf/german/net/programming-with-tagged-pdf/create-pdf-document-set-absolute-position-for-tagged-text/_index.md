---
category: general
date: 2026-03-24
description: Erstellen Sie ein PDF-Dokument und lernen Sie, wie Sie die absolute Position
  für getaggten Text festlegen. Dieses Tutorial zeigt, wie man ein Span‑Element hinzufügt,
  wie man getaggten Inhalt einfügt und Text auf der Seite positioniert.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: de
og_description: Erstelle ein PDF‑Dokument und sieh sofort, wie du eine absolute Position
  festlegst, ein Span‑Element hinzufügst und Text auf der Seite mit getaggtem PDF‑Inhalt
  positionierst.
og_title: PDF-Dokument erstellen – Absolute Positionierung von getaggtem Text
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: PDF-Dokument erstellen – Absolute Position für getaggten Text festlegen
url: /de/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF-Dokument erstellen – Absolute Position für getaggten Text festlegen

Haben Sie schon einmal **ein PDF-Dokument erstellen** müssen, das zugänglichen, getaggten Text enthält, der genau dort positioniert ist, wo Sie ihn haben wollen? Vielleicht bauen Sie ein formularähnliches PDF, bei dem das Etikett an einer genauen Koordinate sitzen muss, oder Sie erzeugen ein Zertifikat und der Name muss perfekt mit einem Hintergrundbild ausgerichtet sein.  

In diesem Leitfaden gehen wir ein komplettes, ausführbares Beispiel durch, das zeigt, **wie man getaggten** Inhalt **hinzufügt**, **eine absolute Position festlegt** und **ein Span-Element hinzufügt**, sodass Sie **Text auf der Seite positionieren** können, ohne zu raten. Keine externen Referenzen – nur der Code, den Sie kopieren‑und‑einfügen können, plus Erklärungen zum „Warum“ hinter jeder Zeile.

## Voraussetzungen

- .NET 6+ (or .NET Framework 4.6+) with a C# compiler  
- Aspose.Pdf for .NET (latest version at the time of writing, 23.12) installed via NuGet  
- Basic familiarity with C# syntax  

Wenn Sie das haben, legen wir los.

---

## PDF-Dokument erstellen – Absolute Position festlegen

Das Erste, was wir tun, ist ein leeres `Document` zu instanziieren. Dieses Objekt repräsentiert die gesamte PDF‑Datei und gibt uns Zugriff auf den getaggten Inhaltsbaum.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Warum das wichtig ist:**  
`Document` ist die Wurzel der PDF‑Struktur. Indem wir es zuerst erstellen, stellen wir sicher, dass es eine Leinwand sowohl für visuelle Elemente (Seiten, Grafiken) als auch für die logische Struktur (Tags) gibt. Die `using`‑Anweisung garantiert, dass die Datei ordnungsgemäß freigegeben wird, was Datei‑Handle‑Lecks unter Windows verhindert.

## Getaggten Inhalt aktivieren (Wie man getaggten Inhalt hinzufügt)

Bevor wir irgendwelche getaggten Elemente einfügen können, muss das Dokument als *tagged* markiert sein. Aspose.Pdf erstellt automatisch ein `TaggedContent`‑Objekt, aber Sie müssen das Flag trotzdem aktivieren.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**Was passiert im Hintergrund?**  
Das Setzen von `TaggedContent` auf `true` teilt PDF‑Readern mit, dass die Datei einen logischen Strukturbaum enthält. Das ist entscheidend für Screen‑Reader und dafür, dass die `SetPosition`‑Methode bei einem Span‑Element korrekt funktioniert.

## Das Wurzelelement des getaggten Inhaltsbaums abrufen

Das Wurzelelement ist der Einstiegspunkt für alle strukturellen Tags (wie `<Document>`, `<Section>`, `<Span>`). Betrachten Sie es als den unsichtbaren „Body“ des PDFs.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Warum wir das Wurzelelement benötigen:**  
Alle nachfolgenden Tags müssen irgendwo im Baum angehängt werden; andernfalls erscheinen sie nicht in der Zugänglichkeits‑Hierarchie.

## Span-Element hinzufügen – Der Baustein für Inline‑Text

Ein *Span* ist das PDF‑Äquivalent zu einem HTML‑`<span>` – perfekt für kurze Textstücke, die Sie präzise positionieren möchten.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Design‑Hinweis:**  
Wenn Sie umfangreichere Formatierung benötigen (fett, kursiv, Hyperlinks), können Sie das Span in ein `<Paragraph>` einbetten oder später `TextFragment`‑Objekte verwenden. Für absolute Positionierung ist ein einfaches Span das leichteste.

## Absolute Position festlegen – X=100, Y=200

Jetzt kommt der spaßige Teil: das Span an einer genauen Stelle auf der Seite zu platzieren. Das Koordinatensystem beginnt in der linken unteren Ecke (0,0) und verwendet Punkte (1 pt ≈ 1/72 in).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**Warum absolute Positionierung?**  
Wenn Sie ein pixelgenaues Layout benötigen – denken Sie an Zertifikate, Rechnungen oder Formulare – reicht relativer Fluss (wie links‑nach‑rechts‑Text) nicht aus. `SetPosition` umgeht den normalen Textfluss und verankert das Element an der von Ihnen angegebenen Stelle.

## Text zum Span hinzufügen

Nachdem das Span positioniert ist, fügen wir nun die eigentliche Zeichenkette ein.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**Tipp:**  
Wenn Sie Unicode‑Zeichen oder Rechts‑nach‑Links‑Schriften benötigen, übergeben Sie einfach die Zeichenkette; Aspose.Pdf kümmert sich automatisch um die Kodierung.

## Das Span an das Wurzelelement anhängen

Abschließend hängen wir das Span an den logischen Baum des Dokuments an, sodass es Teil des finalen PDFs wird.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**Was passiert, wenn Sie diesen Schritt vergessen?**  
Das Span würde im Speicher existieren, aber nie in die Datei serialisiert werden, sodass kein Text angezeigt wird und der Zugänglichkeits‑Baum unvollständig bleibt.

## Vollständiges, ausführbares Beispiel

Unten finden Sie das vollständige Programm, das Sie in eine Konsolen‑App einfügen können. Es erstellt ein einseitiges PDF, fügt ein getaggtes Span bei (100, 200) hinzu und speichert die Datei als `TaggedPositioned.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**Erwartete Ausgabe:**  
Öffnen Sie `TaggedPositioned.pdf` in einem beliebigen Viewer (Adobe Acrobat, Foxit usw.). Sie sehen die Phrase **„Positioned tagged text“** exakt 100 pt vom linken Rand und 200 pt vom unteren Rand der Seite. Wenn Sie das *Tags*-Panel inspizieren, wird ein `<Span>`‑Element unter dem Wurzelelement des Dokuments aufgeführt, was bestätigt, dass der Inhalt korrekt getaggt ist.

## Häufige Fragen & Sonderfälle

### Was, wenn ich Text auf einer anderen Seite als der ersten positionieren muss?

Fügen Sie die gewünschte Seite hinzu (`var page = pdfDocument.Pages[3];`) bevor Sie `SetPosition` aufrufen. Das Span wird automatisch an den aktiven Seiten‑Kontext angehängt.

### Kann ich die Position in Zoll oder Zentimetern festlegen?

`SetPosition` akzeptiert Punkte. Konvertieren Sie mit den Formeln:  
- **Zoll → Punkte:** `points = inches * 72`  
- **Zentimeter → Punkte:** `points = cm * 28.3465`

### Wie ändere ich die Schriftart oder Farbe des Span?

Nachdem Sie das Span erstellt haben, können Sie dessen `TextState` abrufen und ändern:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### Was, wenn das Dokument bereits vorhandene Tags hat?

Sie können weiterhin ein neues Span erstellen und es an ein beliebiges vorhandenes Element anhängen (`rootElement`, ein bestimmtes `<Section>` usw.). Achten Sie nur darauf, eine logische Hierarchie beizubehalten – Screen‑Reader erwarten einen gut strukturierten Baum.

### Funktioniert das mit PDF/A‑ oder PDF/UA‑Konformität?

Ja. Getaggte PDFs sind eine Kernanforderung für PDF/UA. Wenn Sie PDF/A benötigen, setzen Sie nach dem Erstellen des Inhalts `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));`.

## Pro‑Tipps & Fallstricke

- **Pro‑Tipp:** Fügen Sie immer eine Seite hinzu, bevor Sie Inhalte positionieren. Ohne Seite schlägt `SetPosition` stillschweigend fehl, weil es keinen Ort zum Rendern gibt.
- **Achten Sie auf Einheiten:** Das Mischen von Pixeln aus einem UI‑Design mit PDF‑Punkten verschiebt Ihren Text. Überprüfen Sie die Umrechnung doppelt.
- **Performance‑Hinweis:** Wenn Sie Tausende von PDFs erzeugen, verwenden Sie eine einzelne `Document`‑Instanz wieder und rufen Sie `pdfDocument.Pages.Clear()` zwischen den Durchläufen auf, um übermäßige Speicherzuweisungen zu vermeiden.
- **Barrierefreiheits‑Erinnerung:** Tagging ist nicht nur ein nettes Feature; viele Vorschriften (Section 508, EN 301 549) verlangen es. Die Verwendung von `CreateSpanElement` stellt sicher, dass der Text von unterstützenden Technologien gefunden wird.

## Fazit

Wir haben gerade **ein PDF-Dokument** von Grund auf **erstellt**, **eine absolute Position festgelegt**, **ein Span‑Element hinzugefügt** und gezeigt, **wie man getaggten** Inhalt einfügt, sodass Sie **Text auf der Seite** mit pixelgenauer Genauigkeit **positionieren** können. Das vollständige Beispiel ist bereit zum Ausführen, und die Erklärung deckte sowohl das *Wie* als auch das *Warum* ab – genau das, wonach Entwickler (und KI‑Assistenten) suchen, wenn sie eine zuverlässige Lösung benötigen.

Als Nächstes könnten Sie erkunden:
- Bilder hinter dem positionierten Text für wasserzeichen‑geschützte Zertifikate hinzufügen.
- `CreateParagraphElement` für mehrzeilige Blöcke verwenden, die dennoch absolute Platzierung benötigen.
- Export nach PDF/UA, um strenge Barrierefreiheits‑Audits zu erfüllen.

Passen Sie die Koordinaten, Schriftarten oder Farben gerne an – Experimentieren ist der schnellste Weg, die Erstellung getaggter PDFs zu meistern. Wenn Sie auf ein Problem stoßen, hinterlassen Sie unten einen Kommentar; happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}