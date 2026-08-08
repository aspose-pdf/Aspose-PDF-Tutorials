---
category: general
date: 2026-06-30
description: Προσθέστε αρίθμηση Bates σε PDF χρησιμοποιώντας το Aspose.PDF σε C#.
  Μάθετε πώς να αριθμείτε τις σελίδες PDF, να ορίσετε προσαρμοσμένο πρόθεμα και να
  δημιουργήσετε ένα αξιόπιστο έγγραφο αρίθμησης Bates.
draft: false
keywords:
- add bates numbering
- how to add bates
- number pdf pages
- how to number pdf
- bates numbering document
language: el
og_description: Προσθέστε αριθμήση Bates σε PDF με το Aspose.PDF. Αυτός ο οδηγός δείχνει
  πώς να αριθμήσετε τις σελίδες PDF και να δημιουργήσετε ένα έγγραφο αριθμήσης Bates
  σε C#.
og_title: Προσθήκη αρίθμησης Bates σε PDF – Οδηγός Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add Bates numbering to PDF using Aspose.PDF in C#. Learn how to number
    PDF pages, set a custom prefix, and create a reliable Bates numbering document.
  headline: Add Bates Numbering to PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Add Bates numbering to PDF using Aspose.PDF in C#. Learn how to number
    PDF pages, set a custom prefix, and create a reliable Bates numbering document.
  name: Add Bates Numbering to PDF with Aspose.PDF – Complete Guide
  steps:
  - name: Customizing Appearance (Optional)
    text: 'If you need a different font, size, or placement, you can tweak the `BatesNumbering`
      properties:'
  - name: Expected Output
    text: Open `bates_numbered.pdf` in any PDF viewer. You’ll see a label like **CASE‑1000**
      on the first page, **CASE‑1001** on the second, and so on. The numbers appear
      in the bottom‑left corner by default (or wherever you set `XIndent`/`YIndent`).
  - name: 1. What if the PDF is huge (hundreds of MB)?
    text: 'Aspose.PDF streams pages to disk by default, so memory consumption stays
      low. However, you can explicitly enable **compression**:'
  - name: 2. Need a different numbering format (e.g., suffix instead of prefix)?
    text: 'Set the `Suffix` property:'
  - name: 3. How to restart numbering for a new section?
    text: Call `bates.StartNumber = 1;` before processing the next batch, or create
      a second `BatesNumbering` instance.
  - name: 4. The PDF already contains watermarks—will the numbers overlap?
    text: 'Adjust `XIndent` and `YIndent` to move the numbers away from existing elements.
      You can also change the `Position` enum (`BatesNumberingPosition.TopRight`,
      etc.):'
  - name: 5. Does this work with encrypted PDFs?
    text: 'If the source PDF is password‑protected, open it like this:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF processing
- Bates numbering
title: Προσθήκη αρίθμησης Bates σε PDF με το Aspose.PDF – Πλήρης Οδηγός
url: /el/net/programming-with-pdf-pages/add-bates-numbering-to-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Bates Numbering σε PDF με Aspose.PDF – Πλήρης Οδηγός

Έχετε χρειαστεί ποτέ να **add bates numbering** σε ένα PDF αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε ο μόνος—νομικές ομάδες, ελεγκτές και ακόμη και προγραμματιστές συχνά ρωτούν *how to add bates* για την παρακολούθηση μεγάλων συνόλων εγγράφων. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα μια πλήρη, έτοιμη‑για‑εκτέλεση λύση που αριθμεί τις σελίδες PDF, εφαρμόζει ένα προσαρμοσμένο πρόθεμα και αποθηκεύει ένα νέο **bates numbering document**. Χωρίς περιττά, μόνο ο κώδικας που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σήμερα.

Θα καλύψουμε τα πάντα, από τη ρύθμιση του Aspose.PDF, την επιλογή αριθμού εκκίνησης, τη διαχείριση ειδικών περιπτώσεων όπως τεράστια αρχεία, και ακόμη την προσαρμογή της μορφής αν χρειάζεστε κάτι πέρα από το προεπιλεγμένο. Στο τέλος θα μπορείτε να **number pdf pages** αυτόματα, και θα καταλάβετε γιατί αυτή η προσέγγιση είναι τόσο ανθεκτική όσο και εύκολη στη συντήρηση.

## Προαπαιτήσεις

- .NET 6.0 ή νεότερο (το παράδειγμα χρησιμοποιεί .NET 6 αλλά λειτουργεί με .NET Core 3.1+)
- Άδεια Aspose.PDF for .NET (η δωρεάν αξιολόγηση λειτουργεί για δοκιμές)
- Ένα αρχείο PDF που θέλετε να επεξεργαστείτε (ονομάζεται `source.pdf` στο παράδειγμα)
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή C# προτιμάτε

Αυτό είναι όλο—δεν χρειάζονται επιπλέον πακέτα NuGet εκτός από το Aspose.PDF.

## Βήμα 1: Εγκατάσταση Aspose.PDF για .NET

Ανοίξτε το τερματικό ή το Package Manager Console και εκτελέστε:

```bash
dotnet add package Aspose.PDF
```

ή, μέσα στο Visual Studio:

```
Tools → NuGet Package Manager → Manage NuGet Packages for Solution…
Search “Aspose.PDF” and click Install.
```

> **Pro tip:** Αν σκοπεύετε να επεξεργαστείτε χιλιάδες σελίδες, ενεργοποιήστε **Aspose.PDF’s memory‑saving mode** ορίζοντας `PdfConversion.SaveOptions.UseObjectPooling = true;` αργότερα.

## Βήμα 2: Δημιουργία Απλού Σκελετού Console App

Ας δημιουργήσουμε ένα ελάχιστο console app ώστε να μπορείτε να τρέξετε τον κώδικα αμέσως:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in the next steps.
        }
    }
}
```

Αποθηκεύστε το αρχείο ως `Program.cs`. Αυτός ο σκελετός μας δίνει ένα καθαρό σημείο για να ενσωματώσουμε τη λογική **bates numbering**.

## Βήμα 3: Άνοιγμα του Πηγαίου Αρχείου PDF

Η πρώτη πραγματική ενέργεια είναι το άνοιγμα του PDF που θέλετε να σφραγίσετε. Θα χρησιμοποιήσουμε ένα `using` block ώστε το handle του αρχείου να απελευθερώνεται αυτόματα:

```csharp
// Step 3: Open the source PDF document
using (var doc = new Document("YOUR_DIRECTORY/source.pdf"))
{
    // Subsequent steps go here.
}
```

> **Why a `using` block?** Εξασφαλίζει ότι η υποκείμενη ροή αρχείου κλείνει, αποτρέποντας προβλήματα κλειδώματος αρχείου όταν αργότερα προσπαθήσετε να αντικαταστήσετε το ίδιο αρχείο.

## Βήμα 4: Ρύθμιση του BatesNumbering Facade

Το Aspose.PDF παρέχει ένα βολικό façade με όνομα `BatesNumbering`. Κρύβει τη χαμηλού επιπέδου διαχείριση σελίδα‑με‑σελίδα και σας επιτρέπει να εστιάσετε στην αριθμητική.

```csharp
// Step 4: Create a Bates numbering facade
var bates = new BatesNumbering
{
    // Step 4a: Choose the starting number
    StartNumber = 1000,

    // Step 4b: Add an optional prefix (e.g., CASE-)
    Prefix = "CASE-"
    
    // You can also set a suffix, font size, or position if needed.
};
```

### Προσαρμογή Εμφάνισης (Προαιρετικό)

Αν χρειάζεστε διαφορετική γραμματοσειρά, μέγεθος ή θέση, μπορείτε να τροποποιήσετε τις ιδιότητες του `BatesNumbering`:

```csharp
bates.FontSize = 10;               // Smaller than the default 12
bates.TextColor = Color.Black;    // Ensure high contrast
bates.XIndent = 20;               // Move number 20 points from the left edge
bates.YIndent = 30;               // Move number 30 points from the bottom edge
```

Αυτές οι ρυθμίσεις είναι χρήσιμες όταν η προεπιλεγμένη θέση παρεμβαίνει στο υπάρχον περιεχόμενο.

## Βήμα 5: Εφαρμογή του Bates Numbering στο Έγγραφο

Τώρα σφραγίζουμε πραγματικά τους αριθμούς σε κάθε σελίδα:

```csharp
// Step 5: Apply the Bates numbering to the document
bates.AddBatesNumbering(doc);
```

Πίσω από τη σκηνή, το Aspose.PDF διατρέχει κάθε σελίδα, εισάγει τη μορφοποιημένη συμβολοσειρά (π.χ. `CASE-1000`, `CASE-1001`, …) και σέβεται τυχόν επιλογές διάταξης που ορίσατε νωρίτερα.

## Βήμα 6: Αποθήκευση του Νέου Αριθμημένου PDF

Τέλος, γράφουμε το αποτέλεσμα στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή να δημιουργήσετε ένα νέο—εδώ θα κρατήσουμε και τα δύο για ασφάλεια:

```csharp
// Step 6: Save the newly numbered PDF
doc.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering applied successfully!");
```

Η εκτέλεση του προγράμματος θα πρέπει να παραγάγει ένα αρχείο με όνομα `bates_numbered.pdf` με κάθε σελίδα σαφώς επισημασμένη.

### Αναμενόμενο Αποτέλεσμα

Ανοίξτε το `bates_numbered.pdf` σε οποιονδήποτε προβολέα PDF. Θα δείτε μια ετικέτα όπως **CASE‑1000** στην πρώτη σελίδα, **CASE‑1001** στη δεύτερη, κ.ο.κ. Οι αριθμοί εμφανίζονται στην κάτω‑αριστερή γωνία εξ ορισμού (ή όπου έχετε ορίσει `XIndent`/`YIndent`).

## Πλήρης Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι ο πλήρης κώδικας που μπορείτε να αντιγράψετε‑και‑επικολλήσετε:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            const string sourcePath = "YOUR_DIRECTORY/source.pdf";
            const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";

            // Open the source PDF
            using (var doc = new Document(sourcePath))
            {
                // Configure Bates numbering
                var bates = new BatesNumbering
                {
                    StartNumber = 1000,
                    Prefix = "CASE-",
                    // Optional customizations:
                    // FontSize = 10,
                    // TextColor = Color.Black,
                    // XIndent = 20,
                    // YIndent = 30
                };

                // Apply numbering
                bates.AddBatesNumbering(doc);

                // Save the result
                doc.Save(outputPath);
                Console.WriteLine($"Bates numbering added. Saved to: {outputPath}");
            }
        }
    }
}
```

Τρέξτε `dotnet run` από το φάκελο του έργου, και θα δείτε το μήνυμα στην κονσόλα που επιβεβαιώνει την επιτυχία.

## Edge Cases & Common Questions

### 1. Τι γίνεται αν το PDF είναι τεράστιο (εκατοντάδες MB);

Το Aspose.PDF μεταφέρει τις σελίδες στο δίσκο από προεπιλογή, έτσι η κατανάλωση μνήμης παραμένει χαμηλή. Ωστόσο, μπορείτε ρητά να ενεργοποιήσετε **compression**:

```csharp
doc.Compress();
```

### 2. Χρειάζεστε διαφορετική μορφή αρίθμησης (π.χ. επίθημα αντί προθέματος);

Ορίστε την ιδιότητα `Suffix`:

```csharp
bates.Suffix = "-2026";
```

Μπορείτε να συνδυάσετε και τα δύο:

```csharp
bates.Prefix = "CASE-";
bates.Suffix = "-2026";
```

Αποτέλεσμα: `CASE-1000-2026`.

### 3. Πώς να επανεκκινήσετε την αρίθμηση για νέα ενότητα;

Καλέστε `bates.StartNumber = 1;` πριν επεξεργαστείτε την επόμενη παρτίδα, ή δημιουργήστε ένα δεύτερο αντικείμενο `BatesNumbering`.

### 4. Το PDF περιέχει ήδη υδατογραφήματα—θα επικαλυφθούν οι αριθμοί;

Ρυθμίστε τα `XIndent` και `YIndent` ώστε να μετακινήσετε τους αριθμούς μακριά από υπάρχοντα στοιχεία. Μπορείτε επίσης να αλλάξετε το enum `Position` (`BatesNumberingPosition.TopRight`, κλπ.):

```csharp
bates.Position = BatesNumberingPosition.TopRight;
```

### 5. Λειτουργεί αυτό με κρυπτογραφημένα PDFs;

Αν το πηγαίο PDF είναι προστατευμένο με κωδικό, ανοίξτε το ως εξής:

```csharp
var doc = new Document(sourcePath, new LoadOptions { Password = "yourPassword" });
```

Το υπόλοιπο του workflow παραμένει αμετάβλητο.

## Συμβουλές για Παραγωγικές Υλοποιήσεις

- **License early**: Εισάγετε `Aspose.Pdf.License license = new Aspose.Pdf.License(); license.SetLicense("Aspose.Pdf.lic");` στην αρχή του `Main` για να αποφύγετε το υδατογράφημα αξιολόγησης.
- **Parallel processing**: Για παρτίδες λειτουργίες σε πολλά αρχεία, τυλίξτε τη λογική ανά‑αρχείο σε έναν βρόχο `Parallel.ForEach`—απλώς προσέξτε τα όρια I/O.
- **Logging**: Use `Ser

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική Σας

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add a Text Stamp to PDF Using Aspose.PDF .NET: Comprehensive Guide](/pdf/english/net/watermarks-backgrounds/add-text-stamp-pdf-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}