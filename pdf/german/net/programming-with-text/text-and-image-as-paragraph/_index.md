---
"description": "Erstellen Sie PDFs mit Text und Bildern mit Aspose.PDF für .NET. Erfahren Sie Schritt für Schritt, wie Sie Text und Inline-Bilder hinzufügen."
"linktitle": "Text und Bild als Absatz in einer PDF-Datei"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Text und Bild als Absatz in einer PDF-Datei"
"url": "/de/net/programming-with-text/text-and-image-as-paragraph/"
"weight": 530
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Text und Bild als Absatz in einer PDF-Datei

## Einführung

In der heutigen digitalen Welt sind PDFs ein universelles Dokumentformat, mit dem die meisten von uns täglich zu tun haben. Ob Bericht, E-Book oder Geschäftsrechnung – PDFs erleichtern den Informationsaustausch über verschiedene Plattformen hinweg. Doch was, wenn Sie ein PDF programmgesteuert anpassen möchten? Hier kommt Aspose.PDF für .NET ins Spiel. In diesem Tutorial zeigen wir Ihnen, wie Sie mit Aspose.PDF für .NET Text und Bilder als Inline-Absätze in eine PDF-Datei einfügen.

## Voraussetzungen

Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie alles haben, was Sie brauchen, um reibungslos mitmachen zu können:

- Aspose.PDF für .NET Bibliothek: Sie müssen Aspose.PDF für .NET installieren. Sie können es herunterladen [Hier](https://releases.aspose.com/pdf/net/).
- Visual Studio: Jede Version, die .NET unterstützt, funktioniert einwandfrei.
- Grundlegende Kenntnisse in C#: Etwas Vertrautheit mit C# ist hilfreich, aber keine Sorge – ich werde Sie durch jeden Schritt führen!
- PDF-Dokument bereit: Wenn Sie ein benutzerdefiniertes Bild hinzufügen möchten, halten Sie es bereit.

Sie können auch eine kostenlose Testversion der Bibliothek erhalten [Hier](https://releases.aspose.com/), oder wenn Sie an einem Großprojekt arbeiten, sollten Sie den Kauf in Erwägung ziehen [Hier](https://purchase.aspose.com/buy)Benötigen Sie weitere Informationen? Schauen Sie sich die Dokumentation an [Hier](https://reference.aspose.com/pdf/net/).

## Pakete importieren

Um mit Aspose.PDF für .NET zu beginnen, müssen Sie die erforderlichen Namespaces importieren. Diese Namespaces ermöglichen Ihrem C#-Code die Interaktion mit Aspose.PDF-Funktionen.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System;
```

Einfach, oder? Jetzt kommen wir zum spaßigen Teil: dem Erstellen Ihrer eigenen PDF-Datei.

## Schritt-für-Schritt-Anleitung: Erstellen eines PDFs mit Text und Inline-Bild

Lassen Sie uns dies in verständliche, leicht verständliche Schritte unterteilen. Stellen Sie sich vor, Sie setzen ein Puzzle zusammen; jeder Schritt ist wie das Finden und Platzieren des richtigen Teils.

## Schritt 1: Initialisieren Sie das PDF-Dokument

Der erste Schritt besteht darin, ein neues PDF-Dokument mit Aspose.PDF zu initialisieren. Dieses Dokument dient als Grundlage für das Hinzufügen von Text und Bildern.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// Dokumentinstanz instanziieren
Document doc = new Document();
```

Was passiert hier? Wir erstellen einfach ein neues Dokument mit dem `Document` Klasse und definieren Sie das Verzeichnis, in dem Sie die PDF-Datei speichern möchten. Es ist, als würden Sie eine neue Leinwand für Ihr Meisterwerk öffnen!

## Schritt 2: Fügen Sie Ihrer PDF-Datei eine Seite hinzu

Ein Dokument ohne Seiten ist nicht besonders nützlich, oder? Fügen wir Ihrem Dokument eine leere Seite hinzu.

```csharp
// Seite zur Seitensammlung der Dokumentinstanz hinzufügen
Page page = doc.Pages.Add();
```

Dieser Codeausschnitt fügt der Seitensammlung Ihres Dokuments eine neue Seite hinzu. Stellen Sie sich das so vor, als würden Sie eine leere Seite in einem Notizbuch aufschlagen.

## Schritt 3: Text als Absatz hinzufügen

Als Nächstes fügen wir einen Textabschnitt hinzu. Hier können Sie Ihre Nachricht oder Überschrift einfügen.

```csharp
// TextFragment erstellen
TextFragment text = new TextFragment("Hello World.. ");
// Fügen Sie der Absatzsammlung des Seitenobjekts ein Textfragment hinzu
page.Paragraphs.Add(text);
```

Hier erstellen wir eine `TextFragment` Objekt für den Text „Hallo Welt…“, der dann als Absatz zur Seite hinzugefügt wird. Es ist, als würde man den ersten Satz in einem PDF-Dokument schreiben.

## Schritt 4: Ein Bild als Inline-Absatz hinzufügen

Nachdem wir nun den Text erstellt haben, können wir ihn aufpeppen, indem wir ein Bild als Inline-Absatz hinzufügen. Ein Inline-Absatz bedeutet einfach, dass das Bild direkt nach dem Text erscheint, ähnlich wie Bilder in Word-Dokumenten angezeigt werden.

```csharp
// Erstellen einer Imageinstanz
Aspose.Pdf.Image image = new Aspose.Pdf.Image();
// Bild als Inline-Absatz festlegen, sodass es direkt danach erscheint 
// Das vorherige Absatzobjekt (TextFragment)
image.IsInLineParagraph = true;
// Bilddateipfad angeben 
image.File = dataDir + "aspose-logo.jpg";
```

In diesem Snippet erstellen wir ein `Image` Objekt, weisen Sie es an, es inline mit dem Text auszurichten, und geben Sie den Pfad zur Bilddatei an. Dies entspricht dem Einfügen eines Bildes direkt nach einem Satz in einem Dokument. Sie können „aspose-logo.jpg“ durch Ihr gewünschtes Bild ersetzen.

## Schritt 5: Bildgröße festlegen (optional)

Möchten Sie die Größe des Bildes ändern? Kein Problem. Aspose.PDF bietet Ihnen die Möglichkeit, die Höhe und Breite des Bildes anzupassen, bevor Sie es Ihrem Dokument hinzufügen.

```csharp
// Bildhöhe festlegen (optional)
image.FixHeight = 30;
// Bildbreite festlegen (optional)
image.FixWidth = 100;
```

Dieser Teil ist optional, hilft Ihnen aber dabei, die Größe des Bildes in Ihrer PDF-Datei zu steuern. Es ist, als würden Sie die Größe eines Fotos vor dem Ausdrucken ändern.

## Schritt 6: Bild zur Absatzsammlung hinzufügen

Wir haben das Bild vorbereitet. Jetzt fügen wir es als Inline-Absatz in das Dokument ein.

```csharp
// Bild zur Absatzsammlung des Seitenobjekts hinzufügen
page.Paragraphs.Add(image);
```

Diese Zeile fügt das Bild direkt nach dem Text in die Absatzsammlung ein. Es ist vergleichbar mit dem Klicken auf die Schaltfläche „Bild einfügen“ in einem Texteditor.

## Schritt 7: Einen weiteren Inline-Textabsatz hinzufügen

Was ist, wenn Sie direkt nach dem Bild weiteren Text hinzufügen möchten? Fügen Sie dazu ein weiteres Inline-Textfragment ein.

```csharp
// TextFragment-Objekt mit anderem Inhalt neu initialisieren
text = new TextFragment(" Hello Again..");
// TextFragment als Inline-Absatz festlegen
text.IsInLineParagraph = true;
// Fügen Sie der Absatzsammlung der Seite ein neu erstelltes TextFragment hinzu
page.Paragraphs.Add(text);
```

Wir verwenden die `TextFragment` Objekt hier mit neuem Text („Hello Again…“) und fügen Sie ihn direkt nach dem Bild ein. Dies verleiht Ihrem PDF ein fließendes, einheitliches Aussehen.

## Schritt 8: Speichern Sie das PDF-Dokument

Wir sind fast fertig! Speichern wir das Dokument nun im angegebenen Verzeichnis.

```csharp
dataDir = dataDir + "TextAndImageAsParagraph_out.pdf";
doc.Save(dataDir);
Console.WriteLine("\nText and image added successfully as inline paragraphs.\nFile saved at " + dataDir);
```

Dieser letzte Schritt speichert die Datei in Ihrem Verzeichnis unter dem Namen „TextAndImageAsParagraph_out.pdf“. Herzlichen Glückwunsch – Sie haben eine PDF-Datei mit Text und Inline-Bildern erstellt!

## Abschluss

Und fertig – das Erstellen einer PDF-Datei mit Text und Bildern als Inline-Absätze mit Aspose.PDF für .NET ist so einfach wie diese Schritte. Mit nur wenigen Codezeilen können Sie Ihren PDF-Dateien dynamische Inhalte hinzufügen und sie optisch ansprechender und professioneller gestalten. Ob Geschäftsbericht oder E-Book – die Kontrolle über das Layout Ihrer PDFs kann einen großen Unterschied machen.

## Häufig gestellte Fragen

### Kann ich mehrere Bilder als Inline-Absätze hinzufügen?  
Ja, Sie können mehrere Bilder hinzufügen, indem Sie separate `Image` Objekte und fügen Sie sie der Absatzsammlung hinzu.

### Kann ich die Position von Text und Bild im PDF steuern?  
Ja, mithilfe von Eigenschaften wie Rändern können Sie die genaue Platzierung Ihres Textes und Ihrer Bilder steuern.

### Ist Aspose.PDF für .NET kostenlos?  
Nein, es ist ein lizenziertes Produkt, aber Sie können eine [kostenlose Testversion](https://releases.aspose.com/) oder eine Lizenz kaufen [Hier](https://purchase.aspose.com/buy).

### Kann ich dem Text Hyperlinks hinzufügen?  
Ja, Aspose.PDF ermöglicht das Einfügen von Hyperlinks in Textfragmente. Überprüfen Sie die [Dokumentation](https://reference.aspose.com/pdf/net/) für weitere Details.

### Kann ich die Schriftart und den Stil des Textes anpassen?  
Absolut! Sie können Schriftarten, Farben und andere Stileigenschaften der Textfragmente ganz einfach anpassen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}