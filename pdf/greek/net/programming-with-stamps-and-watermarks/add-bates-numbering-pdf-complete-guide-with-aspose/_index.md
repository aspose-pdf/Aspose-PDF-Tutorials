---
category: general
date: 2026-06-08
description: Προσθήκη αρίθμησης Bates σε PDF χρησιμοποιώντας το Aspose.Pdf σε C#.
  Μάθετε πώς να προσθέτετε Bates, να προσθέτετε αριθμούς σελίδων σε PDF, να προσθέτετε
  διαδοχικούς αριθμούς σε PDF και δείτε ένα παράδειγμα PDF με αριθμό Bates.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add page numbers pdf
- add sequential numbers pdf
- bates number pdf example
language: el
og_description: Προσθήκη αρίθμησης Bates σε PDF με C#. Αυτό το σεμινάριο δείχνει πώς
  να προσθέσετε Bates, να προσθέσετε αριθμούς σελίδων σε PDF και να προσθέσετε διαδοχικούς
  αριθμούς σε PDF με ένα πλήρες παράδειγμα αρίθμησης Bates σε PDF.
og_title: Προσθήκη Αρίθμησης Bates σε PDF – Πλήρης Οδηγός με το Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  headline: Add Bates Numbering PDF – Complete Guide with Aspose
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  name: Add Bates Numbering PDF – Complete Guide with Aspose
  steps:
  - name: Install the Aspose.Pdf NuGet Package
    text: 'First, add the library to your project. Open the Package Manager Console
      and run:'
  - name: Open the Source PDF Document
    text: Now we load the PDF we want to stamp. The `using` statement ensures the
      file is closed properly even if an exception occurs.
  - name: Create a Bates Numbering Facade
    text: 'The *facade* pattern hides the complexity of the underlying PDF structure.
      Here’s how we instantiate it:'
  - name: Configure the Starting Number and Prefix
    text: Bates numbers often include a case‑specific prefix. You can also control
      the number of digits, the separator, and the placement on the page.
  - name: Apply the Bates Numbering to the Document
    text: 'With the facade configured, we now stamp every page:'
  - name: Save the Modified PDF
    text: 'Finally, write the output to disk:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF processing
title: Προσθήκη αριθμητικής Bates σε PDF – Πλήρης οδηγός με το Aspose
url: /el/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-guide-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Bates Numbering PDF – Πλήρης Οδηγός Προγραμματισμού

Έχετε ποτέ χρειαστεί να **add bates numbering pdf** αλλά δεν ήξερες από πού να ξεκινήσεις; Αν έχετε ποτέ αναρωτηθεί *πώς να προσθέσετε bates* σε ένα νομικό έγγραφο, βρίσκεστε στο σωστό μέρος. Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό, ολοκληρωμένο παράδειγμα που όχι μόνο προσθέτει αριθμούς Bates αλλά επίσης σας δείχνει πώς να **add page numbers pdf**, **add sequential numbers pdf**, και ακόμη παρέχει ένα έτοιμο προς εκτέλεση **bates number pdf example**.

Θα χρησιμοποιήσουμε τη βιβλιοθήκη Aspose.Pdf για .NET, επειδή αφαιρεί την πολυπλοκότητα των χαμηλού επιπέδου εσωτερικών του PDF ενώ σας παρέχει λεπτομερή έλεγχο. Στο τέλος αυτού του οδηγού θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο C#, και θα καταλάβετε γιατί κάθε γραμμή είναι σημαντική.

## Τι Θα Χρειαστείτε

- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+).  
- Μια **license** για Aspose.Pdf ή ένα δωρεάν προσωρινό κλειδί αξιολόγησης.  
- Ένα δείγμα PDF με όνομα `input.pdf` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε.  
- Visual Studio, Rider ή οποιονδήποτε επεξεργαστή C# προτιμάτε.

Αυτό είναι όλο—χωρίς επιπλέον εργαλεία, χωρίς γυμναστική στη γραμμή εντολών. Έτοιμοι; Ας ξεκινήσουμε.

## Προσθήκη Bates Numbering PDF – Υλοποίηση Βήμα‑βήμα

Παρακάτω χωρίζουμε τη διαδικασία σε έξι λογικά βήματα. Κάθε βήμα περιλαμβάνει ένα σύντομο απόσπασμα κώδικα, μια εξήγηση του *γιατί* το κάνουμε, και μια συμβουλή που μπορεί να βρείτε χρήσιμη.

### Βήμα 1: Εγκατάσταση του πακέτου NuGet Aspose.Pdf

Πρώτα, προσθέστε τη βιβλιοθήκη στο έργο σας. Ανοίξτε το Package Manager Console και εκτελέστε:

```powershell
Install-Package Aspose.Pdf
```

> **Συμβουλή:** Αν βρίσκεστε σε .NET Core, μπορείτε επίσης να χρησιμοποιήσετε `dotnet add package Aspose.Pdf`.

Η εγκατάσταση του πακέτου σας δίνει πρόσβαση στην κλάση `Aspose.Pdf.Facades.BatesNumbering`, η οποία είναι η κύρια μηχανή για **add bates numbering pdf**.

### Βήμα 2: Άνοιγμα του Πηγαίου Εγγράφου PDF

Τώρα φορτώνουμε το PDF που θέλουμε να σφραγίσουμε. Η δήλωση `using` εξασφαλίζει ότι το αρχείο κλείνει σωστά ακόμα και αν προκύψει εξαίρεση.

```csharp
using (var doc = new Aspose.Pdf.Document(@"C:\MyPdfs\input.pdf"))
{
    // All further steps happen inside this block.
}
```

Γιατί να χρησιμοποιήσουμε το `Aspose.Pdf.Document`; Αντιπροσωπεύει ολόκληρο το PDF στη μνήμη, επιτρέποντάς μας να χειριζόμαστε σελίδες, γραμματοσειρές και μεταδεδομένα χωρίς να αγγίζουμε το αρχικό αρχείο στο δίσκο.

### Βήμα 3: Δημιουργία Facade Αρίθμησης Bates

Το πρότυπο *facade* κρύβει την πολυπλοκότητα της υποκείμενης δομής PDF. Να πώς το δημιουργούμε:

```csharp
var bates = new Aspose.Pdf.Facades.BatesNumbering();
```

Αυτό το αντικείμενο θα ρυθμιστεί αργότερα με πρόθεμα, αριθμό εκκίνησης και επιλογές μορφοποίησης. Σκεφτείτε το ως “μηχανή” που θα **add page numbers pdf** με τρόπο συμβατό με το Bates.

### Βήμα 4: Διαμόρφωση Αριθμού Έναρξης και Προθέματος

Οι αριθμοί Bates συχνά περιλαμβάνουν πρόθεμα ειδικό για την υπόθεση. Μπορείτε επίσης να ελέγξετε τον αριθμό των ψηφίων, το διαχωριστικό και τη θέση στη σελίδα.

```csharp
bates.StartNumber = 1000;          // First number in the sequence
bates.Prefix = "CASE-";            // Prefix that appears before each number
bates.NumberOfDigits = 5;          // Pads numbers with leading zeros (e.g., 01000)
bates.Separator = "-";             // Optional separator between prefix and number
bates.Location = new Aspose.Pdf.Rectangle(0, 0, 200, 20); // Bottom‑left corner
bates.FontSize = 12;
bates.FontColor = System.Drawing.Color.Blue;
```

**Γιατί αυτές οι ρυθμίσεις;**  
- `StartNumber` σας επιτρέπει να συνεχίσετε μια προηγούμενη σειρά.  
- `NumberOfDigits` εγγυάται ομοιόμορφο μήκος, κάτι που είναι κρίσιμο για νομική ευρετηρίαση.  
- `Location` ορίζει πού θα εμφανιστεί το **add sequential numbers pdf**· μπορείτε να το μετακινήσετε στην επάνω‑δεξιά γωνία αν προτιμάτε.

### Βήμα 5: Εφαρμογή της Αρίθμησης Bates στο Έγγραφο

Με το facade ρυθμισμένο, τώρα σφραγίζουμε κάθε σελίδα:

```csharp
bates.AddBatesNumbering(doc);
```

Στο παρασκήνιο, το Aspose επαναλαμβάνει κάθε σελίδα, σχεδιάζει το κείμενο στην καθορισμένη θέση και σέβεται τυχόν υπάρχον περιεχόμενο. Αυτή η μοναδική γραμμή είναι αυτή που πραγματικά **add bates numbering pdf** στο αρχείο σας.

### Βήμα 6: Αποθήκευση του Τροποποιημένου PDF

Τέλος, γράψτε το αποτέλεσμα στο δίσκο:

```csharp
doc.Save(@"C:\MyPdfs\output.pdf");
```

Τώρα έχετε ένα PDF όπου κάθε σελίδα φέρει ένα μοναδικό αναγνωριστικό Bates, έτοιμο για αναζήτηση ή υποβολή στο δικαστήριο.

#### Πλήρες Παράδειγμα Εργασίας (Bates Number PDF Example)

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα πλήρες, αυτόνομο πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using (var doc = new Document(@"C:\MyPdfs\input.pdf"))
        {
            // 2️⃣ Create the Bates numbering facade
            var bates = new BatesNumbering();

            // 3️⃣ Configure prefix, start number, and formatting
            bates.StartNumber = 1000;
            bates.Prefix = "CASE-";
            bates.NumberOfDigits = 5;
            bates.Separator = "-";
            bates.Location = new Rectangle(0, 0, 200, 20); // Bottom‑left
            bates.FontSize = 12;
            bates.FontColor = Color.Blue;

            // 4️⃣ Apply the numbering to every page
            bates.AddBatesNumbering(doc);

            // 5️⃣ Save the result
            doc.Save(@"C:\MyPdfs\output.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

> **Αναμενόμενο αποτέλεσμα:** Ανοίξτε το `output.pdf` και θα δείτε “CASE‑01000”, “CASE‑01001”, … στην κάτω‑αριστερή γωνία κάθε σελίδας.

![Στιγμιότυπο οθόνης μιας σελίδας PDF με αριθμούς Bates στην κάτω‑αριστερή γωνία – add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "add bates numbering pdf example")

*(Κείμενο alt εικόνας: *add bates numbering pdf example* – δείχνει τους αριθμούς Bates που εφαρμόζονται σε ένα δείγμα PDF.)*

## Πώς να Προσθέσετε Bates – Κατανόηση του Facade

Μπορεί να αναρωτιέστε **how to add bates** χωρίς το facade του Aspose. Η εναλλακτική είναι να σχεδιάζετε χειροκίνητα κείμενο σε κάθε σελίδα χρησιμοποιώντας χαμηλού επιπέδου PDF operators, αλλά αυτή η προσέγγιση είναι επιρρεπής σε σφάλματα και απαιτεί βαθιά γνώση του προτύπου PDF. Το facade αφαιρεί αυτές τις λεπτομέρειες, επιτρέποντάς σας να εστιάσετε στο *τι* θέλετε (πρόθεμα, αριθμό εκκίνησης) αντί στο *πώς* να το αποδώσετε.

Αν ποτέ χρειαστείτε να **add page numbers pdf** με μη‑Bates στυλ (π.χ., “Σελίδα 3 από 12”), μπορείτε να επαναχρησιμοποιήσετε την ίδια κλάση `BatesNumbering`—απλώς αλλάξτε το `Prefix` σε κενό string και προσαρμόστε το `Location`. Η υποκείμενη μηχανή είναι η ίδια, πράγμα που σημαίνει ότι θα έχετε συνεπή απόδοση και στις δύο περιπτώσεις.

## Προσθήκη Αριθμών Σελίδων PDF – Προσαρμογή Θέσης και Στυλ

Οι νομικές ομάδες συχνά ζητούν τον αριθμό σελίδας στην κεφαλίδα, ενώ το προσωπικό υποστήριξης διαμάχης το προτιμά στο υποσέλιδο. Εδώ είναι μια γρήγορη τροποποίηση:

```csharp
bates.Location = new Rectangle(0, doc.Pages[1].PageInfo.Height - 20, 200, 20); // Top‑right
bates.Prefix = "";               // No prefix for plain page numbers
bates.StartNumber = 1;           // Start from 1
bates.NumberOfDigits = 0;        // No padding
bates.FontColor = Color.Black;
```

Η ίδια κλήση `AddBatesNumbering` θα **add page numbers pdf** τώρα στην κορυφή κάθε σελίδας. Επειδή το facade λειτουργεί στο αντικείμενο του εγγράφου, μπορείτε να εναλλάξετε μεταξύ Bates και απλής αρίθμησης σελίδων με μερικές αλλαγές ιδιοτήτων—χωρίς ανάγκη επανεγγραφής του βρόχου.

## Προσθήκη Διαδοχικών Αριθμών PDF – Προηγμένη Μορφοποίηση

Ας υποθέσουμε ότι χρειάζεστε μορφή όπως `2023-CASE-00123`. Μπορείτε να συνδυάσετε ένα πρόθεμα ημερομηνίας με τις υπάρχουσες ρυθμίσεις:

```csharp
bates.Prefix = $"{DateTime.Now:yyyy}-CASE-";
bates.NumberOfDigits = 5;
bates.Separator = "-";
```

Τώρα κάθε σελίδα θα εμφανίζει `2023-CASE-00123`, `2023-CASE-00124`, κ.λπ. Αυτό δείχνει πόσο εύκολα μπορείτε να **add sequential numbers pdf** που ικανοποιούν σύνθετες συμβάσεις ονομασίας.

## Ακραίες Περιπτώσεις και Συνηθισμένα Πιθανά Σφάλματα

| Κατάσταση | Σε τι πρέπει να προσέξετε | Προτεινόμενη λύση |
|-----------|--------------------------|-------------------|
| **Πολύ μεγάλα PDFs ( > 500 MB )** | Η κατανάλωση μνήμης μπορεί να αυξηθεί επειδή ολόκληρο το έγγραφο φορτώνεται στη RAM. | Χρησιμοποιήστε το `Document` με ρυθμίσεις `MemoryManagement` ή επεξεργαστείτε το αρχείο σε τμήματα με το `PdfFileEditor`. |
| **Existing page numbers** |

## Τι Θα Πρέπει να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Προσθέσετε και να Προσαρμόσετε Αριθμούς Σελίδων σε PDFs Χρησιμοποιώντας Aspose.PDF για .NET | Οδηγός Διαχείρισης Εγγράφων](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Πώς να Προσθέσετε Σφραγίδες Αριθμού Σελίδας σε PDFs Χρησιμοποιώντας Aspose.PDF για .NET | Υδατογραφήματα & Υπόβαθρα](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Aspose.PDF .NET: Προσθήκη Αριθμών Σελίδων σε PDFs Χρησιμοποιώντας FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}