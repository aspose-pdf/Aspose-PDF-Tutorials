---
category: general
date: 2026-09-05
description: Δημιουργήστε ένα έγγραφο PDF σε C# προσθέτοντας μια κενή σελίδα, σχεδιάζοντας
  ένα ορθογώνιο και αποθηκεύοντας το αρχείο PDF. Ακολουθήστε ένα βήμα‑βήμα παράδειγμα
  Aspose.PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add blank page pdf
- draw rectangle pdf
- save pdf file
- how to add rectangle
language: el
lastmod: 2026-09-05
og_description: Δημιουργήστε έγγραφο PDF σε C# προσθέτοντας μια κενή σελίδα, σχεδιάζοντας
  ένα ορθογώνιο και αποθηκεύοντας το αρχείο PDF. Ακολουθήστε αυτό το πλήρες παράδειγμα
  με το Aspose.PDF.
og_image_alt: Screenshot showing a PDF document with a drawn rectangle on a blank
  page
og_title: Δημιουργία εγγράφου PDF με κενή σελίδα και ορθογώνιο – Οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  headline: How to create PDF document with a blank page and rectangle
  type: TechArticle
- description: Create PDF document in C# by adding a blank page, drawing a rectangle,
    and saving the PDF file. Follow a step‑by‑step Aspose.PDF example.
  name: How to create PDF document with a blank page and rectangle
  steps:
  - name: 'Edge case: custom page size'
    text: 'If your layout requires a 6 × 9 inch page, replace the default call with:'
  - name: 'Pro tip: styling the rectangle'
    text: 'You can change the stroke color and line width:'
  - name: 'Edge case: overwriting existing files'
    text: 'Aspose.PDF overwrites an existing file by default. To protect previous
      outputs, check for file existence first:'
  - name: Expected output
    text: Running the program creates a single‑page PDF. When you open `output.pdf`
      you will see a blank white page with a red rectangle positioned 100 points from
      the left and bottom edges, measuring 200 × 200 points.
  type: HowTo
tags:
- PDF
- C#
- Aspose.PDF
- PDF generation
title: Πώς να δημιουργήσετε έγγραφο PDF με κενή σελίδα και ορθογώνιο
url: /el/net/document-creation/how-to-create-pdf-document-with-a-blank-page-and-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε έγγραφο PDF με κενή σελίδα και ορθογώνιο

Αν χρειάζεται να **δημιουργήσετε έγγραφο PDF** προγραμματιστικά, αυτός ο οδηγός παρουσιάζει μια πλήρη λύση σε C#. Θα μάθετε πώς να προσθέσετε μια κενή σελίδα, να σχεδιάσετε ένα ορθογώνιο σε αυτή τη σελίδα και, τέλος, να αποθηκεύσετε το αρχείο PDF. Το παράδειγμα χρησιμοποιεί τη βιβλιοθήκη Aspose.PDF, η οποία λειτουργεί με .NET 6+ και .NET Framework 4.5+.

Η προσθήκη κενής σελίδας και η σχεδίαση σχημάτων είναι συχνή απαίτηση για τιμολόγια, πιστοποιητικά ή προσαρμοσμένες αναφορές. Στο τέλος αυτού του tutorial θα έχετε ένα εκτελέσιμο έργο που παράγει ένα PDF που περιέχει ένα μόνο ορθογώνιο τοποθετημένο στο (100, 100) με μέγεθος 200 × 200 points.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* Visual Studio 2022 (ή οποιοδήποτε IDE για C#)
* .NET 6 SDK ή .NET Framework 4.5+
* Πακέτο NuGet Aspose.PDF for .NET  
  ```bash
  dotnet add package Aspose.PDF
  ```
* Δικαίωμα εγγραφής στον φάκελο εξόδου

Δεν απαιτείται πρόσθετη διαμόρφωση· ο κώδικας εκτελείται αμέσως.

## Δημιουργία εγγράφου PDF – επισκόπηση

Η διαδικασία αποτελείται από τέσσερα λογικά βήματα:

1. **Instantiate** ένα αντικείμενο `Document` – αντιπροσωπεύει το αρχείο PDF.
2. **Add a blank page** – η σελίδα παρέχει καμβά για σχεδίαση.
3. **Draw a rectangle** – ένα αντικείμενο `Path` ορίζει το σχήμα.
4. **Save the PDF file** – αποθηκεύει το έγγραφο στο δίσκο.

Κάθε βήμα είναι απομονωμένο στη δική του ενότητα ώστε να μπορείτε να το επαναχρησιμοποιήσετε ή να το αντικαταστήσετε όπως χρειάζεται.

![Διάγραμμα PDF με ορθογώνιο σε κενή σελίδα](https://example.com/placeholder-image.png){.img-fluid alt="Στιγμιότυπο που δείχνει ένα έγγραφο PDF με σχεδιασμένο ορθογώνιο σε κενή σελίδα"}

## Προσθήκη κενής σελίδας pdf

Ένα PDF πρέπει να περιέχει τουλάχιστον μία σελίδα πριν τοποθετηθεί οποιοδήποτε γραφικό. Η μέθοδος `Pages.Add()` δημιουργεί μια κενή σελίδα με προεπιλεγμένες διαστάσεις (A4). Αν χρειάζεστε διαφορετικό μέγεθος, περάστε ένα όρισμα `PageSize`.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();

// Step 2: Add a blank page to the document
Page pdfPage = pdfDocument.Pages.Add();   // adds an A4 page by default
```

*Γιατί είναι σημαντικό αυτό το βήμα* – Το αντικείμενο σελίδας κρατά συλλογές για κείμενο, εικόνες και διανυσματικά γραφικά. Χωρίς σελίδα, οποιαδήποτε προσπάθεια προσθήκης ορθογωνίου θα προκαλέσει εξαίρεση.

### Edge case: προσαρμοσμένο μέγεθος σελίδας

Αν η διάταξή σας απαιτεί σελίδα 6 × 9 ίντσες, αντικαταστήστε την προεπιλεγμένη κλήση με:

```csharp
var pageSize = new Size(432, 648); // 72 points per inch
Page pdfPage = pdfDocument.Pages.Add(pageSize);
```

## Σχεδίαση ορθογωνίου pdf

Η σχεδίαση ενός ορθογωνίου είναι απλώς η δημιουργία μιας γεωμετρίας `Rectangle` και η ενσωμάτωσή της σε ένα `Path`. Η κλήση `ValidateBounds()` εξασφαλίζει ότι το σχήμα χωράει μέσα στα περιθώρια της σελίδας, αποτρέποντας την αποκοπή.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

// Step 4: Add the rectangle to the page contents
Path rectanglePath = new Path(shapeRect).ValidateBounds();
pdfPage.Contents.Add(rectanglePath);
```

*Γιατί είναι σημαντικό αυτό το βήμα* – Το αντικείμενο `Path` είναι το χαμηλού επιπέδου διανυσματικό πρωτότυπο που χρησιμοποιεί το Aspose.PDF. Με την επικύρωση των ορίων αποφεύγετε σφάλματα χρόνου εκτέλεσης όταν το ορθογώνιο υπερβαίνει τα όρια της σελίδας.

### Pro tip: στυλ του ορθογωνίου

Μπορείτε να αλλάξετε το χρώμα γραμμής και το πάχος:

```csharp
rectanglePath.GraphInfo = new GraphInfo
{
    StrokeColor = Color.Red,
    LineWidth = 2
};
```

Αυτό παράγει ένα κόκκινο περίγραμμα με πάχος 2 points.

## Αποθήκευση αρχείου pdf

Η αποθήκευση του εγγράφου ολοκληρώνει το αρχείο στο δίσκο. Η μέθοδος `Save` δέχεται διαδρομή αρχείου ή ροή. Η παροχή απόλυτης διαδρομής κάνει την τοποθεσία σαφή, κάτι χρήσιμο για σενάρια αυτοματοποίησης.

```csharp
// Step 5: Save the PDF to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

*Γιατί είναι σημαντικό αυτό το βήμα* – Η αποθήκευση είναι το μοναδικό σημείο όπου η αναπαράσταση στη μνήμη μετατρέπεται σε φυσικό αρχείο. Αν χρειάζεται να επιστρέψετε το PDF από ένα web API, αντικαταστήστε τη διαδρομή αρχείου με ένα `MemoryStream`.

### Edge case: αντικατάσταση υπαρχόντων αρχείων

Το Aspose.PDF αντικαθιστά ένα υπάρχον αρχείο εξ ορισμού. Για να προστατεύσετε προηγούμενες εξόδους, ελέγξτε πρώτα αν το αρχείο υπάρχει:

```csharp
if (File.Exists(outputPath))
{
    File.Delete(outputPath);
}
pdfDocument.Save(outputPath);
```

## Πώς να προσθέσετε ορθογώνιο – βέλτιστες πρακτικές

* **Κρατήστε τις συντεταγμένες εντός των περιθωρίων της σελίδας** – χρησιμοποιήστε `ValidateBounds()` ή υπολογίστε τα περιθώρια χειροκίνητα.
* **Επαναχρησιμοποιήστε αντικείμενα `GraphInfo`** όταν σχεδιάζετε πολλά σχήματα· αυτό μειώνει την κατανομή μνήμης.
* **Κλείστε το αντικείμενο `Document`** (όπως φαίνεται με `using var`) για άμεση απελευθέρωση των εγγενών πόρων.
* **Δοκιμάστε με διαφορετικές ρυθμίσεις DPI** αν αργότερα ενσωματώσετε raster εικόνες· τα διανυσματικά σχήματα όπως τα ορθογώνια παραμένουν οξυμένα σε οποιαδήποτε ανάλυση.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε σε μια εφαρμογή console. Συγκεντώνεται χωρίς τροποποιήσεις και παράγει το `output.pdf` στον φάκελο του έργου.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using var pdfDocument = new Document();

        // Add a blank page to the document
        Page pdfPage = pdfDocument.Pages.Add();

        // Define a rectangle shape (x, y, width, height)
        Rectangle shapeRect = new Rectangle(100, 100, 200, 200);

        // Create a path for the rectangle and validate its bounds
        Path rectanglePath = new Path(shapeRect).ValidateBounds();

        // Optional: style the rectangle (red outline, 2‑pt width)
        rectanglePath.GraphInfo = new GraphInfo
        {
            StrokeColor = Color.Red,
            LineWidth = 2
        };

        // Add the rectangle to the page contents
        pdfPage.Contents.Add(rectanglePath);

        // Determine output path
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");

        // Ensure no leftover file blocks the save operation
        if (File.Exists(outputPath))
        {
            File.Delete(outputPath);
        }

        // Save the PDF to a file
        pdfDocument.Save(outputPath);
        Console.WriteLine($"PDF saved to {outputPath}");
    }
}
```

### Αναμενόμενο αποτέλεσμα

Η εκτέλεση του προγράμματος δημιουργεί ένα PDF μιας σελίδας. Όταν ανοίξετε το `output.pdf` θα δείτε μια κενή λευκή σελίδα με ένα κόκκινο ορθογώνιο τοποθετημένο 100 points από τις αριστερές και κάτω άκρες, με διαστάσεις 200 × 200 points.

## Συμπέρασμα

Τώρα ξέρετε πώς να **δημιουργήσετε έγγραφο PDF**, **προσθέσετε κενή σελίδα pdf**, **σχεδιάσετε ορθογώνιο pdf** και **αποθηκεύσετε αρχείο pdf** χρησιμοποιώντας το Aspose.PDF σε C#. Το παράδειγμα καλύπτει τις βασικές κλήσεις API, εξηγεί γιατί κάθε κλήση είναι απαραίτητη και παρέχει συμβουλές για κοινές παραλλαγές όπως προσαρμοσμένα μεγέθη σελίδας ή στυλ ορθογωνίου.

Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **προσθήκη κειμένου**, **ενσωμάτωση εικόνων** ή **δημιουργία πολυσελιδών αναφορών**. Το ίδιο μοτίβο—instantiate ένα `Document`, χειριστείτε τις σελίδες, προσθέστε διανυσματικό ή raster περιεχόμενο, στη συνέχεια `Save`—εφαρμόζεται σε όλα αυτά τα σενάρια. Μη διστάσετε να πειραματιστείτε με διαφορετικά σχήματα, χρώματα και διατάξεις σελίδας ώστε να ταιριάζουν στις ανάγκες του έργου σας.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Create PDF Document C# – Add Page, Draw Rectangle & Save](/pdf/english/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/)
- [Create PDF Document with Aspose.PDF – Step‑by‑Step Guide](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-step-by-step-guide/)
- [Create PDF Document with Aspose – Add Page, Text Box, and Form](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}