---
category: general
date: 2026-11-16
description: Erfahren Sie, wie Sie in C# mit Aspose.Pdf einen PDF‑Grafikstatus erstellen.
  Dieser Leitfaden behandelt Transparenz, Mischmodus und enthält ein vollständiges
  Codebeispiel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf graphics state
- Aspose.Pdf ExtGState
- PDF opacity
- C# PDF manipulation
- PDF blend mode
- Aspose.Pdf graphics state
language: de
lastmod: 2026-11-16
og_description: Erstellen Sie den Grafikzustand einer PDF‑Datei in C# mit Aspose.Pdf.
  Folgen Sie diesem vollständigen Tutorial, um Deckkraft und Mischmodus programmgesteuert
  festzulegen.
og_image_alt: Illustration of how to create PDF graphics state with Aspose.Pdf in
  C#
og_title: PDF-Grafikzustand in C# erstellen – Schritt‑für‑Schritt Aspose.Pdf‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to create PDF graphics state in C# using Aspose.Pdf. This
    guide covers opacity, blend mode, and full code example.
  headline: How to create PDF graphics state in C# with Aspose.Pdf
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF
title: Wie man den PDF‑Grafikzustand in C# mit Aspose.Pdf erstellt
url: /de/net/images-graphics/how-to-create-pdf-graphics-state-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man PDF‑Grafikzustand in C# mit Aspose.Pdf erstellt

Wenn Sie **PDF graphics state** in einem .NET‑Projekt erstellen müssen, zeigt Ihnen dieses Tutorial genau, wie Sie das mit Aspose.Pdf erledigen. Egal, ob Sie die Opazität steuern, den Blend‑Modus ändern oder einen benutzerdefinierten Grafikzustand über Seiten hinweg wiederverwenden möchten, die nachfolgenden Schritte bieten Ihnen eine vollständige, sofort ausführbare Lösung.

In diesem Leitfaden lernen Sie, wie Sie auf die Seitenressourcen zugreifen, einen **ExtGState**‑Eintrag hinzufügen und die Änderungen in einer neuen Datei speichern. Das Beispiel funktioniert mit Aspose.Pdf 23.12 (oder neuer) und richtet sich an .NET 6+, aber die Konzepte gelten auch für frühere Versionen.

## Voraussetzungen

* Visual Studio 2022 (oder jede C#‑IDE) mit installiertem .NET 6‑SDK.  
* Eine Aspose.Pdf‑für‑.NET‑Lizenz oder ein temporärer Evaluierungsschlüssel.  
* Eine PDF‑Datei mit dem Namen `input.pdf`, die in einem Ordner liegt, den Sie im Code referenzieren können.  

Keine zusätzlichen NuGet‑Pakete sind über `Aspose.Pdf` hinaus erforderlich.

## Was das Tutorial abdeckt

* Laden eines bestehenden PDF‑Dokuments.  
* Navigieren zum Ressourcen‑Dictionary der ersten Seite.  
* Erstellen eines neuen Grafikzustands‑Dictionarys, das Strich‑Opazität (`CA`), Füll‑Opazität (`ca`) und Blend‑Modus (`BM`) definiert.  
* Hinzufügen des neuen Grafikzustands zur **ExtGState**‑Sammlung mit einem benutzerdefinierten Namen (`GS0`).  
* Speichern des aktualisierten PDFs, sodass nachfolgende Zeichenbefehle den neuen Zustand referenzieren können.

Am Ende des Tutorials können Sie **PDF graphics state**‑Objekte programmgesteuert erstellen und in jeder Zeichenoperation wiederverwenden.

## Schritt 1: Projekt einrichten und Namespaces importieren

Erstellen Sie eine neue Konsolenanwendung (oder integrieren Sie den Code in ein bestehendes Projekt). Fügen Sie den Aspose.Pdf‑Verweis hinzu und binden Sie die erforderlichen Namespaces ein:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators;
using Aspose.Pdf.Generator;
```

> **Pro‑Tipp:** Wenn Sie die kostenlose Evaluierungsversion verwenden, fügen Sie `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` vor dem Laden des Dokuments hinzu, um Wasserzeichen‑Meldungen zu vermeiden.

## Schritt 2: PDF‑Dokument laden

Das Öffnen der Datei ist unkompliziert. Die Klasse `Document` repräsentiert das gesamte PDF und gibt Ihnen Zugriff auf dessen Seiten und Ressourcen.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";

using (var document = new Document(inputPath))
{
    // All subsequent steps run inside this using block
```

Das Platzieren des Codes in einem `using`‑Block stellt sicher, dass der Dateihandle nach der Operation freigegeben wird, was für **C# PDF manipulation** in Produktionsdiensten unerlässlich ist.

## Schritt 3: Ressourcen‑Dictionary der ersten Seite abrufen

Jede PDF‑Seite besitzt ein *Resources*‑Dictionary, das Schriften, Bilder und Grafikzustände speichert. Wir benötigen einen `DictionaryEditor`, um diese Struktur zu bearbeiten.

```csharp
    // Step 3: Get the first page and its resources dictionary
    var page = document.Pages[1];
    var resourcesEditor = new DictionaryEditor(page.Resources);
```

Falls das PDF bereits einen `ExtGState`‑Eintrag enthält, liefert `resourcesEditor["ExtGState"]` diesen zurück; andernfalls erstellt Aspose.Pdf ein leeres Dictionary für uns, wenn wir den ersten Eintrag hinzufügen.

## Schritt 4: ExtGState‑Dictionary zugreifen oder erstellen

Das **ExtGState**‑Dictionary enthält benannte Grafikzustands‑Objekte. Wir holen entweder ein vorhandenes oder erstellen einen neuen Container.

```csharp
    // Step 4: Access (or create) the ExtGState dictionary within the resources
    var extGState = resourcesEditor["ExtGState"].ToCosPdfDictionary();
```

Wenn `ExtGState` nicht existiert, liefert `resourcesEditor["ExtGState"]` automatisch ein neues leeres Dictionary, wodurch der Code für jedes PDF funktioniert.

## Schritt 5: Neues Grafikzustands‑Dictionary erstellen

Ein Grafikzustand ist ein `CosPdfDictionary` mit spezifischen Schlüsseln:

* `CA` – Strich‑Opazität (0‑1)  
* `ca` – Füll‑Opazität (0‑1)  
* `BM` – Blend‑Modus (`Normal`, `Multiply`, etc.)

Wir erstellen ein leeres Dictionary, füllen es und fügen es anschließend zu `ExtGState` hinzu.

```csharp
    // Step 5: Create a new graphics state dictionary with desired parameters
    var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(document);
    var parameters = new[]
    {
        new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (fully opaque)
        new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (50% transparent)
        new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
    };

    foreach (var p in parameters)
        newGraphicsState.Add(p);
```

Sie können `0.5` zu einem beliebigen Wert zwischen `0` und `1` ändern, um die Füll‑Opazität anzupassen, oder `"Normal"` durch `"Multiply"` ersetzen, um einen anderen **PDF blend mode** zu erhalten. Diese Flexibilität erklärt, warum das Erstellen eines benutzerdefinierten Grafikzustands eine leistungsstarke Technik im Umgang mit **Aspose.Pdf graphics state** ist.

## Schritt 6: Grafikzustand mit einem Namen registrieren

PDF‑Inhaltsstreams referenzieren Grafikzustände über Namen. Hier verwenden wir `GS0`, aber jeder eindeutige Name funktioniert.

```csharp
    // Step 6: Add the new graphics state to the ExtGState dictionary with a name (e.g., GS0)
    extGState.Add("GS0", newGraphicsState);
```

Falls Sie mehrere Zustände benötigen, wiederholen Sie den Erstellungsschritt mit unterschiedlichen Parametern und fügen Sie sie als `GS1`, `GS2` usw. hinzu. Dieses Muster skaliert gut für komplexe Dokumente, die unterschiedliche Opazitäts‑ oder Blend‑Einstellungen auf verschiedenen Ebenen erfordern.

## Schritt 7: Modifiziertes PDF speichern

Schließlich schreiben Sie das aktualisierte Dokument in eine neue Datei. Das Original unverändert zu lassen erleichtert das Debugging.

```csharp
    // Step 7: Save the updated PDF document
    string outputPath = @"YOUR_DIRECTORY\output.pdf";
    document.Save(outputPath);
}
```

Nach der Ausführung enthält `output.pdf` einen `ExtGState`‑Eintrag mit dem Namen `GS0`. Jeder nachfolgende Zeichenoperator kann ihn über den `gs`‑Operator referenzieren (z. B. `GS0 gs` in einem Inhaltsstream).  

> **Warum das wichtig ist:** Durch das Erstellen eines wiederverwendbaren Grafikzustands vermeiden Sie das wiederholte Setzen von Opazität und Blend‑Einstellungen für jeden Zeichenbefehl, was sowohl die Leistung als auch die Wartbarkeit verbessert.

## Verwendung des neuen Grafikzustands in einem Inhaltsstream (optional)

Wenn Sie die Wirkung sofort sehen möchten, können Sie ein einfaches Rechteck hinzufügen, das den gerade erstellten Zustand verwendet:

```csharp
using (var document = new Document(outputPath))
{
    var page = document.Pages[1];
    var content = page.Contents[1]; // Get the first content stream

    // Insert graphics state selection and a semi‑transparent rectangle
    var operators = new List<Operator>
    {
        new Operator("GS0", "gs"),                     // Select our custom graphics state
        new Operator("0.5", "w"),                      // Set line width (optional)
        new Operator("100", "100", "200", "150", "re"), // Rectangle (x, y, width, height)
        new Operator("B")                              // Stroke the rectangle
    };

    foreach (var op in operators)
        content.Operators.Add(op);

    document.Save(@"YOUR_DIRECTORY\final_output.pdf");
}
```

Das Rechteck wird mit 50 % Füll‑Opazität gezeichnet, während die Kontur vollständig undurchsichtig bleibt, genau wie im **create PDF graphics state**‑Dictionary definiert.

## Häufige Fallstricke und wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| `ExtGState`‑Eintrag nicht gefunden | Einige PDFs lassen das Dictionary vollständig weg. | Der `DictionaryEditor` erstellt es automatisch, wenn Sie den ersten Eintrag hinzufügen, sodass keine zusätzliche Prüfung erforderlich ist. |
| Opazitätswerte > 1 oder < 0 | Die PDF‑Spezifikation begrenzt die Opazität auf den Bereich `[0,1]`. | Begrenzen Sie die Werte, bevor Sie `CosPdfNumber` erstellen. |
| Blend‑Modus Tippfehler | PDF‑Blend‑Modus‑Namen sind case‑sensitive. | Verwenden Sie exakte Namen wie `"Normal"`, `"Multiply"`, `"Screen"`. |
| Lizenz‑Wasserzeichen | Die Evaluierungsversion fügt auf der ersten Seite ein Wasserzeichen hinzu. | Wenden Sie eine gültige Lizenzdatei an, bevor Sie das Dokument öffnen. |

Die Behandlung dieser Randfälle stellt sicher, dass Ihre **create PDF graphics state**‑Implementierung zuverlässig über verschiedene PDF‑Quellen hinweg funktioniert.

## Vollständiges, ausführbares Beispiel

Unten finden Sie ein eigenständiges Programm, das Sie kopieren, einfügen und ausführen können. Ersetzen Sie `YOUR_DIRECTORY` durch einen tatsächlichen Ordnerpfad auf Ihrem Rechner.



## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Benutzerdefinierten Grafikzustand in PDF mit Aspose.Pdf erstellen](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [Grafikzustand zu PDF hinzufügen mit Aspose.PDF für .NET (C#)](/pdf/english/net/programming-with-operators/how-to-add-graphics-state-pdf-using-aspose-pdf-in-c/)
- [Leeren Grafikzustand in einem PDF mit C# erstellen](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}