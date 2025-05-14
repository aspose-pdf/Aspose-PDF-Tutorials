---
"date": "2025-04-10"
"description": "Erfahren Sie, wie Sie PDFs mit Aspose.PDF für .NET in HTML konvertieren und dabei Schriftarten im TrueType-Format (TTF) und Web Open Font Format (WOFF) beibehalten. Schritt-für-Schritt-Anleitung mit Codebeispielen."
"title": "Konvertieren Sie PDF in HTML mit Aspose.PDF für .NET. Bewahren Sie Schriftarten in den Formaten TTF und WOFF auf."
"url": "/de/net/conversion-export/convert-pdf-html-aspose-net-truetype-woff/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Konvertieren Sie PDF in HTML mit Aspose.PDF für .NET: Bewahren Sie Schriftarten in den Formaten TTF und WOFF auf

## Einführung
Haben Sie Probleme, das ursprüngliche Layout und die Schriftintegrität Ihrer PDF-Dokumente bei der Konvertierung in HTML beizubehalten? Die Konvertierung von PDFs unter Beibehaltung der Schriftarten kann eine Herausforderung sein, muss es aber nicht. Mit **Aspose.PDF für .NET**Mit konvertieren Sie PDF-Dateien mühelos ins HTML-Format und stellen dabei sicher, dass die Schriftarten im TrueType-Format (TTF) oder Web Open Font Format (WOFF) erhalten bleiben. Diese Anleitung führt Sie Schritt für Schritt durch den Vorgang.

In diesem Tutorial behandeln wir:
- So speichern Sie Schriftarten als TTF beim Konvertieren von PDFs in HTML
- Konfigurieren Ihrer Konvertierung zum Speichern von Schriftarten als WOFF
- Speichern von Schriftarten in allen Formaten während der Konvertierung

Am Ende dieses Artikels verfügen Sie über umfassende Kenntnisse zur Verwendung von Aspose.PDF für .NET zur effektiven Verwaltung von Schriftkonvertierungen. Lassen Sie uns zunächst die erforderlichen Voraussetzungen erläutern.

## Voraussetzungen
Bevor Sie mit der Konvertierung von PDFs in HTML mit Aspose.PDF beginnen, stellen Sie sicher, dass Sie die folgenden Anforderungen erfüllen:

### Erforderliche Bibliotheken und Abhängigkeiten
- **Aspose.PDF für .NET**: Diese Bibliothek ist für die Verarbeitung von PDF-Dateien in .NET-Anwendungen unerlässlich.
- **.NET Framework oder .NET Core/5+**: Stellen Sie sicher, dass Ihre Entwicklungsumgebung diese Frameworks unterstützt.

### Anforderungen für die Umgebungseinrichtung
Stellen Sie sicher, dass Ihre Entwicklungsumgebung (z. B. Visual Studio) für die Verwendung mit der Aspose.PDF-Bibliothek eingerichtet ist. Sie benötigen:
- Ein Projekt, das entweder im .NET Framework oder in .NET Core/5+ erstellt wurde
- Zugriff auf den NuGet-Paketmanager zum Installieren von Bibliotheken

### Voraussetzungen
Grundkenntnisse in C# und Vertrautheit mit der Dateiverwaltung in .NET sind von Vorteil.

## Einrichten von Aspose.PDF für .NET
Um zu beginnen, müssen Sie die Aspose.PDF-Bibliothek installieren. Dies können Sie über verschiedene Paketmanager tun:

**.NET-CLI:**
```bash
dotnet add package Aspose.PDF
```

**Paketmanager-Konsole:**
```powershell
Install-Package Aspose.PDF
```

**NuGet-Paket-Manager-Benutzeroberfläche:**
Suchen Sie nach „Aspose.PDF“ und installieren Sie die neueste Version.

### Lizenzerwerb
Sie können eine temporäre Lizenz oder eine Volllizenz von Aspose erwerben. Mit der kostenlosen Testversion können Sie alle Funktionen uneingeschränkt nutzen und sich somit ideal für erste Evaluierungen eignen. So richten Sie Ihre Umgebung mit einer Lizenz ein:
1. Fordern Sie eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).
2. Wenden Sie die Lizenz in Ihrer Anwendung mithilfe des folgenden Codeausschnitts an, bevor Sie irgendwelche Vorgänge ausführen:

```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to your License File");
```

## Implementierungshandbuch
Lassen Sie uns die Implementierung in drei Hauptfunktionen aufteilen: Speichern von Schriftarten als TTF, WOFF und alle Formate.

### Schriftarten als TTF speichern
**Überblick**
Mit dieser Funktion können Sie Schriftarten aus einem PDF-Dokument im TrueType-Format (TTF) speichern, während Sie es in HTML konvertieren. Dadurch wird sichergestellt, dass die visuelle Integrität Ihrer Schriftarten bei der Konvertierung erhalten bleibt.

#### Schrittweise Implementierung
1. **Dokument und Optionen initialisieren:**
   Beginnen Sie mit dem Laden Ihres PDF-Dokuments mit Aspose.PDF's `Document` Klasse und Aufbau `HtmlSaveOptions`.

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   string outFile = Path.GetFullPath(dataDir + "/36192_out.html");
   Document doc = new Document(dataDir + "/input.pdf");

   HtmlSaveOptions saveOptions = new HtmlSaveOptions();
   ```

2. **Speicheroptionen konfigurieren:**
   Legen Sie die erforderlichen Optionen fest, um das Layout beizubehalten und den Schriftartenspeichermodus festzulegen.

   ```csharp
   saveOptions.FixedLayout = true; // Behalten Sie das ursprüngliche PDF-Layout bei
   saveOptions.SplitIntoPages = false; // Nicht in mehrere HTML-Dateien aufteilen
   saveOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.AlwaysSaveAsTTF;
   ```

3. **Ausgabeverzeichnis vorbereiten:**
   Stellen Sie sicher, dass das Ausgabeverzeichnis zum Speichern verknüpfter Schriftartdateien bereit ist.

   ```csharp
   string linkedFilesFolder = Path.GetDirectoryName(outFile) + "/36192_files";
   if (Directory.Exists(linkedFilesFolder))
   {
       Directory.Delete(linkedFilesFolder, true); // Vorhandene Dateien löschen
   }
   ```

4. **Speichern Sie das Dokument:**
   Speichern Sie abschließend Ihr Dokument mit den angegebenen Optionen.

   ```csharp
doc.Save(outFile, saveOptions);
```

### Save Fonts as WOFF
**Overview**
Configuring Aspose.PDF to save fonts in Web Open Font Format (WOFF) is beneficial for web optimization, reducing font file sizes while maintaining quality.

#### Step-by-Step Implementation
1. **Configure Save Options:**
   Initialize `HtmlSaveOptions` and set the font saving mode to WOFF.

   ```csharp
   HtmlSaveOptions woffSaveOptions = new HtmlSaveOptions();
   woffSaveOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.AlwaysSaveAsWOFF;
   ```

2. **Speicheroptionen anwenden:**
   Verwenden Sie diese Optionen beim Speichern Ihres Dokuments, ähnlich wie bei der TTF-Methode.

### Speichern Sie Schriftarten in allen Formaten
**Überblick**
Um maximale Kompatibilität und Flexibilität zu gewährleisten, möchten Sie möglicherweise Schriftarten während der Konvertierung in allen verfügbaren Formaten speichern.

#### Schrittweise Implementierung
1. **Dokument und Optionen initialisieren:**
   Laden Sie das PDF-Dokument und konfigurieren Sie `HtmlSaveOptions`.

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   Document doc = new Document(dataDir + "/input.pdf");
   HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
   ```

2. **Speicheroptionen konfigurieren:**
   Legen Sie Optionen fest, um alle Schriftformate zu speichern und das Layout beizubehalten.

   ```csharp
   htmlOptions.FixedLayout = true;
   htmlOptions.RasterImagesSavingMode = HtmlSaveOptions.RasterImagesSavingModes.AsExternalPngFilesReferencedViaSvg;
   htmlOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.SaveInAllFormats;
   ```

3. **Speichern Sie das Dokument:**
   Speichern Sie Ihr Dokument mit diesen Einstellungen.

   ```csharp
doc.Save(dataDir + "/ThreeSetFonts_out.html", htmlOptions);
```

## Practical Applications
Converting PDFs to HTML with font preservation has numerous real-world applications:
1. **Web Publishing**: Ensure that documents retain their original styling when published online.
2. **Content Portability**: Easily move content between desktop and web environments without loss of formatting.
3. **Document Archiving**: Maintain document integrity during long-term storage or migration.

Integration possibilities include embedding these conversions into CMS systems, automated reporting tools, or digital libraries for seamless font management across platforms.

## Performance Considerations
When using Aspose.PDF for .NET, consider the following tips to optimize performance:
- **Memory Management**: Dispose of objects properly and utilize `using` statements where applicable.
- **Batch Processing**: Process documents in batches if dealing with large volumes to prevent memory overflow.
- **Resource Optimization**: Configure options like image compression and font subsetting to reduce file sizes.

## Conclusion
We've explored how to convert PDFs to HTML while preserving fonts using Aspose.PDF for .NET. Whether saving fonts as TTF, WOFF, or all formats, these techniques ensure your documents maintain their original design and readability in web environments. 

For further exploration, consider diving into Aspose's extensive documentation or experimenting with additional conversion features offered by the library.

## FAQ Section
1. **What are the benefits of converting PDFs to HTML using Aspose.PDF?**
   - Maintains document layout and font integrity.
   - Facilitates web publishing and content portability.
2. **Can I convert large PDF files efficiently with Aspose.PDF?**
   - Yes, by optimizing memory usage and processing in batches.
3. **How do I handle licensing for Aspose.PDF?**
   - Obtain a temporary or full license from the [Aspose website](https://purchase.aspose.com/buy).
4. **Is it possible to customize font settings during conversion?**
   - Yes, through various `HtmlSaveOptions`.
5. **What are some common issues when converting PDFs and how can I address them?**
   - Common issues include missing fonts or layout discrepancies. Adjusting save options and ensuring proper licensing can help mitigate these problems.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}