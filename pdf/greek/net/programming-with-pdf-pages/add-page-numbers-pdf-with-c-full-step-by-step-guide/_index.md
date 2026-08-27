---
category: general
date: 2026-01-02
description: Προσθέστε γρήγορα αριθμούς σελίδων σε PDF χρησιμοποιώντας το Aspose.Pdf
  σε C#. Μάθετε πώς να προσθέτετε αρίθμηση Bates, κείμενο υποσέλιδου, προσαρμοσμένο
  υδατογράφημα και να επαναλαμβάνετε τις σελίδες PDF σε ένα ενιαίο σενάριο.
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: el
og_description: Προσθέστε αμέσως αριθμούς σελίδων σε PDF με το Aspose.Pdf. Αυτός ο
  οδηγός καλύπτει επίσης την προσθήκη αρίθμησης Bates, κειμένου υποσέλιδου, προσαρμοσμένου
  υδατογραφήματος και την επανάληψη σελίδων PDF.
og_title: Προσθήκη αριθμών σελίδων PDF με C# – Πλήρες Μάθημα Προγραμματισμού
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: Προσθήκη αριθμών σελίδων σε PDF με C# – Πλήρης οδηγός βήμα‑βήμα
url: /el/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη αριθμών σελίδας pdf με C# – Πλήρες Πρόγραμμα Εκμάθησης

Κάποτε χρειάστηκε να **προσθέσετε αριθμούς σελίδας pdf** αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε οι μόνοι—οι προγραμματιστές ρωτούν συνεχώς πώς να σφραγίζουν αριθμούς, υποσέλιδα ή ακόμη και έναν αναγνωριστικό τύπου Bates σε κάθε σελίδα ενός PDF.  

Σε αυτό το tutorial θα δείτε ένα έτοιμο παράδειγμα C# που **διασχίζει τις σελίδες pdf**, προσθέτει ένα υποσέλιδο με αριθμό σελίδας και (αν το επιθυμείτε) προσθέτει ένα προσαρμοσμένο υδατογράφημα. Θα σας δείξουμε επίσης πώς να αλλάξετε τη σφραγίδα σε αριθμό Bates, που είναι απλώς ένας κομψός τρόπος να πείτε «προσθήκη αρίθμησης Bates» για νομικά ή εγκληματολογικά έγγραφα. Στο τέλος, θα έχετε μια ενιαία, επαναχρησιμοποιήσιμη μέθοδο που διαχειρίζεται όλες αυτές τις εργασίες χωρίς κόπο.

## Προσθήκη αριθμών σελίδας pdf – Επισκόπηση

Πριν βουτήξουμε στον κώδικα, ας διευκρινίσουμε τι σημαίνει πραγματικά “προσθήκη αριθμών σελίδας pdf” στον κόσμο του Aspose.Pdf. Η βιβλιοθήκη αντιμετωπίζει οποιοδήποτε κομμάτι κειμένου τοποθετείτε σε μια σελίδα ως **TextStamp**. Δημιουργώντας μια σφραγίδα με έναν αντικαταστάτη σελίδας (`{page}`) και εφαρμόζοντάς την σε κάθε σελίδα, παίρνετε αυτόματα διαδοχική αρίθμηση. Η ίδια σφραγίδα μπορεί να περιέχει επιπλέον κείμενο, ώστε να μπορείτε να **προσθέσετε κείμενο υποσέλιδου** όπως “Confidential” ή έναν ειδικό αναγνωριστικό.

> **Γιατί να χρησιμοποιήσετε σφραγίδα αντί για επεξεργασία του ρεύματος περιεχομένου PDF;**  
> Οι σφραγίδες είναι αντικείμενα υψηλού επιπέδου που σέβονται τα περιθώρια της σελίδας, την περιστροφή και τα υπάρχοντα γραφικά. Είναι επίσης πολύ πιο εύκολο να τις συντηρείτε—απλώς αλλάζετε μερικές ιδιότητες και ξανατρέχετε το script.

## Διασχίστε τις σελίδες PDF για να εφαρμόσετε σφραγίδες

Το πρώτο πρακτικό βήμα είναι να ανοίξετε το πηγαίο PDF και να επαναλάβετε τις σελίδες του. Αυτό είναι το κλασικό πρότυπο **loop through pdf pages** που χρησιμοποιούν τα περισσότερα παραδείγματα Aspose.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **Συμβουλή:** Αν το PDF σας είναι τεράστιο (εκατοντάδες σελίδες), σκεφτείτε να το επεξεργάζεστε σε παρτίδες για να κρατήσετε τη χρήση μνήμης χαμηλή. Το Aspose.Pdf διαβάζει τις σελίδες αργά, οπότε ο βρόχος είναι ήδη αρκετά αποδοτικός.

## Προσθήκη αρίθμησης Bates και κειμένου υποσέλιδου

Τώρα που μπορούμε να περάσουμε από κάθε σελίδα, ας δημιουργήσουμε μια **επαναχρησιμοποιήσιμη TextStamp** που μεταφέρει τόσο τον αριθμό σελίδας όσο και το προαιρετικό κείμενο υποσέλιδου. Ο αντικαταστάτης `{page}` αντικαθίσταται αυτόματα με τον τρέχοντα αριθμό σελίδας.

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### Γιατί λειτουργεί αυτό

* **`Bates-{page}`** – Το Aspose αντικαθιστά το `{page}` με τον πραγματικό αριθμό σελίδας, παρέχοντάς σας αυτόματα έναν κλασικό αριθμό Bates.
* **`Confidential`** – Αυτό είναι το τμήμα **add footer text**. Μπορείτε να το αντικαταστήσετε με οποιοδήποτε κείμενο, ακόμη και να αντλήσετε δεδομένα από βάση.
* **Στυλ** – Χρησιμοποιώντας το `TextState` μπορείτε να ρυθμίσετε χρώμα, διαφάνεια και ακόμη περιστροφή χωρίς να αγγίζετε τα εσωτερικά ρεύματα περιεχομένου του PDF.

Αν χρειάζεστε μόνο απλούς αριθμούς, αφαιρέστε το πρόθεμα “Bates‑” και το επιπλέον κείμενο:

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Προσθήκη προσαρμοσμένου υδατογραφήματος (προαιρετικό)

Μερικές φορές θέλετε κάτι παραπάνω από ένα υποσέλιδο—χρειάζεστε ένα ημιδιαφανές λογότυπο ή μια επικάλυψη “DRAFT” σε όλη τη σελίδα. Εδώ έρχεται το **add custom watermark**. Η ίδια κλάση `TextStamp` μπορεί να επαναχρησιμοποιηθεί, απλώς αλλάξτε την ευθυγράμμιση και τη διαφάνεια.

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **Σημείωση:** Η σειρά έχει σημασία. Προσθέτοντας πρώτα το υδατογράφημα εξασφαλίζετε ότι οι αριθμοί σελίδας παραμένουν αναγνώσιμοι πάνω από το ημιδιαφανές κείμενο.

## Αποθήκευση του PDF και επαλήθευση αποτελεσμάτων

Μετά τη σφράγιση, το τελευταίο βήμα είναι να γράψετε τις αλλαγές πίσω στο δίσκο. Η κλήση `Save` που τοποθετήσαμε νωρίτερα κάνει το σκληρό έργο, αλλά ας προσθέσουμε ένα γρήγορο απόσπασμα επαλήθευσης που ανοίγει το νέο αρχείο και εκτυπώνει πόσες σελίδες επεξεργάστηκαν.

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

Όταν τρέξετε το πλήρες πρόγραμμα, θα πρέπει να δείτε ένα PDF όπου κάθε σελίδα τελειώνει με κάτι όπως **“Bates‑3 – Confidential”** (ή απλώς “3” αν χρησιμοποιήσατε τη απλή σφραγίδα) και, αν ενεργοποιήσατε το υδατογράφημα, ένα αχνό “DRAFT” στο κέντρο.

### Αναμενόμενο αποτέλεσμα

| Σελίδα | Υποσέλιδο (παράδειγμα) |
|--------|------------------------|
| 1      | Bates‑1 – Confidential |
| 2      | Bates‑2 – Confidential |
| …      | … |
| N      | Bates‑N – Confidential |

Αν ανοίξετε το αρχείο σε προβολέα, οι αριθμοί θα βρίσκονται 20 pts από τα αριστερά και κάτω περιθώρια, σύμφωνα με τις τυπικές νομικές συμβάσεις.

## Πλήρες λειτουργικό παράδειγμα (έτοιμο για αντιγραφή‑επικόλληση)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

Αποθηκεύστε το ως `AddPageNumbers.cs`, επαναφέρετε το πακέτο NuGet Aspose.Pdf (`Install-Package Aspose.Pdf`) και τρέξτε το. Θα πάρετε ένα **add page numbers pdf** αρχείο που επίσης δείχνει **add bates numbering**, **add footer text**, **add custom watermark**, και το κλασικό **loop through pdf pages** πρότυπο—όλα σε ένα καθαρό script.

![add page numbers pdf example](https://example.com/images/add-page-numbers-pdf.png "Στιγμιότυπο που δείχνει αριθμημένες σελίδες PDF με υποσέλιδο και υδατογράφημα")

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **προσθέσετε αριθμούς σελίδας pdf** χρησιμοποιώντας το Aspose.Pdf σε C#. Από τη διασχίση κάθε σελίδας, στη σφράγιση αριθμών Bates, στην προσθήκη προσαρμοσμένου κειμένου υποσέλιδου, και ακόμη στην τοποθέτηση ημιδιαφανούς υδατογραφήματος, ο κώδικας είναι αρκετά συμπαγής ώστε να ενσωματωθεί σε οποιοδήποτε υπάρχον έργο.  

Στη συνέχεια, ίσως θελήσετε να εξερευνήσετε πιο προχωρημένα σενάρια—όπως η λήψη του κειμένου υποσέλιδου από βάση δεδομένων, η εφαρμογή διαφορετικών γραμματοσειρών ανά ενότητα, ή η δημιουργία ξεχωριστού PDF ευρετηρίου που καταγράφει όλους τους αριθμούς Bates. Όλες αυτές οι επεκτάσεις βασίζονται στις ίδιες βασικές ιδέες που παρουσιάσαμε, οπότε είστε έτοιμοι να επεκτείνετε τη λύση καθώς αυξάνονται οι απαιτήσεις σας.  

Δοκιμάστε το, προσαρμόστε το στυλ, και ενημερώστε μας στα σχόλια πώς σας φάνηκε. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}