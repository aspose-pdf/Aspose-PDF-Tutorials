---
category: general
date: 2026-01-15
description: Προσθέστε αριθμούς Bates στο PDF σας γρήγορα με το Aspose.Pdf. Μάθετε
  πώς να προσθέσετε υποσέλιδο σε PDF, να προσθέσετε αριθμούς σελίδων σε PDF και να
  δημιουργήσετε προσαρμοσμένη αρίθμηση σελίδων.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: el
og_description: Προσθέστε αριθμούς Bates στο PDF σας γρήγορα με το Aspose.Pdf. Μάθετε
  πώς να προσθέσετε υποσέλιδο στο PDF, να προσθέσετε αριθμούς σελίδων στο PDF και
  να προσθέσετε προσαρμοσμένη αρίθμηση σελίδων.
og_title: Προσθήκη αριθμών Bates σε PDF – αρίθμηση Bates PDF
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Προσθήκη αριθμών Bates σε PDF – αρίθμηση Bates PDF
url: /el/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Bates Numbers σε PDF – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **add bates numbers** σε ένα PDF αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι—νομικές ομάδες, ελεγκτές και όποιος ασχολείται με τεράστιες συλλογές εγγράφων αντιμετωπίζει αυτό το πρόβλημα καθημερινά. Τα καλά νέα; Με το Aspose.Pdf για .NET μπορείτε να προσθέσετε αυτούς τους αριθμούς σε κάθε σελίδα με λίγες μόνο γραμμές κώδικα.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από την προσθήκη της βιβλιοθήκης Aspose.Pdf, τη φόρτωση του αρχείου πηγής, τη ρύθμιση ενός *BatesNumberingArtifact*, την προσθήκη του ως υποσέλιδο, και τέλος την αποθήκευση του αποτελέσματος. Στο τέλος θα γνωρίζετε επίσης πώς να **add footer to pdf**, **add page numbers pdf**, και ακόμη **add custom page numbering** για εκείνες τις δύσκολες περιπτώσεις.

## Τι Θα Χρειαστείτε

- .NET 6+ (ή .NET Framework 4.8 εάν εξακολουθείτε να χρησιμοποιείτε την κλασική πλατφόρμα)  
- Μια αναφορά στο πακέτο NuGet **Aspose.Pdf** (`Install-Package Aspose.Pdf`)  
- Ένα αρχείο PDF που θέλετε να σφραγίσετε (θα το ονομάσουμε `source.pdf`)  

Αυτό είναι όλο—χωρίς επιπλέον εργαλεία, χωρίς βαριές εφαρμογές PDF. Ας βουτήξουμε.

![add bates numbers example](https://example.com/images/add-bates-numbers.png "add bates numbers example")

## Βήμα 1: Προσθήκη Bates Numbers – Φόρτωση του Εγγράφου PDF

Πρώτα, χρειαζόμαστε ένα αντικείμενο `Document` που αντιπροσωπεύει το PDF που πρόκειται να τροποποιήσουμε. Σκεφτείτε το ως το άνοιγμα ενός εγγράφου Word πριν αρχίσετε να πληκτρολογείτε.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του αρχείου σας δίνει πρόσβαση στη συλλογή `Pages`, όπου θα προσθέσουμε το Bates numbering artifact αργότερα. Εάν το αρχείο δεν βρεθεί, το Aspose θα ρίξει ένα σαφές `FileNotFoundException`, οπότε ελέγξτε ξανά τη διαδρομή.

## Βήμα 2: Ρύθμιση των ρυθμίσεων bates numbering pdf

Τώρα ορίζουμε *πώς* πρέπει να φαίνονται οι αριθμοί. Το `BatesNumberingArtifact` σας επιτρέπει να ορίσετε πρόθεμα, αριθμό εκκίνησης, μηδενική συμπλήρωση ψηφίων, επίθημα και θέση. Αυτό είναι ο πυρήνας του **bates numbering pdf**.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **Συμβουλή:** Εάν χρειάζεστε τους αριθμούς να εμφανίζονται στην κεφαλίδα αντί για το υποσέλιδο, αντικαταστήστε το `BottomCenter` με `TopCenter`. Το enum τοποθέτησης υποστηρίζει επίσης `BottomLeft`, `BottomRight`, κ.λπ., προσφέροντάς σας ευελιξία για διαφορετικά στυλ **add footer to pdf**.

## Βήμα 3: Προσθήκη page numbers pdf – Επισύναψη του Artifact σε Κάθε Σελίδα

Με το artifact έτοιμο, κάνουμε βρόχο σε κάθε σελίδα και το προσθέτουμε στη συλλογή `Artifacts`. Αυτό είναι το βήμα που πραγματικά **adds page numbers pdf**.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **Τι συμβαίνει στο παρασκήνιο;** Η συλλογή `Artifacts` αποδίδεται μετά το κύριο περιεχόμενο της σελίδας, εξασφαλίζοντας ότι ο αριθμός Bates βρίσκεται πάνω από τυχόν υπάρχον κείμενο αλλά κάτω από τις σημειώσεις. Εάν χρειάζεστε τον αριθμό πίσω από το περιεχόμενο (σπάνια), θα χρησιμοποιούσατε `page.Artifacts.Insert(0, batesArtifact)`.

## Βήμα 4: Προσθήκη custom page numbering – Αποθήκευση του Ενημερωμένου PDF

Τέλος, γράφουμε το τροποποιημένο έγγραφο στο δίσκο. Το αρχείο εξόδου θα περιέχει τους Bates numbers ως μόνιμο μέρος κάθε σελίδας.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **Συμβουλή επαλήθευσης:** Ανοίξτε το `bates_out.pdf` σε οποιονδήποτε προβολέα. Θα πρέπει να δείτε κάτι όπως `CASE-01000-A` κεντραρισμένο στο κάτω μέρος κάθε σελίδας. Εάν λείπουν οι αριθμοί, ελέγξτε ξανά ότι η ιδιότητα `Placement` ταιριάζει με την επιθυμητή θέση.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

- **File:** `bates_out.pdf` στον ίδιο φάκελο με το `source.pdf`  
- **Visual:** Κείμενο κεντραρισμένο κάτω‑κέντρο `CASE-01000-A`, `CASE-01001-A`, … για κάθε επόμενη σελίδα  
- **Behaviour:** Οι αριθμοί είναι μόνιμα ενσωματωμένοι· διατηρούνται κατά την εκτύπωση, την εξομάλυνση και περαιτέρω επεξεργασία.  

## Συνηθισμένες Παραλλαγές & Edge Cases

| Situation | How to Adjust |
|-----------|---------------|
| **Διαφορετικός αριθμός εκκίνησης** | Αλλάξτε το `StartNumber` σε οποιονδήποτε ακέραιο (π.χ., `StartNumber = 500`). |
| **Γράμματα επίθημα ανά τόμο** | Χρησιμοποιήστε βρόχο για να τροποποιήσετε το `Suffix` ανά σελίδα, ή δημιουργήστε πολλαπλά artifacts με διαφορετικά επίθημα. |
| **Αρίθμηση δεξιά‑ευθυγραμμισμένη** | Ορίστε `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **Μεγάλα έγγραφα (10k+ σελίδες)** | Σκεφτείτε την ομαδοποίηση σελίδων ή την αύξηση του `NumberDigits` για να αποφύγετε υπερχείλιση. |
| **Απαίτηση απόκρυψης αριθμών σε ορισμένες σελίδες** | Παραλείψτε αυτές τις σελίδες στον βρόχο `foreach` (π.χ., `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **Προσοχή:** Η χρήση `Prefix` ή `Suffix` που περιέχει μη επιτρεπόμενους χαρακτήρες ονόματος αρχείου (π.χ., `*` ή `?`). Το Aspose θα τα ενσωματώσει, αλλά μπορεί να προκαλέσουν προβλήματα όταν αργότερα εξάγετε το κείμενο.

## Συμβουλές για Παραγωγική Χρήση

- **Cache the artifact** εάν επεξεργάζεστε πολλά PDF διαδοχικά· η δημιουργία του μία φορά εξοικονομεί μερικά χιλιοστά του δευτερολέπτου ανά αρχείο.  
- **Thread‑safety:** Η παρουσία `BatesNumberingArtifact` δεν είναι ασφαλής για νήματα, γι' αυτό δώστε σε κάθε νήμα το δικό του αντίγραφο.  
- **Performance:** Για τεράστιες παρτίδες, απενεργοποιήστε τη συμπίεση PDF (`pdfDocument.Compress = false`) πριν την αποθήκευση, και ενεργοποιήστε ξανά αν χρειαστεί.  
- **Testing:** Πάντα εκτελέστε έναν γρήγορο οπτικό έλεγχο στο πρώτο παραγόμενο PDF για να βεβαιωθείτε ότι η θέση ταιριάζει με τα πρότυπα της νομικής σας ομάδας.  

## Συμπέρασμα

Τώρα έχετε μια ολοκληρωμένη, από‑αρχή‑μέχρι‑τέλος συνταγή για το πώς να **add bates numbers** σε οποιοδήποτε PDF χρησιμοποιώντας το Aspose.Pdf, με επιλογές για **add footer to pdf**, **add page numbers pdf**, και **add custom page numbering**. Ο κώδικας είναι πλήρως αυτόνομος, λειτουργεί με .NET 6 και νεότερες εκδόσεις, και μπορεί να ενσωματωθεί σε οποιοδήποτε υπάρχον pipeline αυτοματοποίησης.

Τι ακολουθεί; Δοκιμάστε να αλλάξετε τη θέση `BottomCenter` σε στυλ κεφαλίδας, πειραματιστείτε με δυναμικά προθέματα (π.χ., IDs υποθέσεων από βάση δεδομένων), ή συνδυάστε το με τις δυνατότητες εξαγωγής κειμένου του Aspose για να δημιουργήσετε ένα ευρετήριο αναζήτησης των νέων αριθμημένων εγγράφων σας. Ο ουρανός είναι το όριο, και μόλις αποκτήσατε ένα ισχυρό εργαλείο για τον έλεγχο εγγράφων.

Καλό κώδικα, και εύχομαι τα PDF σας να παραμένουν πάντα τέλεια αριθμημένα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}