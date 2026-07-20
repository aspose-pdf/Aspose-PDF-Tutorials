---
category: general
date: 2026-07-20
description: Πώς να προσθέσετε αρίθμηση Bates σε ένα PDF χρησιμοποιώντας το Aspose.Pdf.
  Μάθετε πώς να προσθέσετε αριθμούς Bates σε PDF και να προσθέσετε σφραγίδα σε κάθε
  σελίδα γρήγορα και αξιόπιστα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to add bates numbering
- add bates numbers pdf
- add stamp to each page
language: el
lastmod: 2026-07-20
og_description: Πώς να προσθέσετε αρίθμηση Bates σε ένα PDF με το Aspose.Pdf. Αυτός
  ο οδηγός σας δείχνει πώς να προσθέσετε αριθμούς Bates σε PDF και να σφραγίσετε κάθε
  σελίδα με λίγες μόνο γραμμές κώδικα C#.
og_image_alt: Screenshot of a PDF page displaying Bates numbering added by Aspose.Pdf
og_title: Πώς να προσθέσετε αρίθμηση Bates σε PDF – Πλήρης οδηγός Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: How to add bates numbering to a PDF using Aspose.Pdf. Learn to add
    bates numbers pdf and add stamp to each page quickly and reliably.
  headline: How to Add Bates Numbering in PDF with Aspose – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Yes. Load the document with a `PdfLoadOptions` object that supplies the
      password, then proceed exactly as shown.
    question: Does this work with password‑protected PDFs?
  - answer: Create multiple `BatesNumberingStamp` instances, configure each with its
      own `Prefix`, and apply them only to the appropriate page ranges.
    question: What if I need different prefixes per case?
  - answer: 'Aspose.Pdf offers a 30‑day trial. For production use you’ll need a license,
      but the API surface remains identical. --- ## Conclusion We’ve just covered
      **how to add bates numbering** to any PDF using Aspose.Pdf, demonstrated how
      to **add bates numbers pdf** in a clean, repeatable fashion, and showed'
    question: Is the library free?
  type: FAQPage
tags:
- Aspose.Pdf
- Bates numbering
- PDF automation
title: Πώς να προσθέσετε αρίθμηση Bates σε PDF με το Aspose – Οδηγός βήμα‑προς‑βήμα
url: /el/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-aspose-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Προσθέσετε Αρίθμηση Bates σε PDF με το Aspose – Οδηγός Βήμα‑Βήμα

Έχετε αναρωτηθεί **πώς να προσθέσετε αρίθμηση bates** σε ένα νομικό έγγραφο χωρίς να ξοδέψετε ώρες σε γραφικό περιβάλλον; Δεν είστε οι μόνοι. Σε πολλά δικηγορικά γραφεία, κυβερνητικούς οργανισμούς και ακόμη και μεγάλες επιχειρήσεις, η σήμανση κάθε σελίδας με ένα μοναδικό αναγνωριστικό είναι καθημερινή εργασία—και όμως μια μόνο γραμμή C# μπορεί να το κάνει παιχνιδάκι.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει ακριβώς **πώς να προσθέσετε αρίθμηση bates** χρησιμοποιώντας τη βιβλιοθήκη Aspose.Pdf. Στο τέλος θα ξέρετε επίσης πώς να **προσθέσετε bates numbers pdf** σε αρχεία και **να προσθέσετε σφραγίδα σε κάθε σελίδα** με λίγες μόνο γραμμές κώδικα. Χωρίς μαγεία, μόνο σαφής λογική και πρακτικές συμβουλές.

## Τι Θα Μάθετε

- Φόρτωση υπάρχοντος PDF με Aspose.Pdf.  
- Δημιουργία ενός `BatesNumberingStamp` και προσαρμογή της εμφάνισής του.  
- Επανάληψη σε κάθε σελίδα και **προσθήκη σφραγίδας σε κάθε σελίδα** αυτόματα.  
- Αποθήκευση του αποτελέσματος ως νέο PDF που φέρει επαγγελματική αρίθμηση Bates σε κάθε φύλλο.

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
- Έγκυρη άδεια Aspose.Pdf for .NET (ή προσωρινό κλειδί αξιολόγησης).  
- Ένα αρχικό αρχείο PDF που θέλετε να αριθμήσετε (θα το ονομάσουμε `Original.pdf`).

Αν έχετε αυτά τα τρία στοιχεία, είστε έτοιμοι να ξεκινήσετε.

---

## Βήμα 1: Ρυθμίστε το Έργο σας και Εγκαταστήστε το Aspose.Pdf

Πρώτα, δημιουργήστε ένα νέο έργο console (ή προσθέστε τον κώδικα σε υπάρχον). Στη συνέχεια, προσθέστε το πακέτο NuGet:

```bash
dotnet add package Aspose.Pdf
```

> **Συμβουλή:** Αν εργάζεστε σε εταιρικό δίκτυο, βεβαιωθείτε ότι η πηγή NuGet είναι ρυθμισμένη ώστε να φτάνει στο `https://www.nuget.org`.

## Βήμα 2: Φορτώστε το Πηγαίο PDF Έγγραφο

Η φόρτωση ενός PDF είναι τόσο απλή όσο το να δείξετε στο Aspose το μονοπάτι του αρχείου. Η κλάση `Document` αντιπροσωπεύει ολόκληρο το αρχείο.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF (replace the path with your own)
var document = new Document(@"C:\Temp\Original.pdf");

// Quick sanity check – how many pages are we dealing with?
Console.WriteLine($"Document contains {document.Pages.Count} pages.");
```

Γιατί καταγράφουμε τον αριθμό σελίδων; Επειδή η αρίθμηση Bates πρέπει να είναι διαδοχική σε *όλες* τις σελίδες, και είναι καλό να επαληθεύετε ότι δεν φορτώνετε κατά λάθος διαφορετικό αρχείο.

## Βήμα 3: Δημιουργήστε μια Σφραγίδα Αρίθμησης Bates

Η καρδιά της λειτουργίας είναι το `BatesNumberingStamp`. Σας επιτρέπει να ορίσετε πρόθεμα, διαχωριστικό, πλήθος ψηφίων και ακόμη και αν η σφραγίδα πρέπει να θεωρείται *artifact* (δηλαδή αόρατη στα εργαλεία εξαγωγής κειμένου).

```csharp
var batesStamp = new BatesNumberingStamp
{
    // Starting number – change this to whatever your workflow requires
    StartingNumber = 1000,

    // A human‑readable prefix, often a case or project code
    Prefix = "ABC-",

    // Separator between the running number and the total page count
    Separator = "/",

    // Pad the number with leading zeros to a fixed width (5 digits here)
    NumberOfDigits = 5,

    // Mark the stamp as an artifact so it won’t be indexed by search
    Artifact = true
};
```

**Γιατί αυτές οι ρυθμίσεις;**  
- `StartingNumber = 1000` προσομοιώνει ένα τυπικό νομικό δίκτυο που έχει ήδη ένα απόθεμα.  
- `NumberOfDigits = 5` εγγυάται ότι αριθμοί όπως `01000`, `01001` κ.λπ., ευθυγραμμίζονται όμορφα.  
- `Artifact = true` είναι απαραίτητο όταν το PDF θα περάσει σε OCR ή pipelines e‑discovery· οι αριθμοί παραμένουν ορατοί στους ανθρώπους αλλά αγνοούνται από τις μηχανές αναζήτησης κειμένου.

## Βήμα 4: Προσθέστε τη Σφραγίδα σε Κάθε Σελίδα

Τώρα επαναλαμβάνουμε το `document.Pages` και εφαρμόζουμε την ίδια σφραγίδα σε κάθε σελίδα. Το Aspose αυξάνει αυτόματα τον αριθμό για εσάς.

```csharp
foreach (Page page in document.Pages)
{
    // The AddStamp method clones the stamp for the current page,
    // updates the running number, and positions it at the default location.
    page.AddStamp(batesStamp);
}
```

> **Συχνή ερώτηση:** *Μπορώ να ελέγξω πού εμφανίζεται η σφραγίδα;*  
> Απόλυτα. Το `BatesNumberingStamp` κληρονομεί από το `Stamp`, οπότε μπορείτε να ορίσετε ιδιότητες όπως `HorizontalAlignment`, `VerticalAlignment`, `XIndent` και `YIndent` πριν από τη βρόχο. Για συντομία θα μείνουμε στην προεπιλεγμένη γωνία κάτω‑δεξιά.

## Βήμα 5: Αποθηκεύστε το Τροποποιημένο PDF

Τέλος, αποθηκεύστε τις αλλαγές. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή να γράψετε σε νέα θέση—εδώ θα κρατήσουμε και τα δύο αντίγραφα.

```csharp
// Save the new PDF with Bates numbers
document.Save(@"C:\Temp\BatesNumbered.pdf");

// Inform the user
Console.WriteLine("Bates numbering added successfully!");
```

Όταν ανοίξετε το `BatesNumbered.pdf`, κάθε σελίδα θα εμφανίζει μια σφραγίδα παρόμοια με:

```
ABC-01000/00123
ABC-01001/00123
…
ABC-01122/00123
```

όπου το `00123` είναι ο συνολικός αριθμός σελίδων, και το πρόθεμα `ABC-` παραμένει σταθερό.

---

## Πλήρες Παράδειγμα Εργασίας

Αντιγράψτε ολόκληρο το παρακάτω μπλοκ σε ένα νέο αρχείο `Program.cs` και τρέξτε το. Προσαρμόστε τα μονοπάτια αρχείων ώστε να ταιριάζουν με το περιβάλλον σας.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source PDF
            var srcPath = @"C:\Temp\Original.pdf";
            var document = new Document(srcPath);
            Console.WriteLine($"Loaded '{srcPath}' with {document.Pages.Count} pages.");

            // 2️⃣ Configure the Bates numbering stamp
            var batesStamp = new BatesNumberingStamp
            {
                StartingNumber = 1000,
                Prefix = "ABC-",
                Separator = "/",
                NumberOfDigits = 5,
                Artifact = true,
                // Optional: change alignment if you need a different location
                // HorizontalAlignment = HorizontalAlignment.Left,
                // VerticalAlignment = VerticalAlignment.Top,
                // XIndent = 20,
                // YIndent = 20
            };

            // 3️⃣ Apply the stamp to every page
            foreach (Page page in document.Pages)
            {
                page.AddStamp(batesStamp);
            }

            // 4️⃣ Save the new PDF
            var outPath = @"C:\Temp\BatesNumbered.pdf";
            document.Save(outPath);
            Console.WriteLine($"Saved Bates‑numbered PDF to '{outPath}'.");
        }
    }
}
```

**Αναμενόμενη έξοδος στην κονσόλα:**

```
Loaded 'C:\Temp\Original.pdf' with 12 pages.
Saved Bates-numbered PDF to 'C:\Temp\BatesNumbered.pdf'.
```

Ανοίξτε το αποθηκευμένο αρχείο και θα δείτε τους διαδοχικούς αριθμούς σε κάθε σελίδα—ακριβώς αυτό που περιμένατε όταν **προσθέτετε bates numbers pdf**.

---

## Προχωρημένες Ρυθμίσεις (Προαιρετικά)

| Στόχος | Πώς να το επιτύχετε |
|------|-------------------|
| **Αλλαγή χρώματος σφραγίδας** | Ορίστε `batesStamp.Color = Color.FromRgb(255, 0, 0);` πριν από τη βρόχο. |
| **Τοποθέτηση σφραγίδας στην κεφαλίδα** | Προσαρμόστε τις ιδιότητες `HorizontalAlignment` και `VerticalAlignment` όπως φαίνεται στον σχολιασμένο κώδικα. |
| **Παράλειψη ορισμένων σελίδων** | Προσθέστε μια συνθήκη `if (page.Number % 2 == 0) continue;` μέσα στο `foreach`. |
| **Χρήση προσαρμοσμένης γραμματοσειράς** | Αναθέστε `batesStamp.Font = FontRepository.FindFont("Arial");`. |
| **Κάντε τη σφραγίδα ορατή στο OCR** | Ορίστε `Artifact = false`. |

Αυτές οι παραλλαγές σας επιτρέπουν να **προσθέσετε σφραγίδα σε κάθε σελίδα** διατηρώντας ταυτόχρονα τον βασικό κώδικα καθαρό.

---

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό με PDF που έχουν προστασία κωδικού;**  
Α: Ναι. Φορτώστε το έγγραφο με ένα αντικείμενο `PdfLoadOptions` που παρέχει τον κωδικό, και συνεχίστε όπως φαίνεται.

**Ε: Τι γίνεται αν χρειαστώ διαφορετικά προθέματα ανά υπόθεση;**  
Α: Δημιουργήστε πολλαπλά αντικείμενα `BatesNumberingStamp`, ρυθμίστε το `Prefix` του καθενός και εφαρμόστε τα μόνο στις αντίστοιχες περιοχές σελίδων.

**Ε: Είναι η βιβλιοθήκη δωρεάν;**  
Α: Το Aspose.Pdf προσφέρει δοκιμαστική έκδοση 30 ημερών. Για παραγωγική χρήση θα χρειαστεί άδεια, αλλά η διεπαφή API παραμένει η ίδια.

---

## Συμπέρασμα

Συνοψίσαμε **πώς να προσθέσετε αρίθμηση bates** σε οποιοδήποτε PDF χρησιμοποιώντας το Aspose.Pdf, δείξαμε πώς να **προσθέσετε bates numbers pdf** με καθαρό, επαναχρησιμοποιήσιμο τρόπο, και παρουσιάσαμε τον πιο απλό τρόπο για **προσθήκη σφραγίδας σε κάθε σελίδα** με έναν μόνο βρόχο. Ο κώδικας είναι πλήρως αυτόνομος, εκτελείται σε δευτερόλεπτα, και μπορεί να ενσωματωθεί σε μεγαλύτερα pipelines επεξεργασίας εγγράφων χωρίς τροποποιήσεις.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να δημιουργήσετε μια εξώφυλλο που να αναφέρει το εύρος Bates, ή να ενσωματώσετε QR code δίπλα σε κάθε σφραγίδα. Οι δυνατότητες είναι ατελείωτες, και το ίδιο μοτίβο που μάθατε σήμερα θα σας εξυπηρετήσει όπου και αν χρειαστεί να αυτοματοποιήσετε μεταδεδομένα PDF.

Αν βρήκατε αυτόν τον οδηγό χρήσιμο, μοιραστείτε τον, αφήστε ένα σχόλιο ή εξερευνήστε τα άλλα tutorials μας για συγχώνευση PDF, υδατογράφημα και ψηφιακές υπογραφές. Καλή προγραμματιστική δουλειά!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [How to Add Page Stamps in PDFs Using Aspose.PDF for .NET&#58; A Complete Guide](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}