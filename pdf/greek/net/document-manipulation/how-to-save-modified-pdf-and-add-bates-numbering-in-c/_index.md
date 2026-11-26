---
category: general
date: 2026-11-25
description: Μάθετε πώς να αποθηκεύετε τροποποιημένα PDF, να προσθέτετε αριθμητική
  σήμανση Bates σε PDF και να εισάγετε προσαρμοσμένο σχήμα PDF χρησιμοποιώντας το
  Aspose.PDF για C# σε έναν πλήρη οδηγό βήμα‑προς‑βήμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save modified pdf
- add bates numbering pdf
- add bates numbers pdf
- add custom shape pdf
- load pdf document c#
language: el
lastmod: 2026-11-25
og_description: Αποθήκευση τροποποιημένου PDF με το Aspose.PDF για C#. Αυτός ο οδηγός
  δείχνει πώς να προσθέσετε αρίθμηση Bates σε PDF, να προσθέσετε προσαρμοσμένο σχήμα
  σε PDF και να φορτώσετε αποδοτικά έγγραφο PDF με C#.
og_image_alt: Screenshot of a C# program that saves modified PDF after adding Bates
  numbering and a custom shape
og_title: Αποθήκευση τροποποιημένου PDF και προσθήκη αριθμολόγησης Bates σε C# – πλήρης
  οδηγός
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to save modified PDF, add Bates numbering PDF, and insert
    a custom shape PDF using Aspose.PDF for C# in a complete step‑by‑step guide.
  headline: How to save modified PDF and add Bates numbering in C#
  type: TechArticle
tags:
- PDF
- C#
- Aspose.PDF
title: Πώς να αποθηκεύσετε ένα τροποποιημένο PDF και να προσθέσετε αρίθμηση Bates
  σε C#
url: /el/net/document-manipulation/how-to-save-modified-pdf-and-add-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποθηκεύσετε τροποποιημένο PDF και να προσθέσετε αρίθμηση Bates σε C#

Αν χρειάζεστε να **save modified PDF** αρχεία μετά την εφαρμογή νομικής αρίθμησης Bates, η λύση είναι εδώ. Αυτό το tutorial σας καθοδηγεί στη φόρτωση ενός εγγράφου PDF σε C#, την προσθήκη αριθμών Bates, την εισαγωγή προσαρμοσμένου σχήματος και, τελικά, **saving the modified PDF** με το Aspose.PDF. Είτε προετοιμάζετε φακέλους υποθέσεων είτε αυτοματοποιείτε ροές εργασίας εγγράφων, θα λάβετε ένα πλήρες, εκτελέσιμο παράδειγμα.

Θα δείτε επίσης πώς να **load PDF document C#** κώδικα, να εντοπίσετε παραβιασμένες ψηφιακές υπογραφές και να επαληθεύσετε τα όρια των σχημάτων—όλα όσα χρειάζεστε για να δημιουργήσετε μια αξιόπιστη pipeline επεξεργασίας PDF. Στο τέλος αυτού του οδηγού θα μπορείτε να εκτελέσετε το δείγμα και να παραγάγετε ένα PDF που περιέχει διαδοχικούς αριθμούς Bates, ένα προσαρμοσμένο γραφικό και οποιεσδήποτε άλλες τροποποιήσεις απαιτούνται.

## Προαπαιτούμενα

| Απαίτηση | Λόγος |
|-------------|--------|
| .NET 6.0 ή νεότερο | Παρέχει το runtime για έργα C# |
| Visual Studio 2022 (ή οποιοδήποτε IDE C#) | Διευκολύνει την επεξεργασία και την αποσφαλμάτωση |
| Aspose.PDF for .NET (πακέτο NuGet `Aspose.Pdf`) | Παρέχει το API χειρισμού PDF |
| Ένα αρχείο PDF εισόδου (`input.pdf`) | Λειτουργεί ως το έγγραφο προέλευσης |

Βεβαιωθείτε ότι το πακέτο Aspose.PDF είναι εγκατεστημένο:

```bash
dotnet add package Aspose.Pdf
```

## Βήμα 1: Φόρτωση εγγράφου PDF C# – αρχικοποίηση του αρχικού αρχείου

Η πρώτη ενέργεια είναι η ανάγνωση του υπάρχοντος PDF στη μνήμη. Η χρήση της κλάσης `Document` σας δίνει πλήρη πρόσβαση στις σελίδες, τις υπογραφές και άλλες δομές χαμηλού επιπέδου.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

// Load the PDF document from disk
var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

// Optional: verify the document opened correctly
if (pdfDocument.Pages.Count == 0)
{
    throw new InvalidOperationException("The input PDF contains no pages.");
}
```

**Γιατί είναι σημαντικό:** Η φόρτωση του αρχείου είναι η βάση για οποιεσδήποτε επόμενες αλλαγές. Εάν το έγγραφο δεν φορτωθεί, τα επόμενα βήματα όπως **add bates numbering pdf** ή **add custom shape pdf** θα προκαλέσουν εξαιρέσεις.

## Βήμα 2: Ανίχνευση παραβιασμένων ψηφιακών υπογραφών (έλεγχος ασφαλείας)

Τα νομικά έγγραφα συχνά περιέχουν ψηφιακές υπογραφές. Πριν τροποποιήσετε το αρχείο, είναι καλή πρακτική να ελέγξετε εάν κάποια υπογραφή έχει παραβιαστεί.

```csharp
// Detect any compromised digital signatures
var compromisedSignatures = pdfDocument.DigitalSignatures.DetectCompromisedSignatures();

if (compromisedSignatures.Count > 0)
{
    Console.WriteLine("Warning: Compromised signatures detected.");
    // You may choose to abort or log details here
}
```

**Γιατί είναι σημαντικό:** Η τροποποίηση ενός υπογεγραμμένου PDF μπορεί να ακυρώσει την υπογραφή. Η ανίχνευση παραβιασμένων υπογραφών σας επιτρέπει να αποφασίσετε αν θα διατηρήσετε, αφαιρέσετε ή επαναυπογράψετε το έγγραφο μετά τις αλλαγές.

## Βήμα 3: Προσθήκη αρίθμησης Bates PDF – ρύθμιση προθέματος και αριθμού εκκίνησης

Η αρίθμηση Bates είναι ουσιώδης για τη διαχείριση νομικών υποθέσεων. Το Aspose.PDF παρέχει ένα απλό API για να ορίσετε πρόθεμα και αριθμό εκκίνησης.

```csharp
// Configure Bates numbering (starting number and prefix)
pdfDocument.BatesNumbering.Start = 1000;          // Start at 1000
pdfDocument.BatesNumbering.Prefix = "CASE-";     // Prefix for each number
pdfDocument.BatesNumbering.Suffix = "";          // Optional suffix
pdfDocument.BatesNumbering.FontSize = 12;        // Readable font size
pdfDocument.BatesNumbering.Color = Color.Black; // Standard black text
pdfDocument.BatesNumbering.Position = new Position(50, 20); // Bottom‑left corner
```

**Γιατί είναι σημαντικό:** Το αντικείμενο `BatesNumbering` τοποθετεί αυτόματα διαδοχικούς αριθμούς σε κάθε σελίδα. Η ρύθμιση του `Position` σας επιτρέπει να ελέγξετε πού εμφανίζεται ο αριθμός, ώστε να μην επικαλύπτεται με υπάρχον περιεχόμενο.

## Βήμα 4: Προσθήκη προσαρμοσμένου σχήματος PDF – δημιουργία και τοποθέτηση γραφικού στοιχείου

Οι νομικές ομάδες μερικές φορές χρειάζονται να σφραγίσουν ένα λογότυπο ή να σχεδιάσουν ένα πλαίσιο γύρω από μια παράγραφο. Το Aspose.PDF σας επιτρέπει να ορίσετε ένα σχήμα μέσω ενός αντικειμένου `Path` και να το συνδέσετε με μια σελίδα.

```csharp
// Create a custom shape (a simple rectangle in this example)
var shapePath = new Path();
shapePath.PathData = "M 100 200 L 300 200 L 300 400 L 100 400 Z"; // Rectangle path
shapePath.Stroke = new Stroke(Color.Blue, 2); // Blue border, 2pt thickness
shapePath.Fill = new Fill(Color.LightGray);   // Light gray fill

// Verify that the shape stays within page bounds
shapePath.VerifyBounds(); // Throws if the shape exceeds page size

// Add the shape to the first page
pdfDocument.Pages[1].Add(shapePath);
```

**Γιατί είναι σημαντικό:** Ο ορισμός ενός σχήματος με τη σύνταξη `Path` παρέχει έλεγχο σε επίπεδο διανυσματικού, το οποίο κλιμακώνεται καθαρά για οποιαδήποτε συσκευή εξόδου. Η κλήση `VerifyBounds` αποτρέπει σφάλματα χρόνου εκτέλεσης που προκαλούνται από σχήματα που ξεπροβάλλουν από τη σελίδα.

## Βήμα 5: Προσθήκη στοιχείου με ετικέτα – προαιρετική βελτίωση προσβασιμότητας

Εάν χρειάζεται να βελτιώσετε την προσβασιμότητα, μπορείτε να προσθέσετε ένα στοιχείο με ετικέτα που οι αναγνώστες οθόνης μπορούν να ερμηνεύσουν.

```csharp
var taggedElement = new TaggedElement();
taggedElement.Position = new Position(100, 200); // X=100, Y=200 points
taggedElement.Tag = "Figure"; // Semantic tag
pdfDocument.Pages[1].Add(taggedElement);
```

**Γιατί είναι σημαντικό:** Τα στοιχεία με ετικέτα βοηθούν στη συμμόρφωση με PDF/UA, καθιστώντας το έγγραφο χρήσιμο για βοηθητικές τεχνολογίες.

## Βήμα 6: Αποθήκευση τροποποιημένου PDF – ολοκλήρωση του αρχείου εξόδου

Αφού εφαρμοστούν όλες οι τροποποιήσεις, **save the modified PDF** σε νέα τοποθεσία. Αυτό το βήμα γράφει τις αλλαγές στη μνήμη πίσω στο δίσκο.

```csharp
// Save the modified PDF document
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

// Confirmation message
Console.WriteLine("Modified PDF saved successfully as output.pdf");
```

**Γιατί είναι σημαντικό:** Η μέθοδος `Save` ολοκληρώνει το αρχείο, ενσωματώνοντας τους αριθμούς Bates, το προσαρμοσμένο σχήμα και τυχόν άλλες επεμβάσεις. Χωρίς αυτήν την κλήση, καμία από τις αλλαγές δεν θα παραμείνει.

## Πλήρες εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που ενσωματώνει κάθε βήμα που συζητήθηκε. Αντιγράψτε τον κώδικα σε ένα νέο έργο κονσόλας, προσαρμόστε τις διαδρομές αρχείων και εκτελέστε το.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Drawing; // For Path, Stroke, Fill, etc.

namespace PdfProcessingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the PDF document
            var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

            // Step 2: Detect compromised digital signatures
            var compromisedSignatures = pdfDocument.DigitalSignatures.DetectCompromisedSignatures();
            if (compromisedSignatures.Count > 0)
            {
                Console.WriteLine("Warning: Compromised signatures detected.");
                // Handle according to business rules
            }

            // Step 3: Configure Bates numbering (add bates numbers pdf)
            pdfDocument.BatesNumbering.Start = 1000;
            pdfDocument.BatesNumbering.Prefix = "CASE-";
            pdfDocument.BatesNumbering.FontSize = 12;
            pdfDocument.BatesNumbering.Color = Color.Black;
            pdfDocument.BatesNumbering.Position = new Position(50, 20);

            // Step 4: Create a custom shape (add custom shape pdf)
            var shapePath = new Path();
            shapePath.PathData = "M 100 200 L 300 200 L 300 400 L 100 400 Z";
            shapePath.Stroke = new Stroke(Color.Blue, 2);
            shapePath.Fill = new Fill(Color.LightGray);
            shapePath.VerifyBounds(); // Ensure shape fits the page
            pdfDocument.Pages[1].Add(shapePath);

            // Step 5: Add a tagged element (optional accessibility aid)
            var taggedElement = new TaggedElement
            {
                Position = new Position(100, 200),
                Tag = "Figure"
            };
            pdfDocument.Pages[1].Add(taggedElement);

            // Step 6: Save the modified PDF (save modified pdf)
            pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
            Console.WriteLine("Modified PDF saved successfully as output.pdf");
        }
    }
}
```

### Αναμενόμενη έξοδος

Η εκτέλεση του προγράμματος παράγει το `output.pdf` με:

* Αριθμοί Bates όπως `CASE-1000`, `CASE-1001`, … σε κάθε σελίδα.
* Ένα ανοιχτόγκρι ορθογώνιο με μπλε περίγραμμα τοποθετημένο στο (100, 200).
* Ένα προαιρετικό στοιχείο με ετικέτα για προσβασιμότητα.
* Όλο το αρχικό περιεχόμενο διατηρείται εκτός εάν εντοπιστεί παραβιασμένη υπογραφή (μπορείτε να επιλέξετε την ακύρωση).

## Συμπέρασμα

Τώρα ξέρετε πώς να **save modified PDF** αρχεία μετά την εφαρμογή **add bates numbering PDF**, την εισαγωγή ενός **add custom shape pdf**, και τον έλεγχο ασφαλείας με **load PDF document C#**. Το πλήρες παράδειγμα δείχνει βέλτιστες πρακτικές όπως η επαλήθευση ορίων σχήματος, η διαχείριση ψηφιακών υπογραφών και η χρήση του ευέλικτου API του Aspose.PDF.

Από εδώ μπορείτε να εξερευνήσετε περαιτέρω βελτιώσεις:

* **Add bates numbers pdf** με προσαρμοσμένες ημερομηνίες ή αναγνωριστικά υποθέσεων.
* Εισαγωγή πολλαπλών σχημάτων ή εικόνων για δημιουργία υδατογραφιών.
* Επαναυπογραφή του PDF μετά τις τροποποιήσεις χρησιμοποιώντας `DigitalSignatureFacade`.
* Εξαγωγή του εγγράφου σε άλλες μορφές (DOCX, TIFF) χρησιμοποιώντας τα APIs μετατροπής της Aspose.

Μη διστάσετε να πειραματιστείτε με διαφορετικά προθέματα, αριθμούς εκκίνησης ή γεωμετρίες σχημάτων για να ταιριάζουν στη ροή εργασίας του οργανισμού σας. Καλός κώδικας!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Πώς να προσθέσετε σχήμα σε PDF με Aspose.PDF σε C# – Οδηγός βήμα προς βήμα](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Πώς να αποθηκεύσετε τροποποιημένο PDF με Aspose.Pdf και να προσθέσετε διαφάνεια](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Δημιουργία εγγράφου PDF με Aspose.PDF – Προσθήκη σελίδας, σχήματος & αποθήκευση](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}