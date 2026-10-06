---
category: general
date: 2026-03-03
description: Δημιουργία εγγράφου PDF C# με αρίθμηση Bates – μάθετε πώς να προσθέτετε
  Bates, να προσθέτετε διαδοχικούς αριθμούς σελίδων και να δημιουργείτε Bates σε λίγα
  μόνο βήματα.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- how to generate bates
language: el
og_description: Δημιουργία PDF εγγράφου C# με αρίθμηση Bates. Αυτός ο οδηγός δείχνει
  πώς να προσθέσετε Bates, να προσθέσετε διαδοχικούς αριθμούς σελίδων και να δημιουργήσετε
  Bates γρήγορα.
og_title: Δημιουργία εγγράφου PDF C# – Προσθήκη αρίθμησης Bates
tags:
- C#
- PDF
- Bates numbering
title: Δημιουργία εγγράφου PDF C# – Προσθήκη αρίθμησης Bates
url: /el/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Εγγράφου PDF C# – Προσθήκη Αρίθμησης Bates

Έχετε χρειαστεί ποτέ να **create PDF document C#** και στη συνέχεια να επισημάνετε κάθε σελίδα με ένα μοναδικό αναγνωριστικό για νομικούς ή αρχειοθετητικούς σκοπούς; Δεν είστε οι μόνοι—γραφεία δικηγόρων, δικαστήρια και ακόμη και μεγάλες εταιρείες ρωτούν συνεχώς: «Πώς μπορώ να προσθέσω αριθμούς Bates στα PDF μου αυτόματα;» Το καλό νέο είναι ότι με λίγες γραμμές κώδικα μπορείτε να δημιουργήσετε ένα PDF, να διασκορπίσετε αριθμούς Bates σε κάθε σελίδα και να αποθηκεύσετε το αποτέλεσμα χωρίς ποτέ να ανοίξετε έναν επεξεργαστή.

Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό, ολοκληρωμένο παράδειγμα που δείχνει **πώς να προσθέσετε Bates**, πώς να **προσθέσετε διαδοχικούς αριθμούς σελίδων**, και ακόμη πώς να **δημιουργήσετε Bates** με προσαρμοσμένα προθέματα. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

## Τι Θα Χρειαστείτε

- **.NET 6+** (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+)
- **Aspose.Pdf for .NET** – εμπορική βιβλιοθήκη που προσφέρει καθαρό API για επεξεργασία PDF. Μια δωρεάν αξιολόγηση λειτουργεί καλά για δοκιμές.
- Βασική κατανόηση της C# (πιθανότατα είστε ήδη εξοικειωμένοι με δηλώσεις `using` και αντικείμενα).

Δεν απαιτούνται επιπλέον πακέτα NuGet εκτός από το `Aspose.Pdf`. Αν δεν το έχετε εγκαταστήσει ακόμη, εκτελέστε:

```bash
dotnet add package Aspose.Pdf
```

> **Pro tip:** Κρατήστε την έκδοση του Aspose ενημερωμένη· η τελευταία έκδοση 23.x προσθέτει βελτιώσεις απόδοσης για μεγάλα έγγραφα.

## Step 1: Open (or Create) the Source PDF Document

Πρώτα χρειαζόμαστε ένα PDF για να εργαστούμε. Σε πολλές πραγματικές περιπτώσεις έχετε ήδη ένα αρχείο εισόδου—π.χ. ένα σαρωμένο συμβόλαιο. Για το παράδειγμα, θα ανοίξουμε ένα υπάρχον αρχείο με όνομα `input.pdf`.

```csharp
using Aspose.Pdf;

// Step 1 – Load the PDF you want to number
var pdfPath = @"C:\Docs\input.pdf";
using var pdfDocument = new Document(pdfPath);
```

> **Why this matters:** Το άνοιγμα του εγγράφου μέσα σε μπλοκ `using` εγγυάται ότι το χειριστήριο του αρχείου απελευθερώνεται άμεσα, αποφεύγοντας προβλήματα κλειδώματος αρχείου όταν αργότερα προσπαθήσετε να αντικαταστήσετε το ίδιο αρχείο.

## Step 2: Define Your Bates Numbering Options

Οι αριθμοί Bates αποτελούνται από ένα **prefix** (συχνά αναγνωριστικό υπόθεσης) και έναν **starting number**. Μπορείτε επίσης να ελέγξετε τον αριθμό των ψηφίων, τη θέση στη σελίδα και το στυλ γραμματοσειράς. Εδώ θα χρησιμοποιήσουμε τη δευτερεύουσα λέξη-κλειδί **add bates numbering pdf** διαμορφώνοντας ένα αντικείμενο `BatesNumberingOptions`.

```csharp
// Step 2 – Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    // Primary keyword in action: create pdf document c# with custom settings
    Prefix = "CASE-",
    Start = 1000,
    // Optional: set zero‑padding to 6 digits (e.g., CASE-001000)
    NumberOfDigits = 6,
    // Optional: define where the number appears (bottom‑right corner)
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Optional: choose a readable font
    Font = FontRepository.FindFont("Arial")
};
```

> **How to add bates:** Με την τροποποίηση των `Prefix` και `Start` ελέγχετε το ακριβές κείμενο που θα εμφανίζεται σε κάθε σελίδα. Η ιδιότητα `NumberOfDigits` εξασφαλίζει σταθερό πλάτος, κάτι χρήσιμο για νομικές υποβολές.

## Step 3: Apply Bates Numbering to Every Page

Τώρα έρχεται η κύρια λειτουργία—η προσθήκη των αριθμών. Η μέθοδος `AddBatesNumbering` διασχίζει κάθε σελίδα, σχεδιάζει το κείμενο και σέβεται τις επιλογές που ορίσαμε.

```csharp
// Step 3 – Apply Bates numbering to all pages
pdfDocument.AddBatesNumbering(batesOptions);
```

Στο παρασκήνιο το Aspose αποδίδει το κείμενο ως στοιχείο *content*, πράγμα που σημαίνει ότι οι αριθμοί γίνονται μέρος του PDF και δεν μπορούν να απενεργοποιηθούν σε έναν προβολέα. Αυτό είναι ακριβώς ό,τι χρειάζεστε όταν θέλετε **add sequential page numbers** που είναι αμετάβλητοι.

### Edge Cases & Variations

- **Multiple prefixes:** Αν χρειάζεστε διαφορετικά προθέματα ανά ενότητα, δημιουργήστε ξεχωριστά `BatesNumberingOptions` και καλέστε `AddBatesNumbering` σε ένα εύρος σελίδων (`pdfDocument.Pages[1..5]`).
- **Zero‑padding control:** Παραλείψτε το `NumberOfDigits` για αριθμό μεταβλητού μήκους, ή ορίστε το σε υψηλότερη τιμή για να προσθέσετε μηδενικά στην αρχή.
- **Custom positioning:** Χρησιμοποιήστε το `Margin` για να μετατοπίσετε τον αριθμό από το άκρο, ή αλλάξτε το `HorizontalAlignment` σε `Center` για στυλ υποσέλιδου.

## Step 4: Save the Modified PDF

Τέλος, γράψτε το ενημερωμένο έγγραφο στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό ή να δημιουργήσετε ένα ολοκαίνουργιο αρχείο.

```csharp
// Step 4 – Save the PDF with Bates numbers applied
var outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
```

Μετά την εκτέλεση αυτής της γραμμής, το `output.pdf` περιέχει το αρχικό περιεχόμενο συν έναν ορατό ετικέτα Bates σε κάθε σελίδα—ακριβώς αυτό που θα περιμένατε όταν **how to generate bates** για ένα αρχείο υπόθεσης.

## Full, Runnable Example

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες snippet που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε μια εφαρμογή κονσόλας:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Open the source PDF
        var inputFile = @"C:\Docs\input.pdf";
        using var pdf = new Document(inputFile);

        // 2️⃣ Configure Bates numbering (add bates numbering pdf)
        var options = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 1000,
            NumberOfDigits = 6,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = FontRepository.FindFont("Arial")
        };

        // 3️⃣ Apply the numbering (how to add bates)
        pdf.AddBatesNumbering(options);

        // 4️⃣ Save the result (add sequential page numbers)
        var outputFile = @"C:\Docs\output.pdf";
        pdf.Save(outputFile);

        Console.WriteLine("Bates numbering applied successfully!");
    }
}
```

### Expected Result

Ανοίξτε το `output.pdf` σε οποιονδήποτε προβολέα (Adobe Reader, Edge κ.λπ.). Θα δείτε κάθε σελίδα σφραγισμένη με κάτι όπως **CASE-001000**, **CASE-001001**, … μέχρι την τελευταία σελίδα. Οι αριθμοί τοποθετούνται κομψά στο κάτω‑δεξιό μέρος, σύμφωνα με τις επιλογές που ορίσαμε.

## Common Questions & Troubleshooting

- **«Τι γίνεται αν το PDF μου είναι προστατευμένο με κωδικό;»**  
  Φορτώστε το με τον κωδικό: `new Document(inputFile, new LoadOptions { Password = "secret" })`.

- **«Μπορώ να προσθέσω αριθμούς Bates σε ένα νεοδημιουργημένο PDF;»**  
  Σίγουρα. Απλώς δημιουργήστε πρώτα το έγγραφο (`var doc = new Document();`) και μετά ακολουθήστε τα Βήματα 2‑4 πριν το αποθηκεύσετε.

- **«Ενσωματώνεται πάντα η γραμματοσειρά;»**  
  Το Aspose ενσωματώνει αυτόματα τη γραμματοσειρά αν δεν υπάρχει ήδη στο PDF. Αν χρειάζεστε συγκεκριμένη οικογένεια γραμματοσειρών, ορίστε `options.Font` αναλόγως.

- **«Τι γίνεται με την απόδοση σε αρχεία 10.000 σελίδων;»**  
  Η βιβλιοθήκη κάνει streaming των σελίδων, έτσι η χρήση μνήμης παραμένει μέτρια. Ωστόσο, ίσως θελήσετε να αυξήσετε το `PdfSaveOptions.CompressionMode` για ταχύτερο I/O.

## Pro Tips for Production Use

1. **Batch processing:** Τυλίξτε τη λογική σε έναν βρόχο που διατρέχει έναν φάκελο PDF. Χρησιμοποιήστε `Directory.GetFiles("*.pdf")` και επεξεργαστείτε κάθε αρχείο ξεχωριστά.
2. **Logging:** Καταγράψτε τους πρώτους και τελευταίους αριθμούς Bates σε αρχείο καταγραφής—βοηθά τους ελεγκτές να επαληθεύσουν ότι η αρίθμηση ήταν συνεχής.
3. **Error handling:** Περιβάλλετε ολόκληρο το τμήμα σε `try/catch` και εμφανίστε σαφές μήνυμα αν το πηγαίο PDF λείπει ή είναι κατεστραμμένο.
4. **Zero‑padding flexibility:** Αν χρειάζεστε δυναμικό αριθμό ψηφίων βάσει του συνολικού αριθμού σελίδων, υπολογίστε `NumberOfDigits = (pdf.Pages.Count + options.Start).ToString().Length`.

## Conclusion

Μόλις δείξαμε πώς να **create PDF document C#** και αβίαστα **add Bates numbering**—καλύπτοντας τα πάντα από τη φόρτωση μέχρι την αποθήκευση. Το σύντομο παράδειγμα επιδεικνύει **how to add bates**, **add sequential page numbers**, και **how to generate bates** με προσαρμοσμένα προθέματα και μηδενική συμπλήρωση. Με λίγες προσαρμογές μπορείτε να εφαρμόσετε αυτό το μοτίβο σε παρτίδες εργασιών, διαφορετικές διατάξεις ή ακόμη και να το ενσωματώσετε σε ένα web API που επιστρέφει ένα φρέσκο‑αριθμημένο PDF κατόπιν αιτήματος.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να το συνδυάσετε με τη λειτουργία **watermark** του Aspose, ή δημιουργήστε ένα ευρετήριο σύνοψης που καταγράφει κάθε αριθμό Bates μαζί με μια σύντομη περιγραφή του περιεχομένου της σελίδας. Οι δυνατότητες είναι απεριόριστες, και ο κώδικας που έχετε τώρα αποτελεί ισχυρό θεμέλιο για οποιοδήποτε workflow αυτοματοποίησης εγγράφων.

Καλή προγραμματιστική, και ας είναι τα PDF σας πάντα τέλεια αριθμημένα! 

![Screenshot of a PDF viewer showing create pdf document c# with Bates numbers applied](image-placeholder.png "create pdf document c# with Bates numbers")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}