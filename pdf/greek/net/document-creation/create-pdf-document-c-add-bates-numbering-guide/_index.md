---
category: general
date: 2026-02-28
description: Δημιουργήστε έγγραφο PDF C# με αρίθμηση Bates. Μάθετε πώς να προσθέσετε
  αρίθμηση Bates σε PDF, να ορίσετε προθέματα και να δημιουργήσετε διαδοχικούς αριθμούς
  PDF σε έναν ενιαίο οδηγό.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add document identification numbers
- add sequential pdf numbers
language: el
og_description: Δημιουργήστε έγγραφο PDF C# με αρίθμηση Bates. Αυτό το σεμινάριο δείχνει
  πώς να προσθέσετε αρίθμηση Bates σε PDF, να ορίσετε προσαρμοσμένα προθέματα και
  να παράγετε διαδοχικούς αριθμούς PDF.
og_title: Δημιουργία εγγράφου PDF C# – Προσθήκη αρίθμησης Bates
tags:
- Aspose.PDF
- C#
- PDF automation
title: Δημιουργία εγγράφου PDF C# – Οδηγός προσθήκης αρίθμησης Bates
url: /el/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PDF Εγγράφου C# – Οδηγός Προσθήκης Αρίθμησης Bates

Έχετε αναρωτηθεί ποτέ πώς να **δημιουργήσετε PDF έγγραφο C#** που ήδη περιέχει ένα μοναδικό αναγνωριστικό σε κάθε σελίδα; Αυτό είναι ένα κοινό πρόβλημα όταν χρειάζεται να παρακολουθείτε νομικά αρχεία, καταθέσεις σε δικαστήριο ή οποιοδήποτε σύνολο PDF που πρέπει να είναι αναζητήσιμο με αριθμό. Τα καλά νέα; Με το Aspose.PDF μπορείτε να προσθέσετε αριθμούς Bates με λίγες μόνο γραμμές κώδικα — χωρίς χειροκίνητη επεξεργασία.

Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία: φόρτωση ενός υπάρχοντος PDF, διαμόρφωση της **προσθήκης αριθμησης bates pdf**, εφαρμογή των αριθμών και τέλος αποθήκευση του αποτελέσματος. Στο τέλος θα μπορείτε να **προσθέσετε αριθμούς ταυτοποίησης εγγράφου** και ακόμη και **προσθέσετε διαδοχικούς αριθμούς PDF** αυτόματα, όλα από C#.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (το API λειτουργεί επίσης με .NET Framework 4.5+)
- Ένα αδειοδοτημένο αντίγραφο του **Aspose.PDF for .NET** (η δωρεάν δοκιμή λειτουργεί για δοκιμές)
- Ένα αρχείο PDF εισόδου που θέλετε να αριθμήσετε (θα το ονομάσουμε `input.pdf`)
- Visual Studio 2022 (ή οποιοδήποτε IDE προτιμάτε)

Δεν απαιτούνται επιπλέον πακέτα NuGet πέρα από το Aspose.PDF.

![Δημιουργία PDF Εγγράφου C# με αριθμηση Bates](https://example.com/image.png "Παράδειγμα δημιουργίας PDF Εγγράφου C#")

## Βήμα 1: Φόρτωση του Πηγαίου PDF Εγγράφου

Πριν μπορέσετε να **προσθέσετε αριθμηση bates pdf**, χρειάζεστε ένα αντικείμενο `Document` που να αντιπροσωπεύει το αρχείο στο δίσκο.

```csharp
using Aspose.Pdf;

// Load the source PDF document
var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

*Γιατί είναι σημαντικό*: Η κλάση `Document` είναι το σημείο εισόδου για κάθε λειτουργία στο Aspose.PDF. Απομονώνει το σύστημα αρχείων, ώστε να μπορείτε να εργάζεστε με σελίδες, σημειώσεις και μεταδεδομένα χωρίς να αγγίζετε τα ακατέργαστα bytes.

> **Συμβουλή επαγγελματία:** Αν επεξεργάζεστε πολλά αρχεία σε βρόχο, επαναχρησιμοποιήστε το ίδιο αντικείμενο `Document` μόνο όταν η πηγή είναι ίδια· διαφορετικά, δημιουργήστε νέο αντικείμενο για κάθε αρχείο ώστε να αποφύγετε διαρροές μνήμης.

## Βήμα 2: Ορισμός Επιλογών Αρίθμησης Bates

Εδώ η **διαδικασία προσθήκης bates** γίνεται συγκεκριμένη. Διαμορφώνετε ένα αντικείμενο `BatesNumberingOptions` για να πείτε στο Aspose ποιο πρόθεμα πρέπει να χρησιμοποιηθεί, από πού να ξεκινήσει και πόσο μεγάλο πρέπει να είναι το γράμμα.

```csharp
// Define Bates numbering options (prefix, start number, font size)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",   // You can change this to any string you need
    Start = 1000,      // Starting number – useful for continuous numbering across batches
    FontSize = 9       // Small enough to fit in the margin but still readable
};
```

*Γιατί είναι σημαντικό*: Το `Prefix` σας επιτρέπει να ενσωματώσετε έναν αναγνωριστικό υπόθεσης (π.χ., “ABC-”). Η ιδιότητα `Start` είναι κρίσιμη όταν **προσθέτετε διαδοχικούς αριθμούς PDF** σε πολλά έγγραφα — απλώς αυξήστε την τιμή. Και το `FontSize` εξασφαλίζει ότι οι αριθμοί δεν θα καλύπτουν το υπάρχον περιεχόμενο.

## Βήμα 3: Εφαρμογή Αρίθμησης Bates σε Ολόκληρο το Έγγραφο

Τώρα πραγματικά σφραγίζουμε τους αριθμούς σε κάθε σελίδα. Η κλάση `BatesNumbering` κάνει όλη τη βαριά δουλειά.

```csharp
// Apply Bates numbering to the entire document
var bates = new BatesNumbering();
bates.AddBatesNumbering(pdfDocument, batesOptions);
```

*Γιατί είναι σημαντικό*: Στο παρασκήνιο, το Aspose διασχίζει κάθε σελίδα, υπολογίζει τον κατάλληλο αριθμό (Prefix + (Start + pageIndex)) και τον σχεδιάζει στην κάτω‑δεξιά γωνία εξ ορισμού. Μπορείτε να προσαρμόσετε τη θέση αργότερα, αλλά η προεπιλογή λειτουργεί για τα περισσότερα νομικά έγγραφα.

> **Συχνή ερώτηση:** *Τι γίνεται αν χρειάζομαι να αριθμήσω μόνο ένα υποσύνολο σελίδων;*  
> Χρησιμοποιήστε την υπερφόρτωση `AddBatesNumbering(Document, BatesNumberingOptions, int startPage, int endPage)` για να περιορίσετε το εύρος.

## Βήμα 4: Αποθήκευση του PDF με Εφαρμοσμένους Αριθμούς Bates

Το τελικό βήμα είναι η εγγραφή του τροποποιημένου εγγράφου πίσω στο δίσκο.

```csharp
// Save the PDF with Bates numbers applied
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

*Γιατί είναι σημαντικό*: Η μέθοδος `Save` σέβεται την αρχική μορφή αρχείου, έτσι καταλήγετε με ένα τυπικό PDF που μπορεί να ανοίξει οποιοσδήποτε προβολέας — πλήρες με **προσθήκη αριθμών ταυτοποίησης εγγράφου** σε κάθε σελίδα.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα αυτόνομο πρόγραμμα που μπορείτε να επικολλήσετε σε μια νέα εφαρμογή κονσόλας και να τρέξετε αμέσως.

```csharp
using System;
using Aspose.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF document
            var inputPath = @"YOUR_DIRECTORY/input.pdf";
            var pdfDocument = new Document(inputPath);

            // 2️⃣ Define Bates numbering options (prefix, start number, font size)
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                FontSize = 9
            };

            // 3️⃣ Apply Bates numbering to the entire document
            var bates = new BatesNumbering();
            bates.AddBatesNumbering(pdfDocument, batesOptions);

            // 4️⃣ Save the PDF with Bates numbers applied
            var outputPath = @"YOUR_DIRECTORY/output.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbering added successfully. Output saved to {outputPath}");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Ανοίξτε το `output.pdf` σε οποιονδήποτε προβολέα· θα δείτε “ABC‑1000”, “ABC‑1001”, … τυπωμένα στην κάτω‑δεξιά γωνία κάθε σελίδας. Οι αριθμοί είναι κείμενο που μπορεί να επιλεγεί, επομένως είναι αναζητήσιμοι και μπορούν να αντιγραφούν — ακριβώς αυτό που περιμένετε από μια σωστή υλοποίηση **προσθήκης διαδοχικών αριθμών PDF**.

## Περιπτώσεις Άκρων & Παραλλαγές

### Προσαρμοσμένη Τοποθέτηση

Αν η προεπιλεγμένη γωνία συγκρούεται με υπάρχοντα υποσέλιδα, μπορείτε να μετακινήσετε τη θέση:

```csharp
batesOptions.Position = new Position(10, 10); // X, Y from the bottom‑left
```

### Διαφορετικές Μορφές Αριθμών

Θέλετε αριθμούς με μηδενικά στην αρχή (π.χ., 001000); Χρησιμοποιήστε το `NumberFormat`:

```csharp
batesOptions.NumberFormat = "D6"; // Pads to 6 digits
```

### Πολλαπλά Αρχεία σε Παρτίδα

Κατά την επεξεργασία πολλών PDF, διατηρήστε έναν τρέχοντα μετρητή:

```csharp
int globalStart = 5000;
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY\Batch", "*.pdf"))
{
    var doc = new Document(file);
    var opts = new BatesNumberingOptions
    {
        Prefix = "BATCH-",
        Start = globalStart,
        FontSize = 9
    };
    new BatesNumbering().AddBatesNumbering(doc, opts);
    doc.Save(Path.ChangeExtension(file, ".bated.pdf"));
    globalStart += doc.Pages.Count; // Increment for the next file
}
```

### Διαχείριση PDF με Κωδικό Πρόσβασης

Αν το πηγαίο PDF είναι κρυπτογραφημένο, περάστε τον κωδικό πρόσβασης κατά τη δημιουργία του `Document`:

```csharp
var pdfDocument = new Document("protected.pdf", new LoadOptions { Password = "mySecret" });
```

## Συχνές Ερωτήσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Μπορώ να χρησιμοποιήσω διαφορετική βιβλιοθήκη;** | Ναι, βιβλιοθήκες όπως iTextSharp ή PdfSharp υποστηρίζουν επίσης εισαγωγή κειμένου σε επίπεδο σελίδας, αλλά το Aspose.PDF προσφέρει το πιο απλό API για αριθμηση Bates. |
| **Επηρεάζει το μέγεθος του αρχείου;** | Η προσθήκη μερικών bytes κειμένου ανά σελίδα είναι αμελητέα· το μέγεθος εξόδου συνήθως αυξάνεται λιγότερο από 1 KB ανά σελίδα. |
| **Είναι η αρίθμηση αναζητήσιμη;** | Απόλυτα. Το Aspose γράφει τους αριθμούς ως αντικείμενα κειμένου, όχι ως εικόνες, ώστε να μπορούν να ευρετηριαστούν από τους αναγνώστες PDF. |
| **Τι γίνεται αν χρειάζομαι διαφορετική γραμματοσειρά;** | Ορίστε `batesOptions.Font` σε ένα αντικείμενο `Font` (π.χ., `FontRepository.FindFont("Arial")`). |

## Συμπέρασμα

Δείξαμε πώς να **δημιουργήσετε PDF έγγραφο C#** και άμεσα **προσθέσετε αριθμηση bates pdf** χρησιμοποιώντας το Aspose.PDF. Η διαδικασία είναι απλή, αξιόπιστη και πλήρως προγραμματιζόμενη — ιδανική για νομικές εταιρείες, κυβερνητικούς οργανισμούς ή οποιονδήποτε οργανισμό που πρέπει να **προσθέσει αριθμούς ταυτοποίησης εγγράφου** και **προσθέσει διαδοχικούς αριθμούς PDF** σε μεγάλες παρτίδες αρχείων.

Χρησιμοποιήστε αυτή τη βάση και πειραματιστείτε: δοκιμάστε διαφορετικά προθέματα για διαφορετικά τμήματα, συνδέστε την αρίθμηση σε πολλαπλά αρχεία ή ενσωματώστε QR codes δίπλα στους αριθμούς Bates για επιπλέον ιχνηλασιμότητα. Οι δυνατότητες είναι απεριόριστες μόλις έχετε το βασικό workflow.

Αν βρήκατε αυτόν τον οδηγό χρήσιμο, μοιραστείτε τον, αφήστε ένα σχόλιο ή εξερευνήστε τα άλλα μας guides για επεξεργασία PDF με C#. Καλό κώδικα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}