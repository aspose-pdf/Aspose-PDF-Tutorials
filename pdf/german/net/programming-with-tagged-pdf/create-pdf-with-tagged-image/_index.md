---
"description": "Erfahren Sie, wie Sie mit Aspose.PDF für .NET ein getaggtes PDF mit Bildern erstellen. Folgen Sie unserer Schritt-für-Schritt-Anleitung zur barrierefreien und professionellen Dokumenterstellung."
"linktitle": "PDF mit markiertem Bild erstellen"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "PDF mit markiertem Bild erstellen"
"url": "/de/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/"
"weight": 40
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF mit markiertem Bild erstellen

## Einführung

Das Erstellen von PDFs kann komplex sein, muss es aber nicht! Heute zeigen wir Ihnen, wie Sie mit Aspose.PDF für .NET ein PDF-Dokument mit einem getaggten Bild erstellen. Wenn Sie Bilder in Ihre PDFs integrieren und deren Barrierefreiheit sicherstellen möchten, sind Sie hier genau richtig. Wir erklären Ihnen Schritt für Schritt, wie Sie mühelos professionelle und barrierefreie PDFs erstellen.

## Voraussetzungen

Bevor Sie mit der Erstellung Ihrer PDF-Datei mit getaggten Bildern beginnen, benötigen Sie einige Dinge:

1. Aspose.PDF für .NET: Diese leistungsstarke Bibliothek ist für die Verarbeitung von PDF-Dokumenten in .NET-Anwendungen unerlässlich. Sie finden die Bibliothek hier: [Aspose.PDF für .NET herunterladen](https://releases.aspose.com/pdf/net/).
2. .NET Framework oder .NET Core: Stellen Sie sicher, dass auf Ihrem Computer eine kompatible Version von .NET Framework oder .NET Core installiert ist. Diese Bibliothek unterstützt beide Versionen.
3. Bilddatei: Sie benötigen eine Bilddatei zum Einbetten in Ihre PDF-Datei. In unserem Beispiel verwenden wir die Datei „aspose-logo.png“. Stellen Sie sicher, dass diese in Ihrem Dokumentenverzeichnis bereitliegt. 

Wenn Sie sicherstellen, dass diese Voraussetzungen erfüllt sind, können Sie beginnen!

## Pakete importieren

Um mit unserem Programmierabenteuer zu beginnen, müssen wir unseren Arbeitsbereich einrichten, indem wir die erforderlichen Aspose.PDF-Namespaces importieren. So geht's:

### Neues Projekt erstellen

- Öffnen Sie Ihre bevorzugte IDE (z. B. Visual Studio).
- Erstellen Sie ein neues Konsolenanwendungsprojekt. Warum eine Konsolenanwendung? Sie ist einfach und perfekt für Tutorials!

### Aspose.PDF-Referenz hinzufügen

- Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt und wählen Sie „NuGet-Pakete verwalten“ aus.
- Suchen Sie nach „Aspose.PDF“ und installieren Sie es. 
- Dadurch werden Ihrem Projekt alle erforderlichen Pakete hinzugefügt, sodass Sie auf die Funktionen zugreifen können, die wir für die PDF-Bearbeitung benötigen.

### Importieren der erforderlichen Namespaces

Oben in Ihrer Hauptprogrammdatei (wie `Program.cs`), importieren Sie die folgenden Namespaces:

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Durch den Import dieser Pakete weisen Sie Ihre Anwendung an, die von uns genutzten Aspose.PDF-Funktionen einzubinden.

Nachdem wir nun alles eingerichtet haben, erstellen wir Schritt für Schritt unser PDF mit einem getaggten Bild.

## Schritt 1: Initialisieren des Dokuments

Zuerst müssen wir ein neues PDF-Dokument erstellen:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Legen Sie den Pfad zu Ihrem Verzeichnis fest
Document document = new Document();
```

- Was ist hier los? Wir instanziieren ein neues `Document` Objekt, das unser PDF darstellt. Betrachten Sie es als eine leere Leinwand, die auf Ihre Meisterwerke wartet!

## Schritt 2: Einrichten des getaggten Inhalts

Als Nächstes richten wir den getaggten Inhalt ein:

```csharp
ITaggedContent taggedContent = document.TaggedContent;
```

- Warum getaggte Inhalte verwenden? Getaggte PDF-Dateien sind für die Barrierefreiheit unerlässlich, da sie es Bildschirmleseprogrammen ermöglichen, die Struktur des Dokuments zu verstehen.

## Schritt 3: Metadaten konfigurieren

Fügen wir nun einige Metadaten hinzu, die unser PDF beschreiben:

```csharp
taggedContent.SetTitle("CreatePDFwithTaggedImage");
taggedContent.SetLanguage("en-US");
```

- Meta was? Das Hinzufügen eines Titels und einer Sprache ist wie das Anbringen eines Namensschilds an Ihrer Kreation – es hilft anderen zu verstehen, worum es geht!

## Schritt 4: Erstellen Sie ein Illustrationselement

Wir müssen das Element erstellen, das unser Bild enthält:

```csharp
IllustrationElement figure1 = taggedContent.CreateFigureElement();
taggedContent.RootElement.AppendChild(figure1);
```

- Einfach so?! Ja! Die `CreateFigureElement` Mit der Methode können wir eine neue Illustration erstellen und sie an das Stammelement unseres getaggten Inhalts anhängen.

## Schritt 5: Bildeigenschaften festlegen

Als Nächstes legen wir die Eigenschaften für das Bild fest:

```csharp
figure1.AlternativeText = "Aspose Logo";
figure1.Title = "Image 1";
figure1.SetTag("Fig");
```

- Warum all diese Eigenschaften? Alternativtext beschreibt das Bild für diejenigen, die es nicht sehen können, während Titel und Tag das Bild für eine bessere Zugänglichkeit kategorisieren.

## Schritt 6: Bild hinzufügen

Jetzt ist es an der Zeit, das eigentliche Bild zu unserem PDF hinzuzufügen:

```csharp
figure1.SetImage(dataDir + @"aspose-logo.png"); // Stellen Sie sicher, dass Ihr Bildpfad korrekt ist!
```

- Und hier geschieht die Magie! Sie betten das Bild direkt in Ihre PDF-Datei ein. 

## Schritt 7: Speichern Sie das PDF-Dokument

Zum Schluss speichern wir unsere Kreation in einer Datei:

```csharp
document.Save(dataDir + "PDFwithTaggedImage.pdf");
```

- Das große Finale! Nach der Ausführung dieser Zeile finden Sie Ihr neues PDF im angegebenen Verzeichnis.

## Abschluss

Das Erstellen von PDFs mit getaggten Bildern mit Aspose.PDF für .NET ist kinderleicht, wenn Sie es in überschaubare Schritte unterteilen. In dieser Anleitung haben Sie gelernt, nicht nur ein PDF zu erstellen, sondern auch dessen Zugänglichkeit mit getaggten Inhalten zu verbessern. Egal, ob Sie Dokumente für ein breiteres Publikum vorbereiten oder einfach Ihre PDF-Kreationen verfeinern, dieses Wissen wird Ihnen von Nutzen sein.

## Häufig gestellte Fragen

### Was ist ein getaggtes PDF?
Eine getaggte PDF-Datei ist barrierefrei gestaltet. Sie enthält Metadaten, die es unterstützenden Technologien ermöglichen, die PDF-Datei korrekt zu lesen und darin zu navigieren.

### Kann ich mit Aspose.PDF mehrere Bilder hinzufügen?
Absolut! Wiederholen Sie einfach die Schritte zum Erstellen neuer `IllustrationElement` Instanzen in Ihrem Dokument.

### Wo finde ich weitere Dokumentation zu Aspose.PDF?
Schauen Sie sich die Dokumentation an [Hier](https://reference.aspose.com/pdf/net/).

### Gibt es eine kostenlose Testversion für Aspose.PDF?
Ja! Sie können auf eine kostenlose Testversion zugreifen [Hier](https://releases.aspose.com/).

### Wie erhalte ich Support für Aspose.PDF?
Sie erhalten Unterstützung durch den Besuch der [Aspose-Foren](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}