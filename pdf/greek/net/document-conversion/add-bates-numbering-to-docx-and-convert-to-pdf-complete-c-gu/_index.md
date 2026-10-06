---
category: general
date: 2026-02-20
description: Προσθέστε αριθμολόγηση Bates στα έγγραφά σας και μετατρέψτε DOCX σε PDF
  με προσαρμοσμένους αριθμούς σελίδων σε C#. Μάθετε πώς να προσθέτετε διαδοχικούς
  αριθμούς σελίδων και να αποθηκεύετε το έγγραφο ως PDF.
draft: false
keywords:
- add bates numbering
- convert docx to pdf
- add custom page numbers
- save document as pdf
- add sequential page numbers
language: el
og_description: Προσθέστε αριθμολόγηση Bates στα αρχεία DOCX σας και μετατρέψτε τα
  σε PDF με προσαρμοσμένους αριθμούς σελίδων χρησιμοποιώντας C#. Αυτός ο οδηγός σας
  καθοδηγεί βήμα προς βήμα.
og_title: Προσθήκη αρίθμησης Bates σε DOCX και μετατροπή σε PDF – Οδηγός C#
tags:
- C#
- PDF
- Document Automation
title: Προσθήκη αρίθμησης Bates σε DOCX και μετατροπή σε PDF – Πλήρης οδηγός C#
url: /el/net/document-conversion/add-bates-numbering-to-docx-and-convert-to-pdf-complete-c-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Bates Numbering σε DOCX και Μετατροπή σε PDF – Πλήρης Οδηγός C#

Έχετε ποτέ χρειαστεί να **προσθέσετε bates numbering** σε ένα νομικό σημείωμα αλλά δεν ήσασταν σίγουροι πώς να το αυτοματοποιήσετε; Δεν είστε οι μόνοι. Σε πολλές εταιρείες η χειροκίνητη διαδικασία σφράγισης κάθε σελίδας είναι πραγματική σπατάλη χρόνου, και ο κίνδυνος να λείπει ένας αριθμός μπορεί να είναι δαπανηρός.  

Τα καλά νέα; Με λίγες γραμμές C# μπορείτε να **προσθέσετε bates numbering**, **μετατρέψετε docx σε pdf**, και **αποθηκεύσετε το έγγραφο ως pdf** σε μια ομαλή ροή. Παρακάτω θα βρείτε μια αυτόνομη λύση που λειτουργεί σήμερα, μαζί με το “γιατί” πίσω από κάθε επιλογή ώστε να την προσαρμόσετε στη δική σας ροή εργασίας.

---

## Τι Καλύπτει Αυτό το Σεμινάριο

1. Φορτώστε ένα αρχείο DOCX από το δίσκο.  
2. Ορίστε **προσαρμοσμένους αριθμούς σελίδας** (πρόθεμα, αρχική τιμή και προαιρετική μορφοποίηση).  
3. Εφαρμόστε **add bates numbering** σε κάθε σελίδα του πηγαίου αρχείου.  
4. **Μετατρέψτε docx σε pdf** διατηρώντας την αρίθμηση.  
5. **Αποθηκεύστε το έγγραφο ως pdf** σε μια τοποθεσία της επιλογής σας.  

Χωρίς εξωτερικές υπηρεσίες, χωρίς κρυφές ρυθμίσεις—μόνο απλό C# και μια δημοφιλής βιβλιοθήκη επεξεργασίας εγγράφων (π.χ., GroupDocs.Conversion). Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή κονσόλας που παράγει ένα PDF με διαδοχικούς αριθμούς σελίδας ακριβώς όπου τους χρειάζεστε.

## Προαπαιτούμενα

- **.NET 6.0** ή νεότερο (ο κώδικας μεταγλωττίζεται επίσης σε .NET Framework 4.7+).  
- Το πακέτο NuGet **GroupDocs.Conversion** (ή οποιαδήποτε βιβλιοθήκη που εκθέτει `Document`, `BatesNumberingOptions` και `Pages.AddBatesNumbering`). Εγκαταστήστε το με:  

```bash
dotnet add package GroupDocs.Conversion
```

- Ένα αρχείο DOCX που θέλετε να επεξεργαστείτε (τοποθετήστε το στο `YOUR_DIRECTORY/input.docx`).  
- Βασική εξοικείωση με έργα κονσόλας C#.

## Υλοποίηση Βήμα‑βήμα

### ## Προσθήκη Bates Numbering – Προετοιμασία του Έργου

Πρώτα, δημιουργήστε ένα νέο έργο κονσόλας και εισάγετε τα απαιτούμενα namespaces:

```csharp
using System;
using GroupDocs.Conversion;               // Core document handling
using GroupDocs.Conversion.Options;       // Options like BatesNumberingOptions
using GroupDocs.Conversion.Options.Pdf;   // PDF‑specific options (if needed)

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill the body in the next steps
        }
    }
}
```

> **Γιατί είναι σημαντικό:** Η εισαγωγή των σωστών namespaces σας δίνει πρόσβαση στην κλάση `Document` (το σημείο εισόδου) και στο αντικείμενο **BatesNumberingOptions** που ελέγχει τη μορφή της αρίθμησης. Η παράλειψη αυτού του βήματος προκαλεί σφάλμα μεταγλώττισης, γι' αυτό ξεκινάμε εδώ.

### ## Φόρτωση του Πηγαίου Αρχείου DOCX

Τώρα διαβάζουμε το αρχείο Word. Ο κατασκευαστής `Document` δέχεται μια διαδρομή, οπότε κρατήστε τις διαδρομές σας απόλυτες ή σχετικές με το εκτελέσιμο.

```csharp
// Step 1: Load the source document
string inputPath = @"YOUR_DIRECTORY/input.docx";
Document document = new Document(inputPath);
```

> **Συμβουλή:** Αν το αρχείο μπορεί να λείπει, τυλίξτε το σε `try/catch` και εμφανίστε ένα φιλικό μήνυμα. Αποτρέπει την κατάρρευση ολόκληρης της εφαρμογής και βελτιώνει την εμπειρία του χρήστη.

### ## Ορισμός Προσαρμοσμένων Αριθμών Σελίδας (Bates Options)

Εδώ ορίζουμε **add custom page numbers**. Μπορείτε να αλλάξετε το `Prefix`, το `Start` και ακόμη και τη μορφή του αριθμού (π.χ., μηδενικά στην αρχή).

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC",      // Anything you need – legal firms love prefixes
    Start = 1000,        // First number in the sequence
    // Optional: NumberFormat = "0000" // forces four‑digit padding
};
```

> **Γιατί χρειάζεστε πρόθεμα:** Σε πολλές δικαιοδοσίες το πρόθεμα προσδιορίζει το αρχείο της υπόθεσης ή τον πελάτη. Η βιβλιοθήκη θα το προσθέσει αυτόματα σε κάθε αριθμό σελίδας.

### ## Εφαρμογή Bates Numbering σε Κάθε Σελίδα

Με τις επιλογές έτοιμες, λέμε στο έγγραφο να σφραγίσει κάθε σελίδα:

```csharp
// Step 3: Apply Bates numbering to every page in the document
document.Pages.AddBatesNumbering(batesOptions);
```

> **Ακραία περίπτωση:** Αν το DOCX σας περιέχει ήδη υποσέλιδα, η βιβλιοθήκη θα επικάλυψει τους αριθμούς εξ ορισμού. Ορισμένες βιβλιοθήκες σας επιτρέπουν να καθορίσετε τη θέση (πάνω‑δεξιά, κάτω‑κέντρο κ.λπ.) μέσω πρόσθετων ιδιοτήτων στο `BatesNumberingOptions`.

### ## Μετατροπή σε PDF και Αποθήκευση

Τέλος, εξάγουμε ένα PDF που περιέχει τους νεοπροστέθηκαν αριθμούς. Η μέθοδος `Save` ανιχνεύει αυτόματα τη μορφή από την επέκταση του αρχείου.

```csharp
// Step 4: Save the document with the new Bates numbers as PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";
document.Save(outputPath);
Console.WriteLine($"✅ PDF saved with Bates numbering at: {outputPath}");
```

> **Γιατί αποθηκεύουμε ως PDF:** Τα PDF διατηρούν τη διάταξη, τις γραμματοσειρές και την ακριβή θέση των αριθμών, καθιστώντας τα ιδανικά για νομικές υποβολές και αρχειοθέτηση.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `Program.cs` και να εκτελέσετε:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source DOCX
            string inputPath = @"YOUR_DIRECTORY/input.docx";
            Document document = new Document(inputPath);

            // 2️⃣ Set up Bates numbering (custom prefix & start)
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC",
                Start = 1000
                // NumberFormat = "0000" // Uncomment for zero‑padded numbers
            };

            // 3️⃣ Apply the numbering to every page
            document.Pages.AddBatesNumbering(batesOptions);

            // 4️⃣ Convert and save as PDF
            string outputPath = @"YOUR_DIRECTORY/output.pdf";
            document.Save(outputPath);

            Console.WriteLine($"✅ Done! PDF with Bates numbers saved to {outputPath}");
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Ανοίξτε το `output.pdf` σε οποιονδήποτε προβολέα. Θα δείτε κάθε σελίδα αριθμημένη όπως **ABC‑1000**, **ABC‑1001**, … συνεχίζοντας μέχρι την τελευταία σελίδα. Οι αριθμοί εμφανίζονται στην προεπιλεγμένη θέση (κάτω‑δεξιά) εκτός αν έχετε αλλάξει τις επιλογές.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| **Μπορώ να αλλάξω τη θέση των αριθμών;** | Ναι. Οι περισσότερες βιβλιοθήκες εκθέτουν τις ιδιότητες `Position` ή `Margin` στο `BatesNumberingOptions`. Ορίστε `batesOptions.Position = BatesNumberingPosition.BottomLeft;` για διαφορετική γωνία. |
| **Τι γίνεται αν το DOCX έχει υπάρχοντα υποσέλιδα;** | Η βιβλιοθήκη συνήθως αντικαθιστά την περιοχή όπου σχεδιάζει τον αριθμό. Αν χρειάζεται να διατηρήσετε τα υπάρχοντα υποσέλιδα, ψάξτε για μια σημαία `OverwriteExisting` ή προσθέστε τους αριθμούς χειροκίνητα μέσω ενός προσαρμοσμένου προτύπου υποσέλιδου. |
| **Πρέπει να ανησυχήσω για χαρακτήρες Unicode;** | Το πρόθεμα μπορεί να περιέχει οποιοδήποτε κείμενο Unicode, αλλά βεβαιωθείτε ότι η γραμματοσειρά που χρησιμοποιείται στο PDF υποστηρίζει αυτούς τους χαρακτήρες· διαφορετικά θα εμφανιστούν ως τετράγωνα. |
| **Πώς προσθέτω μηδενικά στην αρχή;** | Ορίστε `NumberFormat = "0000"` (ή οποιοδήποτε μοτίβο) στο `BatesNumberingOptions`. Αυτό εξαναγκάζει αριθμούς όπως 0010, 0011 κ.λπ. |
| **Μπορώ να επεξεργαστώ μαζικά πολλά αρχεία DOCX;** | Απολύτως. Τυλίξτε τη λογική σε έναν βρόχο `foreach (var file in Directory.GetFiles(..., "*.docx"))` και επαναχρησιμοποιήστε το ίδιο αντικείμενο `batesOptions` ή διαφοροποιήστε το ανά αρχείο. |

## Επαγγελματικές Συμβουλές & Καλές Πρακτικές

- **Performance:** Αν επεξεργάζεστε εκατοντάδες αρχεία, επαναχρησιμοποιήστε μια μόνο παρουσία `Document` όπου είναι δυνατόν και καλέστε `document.Dispose()` μετά από κάθε αποθήκευση για να ελευθερώσετε μη διαχειριζόμενους πόρους.  
- **Version control:** Κρατήστε τις τιμές `Prefix` και `Start` σε αρχείο ρυθμίσεων (`appsettings.json`). Έτσι μπορείτε να τις αλλάξετε χωρίς επαναμεταγλώττιση.  
- **Testing:** Εκτελέστε το πρόγραμμα πρώτα σε ένα DOCX μιας σελίδας. Επαληθεύστε ότι ο αριθμός εμφανίζεται όπου περιμένετε πριν το κλιμακώσετε σε τεράστιες συμβάσεις.  
- **Compliance:** Ορισμένες δικαιοδοσίες απαιτούν ο Bates number να είναι τουλάχιστον 8 χαρακτήρες. Προσαρμόστε το `Prefix` και το `NumberFormat` αναλόγως.  

## Επόμενα Βήματα – Επέκταση της Αυτοματοποίησής Σας

Τώρα που έχετε κατακτήσει το **add bates numbering**, σκεφτείτε αυτές τις σχετικές βελτιώσεις:

- **Convert docx to pdf** διατηρώντας τους υπερσυνδέσμους και τους σελιδοδείκτες.  
- **Add custom page numbers** σε υπάρχοντα PDF χρησιμοποιώντας μια βιβλιοθήκη ειδική για PDF (π.χ., iTextSharp).  
- **Save document as pdf** με διαφορετικές ρυθμίσεις ποιότητας για web vs. εκτύπωση.  
- **Add sequential page numbers** σε σαρωμένες εικόνες μέσω OCR‑επεξεργασίας κάθε σελίδας πρώτα.  

Κάθε ένα από αυτά τα θέματα βασίζεται στις ίδιες βασικές έννοιες—φόρτωση εγγράφου, διαμόρφωση επιλογών και αποθήκευση του αποτελέσματος—οπότε θα νιώσετε άνετα.

## Συμπέρασμα

Διασχίσαμε μια πλήρη, ολοκληρωμένη λύση για **add bates numbering** σε αρχείο DOCX, **convert docx to pdf**, και **save document as pdf** με προσαρμοσμένους, διαδοχικούς αριθμούς σελίδας. Ο κώδικας είναι σύντομος, οι εξαρτήσεις ελάχιστες, και η προσέγγιση αρκετά ευέλικτη για μικρά έργα δικηγορικών γραφείων και μεγάλης κλίμακας εταιρικές γραμμές παραγωγής.

Δοκιμάστε το, προσαρμόστε το πρόθεμα, πειραματιστείτε με μορφές αριθμών, και θα έχετε ένα ισχυρό εργαλείο στο κουτί εργαλείων σας. Αν αντιμετωπίσετε ιδιομορφίες ή έχετε ιδέες για περαιτέρω αυτοματοποίηση, αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}