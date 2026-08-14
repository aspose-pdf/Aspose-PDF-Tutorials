---
category: general
date: 2026-08-14
description: Πώς να ορίσετε επιλογές αρίθμησης Bates σε C# χρησιμοποιώντας το GroupDocs.
  Ακολουθήστε αυτό το βήμα‑βήμα οδηγό για να προσθέσετε προσαρμοσμένα προθέματα και
  αριθμούς εκκίνησης κατά τη μετατροπή Word σε PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: el
lastmod: 2026-08-14
og_description: Πώς να ορίσετε γρήγορα τις επιλογές αρίθμησης Bates σε C#. Αυτός ο
  οδηγός σας δείχνει πώς να προσθέσετε προσαρμοσμένα πρόθεμα και αριθμούς έναρξης
  κατά τη μετατροπή Word σε PDF.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: Πώς να ορίσετε επιλογές αρίθμησης Bates σε C# – οδηγός βήμα‑προς‑βήμα
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: Πώς να ορίσετε τις επιλογές αρίθμησης Bates σε C# – πλήρης οδηγός
url: /el/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε επιλογές αρίθμησης Bates σε C# – πλήρης οδηγός

Αν χρειάζεστε **πώς να ορίσετε επιλογές αρίθμησης Bates** σε C#, αυτός ο οδηγός σας οδηγεί βήμα προς βήμα. Θα μάθετε πώς να ρυθμίσετε τον αριθμό εκκίνησης, να προσθέσετε πρόθεμα και να εφαρμόσετε την αρίθμηση κατά τη μετατροπή ενός εγγράφου Word σε PDF χρησιμοποιώντας το GroupDocs API.

Η επεξεργασία εγγράφων συχνά απαιτεί μοναδικά αναγνωριστικά σε κάθε σελίδα για νομικούς ή αρχειακούς σκοπούς. Στο τέλος αυτού του tutorial θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project, είτε δημιουργείτε εργαλείο υποστήριξης διαδίκων είτε αυτόματο γεννήτρια αναφορών. Δεν απαιτούνται εξωτερικά εργαλεία—μόνο η βιβλιοθήκη GroupDocs.Conversion και μερικές γραμμές C#.

## Τι θα χρειαστείτε

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 SDK ή νεότερη έκδοση εγκατεστημένη  
* Visual Studio 2022 (ή οποιοδήποτε IDE που υποστηρίζει .NET)  
* Έγκυρη άδεια GroupDocs.Conversion (η δωρεάν δοκιμή λειτουργεί για δοκιμές)  
* Ένα δείγμα εγγράφου Word (`input.docx`) που θέλετε να αριθμήσετε  

Αυτές οι προαπαιτήσεις εξασφαλίζουν ότι ο κώδικας εκτελείται χωρίς πρόσθετη διαμόρφωση.

## Πώς να ορίσετε επιλογές αρίθμησης Bates – επισκόπηση

Ο πυρήνας του **πώς να ορίσετε επιλογές αρίθμησης Bates** βρίσκεται σε τρία αντικείμενα:

1. `Document` – φορτώνει το αρχείο προέλευσης.  
2. `BatesNumberingOptions` – περιέχει τον αριθμό εκκίνησης, το πρόθεμα και άλλες λεπτομέρειες μορφοποίησης.  
3. `AddBatesNumbering` – η μέθοδος που ενσωματώνει την αρίθμηση σε κάθε σελίδα.

Η κατανόηση του λόγου ύπαρξης κάθε στοιχείου σας βοηθά να προσαρμόσετε τη λύση σε πιο σύνθετα σενάρια, όπως προσαρμοσμένες γραμματοσειρές ή πολυγλωσσική αρίθμηση.

## Βήμα 1: Εγκατάσταση του πακέτου NuGet GroupDocs.Conversion

Ανοίξτε ένα τερματικό στον φάκελο της λύσης σας και εκτελέστε:

```bash
dotnet add package GroupDocs.Conversion
```

Το **GroupDocs API** παρέχει την κλάση `Document` και τη μέθοδο επέκτασης `AddBatesNumbering` που χρησιμοποιείται αργότερα στο tutorial.

## Βήμα 2: Φόρτωση του αρχείου προέλευσης

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*Γιατί αυτό το βήμα;*  
Η φόρτωση του αρχείου δημιουργεί μια αναπαράσταση στη μνήμη που η μηχανή μετατροπής μπορεί να χειριστεί. Χωρίς ένα αντικείμενο `Document` δεν μπορείτε να εφαρμόσετε αρίθμηση Bates ή οποιαδήποτε άλλη μετατροπή.

## Βήμα 3: Δημιουργία των επιλογών αρίθμησης Bates

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*Γιατί αυτό το βήμα;*  
`BatesNumberingOptions` περιλαμβάνει όλες τις ρυθμίσεις που μπορεί να χρειαστείτε όταν **ορίζετε επιλογές αρίθμησης Bates**. Η προσαρμογή του `StartNumber` και του `Prefix` σας επιτρέπει να ευθυγραμμίσετε το αποτέλεσμα με το σύστημα διαχείρισης υποθέσεων. Η ιδιότητα `Position` ελέγχει την οπτική θέση, η οποία συχνά αποτελεί απαίτηση συμμόρφωσης.

## Βήμα 4: Εφαρμογή αρίθμησης Bates στο έγγραφο

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

Η μέθοδος `AddBatesNumbering` διασχίζει κάθε σελίδα του φορτωμένου `Document` και εισάγει τη διαμορφωμένη συμβολοσειρά. Επειδή η μέθοδος λειτουργεί στην αναπαράσταση στη μνήμη, μπορείτε να αλυσίδετε επιπλέον βήματα επεξεργασίας (π.χ., προσθήκη υδατογραφήματος) πριν από την αποθήκευση.

## Βήμα 5: Μετατροπή και αποθήκευση του αποτελέσματος ως PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*Γιατί αυτό το βήμα;*  
Η αποθήκευση ως PDF είναι μια κοινή τελική μορφή για νομικά έγγραφα. Το αντικείμενο `PdfConvertOptions` σας επιτρέπει να ρυθμίσετε λεπτομερώς το αποτέλεσμα, αλλά δεν απαιτείται για βασική αρίθμηση. Η κλήση `Save` γράφει το πλήρως αριθμημένο PDF στο δίσκο.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα, εδώ είναι μια αυτόνομη εφαρμογή κονσόλας που μπορείτε να μεταγλωττίσετε και να εκτελέσετε:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα**

Η εκτέλεση του προγράμματος δημιουργεί το `output.pdf` όπου κάθε σελίδα εμφανίζει μια ετικέτα όπως `CASE-1000`, `CASE-1001`, κ.λπ., τοποθετημένη στο δεξιό υποσέλιδο. Ανοίξτε το PDF σε οποιονδήποτε προβολέα για να επαληθεύσετε ότι οι αριθμοί εμφανίζονται όπως προορίζεται.

## Συνηθισμένα προβλήματα και βέλτιστες πρακτικές

| Πρόβλημα | Γιατί συμβαίνει | Πώς να το αποφύγετε |
|----------|----------------|----------------------|
| **Σχετικές διαδρομές προκαλούν `FileNotFoundException`** | Ο τρέχων φάκελος μιας εφαρμογής κονσόλας μπορεί να διαφέρει από αυτόν του Visual Studio. | Χρησιμοποιήστε απόλυτες διαδρομές ή `Path.Combine(AppContext.BaseDirectory, "input.docx")`. |
| **Η αρίθμηση επικαλύπτεται με υπάρχοντα υποσέλιδα** | Αν το αρχείο προέλευσης έχει ήδη περιεχόμενο στην επιλεγμένη περιοχή υποσέλιδου, ο νέος αριθμός μπορεί να κρύβεται. | Επιλέξτε διαφορετικό `Position` (π.χ., `HeaderLeft`) ή προσαρμόστε το πρότυπο προέλευσης. |
| **Μεγάλα έγγραφα είναι αργά** | Η αρίθμηση Bates επαναλαμβάνεται για κάθε σελίδα· η χρήση μνήμης αυξάνεται με το μέγεθος του αρχείου. | Επεξεργαστείτε το έγγραφο σε τμήματα χρησιμοποιώντας `Document.Split` αν ξεπεράσετε τις 500 σελίδες. |
| **Λήξη άδειας** | Η δωρεάν δοκιμή του GroupDocs λήγει μετά από 30 ημέρες, προκαλώντας εξαίρεση στο `AddBatesNumbering`. | Εφαρμόστε έγκυρο κλειδί άδειας πριν φορτώσετε το έγγραφο: `License license = new License(); license.SetLicense("license.lic");`. |

**Συμβουλή:** Εάν χρειάζεστε διαφορετική μορφή αριθμού ανά υπόθεση (π.χ., `2023-CASE-001`), δημιουργήστε το πρόθεμα δυναμικά πριν δημιουργήσετε το `BatesNumberingOptions`.

## Επέκταση της λύσης

Η ίδια προσέγγιση **Bates numbering C#** λειτουργεί με άλλες μορφές προέλευσης όπως `.txt`, `.html`, ή ακόμη και εικόνες. Απλώς αλλάξτε την επέκταση αρχείου όταν δημιουργείτε το αντικείμενο `Document`, και η μηχανή μετατροπής θα διαχειριστεί το υπόλοιπο.

Μπορείτε επίσης να συνδυάσετε **document conversion C#** με OCR για σαρωμένα PDF:

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να ορίσετε επιλογές αρίθμησης Bates** σε C# από την αρχή μέχρι το τέλος. Δημιουργώντας ένα αντικείμενο `BatesNumberingOptions`, εφαρμόζοντάς το με `AddBatesNumbering` και αποθηκεύοντας το αποτέλεσμα ως PDF, μπορείτε να αυτοματοποιήσετε την παραγωγή νομικά συμμορφωμένων, μοναδικά ταυτοποιημένων εγγράφων.  

Από εδώ μπορείτε να εξερευνήσετε σχετικές θεματικές όπως **C# PDF generation**, **document conversion C#**, ή προχωρημένα χαρακτηριστικά του **GroupDocs API** όπως υδατογραφήματα και ψηφιακές υπογραφές. Πειραματιστείτε με διαφορετικά προθέματα, θέσεις και μορφές αριθμών για να ταιριάζουν στη ροή εργασίας σας.

Καλό κώδικα!

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Προσθήκη αρίθμησης Bates σε PDF σε C# – Πλήρης Οδηγός](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [Πώς να προσθέσετε και να προσαρμόσετε αριθμούς σελίδων σε PDF χρησιμοποιώντας Aspose.PDF για .NET | Οδηγός Διαχείρισης Εγγράφων](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Πώς να προσθέσετε υποσέλιδο σήματος κειμένου σε PDF χρησιμοποιώντας Aspose.PDF για .NET&#58; Οδηγός βήμα‑βήμα](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}