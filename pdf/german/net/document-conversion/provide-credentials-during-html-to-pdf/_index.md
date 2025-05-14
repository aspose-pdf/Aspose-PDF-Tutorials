---
"description": "Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.PDF für .NET HTML in PDF konvertieren. Perfekt für Entwickler, die die Dokumenterstellung optimieren möchten."
"linktitle": "Geben Sie beim Konvertieren von HTML in PDF Anmeldeinformationen an"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Geben Sie beim Konvertieren von HTML in PDF Anmeldeinformationen an"
"url": "/de/net/document-conversion/provide-credentials-during-html-to-pdf/"
"weight": 240
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Geben Sie beim Konvertieren von HTML in PDF Anmeldeinformationen an

## Einführung

In der Softwareentwicklung ist die Konvertierung von HTML in PDF eine gängige Anforderung. Ob Sie Berichte, Rechnungen oder andere Dokumente erstellen – eine zuverlässige Bibliothek für diese Aufgabe spart Ihnen viel Zeit und Mühe. Aspose.PDF für .NET ist eine leistungsstarke Bibliothek, mit der Entwickler PDF-Dokumente mühelos erstellen, bearbeiten und konvertieren können. In diesem Tutorial führen wir Sie durch die Konvertierung von HTML in PDF mit Aspose.PDF und stellen Ihnen gleichzeitig die Anmeldeinformationen für den sicheren Zugriff bereit. Also, schnappen Sie sich Ihren Programmierhut und legen Sie los!

## Voraussetzungen

Bevor wir beginnen, müssen Sie einige Dinge vorbereitet haben:

1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist. Dies wird unsere Entwicklungsumgebung sein.
2. Aspose.PDF für .NET: Sie können die Bibliothek von der [Webseite](https://releases.aspose.com/pdf/net/)Wenn Sie es erst einmal ausprobieren möchten, können Sie auch eine [kostenlose Testversion](https://releases.aspose.com/).
3. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie die Beispiele besser verstehen.
4. Internetzugang: Da wir HTML-Inhalte von einer URL abrufen, stellen Sie sicher, dass Sie über eine aktive Internetverbindung verfügen.

## Pakete importieren

Um mit Aspose.PDF zu beginnen, müssen Sie die erforderlichen Pakete in Ihr Projekt importieren. So geht's:

1. Öffnen Sie Ihr Visual Studio-Projekt.
2. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt und wählen Sie „NuGet-Pakete verwalten“ aus.
3. Suchen Sie nach „Aspose.PDF“ und installieren Sie die neueste Version.

```csharp
using System.IO;
using Aspose.Pdf;
using System;
using System.Net;
```
Nachdem wir nun alles eingerichtet haben, unterteilen wir den Prozess der Konvertierung von HTML in PDF mit Anmeldeinformationen in überschaubare Schritte.

## Schritt 1: Richten Sie Ihr Dokumentverzeichnis ein

Bevor wir HTML in PDF konvertieren können, müssen wir angeben, wo unser Ausgabe-PDF gespeichert werden soll. Dies geschieht durch die Definition eines Pfads zum Dokumentenverzeichnis.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Ersetzen `"YOUR DOCUMENT DIRECTORY"` mit dem tatsächlichen Pfad, in dem Sie Ihre PDF-Datei speichern möchten. Dies kann ein Ordner auf Ihrem Desktop oder ein anderer Speicherort auf Ihrem System sein.

## Schritt 2: Erstellen einer Webanforderung

Als nächstes müssen wir eine Anfrage erstellen, um den HTML-Inhalt von einer bestimmten URL abzurufen. Hier verwenden wir die `WebRequest` Klasse.

```csharp
WebRequest request = WebRequest.Create("http://My.signchart.com/Report/PrintBook.asp?ProjectGuid=6FB9DBB0-");
```

Hier erstellen wir eine Anfrage an die URL, die das zu konvertierende HTML enthält. Ersetzen Sie die URL durch die gewünschte URL.

## Schritt 3: Anmeldeinformationen festlegen (falls erforderlich)

Wenn der Server Anmeldeinformationen für den Zugriff auf den Inhalt benötigt, müssen wir diese festlegen. Dies geschieht mit dem `CredentialCache.DefaultCredentials`.

```csharp
request.Credentials = CredentialCache.DefaultCredentials;
```

Diese Zeile stellt sicher, dass die Anforderung die Standardanmeldeinformationen des aktuellen Benutzers verwendet. Wenn Sie spezifische Anmeldeinformationen angeben müssen, können Sie eine neue `NetworkCredential` Objekt.

## Schritt 4: Erhalten Sie die Antwort

Nachdem wir unsere Anfrage eingerichtet haben, ist es an der Zeit, die Antwort vom Server zu erhalten.

```csharp
HttpWebResponse response = (HttpWebResponse)request.GetResponse();
```

Diese Zeile sendet die Anfrage und wartet auf die Antwort des Servers. Wenn alles gut geht, erhalten wir den benötigten HTML-Inhalt.

## Schritt 5: Lesen Sie den Antwortstream

Sobald wir die Antwort erhalten haben, müssen wir den vom Server zurückgegebenen Inhalt lesen. Dies geschieht mit einem `StreamReader`.

```csharp
Stream dataStream = response.GetResponseStream();
StreamReader reader = new StreamReader(dataStream);
string responseFromServer = reader.ReadToEnd();
reader.Close();
dataStream.Close();
response.Close();
```

Hier lesen wir den gesamten Inhalt des Antwortstroms in eine String-Variable namens `responseFromServer`. Vergessen Sie nicht, den Reader und den Stream zu schließen, um Ressourcen freizugeben.

## Schritt 6: HTML in PDF konvertieren

Jetzt kommt der spannende Teil! Wir konvertieren den HTML-Inhalt mit Aspose.PDF in ein PDF-Dokument.

```csharp
MemoryStream stream = new MemoryStream(System.Text.Encoding.UTF8.GetBytes(responseFromServer));
HtmlLoadOptions options = new HtmlLoadOptions("http://My.signchart.com/");
options.ExternalResourcesCredentials = CredentialCache.DefaultCredentials;

Document pdfDocument = new Document(stream, options);
```

In diesem Schritt erstellen wir eine `MemoryStream` aus dem HTML-Inhalt und Einrichten `HtmlLoadOptions`. Dadurch können wir die Basis-URL für alle externen Ressourcen (wie Bilder oder Stylesheets) angeben, auf die das HTML verweisen könnte.

## Schritt 7: Speichern Sie das PDF-Dokument

Schließlich müssen wir das generierte PDF-Dokument im angegebenen Verzeichnis speichern.

```csharp
pdfDocument.Save(dataDir + "ProvideCredentialsDuringHTMLToPDF_out.pdf");
```

Diese Zeile speichert die PDF-Datei unter dem Namen `ProvideCredentialsDuringHTMLToPDF_out.pdf` in dem Verzeichnis, das wir zuvor angegeben haben.

## Abschluss

Und da haben Sie es! Sie haben HTML erfolgreich mit Aspose.PDF für .NET in PDF konvertiert und gleichzeitig Anmeldeinformationen für den sicheren Zugriff angegeben. Diese leistungsstarke Bibliothek vereinfacht die Handhabung von PDF-Dokumenten und ermöglicht Ihnen mit nur wenigen Codezeilen die Erstellung professioneller PDFs aus HTML-Inhalten. 

## Häufig gestellte Fragen

### Was ist Aspose.PDF für .NET?
Aspose.PDF für .NET ist eine Bibliothek, mit der Entwickler PDF-Dokumente in .NET-Anwendungen erstellen, bearbeiten und konvertieren können.

### Wie installiere ich Aspose.PDF?
Sie können Aspose.PDF über den NuGet Package Manager in Visual Studio installieren oder von der [Webseite](https://releases.aspose.com/pdf/net/).

### Kann ich Aspose.PDF kostenlos nutzen?
Ja, Aspose bietet eine kostenlose Testversion an, mit der Sie die Bibliothek vor dem Kauf testen können.

### Welche Dokumenttypen kann ich mit Aspose.PDF erstellen?
Mit Aspose.PDF können Sie eine Vielzahl von Dokumenten erstellen, darunter Berichte, Rechnungen und Formulare.

### Wo finde ich Unterstützung für Aspose.PDF?
Sie finden Unterstützung und können Fragen stellen auf der [Aspose-Supportforum](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}