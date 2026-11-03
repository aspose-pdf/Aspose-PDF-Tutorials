---
category: general
date: 2026-09-27
description: Προσθέστε αριθμητική Bates σε PDF χρησιμοποιώντας το Aspose.PDF σε C#.
  Μάθετε πώς να φορτώνετε ένα έγγραφο PDF, να ορίζετε τις επιλογές αριθμητικής Bates
  και να αποθηκεύετε το ενημερωμένο αρχείο.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- load pdf document
- how to add bates numbering
- Aspose.PDF C#
- PDF Bates numbering example
language: el
lastmod: 2026-09-27
og_description: Προσθέστε αρίθμηση Bates σε PDF χρησιμοποιώντας το Aspose.PDF σε C#.
  Αυτό το σεμινάριο σας δείχνει πώς να φορτώσετε ένα έγγραφο PDF, να διαμορφώσετε
  την αρίθμηση Bates και να αποθηκεύσετε το αποτέλεσμα.
og_image_alt: Screenshot of a PDF page displaying Bates numbers in the footer
og_title: Προσθέστε αρίθμηση Bates σε PDF με το Aspose.PDF – Οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Add bates numbering to PDF using Aspose.PDF in C#. Learn how to load
    a PDF document, set Bates numbering options, and save the updated file.
  headline: Add bates numbering to PDF using Aspose.PDF in C#
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF processing
title: Προσθήκη αρίθμησης Bates σε PDF χρησιμοποιώντας το Aspose.PDF σε C#
url: /el/net/programming-with-text/add-bates-numbering-to-pdf-using-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη αρίθμησης Bates σε PDF χρησιμοποιώντας το Aspose.PDF σε C#

Αν χρειάζεστε **προσθήκη αρίθμησης Bates** σε ένα αρχείο PDF, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, έτοιμη‑για‑εκτέλεση λύση. Θα δείτε πώς να **φορτώσετε ένα έγγραφο PDF**, να διαμορφώσετε τις επιλογές αρίθμησης Bates και να γράψετε το αριθμημένο αρχείο ξανά στο δίσκο—όλα με το Aspose.PDF για .NET.

Η εφαρμογή αριθμών Bates είναι κοινή σε νομικές, αστυνομικές και αρχειακές διαδικασίες. Στο τέλος αυτού του tutorial θα μπορείτε να ενσωματώσετε ένα διαδοχικό αναγνωριστικό σε κάθε σελίδα, να προσαρμόσετε το πρόθεμα και να ξεκινήσετε την αρίθμηση από οποιονδήποτε αριθμό επιλέξετε.

## Τι θα μάθετε

* Πώς να **φορτώσετε το περιεχόμενο ενός PDF εγγράφου** σε ένα αντικείμενο `Aspose.Pdf.Document`.  
* Τα ακριβή βήματα **πώς να προσθέσετε αρίθμηση Bates** με `BatesNumberingOptions`.  
* Πώς να αποθηκεύσετε το τροποποιημένο αρχείο διατηρώντας την αρχική διάταξη και ποιότητα.  

Δεν απαιτούνται εξωτερικά εργαλεία—μόνο το πακέτο NuGet του Aspose.PDF και ένα περιβάλλον ανάπτυξης .NET (Visual Studio, VS Code ή Rider).  

---

## Βήμα 1: Εγκατάσταση του Aspose.PDF για .NET

Ανοίξτε το φάκελο του έργου σας σε ένα τερματικό και εκτελέστε:

```bash
dotnet add package Aspose.PDF
```

Το πακέτο περιλαμβάνει το namespace `Aspose.Pdf`, το οποίο παρέχει όλες τις κλάσεις που χρησιμοποιούνται σε αυτόν τον οδηγό. Μετά την εγκατάσταση, επαναφορτώστε το έργο ώστε το IDE να εντοπίσει τη νέα αναφορά.

## Βήμα 2: Φόρτωση PDF εγγράφου

Η φόρτωση του αρχικού αρχείου είναι η πρώτη ενέργεια επειδή η μηχανή αρίθμησης Bates λειτουργεί πάνω σε μια υπάρχουσα παρουσία `Document`.

```csharp
using Aspose.Pdf;

// ...

// Replace with the path to your input PDF
string inputPath = @"YOUR_DIRECTORY\input.pdf";

// Load the PDF document into memory
Document doc = new Document(inputPath);
```

**Γιατί είναι σημαντικό:** Η κλάση `Document` αναλύει τη δομή του PDF, παρέχοντάς σας πρόσβαση σε σελίδες, σημειώσεις και μεταδεδομένα. Χωρίς να φορτώσετε πρώτα το αρχείο, δεν μπορείτε να εφαρμόσετε καμία αρίθμηση.

## Βήμα 3: Διαμόρφωση επιλογών αρίθμησης Bates

Δημιουργήστε ένα αντικείμενο `BatesNumberingOptions` και ορίστε το επιθυμητό πρόθεμα, τον αριθμό εκκίνησης και προαιρετικές παραμέτρους μορφοποίησης.

```csharp
using Aspose.Pdf;

// ...

BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Text that appears before the numeric part
    Prefix = "CASE01",

    // First number to use (1 means the first page gets CASE01-1)
    StartNumber = 1,

    // Optional: customize the appearance
    // The default places the number in the footer, centered.
    // You can change Font, FontSize, Color, and Position if needed.
    // Example:
    // Font = FontRepository.FindFont("Arial"),
    // FontSize = 10,
    // Color = Color.Black,
    // Margin = new Margin(0, 0, 0, 20)
};
```

**Γιατί είναι σημαντικό:** Το `BatesNumberingOptions` καθορίζει στο Aspose.PDF πώς να δημιουργήσει την ετικέτα για κάθε σελίδα. Το `Prefix` σας βοηθά να ομαδοποιήσετε σχετικές υποθέσεις, ενώ το `StartNumber` σας επιτρέπει να συνεχίσετε μια ακολουθία από μια προηγούμενη παρτίδα.

## Βήμα 4: Αποθήκευση του PDF με εφαρμοσμένη αρίθμηση Bates

Περάστε το αντικείμενο επιλογών στη μέθοδο `Save`. Το Aspose.PDF γράφει τους αριθμούς απευθείας σε κάθε σελίδα.

```csharp
// Replace with the desired output path
string outputPath = @"YOUR_DIRECTORY\output.pdf";

// Save the document, applying the Bates numbering
doc.Save(outputPath, batesOptions);
```

**Γιατί είναι σημαντικό:** Η υπερφόρτωση `Save(string, BatesNumberingOptions)` συνδυάζει το βήμα απόδοσης με τη διαδικασία αρίθμησης, διασφαλίζοντας ότι το αρχείο εξόδου περιέχει τα ορατά αναγνωριστικά.

## Πλήρες παράδειγμα – όλα μαζί

Παρακάτω υπάρχει ένα ενιαίο, αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε. Δείχνει **πώς να προσθέσετε αρίθμηση Bates** από την αρχή μέχρι το τέλος.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the PDF document
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Set up Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                Prefix = "CASE01",
                StartNumber = 1,
                // Optional appearance tweaks:
                // Font = FontRepository.FindFont("Times New Roman"),
                // FontSize = 9,
                // Color = Color.DarkBlue,
                // Margin = new Margin(0, 0, 0, 15)
            };

            // 3️⃣ Save the document with Bates numbers
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            doc.Save(outputPath, batesOptions);

            Console.WriteLine($"Bates numbering added. Output saved to: {outputPath}");
        }
    }
}
```

### Αναμενόμενο αποτέλεσμα

Η εκτέλεση του προγράμματος παράγει το `output.pdf` όπου κάθε σελίδα εμφανίζει μια ετικέτα παρόμοια με:

```
CASE01-1
CASE01-2
CASE01-3
...
```

Οι αριθμοί εμφανίζονται στο υποσέλιδο από προεπιλογή, αλλά μπορείτε να τους μετακινήσετε ρυθμίζοντας την ιδιότητα `Margin` στο `BatesNumberingOptions`.

## Περιπτώσεις άκρων και κοινές παραλλαγές

| Κατάσταση | Τι να προσαρμόσετε |
|-----------|--------------------|
| **Διαφορετικό πρόθεμα ανά παρτίδα** | Αλλάξτε το `Prefix` πριν καλέσετε το `Save`. Μπορείτε να κάνετε βρόχο πάνω από πολλά έγγραφα με διαφορετικά προθέματα. |
| **Συνέχιση αρίθμησης από προηγούμενο αρχείο** | Ορίστε το `StartNumber` στον τελευταίο χρησιμοποιημένο αριθμό + 1. |
| **Τοποθέτηση αριθμών στο κεφαλίδα** | Χρησιμοποιήστε `batesOptions.Margin = new Margin(20, 0, 0, 0);` (επάνω περιθώριο) ή προσαρμόστε το `batesOptions.Position`. |
| **Προσαρμοσμένη γραμματοσειρά ή χρώμα** | Αναθέστε τις ιδιότητες `Font`, `FontSize` και `Color` όπως φαίνεται στην ενότητα με σχόλια. |
| **Μεγάλα PDF (1000+ σελίδες)** | Η λειτουργία είναι αποδοτική σε μνήμη· ωστόσο, μπορεί να θέλετε να ενεργοποιήσετε το `doc.OptimizeResources()` πριν την αποθήκευση για να μειώσετε το μέγεθος του αρχείου. |

**Συμβουλή:** Εάν η ροή εργασίας σας απαιτεί διαφορετικά σχήματα αρίθμησης ανά έγγραφο, ενσωματώστε τη λογική σε μια βοηθητική μέθοδο:

```csharp
static void ApplyBatesNumbering(string src, string dst, string prefix, int start)
{
    var doc = new Document(src);
    var opts = new BatesNumberingOptions { Prefix = prefix, StartNumber = start };
    doc.Save(dst, opts);
}
```

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να προσθέσετε αρίθμηση Bates** σε οποιοδήποτε PDF χρησιμοποιώντας το Aspose.PDF σε C#. Ο οδηγός κάλυψε τη φόρτωση του PDF εγγράφου, τη διαμόρφωση των επιλογών αρίθμησης και την αποθήκευση του τελικού αρχείου—όλα σε ένα ενιαίο, εκτελέσιμο πρόγραμμα.

Από εδώ μπορείτε να εξερευνήσετε συναφή θέματα όπως **προσθήκη υδατογραφιών**, **συγχώνευση πολλαπλών PDF**, ή **εξαγωγή κειμένου** με το Aspose.PDF. Πειραματιστείτε με διαφορετικές γραμματοσειρές, χρώματα και θέσεις για να ταιριάξετε τα πρότυπα μορφοποίησης του οργανισμού σας.

Έτοιμοι να αυτοματοποιήσετε τη ροή εργασίας των νομικών εγγράφων σας; Προσθέστε τον κώδικα στη διαδικασία κατασκευής, εκτελέστε τον σε παρτίδες αρχείων και αφήστε το Aspose.PDF να αναλάβει το δύσκολο μέρος. Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Δημιουργία PDF Εγγράφου C# – Προσθήκη Αρίθμησης Bates](/pdf/english/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/)
- [Προσθήκη Αρίθμησης Bates PDF – Οδηγός Βήμα‑Βήμα για Αρίθμηση Σελίδων PDF](/pdf/english/net/programming-with-pdf-pages/add-bates-numbering-pdf-step-by-step-guide-to-number-pdf-pag/)
- [Aspose PDF Tutorial – Εισαγωγή Κενής Σελίδας και Ενημέρωση Αρίθμησης Bates](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}