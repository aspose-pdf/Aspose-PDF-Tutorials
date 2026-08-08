---
category: general
date: 2026-06-05
description: Πώς να προσθέσετε αρίθμηση Bates σε PDF χρησιμοποιώντας C#. Μάθετε πώς
  να φορτώνετε ένα έγγραφο PDF, να ενημερώνετε την αρίθμηση σελίδων και να προσθέτετε
  σφραγίδες Bates γρήγορα.
draft: false
keywords:
- how to add bates numbering
- add bates numbers pdf
- load pdf document c#
- add bates stamps to pdf
- update pagination pdf
language: el
og_description: Πώς να προσθέσετε αρίθμηση Bates σε PDF χρησιμοποιώντας C#. Αυτός
  ο οδηγός δείχνει τη φόρτωση ενός PDF, την ενημέρωση της σελιδοποίησης και την αποθήκευση
  του σφραγισμένου εγγράφου.
og_title: Πώς να προσθέσετε αρίθμηση Bates σε PDF με C# – Βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to add bates numbering in PDF using C#. Learn to load a PDF document,
    update pagination, and add bates stamps quickly.
  headline: How to Add Bates Numbering in PDF with C# – Complete Guide
  type: TechArticle
- description: How to add bates numbering in PDF using C#. Learn to load a PDF document,
    update pagination, and add bates stamps quickly.
  name: How to Add Bates Numbering in PDF with C# – Complete Guide
  steps:
  - name: Load PDF Document in C#
    text: Before any numbering can happen, the PDF must be loaded into memory. Aspose.Pdf’s
      `Document` class does the heavy lifting, handling everything from encryption
      to page streams.
  - name: Add Bates Stamps to PDF
    text: The real hero of the library is `UpdatePagination()`. When you call it without
      parameters, Aspose automatically inserts Bates numbers on every page, using
      the default format `Page 1 of N`. If you need a custom prefix (e.g., “ABC‑2023‑”),
      you can supply a `PaginationInfo` object.
  - name: Save the Updated PDF
    text: After stamping, you simply persist the modified document. You can overwrite
      the original or write to a new file—both are safe as long as you respect file
      locks.
  - name: Full Working Example
    text: 'Putting the three pieces together yields a compact, production‑ready program:'
  type: HowTo
- questions:
  - answer: 'Pass the password to the `Document` constructor:'
    question: What if my PDF is password‑protected?
  - answer: 'Embed the font when you save: `pdf.FontEmbeddingMode = FontEmbeddingMode.Always;`.'
    question: Fonts missing on the target machine?
  - answer: The free evaluation works but adds a watermark. For production, acquire
      a license to remove it and unlock full pagination features.
    question: Do I need a license for Aspose.Pdf?
  type: FAQPage
tags:
- PDF
- C#
- Aspose.Pdf
title: Πώς να προσθέσετε αρίθμηση Bates σε PDF με C# – Πλήρης οδηγός
url: /el/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Προσθέσετε Αρίθμηση Bates σε PDF με C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να προσθέσετε αρίθμηση bates** σε ένα PDF χωρίς να ξοδεύετε ώρες παίζοντας με χειροκίνητα εργαλεία; Δεν είστε μόνοι. Σε πολλές νομικές, εγκληματολογικές ή διαδικασίες συμμόρφωσης, η σήμανση ενός εγγράφου με διαδοχικούς αριθμούς Bates είναι ένα αδιαπραγμάτευτο βήμα, και η υλοποίηση του προγραμματιστικά σε C# μπορεί να σας εξοικονομήσει πολύ χρόνο.

Σε αυτό το εκπαιδευτικό υλικό θα περάσουμε από μια καθαρή, ολοκληρωμένη λύση που σας δείχνει ακριβώς πώς να **φορτώσετε ένα PDF έγγραφο σε C#**, να ανανεώσετε την αρίθμηση σελίδων, και να **προσθέσετε σφραγίδες bates σε PDF** αρχεία χρησιμοποιώντας τη βιβλιοθήκη Aspose.Pdf. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση δείγμα κώδικα, μια σειρά πρακτικών συμβουλών, και μια σαφή ιδέα για το πώς να προσαρμόσετε τη διαδικασία στα δικά σας έργα.

## Τι Θα Μάθετε

- Πώς να αναφέρετε και να διαμορφώσετε το Aspose.Pdf για .NET.
- Το τρι‑βήμα μοτίβο: φόρτωση → ενημέρωση αρίθμησης → αποθήκευση.
- Γιατί το `UpdatePagination()` είναι η μαγεία πίσω από την αυτόματη **add bates numbers pdf**.
- Επιλογές προσαρμογής για τη μορφή, τη θέση και το στυλ του αριθμού Bates.
- Κοινά προβλήματα (π.χ., ελλιπείς γραμματοσειρές, μεγάλα αρχεία) και πώς να τα αποφύγετε.

> **Προαπαιτούμενα** – Χρειάζεστε .NET 6+ (ή .NET Framework 4.6+), μια αδειοδοτημένη έκδοση του Aspose.Pdf για .NET, και βασική κατανόηση της C#. Δεν απαιτούνται άλλα εξωτερικά εργαλεία.

![πώς να προσθέσετε αρίθμηση bates σε PDF χρησιμοποιώντας C#](image.png "πώς να προσθέσετε αρίθμηση bates σε PDF χρησιμοποιώντας C#")

## Πώς να Προσθέσετε Αρίθμηση Bates – Βήμα‑Βήμα

Παρακάτω χωρίζουμε τη διαδικασία σε τρία λογικά βήματα. Κάθε βήμα είναι τυλιγμένο σε δικό του **H2** τίτλο ώστε να μπορείτε να μεταβείτε απευθείας στο τμήμα που χρειάζεστε.

### Φόρτωση PDF Εγγράφου σε C#

Πριν μπορέσει να γίνει οποιαδήποτε αρίθμηση, το PDF πρέπει να φορτωθεί στη μνήμη. Η κλάση `Document` του Aspose.Pdf κάνει τη βαριά δουλειά, διαχειριζόμενη τα πάντα από την κρυπτογράφηση μέχρι τις ροές σελίδων.

```csharp
using System;
using Aspose.Pdf;          // Make sure the Aspose.Pdf namespace is referenced

class BatesNumberingDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF
        // Replace YOUR_DIRECTORY with the actual folder path on your machine.
        var inputPath = @"YOUR_DIRECTORY\input.pdf";

        // The `using` block ensures the document is properly disposed.
        using (var pdf = new Document(inputPath))
        {
            // The rest of the workflow continues inside this block.
            // ...
        }
    }
}
```

**Γιατί αυτό είναι σημαντικό:**
- Η δήλωση `using` εγγυάται ότι οι χειριστές αρχείων απελευθερώνονται, αποτρέποντας σφάλματα “αρχείο σε χρήση” αργότερα όταν προσπαθήσετε να αποθηκεύσετε.
- Η φόρτωση του αρχείου μία φορά διατηρεί τη χρήση μνήμης χαμηλή, ακόμη και για PDF με εκατοντάδες σελίδες.

### Προσθήκη Σφραγίδων Bates σε PDF

Ο πραγματικός ήρωας της βιβλιοθήκης είναι το `UpdatePagination()`. Όταν το καλέσετε χωρίς παραμέτρους, το Aspose εισάγει αυτόματα αριθμούς Bates σε κάθε σελίδα, χρησιμοποιώντας την προεπιλεγμένη μορφή `Page 1 of N`. Εάν χρειάζεστε προσαρμοσμένο πρόθεμα (π.χ., “ABC‑2023‑”), μπορείτε να παρέχετε ένα αντικείμενο `PaginationInfo`.

```csharp
using Aspose.Pdf.Text;

// Inside the using block from the previous step:
{
    // 👉 Step 2: Configure and apply Bates numbering
    var pagination = new PaginationInfo
    {
        // Example: "ABC-2023-" will be prepended to each page number.
        Prefix = "ABC-2023-",
        // Suffix can be left empty or used for things like "-END".
        Suffix = string.Empty,
        // Choose where the stamp appears. Bottom‑right is common.
        HorizontalAlignment = HorizontalAlignment.Right,
        VerticalAlignment = VerticalAlignment.Bottom,
        // Font settings ensure the numbers are legible.
        Font = new FontRepository().FindFont("Arial"),
        FontSize = 10,
        // Optional: Add a border or background if you need a stamp look.
        // Border = new BorderInfo(BorderSide.All, 0.5f, Color.Black)
    };

    // This call adds the stamps to every page.
    pdf.Pages.UpdatePagination(pagination);
}
```

**Γιατί αυτό λειτουργεί:**
- `PaginationInfo` σας δίνει λεπτομερή έλεγχο πάνω στην **add bates stamps to pdf** χωρίς να γράψετε εσείς βρόχο.
- Η βιβλιοθήκη διαχειρίζεται αυτόματα τον αριθμό σελίδων, την προσθήκη μηδενικών και ακόμη και γλώσσες από δεξιά προς αριστερά αν χρειαστεί.

### Αποθήκευση του Ενημερωμένου PDF

Μετά τη σήμανση, απλώς αποθηκεύετε το τροποποιημένο έγγραφο. Μπορείτε να αντικαταστήσετε το αρχικό ή να γράψετε σε νέο αρχείο—και τα δύο είναι ασφαλή εφόσον τηρείτε τα κλειδώματα αρχείων.

```csharp
// 👉 Step 3: Save the output PDF
var outputPath = @"YOUR_DIRECTORY\output.pdf";
pdf.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

**Συμβουλή:** Αν επεξεργάζεστε πολλά αρχεία σε παρτίδα, σκεφτείτε να χρησιμοποιήσετε `pdf.Save(outputPath, SaveFormat.PdfA_1b)` για να δημιουργήσετε ένα αρχείο συμβατό με PDF/A, το οποίο συχνά απαιτείται για νομικά αποδεικτικά στοιχεία.

### Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας τα τρία κομμάτια προκύπτει ένα συμπαγές, έτοιμο για παραγωγή πρόγραμμα:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class BatesNumberingDemo
{
    static void Main()
    {
        var inputPath = @"YOUR_DIRECTORY\input.pdf";
        var outputPath = @"YOUR_DIRECTORY\output.pdf";

        using (var pdf = new Document(inputPath))
        {
            var pagination = new PaginationInfo
            {
                Prefix = "ABC-2023-",
                HorizontalAlignment = HorizontalAlignment.Right,
                VerticalAlignment = VerticalAlignment.Bottom,
                Font = new FontRepository().FindFont("Arial"),
                FontSize = 10
            };

            // Add or refresh Bates numbers
            pdf.Pages.UpdatePagination(pagination);

            // Persist the changes
            pdf.Save(outputPath);
        }

        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
Ανοίξτε το `output.pdf` σε οποιονδήποτε προβολέα και θα δείτε μια ακολουθία όπως `ABC-2023-001`, `ABC-2023-002`, … στο κάτω‑δεξιό μέρος κάθε σελίδας. Οι αριθμοί αυξάνονται αυτόματα, ακόμη και αν αργότερα εισάγετε ή διαγράψετε σελίδες και ξανατρέξετε το `UpdatePagination()`.

## Προσαρμογή Εμφάνισης Αριθμού Bates (Προαιρετικό)

Αν οι προεπιλεγμένες ρυθμίσεις δεν ταιριάζουν στη ροή εργασίας σας, μπορείτε να ρυθμίσετε μερικές ακόμη ιδιότητες:

| Ιδιότητα | Τι ελέγχει | Παράδειγμα |
|----------|------------|------------|
| `StartNumber` | Πρώτος αριθμός στη σειρά | `StartNumber = 1000` |
| `NumberStyle` | Αριθμητικό, Ρωμαϊκό ή αλφαριθμητικό | `NumberStyle = NumberStyle.AlphaNumeric` |
| `Margin` | Απόσταση από τις άκρες της σελίδας (σε σημεία) | `Margin = new MarginInfo(10, 10, 10, 10)` |
| `Color` | Χρώμα κειμένου για τη σφραγίδα | `Color = Color.Red` |

```csharp
pagination.StartNumber = 1000;
pagination.NumberStyle = NumberStyle.AlphaNumeric;
pagination.Margin = new MarginInfo(5, 5, 5, 5);
pagination.Color = Color.Red;
```

Αυτές οι ρυθμίσεις είναι ιδιαίτερα χρήσιμες όταν χρειάζεται να **add bates numbers pdf** για δικαστικές καταθέσεις που απαιτούν συγκεκριμένη μορφή.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

- **Τι γίνεται αν το PDF μου είναι προστατευμένο με κωδικό;**  
  Περνάτε τον κωδικό στον κατασκευαστή `Document`:  
  `new Document(inputPath, new LoadOptions { Password = "secret" })`.

- **Μεγάλα PDF (>500 MB) προκαλούν OutOfMemoryException.**  
  Ενεργοποιήστε τη ροή: `var pdf = new Document(inputPath) { EnableMemoryOptimization = true };`.

- **Λείπουν γραμματοσειρές στον προορισμό;**  
  Ενσωματώστε τη γραμματοσειρά κατά την αποθήκευση: `pdf.FontEmbeddingMode = FontEmbeddingMode.Always;`.

- **Χρειάζομαι άδεια για το Aspose.Pdf;**  
  Η δωρεάν αξιολόγηση λειτουργεί αλλά προσθέτει υδατογράφημα. Για παραγωγή, αποκτήστε άδεια για να το αφαιρέσετε και να ξεκλειδώσετε όλες τις δυνατότητες αρίθμησης.

## Συνοπτική Επισκόπηση

Καλύψαμε **πώς να προσθέσετε αρίθμηση bates** σε PDF χρησιμοποιώντας C# από την αρχή μέχρι το τέλος. Τα βασικά βήματα—**φόρτωση pdf εγγράφου c#**, κλήση του `UpdatePagination()` (η καρδιά της **add bates stamps to pdf**), και **αποθήκευση**—είναι απλά αλλά ισχυρά. Προσαρμόζοντας το `PaginationInfo`, μπορείτε να ικανοποιήσετε σχεδόν οποιαδήποτε νομική ή εγκληματολογική απαίτηση, και οι ενσωματωμένες προστασίες διατηρούν τον κώδικά σας ανθεκτικό για μεγάλα ή προστατευμένα αρχεία.

## Τι Ακολουθεί;

- Βυθιστείτε πιο βαθιά στην **add bates numbers pdf** δημιουργώντας ξεχωριστές σελίδες ευρετηρίου που καταγράφουν κάθε σφραγίδα.
- Συνδυάστε αυτή την προσέγγιση με OCR για να ενσωματώσετε αναζητήσιμο κείμενο μαζί με τους αριθμούς Bates.
- Εξερευνήστε άλλες δυνατότητες του Aspose.Pdf όπως υδατογράφημα, ψηφιακές υπογραφές ή μετατροπή PDF/A.

Νιώστε ελεύθεροι να πειραματιστείτε, να σπάσετε πράγματα και μετά να τα διορθώσετε—αυτή είναι η πραγματική εξάσκηση στην αυτοματοποίηση PDF. Αν αντιμετωπίσετε κάποιο πρόβλημα ή έχετε μια έξυπνη περίπτωση χρήσης, αφήστε ένα σχόλιο παρακάτω. Καλή κωδικοποίηση!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω εκπαιδευτικά υλικά καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Προσθέσετε και να Προσαρμόσετε Αριθμούς Σελίδων σε PDF χρησιμοποιώντας Aspose.PDF για .NET | Οδηγός Διαχείρισης Εγγράφων](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Πώς να Προσθέσετε Σφραγίδες Αριθμών Σελίδων σε PDF χρησιμοποιώντας Aspose.PDF για .NET | Υδατογραφήματα & Φόντα](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Πώς να Προσθέσετε Σφραγίδες Σελίδας σε PDF χρησιμοποιώντας Aspose.PDF για .NET&#58; Πλήρης Οδηγός](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}