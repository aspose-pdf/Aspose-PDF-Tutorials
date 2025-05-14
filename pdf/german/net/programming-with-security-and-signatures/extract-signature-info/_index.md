---
"description": "Erfahren Sie, wie Sie mit Aspose.PDF für .NET digitale Signaturen und Zertifikatsinformationen aus PDF-Dokumenten extrahieren. Eine vollständige Schritt-für-Schritt-Anleitung für C#-Entwickler."
"linktitle": "Signaturinformationen extrahieren"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Signaturinformationen extrahieren"
"url": "/de/net/programming-with-security-and-signatures/extract-signature-info/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Signaturinformationen extrahieren

## Einführung

In der heutigen digitalen Welt ist die Gewährleistung der Sicherheit und Integrität von Dokumenten entscheidend. Eine gängige Methode zum Sichern von PDFs ist das Hinzufügen einer digitalen Signatur. Das Abrufen und Überprüfen der Signaturdetails kann jedoch manchmal eine Herausforderung darstellen, insbesondere bei der Verwendung verschiedener Zertifikate. In dieser Anleitung führen wir Sie durch den Prozess des Extrahierens von Signaturinformationen aus PDF-Dokumenten mit Aspose.PDF für .NET und machen die Aufgabe zum Kinderspiel. Sie erfahren, wie Sie auf Signaturfelder zugreifen, Zertifikatsinformationen extrahieren und in einer Datei speichern.

## Voraussetzungen

Bevor wir beginnen, stellen wir sicher, dass Sie alles für den Start bereit haben.

- Aspose.PDF für .NET-Bibliothek: Wenn Sie es noch nicht haben, können Sie es von der [Aspose.PDF für .NET-Downloadseite](https://releases.aspose.com/pdf/net/). 
- .NET-Entwicklungsumgebung: Sie benötigen eine IDE wie Visual Studio.
- Grundlegende C#-Kenntnisse: Kenntnisse in C# sind hilfreich, um die Codeausschnitte in diesem Tutorial zu verstehen.
- PDF-Dokument mit digitaler Signatur: Stellen Sie zu Testzwecken sicher, dass Sie über eine PDF-Datei verfügen, die mindestens eine digitale Signatur enthält.

## Importieren erforderlicher Namespaces

Bevor Sie mit dem Code beginnen, ist es wichtig, die erforderlichen Namespaces zu importieren. Diese Namespaces ermöglichen Ihnen den Zugriff auf die Aspose.PDF-Funktionalität und die Arbeit mit PDF-Dokumenten.

```csharp
using System.IO;
using Aspose.Pdf.Forms;
using Aspose.Pdf;
using System;
```

Nachdem Sie nun die Grundlagen eingerichtet haben, fahren wir mit dem eigentlichen Vorgang des Extrahierens der Signaturinformationen aus einer PDF-Datei fort.

## Schritt 1: Einrichten des Dokumentverzeichnisses

Bevor Sie ein PDF-Dokument bearbeiten, müssen Sie den Speicherort der zu verwendenden Datei angeben. Sie können `"YOUR DOCUMENT DIRECTORY"` durch den tatsächlichen Pfad des Verzeichnisses, in dem Ihre PDFs gespeichert sind.

```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string input = dataDir + "ExtractSignatureInfo.pdf";
```

Hier geben wir das Verzeichnis an, in dem sich die PDF-Datei befindet, sowie den Dateinamen selbst. Stellen Sie sicher, dass die Datei in diesem Verzeichnis vorhanden ist!

## Schritt 2: Laden des PDF-Dokuments

Nachdem Sie nun Ihr Verzeichnis eingerichtet haben, besteht der nächste Schritt darin, das PDF-Dokument mit dem `Document` Klasse von Aspose.PDF.

```csharp
using (Document pdfDocument = new Document(input))
{
    // Bearbeiten Sie hier das PDF.
}
```

Diese Codezeile initialisiert eine `Document` Objekt, das die PDF-Datei darstellt. Das `using` Anweisung stellt sicher, dass die Ressourcen nach der Verarbeitung des Dokuments bereinigt werden.

## Schritt 3: Zugriff auf Formularfelder

In diesem Schritt durchlaufen wir alle Formularfelder im PDF-Dokument. Da Signaturen üblicherweise als Formularfelder gespeichert werden, hilft uns dieser Schritt, die Signaturfelder zu identifizieren.

```csharp
foreach (Field field in pdfDocument.Form)
{
    // Identifizieren Sie hier Signaturfelder.
}
```

Durch Iteration durch die `Form` Eigentum der `Document` Objekt können wir jedes Formularfeld untersuchen, um zu prüfen, ob es ein Signaturfeld ist.

## Schritt 4: Signaturfelder identifizieren

Nachdem Sie die Formularfelder aufgerufen haben, müssen Sie im nächsten Schritt die Signaturfelder identifizieren. Dies erreichen Sie, indem Sie jedes Feld in ein `SignatureField` Objekt.

```csharp
SignatureField sf = field as SignatureField;
if (sf != null)
{
    // Signaturinformationen extrahieren.
}
```

Hier verwenden wir die `as` Schlüsselwort, um zu versuchen, jedes Formularfeld in ein `SignatureField`Wenn die Übertragung erfolgreich ist, wissen wir, dass das Feld eine Signatur ist.

## Schritt 5: Extrahieren des Zertifikats

Nachdem Sie das Signaturfeld identifiziert haben, besteht die nächste Aufgabe darin, das Zertifikat aus der Signatur zu extrahieren. Zertifikate enthalten wichtige Informationen über den Unterzeichner und die Gültigkeit der Signatur.

```csharp
Stream cerStream = sf.ExtractCertificate();
```

Der `ExtractCertificate` Methode gibt einen `Stream` Objekt, das die Zertifikatsdaten enthält. Dieser Stream kann verwendet werden, um das Zertifikat für weitere Analysen oder zur Speicherung zu speichern.

## Schritt 6: Speichern des Zertifikats in einer Datei

Nachdem Sie das Zertifikat extrahiert haben, speichern Sie es abschließend in einer Datei. In diesem Fall speichern wir das Zertifikat als `.cer` Datei.

```csharp
if (cerStream != null)
{
    using (cerStream)
    {
        byte[] bytes = new byte[cerStream.Length];
        using (FileStream fs = new FileStream(dataDir + @"input.cer", FileMode.CreateNew))
        {
            cerStream.Read(bytes, 0, bytes.Length);
            fs.Write(bytes, 0, bytes.Length);
        }
    }
}
```

In diesem Codeblock führen wir Folgendes aus:

1. Überprüfen Sie, ob der Zertifikatsstream nicht null ist.
2. Lesen Sie die Zertifikatsdaten in ein Byte-Array.
3. Schreiben Sie das Byte-Array in ein `.cer` Datei im Dokumentverzeichnis.

## Abschluss

Das Extrahieren digitaler Signaturen und der zugehörigen Zertifikatsinformationen aus PDF-Dokumenten mit Aspose.PDF für .NET ist in wenigen Schritten ganz einfach. Ob Sie Dokumente prüfen, Signaturen verifizieren oder Zertifikate einfach zur sicheren Aufbewahrung speichern – dieses Tutorial vermittelt Ihnen das Wissen, um dies effizient zu erledigen. Denken Sie daran: Die Sicherung und Verifizierung von Dokumenten ist in der heutigen digitalen Welt von entscheidender Bedeutung. Tools wie Aspose.PDF für .NET vereinfachen die Handhabung erheblich.

## Häufig gestellte Fragen

### Kann ich mit Aspose.PDF für .NET mehrere Signaturen aus einer PDF-Datei extrahieren?
Ja, der Code durchläuft alle Formularfelder im Dokument und ermöglicht Ihnen, mehrere Signaturen zu extrahieren, falls vorhanden.

### Was passiert, wenn im PDF keine Signatur gefunden wird?
Wenn keine Signaturfelder vorhanden sind, überspringt der Code sie einfach, ohne einen Fehler zu verursachen.

### Kann ich mit diesem Ansatz die Gültigkeit einer Signatur überprüfen?
Sie können zwar das Zertifikat extrahieren, zur Überprüfung der Gültigkeit einer Signatur sind jedoch zusätzliche Schritte erforderlich, beispielsweise die Überprüfung der Vertrauenskette des Zertifikats.

### Ist es möglich, mit Aspose.PDF für .NET andere Formularfelddaten zu extrahieren?
Ja, mit Aspose.PDF können Sie auf verschiedene Arten von Formularfeldern in einer PDF-Datei zugreifen und diese bearbeiten, nicht nur auf Signaturfelder.

### Wie kann ich die Details des extrahierten Zertifikats anzeigen?
Sobald das Zertifikat als `.cer` Datei können Sie sie mit einem beliebigen Zertifikatsanzeigeprogramm öffnen oder zur weiteren Überprüfung in einen Systemzertifikatsspeicher importieren.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}