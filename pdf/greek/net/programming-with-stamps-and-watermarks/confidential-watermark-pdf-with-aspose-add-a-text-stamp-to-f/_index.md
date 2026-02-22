---
category: general
date: 2026-02-22
description: Εκπαιδευτικό σεμινάριο για υδατογράφημα «Εμπιστευτικό» σε PDF με χρήση
  του Aspose.Pdf – μάθετε πώς να προσθέσετε μια ετικέτα «Εμπιστευτικό» ως σφραγίδα
  κειμένου στην πρώτη σελίδα οποιουδήποτε PDF.
draft: false
keywords:
- confidential watermark pdf
- add confidential label
- aspose pdf watermark
- add stamp first page
- add text stamp pdf
language: el
og_description: 'Οδηγός PDF με εμπιστευτικό υδατογράφημα: βήμα‑βήμα οδηγίες για την
  προσθήκη ετικέτας «Εμπιστευτικό» ως κείμενο σφραγίδα στην πρώτη σελίδα χρησιμοποιώντας
  το Aspose.Pdf για .NET.'
og_title: PDF με εμπιστευτικό υδατογράφημα με Aspose – Προσθήκη κειμενικής σφραγίδας
tags:
- aspose
- pdf
- watermark
- csharp
title: 'Εμπιστευτικό υδατογράφημα PDF με το Aspose: Προσθήκη κειμενικής σφραγίδας
  στην πρώτη σελίδα'
url: /el/net/programming-with-stamps-and-watermarks/confidential-watermark-pdf-with-aspose-add-a-text-stamp-to-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF με εμπιστευτικό υδατογράφημα – Πώς να προσθέσετε σφραγίδα κειμένου στην πρώτη σελίδα

Έχετε ποτέ χρειαστεί ένα **confidential watermark PDF** αλλά δεν ήσασταν σίγουροι πώς να προσθέσετε μια ετικέτα μόνο στην πρώτη σελίδα; Δεν είστε μόνοι—πολλοί προγραμματιστές παλεύουν με το «Πώς να προσθέσω μια εμπιστευτική ετικέτα χωρίς να χαλάσω τη διάταξη;»

Τα καλά νέα; Με το Aspose.Pdf για .NET μπορείτε να το κάνετε σε λίγες γραμμές, και θα σας καθοδηγήσω σε όλη τη διαδικασία τώρα. Χωρίς ασαφείς αναφορές, μόνο μια πλήρης, λύση copy‑and‑paste που λειτουργεί σήμερα.

## Τι θα μάθετε

* Εγκατάσταση του πακέτου Aspose.Pdf NuGet (η μόνη προϋπόθεση).
* Φόρτωση ενός υπάρχοντος PDF.
* Δημιουργία ενός **confidential watermark PDF** χρησιμοποιώντας `TextStamp`.
* Προσθήκη αυτής της σφραγίδας μόνο στην **πρώτη σελίδα** (η απαίτηση «add stamp first page»).
* Αποθήκευση του αποτελέσματος και επαλήθευση του εξόδου.

## Προαπαιτούμενα

* .NET 6+ (ο κώδικας λειτουργεί τόσο σε .NET Core όσο και σε .NET Framework).
* Visual Studio 2022 ή οποιοδήποτε IDE προτιμάτε.
* Aspose.Pdf for .NET – συνιστάται η έκδοση 23.10 ή νεότερη για τις τελευταίες διορθώσεις σφαλμάτων.

Αν δεν έχετε προσθέσει ακόμη το Aspose.Pdf στο έργο σας, εκτελέστε:

```bash
dotnet add package Aspose.Pdf
```

Αυτό είναι—χωρίς επιπλέον DLLs, χωρίς προβλήματα αδειοδότησης για τη δοκιμαστική έκδοση (απλώς θυμηθείτε να εφαρμόσετε το κλειδί άδειας πριν τη διανομή).

## Βήμα 1: Φόρτωση του Πηγαίου PDF Εγγράφου

Πρώτα πρέπει να ανοίξουμε το αρχείο που θέλουμε να προστατεύσουμε. Η κλάση `Document` αντιπροσωπεύει ολόκληρο το PDF, και η φόρτωσή του είναι τόσο απλή όσο η παροχή της διαδρομής.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Path to the PDF you want to watermark
string inputPdfPath = @"C:\MyDocs\input.pdf";

// Load the PDF into memory
using var pdfDocument = new Document(inputPdfPath);
```

*Γιατί είναι σημαντικό*: Η φόρτωση του εγγράφου σας δίνει πρόσβαση στη συλλογή `Pages`, όπου θα προσθέσουμε τη σφραγίδα. Η χρήση του `using var` εξασφαλίζει ότι το χειριστήριο του αρχείου απελευθερώνεται άμεσα—σημαντικό για μεγάλες παρτίδες.

## Βήμα 2: Δημιουργία της Εμπιστευτικής Σφραγίδας Κειμένου

Τώρα δημιουργούμε την οπτική ετικέτα. Ένα `TextStamp` μας επιτρέπει να ελέγχουμε το μέγεθος, την αναδίπλωση και την κλιμάκωση. Οι παρακάτω ρυθμίσεις εξασφαλίζουν ότι η λέξη *Confidential* ταιριάζει όμορφα χωρίς να υπερβαίνει τα όρια.

```csharp
// Build a text stamp that says "Confidential"
var confidentialStamp = new TextStamp("Confidential")
{
    // Auto‑adjust the font so it never exceeds the rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    AutoAdjustFontSizePrecision = 0.01f,

    // Wrap by whole words—no broken words in the middle
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,

    // Define the stamp rectangle (you can tweak width/height)
    Width = 300,
    Height = 100,

    // Keep the stamp size constant even if the page is resized
    Scale = false
};
```

**Συμβουλή**: Αν χρειάζεστε διαφορετική γραμματοσειρά ή χρώμα, ορίστε `confidentialStamp.TextState.Font` και `confidentialStamp.TextState.ForegroundColor`. Για παράδειγμα, `confidentialStamp.TextState.Font = FontRepository.FindFont("Arial")` και `confidentialStamp.TextState.ForegroundColor = Color.Red`.

## Βήμα 3: Προσθήκη της Σφραγίδας μόνο στην Πρώτη Σελίδα

Το Aspose χρησιμοποιεί αρίθμηση σελίδων που ξεκινά από το 1, έτσι το `Pages[1]` είναι η πρώτη σελίδα. Η προσθήκη της σφραγίδας εκεί ικανοποιεί την απαίτηση **add stamp first page**.

```csharp
// Attach the stamp to the very first page
pdfDocument.Pages[1].AddStamp(confidentialStamp);
```

Αν ποτέ χρειαστεί να βάλετε υδατογράφημα σε κάθε σελίδα, κάντε βρόχο μέσω του `pdfDocument.Pages`. Αλλά για ετικέτα μίας σελίδας, αυτή η μία γραμμή κάνει τη δουλειά.

## Βήμα 4: Αποθήκευση του Υδατογραφημένου PDF

Τέλος, γράψτε το τροποποιημένο έγγραφο ξανά στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό ή να δημιουργήσετε νέο αρχείο—όπως προτιμάτε.

```csharp
// Destination path for the watermarked PDF
string outputPdfPath = @"C:\MyDocs\Stamped.pdf";

// Persist the changes
pdfDocument.Save(outputPdfPath);
```

Όταν ανοίξετε το `Stamped.pdf`, θα δείτε το *Confidential* να εμφανίζεται στην επάνω‑αριστερή γωνία της σελίδας 1 (ή όπου έχετε τοποθετήσει τη σφραγίδα). Το υπόλοιπο του εγγράφου παραμένει άθικτο.

## Αναμενόμενο Αποτέλεσμα

| Πριν | Μετά (πρώτη σελίδα) |
|--------|-------------------|
| ![Αρχική σελίδα PDF](/images/original.png "Αρχική σελίδα PDF") | ![Παράδειγμα PDF με εμπιστευτικό υδατογράφημα](/images/confidential-watermark.png "Παράδειγμα PDF με εμπιστευτικό υδατογράφημα") |

*Κείμενο alt εικόνας*: **παράδειγμα PDF με εμπιστευτικό υδατογράφημα** (περιλαμβάνει τη βασική λέξη-κλειδί).

## Περιπτώσεις Ορίων & Συχνές Ερωτήσεις

### Τι γίνεται αν το PDF δεν έχει σελίδες;

Η προσπάθεια πρόσβασης στο `Pages[1]` θα προκαλέσει `ArgumentOutOfRangeException`. Προστατέψτε το από αυτό:

```csharp
if (pdfDocument.Pages.Count == 0)
    throw new InvalidOperationException("The PDF is empty.");
```

### Πώς να βάλω υδατογράφημα σε πολλές σελίδες;

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(confidentialStamp);
}
```

Θυμηθείτε να επαναφέρετε τη θέση του `confidentialStamp` αν θέλετε να τοποθετήσετε τη σφραγίδα σε διαφορετικές γωνίες ανά σελίδα.

### Μπορώ να αλλάξω τη θέση της σφραγίδας;

Ναι—ορίστε `confidentialStamp.HorizontalAlignment` και `confidentialStamp.VerticalAlignment`, ή χρησιμοποιήστε `confidentialStamp.XIndent` / `YIndent` για τοποθέτηση με ακρίβεια pixel.

### Λειτουργεί αυτό με PDF που προστατεύονται με κωδικό;

Aspose μπορεί να ανοίξει κρυπτογραφημένα αρχεία εάν παρέχετε τον κωδικό:

```csharp
var pdfDocument = new Document(inputPdfPath, new LoadOptions { Password = "mySecret" });
```

### Τι γίνεται με την απόδοση σε μεγάλες παρτίδες;

Η φόρτωση και αποθήκευση κάθε εγγράφου ξεχωριστά μπορεί να είναι βαριά σε I/O. Σκεφτείτε να επαναχρησιμοποιήσετε ένα μόνο αντικείμενο `Document` για λειτουργίες στη μνήμη και να αποθηκεύετε μόνο μία φορά ανά παρτίδα.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε μια εφαρμογή κονσόλας. Περιλαμβάνει όλα τα βήματα, τη διαχείριση σφαλμάτων και ένα απλό μήνυμα επαλήθευσης.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        string inputPdfPath = @"C:\MyDocs\input.pdf";
        if (!System.IO.File.Exists(inputPdfPath))
        {
            Console.WriteLine("Input file not found.");
            return;
        }

        using var pdfDocument = new Document(inputPdfPath);

        if (pdfDocument.Pages.Count == 0)
        {
            Console.WriteLine("The PDF contains no pages.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Create the confidential text stamp
        // -------------------------------------------------
        var confidentialStamp = new TextStamp("Confidential")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
            Width = 300,
            Height = 100,
            Scale = false,
            // Optional styling
            TextState = { FontSize = 24, Font = FontRepository.FindFont("Arial"), ForegroundColor = Color.Red }
        };

        // -------------------------------------------------
        // 3️⃣ Add the stamp to the first page only
        // -------------------------------------------------
        pdfDocument.Pages[1].AddStamp(confidentialStamp);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        string outputPdfPath = @"C:\MyDocs\Stamped.pdf";
        pdfDocument.Save(outputPdfPath);

        Console.WriteLine($"Successfully added a confidential watermark PDF. Saved to: {outputPdfPath}");
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το `Stamped.pdf`, και θα δείτε το **confidential watermark PDF** να έχει εφαρμοστεί ακριβώς όπου το θέλαμε.

## Συμπέρασμα

Τώρα έχετε έναν αξιόπιστο, έτοιμο για παραγωγή τρόπο να **προσθέσετε μια εμπιστευτική ετικέτα** ως **σφραγίδα κειμένου** στην **πρώτη σελίδα** οποιουδήποτε PDF χρησιμοποιώντας το Aspose.Pdf. Η λύση είναι πλήρως αυτόνομη, λειτουργεί με τις τελευταίες εκδόσεις .NET, και μπορεί να επεκταθεί σε πολλές σελίδες, προσαρμοσμένες γραμματοσειρές ή διαφορετικά χρώματα.

**Επόμενα βήματα** που μπορείτε να εξερευνήσετε:

* Αντικαταστήστε τη σφραγίδα κειμένου με σφραγίδα εικόνας (`ImageStamp`) για ενσωμάτωση λογότυπου.
* Συνδυάστε αυτήν την προσέγγιση με βρόχο για δημιουργία ενός **aspose pdf watermark** σε ολόκληρο το έγγραφο.
* Ενσωματώστε τον κώδικα σε ένα ASP.NET Core API ώστε οι χρήστες να μπορούν να ανεβάζουν PDF και να λαμβάνουν εκδόσεις με υδατογράφημα άμεσα.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}