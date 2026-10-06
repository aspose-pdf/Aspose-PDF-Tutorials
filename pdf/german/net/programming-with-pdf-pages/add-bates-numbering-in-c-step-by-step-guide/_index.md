---
category: general
date: 2026-03-27
description: Bates-Nummerierung in C# schnell hinzufügen. Erfahren Sie, wie Sie benutzerdefinierte
  Seitenzahlen, fortlaufende Seitenzahlen und benutzerdefinierte Nummern zu Word‑Dokumenten
  hinzufügen.
draft: false
keywords:
- add bates numbering
- how to add bates
- add custom page numbers
- add sequential page numbers
- add custom numbers
language: de
og_description: Fügen Sie Bates-Nummerierung in C# mit einem klaren Beispiel hinzu.
  Dieser Leitfaden zeigt, wie man benutzerdefinierte Seitenzahlen, sequentielle Seitenzahlen
  und mehr hinzufügt.
og_title: Bates‑Nummerierung in C# hinzufügen – Vollständiges Tutorial
tags:
- C#
- Document Processing
- Bates Numbering
title: Bates-Nummerierung in C# hinzufügen – Schritt‑für‑Schritt‑Anleitung
url: /de/net/programming-with-pdf-pages/add-bates-numbering-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates‑Nummerierung in C# hinzufügen – Schritt‑für‑Schritt‑Anleitung

Haben Sie sich schon einmal gefragt, wie man **Bates‑Nummerierung** zu einem Word‑Dokument hinzufügt, ohne sich die Haare zu raufen? Sie sind nicht allein. In vielen juristischen oder Compliance‑Projekten muss jede Seite eine eindeutige Kennung erhalten, und das manuell zu erledigen ist ein Albtraum.  

In diesem Tutorial gehen wir ein komplettes, ausführbares Beispiel durch, das **Bates‑Nummerierung hinzufügt**, Ihnen **zeigt, wie man Bates** in wenigen Zeilen einbaut, und sogar erklärt, wie man **benutzerdefinierte Seitenzahlen** und **sequenzielle Seitenzahlen** hinzufügt, wenn Sie sie benötigen. Am Ende haben Sie eine .docx‑Datei, die mit den von Ihnen gewählten Zahlen versehen ist – ohne Drittanbieter‑Tools.

## Was Sie lernen werden

- Laden einer DOCX‑Datei mit der Aspose.Words for .NET API (oder einer kompatiblen Bibliothek).  
- Konfigurieren von **benutzerdefinierten Zahlen** wie Präfix, Startwert und Schriftgröße.  
- Anwenden der Nummerierung auf jede Seite mit einem einzigen Aufruf.  
- Speichern des Ergebnisses und Überprüfen, dass die Zahlen wie erwartet erscheinen.  

Vorkenntnisse zur Bates‑Nummerierung sind nicht nötig; ein einfaches C#‑Setup und eine Kopie des Quelldokuments reichen. Lassen Sie uns loslegen.

## Voraussetzungen

- .NET 6+ (der Code funktioniert sowohl unter .NET Core als auch .NET Framework).  
- Aspose.Words for .NET, installiert via NuGet (`Install-Package Aspose.Words`).  
- Ein Word‑Dokument namens `input.docx` in einem Ordner, den Sie referenzieren können (`YOUR_DIRECTORY`).  
- Visual Studio, VS Code oder irgendeine C#‑IDE Ihrer Wahl.

> **Profi‑Tipp:** Wenn Sie eine andere Bibliothek verwenden (z. B. Open XML SDK), bleiben die Konzepte gleich – Sie müssen nur die API‑Aufrufe austauschen.

## Schritt 1: Quell‑Dokument laden

Zuerst müssen wir die Word‑Datei in den Speicher laden.

```csharp
using Aspose.Words;

// Step 1: Load the source document
Document document = new Document("YOUR_DIRECTORY/input.docx");
```

*Warum das wichtig ist:* Das Laden der Datei erzeugt ein `Document`‑Objekt, das Ihnen Zugriff auf Seiten, Abschnitte und den Low‑Level‑Knotenbaum gibt. Ohne dieses Objekt können Sie keine Nummerierung anhängen.

## Schritt 2: Optionen für die Bates‑Nummerierung konfigurieren

Jetzt definieren wir genau, wie die Zahlen aussehen sollen. Hier fügen Sie **benutzerdefinierte Seitenzahlen** oder **sequenzielle Seitenzahlen** hinzu.

```csharp
// Step 2: Define Bates numbering options (prefix, start number, font size)
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Prefix that appears before every number, e.g., "ABC"
    Prefix = "ABC",
    // The first number in the sequence; change to 1 if you prefer
    Start = 1000,
    // Font size in points; 9 works well for most legal docs
    FontSize = 9
};
```

*Warum das wichtig ist:* Der `Prefix` ermöglicht es Ihnen, **benutzerdefinierte Zahlen** wie eine Fall‑ID hinzuzufügen, während `Start` den Anfangszähler bestimmt. Durch Ändern von `FontSize` stellen Sie sicher, dass die Zahlen nicht in die Seitenränder hineinragen.

## Schritt 3: Bates‑Nummerierung auf jede Seite anwenden

Mit den konfigurierten Optionen sagen wir der Bibliothek, dass sie jede Seite versehen soll.

```csharp
// Step 3: Apply Bates numbering to all pages of the document
document.Pages.AddBatesNumbering(batesOptions);
```

*Warum das wichtig ist:* Die Methode `AddBatesNumbering` durchläuft die interne Seitensammlung und fügt in der rechten unteren Ecke (Standardposition) ein Textfeld ein. Das ist das Kernstück **wie man Bates hinzufügt**, ohne selbst eine Schleife zu schreiben.

## Schritt 4: Das aktualisierte Dokument speichern

Abschließend schreiben wir die geänderte Datei zurück auf die Festplatte.

```csharp
// Step 4: Save the updated document
document.Save("YOUR_DIRECTORY/output.docx");
```

*Warum das wichtig ist:* Beim Speichern entsteht ein neues `output.docx`, das Sie in Word, LibreOffice oder einem anderen Viewer öffnen können, um zu bestätigen, dass die Zahlen erscheinen.

## Erwartetes Ergebnis

Öffnen Sie `output.docx`. Jede Seite sollte etwa Folgendes anzeigen:

```
ABC‑1000   (on page 1)
ABC‑1001   (on page 2)
ABC‑1002   (on page 3)
...
```

Wenn Sie die Druckvorschau des Dokuments öffnen, sehen Sie die Zahlen in der rechten unteren Ecke, mit der von Ihnen festgelegten Schriftgröße.

## Randfälle & Variationen

| Situation | Was zu ändern | Warum |
|-----------|----------------|-----|
| **Kein Präfix nötig** | `Prefix = string.Empty` | Entfernt den „ABC‑“-Teil und lässt nur die numerische Sequenz stehen. |
| **Start bei 1** | `Start = 1` | Praktisch für einfaches **sequenzielles Seitenzahlen‑Hinzufügen** ohne benutzerdefinierten Präfix. |
| **Große Dokumente (>10.000 Seiten)** | `FontSize` erhöhen oder `Location` anpassen (überladene Varianten von `AddBatesNumbering` verwenden) | Verhindert Überlappungen mit Fuß- oder Kopfzeilen. |
| **Schreibgeschützte Quelldatei** | Mit `LoadOptions` öffnen, die Schreibzugriff erlauben, oder die Datei zuerst kopieren | Sonst wirft `document.Save` eine Ausnahme. |
| **Andere Platzierung** | `batesOptions.Position = BatesNumberingPosition.TopLeft` (oder ein anderer Enum‑Wert) | Einige Firmen verlangen die Nummern oben auf der Seite. |

> **Hinweis:** Nicht alle Bibliotheken stellen eine `BatesNumberingOptions`‑Klasse bereit. Mit dem Open XML SDK würden Sie ein `TextBox`‑Element manuell einfügen – dasselbe Prinzip, mehr Code.

## Vollständiges funktionierendes Beispiel

Hier ist das gesamte Programm an einem Ort. Kopieren Sie es in eine Konsolen‑App und führen Sie es aus.

```csharp
using System;
using Aspose.Words;

class Program
{
    static void Main()
    {
        // Load the source document
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Define Bates numbering options
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",      // custom prefix
            Start = 1000,        // starting number
            FontSize = 9         // font size in points
        };

        // Apply numbering to every page
        document.Pages.AddBatesNumbering(batesOptions);

        // Save the result
        document.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Starten Sie das Programm, öffnen Sie `output.docx` und Sie sehen die Nummerierung genau dort, wo Sie sie erwartet haben. 🎉

## Häufig gestellte Fragen

**F: Kann ich die Farbe der Zahlen ändern?**  
A: Ja. Nach dem Aufruf von `AddBatesNumbering` können Sie die erzeugten `Shape`‑Objekte abrufen und deren `FillColor`‑Eigenschaft setzen.

**F: Was, wenn ich die Zahlen lieber links statt rechts haben möchte?**  
A: Verwenden Sie `batesOptions.Position = BatesNumberingPosition.BottomLeft` (oder `TopLeft`, `TopRight`). Die API unterstützt alle vier Ecken.

**F: Funktioniert das auch mit PDF‑Ausgabe?**  
A: Absolut. Nachdem Sie die Nummerierung hinzugefügt haben, rufen Sie `document.Save("output.pdf")` auf. Die Zahlen werden in das PDF gerendert, genau wie in Word.

## Fazit

Sie wissen jetzt, **wie man Bates‑Nummerierung** zu einer Word‑Datei mit C# hinzufügt. Das Tutorial behandelte das Laden eines Dokuments, das Konfigurieren von **benutzerdefinierten Zahlen**, das Anwenden von **sequenziellen Seitenzahlen** und das Speichern des Endergebnisses. Mit dem vollständigen Code‑Beispiel können Sie das in jedes Projekt einbinden und sofort Dokumente kennzeichnen.

Bereit für die nächste Herausforderung? Kombinieren Sie das mit einem Batch‑Prozessor, der einen Ordner mit Dateien durchläuft, oder erkunden Sie **benutzerdefinierte Seitenzahlen** in Kopf‑ bzw. Fußzeile für ein noch professionelleres Ergebnis. So oder so haben Sie eine solide Basis für jede Legal‑Tech‑ oder Compliance‑Automatisierungsaufgabe.

Haben Sie Fragen oder ein cooles Anwendungsbeispiel? Hinterlassen Sie unten einen Kommentar und happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}