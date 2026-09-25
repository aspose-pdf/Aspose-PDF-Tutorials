---
category: general
date: 2026-03-19
description: Προσθέστε σφραγίδα σε PDF στην πρώτη σελίδα και εφαρμόστε υδατογράφημα
  PDF χρησιμοποιώντας το Aspose.Pdf σε C#. Μάθετε πώς να προσθέσετε σημείωση σε PDF
  και δείτε ένα πλήρες λειτουργικό παράδειγμα.
draft: false
keywords:
- add stamp to pdf
- apply watermark pdf
- add note to pdf
- how to add stamp
- add stamp first page
language: el
og_description: Προσθέστε σφραγίδα σε PDF στην πρώτη σελίδα και εφαρμόστε υδατογράφημα
  PDF χρησιμοποιώντας το Aspose.Pdf σε C#. Πλήρης οδηγός βήμα προς βήμα.
og_title: Προσθήκη Σφραγίδας σε PDF – Εφαρμογή Υδατογραφήματος PDF στην Πρώτη Σελίδα
tags:
- aspnet
- csharp
- pdf
- aspose
title: Προσθήκη Σφραγίδας σε PDF – Εφαρμογή Υδατογραφήματος PDF στην Πρώτη Σελίδα
url: /el/net/programming-with-stamps-and-watermarks/add-stamp-to-pdf-apply-watermark-pdf-on-first-page/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Σφραγίδας σε PDF – Εφαρμογή Υδατογραφήματος PDF στην Πρώτη Σελίδα

Έχετε χρειαστεί ποτέ να **προσθέσετε σφραγίδα σε PDF** αλλά δεν ήξερατε από πού να ξεκινήσετε; Ίσως θέλετε επίσης να **εφαρμόσετε υδατογράφημα PDF** στην ίδια σελίδα, ή απλώς να προσθέσετε μια γρήγορη **προσθήκη σημείωσης σε PDF** για τους ελεγκτές. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα C# που κάνει ακριβώς αυτό, και θα εξηγήσουμε το «γιατί» πίσω από κάθε γραμμή ώστε να το προσαρμόσετε σε οποιοδήποτε σενάριο.

Θα καλύψουμε τα πάντα, από τη φόρτωση του πηγαίου εγγράφου μέχρι την αποθήκευση της έκδοσης με σφραγίδα, καθώς και μερικές συμβουλές για τη διαχείριση πολυ‑σελιδών PDF, προβλήματα κλιμάκωσης και προσαρμογή της εμφάνισης της σφραγίδας. Στο τέλος θα μπορείτε να απαντήσετε με σιγουριά στην ερώτηση «**πώς να προσθέσετε σφραγίδα**;» και να ξέρετε πώς να **προσθέσετε σφραγίδα στην πρώτη σελίδα** χωρίς καμία δυσκολία.

---

## Τι Θα Χρειαστείτε

- **Aspose.Pdf for .NET** (οποιαδήποτε πρόσφατη έκδοση, π.χ. 23.10) – η βιβλιοθήκη που κάνει την επεξεργασία PDF απλή.  
- Ένα περιβάλλον ανάπτυξης .NET (Visual Studio, VS Code, Rider – ό,τι προτιμάτε).  
- Ένα αρχείο PDF εισόδου (θα το ονομάσουμε `input.pdf`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε.  

Δεν απαιτούνται επιπλέον πακέτα NuGet πέρα από το Aspose.Pdf, και ο κώδικας λειτουργεί σε .NET 6+ καθώς και σε .NET Framework 4.7.2.

---

![Add stamp to PDF example](/images/add-stamp-to-pdf.png "Screenshot showing a PDF with a text stamp – add stamp to pdf")

*Alt text: add stamp to pdf – visual example of a text stamp applied to the first page of a PDF.*

---

## Βήμα 1 – Φόρτωση του Πηγαίου Εγγράφου PDF

Για να **προσθέσετε σφραγίδα σε PDF**, χρειάζεται πρώτα μια αναπαράσταση του αρχείου στη μνήμη. Η κλάση `Aspose.Pdf.Document` κάνει το βαριά δουλειά.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class PdfStampDemo
{
    static void Main()
    {
        // Load the original PDF (replace YOUR_DIRECTORY with your actual path)
        var pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);
```

**Γιατί είναι σημαντικό:**  
`Document` αναλύει τη δομή του αρχείου, δίνοντάς σας πρόσβαση σε σελίδες, σημειώσεις και πόρους. Η χρήση ενός μπλοκ `using` εξασφαλίζει ότι το χειριστήριο του αρχείου απελευθερώνεται άμεσα — κάτι κρίσιμο όταν αργότερα προσπαθήσετε να αντικαταστήσετε το ίδιο αρχείο.

---

## Βήμα 2 – Δημιουργία και Διαμόρφωση της Σφραγίδας Κειμένου

Τώρα θα **προσθέσουμε σημείωση σε PDF** δημιουργώντας ένα `TextStamp`. Αυτό το αντικείμενο συμπεριφέρεται όπως ένα υδατογράφημα, αλλά μπορείτε να ελέγξετε το μέγεθος, τη γραμματοσειρά και τη συσπείρωση κειμένου.

```csharp
        // Step 2: Create a text stamp that will serve as a note/watermark
        var textStamp = new TextStamp("Important note")
        {
            // Auto‑adjust font size so the text fits inside the stamp rectangle
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,

            // Wrap words rather than breaking them mid‑word
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,

            // Define the stamp rectangle (you can tweak these values)
            Width = 400,
            Height = 200,

            // Turn off scaling – we want the stamp to keep its exact size
            Scale = false
        };
```

**Βασικά σημεία που πρέπει να θυμάστε:**

- `AutoAdjustFontSizeToFitStampRectangle` επιτρέπει στη σφραγίδα να μικραίνει ή να μεγαλώνει ώστε το κείμενο να μην υπερβαίνει τα όρια – χρήσιμο όταν **εφαρμόζετε υδατογράφημα PDF** σε διαφορετικά μεγέθη σελίδας.  
- `WordWrapMode.ByWords` εξασφαλίζει ότι το κείμενο σπάει στις λέξεις, κάνοντας τη σημείωση ευανάγνωστη.  
- Ορίζοντας `Scale = false` αποτρέπει την τέντωμα της σφραγίδας αν αλλάξει το DPI της σελίδας.

---

## Βήμα 3 – Επισύναψη της Σφραγίδας στην Πρώτη Σελίδα

Αν αναρωτιέστε **πώς να προσθέσετε σφραγίδα** συγκεκριμένα στην πρώτη σελίδα, αυτό είναι το σημείο. Η συλλογή `Pages` είναι 1‑βασισμένη, έτσι `Pages[1]` είναι η πρώτη σελίδα.

```csharp
        // Step 3: Add the configured stamp to the first page
        pdfDocument.Pages[1].AddStamp(textStamp);
```

**Γιατί η πρώτη σελίδα;**  
Πολλές νομικές ή εμπορικές απαιτήσεις ζητούν ένα ορατό υδατογράφημα μόνο στην εξώφυλλο. Στοχεύοντας το `Pages[1]` ικανοποιούμε το σενάριο **προσθήκη σφραγίδας στην πρώτη σελίδα** χωρίς να χρειάζεται βρόχος σε ολόκληρο το έγγραφο.

---

## Βήμα 4 – Αποθήκευση του Τροποποιημένου PDF

Τέλος, γράψτε τις αλλαγές πίσω στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή να δημιουργήσετε νέο; Εδώ θα δημιουργήσουμε το `Stamped.pdf`.

```csharp
        // Step 4: Save the stamped PDF
        var outputPath = @"YOUR_DIRECTORY\Stamped.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Stamp added successfully! Output saved to {outputPath}");
    }
}
```

Η εκτέλεση του προγράμματος θα παραγάγει ένα PDF όπου η πρώτη σελίδα εμφανίζει τη σφραγίδα «Important note», επιτυγχάνοντας έτσι **προσθήκη σφραγίδας σε pdf** και επίσης **εφαρμογή υδατογραφήματος pdf** σε μία ενέργεια.

---

## Προαιρετικό: Ρύθμιση της Σφραγίδας για Διάφορα Σενάρια

### Πολλαπλές Σελίδες

Αν αργότερα αποφασίσετε ότι χρειάζεστε την ίδια σημείωση σε *κάθε* σελίδα, αντικαταστήστε τη γραμμή μιας σελίδας με βρόχο:

```csharp
foreach (var page in pdfDocument.Pages)
{
    page.AddStamp(textStamp);
}
```

### Σφραγίδες Εικόνας

Το Aspose υποστηρίζει επίσης `ImageStamp` αν προτιμάτε λογότυπο αντί για κείμενο. Οι ίδιες ιδιότητες (μέγεθος, θέση, κλιμάκωση) ισχύουν.

### Τοποθέτηση της Σφραγίδας

Από προεπιλογή η σφραγίδα εμφανίζεται στην επάνω‑αριστερή γωνία του ορθογωνίου. Για να τη μετακινήσετε, ορίστε `HorizontalAlignment` και `VerticalAlignment`:

```csharp
textStamp.HorizontalAlignment = HorizontalAlignment.Center;
textStamp.VerticalAlignment = VerticalAlignment.Middle;
```

---

## Συνηθισμένα Πάγια & Επαγγελματικές Συμβουλές

- **Κλειδώματα αρχείων:** Αν λάβετε `IOException` που λέει ότι το αρχείο είναι σε χρήση, βεβαιωθείτε ότι καμία άλλη διεργασία (συμπεριλαμβανομένου του Explorer) δεν έχει ανοιχτό το PDF. Το μπλοκ `using` βοηθά, αλλά ελέγξτε ξανά.  
- **Προβλήματα γραμματοσειράς:** Το Aspose χρησιμοποιεί τις συστημικές γραμματοσειρές από προεπιλογή. Για μη‑λατινικά αλφάβητα, ενσωματώστε τη ζητούμενη γραμματοσειρά ή ορίστε ρητά το `textStamp.Font`.  
- **Μεγάλα PDF:** Για PDF άνω των 100 MB, σκεφτείτε να καλέσετε `pdfDocument.Optimize()` πριν την αποθήκευση για μείωση του μεγέθους.  
- **Δοκιμές:** Ανοίξτε το παραγόμενο `Stamped.pdf` σε πολλαπλούς προβολείς (Adobe Reader, Edge, Chrome) για να βεβαιωθείτε ότι η σφραγίδα αποδίδεται ομοιόμορφα.  

---

## Πλήρες Παράδειγμα Εργασίας (Αντιγραφή‑Επικόλληση)

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class PdfStampDemo
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var pdfPath = @"YOUR_DIRECTORY\input.pdf";
        using var pdfDocument = new Document(pdfPath);

        // 2️⃣ Create a configurable text stamp (our note/watermark)
        var textStamp = new TextStamp("Important note")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            AutoAdjustFontSizePrecision = 0.01f,
            WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
            Width = 400,
            Height = 200,
            Scale = false,
            HorizontalAlignment = HorizontalAlignment.Center,
            VerticalAlignment = VerticalAlignment.Middle
        };

        // 3️⃣ Add the stamp to the first page (add stamp first page)
        pdfDocument.Pages[1].AddStamp(textStamp);

        // 4️⃣ Save the stamped PDF
        var outputPath = @"YOUR_DIRECTORY\Stamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"Stamp added successfully! Output saved to {outputPath}");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Ανοίξτε το `Stamped.pdf`; η πρώτη σελίδα δείχνει ένα κεντραρισμένο πλαίσιο «Important note» διαστάσεων 400 × 200 points, με το κείμενο αυτόματα προσαρμοσμένο ώστε να χωράει. Όλες οι άλλες σελίδες παραμένουν αμετάβλητες.

---

## Συμπέρασμα

Δείξαμε πώς να **προσθέσετε σφραγίδα σε pdf** και **εφαρμόσετε υδατογράφημα pdf** με έναν καθαρό, επαναχρησιμοποιήσιμο τρόπο. Φορτώνοντας το έγγραφο, διαμορφώνοντας ένα `TextStamp`, συνδέοντάς το με το **προσθήκη σφραγίδας στην πρώτη σελίδα**, και αποθηκεύοντας, λαμβάνετε μια επαγγελματική σημείωση χωρίς να ασχολείστε με χαμηλού επιπέδου ροές PDF.

Από εδώ μπορείτε να εξερευνήσετε την προσθήκη σφραγίδων σε κάθε σελίδα, την αντικατάσταση με εικόνες, ή ακόμη και τη στοίβαξη πολλαπλών σφραγίδων για σύνθετο branding. Το ίδιο μοτίβο — δημιουργία, διαμόρφωση, επισύναψη, αποθήκευση — ισχύει για τις περισσότερες εργασίες Aspose.Pdf, οπότε θα βρείτε εύκολο το να το επεκτείνετε.

Έχετε διαφορετική περίπτωση χρήσης, όπως σφράγιση ετικέτας «confidential» σε δεκάδες PDF σε μια παρτίδα; Δοκιμάστε να τυλίξετε τη λογική παραπάνω σε ένα `foreach` που διατρέχει έναν φάκελο αρχείων. Ή, αν χρειάζεστε **προσθήκη σημείωσης σε pdf** υπό όρους βάσει του περιεχομένου της σελίδας, ρίξτε μια ματιά στο `TextFragmentAbsorber` του Aspose για αναζήτηση κειμένου πριν τη σφράγιση.

Καλή προγραμματιστική δουλειά, και εύχομαι τα PDF σας να είναι πάντα σφραγισμένα ακριβώς όπως θέλετε! 

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}