---
category: general
date: 2026-07-03
description: Μάθημα αρίθμησης Bates που δείχνει πώς να προσθέσετε αρίθμηση Bates σε
  αρχεία PDF χρησιμοποιώντας το Aspose.PDF. Περιλαμβάνει ρύθμιση προθέματος αριθμού
  Bates και ένα πλήρες παράδειγμα αρίθμησης Bates.
draft: false
keywords:
- bates numbering tutorial
- add bates numbering pdf
- bates numbering example
- prefix bates number
language: el
og_description: Μάθημα αριθμησης Bates που σας καθοδηγεί στη προσθήκη αριθμησης Bates
  σε αρχεία PDF, στον ορισμό προθέματος αριθμού Bates και στην παροχή ενός πλήρους
  λειτουργικού παραδείγματος.
og_title: 'Οδηγός Αρίθμησης Bates: Προσθήκη Αριθμών σε PDF με το Aspose'
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Bates numbering tutorial showing how to add bates numbering pdf files
    using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
    example.
  headline: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
  type: TechArticle
- description: Bates numbering tutorial showing how to add bates numbering pdf files
    using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
    example.
  name: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
  steps:
  - name: What if I need to reset the counter for each section?
    text: You can call `pdfDocument.BatesNumbering.Reset()` before processing a new
      range of pages. Combine it with a loop over `pdfDocument.Pages` and set `Start`
      again for each section.
  - name: How do I apply different prefixes to different page ranges?
    text: 'Create multiple `BatesNumbering` objects—one per range—by cloning the document
      or by using the `Add` method (available in newer Aspose versions). Here’s a
      quick sketch:'
  - name: Does the library support Unicode prefixes?
    text: Absolutely. Pass any Unicode string (e.g., `"案件‑"`). Aspose.PDF handles
      right‑to‑left scripts and special symbols without extra configuration.
  - name: What about PDF security—will Bates numbering break encryption?
    text: If the source PDF is encrypted, you must provide the password before accessing
      `BatesNumbering`. The numbering process respects the original encryption settings—your
      output will stay encrypted unless you explicitly change it.
  type: HowTo
tags:
- Aspose.PDF
- PDF processing
- Bates numbering
title: 'Οδηγός Αρίθμησης Bates: Προσθήκη Αριθμών σε PDF με το Aspose'
url: /el/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-numbers-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μάθημα Bates Numbering – Προσθήκη αριθμών Bates σε PDF με Aspose

Κάποτε χρειάστηκε ένα **bates numbering tutorial** επειδή έπρεπε να επισημάνετε χιλιάδες σελίδες για δίκη; Δεν είστε μόνοι. Σε πολλές νομικές και συμμορφωτικές ροές εργασίας, ένας αξιόπιστος τρόπος για *add bates numbering pdf* αρχεία είναι απαραίτητος. Ευτυχώς, το Aspose.PDF κάνει όλη τη διαδικασία παιχνιδάκι, και σε αυτόν τον οδηγό θα περάσουμε από ένα πλήρες **bates numbering example** που μπορείτε να ενσωματώσετε αμέσως στο πρόγραμμά σας.

> **Τι θα πάρετε:** ένα εκτελέσιμο απόσπασμα κώδικα που ορίζει τον αριθμό εκκίνησης, εφαρμόζει ένα **prefix bates number**, και αποθηκεύει το αποτέλεσμα—όλα σε λιγότερο από 30 γραμμές C#.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 ή νεότερο (το API λειτουργεί το ίδιο και σε .NET Framework 4.6+)
- Ένα έγκυρο λ licenσ Aspose.PDF for .NET (ή μπορείτε να χρησιμοποιήσετε τη δωρεάν λειτουργία αξιολόγησης)
- Ένα αρχείο PDF με όνομα `input.pdf` τοποθετημένο σε φάκελο που ελέγχετε
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή που καταλαβαίνει έργα C#

Δεν απαιτούνται επιπλέον πακέτα NuGet πέρα από `Aspose.Pdf`.

## Βήμα 1: Εγκατάσταση Aspose.PDF for .NET

Ανοίξτε το τερματικό σας (ή το Package Manager Console) και εκτελέστε:

```bash
dotnet add package Aspose.Pdf
```

Ή, αν προτιμάτε το UI, κάντε δεξί‑κλικ στο **Dependencies → Manage NuGet Packages**, αναζητήστε *Aspose.Pdf* και κάντε κλικ στο **Install**. Αυτό θα κατεβάσει την πιο πρόσφατη σταθερή έκδοση (από Ιούλιο 2026, έκδοση 23.12).

## Βήμα 2: Άνοιγμα του Πηγαίου PDF Εγγράφου

Η πρώτη γραμμή κάθε ροής εργασίας **add bates numbering pdf** είναι η φόρτωση του αρχείου που θέλετε να σφραγίσετε. Θα τυλίξουμε τη λειτουργία σε ένα μπλοκ `using` ώστε το έγγραφο να απελευθερώνεται αυτόματα.

```csharp
using Aspose.Pdf;

// Step 2: Load the PDF you want to number
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here...
}
```

> **Pro tip:** Αν το PDF σας βρίσκεται σε cloud bucket, μπορείτε να περάσετε ένα `Stream` αντί για διαδρομή αρχείου—το Aspose.PDF διαχειρίζεται και τα δύο αβίαστα.

## Βήμα 3: Ορισμός του Αριθμού Εκκίνησης και του Προθέματος

Τώρα έρχεται η καρδιά του **bates numbering example**: να πείτε στο Aspose από πού να ξεκινήσει και ποιο κείμενο θα προηγείται κάθε αριθμού. Η ιδιότητα `BatesNumbering` εκθέτει τόσο το `Start` όσο και το `Prefix`.

```csharp
    // Step 3a: Define where the numbering begins
    pdfDocument.BatesNumbering.Start = 1000;   // you can start anywhere

    // Step 3b: Add a custom prefix – this is the prefix bates number you asked for
    pdfDocument.BatesNumbering.Prefix = "ABC-";
```

Γιατί να χρησιμοποιήσετε πρόθεμα; Σε πολλές νομικές υποθέσεις το πρόθεμα αναγνωρίζει το φάκελο της υπόθεσης, το τμήμα ή την παρτίδα παραγωγής. Χρησιμοποιώντας το `"ABC-"` ως placeholder, μπορείτε να το αλλάξετε σε `"CASE42-"` ή σε οποιοδήποτε string ταιριάζει με τη σύμβαση ονοματοδοσίας σας.

## Βήμα 4: Επιλογή Θέσης των Αριθμών (Προαιρετικό)

Το Aspose τοποθετεί εξ ορισμού τον αριθμό στην κάτω‑δεξιά γωνία, αλλά μπορείτε να τον μετακινήσετε οπουδήποτε τροποποιώντας την ιδιότητα `Location`. Αυτό το βήμα δεν είναι υποχρεωτικό για μια βασική λειτουργία **add bates numbering pdf**, ωστόσο είναι χρήσιμο να το γνωρίζετε.

```csharp
    // Optional: Move the number to the top‑left corner
    pdfDocument.BatesNumbering.Location = new Location(10, pdfDocument.Pages[1].PageInfo.Height - 30);
```

Η `Location` δέχεται συντεταγμένες X και Y μετρημένες σε points (1 pt ≈ 1/72 in). Προσαρμόστε τις όπως χρειάζεται για τη διάταξη της σελίδας σας.

## Βήμα 5: Αποθήκευση του Ενημερωμένου PDF

Τέλος, αποθηκεύστε τις αλλαγές. Η μέθοδος `Save` του `BatesNumbering` γράφει ένα νέο αρχείο ενώ διατηρεί το αρχικό ανέγγιχτο.

```csharp
    // Step 5: Write the output file with numbering applied
    pdfDocument.BatesNumbering.Save("YOUR_DIRECTORY/output.pdf");
}
```

Όταν ανοίξετε το `output.pdf`, κάθε σελίδα θα εμφανίζει κάτι όπως `ABC-1000`, `ABC-1001`, … μέχρι την τελευταία σελίδα.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το **bates numbering example** που μπορείτε να αντιγράψετε‑επικολλήσετε στη μέθοδο `Main` μιας εφαρμογής console:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Path configuration – adjust to your environment
        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        // Load the PDF
        using (var pdfDocument = new Document(inputPath))
        {
            // Set start number and prefix
            pdfDocument.BatesNumbering.Start = 1000;
            pdfDocument.BatesNumbering.Prefix = "ABC-";

            // (Optional) Change location – comment out if default is fine
            // pdfDocument.BatesNumbering.Location = new Location(10, pdfDocument.Pages[1].PageInfo.Height - 30);

            // Save the numbered PDF
            pdfDocument.BatesNumbering.Save(outputPath);
        }

        Console.WriteLine($"Bates numbering applied! Check: {outputPath}");
    }
}
```

**Αναμενόμενη έξοδος** (στο console):

```
Bates numbering applied! Check: YOUR_DIRECTORY\output.pdf
```

Ανοίξτε το παραγόμενο PDF και θα δείτε διαδοχικούς αριθμούς με πρόθεμα `ABC-` που ξεκινούν από `1000`.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν χρειαστεί να επαναφέρω τον μετρητή για κάθε ενότητα;

Μπορείτε να καλέσετε `pdfDocument.BatesNumbering.Reset()` πριν επεξεργαστείτε ένα νέο εύρος σελίδων. Συνδυάστε το με έναν βρόχο πάνω από `pdfDocument.Pages` και ορίστε ξανά το `Start` για κάθε ενότητα.

### Πώς εφαρμόζω διαφορετικά προθέματα σε διαφορετικά εύρη σελίδων;

Δημιουργήστε πολλαπλά αντικείμενα `BatesNumbering`—ένα ανά εύρος—με κλωνοποίηση του εγγράφου ή χρησιμοποιώντας τη μέθοδο `Add` (διαθέσιμη σε νεότερες εκδόσεις Aspose). Ένα γρήγορο σκίτσο:

```csharp
// Number first 10 pages with "PRE‑"
pdfDocument.BatesNumbering.Start = 1;
pdfDocument.BatesNumbering.Prefix = "PRE-";
pdfDocument.BatesNumbering.Save(outputPath, new PageRange(1, 10));

// Number the rest with "POST‑"
pdfDocument.BatesNumbering.Start = 1;
pdfDocument.BatesNumbering.Prefix = "POST-";
pdfDocument.BatesNumbering.Save(outputPath, new PageRange(11, pdfDocument.Pages.Count));
```

### Υποστηρίζει η βιβλιοθήκη προθέματα Unicode;

Απόλυτα. Περάστε οποιοδήποτε Unicode string (π.χ. `"案件‑"`). Το Aspose.PDF διαχειρίζεται δεξιά‑προς‑αριστερά σενάρια και ειδικά σύμβολα χωρίς επιπλέον ρυθμίσεις.

### Τι γίνεται με την ασφάλεια του PDF—θα σπάσει η κρυπτογράφηση από το Bates numbering;

Αν το πηγαίο PDF είναι κρυπτογραφημένο, πρέπει να δώσετε τον κωδικό πρόσβασης πριν αποκτήσετε πρόσβαση στο `BatesNumbering`. Η διαδικασία αριθμησης σέβεται τις αρχικές ρυθμίσεις κρυπτογράφησης—το αποτέλεσμα θα παραμείνει κρυπτογραφημένο εκτός αν το αλλάξετε ρητά.

```csharp
pdfDocument.Encrypt(new DocumentEncryption("ownerPwd", "userPwd"));
```

## Συμβουλές & Καλές Πρακτικές

- **Batch processing:** Τυλίξτε όλη τη ρουτίνα σε έναν βρόχο `foreach` για να επεξεργαστείτε δεκάδες αρχεία αυτόματα.
- **Logging:** Καταγράψτε τον αριθμό εκκίνησης, το πρόθεμα και τη διαδρομή εξόδου σε αρχείο καταγραφής· αυτό διευκολύνει τα audit trails για τις νομικές ομάδες.
- **Performance:** Για τεράστια PDF (500 + σελίδες), σκεφτείτε την ενεργοποίηση **memory optimization** μέσω `pdfDocument.OptimizeMemory = true;`.
- **Testing:** Κρατήστε πάντα ένα αντίγραφο του αρχικού PDF· η προσθήκη Bates numbers είναι μη αναστρέψιμη μετά την αποθήκευση.

## Συμπέρασμα

Σε αυτό το **bates numbering tutorial** καλύψαμε όλα όσα χρειάζεστε για να **add bates numbering pdf** αρχεία με το Aspose.PDF:

1. Εγκατάσταση της βιβλιοθήκης.  
2. Φόρτωση του πηγαίου εγγράφου.  
3. Ορισμός του αριθμού εκκίνησης και ενός **prefix bates number**.  
4. (Προαιρετικά) προσαρμογή της θέσης.  
5. Αποθήκευση του αποτελέσματος.

Τώρα έχετε ένα στιβαρό **bates numbering example** που μπορείτε να προσαρμόσετε σε οποιαδήποτε νομική, αρχειακή ή συμμορφωτική ροή εργασίας. Θέλετε να πάτε πιο πέρα; Δοκιμάστε να συνδυάσετε τους αριθμούς Bates με υδατογραφήματα, ή δημιουργήστε ένα CSV manifest που αντιστοιχεί κάθε σελίδα στο αναγνωριστικό της. Ο ουρανός είναι το όριο, και το Aspose σας δίνει τα εργαλεία για να το πετύχετε.

---

*Έτοιμοι να το θέσετε σε παραγωγή; Αφήστε ένα σχόλιο αν συναντήσετε δυσκολίες, και καλή προγραμματιστική!*

## Τι Θα Μάθετε Στη Σειρά Επόμενη;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Εφαρμογή Στυλ Αρίθμησης σε Επικεφαλίδα PDF χρησιμοποιώντας Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Aspose Pdf Net Floatingbox Page Numbering](/pdf/german/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Εφαρμογή Στυλ Αρίθμησης σε Επικεφαλίδα PDF χρησιμοποιώντας Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}