---
category: general
date: 2026-05-27
description: Προσθέστε αρίθμηση Bates σε PDF χρησιμοποιώντας το Aspose.Pdf σε C#.
  Μάθετε πώς να προσθέτετε αρίθμηση Bates γρήγορα, να προσαρμόζετε τη μορφή και να
  αυτοματοποιείτε την ετικετοποίηση νομικών εγγράφων.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbering
language: el
og_description: Προσθήκη αρίθμησης Bates σε PDF με το Aspose.Pdf σε C#. Αυτός ο οδηγός
  δείχνει πώς να προσθέσετε αρίθμηση Bates, να διαμορφώσετε προθέματα και να αποθηκεύσετε
  το αποτέλεσμα.
og_title: Προσθήκη αρίθμησης Bates σε PDF με C# – Βήμα‑βήμα οδηγός
schemas:
- author: Aspose
  dateModified: '2026-05-27'
  description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  headline: Add Bates Numbering PDF in C# – Complete Guide
  type: TechArticle
- description: Add Bates numbering PDF using Aspose.Pdf in C#. Learn how to add Bates
    numbering quickly, customize format, and automate legal document tagging.
  name: Add Bates Numbering PDF in C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you run the program, the console prints:'
  - name: Can I position the Bates number elsewhere?
    text: Yes. Use the `BatesNumberingArtifact`’s `Location` property (e.g., `Location
      = new Position(10, 10)`) to place the number at custom X/Y coordinates. You
      can also set `HorizontalAlignment` and `VerticalAlignment` for more control.
  - name: What if my PDF has thousands of pages?
    text: Aspose.Pdf streams pages efficiently, but it’s still a good idea to process
      in batches if you hit memory limits. The `Document` class also supports `PdfConverter`
      for incremental saving.
  - name: How do I change the font or color?
    text: 'Wrap the artifact in a `TextState` object:'
  - name: Do I need a license for production use?
    text: A licensed version removes evaluation watermarks and unlocks full performance.
      The free trial works fine for testing and proof‑of‑concepts.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- Bates numbering
- PDF automation
title: Προσθήκη Bates Numbering σε PDF με C# – Πλήρης Οδηγός
url: /el/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Αρίθμησης Bates σε PDF με C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να προσθέσετε αρίθμηση Bates** σε ένα PDF χωρίς να ξοδεύετε ώρες παίζοντας με χειροκίνητα εργαλεία; Δεν είστε μόνοι—νομικές ομάδες, ελεγκτές και ειδικοί e‑discovery χρειάζονται όλοι έναν αξιόπιστο τρόπο για **να προσθέτουν αρίθμηση Bates σε PDF** αρχεία προγραμματιστικά.  

Σε αυτό το σεμινάριο θα περάσουμε βήμα-βήμα μια σύντομη, ολοκληρωμένη λύση χρησιμοποιώντας το Aspose.Pdf για .NET, ώστε να μπορείτε να προσθέτετε αριθμούς Bates σε οποιοδήποτε έγγραφο με μόνο λίγες γραμμές κώδικα C#.

## Τι Θα Μάθετε

- Πώς να ανοίξετε ένα υπάρχον PDF με Aspose.Pdf  
- Πώς να δημιουργήσετε ένα αντικείμενο αρίθμησης Bates και να ρυθμίσετε τη μορφή του  
- Πώς να συνδέσετε το αντικείμενο σε κάθε σελίδα (ή μόνο στην πρώτη)  
- Πώς να αποθηκεύσετε το ενημερωμένο αρχείο και να επαληθεύσετε το αποτέλεσμα  

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose—απλώς μια βασική κατανόηση του C# και του .NET. Στο τέλος, θα έχετε ένα επαναχρησιμοποιήσιμο απόσπασμα κώδικα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε οποιοδήποτε έργο.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+)  
- Πακέτο NuGet Aspose.Pdf για .NET (`Install-Package Aspose.Pdf`)  
- Ένα αρχείο PDF προέλευσης που θέλετε να επισημάνετε (τοποθετήστε το σε φάκελο που μπορείτε να αναφέρετε)

> **Συμβουλή:** Αν δεν έχετε ακόμη άδεια, η Aspose προσφέρει ένα δωρεάν προσωρινό κλειδί που αφαιρεί τα υδατογράμματα αξιολόγησης.

## Βήμα 1 – Άνοιγμα του Πηγαίου PDF Εγγράφου  

Πρώτα χρειάζεται ένα αντικείμενο `Document` που αντιπροσωπεύει το αρχείο στο δίσκο. Σκεφτείτε το ως φόρτωση ενός κεννού καμβά που θα ζωγραφίσουμε αργότερα τους αριθμούς Bates.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Adjust the path to point at your source PDF
        string sourcePath = @"C:\Docs\source.pdf";

        // Load the PDF – this is where we start to add Bates numbering
        using (var pdfDocument = new Document(sourcePath))
        {
            // The rest of the logic lives inside this using block
        }
    }
}
```

**Γιατί είναι σημαντικό:** Το άνοιγμα του εγγράφου μέσα σε ένα μπλοκ `using` εξασφαλίζει ότι όλοι οι μη διαχειριζόμενοι πόροι απελευθερώνονται άμεσα, κάτι που είναι ιδιαίτερα σημαντικό για μεγάλα PDF.

## Βήμα 2 – Δημιουργία Αντικειμένου Αρίθμησης Bates  

Ένα *BatesNumberingArtifact* είναι ο τρόπος του Aspose να περιγράψει πώς πρέπει να εμφανίζονται οι αριθμοί. Μπορείτε να ορίσετε πρόθεμα, αρχικό αριθμό, βήμα αύξησης και ακόμη μια προσαρμοσμένη συμβολοσειρά μορφής.

```csharp
// Step 2: Define the Bates numbering artifact
var batesNumbering = new BatesNumberingArtifact
{
    Prefix = "ABC",            // Text that appears before each number
    StartNumber = 1000,        // First number in the sequence
    Increment = 1,             // Step between consecutive numbers
    Format = "{0:D5}"          // Zero‑padded 5‑digit number (e.g., 01000)
};
```

**Γιατί μπορεί να θέλετε να αλλάξετε αυτές τις τιμές:**  
- **Prefix** είναι χρήσιμο για αναγνωριστικά υποθέσεων (“CASE‑”, “DOC‑”).  
- **StartNumber** σας επιτρέπει να συνεχίσετε μια προηγούμενη σειρά.  
- **Increment** μπορεί να οριστεί σε 2 αν χρειάζεστε αριθμική αρίθμηση μονών/ζυγών.  
- **Format** υποστηρίζει οποιαδήποτε σύνθετη μορφή .NET· `{0:D5}` εγγυάται πέντε ψηφία με μηδενικά στην αρχή.

## Βήμα 3 – Σύνδεση του Αντικειμένου στις Επιθυμητές Σελίδες  

Μπορείτε να προσθέσετε το αντικείμενο σε μία σελίδα, σε ένα εύρος ή σε ολόκληρο το έγγραφο. Για τις περισσότερες νομικές ροές εργασίας το συνδέουμε σε *κάθε* σελίδα, αλλά το παρακάτω παράδειγμα δείχνει την ελάχιστη περίπτωση—προσθήκη στην πρώτη σελίδα.

```csharp
// Step 3: Attach the artifact to the first page (index is 1‑based)
pdfDocument.Pages[1].Artifacts.Add(batesNumbering);
```

Αν χρειάζεται να καλύψετε όλες τις σελίδες, κάντε βρόχο πάνω τους:

```csharp
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesNumbering);
}
```

**Γιατί αυτό το βήμα είναι κρίσιμο:** Τα αντικείμενα αποδίδονται *μετά* το περιεχόμενο της σελίδας, έτσι οι αριθμοί εμφανίζονται πάνω από το υπάρχον κείμενο χωρίς να αλλάζουν την αρχική διάταξη.

## Βήμα 4 – Αποθήκευση του Τροποποιημένου PDF  

Τέλος, γράψτε τις αλλαγές πίσω στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό ή να δημιουργήσετε νέο αρχείο—εδώ θα δημιουργήσουμε ένα νέο αντίγραφο με όνομα `bates.pdf`.

```csharp
// Step 4: Persist the changes
string outputPath = @"C:\Docs\bates.pdf";
pdfDocument.Save(outputPath);

Console.WriteLine($"Bates numbering added successfully. File saved to: {outputPath}");
```

Όταν ανοίξετε το `bates.pdf` θα δείτε το «ABC01000» (ή όποια μορφή επιλέξατε) να είναι σφραγισμένο στην προεπιλεγμένη θέση—συνήθως στην κάτω‑δεξιά γωνία.

## Πλήρες Παράδειγμα Λειτουργίας  

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε:

```csharp
using Aspose.Pdf;
using System;

class AddBatesNumbering
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Open the source PDF
        // -----------------------------------------------------------------
        string sourcePath = @"C:\Docs\source.pdf";
        using (var pdfDocument = new Document(sourcePath))
        {
            // -----------------------------------------------------------------
            // 2️⃣ Create and configure the Bates numbering artifact
            // -----------------------------------------------------------------
            var batesNumbering = new BatesNumberingArtifact
            {
                Prefix = "ABC",
                StartNumber = 1000,
                Increment = 1,
                Format = "{0:D5}"
            };

            // -----------------------------------------------------------------
            // 3️⃣ Attach the artifact to each page (or a specific page)
            // -----------------------------------------------------------------
            foreach (Page page in pdfDocument.Pages)
            {
                page.Artifacts.Add(batesNumbering);
            }

            // -----------------------------------------------------------------
            // 4️⃣ Save the new PDF
            // -----------------------------------------------------------------
            string outputPath = @"C:\Docs\bates.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Bates numbers added. Output: {outputPath}");
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Όταν εκτελέσετε το πρόγραμμα, η κονσόλα εμφανίζει:

```
Bates numbers added. Output: C:\Docs\bates.pdf
```

Ανοίγοντας το `bates.pdf` εμφανίζεται το πρόθεμα «ABC» ακολουθούμενο από μια ακολουθία πέντε ψηφίων με μηδενικά στην αρχή σε κάθε σελίδα—ακριβώς αυτό που ζήτησε ο κώδικας.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Μπορώ να τοποθετήσω τον αριθμό Bates αλλού;

Ναι. Χρησιμοποιήστε την ιδιότητα `Location` του `BatesNumberingArtifact` (π.χ., `Location = new Position(10, 10)`) για να τοποθετήσετε τον αριθμό σε προσαρμοσμένες συντεταγμένες X/Y. Μπορείτε επίσης να ορίσετε `HorizontalAlignment` και `VerticalAlignment` για μεγαλύτερο έλεγχο.

### Τι γίνεται αν το PDF μου έχει χιλιάδες σελίδες;

Το Aspose.Pdf διαχειρίζεται τις σελίδες αποδοτικά, αλλά είναι καλό να επεξεργάζεστε σε παρτίδες αν φτάσετε τα όρια μνήμης. Η κλάση `Document` υποστηρίζει επίσης το `PdfConverter` για σταδιακή αποθήκευση.

### Πώς αλλάζω τη γραμματοσειρά ή το χρώμα;

Τυλίξτε το αντικείμενο σε ένα αντικείμενο `TextState`:

```csharp
batesNumbering.TextState = new TextState
{
    FontSize = 12,
    Font = FontRepository.FindFont("Arial"),
    ForegroundColor = Color.FromRgb(255, 0, 0) // red
};
```

### Χρειάζομαι άδεια για παραγωγική χρήση;

Μια έκδοση με άδεια αφαιρεί τα υδατογράμματα αξιολόγησης και ξεκλειδώνει πλήρη απόδοση. Η δωρεάν δοκιμή λειτουργεί καλά για δοκιμές και αποδείξεις‑έννοιας.

## Επαλήθευση – Γρήγορος Οπτικός Έλεγχος  

Αν προτιμάτε αυτοματοποιημένη επαλήθευση, το Aspose μπορεί να εξάγει το κείμενο μιας σελίδας και να επιβεβαιώσει την παρουσία του προθέματος:

```csharp
string pageText = pdfDocument.Pages[1].ExtractText();
bool hasBates = pageText.Contains("ABC01000");
Console.WriteLine(hasBates ? "Bates number verified." : "Number missing!");
```

Η εκτέλεση αυτού μετά το βήμα αποθήκευσης θα εκτυπώσει `Bates number verified.` εάν όλα πήγαν ομαλά.

## Συμπέρασμα  

Τώρα ξέρετε **πώς να προσθέτετε αρίθμηση Bates σε PDF** αρχεία χρησιμοποιώντας το Aspose.Pdf σε C#. Από το άνοιγμα του εγγράφου μέχρι τη διαμόρφωση του αντικειμένου, τη σύνδεσή του στις σελίδες και την αποθήκευση του αποτελέσματος, η διαδικασία είναι απλή και πλήρως αυτοματοποιήσιμη.  

Επόμενα βήματα; Δοκιμάστε να πειραματιστείτε με:

- Διαφορετικές τιμές `Prefix` για πολλαπλές παρτίδες υποθέσεων  
- Προσαρμοσμένο `Location` και `TextState` για branding  
- Προσθήκη προθεμάτων ειδικών για κάθε σελίδα (π.χ., “VOL‑1‑”, “VOL‑2‑”) προσαρμόζοντας το `StartNumber` σε κάθε επανάληψη του βρόχου  

Αυτές οι προσαρμογές σας επιτρέπουν να προσαρμόσετε τη λύση σε σχεδόν οποιαδήποτε νομική ή αρχειακή ροή εργασίας.  

Έχετε περισσότερες ερωτήσεις σχετικά με **πώς να προσθέτετε αρίθμηση Bates** για PDF πολλαπλών γλωσσών ή κρυπτογραφημένα αρχεία; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Σχετικά Σεμινάρια

- [Πώς να Προσθέσετε και να Προσαρμόσετε Αριθμούς Σελίδων σε PDF χρησιμοποιώντας Aspose.PDF για .NET | Οδηγός Διαχείρισης Εγγράφων](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Πώς να Προσθέσετε Διαφορετικές Κεφαλίδες σε PDF χρησιμοποιώντας Aspose.PDF για .NET: Οδηγός Βήμα‑Βήμα](/pdf/english/net/document-manipulation/add-different-headers-aspose-pdf-net/)
- [Πώς να Προσθέσετε Υποσέλιδο Σφραγίδας Κειμένου σε PDF χρησιμοποιώντας Aspose.PDF για .NET: Οδηγός Βήμα‑Βήμα](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}