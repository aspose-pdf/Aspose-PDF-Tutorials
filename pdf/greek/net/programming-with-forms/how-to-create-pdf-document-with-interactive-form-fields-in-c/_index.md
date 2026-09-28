---
category: general
date: 2026-09-27
description: Δημιουργήστε έγγραφο PDF και προσθέστε σελίδες στο PDF ενώ δημιουργείτε
  μια διαδραστική φόρμα PDF. Μάθετε πώς να προσθέσετε TextBox στο PDF και να δημιουργήσετε
  AcroForm PDF με το Aspose.Pdf.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add pages to pdf
- create interactive pdf form
- how to add textbox to pdf
- how to create acroform pdf
language: el
lastmod: 2026-09-27
og_description: Δημιουργήστε έγγραφο PDF και προσθέστε σελίδες στο PDF ενώ δημιουργείτε
  μια διαδραστική φόρμα PDF. Ακολουθήστε αυτόν τον οδηγό για να μάθετε πώς να προσθέσετε
  TextBox στο PDF και να δημιουργήσετε AcroForm PDF χρησιμοποιώντας το Aspose.Pdf.
og_image_alt: Screenshot showing a PDF document with a textbox field on two pages
og_title: Δημιουργία εγγράφου PDF με διαδραστικά πεδία φόρμας – βήμα‑βήμα οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: create PDF document and add pages to PDF while building an interactive
    PDF form. Learn how to add TextBox to PDF and create AcroForm PDF with Aspose.Pdf.
  headline: How to create PDF document with interactive form fields in C#
  type: TechArticle
- description: create PDF document and add pages to PDF while building an interactive
    PDF form. Learn how to add TextBox to PDF and create AcroForm PDF with Aspose.Pdf.
  name: How to create PDF document with interactive form fields in C#
  steps:
  - name: '**Create PDF document** and add the needed pages.'
    text: '**Create PDF document** and add the needed pages.'
  - name: '**Initialize AcroForm** and define a `TextBoxField`.'
    text: '**Initialize AcroForm** and define a `TextBoxField`.'
  - name: '**Add widget annotations** on each page to place the textbox.'
    text: '**Add widget annotations** on each page to place the textbox.'
  - name: '**Save** the document and test the interactive behavior.'
    text: '**Save** the document and test the interactive behavior.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF forms
title: Πώς να δημιουργήσετε έγγραφο PDF με διαδραστικά πεδία φόρμας σε C#
url: /el/net/programming-with-forms/how-to-create-pdf-document-with-interactive-form-fields-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε έγγραφο PDF με διαδραστικά πεδία φόρμας σε C#

Αν χρειάζεστε **να δημιουργήσετε έγγραφο PDF** που περιέχει πολλαπλές σελίδες και μια διαδραστική φόρμα, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα περάσουμε από την προσθήκη σελίδων στο PDF, τη δημιουργία ενός AcroForm και την τοποθέτηση ενός πεδίου TextBox σε κάθε σελίδα χρησιμοποιώντας το Aspose.Pdf για .NET.

Θα ολοκληρώσετε με ένα ενιαίο αρχείο PDF που επιτρέπει στους χρήστες να πληκτρολογούν σχόλια και στις δύο σελίδες. Χωρίς εξωτερικά εργαλεία, μόνο με λίγες γραμμές C# και τη δυνατή βιβλιοθήκη Aspose.Pdf.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+)
* Ένα έγκυρο license του Aspose.Pdf for .NET ή προσωρινό κλειδί αξιολόγησης
* Visual Studio 2022 (ή οποιοδήποτε IDE που υποστηρίζει C#)
* Βασική εξοικείωση με τη σύνταξη C# και τις αντικειμενοστραφείς έννοιες

> **Συμβουλή:** Αν χρησιμοποιείτε τη δωρεάν δοκιμή, θυμηθείτε να ορίσετε το αντικείμενο `License` νωρίς στο πρόγραμμα σας για να αποφύγετε τα υδατογραφήματα αξιολόγησης.

## Βήμα 1: Ρύθμιση του έργου και εισαγωγή namespaces

Create a new console application and add the Aspose.Pdf NuGet package:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
dotnet add package Aspose.Pdf
```

In `Program.cs` import the required namespaces:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Forms;
```

Αυτά τα namespaces σας δίνουν πρόσβαση στα βασικά αντικείμενα PDF, τους τύπους annotation και τις κλάσεις πεδίων φόρμας που απαιτούνται για το tutorial.

## Βήμα 2: Δημιουργία εγγράφου PDF και προσθήκη σελίδων στο PDF

The first functional step is to **create PDF document** and then **add pages to PDF**. Each page will host the same TextBox field.

```csharp
// Initialize a new PDF document
var pdfDocument = new Document();

// Add two blank pages
var firstPage = pdfDocument.Pages.Add();
var secondPage = pdfDocument.Pages.Add();
```

*Γιατί είναι σημαντικό:*  
`Document` αντιπροσωπεύει ολόκληρο το αρχείο PDF. Η ρητή προσθήκη σελίδων εξασφαλίζει ότι έχετε έναν καμβά για την τοποθέτηση widgets φόρμας. Μπορείτε να προσθέσετε όσες σελίδες χρειάζεστε· το παράδειγμα χρησιμοποιεί δύο για σαφήνεια.

## Βήμα 3: Δημιουργία διαδραστικής φόρμας PDF (AcroForm)

An **interactive PDF form** is built on an AcroForm object that lives inside the `Document`. We’ll create a single `TextBoxField` that will be shared across both pages.

```csharp
// Initialize the AcroForm if it doesn't exist
if (!pdfDocument.AcroForm.IsPresent)
{
    pdfDocument.AcroForm = new AcroForm(pdfDocument);
}

// Create a TextBox field named "Comments"
var textBoxField = new TextBoxField(pdfDocument.AcroForm)
{
    Name = "Comments",
    // Optional: set default appearance (font size, color)
    DefaultAppearance = new DefaultAppearance("Helvetica", 12, Color.Black)
};
```

*Γιατί είναι σημαντικό:*  
Το κοντέινερ AcroForm περιέχει όλα τα διαδραστικά στοιχεία. Δημιουργώντας ένα μόνο `TextBoxField`, μπορούμε να επαναχρησιμοποιήσουμε το ίδιο λογικό πεδίο σε πολλαπλές σελίδες, διατηρώντας τα δεδομένα συγχρονισμένα όταν ο χρήστης το συμπληρώνει.

## Βήμα 4: Πώς να προσθέσετε TextBox στο PDF – τοποθέτηση widget annotations

A **widget annotation** links a visual rectangle on a page to the logical form field. We’ll add one widget on each page.

```csharp
// Widget on the first page (coordinates: lower‑left X,Y – upper‑right X,Y)
var firstPageWidget = new WidgetAnnotation(
    firstPage,
    new Rectangle(50, 700, 200, 750))
{
    Parent = textBoxField,
    // Optional visual properties
    HighlightingMode = HighlightingMode.Invert,
    Border = new Border(BorderStyle.Solid, 1, Color.Black)
};

// Widget on the second page, positioned slightly lower
var secondPageWidget = new WidgetAnnotation(
    secondPage,
    new Rectangle(50, 600, 200, 650))
{
    Parent = textBoxField,
    HighlightingMode = HighlightingMode.Invert,
    Border = new Border(BorderStyle.Solid, 1, Color.Black)
};
```

*Γιατί είναι σημαντικό:*  
Το `WidgetAnnotation` καθορίζει πού εμφανίζεται το textbox και πώς φαίνεται. Αναθέτοντας το ίδιο `Parent` (`textBoxField`), και τα δύο widgets αναφέρονται στο ίδιο υποκείμενο πεδίο δεδομένων. Οι χρήστες που πληκτρολογούν σε ένα widget θα δουν την ίδια τιμή στην άλλη σελίδα.

## Βήμα 5: Αποθήκευση του PDF και επαλήθευση του αποτελέσματος

Finally, write the document to disk:

```csharp
// Save the PDF to the output folder
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);

Console.WriteLine($"PDF saved to {outputPath}");
```

When you open `output.pdf` in Adobe Acrobat Reader:

* Το έγγραφο εμφανίζει δύο σελίδες.
* Κάθε σελίδα περιέχει ένα textbox με ετικέτα “Comments”.
* Η πληκτρολόγηση στο textbox σε οποιαδήποτε σελίδα ενημερώνει αμέσως το άλλο (μοιράζονται το ίδιο όνομα πεδίου).

### Αναμενόμενο στιγμιότυπο εξόδου

![PDF με textbox σε δύο σελίδες](https://example.com/pdf-form-screenshot.png "δημιουργία εγγράφου PDF με διαδραστικά πεδία φόρμας")

*(Το κείμενο alt της εικόνας περιέχει τη βασική λέξη-κλειδί για προσβασιμότητα και SEO.)*

## Κοινές παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Πώς να το αντιμετωπίσετε |
|-----------|--------------------------|
| **Περισσότερες από δύο σελίδες** | Δημιουργήστε επιπλέον αντικείμενα `WidgetAnnotation` για κάθε νέα σελίδα, επαναχρησιμοποιώντας το ίδιο `textBoxField`. |
| **Διαφορετικά ονόματα πεδίων ανά σελίδα** | Δημιουργήστε ξεχωριστές εμφανίσεις `TextBoxField` (π.χ., `CommentsPage1`, `CommentsPage2`) και αναθέστε σε κάθε widget το δικό του γονέα. |
| **Πολυγραμμικό textbox** | Ορίστε `textBoxField.Multiline = true;` πριν προσθέσετε τα widgets. |
| **Πεδία μόνο για ανάγνωση** | Ορίστε `textBoxField.ReadOnly = true;` για να αποτρέψετε την επεξεργασία από τον χρήστη. |
| **Προσαρμοσμένες γραμματοσειρές** | Φορτώστε μια `TrueTypeFont` και αναθέστε την μέσω `textBoxField.DefaultAppearance = new DefaultAppearance(font, 12, Color.Black);` |

Αυτές οι παραλλαγές δείχνουν πόσο ευέλικτο είναι το AcroForm API, διατηρώντας ταυτόχρονα το βασικό μοτίβο αμετάβλητο.

## Ανακεφαλαίωση βήμα-βήμα (γρήγορη αναφορά)

1. **Δημιουργήστε έγγραφο PDF** και προσθέστε τις απαιτούμενες σελίδες.  
2. **Αρχικοποιήστε το AcroForm** και ορίστε ένα `TextBoxField`.  
3. **Προσθέστε widget annotations** σε κάθε σελίδα για να τοποθετήσετε το textbox.  
4. **Αποθηκεύστε** το έγγραφο και δοκιμάστε τη διαδραστική συμπεριφορά.

## Επόμενα βήματα

Τώρα που γνωρίζετε **πώς να προσθέσετε textbox σε PDF** και **πώς να δημιουργήσετε AcroForm PDF**, μπορείτε να επεκτείνετε τη φόρμα:

* Προσθέστε πλαίσια ελέγχου (checkboxes), κουμπιά ραδιοφώνου (radio buttons) ή λίστες πτυσσόμενων επιλογών (dropdown lists) χρησιμοποιώντας `CheckBoxField`, `RadioButtonField` και `ComboBoxField`.
* Εξάγετε τα δεδομένα της φόρμας σε FDF ή XFDF για επεξεργασία από τον διακομιστή.
* Εφαρμόστε ενέργειες JavaScript στα πεδία για δυναμική επικύρωση.

Εξερευνήστε την επίσημη τεκμηρίωση του Aspose.Pdf για μια πλήρη λίστα τύπων πεδίων φόρμας και προχωρημένες επιλογές στυλ.

---

*Έχετε μάθει πώς να **δημιουργήσετε έγγραφο PDF**, **προσθέσετε σελίδες σε PDF**, **δημιουργήσετε διαδραστική φόρμα PDF**, **πώς να προσθέσετε textbox σε PDF**, και **πώς να δημιουργήσετε AcroForm PDF** χρησιμοποιώντας ένα σύντομο, εκτελέσιμο παράδειγμα. Μη διστάσετε να πειραματιστείτε με πρόσθετους τύπους πεδίων και ρυθμίσεις διάταξης ώστε να ταιριάζουν στις ανάγκες της εφαρμογής σας.*

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα-βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να δημιουργήσετε PDF με Aspose – Προσθήκη πεδίου φόρμας και σελίδων](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Πώς να προσθέσετε Text Box σε PDF – Δημιουργία πεδίου φόρμας PDF & Αποθήκευση επεξεργασμένου εγγράφου PDF](/pdf/english/net/programming-with-forms/how-to-add-text-box-pdf-create-pdf-form-field-save-edited-pd/)
- [Δημιουργία εγγράφου PDF με Aspose – Προσθήκη σελίδας, Text Box και φόρμα](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}