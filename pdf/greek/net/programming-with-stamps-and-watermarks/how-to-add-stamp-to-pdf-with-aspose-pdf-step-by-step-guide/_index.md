---
category: general
date: 2026-03-24
description: Πώς να προσθέσετε σφραγίδα σε PDF χρησιμοποιώντας το Aspose.Pdf σε C#.
  Μάθετε πώς να τοποθετήσετε σφραγίδα PDF και να προσθέσετε σφραγίδα κειμένου PDF
  με αυτόματο μέγεθος σε λίγα εύκολα βήματα.
draft: false
keywords:
- how to add stamp
- place stamp pdf
- add text stamp pdf
- Aspose.Pdf stamp example
- C# PDF annotation
language: el
og_description: Πώς να προσθέσετε σφραγίδα σε PDF με C#; Αυτός ο οδηγός σας δείχνει
  πώς να τοποθετήσετε σφραγίδα PDF και να προσθέσετε σφραγίδα κειμένου PDF με αυτόματο
  μέγεθος γραμματοσειράς χρησιμοποιώντας το Aspose.Pdf.
og_title: Πώς να προσθέσετε σφραγίδα σε PDF με το Aspose.Pdf – Σύντομος οδηγός
tags:
- pdf
- csharp
- aspose
- stamping
title: Πώς να προσθέσετε σφραγίδα σε PDF με το Aspose.Pdf – Οδηγός βήμα‑προς‑βήμα
url: /el/net/programming-with-stamps-and-watermarks/how-to-add-stamp-to-pdf-with-aspose-pdf-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Προσθέσετε Σφραγίδα σε PDF με Aspose.Pdf – Οδηγός Βήμα‑Βήμα

**Πώς να προσθέσετε σφραγίδα** σε ένα PDF είναι μια συχνή ανάγκη όταν θέλετε να χρωματίσετε, πιστοποιήσετε ή απλώς να σχολιάσετε ένα έγγραφο. Αναρωτηθήκατε ποτέ ποιος είναι ο πιο εύκολος τρόπος να τοποθετήσετε μια σφραγίδα PDF χωρίς να ασχοληθείτε με χαμηλού επιπέδου γραφικά; Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πλήρη, έτοιμη προς εκτέλεση λύση που όχι μόνο δείχνει **πώς να προσθέσετε σφραγίδα**, αλλά εξηγεί επίσης *γιατί* κάθε γραμμή είναι σημαντική.

Θα μάθετε πώς να **τοποθετήσετε σφραγίδα PDF** σε οποιαδήποτε σελίδα, πώς να **προσθέσετε κείμενο σφραγίδας PDF** που αυτόματα μειώνεται ώστε να χωράει στο ορθογώνιο του, και ποιες παγίδες να αποφύγετε όταν το κείμενο είναι πολύ μακρύ. Στο τέλος θα έχετε ένα μόνο αρχείο C# που μπορείτε να προσθέσετε στο πρότζεκτ σας και να αρχίσετε να σφραγίζετε PDFs αμέσως.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework).
* Το πακέτο NuGet **Aspose.Pdf for .NET** (`Aspose.Pdf`) εγκατεστημένο.
* Ένα αρχείο PDF με όνομα `input.pdf` σε φάκελο που μπορείτε να αναφέρετε (οποιοδήποτε απλό PDF μίας σελίδας αρκεί).

Δεν απαιτείται καμία επιπλέον ρύθμιση—το Aspose.Pdf αναλαμβάνει όλη τη βαριά δουλειά.

## Βήμα 1: Ρύθμιση του Έργου και Φόρτωση του Πηγαίου PDF

Το πρώτο που χρειαζόμαστε είναι ένα αντικείμενο `Document` που αντιπροσωπεύει το PDF που θέλουμε να σχολιάσουμε. Σκεφτείτε το ως φόρτωση ενός κεννού καμβά, πάνω στον οποίο θα ζωγραφίσουμε τη σφραγίδα.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the source PDF document
// The using statement ensures the file is closed automatically.
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Γιατί είναι σημαντικό:** Το `Document` είναι το σημείο εισόδου για οποιαδήποτε επεξεργασία PDF στο Aspose.Pdf. Χρησιμοποιώντας το πρότυπο `using` εξασφαλίζουμε ότι το χειριστήριο του αρχείου απελευθερώνεται, αποτρέποντας προβλήματα κλειδώματος αρχείου όταν αργότερα προσπαθήσετε να αποθηκεύσετε το τροποποιημένο PDF.

## Βήμα 2: Δημιουργία Σφραγίδας Κειμένου με Αυτόματη Προσαρμογή Μεγέθους Γραμματοσειράς

Τώρα δημιουργούμε ένα `TextStamp`. Το κόλπο που κάνει αυτό το παράδειγμα ξεχωριστό είναι η σημαία `AutoAdjustFontSizeToFitStampRectangle`—αυτή λέει στο Aspose να μειώσει το κείμενο μέχρι να χωράει μέσα στο ορθογώνιο που ορίζουμε.

```csharp
// Create a text stamp that will automatically resize to fit its rectangle
var textStamp = new TextStamp("Long text that must fit")
{
    // Let Aspose shrink the text if it overflows
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Precision of the auto‑adjust algorithm (lower = more accurate)
    AutoAdjustFontSizePrecision = 0.01f,
    // Define the stamp's bounding box (in points)
    Width = 300,
    Height = 100,
    // Word‑wrap by whole words so we don’t split in the middle of a word
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
    // Optional: set background color or opacity if you want a visible box
    Background = new Background()
    {
        Color = Color.LightGray,
        Opacity = 0.5
    }
};
```

> **Συμβουλή επαγγελματία:** Αν χρειάζεστε λογότυπο ή εικόνα αντί για κείμενο, χρησιμοποιήστε `ImageStamp`—η ίδια λογική αυτόματης προσαρμογής υπάρχει και για την κλιμάκωση εικόνας.

## Βήμα 3: Επιλογή Τοποθεσίας για **Place Stamp PDF** – Πρώτη Σελίδα, Τελευταία Σελίδα ή Προσαρμοσμένος Δείκτης

Το Aspose.Pdf αποθηκεύει τις σελίδες σε μια συλλογή με βάση το 1 (`pdfDocument.Pages[1]` είναι η πρώτη σελίδα). Μπορείτε να **τοποθετήσετε σφραγίδα PDF** σε οποιαδήποτε σελίδα αλλάζοντας τον δείκτη.

```csharp
// Place the stamp on the first page (index 1)
// To stamp the last page use pdfDocument.Pages[pdfDocument.Pages.Count]
pdfDocument.Pages[1].AddStamp(textStamp);
```

> **Γιατί είναι ευέλικτο:** Επειδή η συλλογή `Pages` είναι μεταβλητή, μπορείτε να κάνετε βρόχο σε όλες τις σελίδες και να προσθέσετε την ίδια σφραγίδα σε κάθε μία, ή να στοχεύσετε μια συγκεκριμένη σελίδα βάσει επιχειρηματικής λογικής (π.χ. μόνο την εξώφυλλο).

## Βήμα 4: Αποθήκευση του Τροποποιημένου Εγγράφου

Μετά τη σφράγιση, πρέπει να γράψετε τις αλλαγές πίσω στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή να δημιουργήσετε ένα νέο—όπως προτιμάτε.

```csharp
// Save the stamped PDF – change the path if you don’t want to overwrite
pdfDocument.Save("YOUR_DIRECTORY/output-stamped.pdf");
```

Όταν ανοίξετε το `output-stamped.pdf` θα δείτε ένα ανοιχτό-γκρι ορθογώνιο στην πρώτη σελίδα που περιέχει το κείμενο “Long text that must fit”. Αν το κείμενο ήταν μεγαλύτερο, το Aspose θα το μειώσει αυτόματα μέχρι να χωράει τέλεια μέσα στο ορθογώνιο 300 × 100 pt.

## Πλήρες Παράδειγμα Λειτουργικού Κώδικα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε μια εφαρμογή κονσόλας (`Program.cs`). Περιλαμβάνει όλα τα τμήματα που συζητήσαμε, καθώς και έναν μικρό βοηθό για να επαληθεύσετε ότι η σφραγίδα εμφανίζεται.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;   // Needed for Background and Color

namespace PdfStampDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the source PDF
            using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

            // 2️⃣ Create a text stamp with auto‑adjusting font size
            var textStamp = new TextStamp("Long text that must fit")
            {
                AutoAdjustFontSizeToFitStampRectangle = true,
                AutoAdjustFontSizePrecision = 0.01f,
                Width = 300,
                Height = 100,
                WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
                Background = new Background()
                {
                    Color = Color.LightGray,
                    Opacity = 0.5
                }
            };

            // 3️⃣ Place the stamp on the first page (you can change the index)
            pdfDocument.Pages[1].AddStamp(textStamp);

            // 4️⃣ Save the result
            string outputPath = "YOUR_DIRECTORY/output-stamped.pdf";
            pdfDocument.Save(outputPath);

            Console.WriteLine($"Stamp added successfully! Check the file at: {outputPath}");
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

* Το PDF ανοίγει με ένα ημιδιαφανές γκρι κουτί στην πρώτη σελίδα.
* Μέσα στο κουτί το παρεχόμενο κείμενο ταιριάζει **τέλεια** (ακόμη και αν το αντικαταστήσετε με μια πιο μακριά πρόταση).
* Δεν απαιτούνται χειροκίνητοι υπολογισμοί μεγέθους γραμματοσειράς—το Aspose κάνει όλη τη βαριά δουλειά.

## Συνηθισμένες Παγίδες Όταν **Place Stamp PDF**

| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Το κείμενο κόβεται | `AutoAdjustFontSizeToFitStampRectangle` είναι **false** ή το ορθογώνιο είναι πολύ μικρό. | Ενεργοποιήστε τη σημαία και αυξήστε το `Width`/`Height` ή μειώστε το μήκος του κειμένου. |
| Η σφραγίδα εμφανίζεται εκτός κέντρου | Οι προεπιλεγμένες τιμές `HorizontalAlignment`/`VerticalAlignment` είναι `Left`/`Top`. | Ορίστε `HorizontalAlignment = HorizontalAlignment.Center` και `VerticalAlignment = VerticalAlignment.Center`. |
| Η σφραγίδα δεν είναι ορατή σε ορισμένους προβολείς | Η διαφάνεια φόντου είναι 0 ή το χρώμα της σφραγίδας ταιριάζει με το φόντο της σελίδας. | Χρησιμοποιήστε ένα αντιθετικό `Background.Color` ή ορίστε `Opacity` > 0.3. |
| Πολλές σφραγίδες επικαλύπτονται | Προσθήκη σφραγίδων σε βρόχο χωρίς προσαρμογή συντεταγμένων. | Χρησιμοποιήστε `textStamp.XIndent` και `textStamp.YIndent` για να μετατοπίσετε κάθε σφραγίδα. |

Η αντιμετώπιση αυτών των ζητημάτων νωρίς σας εξοικονομεί πολύ χρόνο εντοπισμού σφαλμάτων αργότερα.

## Επέκταση του Παραδείγματος: Προσθήκη Σφραγίδας Εικόνας

Αν χρειάζεστε **προσθήκη κειμένου σφραγίδας PDF** *και* μια εικόνα (π.χ. λογότυπο εταιρείας), μπορείτε να συνδυάσετε και τα δύο:

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    Width = 100,
    Height = 50,
    XIndent = 400,          // Position to the right of the text stamp
    YIndent = 20,
    Background = new Background()
    {
        Color = Color.Transparent
    }
};

pdfDocument.Pages[1].AddStamp(imageStamp);
```

Τώρα η σελίδα εμφανίζει τόσο μια δυναμική σφραγίδα κειμένου όσο και μια στατική σφραγίδα εικόνας δίπλα-δίπλα.

## Δοκιμή της Υλοποίησής Σας

1. Εκτελέστε την εφαρμογή κονσόλας.  
2. Ανοίξτε το `output-stamped.pdf` σε Adobe Reader, Edge ή οποιονδήποτε προβολέα PDF.  
3. Επαληθεύστε ότι το ορθογώνιο της σφραγίδας υπάρχει και το κείμενο είναι πλήρως ορατό.  
4. Αλλάξτε το κείμενο σε μια πιο μακριά φράση, ξανατρέξτε και επιβεβαιώστε ότι η γραμματοσειρά μειώνεται αυτόματα.

Αν κάτι φαίνεται λανθασμένο, ελέγξτε ξανά τις διαστάσεις του ορθογωνίου και τη ρύθμιση `AutoAdjustFontSizePrecision`.

## Συμπέρασμα

Τώρα ξέρετε **πώς να προσθέσετε σφραγίδα** σε PDF χρησιμοποιώντας Aspose.Pdf, πώς να **τοποθετήσετε σφραγίδα PDF** σε συγκεκριμένη σελίδα, και πώς να **προσθέσετε κείμενο σφραγίδας PDF** που προσαρμόζει αυτόματα το μέγεθός του. Το πλήρες, εκτελέσιμο παράδειγμα παραπάνω αφαιρεί τις εικασίες και σας παρέχει μια σταθερή βάση για πιο προχωρημένα σενάρια σφράγισης—όπως επεξεργασία δεκάδων αρχείων σε batch ή προσθήκη υδατογραφιών υπό ορισμένες συνθήκες.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να σφραγίσετε κάθε σελίδα σε βρόχο, πειραματιστείτε με διαφορετικές γραμματοσειρές, ή συνδυάστε εικόνες και κείμενο για να δημιουργήσετε ένα επαγγελματικό σφραγιστικό σήμα. Ο ουρανός είναι το όριο, και με το Aspose.Pdf έχετε μια αξιόπιστη μηχανή στο παρασκήνιο.

Αν αντιμετωπίσατε δυσκολίες, αφήστε ένα σχόλιο ή ελέγξτε την τεκμηρίωση του Aspose.Pdf για πιο προχωρημένες επιλογές προσαρμογής. Καλή σφράγιση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}