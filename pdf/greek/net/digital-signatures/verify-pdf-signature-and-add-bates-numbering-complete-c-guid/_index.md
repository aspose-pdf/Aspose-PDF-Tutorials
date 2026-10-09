---
category: general
date: 2026-04-02
description: Επαληθεύστε γρήγορα την υπογραφή PDF και μάθετε πώς να προσθέτετε αρίθμηση
  Bates χρησιμοποιώντας το Aspose.Pdf. Περιλαμβάνει κώδικα βήμα‑βήμα και συμβουλές.
draft: false
keywords:
- verify pdf signature
- add bates numbering
- how to verify signature
- how to add bates
- check pdf signature
language: el
og_description: Επαληθεύστε γρήγορα την υπογραφή PDF και μάθετε πώς να προσθέτετε
  αρίθμηση Bates χρησιμοποιώντας το Aspose.Pdf. Ακολουθήστε το πλήρες παράδειγμα και
  αποφύγετε τα κοινά λάθη.
og_title: Επαλήθευση υπογραφής PDF και προσθήκη αρίθμησης Bates – Πλήρης οδηγός C#
tags:
- Aspose.Pdf
- C#
- Digital Signature
- Document Automation
title: Επαλήθευση υπογραφής PDF και προσθήκη αριθμητικής Bates – Πλήρης οδηγός C#
url: /el/net/digital-signatures/verify-pdf-signature-and-add-bates-numbering-complete-c-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Επαλήθευση Υπογραφής PDF και Προσθήκη Αρίθμησης Bates – Πλήρης Οδηγός C#

Κάποτε χρειάστηκε να **επαληθεύσετε την υπογραφή PDF** πριν στείλετε ένα συμβόλαιο, αλλά δεν ήξερες ποια κλήση API να χρησιμοποιήσεις; Δεν είσαι μόνος—πολλοί προγραμματιστές συναντούν αυτό το εμπόδιο όταν διαχειρίζονται νομικά δεσμευτικά PDF. Σε αυτό το tutorial θα δούμε ακριβώς πώς να **επαληθεύσετε την υπογραφή PDF** με το Aspose.Pdf και στη συνέχεια θα σας δείξουμε **πώς να προσθέσετε αρίθμηση Bates** ώστε τα αρχεία σας να είναι έτοιμα για έλεγχο.

Θα αγγίξουμε επίσης **πώς να επαληθεύσετε την υπογραφή** προγραμματιστικά, θα καλύψουμε **πώς να προσθέσετε Bates** σε μία μόνο διεργασία, και θα εξηγήσουμε **τα αποτελέσματα του check pdf signature** ώστε να μπορείτε να εμπιστεύεστε το αποτέλεσμα. Στο τέλος θα έχετε μια εκτελέσιμη εφαρμογή C# console που κάνει και τις δύο εργασίες—χωρίς μυστήριο, μόνο καθαρός κώδικας.

---

## Τι Θα Χρειαστείτε

- **.NET 6.0** ή νεότερο (το παράδειγμα λειτουργεί επίσης με .NET Framework 4.7+)  
- **Aspose.Pdf for .NET** πακέτο NuGet (έκδοση 23.11 ή νεότερη)  
- Ένα υπογεγραμμένο αρχείο PDF (`signed.pdf`) που θέλετε να επικυρώσετε  
- Ένα απλό PDF (`input.pdf`) που θα λάβει τους αριθμούς Bates  

Αν έχετε όλα αυτά, είστε έτοιμοι. Δεν χρειάζονται επιπλέον SDKs, ούτε κρυφά αρχεία ρυθμίσεων.

---

## Βήμα 1: Ρύθμιση του Έργου

Ξεκινήστε δημιουργώντας ένα έργο console:

```bash
dotnet new console -n PdfSignatureAndBatesDemo
cd PdfSignatureAndBatesDemo
dotnet add package Aspose.Pdf
```

Ανοίξτε το `Program.cs` και διαγράψτε τον προεπιλεγμένο κώδικα. Θα χτίσουμε τα πάντα από την αρχή ώστε να μπορείτε να αντιγράψετε‑επικολλήσετε την τελική έκδοση αργότερα.

---

## Βήμα 2: Επαλήθευση Υπογραφής PDF

### Γιατί είναι σημαντική η επαλήθευση

Μια ψηφιακή υπογραφή μπορεί να **συμπιεστεί** εάν το υποκείμενο πιστοποιητικό ανακληθεί ή το έγγραφο τροποποιηθεί μετά την υπογραφή. Το Aspose.Pdf μας παρέχει τη βολική μέθοδο `IsSignatureCompromised` που επιστρέφει boolean—απλό, αλλά αρκετά ισχυρό για τις περισσότερες αλυσίδες ελέγχου.

### Απόσπασμα κώδικα

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;

namespace PdfSignatureAndBatesDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // ---------- Verify PDF Signature ----------
            string signedPdfPath = @"YOUR_DIRECTORY\signed.pdf";

            // Load the signed document inside a using block to ensure disposal
            using (Document signedDoc = new Document(signedPdfPath))
            using (PdfFileSignature pdfSignature = new PdfFileSignature(signedDoc))
            {
                // The name "Signature1" is the default for the first signature.
                // Change it if your PDF uses a custom field name.
                bool isCompromised = pdfSignature.IsSignatureCompromised("Signature1");

                Console.WriteLine($"Signature compromised: {isCompromised}");
                // Expected output: "Signature compromised: False" if everything is fine.
            }

            // The rest of the program (Bates numbering) continues below...
```

**Εξήγηση**

- `Document` φορτώνει το PDF στη μνήμη.  
- `PdfFileSignature` τυλίγει το έγγραφο και εκθέτει μεθόδους σχετικές με υπογραφές.  
- `IsSignatureCompromised("Signature1")` ελέγχει την ακεραιότητα της υπογραφής με όνομα *Signature1*.  
- Το boolean αποτέλεσμα σας λέει αν η υπογραφή είναι ακόμη αξιόπιστη.

> **Συμβουλή:** Αν δεν είστε σίγουροι για το όνομα του πεδίου υπογραφής, καλέστε πρώτα `pdfSignature.GetSignatureNames()`· επιστρέφει μια λίστα με όλα τα αναγνωριστικά υπογραφών.

---

## Βήμα 3: Προετοιμασία Επιλογών Αρίθμησης Bates

### Τι είναι η αρίθμηση Bates;

Οι αριθμοί Bates είναι διαδοχικοί ταυτοποιητές που τυπώνονται σε κάθε σελίδα ενός νομικού ή εγκληματολογικού εγγράφου. Διευκολύνουν την αναφορά σε σελίδες κατά τη διάρκεια της διαδικασίας ανακάλυψης ή ελέγχου. Το `BatesNumberingOptions` του Aspose.Pdf σας επιτρέπει να προσαρμόσετε πρόθεμα, αριθμό εκκίνησης, αριθμό ψηφίων, στοίχιση και περιθώριο—όλα σε ένα αντικείμενο.

### Συνέχεια κώδικα

```csharp
            // ---------- Configure Bates Numbering ----------
            string sourcePdfPath = @"YOUR_DIRECTORY\input.pdf";
            using (Document pdfWithBates = new Document(sourcePdfPath))
            {
                // Set up the numbering style
                BatesNumberingOptions batesOptions = new BatesNumberingOptions
                {
                    Prefix = "INV-",          // Anything before the numeric part
                    StartNumber = 1000,      // First number to use
                    NumberOfDigits = 5,      // Pads numbers with leading zeros (e.g., 01000)
                    Alignment = HorizontalAlignment.Right,
                    BottomMargin = 20        // Distance from the bottom edge (points)
                };

                // Apply the numbering to every page in the document
                pdfWithBates.AddBatesNumbering(batesOptions);

                // Save the newly numbered PDF
                string outputPdfPath = @"YOUR_DIRECTORY\BatesNumbered.pdf";
                pdfWithBates.Save(outputPdfPath);

                Console.WriteLine($"Bates numbering added. File saved to: {outputPdfPath}");
                // Expected output: "Bates numbering added. File saved to: ...\BatesNumbered.pdf"
            }
        }
    }
}
```

**Εξήγηση**

- `BatesNumberingOptions` συγκεντρώνει όλες τις επιλογές μορφοποίησης.  
- `AddBatesNumbering` διασχίζει αυτόματα κάθε σελίδα—χωρίς να χρειάζεται χειροκίνητος βρόχος.  
- Το `Prefix` (`INV-`) και το `StartNumber` (1000) παράγουν ετικέτες όπως `INV-01000`, `INV-01001`, κ.λπ.  
- Προσαρμόστε το `BottomMargin` αν χρειάζεστε τον αριθμό πιο ψηλά ή πιο χαμηλά στη σελίδα.

---

## Βήμα 4: Εκτέλεση του Πλήρους Παραδείγματος

Αποθηκεύστε το αρχείο, έπειτα εκτελέστε:

```bash
dotnet run
```

Θα πρέπει να δείτε δύο γραμμές στην κονσόλα:

```
Signature compromised: False
Bates numbering added. File saved to: YOUR_DIRECTORY\BatesNumbered.pdf
```

Αν η πρώτη γραμμή εμφανίζει `True`, η υπογραφή είναι compromised—δηλαδή το έγγραφο μπορεί να έχει τροποποιηθεί μετά την υπογραφή ή το πιστοποιητικό δεν είναι πλέον έγκυρο. Σε αυτή την περίπτωση, σταματήστε οποιαδήποτε επόμενη επεξεργασία.

---

## Βήμα 5: Συνηθισμένες Ακραίες Περιπτώσεις & Πώς να τις Διαχειριστείτε

| Κατάσταση | Τι Πρέπει να Προσέξετε | Προτεινόμενη Διόρθωση |
|-----------|------------------------|------------------------|
| **Πολλαπλές υπογραφές** | `IsSignatureCompromised` ελέγχει μόνο ένα πεδίο τη φορά. | Κάντε βρόχο μέσω `pdfSignature.GetSignatureNames()` και επαληθεύστε καθεμία. |
| **Προσαρμοσμένο όνομα πεδίου υπογραφής** | Η χρήση του `"Signature1"` μπορεί να προκαλέσει εξαίρεση αν το όνομα διαφέρει. | Πάρτε πρώτα τη λίστα των ονομάτων ή περάστε το ακριβές όνομα που βλέπετε στο Acrobat. |
| **Μεγάλα PDF (100+ σελίδες)** | Η προσθήκη αριθμών Bates μπορεί να καταναλώσει πολύ μνήμη. | Χρησιμοποιήστε `Document.Save` με `SaveOptions` που ενεργοποιούν streaming (`PdfSaveOptions { Compress = true }`). |
| **Μη‑λατινικοί χαρακτήρες στο πρόθεμα** | Ορισμένες γραμματοσειρές δεν υποστηρίζουν Unicode από προεπιλογή. | Ορίστε `pdfWithBates.Font` σε μια γραμματοσειρά συμβατή με Unicode όπως `Arial Unicode MS`. |
| **Ανάγκη τοποθέτησης αριθμών στα αριστερά** | Η στοίχιση είναι σκληρά κωδικοποιημένη σε `Right`. | Αλλάξτε `Alignment = HorizontalAlignment.Left` στο `BatesNumberingOptions`. |

---

## Βήμα 6: Επαλήθευση του Αποτελέσματος Χειροκίνητα (Προαιρετικό)

Ανοίξτε το `BatesNumbered.pdf` σε οποιονδήποτε προβολέα PDF:

1. Περιηγηθείτε στις σελίδες—κάθε μία πρέπει να εμφανίζει μια ετικέτα όπως **INV‑01000** στην κάτω‑δεξιά γωνία.  
2. Χρησιμοποιήστε το **Πάνελ Υπογραφών** του Acrobat, κάντε διπλό κλικ στην υπογραφή και επιβεβαιώστε ότι η κατάσταση ταιριάζει με το αποτέλεσμα της κονσόλας.

Αν όλα ταιριάζουν, έχετε επιτυχώς **check pdf signature** και εφαρμόσει **add bates numbering** σε μία ενέργεια.

---

## Συχνές Ερωτήσεις

**Ε: Μπορώ να επαληθεύσω μια υπογραφή χωρίς να φορτώσω ολόκληρο το έγγραφο;**  
Α: Το Aspose.Pdf κάνει streaming του αρχείου στο παρασκήνιο, αλλά χρειάζεστε ακόμα ένα αντικείμενο `Document`. Για τεράστια αρχεία, σκεφτείτε να χρησιμοποιήσετε απευθείας το `PdfFileSignature` με ροή αρχείου ώστε να μειώσετε το αποτύπωμα μνήμης.

**Ε: Χρειάζομαι άδεια για το Aspose.Pdf;**  
Α: Η δωρεάν αξιολόγηση λειτουργεί, αλλά προσθέτει υδατογράφημα. Για παραγωγή θα χρειαστείτε έγκυρη άδεια· διαφορετικά τα παραγόμενα PDF θα φέρουν το λογότυπο Aspose.

**Ε: Τι γίνεται αν θέλω να προσθέσω αριθμούς Bates μόνο σε υποσύνολο σελίδων;**  
Α: Χρησιμοποιήστε `pdfWithBates.AddBatesNumbering(batesOptions, new[] { 1, 3, 5 })` όπου ο πίνακας περιέχει τους αριθμούς σελίδων που θέλετε να αριθμήσετε.

---

## Συμπέρασμα

Τώρα ξέρετε **πώς να επαληθεύσετε την υπογραφή PDF** με το Aspose.Pdf, κατανοείτε τη σημασία του boolean αποτελέσματος, και μπορείτε με σιγουριά **να προσθέσετε αρίθμηση Bates** σε οποιοδήποτε PDF ελέγχετε. Το πλήρες, εκτελέσιμο παράδειγμα συνδυάζει και τις δύο εργασίες, παρέχοντάς σας ένα μοναδικό εργαλείο console που ελέγχει την αυθεντικότητα ενός εγγράφου και το σφραγίζει με αναγνωριστικά έτοιμα για έλεγχο.

Στη συνέχεια, μπορείτε να εξερευνήσετε **πώς να επαληθεύσετε την υπογραφή** έναντι ενός αξιόπιστου αποθετηρίου ριζών, ή να πειραματιστείτε με προσαρμοσμένα στυλ **add bates numbering** όπως διαγώνιες σφραγίδες ή προθέματα ανά ενότητα. Και τα δύο θέματα βασίζονται στο θεμέλιο που μόλις κατακτήσατε και θα κάνουν τη ροή επεξεργασίας εγγράφων σας ακόμη πιο ανθεκτική.

Καλή προγραμματιστική δουλειά, και θυμηθείτε—ο έλεγχος υπογραφών και η αρίθμηση σελίδων γίνονται παιχνιδάκι όταν έχετε τον σωστό κώδικα! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}