---
category: general
date: 2026-08-04
description: Δημιουργήστε νέο έγγραφο PDF σε C# και προσθέστε γρήγορα αριθμητική Bates
  στο PDF χρησιμοποιώντας το Aspose.Pdf – μάθετε πώς να προσθέσετε κενή σελίδα PDF
  και προσαρμοσμένους αριθμούς σελίδων.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: el
lastmod: 2026-08-04
og_description: Δημιουργήστε νέο έγγραφο PDF σε C# και προσθέστε αυτόματα αρίθμηση
  Bates σε PDF για τη διαχείριση νομικών υποθέσεων – περιλαμβάνεται πλήρες παράδειγμα
  κώδικα.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: Δημιουργία νέου εγγράφου PDF με αρίθμηση Bates σε C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: Δημιουργία νέου εγγράφου PDF με αρίθμηση Bates σε C#
url: /el/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία νέου PDF εγγράφου με αρίθμηση Bates σε C#

Αν χρειάζεστε **δημιουργία νέου PDF εγγράφου** σε C#, αυτός ο οδηγός σας δείχνει πώς να **προσθέσετε αρίθμηση Bates σε PDF** χρησιμοποιώντας το Aspose.Pdf. Θα μάθετε να **προσθέτετε κενή σελίδα PDF**, να διαμορφώνετε **προσθήκη προσαρμοσμένων αριθμών σελίδας**, και να αποθηκεύετε το τελικό αρχείο.

Ο οδηγός καλύπτει κάθε βήμα, από την εγκατάσταση της βιβλιοθήκης μέχρι τη δημιουργία ενός PDF που συμμορφώνεται με τα πρότυπα νομικών φακέλων. Στο τέλος θα μπορείτε να δημιουργήσετε ένα PDF, να εισάγετε μια κενή σελίδα, να εφαρμόσετε αριθμούς Bates και να προσαρμόσετε τη μορφή αρίθμησης—όλα με ένα μόνο, εκτελέσιμο πρόγραμμα.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 SDK ή νεότερη έκδοση εγκατεστημένη  
* Visual Studio 2022 (ή οποιοδήποτε IDE για C#)  
* Ένα ενεργό λ licens Aspose.Pdf for .NET ή ένα δωρεάν κλειδί αξιολόγησης  

Δεν χρειάζεστε επιπλέον πακέτα NuGet· ο οδηγός εγκαθιστά αυτόματα όλα όσα απαιτούνται.

## Βήμα 1: Εγκατάσταση Aspose.Pdf μέσω NuGet

Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.Pdf
```

Η εντολή προσθέτει την πιο πρόσφατη σταθερή έκδοση του Aspose.Pdf στο έργο σας, η οποία παρέχει τις κλάσεις `Document`, `BatesNumbering` και άλλες κλάσεις διαχείρισης PDF που θα χρησιμοποιήσετε.

## Βήμα 2: Δημιουργία νέου PDF εγγράφου – αρχική ρύθμιση

Η δημιουργία του αρχείου PDF αποτελεί τη βάση για όλες τις επόμενες λειτουργίες. Η κλάση `Document` αντιπροσωπεύει ολόκληρο το κοντέινερ PDF.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Γιατί είναι σημαντικό*: Η δημιουργία ενός αντικειμένου `Document` διανέμει τις εσωτερικές δομές που απαιτούνται για σελίδες, γραμματοσειρές και γραφικά. Η χρήση του `using var` εξασφαλίζει ότι το αρχείο θα απελευθερωθεί σωστά μετά την αποθήκευση.

## Βήμα 3: Προσθήκη κενής σελίδας PDF

Ένα PDF πρέπει να περιέχει τουλάχιστον μία σελίδα πριν μπορέσετε να τοποθετήσετε περιεχόμενο. Η προσθήκη μιας κενής σελίδας σας δίνει ένα καθαρό καμβά για τους αριθμούς Bates.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

Η μέθοδος `Pages.Add()` προσθέτει μια νέα, κενή σελίδα στο τέλος της συλλογής σελίδων του εγγράφου. Μπορείτε να επαναλάβετε αυτήν την κλήση για να προσθέσετε περισσότερες σελίδες εάν αργότερα χρειαστεί να **προσθέσετε προσαρμοσμένους αριθμούς σελίδας** σε πολλές σελίδες.

## Βήμα 4: Διαμόρφωση αρίθμησης Bates – πώς να προσθέσετε Bates

Η αρίθμηση Bates είναι ένας διαδοχικός ταυτοποιητής που χρησιμοποιείται συνήθως σε νομικά έγγραφα. Διαμορφώνετε την αρίθμηση μέσω της κλάσης `BatesNumbering`.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Γιατί είναι σημαντικό*: Το `StartNumber` ορίζει τον πρώτο αριθμό, το `Prefix` προσθέτει μια ετικέτα, και το `Increment` ελέγχει το βήμα αύξησης. Μπορείτε επίσης να ρυθμίσετε `HorizontalAlignment`, `VerticalAlignment`, `FontSize` και `Margins` για να ελέγξετε την εμφάνιση του αριθμού σε κάθε σελίδα.

## Βήμα 5: Εφαρμογή της αρίθμησης Bates στο PDF στη σελίδα

Τώρα που οι επιλογές αρίθμησης είναι έτοιμες, εφαρμόστε τες στη σελίδα (ή σε ολόκληρο το έγγραφο).

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

Η κλήση `Apply` εισάγει τον μορφοποιημένο αριθμό στο υποσέλιδο της σελίδας από προεπιλογή. Εάν χρειάζεστε τον αριθμό σε άλλη θέση, ορίστε `bates.Position` πριν καλέσετε το `Apply`.

## Βήμα 6: Αποθήκευση του PDF με εφαρμοσμένους αριθμούς Bates

Τέλος, γράψτε το έγγραφο στη μνήμη στο δίσκο.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

Το αποθηκευμένο αρχείο περιέχει τώρα μια μοναδική σελίδα με τον αριθμό Bates **CaseA-1000** εμφανιζόμενο στο κάτω μέρος. Ανοίξτε το PDF σε οποιονδήποτε προβολέα για να επαληθεύσετε την αρίθμηση.

## Αναμενόμενο αποτέλεσμα

Όταν ανοίξετε το `BatesNumbered.pdf`, θα πρέπει να δείτε:

* Μία κενή σελίδα (ή περισσότερες εάν προσθέσατε επιπλέον σελίδες)  
* Το κείμενο **CaseA-1000** τοποθετημένο στο κάτω μέρος της σελίδας (προεπιλεγμένη θέση)  

Εάν προσθέσετε περισσότερες σελίδες και επαναχρησιμοποιήσετε την ίδια παρουσία `BatesNumbering`, οι αριθμοί θα αυξηθούν αυτόματα (CaseA-1001, CaseA-1002, …).

## Pro tip: Προσθήκη προσαρμοσμένων αριθμών σελίδας εκτός των αριθμών Bates

Μερικές φορές χρειάζονται και οι αριθμοί Bates και οι παραδοσιακοί αριθμοί σελίδας. Μπορείτε να τους συνδυάσετε προσθέτοντας ένα `TextFragment` μετά την εφαρμογή της αρίθμησης Bates:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

Αυτό το απόσπασμα κώδικα δείχνει **προσθήκη προσαρμοσμένων αριθμών σελίδας** διατηρώντας την ετικέτα Bates.

## Edge case: Εφαρμογή αρίθμησης Bates σε πολλαπλές σελίδες

Εάν το έγγραφό σας περιέχει πολλές σελίδες, μπορείτε να εφαρμόσετε την ίδια παρουσία `BatesNumbering` σε κάθε σελίδα μέσα σε βρόχο:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

Ο βρόχος εξασφαλίζει ότι κάθε σελίδα λαμβάνει έναν διαδοχικό αριθμό βάσει του `StartNumber` και του `Increment` που ορίσατε.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Οι αριθμοί εμφανίζονται εκτός κέντρου | Η προεπιλεγμένη στοίχιση μπορεί να μην ταιριάζει με τη διάταξή σας | Ορίστε ρητά `bates.HorizontalAlignment` και `bates.VerticalAlignment` |
| Οι αριθμοί επικαλύπτονται με υπάρχον περιεχόμενο | Δεν έχει οριστεί περιθώριο | Ρυθμίστε `bates.Margin` ή χρησιμοποιήστε `bates.Position` για μετακίνηση του αριθμού |
| Εξαίρεση άδειας χρόνου εκτέλεσης | Η έκδοση αξιολόγησης περιορίζει την έξοδο | Εφαρμόστε μια έγκυρη άδεια Aspose.Pdf πριν δημιουργήσετε το έγγραφο (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Πλήρες λειτουργικό παράδειγμα

Ακολουθεί ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε, να επικολλήσετε και να εκτελέσετε.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET&#58; Add Page Numbers to PDFs Using FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}