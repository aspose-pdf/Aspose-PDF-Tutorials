---
"description": "Erfahren Sie in diesem Schritt-für-Schritt-Tutorial mit einem ausführlichen Codebeispiel, wie Sie mit Aspose.PDF für .NET Text aus einer Stempelanmerkung in PDF extrahieren."
"linktitle": "Text aus Stempelanmerkung extrahieren"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Text aus Stempelanmerkung extrahieren"
"url": "/de/net/programming-with-stamps-and-watermarks/extract-text-from-stamp-annotation/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Stempelanmerkung extrahieren

## Einführung

Beim Arbeiten mit PDF-Dateien kann das Extrahieren bestimmter Daten, wie z. B. Text aus Anmerkungen, sehr praktisch sein. In diesem Tutorial zeigen wir Ihnen Schritt für Schritt, wie Sie mit Aspose.PDF für .NET Text aus einer Stempelanmerkung in einem PDF-Dokument extrahieren. Diese leistungsstarke Bibliothek ermöglicht Entwicklern die Bearbeitung von PDF-Dateien und ermöglicht Aufgaben wie Textextraktion, Anmerkungsverwaltung und vieles mehr. Lassen Sie uns in die Details eintauchen und alles aufschlüsseln!

## Voraussetzungen

Bevor wir mit dem Tutorial beginnen, benötigen Sie einige Dinge:

- Aspose.PDF für .NET: Sie müssen Aspose.PDF für .NET installiert haben. Sie können [Laden Sie hier die neueste Version herunter](https://releases.aspose.com/pdf/net/).
- Visual Studio: In dieser Anleitung wird davon ausgegangen, dass Sie Visual Studio als integrierte Entwicklungsumgebung (IDE) verwenden.
- Grundkenntnisse in C#: Sie sollten über grundlegende Kenntnisse der C#-Programmierung verfügen.

Stellen Sie sicher, dass Sie diese Tools eingerichtet haben, damit Sie dem Tutorial folgen können.

## Pakete importieren

Der erste Schritt in jedem .NET-Projekt ist der Import der erforderlichen Namespaces. Mit Aspose.PDF benötigen Sie für den Einstieg nur wenige wichtige Importe:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

Diese Importe bringen die erforderliche Funktionalität für die Arbeit mit PDF-Dokumenten, Anmerkungen und Textextraktion mit.

Lassen Sie uns den Prozess zum Extrahieren von Text aus einer Stempelanmerkung durchgehen. Dazu müssen Sie ein PDF-Dokument laden, die Stempelanmerkung identifizieren und den Textinhalt extrahieren.

## Schritt 1: Laden Sie das PDF-Dokument

Als Erstes müssen Sie die PDF-Datei mit dem Stempelanmerkungstext laden. In diesem Beispiel laden wir eine Beispiel-PDF-Datei aus Ihrem lokalen Verzeichnis.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "test.pdf");
```

Hier verwenden wir die `Document` Klasse von Aspose.PDF zum Öffnen und Interagieren mit der PDF-Datei. Die `dataDir` Variable stellt den Pfad zu Ihrer Datei dar. Ersetzen `"YOUR DOCUMENT DIRECTORY"` durch den tatsächlichen Pfad, in dem Ihr PDF gespeichert ist.

## Schritt 2: Identifizieren Sie die Stempelanmerkung

PDF-Anmerkungen werden anhand ihres Typs und ihrer Position im Dokument identifiziert. In unserem Fall möchten wir eine Stempelanmerkung auf einer bestimmten Seite finden. So geht's:

```csharp
StampAnnotation annot = doc.Pages[1].Annotations[3] as StampAnnotation;
```

In dieser Codezeile:
- `doc.Pages[1]`: Greift auf die erste Seite des Dokuments zu.
- `Annotations[3]`: Bezieht sich auf die vierte Anmerkung auf der Seite (da die Indizierung bei 0 beginnt).
- `as StampAnnotation`: Wandelt die Anmerkung in eine `StampAnnotation` Objekt, das ist der spezifische Typ von Anmerkung, mit dem wir es zu tun haben.

## Schritt 3: Erstellen Sie einen Textabsorber

Um Text aus der Stempelanmerkung zu extrahieren, benötigen wir einen Textabsorber. Dieses Tool hilft uns, den Text aus einem bestimmten Bereich der PDF-Datei, in diesem Fall der Anmerkung, zu absorbieren oder zu erfassen.

```csharp
TextAbsorber ta = new TextAbsorber();
```

Der `TextAbsorber` Die Klasse ist für das Extrahieren von Text aus jedem beliebigen Teil des Dokuments konzipiert und wir werden sie verwenden, um das Erscheinungsbild der Anmerkung gezielt zu gestalten.

## Schritt 4: Extrahieren des Erscheinungsbilds der Stempelanmerkung

Stempelanmerkungen in PDF-Dateien haben ein zugehöriges Erscheinungsbild, das üblicherweise in Form eines XForms gespeichert ist. Wir müssen dieses Erscheinungsbild abrufen, um auf den eigentlichen Text im Stempel zugreifen zu können.

```csharp
XForm ap = annot.Appearance["N"];
```

Hier:
- `annot.Appearance["N"]`: Ruft den Erscheinungsstream mit dem Namen „N“ ab (der das normale Erscheinungsbild der Anmerkung darstellt).

## Schritt 5: Extrahieren des Textinhalts

Nun, da wir das Aussehen haben, können wir die `TextAbsorber` um das Erscheinungsbild zu besuchen und den Text zu erfassen.

```csharp
ta.Visit(ap);
```

Der `Visit` Methode ermöglicht die `TextAbsorber` um das Erscheinungsbild zu analysieren und darin eingebettete Textinhalte zu extrahieren.

## Schritt 6: Den extrahierten Text anzeigen

Sobald der Text extrahiert ist, können wir ihn schließlich an die Konsole ausgeben oder zur weiteren Verwendung speichern.

```csharp
Console.WriteLine(ta.Text);
```

Diese einfache Codezeile zeigt den extrahierten Text im Konsolenfenster an. Sie können ihn auch in einer Datei speichern oder je nach Bedarf weiter bearbeiten.

## Abschluss

Die Arbeit mit Anmerkungen in PDF-Dokumenten, insbesondere mit Stempelanmerkungen, kann die Funktionalität Ihrer Anwendungen erheblich erweitern. Mit Aspose.PDF für .NET verfügen Sie über ein robustes Toolset, das Ihnen das Extrahieren von Daten, die Bearbeitung von Anmerkungen und die sinnvolle Interaktion mit PDFs erleichtert. In diesem Tutorial haben wir Ihnen gezeigt, wie Sie in wenigen einfachen Schritten Text aus einer Stempelanmerkung extrahieren. Jetzt sind Sie an der Reihe, diese Funktionen in Ihren Projekten auszuprobieren!

## Häufig gestellte Fragen

### Kann ich mit Aspose.PDF Text aus anderen Arten von Anmerkungen extrahieren?  
Ja, mit Aspose.PDF können Sie Text aus verschiedenen Arten von Anmerkungen extrahieren, z. B. Textanmerkungen, Freitextanmerkungen und mehr, nicht nur Stempelanmerkungen.

### Unterstützt Aspose.PDF das Hinzufügen benutzerdefinierter Anmerkungen?  
Absolut! Aspose.PDF unterstützt das Erstellen und Hinzufügen benutzerdefinierter Anmerkungen zu PDF-Dokumenten und bietet Ihnen Flexibilität bei der Verwaltung und Präsentation von Daten.

### Kann ich Bilder aus Stempelanmerkungen extrahieren?  
Ja, Sie können mit ähnlichen Methoden Bilder aus Stempelanmerkungen extrahieren, indem Sie auf das Erscheinungsbild zugreifen und Bilddaten abrufen.

### Welche weiteren Funktionen bietet Aspose.PDF für .NET?  
Aspose.PDF für .NET bietet eine breite Palette an Funktionen, darunter Textbearbeitung, Formularfeldverarbeitung, Dokumentkonvertierung und vieles mehr.

### Ist Aspose.PDF für .NET kostenlos?  
Aspose.PDF für .NET bietet eine kostenlose Testversion an. Um jedoch alle Funktionen nutzen zu können, müssen Sie eine Lizenz erwerben. Sie können auch eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}