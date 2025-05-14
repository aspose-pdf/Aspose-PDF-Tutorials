---
"description": "Erfahren Sie, wie Sie mit Aspose.PDF für .NET ein PDF digital mit einem Zeitstempel signieren. Diese Schritt-für-Schritt-Anleitung behandelt Voraussetzungen, Zertifikatseinrichtung, Zeitstempel und mehr."
"linktitle": "Digitales Signieren mit Zeitstempel in PDF-Dateien"
"second_title": "Aspose.PDF für .NET API-Referenz"
"title": "Digitales Signieren mit Zeitstempel in PDF-Dateien"
"url": "/de/net/programming-with-security-and-signatures/digitally-sign-with-time-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Digitales Signieren mit Zeitstempel in PDF-Dateien

## Einführung

Mussten Sie schon einmal ein PDF digital signieren und für zusätzliche Sicherheit einen Zeitstempel hinzufügen? Ob Sie an juristischen Dokumenten, Verträgen oder anderen Dokumenten arbeiten, die eine sichere Authentifizierung erfordern – eine digitale Signatur mit Zeitstempel sorgt für zusätzliche Glaubwürdigkeit. In diesem Tutorial erklären wir Ihnen, wie Sie mit Aspose.PDF für .NET Ihren PDF-Dokumenten eine digitale Signatur mit Zeitstempel hinzufügen. Keine Sorge, wir gehen Schritt für Schritt vor!

## Voraussetzungen

Bevor wir uns in den Code vertiefen, müssen Sie einige Dinge einrichten, um mitmachen zu können. Hier ist eine kurze Checkliste der Voraussetzungen für den Einstieg:

- Aspose.PDF für .NET Bibliothek: Sie benötigen die Aspose.PDF für .NET Bibliothek in Ihrem Projekt installiert. Sie können [Laden Sie hier die neueste Version herunter](https://releases.aspose.com/pdf/net/) oder fügen Sie es über NuGet zu Ihrem Projekt hinzu.
- Ein PDF-Dokument: Sie benötigen eine Beispiel-PDF-Datei. Stellen Sie sicher, dass sich im Projektverzeichnis eine Datei befindet, die Sie signieren möchten.
- Digitales Zertifikat (PFX-Datei): Stellen Sie sicher, dass Sie über ein digitales Zertifikat verfügen (eine `.pfx` Datei), um das Dokument digital zu signieren.
- Zeitstempel-URL: Dies ist ein Online-Zeitstempeldienst, der verwendet wird, um der digitalen Signatur einen Zeitstempel hinzuzufügen. 
- Grundlegende C#-Kenntnisse: Sie müssen kein Experte sein, aber Kenntnisse der C#-Grundlagen helfen Ihnen, den Code zu verstehen und anzupassen.

Wenn Sie alle diese Kästchen angekreuzt haben, können Sie mit dem Programmieren beginnen!

## Pakete importieren

Um zu beginnen, müssen Sie die folgenden Namespaces in Ihr C#-Projekt importieren. Dadurch stellen Sie sicher, dass Sie Zugriff auf die relevanten Aspose.PDF-Klassen und -Funktionen haben.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System.Collections;
```

## Schritt 1: Laden Sie das PDF-Dokument

Als Erstes müssen wir das PDF-Dokument laden, das wir signieren möchten. So geht's:

```csharp
// Definieren Sie den Pfad zu Ihrem Dokumentverzeichnis
string dataDir = "YOUR DOCUMENTS DIRECTORY";

// Laden Sie das PDF-Dokument
Document document = new Document(dataDir + @"DigitallySign.pdf");
```

Dieser Schritt ist ziemlich einfach. Wir definieren lediglich den Pfad zum Dokument, das wir signieren möchten. Die `Document` Die Klasse von Aspose.PDF übernimmt das Laden der Datei.

## Schritt 2: Einrichten der digitalen Signatur

Als Nächstes erstellen wir die digitale Signatur mit der PKCS7-Klasse und laden die PFX-Datei. Diese PFX-Datei enthält Ihr Zertifikat und Ihren privaten Schlüssel, die zum Signieren des Dokuments erforderlich sind.

```csharp
// Pfad zu Ihrer PFX-Datei
string pfxFile = "YOUR DOCUMENTS DIRECTORY\\certificate.pfx";

// Initialisieren Sie das Signaturobjekt
PdfFileSignature signature = new PdfFileSignature(document);

// Laden Sie die PFX-Datei mit einem Passwort
PKCS7 pkcs = new PKCS7(pfxFile, "pfx_password");
```

An diesem Punkt weisen Sie Aspose an, Ihr digitales Zertifikat zum Signieren des Dokuments zu verwenden. Die `PKCS7` Das Objekt übernimmt die gesamte kryptografische Arbeit für Sie, sodass Sie sich nicht um die kleinsten Details kümmern müssen.

## Schritt 3: Zeitstempeleinstellungen hinzufügen

Eine der Schlüsselkomponenten einer robusten digitalen Signatur ist der Zeitstempel. Er stellt sicher, dass die Signatur des Dokuments auch nach Ablauf des Zertifikats verifiziert werden kann. Richten wir den Zeitstempel mithilfe einer Online-Zeitstempelstelle ein.

```csharp
// Definieren Sie die Zeitstempeleinstellungen
TimestampSettings timestampSettings = new TimestampSettings("https://Ihre_Zeitstempel_URL", "Benutzer:Passwort");

// Hinzufügen von Zeitstempeleinstellungen zum PKCS7-Objekt
pkcs.TimestampSettings = timestampSettings;
```

Hier geben Sie die URL für den Zeitstempeldienst an, der Ihre Signatur automatisch mit Uhrzeit und Datum versieht. Dies kann mit oder ohne Authentifizierung erfolgen.

## Schritt 4: Definieren Sie den Ort und das Aussehen der Signatur

Nun legen wir fest, wo die Signatur im PDF-Dokument erscheinen soll und welche Abmessungen sie haben soll. Sie können die Position des Signaturfelds auf der Seite sowie die Größe anpassen.

```csharp
// Definieren Sie das Aussehen und die Position der Signatur (Seite 1, mit angegebenem Rechteck).
System.Drawing.Rectangle rect = new System.Drawing.Rectangle(100, 100, 200, 100);
```

Hier definieren wir ein Rechteck, das die Signatur an den Koordinaten (100, 100) auf der ersten Seite des PDFs positioniert, mit einer Breite von 200 und einer Höhe von 100. Sie können diese Werte an Ihr Design anpassen.

## Schritt 5: Signieren Sie das PDF-Dokument

Nachdem alles eingerichtet ist, können Sie die PDF-Datei digital signieren. Dieser Schritt kombiniert Zertifikat, Zeitstempel und Positionierung in einem einfachen Befehl.

```csharp
// Unterschreiben Sie das Dokument auf der ersten Seite
signature.Sign(1, "Signature Reason", "Contact", "Location", true, rect, pkcs);
```

Folgendes passiert:
- 1: Dies gibt an, dass die Signatur auf der ersten Seite angebracht werden soll.
- „Unterschriftsgrund“: Hier können Sie angeben, warum Sie das Dokument unterschreiben.
- „Kontakt“: Geben Sie die Kontaktinformationen des Unterzeichners ein.
- „Standort“: Geben Sie den Standort des Unterzeichners an.
- true: Dieser Boolesche Wert gibt an, ob die Signatur im Dokument sichtbar ist.
- Rechteck: Das zuvor definierte Rechteck gibt die Größe und Position der Signatur an.
- pkcs: Das PKCS7-Objekt enthält die digitalen Zertifikats- und Zeitstempeleinstellungen.

## Schritt 6: Speichern Sie die signierte PDF-Datei

Sobald das Dokument signiert ist, müssen Sie es nur noch speichern. Sie können einen neuen Dateinamen wählen, um sowohl das Original als auch die signierte Version zu speichern.

```csharp
// Speichern Sie das signierte PDF-Dokument
signature.Save(dataDir + "DigitallySignWithTimeStamp_out.pdf");
```

Ihr neu signiertes und mit einem Zeitstempel versehenes PDF wird jetzt im angegebenen Verzeichnis gespeichert!

## Abschluss

Und da haben Sie es! Sie haben ein PDF mit Aspose.PDF für .NET erfolgreich digital signiert und mit einem Zeitstempel versehen. Dieser Prozess gewährleistet die Authentizität und Integrität Ihrer Dokumente und gibt Ihnen und dem Empfänger Sicherheit. Digitale Signaturen werden in der heutigen digitalen Welt immer wichtiger, daher ist die Beherrschung dieses Prozesses definitiv eine wertvolle Fähigkeit.

## Häufig gestellte Fragen

### Kann ich für das Zertifikat ein anderes Dateiformat verwenden?  
Ja, aber das Tutorial konzentriert sich auf die Verwendung einer PFX-Datei, dem gängigsten Format für digitale Zertifikate.

### Benötige ich eine Internetverbindung, um den Zeitstempel anzuwenden?  
Ja, da der Zeitstempel von einer Online-Zeitstempelbehörde abgerufen wird, benötigen Sie Internetzugang.

### Kann ich mehrere Seiten in einer PDF-Datei unterschreiben?  
Absolut! Sie können die `signature.Sign()` Methode, um mehrere Seiten anzusprechen oder alle Seiten zu durchlaufen.

### Was passiert, wenn das Kennwort für die PFX-Datei falsch ist?  
Wenn das Passwort falsch ist, erhalten Sie eine Ausnahme. Stellen Sie daher sicher, dass Sie es richtig eingegeben haben.

### Kann ich die Signatur unsichtbar machen?  
Ja, du kannst vorbeikommen `false` zum `Sign` Verwenden Sie den Sichtbarkeitsparameter der Methode, um die Signatur unsichtbar zu machen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}