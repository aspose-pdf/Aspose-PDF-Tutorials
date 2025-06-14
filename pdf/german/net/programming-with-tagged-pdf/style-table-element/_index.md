---
"description": "Erfahren Sie, wie Sie ein Tabellenelement in Aspose.PDF für .NET erstellen und formatieren, mit Schritt-für-Schritt-Anleitungen, benutzerdefiniertem Styling und PDF/UA-Konformität."
"linktitle": "Stiltabellenelement"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Stiltabellenelement"
"url": "/de/net/programming-with-tagged-pdf/style-table-element/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Stiltabellenelement

## Einführung

In diesem Artikel erfahren Sie, wie Sie mit Aspose.PDF für .NET ein Tabellenelement erstellen und formatieren. Sie lernen, wie Sie eine Tabelle strukturieren, benutzerdefinierte Formatierungen anwenden und die PDF/UA-Konformität Ihres Dokuments überprüfen. Nach Abschluss dieses Tutorials können Sie mühelos professionell aussehende Tabellen in Ihren PDFs erstellen!

## Voraussetzungen

Bevor Sie mit dem Lernprogramm beginnen, müssen Sie sicherstellen, dass Sie über Folgendes verfügen:

1. Visual Studio oder eine ähnliche IDE muss auf Ihrem Computer installiert sein.
2. .NET Framework oder .NET Core SDK zum Ausführen der Anwendung.
3. Aspose.PDF für .NET-Bibliothek heruntergeladen und in Ihrem Projekt referenziert. Sie können die neueste Version von [Hier](https://releases.aspose.com/pdf/net/).
4. Eine gültige Aspose-Lizenz oder eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) um die volle Funktionalität der Bibliothek freizuschalten.

## Pakete importieren

Importieren Sie zunächst die erforderlichen Namespaces in Ihr Projekt:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Diese Namespaces decken grundlegende PDF-Vorgänge, getaggte Inhalte, Tabellen und Textformatierungen ab.

Lassen Sie uns nun den Prozess zum Erstellen und Gestalten einer Tabelle in Aspose.PDF genauer betrachten. Wir gehen jeden Abschnitt detailliert durch, damit Sie ihn nachvollziehen können.

## Schritt 1: Erstellen Sie ein neues PDF-Dokument und richten Sie getaggte Inhalte ein

In diesem ersten Schritt erstellen wir ein leeres PDF-Dokument und richten seinen getaggten Inhalt ein.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Erstellen Sie ein neues PDF-Dokument
Document document = new Document();

// Einrichten von getaggtem Inhalt
ITaggedContent taggedContent = document.TaggedContent;
taggedContent.SetTitle("Example table style");
taggedContent.SetLanguage("en-US");
```

Wir beginnen mit der Erstellung eines neuen `Document` Objekt, das unser PDF darstellt. Das `TaggedContent` Das Objekt dient zur Verwaltung der Dokumentstruktur und stellt die Einhaltung der Barrierefreiheitsstandards sicher. Wir legen Titel und Sprache des Dokuments für eine korrekte Verschlagwortung fest.

## Schritt 2: Definieren des Stammelements

Als Nächstes erstellen wir das Stammstrukturelement, das als Container für den gesamten Inhalt unserer PDF-Datei fungiert.

```csharp
// Holen Sie sich das Stammstrukturelement
StructureElement rootElement = taggedContent.RootElement;
```

Der `RootElement` dient als Basiscontainer für alle strukturierten Elemente, einschließlich unserer Tabelle. Es trägt dazu bei, die strukturelle Hierarchie des Dokuments aufrechtzuerhalten, was sowohl für die Organisation als auch für die Zugänglichkeit wichtig ist.

## Schritt 3: Erstellen und Gestalten des Tabellenelements

Nachdem das Stammelement eingerichtet ist, erstellen wir ein `TableElement` und wenden Sie Stile wie Hintergrundfarbe, Rahmen und Ausrichtung an.

```csharp
// Tabellenstrukturelement erstellen
TableElement tableElement = taggedContent.CreateTableElement();
rootElement.AppendChild(tableElement);

// Den Tisch stylen
tableElement.BackgroundColor = Color.Beige;
tableElement.Border = new BorderInfo(BorderSide.All, 0.80F, Color.Gray);
tableElement.Alignment = HorizontalAlignment.Center;
tableElement.Broken = TableBroken.Vertical;
tableElement.ColumnAdjustment = ColumnAdjustment.AutoFitToWindow;
```

Wir schaffen eine `TableElement`, die unsere Tabellenstruktur definiert. Die `BackgroundColor`, `Border`, Und `Alignment` Eigenschaften ermöglichen es uns, das Erscheinungsbild der Tabelle anzupassen. Die `Broken` stellt sicher, dass die Tabelle bei einem Seitenumbruch vertikal umgebrochen wird.

## Schritt 4: Tabellenabmessungen und Zellenstile festlegen

In diesem Schritt definieren wir die Anzahl der Spalten, die Zellenauffüllung und andere wichtige Tabelleneigenschaften.

```csharp
tableElement.ColumnWidths = "80 80 80 80 80";
tableElement.DefaultCellBorder = new BorderInfo(BorderSide.All, 0.50F, Color.DarkBlue);
tableElement.DefaultCellPadding = new MarginInfo(16.0, 2.0, 8.0, 2.0);
tableElement.DefaultCellTextState.ForegroundColor = Color.DarkCyan;
tableElement.DefaultCellTextState.FontSize = 8F;
```

Wir legen die Spaltenbreiten fest, um sicherzustellen, dass jede Spalte in der Tabelle gleichmäßig verteilt ist. Die `DefaultCellBorder`, `DefaultCellPadding`, Und `DefaultCellTextState` Definieren Sie die Standardstile für die Zellen, einschließlich Rahmen, Polsterung, Textfarbe und Schriftgröße.

## Schritt 5: Wiederholende Zeilen und benutzerdefinierte Stile hinzufügen

Wir können auch Stile für sich wiederholende Zeilen und andere spezifische Tabellenelemente wie Kopf- und Fußzeilen definieren.

```csharp
tableElement.RepeatingRowsCount = 3;
TextState rowStyle = new TextState();
rowStyle.BackgroundColor = Color.LightCoral;
tableElement.RepeatingRowsStyle = rowStyle;
```

Der `RepeatingRowsCount` stellt sicher, dass die ersten drei Zeilen wiederholt werden, wenn die Tabelle mehrere Seiten umfasst. Wir setzen die `RepeatingRowsStyle` um diesen Zeilen eine benutzerdefinierte Hintergrundfarbe zuzuweisen.

## Schritt 6: Tabellenkopf-, Tabellenkörper- und Tabellenfußelemente hinzufügen

Lassen Sie uns nun die Abschnitte für Kopfzeile, Text und Fußzeile der Tabelle erstellen und mit Inhalt füllen.

```csharp
TableTHeadElement tableTHeadElement = tableElement.CreateTHead();
TableTBodyElement tableTBodyElement = tableElement.CreateTBody();
TableTFootElement tableTFootElement = tableElement.CreateTFoot();

// Kopfzeile erstellen
TableTRElement headTrElement = tableTHeadElement.CreateTR();
headTrElement.AlternativeText = "Head Row";
for (int colIndex = 0; colIndex < 5; colIndex++)
{
    TableTHElement thElement = headTrElement.CreateTH();
    thElement.SetText($"Head {colIndex}");
}

// Füllen Sie den Tabellenkörper
for (int rowIndex = 0; rowIndex < 10; rowIndex++)
{
    TableTRElement trElement = tableTBodyElement.CreateTR();
    for (int colIndex = 0; colIndex < 5; colIndex++)
    {
        TableTDElement tdElement = trElement.CreateTD();
        tdElement.SetText($"Cell [{rowIndex}, {colIndex}]");
    }
}
```

Die Tabelle ist in drei Teile gegliedert: Kopf, Körper und Fuß. Wir erstellen zunächst die Kopfzeile mit `TableTHElement` und fügen Spaltenüberschriften hinzu. Anschließend füllen wir den Hauptteil der Tabelle mit `TableTDElement`, wobei jede Zelle mit einer Beschriftung gefüllt wird, die ihre Position enthält.

## Schritt 7: Speichern Sie das Dokument

Abschließend speichern wir das PDF-Dokument im angegebenen Verzeichnis.

```csharp
// Speichern Sie das mit Tags versehene PDF-Dokument
document.Save(dataDir + "StyleTableElement.pdf");
```

Dieser Schritt schließt den Dokumenterstellungsprozess ab, indem die PDF-Datei mit der formatierten Tabelle gespeichert wird.

## Schritt 8: PDF/UA-Konformität validieren

Nach dem Speichern des Dokuments muss unbedingt sichergestellt werden, dass es den PDF/UA-Standards (Universal Accessibility) entspricht.

```csharp
// Überprüfen Sie die PDF/UA-Konformität
document = new Document(dataDir + "StyleTableElement.pdf");
bool isPdfUaCompliance = document.Validate(dataDir + "StyleTableElement.xml", PdfFormat.PDF_UA_1);
Console.WriteLine($"PDF/UA compliance: {isPdfUaCompliance}");
```

Hier laden wir das Dokument neu und validieren es anhand der PDF/UA-Standards. Durch die Konformität wird sichergestellt, dass Ihr PDF den Anforderungen an die Barrierefreiheit entspricht und somit für eine breite Benutzergruppe geeignet ist.

## Abschluss

Mit Aspose.PDF für .NET ist das Erstellen und Gestalten von Tabellen in Ihren PDF-Dokumenten einfach und intuitiv. Mit den in diesem Tutorial beschriebenen Schritten können Sie Tabellen mit benutzerdefinierten Stilen erstellen und sicherstellen, dass Ihre PDFs den Barrierefreiheitsstandards entsprechen. Ob Sie Berichte erstellen oder strukturierte Dokumente erstellen – Tabellen sind ein leistungsstarkes Werkzeug zur übersichtlichen Darstellung von Daten.

## Häufig gestellte Fragen

### Kann ich Bilder in Tabellenzellen einfügen?
Ja, Sie können Bilder in Tabellenzellen einfügen, indem Sie `Image` Element.

### Wie passe ich die Spaltenbreiten dynamisch an?
Sie können die `ColumnAdjustment` Eigentum zu `AutoFitToWindow` um die Spaltenbreiten automatisch an den Inhalt anzupassen.

### Ist die PDF/UA-Konformität für alle Dokumente obligatorisch?
Obwohl es nicht zwingend erforderlich ist, wird es für Dokumente empfohlen, die hohe Zugänglichkeitsstandards erfordern.

### Kann ich bestimmten Zeilen unterschiedliche Stile zuweisen?
Ja, Sie können einzelne Zeilen oder Zellen anpassen, indem Sie deren `TextState` oder `BackgroundColor`.

### Welchen Vorteil bietet die Verwendung getaggter Inhalte?
Markierter Inhalt verbessert die Zugänglichkeit von Dokumenten und trägt dazu bei, die Einhaltung von Standards wie PDF/UA sicherzustellen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}