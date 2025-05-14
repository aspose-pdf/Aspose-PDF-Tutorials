---
"description": "Erfahren Sie in dieser detaillierten Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.PDF für .NET eine Tabelle automatisch an das Fenster anpassen. Perfekt für die Erstellung ansprechender und gut angepasster Tabellen in PDFs."
"linktitle": "Automatisch an Fenster anpassen"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Automatisch an Fenster anpassen"
"url": "/de/net/programming-with-tables/auto-fit-to-window/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatisch an Fenster anpassen

## Einführung

Beim Arbeiten mit PDFs arbeitet man häufig mit Tabellen. Manchmal müssen diese perfekt in die Seitenbreite passen. In diesem Tutorial erfahren Sie, wie Sie eine Tabelle mit Aspose.PDF für .NET automatisch an ein Fenster anpassen. So wirken Ihre Tabellen übersichtlich und übersichtlich, und Probleme wie überlaufende oder ungleichmäßige Spalten werden vermieden. Bereit zum Lernen? Los geht’s!

## Voraussetzungen

Bevor wir mit der Schritt-für-Schritt-Anleitung beginnen, benötigen Sie einige Dinge:

1. Aspose.PDF für .NET in Ihrem Projekt installiert. Wenn Sie es noch nicht haben, können Sie [Laden Sie es hier herunter](https://releases.aspose.com/pdf/net/) oder erkunden Sie ihre [kostenlose Testversion](https://releases.aspose.com/).
2. Grundlegende Kenntnisse der .NET-Programmierung.
3. Visual Studio oder eine andere .NET-unterstützte IDE, die auf Ihrem System installiert ist.

> PS: Vergessen Sie nicht, dass Sie eine Lizenz benötigen, um Aspose.PDF uneingeschränkt nutzen zu können. Sie können entweder eine kaufen [Hier](https://purchase.aspose.com/buy) oder erhalten Sie eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) um alle Funktionen auszuprobieren.

## Pakete importieren

Bevor Sie in den Code eintauchen, müssen Sie die erforderlichen Namespaces importieren:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Nachdem wir nun alles vorbereitet haben, wollen wir dies in einfache, leicht verständliche Schritte aufteilen, um zu verstehen, wie Sie mit Aspose.PDF für .NET eine Tabelle automatisch an ein Fenster anpassen können.

## Schritt 1: Initialisieren des Dokumentobjekts

Zunächst müssen Sie ein PDF-Dokument erstellen. Stellen Sie sich dieses Dokument als leeres Blatt vor, auf dem Sie Seiten und Tabellen hinzufügen.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Instanziieren Sie das PDF-Objekt, indem Sie seinen leeren Konstruktor aufrufen
Document doc = new Document();
```
  
Hier erstellen wir ein neues Dokument mit dem `Document` Klasse von Aspose.PDF. Die `dataDir` ist der Speicherort, an dem Ihre PDF-Datei gespeichert wird, wenn Sie fertig sind.

## Schritt 2: Dem Dokument eine Seite hinzufügen

Ein PDF-Dokument benötigt Seiten, oder? Fügen wir eine hinzu.

```csharp
// Erstellen Sie einen Abschnitt (Seite) im PDF-Objekt
Page sec1 = doc.Pages.Add();
```
  
Wir haben dem Dokument eine neue Seite hinzugefügt, indem wir `Pages.Add()` Methode. Sie können sich das so vorstellen, als würden Sie Ihrem Dokument ein neues Blatt hinzufügen, in dem Sie die Tabelle platzieren.

## Schritt 3: Erstellen und Konfigurieren einer Tabelle

Jetzt ist es an der Zeit, eine Tabelle zu erstellen und sie so anzupassen, dass sie in das Fenster passt.

```csharp
// Instanziieren eines Tabellenobjekts
Aspose.Pdf.Table tab1 = new Aspose.Pdf.Table();
// Fügen Sie die Tabelle in die Absatzsammlung des gewünschten Abschnitts ein
sec1.Paragraphs.Add(tab1);
```
  
Wir initialisierten ein neues `Table` Objekt und fügte es der Absatzsammlung der Seite hinzu. Jede PDF-Seite kann unterschiedliche Absätze enthalten, und hier behandeln wir die Tabelle als Absatz.

## Schritt 4: Spaltenbreiten definieren und automatisch an Fenster anpassen

Als nächstes legen wir die Spaltenbreiten fest und sorgen dafür, dass sich die Tabelle an das Fenster anpasst.

```csharp
// Spaltenbreiten für die Tabelle festlegen
tab1.ColumnWidths = "50 50 50";
tab1.ColumnAdjustment = ColumnAdjustment.AutoFitToWindow;
```
  
Wir haben feste Spaltenbreiten für die Tabelle festgelegt, aber auch hinzugefügt `ColumnAdjustment.AutoFitToWindow`, wodurch sichergestellt wird, dass die Tabelle ihre Größe an das verfügbare Fenster anpasst.

## Schritt 5: Rahmen und Ränder für die Tabelle und die Zellen festlegen

Tabellen ohne Rahmen sind oft unleserlich. Definieren wir Rahmen und Ränder, damit die Tabellen übersichtlich aussehen.

```csharp
// Legen Sie den Standardzellenrahmen mit dem BorderInfo-Objekt fest
tab1.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);

// Festlegen des Tabellenrahmens mithilfe eines anderen benutzerdefinierten BorderInfo-Objekts
tab1.Border = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 1F);

// Erstellen Sie ein MarginInfo-Objekt und legen Sie dessen linken, unteren, rechten und oberen Rand fest
Aspose.Pdf.MarginInfo margin = new Aspose.Pdf.MarginInfo();
margin.Top = 5f;
margin.Left = 5f;
margin.Right = 5f;
margin.Bottom = 5f;

// Legen Sie die Standardzellenfüllung auf das MarginInfo-Objekt fest
tab1.DefaultCellPadding = margin;
```
  
Rahmen werden sowohl der Tabelle als auch den Zellen hinzugefügt, indem Sie `BorderInfo` Klasse, in der Sie die Dicke definieren. Ränder werden festgelegt, um den Zellen etwas Platz zum Auffüllen zu geben.

## Schritt 6: Zeilen und Zellen zur Tabelle hinzufügen

Eine Tabelle ohne Inhalt? Das ist nicht gut! Fügen wir Zeilen und Zellen hinzu.

```csharp
// Erstellen Sie Zeilen in der Tabelle und dann Zellen in den Zeilen
Aspose.Pdf.Row row1 = tab1.Rows.Add();
row1.Cells.Add("col1");
row1.Cells.Add("col2");
row1.Cells.Add("col3");

Aspose.Pdf.Row row2 = tab1.Rows.Add();
row2.Cells.Add("item1");
row2.Cells.Add("item2");
row2.Cells.Add("item3");
```
  
Wir erstellen zwei Zeilen und fügen jeder Zeile drei Zellen hinzu. Hier geben Sie Ihre eigentlichen Daten ein (von Zeichenfolgen bis hin zu komplexeren Elementen).

## Schritt 7: Speichern Sie das Dokument

Sobald alles eingestellt ist, möchten Sie Ihr neu erstelltes PDF-Dokument speichern.

```csharp
dataDir = dataDir + "AutoFitToWindow_out.pdf";
// Aktualisiertes Dokument mit Tabellenobjekt speichern
doc.Save(dataDir);
```
  
Der `doc.Save()` Die Methode speichert das PDF im angegebenen Verzeichnis. In diesem Fall wird das Dokument gespeichert als `AutoFitToWindow_out.pdf` in Ihrem definierten Verzeichnis.

## Abschluss

Und da haben Sie es! Sie haben gerade eine Tabelle erstellt, die mit Aspose.PDF für .NET automatisch in das Fenster passt. Dies sorgt nicht nur für ein professionelles und ansprechendes Aussehen Ihrer Tabelle, sondern bietet Ihnen auch Flexibilität bei der Arbeit mit unterschiedlichen Datengrößen. Egal, ob Sie Berichte, Rechnungen oder andere Dokumente mit Tabellen erstellen – diese Methode ist eine hervorragende Möglichkeit, übersichtliche und lesbare Layouts zu erhalten.

## Häufig gestellte Fragen

### Kann ich dynamisch weitere Zeilen hinzufügen?  
Ja, Sie können weiterhin Zeilen hinzufügen, indem Sie `tab1.Rows.Add()` Methode, dynamisch basierend auf dem Inhalt.

### Wie passe ich die Tabelle an, wenn ich keine automatische Anpassung möchte?  
Sie können die `ColumnWidths` ohne Verwendung `ColumnAdjustment.AutoFitToWindow` um eine feste Tabellenbreite beizubehalten.

### Kann ich Bilder oder andere Inhalte in die Zellen einfügen?  
Ja, mit Aspose.PDF können Sie Bilder, Text und sogar andere Tabellen in Zellen einfügen!

### Was ist, wenn ich komplexere Tabellenstile benötige?  
Sie können die Tabellen- und Zellenstile weiter anpassen, indem Sie Eigenschaften wie Hintergrundfarbe, Textausrichtung und Schriftarteinstellungen verwenden.

### Ist es möglich, diese Tabelle in andere Formate als PDF zu exportieren?  
Absolut! Aspose.PDF unterstützt den Export in verschiedene Formate wie HTML, DOCX und mehr.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}