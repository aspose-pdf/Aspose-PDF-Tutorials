---
"description": "Erfahren Sie, wie Sie Seitenzahlen im Inhaltsverzeichnis mit Aspose.PDF für .NET ausblenden. Folgen Sie dieser ausführlichen Anleitung mit Codebeispielen, um professionelle PDFs zu erstellen."
"linktitle": "Seitenzahlen im Inhaltsverzeichnis ausblenden"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Seitenzahlen im Inhaltsverzeichnis ausblenden"
"url": "/de/net/programming-with-document/hidepagenumbersintoc/"
"weight": 220
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Seitenzahlen im Inhaltsverzeichnis ausblenden

## Einführung

Wenn Sie mit PDFs arbeiten, möchten Sie manchmal ein Inhaltsverzeichnis erstellen, aber die Seitenzahlen ausblenden, um die Übersichtlichkeit zu wahren. Vielleicht wirkt das Dokument ohne sie besser, oder es ist eine ästhetische Entscheidung. Was auch immer Ihr Grund ist: Wenn Sie mit Aspose.PDF für .NET arbeiten, zeigt Ihnen dieses Tutorial genau, wie Sie Seitenzahlen in Ihrem Inhaltsverzeichnis ausblenden.

## Voraussetzungen

Bevor wir beginnen, müssen Sie einige Dinge vorbereiten. Hier ist eine kurze Checkliste:

- Visual Studio installiert: Sie benötigen eine funktionierende Version von Visual Studio, um mitzuprogrammieren.
- Aspose.PDF für .NET-Bibliothek: Stellen Sie sicher, dass Sie die Aspose.PDF für .NET-Bibliothek installiert haben.
  - Download-Link: [Aspose.PDF für .NET](https://releases.aspose.com/pdf/net/)
- Temporäre Lizenz: Wenn Sie die Funktionen testen, ist es hilfreich, eine temporäre Lizenz zu haben.
  - Temporäre Lizenz: [Hier herunterladen](https://purchase.aspose.com/temporary-license/)

## Pakete importieren

Bevor Sie mit dem Code beginnen, importieren Sie die folgenden Namespaces in Ihr C#-Projekt. Diese stellen die notwendigen Klassen und Methoden für die Arbeit mit PDF-Dokumenten und die Erstellung Ihres Inhaltsverzeichnisses bereit.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Nachdem Ihre Umgebung nun bereit ist und die Pakete importiert wurden, analysieren wir nun die einzelnen Schritte. Wir gehen auf jeden Teil des Codes ein, um die Übersichtlichkeit zu gewährleisten und Ihnen das Nachvollziehen zu erleichtern.

## Schritt 1: Initialisieren Sie Ihr PDF-Dokument

Als Erstes müssen wir ein neues PDF-Dokument erstellen und eine Seite für das Inhaltsverzeichnis (TOC) hinzufügen.


```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "HiddenPageNumbers_out.pdf";
Document doc = new Document();
Page tocPage = doc.Pages.Add();
```

- dataDir: Dies ist das Verzeichnis, in dem Ihre Ausgabedatei gespeichert wird.
- Document(): Initialisiert ein neues PDF-Dokument.
- Pages.Add(): Fügt dem Dokument eine neue leere Seite hinzu, die später Ihr Inhaltsverzeichnis enthält.

## Schritt 2: Inhaltsverzeichnisinformationen und Titel einrichten

Als Nächstes definieren wir die Inhaltsverzeichnisinformationen und legen unter anderem den Titel fest, der oben im Inhaltsverzeichnis angezeigt wird.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocPage.TocInfo = tocInfo;
```

- TocInfo: Dieses Objekt enthält alle Informationen zum Inhaltsverzeichnis.
- TextFragment: Stellt den Text des Inhaltsverzeichnistitels dar. Hier legen wir ihn als „Inhaltsverzeichnis“ fest.
- FontStyle: Wir formatieren den Inhaltsverzeichnistitel, indem wir seine Größe auf 20 setzen und ihn fett formatieren.
- tocPage.TocInfo: Wir weisen die Inhaltsverzeichnisinformationen der Seite zu, auf der das Inhaltsverzeichnis angezeigt wird.

## Schritt 3: Seitenzahlen im Inhaltsverzeichnis ausblenden

Jetzt kommt der spaßige Teil! Hier konfigurieren wir das Inhaltsverzeichnis, um die Seitenzahlen auszublenden.

```csharp
tocInfo.IsShowPageNumbers = false;
tocInfo.FormatArrayLength = 4;
```

- IsShowPageNumbers: Dies ist der magische Schalter, der die Seitenzahlen ausblendet. Stellen Sie ihn auf `false`und die Seitenzahlen werden nicht im Inhaltsverzeichnis angezeigt.
- FormatArrayLength: Wir setzen dies auf 4, um anzugeben, dass wir die Formatierung für vier Ebenen von Inhaltsverzeichnisüberschriften definieren möchten.

## Schritt 4: Inhaltsverzeichnisformatierung anpassen

Um Ihrem Inhaltsverzeichnis mehr Stil zu verleihen, definieren wir jetzt die Formatierung für verschiedene Überschriftenebenen.

```csharp
tocInfo.FormatArray[0].Margin.Right = 0;
tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
tocInfo.FormatArray[1].Margin.Left = 30;
tocInfo.FormatArray[1].TextState.Underline = true;
tocInfo.FormatArray[1].TextState.FontSize = 10;
tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;
tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;
```

- FormatArray: Dieses Array steuert die Formatierung von Inhaltsverzeichniseinträgen. Jeder Index stellt eine andere Überschriftenebene dar.
- Rand und Textstil: Wir legen Ränder fest und wenden Schriftstile wie Fett, Kursiv und Unterstrichen für jede Überschriftenebene an.

## Schritt 5: Überschriften zum Dokument hinzufügen

Fügen wir abschließend die eigentlichen Überschriften hinzu, die Teil des Inhaltsverzeichnisses sein werden.

```csharp
Page page = doc.Pages.Add();
for (int Level = 1; Level != 5; Level++)
{ 
    Heading heading2 = new Heading(Level); 
    TextSegment segment2 = new TextSegment(); 
    heading2.TocPage = tocPage; 
    heading2.Segments.Add(segment2); 
    heading2.IsAutoSequence = true; 
    segment2.Text = "this is heading of level " + Level; 
    heading2.IsInList = true; 
    page.Paragraphs.Add(heading2); 
}
```

- Überschrift und Textsegment: Diese stellen die Überschriften dar, die in Ihrem Inhaltsverzeichnis erscheinen. Jede Ebene erhält eine eigene Überschrift.
- IsAutoSequence: Nummeriert die Überschriften automatisch.
- IsInList: Stellt sicher, dass jede Überschrift im Inhaltsverzeichnis erscheint.

## Schritt 6: Speichern Sie das Dokument

Sobald alles eingestellt ist, speichern Sie das PDF-Dokument in der angegebenen Ausgabedatei.

```csharp
doc.Save(outFile);
```

Und das war’s! Sie haben erfolgreich ein PDF mit Inhaltsverzeichnis erstellt, und die Seitenzahlen sind ausgeblendet!

## Abschluss

Das Erstellen eines Inhaltsverzeichnisses in einer PDF-Datei und das Ausblenden von Seitenzahlen mag schwierig erscheinen, aber mit Aspose.PDF für .NET ist es ein Kinderspiel. In dieser Schritt-für-Schritt-Anleitung haben Sie gelernt, wie Sie das Inhaltsverzeichnisformat anpassen, Seitenzahlen ausblenden und verschiedene Stile auf Ihre Überschriften anwenden. Jetzt können Sie professionelle PDFs erstellen, die genau auf Ihre Bedürfnisse zugeschnitten sind.

## Häufig gestellte Fragen

### Kann ich im Inhaltsverzeichnis Seitenzahlen für bestimmte Überschriften anzeigen?
Nein, Aspose.PDF blendet Seitenzahlen für das gesamte Inhaltsverzeichnis ein oder aus. Sie können sie nicht selektiv für bestimmte Einträge ausblenden.

### Ist es möglich, dem Inhaltsverzeichnis weitere Ebenen hinzuzufügen?
Ja, Sie können die `FormatArrayLength` um weitere Ebenen von Inhaltsverzeichnisüberschriften zu definieren.

### Wie kann ich die Schriftart für alle Inhaltsverzeichniseinträge ändern?
Sie können die Schriftart ändern, indem Sie die `TextState.Font` Eigenschaft für jede Ebene in der `FormatArray`.

### Kann ich Hyperlinks in das Inhaltsverzeichnis einfügen?
Ja, Sie können jeden Inhaltsverzeichniseintrag mit einem bestimmten Abschnitt im Dokument verknüpfen, indem Sie `Heading.TocPage` Eigentum.

### Benötige ich eine Lizenz für Aspose.PDF?
Ja, für den produktiven Einsatz ist eine gültige Lizenz erforderlich. Sie können eine temporäre Lizenz erhalten [Hier](https://purchase.aspose.com/temporary-license/) um die Funktionen zu testen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}