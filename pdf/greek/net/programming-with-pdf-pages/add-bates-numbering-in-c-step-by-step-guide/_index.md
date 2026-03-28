---
category: general
date: 2026-03-27
description: Προσθέστε γρήγορα αριθμητική Bates σε C#. Μάθετε πώς να προσθέτετε προσαρμοσμένους
  αριθμούς σελίδων, διαδοχικούς αριθμούς σελίδων και προσαρμοσμένους αριθμούς σε έγγραφα
  Word.
draft: false
keywords:
- add bates numbering
- how to add bates
- add custom page numbers
- add sequential page numbers
- add custom numbers
language: el
og_description: Προσθέστε αρίθμηση Bates σε C# με ένα σαφές παράδειγμα. Αυτός ο οδηγός
  δείχνει πώς να προσθέσετε προσαρμοσμένους αριθμούς σελίδων, να προσθέσετε διαδοχικούς
  αριθμούς σελίδων και άλλα.
og_title: Προσθήκη αρίθμησης Bates σε C# – Πλήρης οδηγός
tags:
- C#
- Document Processing
- Bates Numbering
title: Προσθήκη Αρίθμησης Bates σε C# – Οδηγός Βήμα‑Βήμα
url: /el/net/programming-with-pdf-pages/add-bates-numbering-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Bates Numbering σε C# – Οδηγός Βήμα‑Βήμα

Έχετε αναρωτηθεί ποτέ πώς να **add bates numbering** σε ένα έγγραφο Word χωρίς να τσακίζετε τα μαλλιά σας; Δεν είστε ο μόνος. Σε πολλά νομικά ή έργα συμμόρφωσης, κάθε σελίδα χρειάζεται ένα μοναδικό αναγνωριστικό, και η χειροκίνητη προσθήκη είναι εφιάλτης.  

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που **adds bates numbering**, σας δείχνει **how to add bates** σε λίγες γραμμές, και ακόμη καλύπτει πώς να **add custom page numbers** και **add sequential page numbers** όταν τα χρειάζεστε. Στο τέλος θα έχετε ένα αρχείο .docx σφραγισμένο με τους αριθμούς που επιλέγετε—χωρίς εργαλεία τρίτων.

## Τι Θα Μάθετε

- Φορτώστε ένα αρχείο DOCX με το Aspose.Words for .NET API (ή οποιαδήποτε συμβατή βιβλιοθήκη).  
- Διαμορφώστε **add custom numbers** όπως ένα πρόθεμα, μια αρχική τιμή και ένα μέγεθος γραμματοσειράς.  
- Εφαρμόστε την αρίθμηση σε κάθε σελίδα με μία κλήση.  
- Αποθηκεύστε το αποτέλεσμα και επαληθεύστε ότι οι αριθμοί εμφανίζονται όπως αναμένεται.  

Δεν απαιτείται προηγούμενη εμπειρία με Bates numbering· χρειάζεται μόνο μια βασική ρύθμιση C# και ένα αντίγραφο του πηγαίου εγγράφου. Ας βουτήξουμε.

## Προαπαιτούμενα

- .NET 6+ (ο κώδικας λειτουργεί τόσο σε .NET Core όσο και σε .NET Framework).  
- Aspose.Words for .NET εγκατεστημένο μέσω NuGet (`Install-Package Aspose.Words`).  
- Ένα έγγραφο Word με όνομα `input.docx` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε (`YOUR_DIRECTORY`).  
- Visual Studio, VS Code ή οποιοδήποτε IDE C# προτιμάτε.

> **Συμβουλή επαγγελματία:** Αν χρησιμοποιείτε διαφορετική βιβλιοθήκη (π.χ., Open XML SDK), οι έννοιες παραμένουν ίδιες—απλώς αντικαταστήστε τις κλήσεις API.

## Βήμα 1: Φόρτωση του Πηγαίου Εγγράφου

Πρώτα πρέπει να φέρουμε το αρχείο Word στη μνήμη.

```csharp
using Aspose.Words;

// Step 1: Load the source document
Document document = new Document("YOUR_DIRECTORY/input.docx");
```

*Γιατί είναι σημαντικό:* Η φόρτωση του αρχείου δημιουργεί ένα αντικείμενο `Document` που σας δίνει πρόσβαση σε σελίδες, ενότητες και στο χαμηλού επιπέδου δέντρο κόμβων. Χωρίς αυτό δεν μπορείτε να προσθέσετε καμία αρίθμηση.

## Βήμα 2: Διαμόρφωση Επιλογών Bates Numbering

Τώρα ορίζουμε ακριβώς πώς πρέπει να φαίνονται οι αριθμοί. Εδώ είναι που **add custom page numbers** ή **add sequential page numbers**.

```csharp
// Step 2: Define Bates numbering options (prefix, start number, font size)
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Prefix that appears before every number, e.g., "ABC"
    Prefix = "ABC",
    // The first number in the sequence; change to 1 if you prefer
    Start = 1000,
    // Font size in points; 9 works well for most legal docs
    FontSize = 9
};
```

*Γιατί είναι σημαντικό:* Το `Prefix` σας επιτρέπει να **add custom numbers** όπως ένα ID υπόθεσης, ενώ το `Start` καθορίζει τον αρχικό μετρητή. Η αλλαγή του `FontSize` εξασφαλίζει ότι οι αριθμοί δεν καταπίνουν τα περιθώρια της σελίδας.

## Βήμα 3: Εφαρμογή Bates Numbering σε Κάθε Σελίδα

Με τις επιλογές έτοιμες, λέμε στη βιβλιοθήκη να σφραγίσει κάθε σελίδα.

```csharp
// Step 3: Apply Bates numbering to all pages of the document
document.Pages.AddBatesNumbering(batesOptions);
```

*Γιατί είναι σημαντικό:* Η μέθοδος `AddBatesNumbering` διασχίζει τη συλλογή εσωτερικών σελίδων και εισάγει ένα πλαίσιο κειμένου στην κάτω‑δεξιά γωνία (η προεπιλεγμένη θέση). Είναι ο πυρήνας του **how to add bates** χωρίς να γράψετε βρόχο εσείς.

## Βήμα 4: Αποθήκευση του Ενημερωμένου Εγγράφου

Τέλος, γράφουμε το τροποποιημένο αρχείο πίσω στο δίσκο.

```csharp
// Step 4: Save the updated document
document.Save("YOUR_DIRECTORY/output.docx");
```

*Γιατί είναι σημαντικό:* Η αποθήκευση δημιουργεί ένα νέο `output.docx` που μπορείτε να ανοίξετε σε Word, LibreOffice ή οποιονδήποτε προβολέα για να επιβεβαιώσετε ότι οι αριθμοί εμφανίζονται.

## Αναμενόμενο Αποτέλεσμα

Ανοίξτε το `output.docx`. Κάθε σελίδα πρέπει να εμφανίζει κάτι όπως:

```
ABC‑1000   (on page 1)
ABC‑1001   (on page 2)
ABC‑1002   (on page 3)
...
```

Αν ανοίξετε την προεπισκόπηση εκτύπωσης του εγγράφου, θα δείτε τους αριθμούς στην κάτω‑δεξιά γωνία, ταιριάζοντας με το μέγεθος γραμματοσειράς που ορίσατε.

## Ακραίες Περιπτώσεις & Παραλλαγές

| Situation | What to Change | Why |
|-----------|----------------|-----|
| **Δεν απαιτείται πρόθεμα** | `Prefix = string.Empty` | Αφαιρεί το τμήμα “ABC‑”, αφήνοντας μόνο τη αριθμητική ακολουθία. |
| **Έναρξη στο 1** | `Start = 1` | Χρήσιμο για απλή **add sequential page numbers** χωρίς προσαρμοσμένο πρόθεμα. |
| **Μεγάλα έγγραφα (>10.000 σελίδες)** | Increase `FontSize` or adjust `Location` (use overloads of `AddBatesNumbering`) | Αποτρέπει την επικάλυψη με υποσέλιδα ή κεφαλίδες. |
| **Αρχείο πηγής μόνο για ανάγνωση** | Open with `LoadOptions` that allow write access, or copy the file first | Διαφορετικά, το `document.Save` θα πετάξει μια εξαίρεση. |
| **Διαφορετική τοποθέτηση** | Use `batesOptions.Position = BatesNumberingPosition.TopLeft` (or other enum) | Ορισμένες εταιρείες απαιτούν αριθμούς στην κορυφή της σελίδας. |

> **Σημείωση:** Δεν εκθέτουν όλες οι βιβλιοθήκες μια κλάση `BatesNumberingOptions`. Με το Open XML SDK θα εισάγετε ένα `TextBox` χειροκίνητα—ίδια αρχή, περισσότερος κώδικας.

## Πλήρες Παράδειγμα Λειτουργίας

Ακολουθεί ολόκληρο το πρόγραμμα σε ένα μέρος. Αντιγράψτε‑και‑επικολλήστε το σε μια εφαρμογή κονσόλας και τρέξτε το.

```csharp
using System;
using Aspose.Words;

class Program
{
    static void Main()
    {
        // Load the source document
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Define Bates numbering options
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",      // custom prefix
            Start = 1000,        // starting number
            FontSize = 9         // font size in points
        };

        // Apply numbering to every page
        document.Pages.AddBatesNumbering(batesOptions);

        // Save the result
        document.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το `output.docx`, και θα δείτε την αρίθμηση ακριβώς όπου περιμένατε. 🎉

## Συχνές Ερωτήσεις

**Q: Μπορώ να αλλάξω το χρώμα των αριθμών;**  
A: Ναι. Μετά την κλήση του `AddBatesNumbering`, μπορείτε να ανακτήσετε τα παραγόμενα αντικείμενα `Shape` και να ορίσετε την ιδιότητα `FillColor`.

**Q: Τι γίνεται αν χρειάζομαι τους αριθμούς στην αριστερή πλευρά αντί για τη δεξιά;**  
A: Χρησιμοποιήστε `batesOptions.Position = BatesNumberingPosition.BottomLeft` (ή `TopLeft`, `TopRight`). Το API υποστηρίζει όλες τις τέσσερις γωνίες.

**Q: Λειτουργεί αυτό με έξοδο PDF;**  
A: Απολύτως. Μετά την προσθήκη της αρίθμησης, καλέστε `document.Save("output.pdf")`. Οι αριθμοί αποδίδονται στο PDF όπως στο Word.

## Συμπέρασμα

Τώρα γνωρίζετε **how to add bates numbering** σε ένα αρχείο Word χρησιμοποιώντας C#. Το tutorial κάλυψε τη φόρτωση ενός εγγράφου, τη διαμόρφωση **add custom numbers**, την εφαρμογή **add sequential page numbers**, και την αποθήκευση του τελικού αποτελέσματος. Με το πλήρες δείγμα κώδικα, μπορείτε να το ενσωματώσετε σε οποιοδήποτε έργο και να αρχίσετε να σφραγίζετε έγγραφα αμέσως.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να το συνδυάσετε με έναν επεξεργαστή batch που διατρέχει έναν φάκελο αρχείων, ή εξερευνήστε **add custom page numbers** στην κεφαλίδα/υποσέλιδο για πιο επεξεργασμένη εμφάνιση. Σε κάθε περίπτωση, έχετε μια ισχυρή βάση για οποιοδήποτε έργο legal‑tech ή αυτοματοποίησης συμμόρφωσης.

Έχετε ερωτήσεις ή ένα ενδιαφέρον σενάριο χρήσης; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}