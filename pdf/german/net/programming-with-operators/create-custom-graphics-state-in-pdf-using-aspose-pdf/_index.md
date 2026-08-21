---
category: general
date: 2026-08-20
description: Erstellen Sie einen benutzerdefinierten Grafikzustand in PDF mit Aspose.Pdf.
  Erfahren Sie, wie Sie PDF‑Ressourcen bearbeiten und Transparenz zu PDFs hinzufügen,
  in nur wenigen Schritten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom graphics state
- edit pdf resources
- add transparency pdf
- Aspose.Pdf graphics state
- PDF resource dictionary
language: de
lastmod: 2026-08-20
og_description: Erstellen Sie einen benutzerdefinierten Grafikstatus in PDF mit Aspose.Pdf.
  Dieses Tutorial zeigt, wie man PDF‑Ressourcen bearbeitet und schnell Transparenz
  zu PDFs hinzufügt.
og_image_alt: Screenshot of C# code that creates a custom graphics state in a PDF
og_title: Erstellen eines benutzerdefinierten Grafikzustands in PDF – Aspose.Pdf-Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create custom graphics state in PDF with Aspose.Pdf. Learn how to edit
    PDF resources and add transparency PDF in just a few steps.
  headline: Create custom graphics state in PDF using Aspose.Pdf
  type: TechArticle
tags:
- PDF
- Aspose.Pdf
- C#
- Graphics state
title: Erstellen eines benutzerdefinierten Grafikzustands in PDF mit Aspose.Pdf
url: /de/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erstellen eines benutzerdefinierten Grafikzustands in PDF mit Aspose.Pdf

Wenn Sie einen **create custom graphics state** in einem PDF **erstellen** müssen, zeigt Ihnen dieser Leitfaden genau, wie Sie dies mit Aspose.Pdf für .NET tun. Am Ende des Tutorials können Sie **edit PDF resources**, ein neues graphics‑state‑Dictionary einfügen und **add transparency PDF**‑Inhalte hinzufügen, ohne Ihr C#‑Projekt zu verlassen.

Sie sehen ein vollständiges, ausführbares Beispiel, eine Erklärung, warum jede Zeile wichtig ist, und Tipps zum Umgang mit mehrseitigen Dokumenten oder verschiedenen Blend‑Modi. Es werden keine externen Werkzeuge benötigt – nur die Aspose.Pdf‑Bibliothek und eine grundlegende .NET‑Entwicklungsumgebung.

## Voraussetzungen

* .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7+)
* Eine lizenzierte Kopie von **Aspose.Pdf for .NET** (die kostenlose Testversion funktioniert zum Testen)
* Eine Eingabe‑PDF‑Datei mit dem Namen `input.pdf`, die in einem Ordner liegt, den Sie im Code referenzieren können
* Visual Studio 2022 oder jede IDE, die C#‑Entwicklung unterstützt

Das Tutorial geht davon aus, dass Sie mit grundlegender C#‑Syntax und dem Konzept von PDF‑Seiten vertraut sind.

## Schritt 1: Laden Sie das Quell‑PDF und greifen Sie auf die erste Seite zu

Der erste Vorgang besteht darin, die PDF‑Datei zu öffnen und die Seite abzurufen, deren Ressourcen Sie ändern möchten. Aspose.Pdf stellt jede Seite als ein `Page`‑Objekt dar, und jede Seite enthält ein **resource dictionary**, das Grafikzustände, Schriften, XObjects und mehr speichert.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.InteractiveFeatures;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System.Collections.Generic;

// Load the PDF you want to edit
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Get the first page (pages are 1‑based in Aspose.Pdf)
    Page firstPage = pdfDocument.Pages[1];
```

*Warum das wichtig ist:* Die `Document`‑Klasse lädt die Datei in den Speicher, und `Pages[1]` gibt Ihnen direkten Zugriff auf das Ressourcen‑Dictionary der ersten Seite, wo ein Grafikzustand gespeichert ist.

## Schritt 2: Öffnen Sie das Ressourcen‑Dictionary zum Bearbeiten

Aspose.Pdf stellt einen `DictionaryEditor`‑Hilfsmechanismus bereit, mit dem Sie ein Ressourcen‑Dictionary wie ein reguläres .NET‑`Dictionary` behandeln können. Das erleichtert das Lesen, Hinzufügen oder Ersetzen von Einträgen wie `ExtGState`.

```csharp
    // Create an editor for the page’s resources
    var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

*Warum das wichtig ist:* `DictionaryEditor` abstrahiert die Low‑Level‑COS‑Objekte, sodass Sie mit bekannten Schlüssel‑/Wert‑Paaren arbeiten können, während die PDF‑Konformität erhalten bleibt.

## Schritt 3: Abrufen (oder Erstellen) des ExtGState‑Dictionaries

Der **ExtGState**‑Eintrag enthält alle externen graphics‑state‑Objekte für die Seite. Wenn das Dictionary nicht existiert, erstellt Aspose.Pdf automatisch ein leeres für Sie.

```csharp
    // Ensure the ExtGState dictionary exists
    var extGStateDict = resourcesEditor.ContainsKey("ExtGState")
        ? resourcesEditor["ExtGState"].ToCosPdfDictionary()
        : new CosPdfDictionary(pdfDocument);
```

*Warum das wichtig ist:* Ein fehlender `ExtGState`‑Eintrag würde später eine `KeyNotFoundException` auslösen. Diese Prüfung ermöglicht, dass der Code mit PDFs funktioniert, die noch nie einen benutzerdefinierten Grafikzustand definiert haben – ein wesentlicher Teil der Robustheit beim **edit PDF resources**.

## Schritt 4: Erstellen des benutzerdefinierten Grafikzustands‑Dictionaries

Ein Grafikzustand beschreibt, wie Zeichenoperationen gerendert werden. Um **add transparency PDF** zu ermöglichen, müssen Sie die Einträge `ca` (Füll‑Opazität) und `CA` (Strich‑Opazität) setzen und optional einen Blend‑Modus (`BM`) angeben. Der folgende Code erstellt ein neues Dictionary mit diesen Parametern.

```csharp
    // Create an empty dictionary that will become the new graphics state
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

    // Define the parameters you want for the custom state
    var graphicsStateParams = new KeyValuePair<string, ICosPdfPrimitive>[]
    {
        // Stroke opacity (1 = fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
        // Fill opacity (0.5 = 50 % transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
        // Blend mode – "Normal" is the default, but you can use "Multiply", "Screen", etc.
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
    };

    // Populate the dictionary with the parameters
    foreach (var param in graphicsStateParams)
        newGraphicsState.Add(param);
```

*Warum das wichtig ist:* Die Einträge `ca` und `CA` steuern die Transparenz für Füll‑ bzw. Strich‑Operationen. Das Setzen von `BM` ermöglicht das Experimentieren mit verschiedenen Komposit‑Effekten, was nützlich ist, wenn Sie später **add transparency PDF**‑Inhalte wie halbtransparente Formen oder Bilder hinzufügen.

## Schritt 5: Registrieren des neuen Grafikzustands unter einem eindeutigen Namen

Jeder Grafikzustand im `ExtGState`‑Dictionary muss einen eindeutigen Namen haben (z. B. `GS0`, `GS1`). Sie können jeden Namen wählen, der nicht mit bestehenden Einträgen kollidiert.

```csharp
    // Choose a name that is unlikely to collide with existing states
    const string graphicsStateName = "GS0";

    // Add the new graphics state to the ExtGState dictionary
    extGStateDict.Add(graphicsStateName, newGraphicsState);

    // If the ExtGState entry was missing, attach it back to the page resources
    if (!resourcesEditor.ContainsKey("ExtGState"))
        resourcesEditor["ExtGState"] = extGStateDict;
```

*Warum das wichtig ist:* Durch das Einfügen des neuen Dictionaries unter `GS0` machen Sie den Zustand aus den Seiten‑Content‑Streams ansprechbar. Der bedingte Block stellt sicher, dass der `ExtGState`‑Eintrag auch bei PDFs vorhanden ist, die ohne einen begonnen haben – ein weiterer **edit PDF resources**‑Schutz.

## Schritt 6: Verwenden des benutzerdefinierten Grafikzustands im Seiteninhalt (optional)

Die vorherigen Schritte *definieren* nur den Grafikzustand. Um die Wirkung tatsächlich zu sehen, müssen Sie ihn im Content‑Stream der Seite referenzieren. Nachfolgend ein kurzes Beispiel, das ein halbtransparentes Rechteck mit dem gerade erstellten Zustand zeichnet.

```csharp
    // Get the page’s content stream (or create a new one if empty)
    var content = firstPage.Contents[1];
    var graphics = new ContentWriter(content);

    // Save current graphics state
    graphics.WriteOperator(OperatorName.SaveState);
    // Set the custom graphics state we just defined
    graphics.WriteOperand($"/{graphicsStateName}");
    graphics.WriteOperator(OperatorName.SetExtGState);
    // Draw a rectangle (coordinates are in points)
    graphics.WriteOperand(100);   // lower‑left x
    graphics.WriteOperand(500);   // lower‑left y
    graphics.WriteOperand(200);   // width
    graphics.WriteOperand(100);   // height
    graphics.WriteOperator(OperatorName.Rectangle);
    // Fill the rectangle using the current fill opacity (ca = 0.5)
    graphics.WriteOperator(OperatorName.Fill);
    // Restore the previous graphics state
    graphics.WriteOperator(OperatorName.RestoreState);
```

*Warum das wichtig ist:* Der `SetExtGState`‑Operator (`gs`) weist den PDF‑Renderer an, die in `GS0` definierten Parameter anzuwenden. Das Rechteck wird mit 50 % Füll‑Opazität angezeigt, während sein Strich vollständig undurchsichtig bleibt.

## Schritt 7: Speichern des modifizierten PDFs

Zum Schluss schreiben Sie die Änderungen zurück auf die Festplatte. Sie können die Originaldatei überschreiben oder eine neue erstellen.

```csharp
    // Save the updated PDF
    pdfDocument.Save("YOUR_DIRECTORY/output_with_custom_gs.pdf");
}
```

Wenn Sie `output_with_custom_gs.pdf` in einem PDF‑Betrachter öffnen, sollten Sie ein halbtransparentes Rechteck auf der ersten Seite sehen. Das bestätigt, dass Sie erfolgreich **create custom graphics state**, **edit PDF resources** und **add transparency PDF**‑Inhalte erstellt haben.

## Häufige Variationen und Randfälle

| Situation | Was anzupassen ist |
|-----------|--------------------|
| **Mehrere Seiten benötigen denselben Zustand** | Registrieren Sie den Grafikzustand einmal (Schritte 1‑5) und referenzieren Sie `GS0` im Content‑Stream jeder Seite. |
| **Unterschiedliche Opazität pro Element** | Definieren Sie zusätzliche Zustände (`GS1`, `GS2`, …) mit unterschiedlichen `ca`/`CA`‑Werten und wechseln Sie zwischen ihnen mittels `SetExtGState`. |
| **Blend‑Modus anders als Normal** | Ersetzen Sie `"Normal"` durch `"Multiply"`, `"Screen"` oder einen anderen PDF‑Standard‑Blend‑Modus im `BM`‑Eintrag. |
| **Namenskollision** | Vor dem Hinzufügen prüfen Sie `extGStateDict.ContainsKey(yourName)` und wählen Sie bei Bedarf ein eindeutiges Suffix. |
| **PDF enthält bereits ein ExtGState‑Dictionary** | Der Code in Schritt 3 verwendet das vorhandene Dictionary bereits erneut, sodass keine zusätzliche Behandlung erforderlich ist. |

**Pro‑Tipp:** Beim Arbeiten mit großen PDFs sollten Sie die Verwendung von `Document` in einen `using`‑Block (wie gezeigt) einbetten, um native Ressourcen sofort freizugeben. Außerdem sollten Sie erwägen, die `PdfCompliance`‑Eigenschaft von Aspose.Pdf zu aktivieren, wenn Sie nach dem Bearbeiten von Ressourcen PDF/A‑ oder PDF/X‑Konformität garantieren müssen.

## Vollständiges funktionierendes Beispiel



## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man PDF mit Aspose erstellt – Formularfeld und Seiten hinzufügen](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Wie man benutzerdefinierte Tabellen in PDFs mit Aspose.PDF .NET erstellt](/pdf/english/net/tables-lists/create-custom-tables-in-pdfs-aspose-pdf-dot-net/)
- [Benutzerdefinierte PDF‑Stempel mit Aspose Pdf Net erstellen](/pdf/hongkong/net/images-graphics/create-custom-pdf-stamps-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}