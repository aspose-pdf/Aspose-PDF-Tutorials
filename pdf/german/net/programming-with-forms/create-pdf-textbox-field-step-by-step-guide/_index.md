---
category: general
date: 2026-06-21
description: Erstellen Sie ein PDF-Textfeld mit C# und lernen Sie, wie Sie ein PDF-Formularfeld
  duplizieren oder ein Textfeld zu einem PDF-Formular hinzufügen – alles in nur wenigen
  Codezeilen.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: de
og_description: Erstellen Sie schnell ein PDF-Textfeld. Diese Anleitung zeigt, wie
  man ein PDF-Formularfeld dupliziert und ein Textfeld zu einem PDF-Formular hinzufügt,
  indem man eine moderne C#‑PDF‑Bibliothek verwendet.
og_title: PDF-Textbox-Feld erstellen – Komplettes C#‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: PDF-Textbox-Feld erstellen – Schritt‑für‑Schritt‑Anleitung
url: /de/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF-Textbox-Feld erstellen – Vollständiges C#-Tutorial

Haben Sie schon einmal ein **create PDF textbox field** erstellen müssen, waren sich aber nicht sicher, welche API‑Aufrufe Sie verwenden sollen? Sie sind nicht allein. Egal, ob Sie ein Vertrags‑Signing‑Portal oder ein einfaches Datenerfassungs‑Blatt erstellen, das Hinzufügen interaktiver Textfelder zu einem PDF ist eine Kernkompetenz für jeden Form‑Automation‑Entwickler.  

In diesem Leitfaden führen wir Sie durch ein praktisches Beispiel, das nicht nur **adds textbox to PDF form** zeigt, sondern auch, wie man **duplicate PDF form field** verwendet, sodass dieselbe Eingabe auf mehreren Seiten erscheint. Am Ende haben Sie ein ausführbares Programm, das Sie in jedes .NET‑Projekt einbinden können.

## Was Sie benötigen

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Core)  
- Eine moderne C# PDF‑Bibliothek – das untenstehende Snippet verwendet **PDFTron SDK**, aber die Konzepte lassen sich auf iText 7, PdfSharp oder andere Bibliotheken übertragen.  
- Visual Studio 2022 (oder jede andere IDE Ihrer Wahl)  

Das war's – keine zusätzlichen Dienste, keine obskuren Abhängigkeiten. Wenn Sie bereits ein PDF haben, das Sie erweitern möchten, verweisen Sie einfach im Code darauf.

---

## Schritt 1: Projekt einrichten und SDK importieren

Zuerst ein Konsolen‑App erstellen:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

PDFTron‑NuGet‑Paket hinzufügen:

```bash
dotnet add package PDFTron.NET
```

Öffnen Sie nun `Program.cs` und importieren Sie die benötigten Namespaces:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Pro‑Tipp:** Wenn Sie eine andere Bibliothek verwenden, ersetzen Sie die `using`‑Anweisungen durch die entsprechenden (z. B. `iText.Kernel.Pdf` für iText 7).

## Schritt 2: PDF‑Dokument und Formular initialisieren

Wir beginnen mit einem neuen PDF, das zwei Seiten enthält – die Quellseite für das ursprüngliche Textfeld und eine Zielseite für das Duplikat.

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

Das Objekt `Form` ist der Ort, an dem alle interaktiven Felder leben. Wenn das Dokument noch kein Formular hat, erstellt `GetForm()` eines für uns.

## Schritt 3: **Create PDF Textbox Field** auf der ersten Seite

Jetzt kommt der Kern unseres Tutorials – das Erstellen eines Textfeldes. Die Rechteckkoordinaten werden in Punkten angegeben (1 Zoll = 72 Punkte). Das Beispiel platziert das Feld nahe der oberen Mitte der ersten Seite.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

Warum setzen wir `Value` sofort? Das Vorbefüllen des Feldes gibt dem Benutzer einen Hinweis auf die erwartete Eingabe und zeigt zudem, dass das Feld voll funktionsfähig ist.

## Schritt 4: Feld zum Formular hinzufügen – **Add Textbox to PDF Form**

Als Nächstes registrieren wir das Feld im Formular mit einem logischen Namen. Dieser Name wird später verwendet, wenn Sie die Daten des Feldes programmgesteuert lesen oder ändern möchten.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Die Wahl eines klaren Namens (wie `"multiBox"`) erleichtert den späteren Code, besonders wenn Sie Dutzende von Feldern haben.

## Schritt 5: **Duplicate PDF Form Field** auf einer anderen Seite

Eine häufige Anforderung ist, dasselbe Feld auf mehreren Seiten anzuzeigen – denken Sie an ein „Kundenname“-Feld, das auf jeder Rechnungsseite erscheint. PDFTron ermöglicht das Klonen der Widget‑Annotation, die die visuelle Darstellung des Feldes ist.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

Das geklonte Widget teilt dieselben zugrunde liegenden Daten wie das ursprüngliche Textfeld. Wenn ein Benutzer in einer Instanz tippt, wird die andere automatisch aktualisiert – das ist die Magie von **duplicate PDF form field**.

## Schritt 6: Dokument speichern und Aufräumen

Abschließend das PDF auf die Festplatte schreiben und die PDFNet‑Laufzeit schließen.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

Das Ausführen des Programms erzeugt ein zweiseitiges PDF (`output.pdf`). Öffnen Sie es in Adobe Acrobat Reader, klicken Sie auf das Textfeld auf Seite 1, geben Sie etwas ein und wechseln Sie zu Seite 2 – derselbe Text erscheint sofort. Das ist ein voll funktionsfähiges **create pdf textbox field**‑Beispiel mit einem duplizierten Feld.

---

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**Erwartete Ausgabe:** Eine Datei namens `output.pdf` mit zwei Seiten. Beide Seiten zeigen dasselbe editierbare Textfeld mit der Beschriftung „Sample“. Das Bearbeiten eines Feldes aktualisiert das andere sofort.

---

## Häufige Fragen & Sonderfälle

### Was, wenn ich das Feld auf *mehr* als zwei Seiten benötige?

Wiederholen Sie einfach die Schritte Klonen‑und‑Hinzufügen für jede weitere Seite. Das zugrunde liegende Datenobjekt bleibt gleich, sodass alle Widgets synchron bleiben.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### Wie ändere ich das Aussehen (Schrift, Rand, Hintergrund)?

Jedes `Widget` verfügt über die Methoden `SetBorderColor`, `SetBorderWidth` und `SetBackgroundColor`. Sie können auch einen Standard‑Appearance‑String (`DA`) zuweisen, um Schriftart und Größe zu steuern.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### Kann ich das Feld nach der Benutzereingabe schreibgeschützt machen?

Ja. Setzen Sie das `ReadOnly`‑Flag im Feld, nachdem Sie die Daten gesammelt haben, oder schalten Sie es je nach Workflow um.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### Was ist mit PDFs, die bereits ein Formular enthalten?

Wenn das Dokument bereits ein AcroForm hat, gibt `doc.GetForm()` einfach dieses zurück. Sie können dann neue Felder hinzufügen, ohne die bestehenden zu stören. Achten Sie nur darauf, eindeutige Feldnamen zu verwenden.

## Tipps für reale Projekte

- **Naming convention:** Feldnamen mit der Seite oder dem Abschnitt voranstellen (z. B. `invoice_customer_name`), um Kollisionen zu vermeiden.  
- **Validation:** JavaScript‑Aktionen verwenden (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`), wenn clientseitige Validierung nötig ist.  
- **Performance:** Bei großen PDFs `doc.Lock()` vor Massenoperationen aufrufen, um I/O‑Overhead zu reduzieren.  
- **Accessibility:** Die Eigenschaft `AlternateName` setzen, damit Screenreader das Feld beschreiben können.

## Fazit

Wir haben gerade **created a PDF textbox field** erstellt, gezeigt, wie man **duplicate PDF form field** über Seiten hinweg dupliziert, und die einfachste Methode demonstriert, **add textbox to PDF form** mit C# hinzuzufügen. Der vollständige, ausführbare Code befindet sich oben, und Sie können ihn bei Bedarf mit Styling, Validierung oder zusätzlichen Seiten erweitern.

Bereit für den nächsten Schritt? Versuchen Sie, ein Dropdown (`ChoiceField`) oder ein Signatur‑Widget einzubetten, oder erkunden Sie, wie Sie das Formular nach der Dateneingabe für Archivierungszwecke flachlegen können. Das PDFTron SDK (oder jede vergleichbare Bibliothek) liefert die Bausteine – Ihre Vorstellungskraft bestimmt die endgültige Form.

Wenn Sie auf ein Problem stoßen, hinterlassen Sie unten einen Kommentar oder prüfen Sie die offizielle Dokumentation der Bibliothek; sie ist voll von Beispielen, die das hier behandelte ergänzen. Viel Spaß beim Programmieren und möge Ihre Formulare immer synchron bleiben!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man PDF mit Aspose erstellt – Formularfeld und Seiten hinzufügen](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Formularfeld in PDF-Dokument mit Java hinzufügen](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Formularfeld in PDF-Dokument mit Java hinzufügen](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}