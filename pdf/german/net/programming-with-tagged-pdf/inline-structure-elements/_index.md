---
"description": "Schritt-für-Schritt-Anleitung zur Verwendung von Online-Strukturelementen mit Aspose.PDF für .NET. Organisieren Sie Ihre PDFs mit Überschriften und Absätzen."
"linktitle": "Inline-Strukturelemente"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Inline-Strukturelemente"
"url": "/de/net/programming-with-tagged-pdf/inline-structure-elements/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Inline-Strukturelemente

## Einführung

Die Erstellung barrierefreier und gut strukturierter Dokumente ist in der heutigen digitalen Welt unerlässlich. Wer schon einmal beim Durchblättern einer PDF-Datei den Überblick verloren hat, weiß, wie wichtig eine gute Organisation ist. Das Markieren von Elementen in Ihrer PDF-Datei kann die Barrierefreiheit verbessern und Bildschirmleseprogrammen die Interpretation von Inhalten erleichtern. In diesem Leitfaden erfahren Sie mehr über die Verwendung von Aspose.PDF für .NET zur Erstellung getaggter PDF-Dokumente und stellen sicher, dass Ihre Arbeit modernen Standards der Dokumentstrukturierung entspricht.

## Voraussetzungen

Bevor wir loslegen, stellen wir sicher, dass Sie alles haben, was Sie zum Mitmachen brauchen:

1. Grundkenntnisse in C#: Kenntnisse in der C#-Programmierung und den Grundlagen des .NET-Frameworks sind unerlässlich.
2. Visual Studio installiert: Sie benötigen eine IDE wie Visual Studio, um Ihren Code zu schreiben und auszuführen.
3. Aspose.PDF für .NET: Stellen Sie sicher, dass Sie Aspose.PDF für .NET herunterladen und installieren. Sie können es von der [Download-Link](https://releases.aspose.com/pdf/net/).
4. Eine temporäre Lizenz: Dies ist optional, aber wenn Sie alle Funktionen ohne Einschränkungen testen möchten, sollten Sie eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).

Sobald diese Voraussetzungen erfüllt sind, können Sie Ihr erstes getaggtes PDF-Dokument erstellen!

## Pakete importieren

Importieren wir zunächst die erforderlichen Pakete. So kann Ihr Projekt die Funktionen der Aspose.PDF-Bibliothek nutzen.

1. Öffnen Sie Ihr Visual Studio-Projekt.
2. Fügen Sie einen Verweis auf die Aspose.PDF-Bibliothek hinzu. Falls Sie sie noch nicht hinzugefügt haben, können Sie sie mit dem NuGet-Paket-Manager installieren.
3. Fügen Sie am Anfang Ihrer C#-Datei die folgenden Namespaces ein:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Mit diesen Importen sind Sie auf Erfolg eingestellt.

## Code-Aufschlüsselung: Schritt-für-Schritt-Anleitung zum Erstellen eines getaggten PDF

Nachdem wir nun alles eingerichtet haben, analysieren wir den Code Schritt für Schritt. Wir erstellen ein getaggtes PDF mit strukturierten Elementen wie Überschriften und Absätzen, um die Barrierefreiheit zu verbessern.

### Schritt 1: Dokumentverzeichnis festlegen

Legen Sie zunächst den Pfad fest, unter dem Ihr Dokument gespeichert werden soll. Es empfiehlt sich, eine geordnete Dateistruktur beizubehalten.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Ersetzen Sie es durch Ihren tatsächlichen Pfad
```

### Schritt 2: Erstellen Sie eine PDF-Dokumentinstanz

Als nächstes erstellen Sie eine Instanz des `Document` Klasse, die als Container für Ihren PDF-Inhalt dient.

```csharp
Document document = new Document();
```

### Schritt 3: Zugriff auf markierte Inhalte

Greifen Sie nun auf den getaggten Inhalt des Dokuments zu. Hier geschieht der Zauber: Durch das Taggen des Inhalts verbessern wir seine Zugänglichkeit.

```csharp
ITaggedContent taggedContent = document.TaggedContent;    
```

### Schritt 4: Titel und Sprache festlegen

Das Festlegen eines Titels und einer Sprache für Ihr PDF-Dokument ist sowohl für Benutzer als auch für Bildschirmleseprogramme wichtig. Dadurch wird Ihr Dokument informativer und zugänglicher.

```csharp
taggedContent.SetTitle("Tagged Pdf Document");
taggedContent.SetLanguage("en-US");
```

### Schritt 5: Holen Sie sich das Stammstrukturelement

Beginnen wir mit dem Hinzufügen von Elementen zu Ihrem Dokument. Rufen Sie zunächst das Stammstrukturelement des getaggten Inhalts ab, das als Grundlage für die Struktur Ihres Dokuments dient.

```csharp
StructureElement rootElement = taggedContent.RootElement;
```

### Schritt 6: Header-Elemente erstellen

Jetzt ist es an der Zeit, Header-Elemente zu erstellen. Dies hilft dabei, den Inhalt hierarchisch zu ordnen. Wir erstellen sechs Header-Ebenen.

```csharp
HeaderElement h1 = taggedContent.CreateHeaderElement(1);
HeaderElement h2 = taggedContent.CreateHeaderElement(2);
HeaderElement h3 = taggedContent.CreateHeaderElement(3);
HeaderElement h4 = taggedContent.CreateHeaderElement(4);
HeaderElement h5 = taggedContent.CreateHeaderElement(5);
HeaderElement h6 = taggedContent.CreateHeaderElement(6);
```

### Schritt 7: Anhängen von Headern an das Stammelement

Nachdem Sie Header-Elemente erstellt haben, hängen Sie diese an das Stammelement an. Dadurch wird die Strukturhierarchie des Dokuments erstellt.

```csharp
rootElement.AppendChild(h1);
rootElement.AppendChild(h2);
rootElement.AppendChild(h3);
rootElement.AppendChild(h4);
rootElement.AppendChild(h5);
rootElement.AppendChild(h6);
```

### Schritt 8: Fügen Sie jeder Überschrift Text hinzu

Fügen wir nun jeder Überschrift Text hinzu. Dies ist ein einfacher Vorgang, aber wichtig für die Nutzbarkeit Ihres Dokuments. 

```csharp
// H1
SpanElement spanH11 = taggedContent.CreateSpanElement();
spanH11.SetText("H1. ");
h1.AppendChild(spanH11);
SpanElement spanH12 = taggedContent.CreateSpanElement();
spanH12.SetText("Level 1 Header");
h1.AppendChild(spanH12);

// Wiederholen Sie dies für H2 – H6 wie oben gezeigt
```

### Schritt 9: Erstellen Sie ein Absatzelement

Als Nächstes fügen wir ein Absatzelement hinzu. Dieses dient als Hauptinhaltsbereich Ihrer PDF-Datei. 

```csharp
ParagraphElement p = taggedContent.CreateParagraphElement();
p.SetText("P. ");
rootElement.AppendChild(p);
```

### Schritt 10: Fügen Sie dem Absatz Text hinzu

Nachdem wir nun unser Absatzelement erstellt haben, ist es an der Zeit, es mit Text zu füllen. Sie können mehrere Bereiche hinzufügen, um Ihren Inhalt zusammenzustellen.

```csharp
SpanElement span1 = taggedContent.CreateSpanElement();
span1.SetText("Lorem ipsum dolor sit amet, consectetur adipiscing elit. ");
p.AppendChild(span1);
// Fügen Sie bei Bedarf weitere Spannen hinzu
```

### Schritt 11: Speichern Sie das getaggte PDF-Dokument

Nachdem Sie alle Inhalte hinzugefügt haben, müssen Sie Ihr Dokument abschließend speichern. So, jetzt geht's!

```csharp
document.Save(dataDir + "InlineStructureElements.pdf");
```

Und voilà! Sie haben jetzt ein getaggtes PDF-Dokument, das strukturiert und zugänglich ist.

## Abschluss

Das Erstellen getaggter PDF-Dokumente mag schwierig erscheinen, aber mit Aspose.PDF für .NET ist es ein Kinderspiel! Mit dieser Schritt-für-Schritt-Anleitung beherrschen Sie die Grundlagen der Dokumentstrukturierung. Denken Sie daran: Richtiges Taggen Ihrer PDF-Datei verbessert deren Zugänglichkeit und stellt sicher, dass Ihre wertvollen Inhalte ein breiteres Publikum erreichen. Gestalten Sie Ihre PDFs also nicht nur ansprechend, sondern auch benutzerfreundlich!

## Häufig gestellte Fragen

### Was ist ein getaggtes PDF?
Ein getaggtes PDF ist ein PDF, das Informationen zur Struktur des Dokuments enthält und es dadurch für Benutzer mit Behinderungen leichter zugänglich macht.

### Warum ist das Taggen in PDFs wichtig?
Durch Tagging wird die Zugänglichkeit verbessert, da Bildschirmleseprogramme das Dokument klar interpretieren können und Benutzern mit Behinderungen so ein besseres Erlebnis bieten.

### Kann ich Aspose.PDF kostenlos nutzen?
Ja, Sie können Aspose.PDF für .NET über eine [kostenlose Testversion](https://releases.aspose.com/).

### Wo erhalte ich Support für Aspose.PDF?
Support erhalten Sie über die [Aspose-Supportforum](https://forum.aspose.com/c/pdf/10).

### Wie kann ich die Aspose.PDF-Lizenz für .NET erwerben?
Sie können eine Lizenz direkt von der [Kaufseite](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}