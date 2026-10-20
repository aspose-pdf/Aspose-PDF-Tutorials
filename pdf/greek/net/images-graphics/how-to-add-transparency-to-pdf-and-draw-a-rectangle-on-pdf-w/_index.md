---
category: general
date: 2026-09-12
description: Μάθετε πώς να προσθέσετε διαφάνεια σε PDF, να σχεδιάσετε ένα ορθογώνιο
  σε PDF και να αποθηκεύσετε το PDF με διαφάνεια χρησιμοποιώντας το Aspose.PDF σε
  C# – βήμα‑προς‑βήμα οδηγός.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add transparency to pdf
- draw rectangle on pdf
- save pdf with transparency
language: el
lastmod: 2026-09-12
og_description: Προσθέστε διαφάνεια σε PDF, σχεδιάστε ένα ορθογώνιο σε PDF και αποθηκεύστε
  το PDF με διαφάνεια χρησιμοποιώντας το Aspose.PDF σε C#. Ακολουθήστε αυτό το πλήρες
  σεμινάριο.
og_image_alt: Screenshot of a PDF page showing a semi‑transparent rectangle drawn
  with Aspose.PDF
og_title: Προσθήκη διαφάνειας σε PDF και σχεδίαση ορθογωνίου σε PDF – πλήρης οδηγός
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-12'
  description: Learn how to add transparency to PDF, draw a rectangle on PDF, and
    save PDF with transparency using Aspose.PDF in C# – step‑by‑step guide.
  headline: How to add transparency to PDF and draw a rectangle on PDF with Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Πώς να προσθέσετε διαφάνεια σε PDF και να σχεδιάσετε ένα ορθογώνιο σε PDF με
  το Aspose.PDF
url: /el/net/images-graphics/how-to-add-transparency-to-pdf-and-draw-a-rectangle-on-pdf-w/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να προσθέσετε διαφάνεια σε PDF και να σχεδιάσετε ένα ορθογώνιο σε PDF με το Aspose.PDF

Αν χρειάζεστε **προσθήκη διαφάνειας σε PDF** αρχεία, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε σε C#. Θα μάθετε επίσης πώς να **σχεδιάσετε ορθογώνιο σε PDF** και τελικά **αποθηκεύσετε PDF με διαφάνεια**, ώστε το αποτέλεσμα να μπορεί να επαναχρησιμοποιηθεί σε αναφορές, τιμολόγια ή οποιαδήποτε ροή εργασίας αυτοματοποίησης εγγράφων.

Σε αυτό το tutorial θα:

* Φορτώσετε ένα υπάρχον PDF έγγραφο.
* Δημιουργήσετε μια προσαρμοσμένη κατάσταση γραφικών που ορίζει τη διαφάνεια περιγράμματος και γεμίσματος.
* Εφαρμόσετε αυτήν την κατάσταση γραφικών στον καμβά και σχεδιάσετε ένα ορθογώνιο.
* Αποθηκεύσετε το τροποποιημένο αρχείο διατηρώντας τις ρυθμίσεις διαφάνειας.

Δεν απαιτούνται εξωτερικά εργαλεία πέρα από τη βιβλιοθήκη Aspose.PDF for .NET, και κάθε γραμμή κώδικα εξηγείται ώστε να κατανοείτε *γιατί* κάθε βήμα είναι σημαντικό.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+).
* Ένα αδειοδοτημένο ή δοκιμαστικό αντίγραφο του **Aspose.PDF for .NET**. Εγκαταστήστε το μέσω NuGet:

```bash
dotnet add package Aspose.Pdf
```

* Ένα αρχείο PDF εισόδου (`input.pdf`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από το πρόγραμμά σας.

## Βήμα 1: Φόρτωση του PDF εγγράφου

Η πρώτη ενέργεια είναι το άνοιγμα του πηγαίου αρχείου. Η χρήση της δήλωσης `using` εγγυάται ότι το έγγραφο θα αποδεσμευτεί σωστά, αποτρέποντας προβλήματα κλειδώματος αρχείου όταν προσπαθήσετε να το αποθηκεύσετε.

```csharp
// Step 1: Load the PDF document
string pdfPath = @"YOUR_DIRECTORY\input.pdf";
using var pdfDocument = new Aspose.Pdf.Document(pdfPath);
```

*Γιατί είναι σημαντικό*: Η φόρτωση του εγγράφου σας δίνει πρόσβαση στη συλλογή σελίδων, στα λεξικά πόρων και στα αντικείμενα καμβά που απαιτούνται για το σχεδιασμό.

## Βήμα 2: Πρόσβαση στο λεξικό πόρων της πρώτης σελίδας

Κάθε σελίδα PDF διαθέτει ένα **λεξικό πόρων** που αποθηκεύει αντικείμενα όπως γραμματοσειρές, εικόνες και καταστάσεις γραφικών. Για να εισάγουμε μια νέα ρύθμιση διαφάνειας, πρέπει να επεξεργαστούμε την καταχώρηση `ExtGState`.

```csharp
// Step 2: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];               // PDF pages are 1‑based
var resourcesEditor = new Aspose.Pdf.DictionaryEditor(firstPage.Resources);
```

*Γιατί είναι σημαντικό*: Ο `DictionaryEditor` μας επιτρέπει να διαβάζουμε και να τροποποιούμε αντικείμενα PDF χαμηλού επιπέδου χωρίς να διασπάμε τη δομή του εγγράφου.

## Βήμα 3: Δημιουργία προσαρμοσμένης κατάστασης γραφικών με τιμές διαφάνειας

Μια κατάσταση γραφικών (`ExtGState`) ελέγχει πώς αποδίδονται οι λειτουργίες σχεδίασης. Ορίζουμε δύο παραμέτρους διαφάνειας:

* **CA** – διαφάνεια περιγράμματος (stroke opacity).
* **ca** – διαφάνεια γεμίσματος (fill opacity).

Ορίζουμε επίσης τη λειτουργία ανάμειξης (`BM`) σε “Normal”, η οποία είναι η πιο κοινή λειτουργία σύνθεσης.

```csharp
// Step 3: Create a custom graphics state (ExtGState) with transparency settings
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
var customGs = Aspose.Pdf.Cos.CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

var parameters = new[]
{
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "CA", new Aspose.Pdf.Cos.CosPdfNumber(1)),          // stroke opacity = 100 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "ca", new Aspose.Pdf.Cos.CosPdfNumber(0.5)),        // fill opacity = 50 %
    new KeyValuePair<string, Aspose.Pdf.ICosPdfPrimitive>(
        "BM", new Aspose.Pdf.Cos.CosPdfName("Normal"))      // normal blend mode
};

foreach (var p in parameters)
    customGs.Add(p);

// Register the new graphics state under the name "GS0"
extGStateDict.Add("GS0", customGs);
```

*Γιατί είναι σημαντικό*: Προσθέτοντας το `GS0` στο λεξικό `ExtGState` δημιουργούμε μια επαναχρησιμοποιήσιμη αναφορά που ο καμβάς μπορεί να ενεργοποιήσει πριν το σχεδιασμό. Η διαφάνεια γεμίσματος `0.5` κάνει το ορθογώνιο ημιδιαφανές, επιτυγχάνοντας τον στόχο **προσθήκης διαφάνειας σε PDF**.

## Βήμα 4: Εφαρμογή της κατάστασης γραφικών και σχεδίαση ορθογωνίου

Τώρα λέμε στον καμβά της σελίδας να χρησιμοποιήσει την κατάσταση γραφικών που μόλις δημιουργήσαμε, και στη συνέχεια σχεδιάζουμε ένα ορθογώνιο. Οι συντεταγμένες ακολουθούν το σύστημα συντεταγμένων PDF (αρχή στην κάτω‑αριστερή γωνία).

```csharp
// Step 4: Apply the custom graphics state and draw a rectangle
var canvas = firstPage.Canvas;

// Activate the transparency graphics state
canvas.SetGraphicsState("GS0");

// Draw a rectangle from (100, 500) to (200, 600)
canvas.Rectangle(100, 500, 200, 600);

// Render the rectangle outline using the current graphics state
canvas.Stroke();
```

*Γιατί είναι σημαντικό*: Η `SetGraphicsState("GS0")` αλλάζει το περιβάλλον σχεδίασης στις ρυθμίσεις διαφάνειας που ορίστηκαν νωρίτερα. Η μέθοδος `Rectangle` ορίζει το σχήμα, και η `Stroke` αποδίδει το περίγραμμα με τη συγκεκριμένη διαφάνεια. Αν θέλετε επίσης γεμισμένο ορθογώνιο, αντικαταστήστε το `Stroke()` με `FillAndStroke()`.

## Βήμα 5: Αποθήκευση του τροποποιημένου PDF δια διατήρησης της διαφάνειας

Τέλος, γράψτε το έγγραφο πίσω στο δίσκο. Το αρχείο εξόδου περιέχει τη νέα κατάσταση γραφικών, το σχεδιασμένο ορθογώνιο και τις πληροφορίες διαφάνειας.

```csharp
// Step 5: Save the modified PDF
string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
pdfDocument.Save(outputPath);
```

*Γιατί είναι σημαντικό*: Η αποθήκευση του εγγράφου ολοκληρώνει όλες τις αλλαγές. Το προκύπτον αρχείο μπορεί να ανοιχθεί σε οποιονδήποτε προβολέα PDF, και το ορθογώνιο θα εμφανίζεται με 50 % διαφάνεια γεμίσματος.

### Αναμενόμενο αποτέλεσμα

Όταν ανοίξετε το `output_with_extgstate.pdf` θα δείτε ένα ορθογώνιο του οποίου το περίγραμμα είναι πλήρως αδιαφανές και το εσωτερικό του ημιδιαφανές, επιτρέποντας στο υποκείμενο περιεχόμενο της σελίδας να φαίνεται.

## Περιπτώσεις άκρων και πρακτικές συμβουλές

| Κατάσταση | Συνιστώμενη προσαρμογή |
|-----------|------------------------|
| **Πολλές σελίδες** | Επανάληψη μέσω `pdfDocument.Pages` και επανάληψη των βημάτων 2‑4 για κάθε στοχευμένη σελίδα. |
| **Διαφορετικές τιμές διαφάνειας** | Αλλάξτε τις τιμές `CosPdfNumber` για `CA` (stroke) και `ca` (fill) σε οποιονδήποτε αριθμό μεταξύ `0` (πλήρως διαφανές) και `1` (πλήρως αδιαφανές). |
| **Προσαρμοσμένες λειτουργίες ανάμειξης** | Αντικαταστήστε το `"Normal"` με `"Multiply"`, `"Screen"` ή οποιαδήποτε λειτουργία ανάμειξης PDF‑standard που υποστηρίζεται από τον προβολέα σας. |
| **Γεμισμένο ορθογώνιο** | Καλέστε `canvas.FillAndStroke()` αντί για `canvas.Stroke()` για να εφαρμόσετε τόσο το γέμισμα όσο και το περίγραμμα. |
| **Επαναχρησιμοποίηση της ίδιας κατάστασης γραφικών** | Μπορείτε να καλέσετε `canvas.SetGraphicsState("GS0")` πριν σχεδιάσετε όποιον αριθμό σχημάτων στην ίδια σελίδα. |

**Συμβουλή:** Ελέγχετε πάντα το λεξικό πόρων μετά την προσθήκη ενός νέου `ExtGState`. Αν το λεξικό δεν υπάρχει, δημιουργήστε το πρώτα:

```csharp
if (!resourcesEditor.ContainsKey("ExtGState"))
    resourcesEditor.Add("ExtGState", new Aspose.Pdf.Cos.CosPdfDictionary(pdfDocument));
```

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε σε μια εφαρμογή κονσόλας και να εκτελέσετε αμέσως (αντικαταστήστε το `YOUR_DIRECTORY` με πραγματική διαδρομή).

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the PDF document
        string pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Access the first page’s resources
        var firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // Ensure ExtGState dictionary exists
        if (!resourcesEditor.ContainsKey("ExtGState"))
            resourcesEditor.Add("ExtGState", new CosPdfDictionary(pdfDocument));

        // 3️⃣ Create a custom graphics state with transparency
        var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        var customGs = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

        var parameters = new[]
        {
            new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),   // stroke opacity
            new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // fill opacity
            new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
        };

        foreach (var p in parameters)
            customGs.Add(p);

        extGStateDict.Add("GS0", customGs);

        // 4️⃣ Apply the graphics state and draw a rectangle
        var canvas = firstPage.Canvas;
        canvas.SetGraphicsState("GS0");
        canvas.Rectangle(100, 500, 200, 600);
        canvas.Stroke(); // use FillAndStroke() for a filled shape

        // 5️⃣ Save the PDF with transparency
        string outputPath = @"YOUR_DIRECTORY\output_with_extgstate.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine("PDF saved with a transparent rectangle at: " + outputPath);
    }
}
```

Η εκτέλεση του προγράμματος παράγει το `output_with_extgstate.pdf`, το οποίο επιδεικνύει **προσθήκη διαφάνειας σε PDF**, **σχεδίαση ορθογωνίου σε PDF**, και **αποθήκευση PDF με διαφάνεια** όλα σε μία ροή.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **προσθέσετε διαφάνεια σε PDF** αρχεία, να **σχεδιάσετε ορθογώνιο σε PDF**, και να **αποθηκεύσετε PDF με διαφάνεια** χρησιμοποιώντας το Aspose.PDF for .NET. Η διαδικασία περιστρέφεται γύρω από τη δημιουργία μιας προσαρμοσμένης `ExtGState`, την εφαρμογή της στον καμβά, και την αποθήκευση των αλλαγών. Με αυτά τα δομικά στοιχεία μπορείτε να επεκτείνετε την τεχνική σε άλλα σχήματα, πολλαπλές σελίδες ή δυναμικές τιμές διαφάνειας.

**Επόμενα βήματα**

* Εξερευνήστε άλλα primitives σχεδίασης όπως `canvas.Ellipse`, `canvas.Path`, ή `canvas.TextFragment` ενώ επαναχρησιμοποιείτε την ίδια κατάσταση γραφικών.
* Συνδυάστε τη διαφάνεια με επικάλυψη εικόνων για να δημιουργήσετε υδατογραφήματα (`canvas.Image` + προσαρμοσμένο `ExtGState`).
* Ανασκοπήστε την τεκμηρίωση Aspose.PDF σχετικά με **παραμέτρους κατάστασης γραφικών** για προχωρημένα εφέ σύνθεσης.

Καλή προγραμματιστική δουλειά, και απολαύστε την οπτική ευελιξία που προσφέρει η διαφάνεια στις ροές εργασίας PDF σας!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση στα δικά σας έργα.

- [How to Create PDF in C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)
- [How to Add a Line Object in PDF Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Add Image Stamps to PDFs Using Aspose.PDF for .NET: A Step-by-Step Guide](/pdf/english/net/images-graphics/add-image-stamp-to-pdf-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}