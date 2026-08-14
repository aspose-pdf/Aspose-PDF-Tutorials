---
category: general
date: 2026-08-14
description: Δημιουργήστε γρήγορα πεδίο φόρμας PDF με C#. Μάθετε πώς να προσθέσετε
  πλαίσιο κειμένου σε PDF και να τροποποιήσετε το PDF ώστε να περιλαμβάνει πλαίσιο
  κειμένου χρησιμοποιώντας το Aspose.PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf form field
- add text box to pdf
- modify pdf to include text box
- Aspose.PDF form field
- C# PDF manipulation
language: el
lastmod: 2026-08-14
og_description: Δημιουργήστε πεδίο φόρμας PDF με C#. Αυτό το σεμινάριο δείχνει πώς
  να προσθέσετε ένα πλαίσιο κειμένου σε ένα PDF και να τροποποιήσετε ένα PDF ώστε
  να περιλαμβάνει ένα πλαίσιο κειμένου χρησιμοποιώντας το Aspose.PDF.
og_image_alt: Screenshot of a PDF page showing a newly added text box form field
og_title: Δημιουργία πεδίου φόρμας PDF σε C# – πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create pdf form field quickly with C#. Learn how to add text box to
    pdf and modify pdf to include text box using Aspose.PDF.
  headline: Create pdf form field in C# – step‑by‑step guide
  type: TechArticle
- description: Create pdf form field quickly with C#. Learn how to add text box to
    pdf and modify pdf to include text box using Aspose.PDF.
  name: Create pdf form field in C# – step‑by‑step guide
  steps:
  - name: Load the existing PDF document.
    text: Load the existing PDF document.
  - name: Instantiate a `TextBoxField` and configure its name and appearance.
    text: Instantiate a `TextBoxField` and configure its name and appearance.
  - name: Add a widget annotation that defines the visual rectangle on the target
      page.
    text: Add a widget annotation that defines the visual rectangle on the target
      page.
  - name: Insert the field into the document’s form collection.
    text: Insert the field into the document’s form collection.
  - name: Save the modified PDF.
    text: Save the modified PDF.
  - name: Open `output.pdf` in Adobe Acrobat Reader.
    text: Open `output.pdf` in Adobe Acrobat Reader.
  - name: Click inside the “Comments” box; the cursor should appear.
    text: Click inside the “Comments” box; the cursor should appear.
  - name: Type any text and press **Tab** or click elsewhere.
    text: Type any text and press **Tab** or click elsewhere.
  - name: Choose **File → Save As** to persist the entered value.
    text: Choose **File → Save As** to persist the entered value.
  - name: '(Optional) Use Aspose.PDF’s `Form` API to extract the value programmatically:'
    text: '(Optional) Use Aspose.PDF’s `Form` API to extract the value programmatically:'
  type: HowTo
tags:
- pdf
- csharp
- form-fields
title: Δημιουργία πεδίου φόρμας PDF σε C# – οδηγός βήμα‑προς‑βήμα
url: /el/net/programming-with-forms/create-pdf-form-field-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία πεδίου φόρμας pdf σε C# – οδηγός βήμα‑βήμα

Αν χρειάζεστε **create pdf form field** σε ένα έγγραφο, αυτός ο οδηγός σας καθοδηγεί σε όλη τη διαδικασία. Θα δείτε ακριβώς πώς να **add text box to pdf** σε σελίδες, και πώς να **modify pdf to include text box** χρησιμοποιώντας τη βιβλιοθήκη Aspose.PDF για .NET.

Η εργασία με φόρμες PDF είναι συχνή απαίτηση για συστήματα τιμολόγησης, έρευνες ή οποιαδήποτε ροή εργασίας που συλλέγει εισροές χρηστών. Στο τέλος αυτού του tutorial, θα έχετε ένα επαναχρησιμοποιήσιμο απόσπασμα κώδικα που δημιουργεί ένα πλήρως λειτουργικό πεδίο πλαισίου κειμένου, το τοποθετεί όπου θέλετε και αποθηκεύει το ενημερωμένο PDF—όλα χωρίς να αφήσετε το έργο C#.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+)
* Visual Studio 2022 ή οποιοδήποτε IDE που υποστηρίζει C#
* Ένα ενεργό license του Aspose.PDF for .NET (η δωρεάν δοκιμή λειτουργεί για ανάπτυξη)
* Ένα αρχείο PDF με όνομα `input.pdf` τοποθετημένο σε γνωστό φάκελο (το tutorial χρησιμοποιεί το `YOUR_DIRECTORY` ως placeholder)

> **Pro tip:** Αν δεν έχετε ακόμη άδεια, μπορείτε να ζητήσετε ένα προσωρινό κλειδί από την ιστοσελίδα της Aspose· η βιβλιοθήκη λειτουργεί σε λειτουργία αξιολόγησης χωρίς αλλαγές κώδικα.

## Πώς να δημιουργήσετε pdf form field σε C# (επισκόπηση)

1. Φορτώστε το υπάρχον έγγραφο PDF.  
2. Δημιουργήστε ένα `TextBoxField` και ρυθμίστε το όνομα και την εμφάνισή του.  
3. Προσθέστε μια widget annotation που ορίζει το οπτικό ορθογώνιο στην επιλεγμένη σελίδα.  
4. Εισάγετε το πεδίο στη συλλογή φορμών του εγγράφου.  
5. Αποθηκεύστε το τροποποιημένο PDF.

Κάθε βήμα εξηγείται λεπτομερώς παρακάτω, με πλήρη παραδείγματα κώδικα και τη λογική πίσω από τις κλήσεις API.

## Βήμα 1: Φόρτωση του εγγράφου PDF

Η πρώτη ενέργεια είναι η ανάγνωση του πηγαίου PDF. Η Aspose.PDF αντιπροσωπεύει ένα αρχείο PDF με την κλάση `Document`. Η φόρτωση του εγγράφου σας δίνει πρόσβαση στις σελίδες, τη συλλογή φορμών και άλλες δομές.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

// Adjust the path to match your environment
string inputPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");

// Load the PDF you want to modify
Document pdfDocument = new Document(inputPath);
```

**Γιατί αυτό είναι σημαντικό:**  
Η φόρτωση του αρχείου δημιουργεί ένα μοντέλο PDF στη μνήμη, επιτρέποντάς σας να προσθέτετε, να αφαιρείτε ή να επεξεργάζεστε αντικείμενα χωρίς να καταστρέψετε το αρχικό αρχείο. Το αντικείμενο `Document` εκθέτει επίσης την ιδιότητα `Form`, όπου αργότερα θα **add text box to pdf**.

## Βήμα 2: Δημιουργία πεδίου πλαισίου κειμένου

Ένα πεδίο πλαισίου κειμένου είναι ένας τύπος πεδίου φόρμας που επιτρέπει στους χρήστες να πληκτρολογούν ελεύθερο κείμενο. Στην Aspose.PDF το δημιουργείτε με την δημιουργία ενός `TextBoxField`, περνώντας τη σελίδα-στόχο και ένα ορθογώνιο που ορίζει το αρχικό μέγεθος του widget.

```csharp
// Choose the page index (0‑based). Here we use page 2 (index 1).
Page targetPage = pdfDocument.Pages[1];

// Define the rectangle for the field’s *initial* size.
// Rectangle(left, bottom, right, top) – values are in points (1/72 inch).
Rectangle fieldRect = new Rectangle(100, 500, 200, 530);

// Create the TextBoxField with a partial name that will be used in form data.
TextBoxField textBox = new TextBoxField(targetPage, fieldRect)
{
    PartialName = "Comments", // This identifier appears in the PDF form data.
    // Optional: set default appearance (font, size, color)
    DefaultAppearance = new DefaultAppearance(FontRepository.FindFont("Helvetica"), 12, Color.Black)
};
```

**Γιατί αυτό είναι σημαντικό:**  
* Το `PartialName` είναι το κλειδί που τα εργαλεία επεξεργασίας φορμών (π.χ. Adobe Acrobat, server‑side parsers) χρησιμοποιούν για να ανακτήσουν την καταχωρημένη τιμή.  
* Το ορθογώνιο που περνάτε εδώ ορίζει μόνο το *αρχικό* μέγεθος του widget· μπορείτε αργότερα να προσαρμόσετε τη θέση του με μια widget annotation (επόμενο βήμα).  
* Η ρύθμιση του `DefaultAppearance` εξασφαλίζει ότι το κείμενο μέσα στο πλαίσιο εμφανίζεται σταθερά σε όλους τους προβολείς.

## Βήμα 3: Ορισμός της οπτικής widget annotation

Ένα πεδίο φόρμας μπορεί να έχει μία ή περισσότερες **widget annotations** που ελέγχουν πού εμφανίζεται το πεδίο σε κάθε σελίδα. Προσθέτοντας ένα widget μπορείτε να τοποθετήσετε το ίδιο λογικό πεδίο σε διαφορετική θέση ή ακόμη και σε πολλαπλές σελίδες.

```csharp
// Define where the field will actually be displayed on the page.
// This rectangle can differ from the one used in the constructor.
Rectangle widgetRect = new Rectangle(100, 300, 200, 330);
textBox.AddWidgetAnnotation(widgetRect);
```

**Γιατί αυτό είναι σημαντικό:**  
Το ορθογώνιο του widget καθορίζει τις συντεταγμένες στην οθόνη που βλέπουν οι χρήστες. Αν παραλείψετε αυτό το βήμα, το πεδίο μπορεί να υπάρχει στη δομή δεδομένων του PDF αλλά δεν θα είναι ορατό στον τελικό χρήστη. Η προσθήκη widget είναι το βήμα που πραγματικά **adds text box to pdf**.

## Βήμα 4: Προσθήκη του ρυθμισμένου πεδίου στη φόρμα του εγγράφου

Τώρα που το `TextBoxField` είναι πλήρως ρυθμισμένο, πρέπει να το καταχωρίσετε στη συλλογή φορμών του PDF. Αυτό κάνει το πεδίο μέρος της διαδραστικής φόρμας και εξασφαλίζει ότι θα αποθηκευτεί.

```csharp
pdfDocument.Form.Add(textBox);
```

**Γιατί αυτό είναι σημαντικό:**  
Χωρίς την προσθήκη του πεδίου στο `pdfDocument.Form`, ο προβολέας PDF θα αγνοήσει την widget annotation, και τα δεδομένα του πεδίου δεν θα υποβληθούν ποτέ. Αυτή η γραμμή ολοκληρώνει τη λειτουργία **modify pdf to include text box**.

## Βήμα 5: Αποθήκευση του ενημερωμένου PDF

Τέλος, γράψτε τις αλλαγές πίσω στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή να δημιουργήσετε ένα νέο· το παράδειγμα αποθηκεύει στο `output.pdf`.

```csharp
string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");

// Save the document with the new form field
pdfDocument.Save(outputPath);
```

Όταν ανοίξετε το `output.pdf` στο Adobe Acrobat Reader, θα δείτε ένα ορθογώνιο πλαίσιο κειμένου με ετικέτα “Comments” στη σελίδα 2. Οι χρήστες μπορούν να κάνουν κλικ μέσα, να πληκτρολογήσουν, και το κείμενο που εισήχθη θα αποτελεί μέρος των δεδομένων φόρμας PDF.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι ένα πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντιγράψτε το σε ένα νέο κονσολικό project, αντικαταστήστε το `YOUR_DIRECTORY` με πραγματική διαδρομή φακέλου και τρέξτε.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.Drawing; // For Color

namespace PdfFormFieldDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the existing PDF
            string inputPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");
            Document pdfDocument = new Document(inputPath);

            // 2️⃣ Create a TextBoxField on page 2 (index 1)
            Page targetPage = pdfDocument.Pages[1];
            Rectangle fieldRect = new Rectangle(100, 500, 200, 530);
            TextBoxField textBox = new TextBoxField(targetPage, fieldRect)
            {
                PartialName = "Comments",
                DefaultAppearance = new DefaultAppearance(
                    FontRepository.FindFont("Helvetica"), 12, Color.Black)
            };

            // 3️⃣ Add a widget annotation to control visual placement
            Rectangle widgetRect = new Rectangle(100, 300, 200, 330);
            textBox.AddWidgetAnnotation(widgetRect);

            // 4️⃣ Register the field with the document's form collection
            pdfDocument.Form.Add(textBox);

            // 5️⃣ Save the modified PDF
            string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");
            pdfDocument.Save(outputPath);

            Console.WriteLine("PDF form field created successfully.");
            Console.WriteLine($"Output saved to: {outputPath}");
        }
    }
}
```

**Αναμενόμενη έξοδος:**  
Η εκτέλεση του προγράμματος εκτυπώνει δύο γραμμές επιβεβαίωσης στην κονσόλα. Το άνοιγμα του `output.pdf` εμφανίζει ένα πλαίσιο κειμένου στη σελίδα 2 όπου ο χρήστης μπορεί να γράψει σχόλια. Όταν η φόρμα υποβληθεί (π.χ. μέσω του κουμπιού “Submit” του Adobe Acrobat), το όνομα πεδίου `Comments` εμφανίζεται στα εξαγόμενα δεδομένα FDF ή XFDF.

## Κοινές παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Πώς να προσαρμόσετε τον κώδικα |
|-----------|-------------------------------|
| **Προσθήκη του πεδίου σε διαφορετική σελίδα** | Αλλάξτε το `pdfDocument.Pages[1]` στον επιθυμητό δείκτη σελίδας (`0`‑based). |
| **Δημιουργία πλαισίου κειμένου πολλαπλών γραμμών** | Ορίστε `textBox.Multiline = true;` πριν προσθέσετε το widget. |
| **Ορισμός προεπιλεγμένης τιμής** | Αναθέστε `textBox.Value = "Enter your comments here";`. |
| **Κάνοντας το πεδίο υποχρεωτικό** | Ορίστε `textBox.Required = true;`. |
| **Τοποθέτηση του πεδίου σε πολλαπλές σελίδες** | Καλέστε `textBox.AddWidgetAnnotation` για κάθε επιπλέον ορθογώνιο στις στόχες σελίδες. |
| **Χρήση προσαρμοσμένης γραμματοσειράς** | Φορτώστε τη γραμματοσειρά με `FontRepository.AddFont("path/to/font.ttf")` και αναφερθείτε σε αυτήν στο `DefaultAppearance`. |

**Pro tip:** Πάντα να επαληθεύετε τις συντεταγμένες του ορθογωνίου σε σχέση με το μέγεθος της σελίδας (`pdfDocument.Pages[1].Rect`). Αν το widget βρίσκεται εκτός των ορίων της σελίδας, οι προβολείς μπορεί να το κόψουν ή να το κρύψουν.

## Δοκιμή του πεδίου φόρμας

1. Ανοίξτε το `output.pdf` στο Adobe Acrobat Reader.  
2. Κάντε κλικ μέσα στο πλαίσιο “Comments”; ο κέρσορας πρέπει να εμφανιστεί.  
3. Πληκτρολογήστε οποιοδήποτε κείμενο και πατήστε **Tab** ή κάντε κλικ αλλού.  
4. Επιλέξτε **File → Save As** για να αποθηκεύσετε την καταχωρημένη τιμή.  
5. (Προαιρετικά) Χρησιμοποιήστε το API `Form` της Aspose.PDF για να εξάγετε την τιμή προγραμματιστικά:

```csharp
string commentValue = pdfDocument.Form["Comments"].Value;
Console.WriteLine($"Submitted comment: {commentValue}");
```

Αυτό το απόσπασμα δείχνει ότι το πεδίο είναι όχι μόνο ορατό, αλλά και ανακτήσιμο μέσω κώδικα—σημαντικό για επεξεργασία από τον server.

## Συμπέρασμα

Τώρα ξέρετε πώς να **create pdf form field** σε C# από την αρχή μέχρι το τέλος. Το tutorial κάλυψε τη φόρτωση PDF, τη ρύθμιση ενός `TextBoxField`, την προσθήκη widget annotation, την καταχώριση του πεδίου και την αποθήκευση του αποτελέσματος. Με αυτά τα δομικά στοιχεία μπορείτε να **add text box to pdf** έγγραφα, **modify pdf to include text box**, και να επεκτείνετε την προσέγγιση σε άλλους τύπους πεδίων όπως checkboxes, radio buttons ή dropdowns.

Στη συνέχεια, εξερευνήστε σχετικές θεματικές όπως **extracting form data**, **flattening PDF forms**, ή **styling fields with borders and colors**. Κάθε μία από αυτές τις έννοιες βασίζεται στο ίδιο βασικό API που μόλις μάθατε, επιτρέποντάς σας να δημιουργήσετε σύνθετα διαδραστικά PDFs εξ ολοκλήρου σε C#.

Καλή προγραμματιστική, και μη διστάσετε να πειραματιστείτε με διαφορετικά ορθογώνια, γραμματοσειρές και κανόνες επικύρωσης ώστε να ταιριάζουν στις ανάγκες της εφαρμογής σας!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Create PDF Document with Aspose – Add Page, Text Box, and Form](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)
- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [How to Add a Text Stamp to PDF Using Aspose.PDF .NET: Comprehensive Guide](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}