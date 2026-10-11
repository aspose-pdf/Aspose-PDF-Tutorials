---
category: general
date: 2026-10-10
description: Μάθετε πώς να αποθηκεύετε PDF ως HTML με το Aspose.PDF, παραλείποντας
  τις ραστερ εικόνες. Αυτός ο οδηγός καλύπτει τη μετατροπή PDF σε HTML και την αποθήκευση
  του εγγράφου ως HTML αποδοτικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- convert pdf to html
- aspose pdf to html
- save pdf without images
- save document as html
language: el
lastmod: 2026-10-10
og_description: Αποθηκεύστε το PDF ως HTML χρησιμοποιώντας το Aspose.PDF, παραλείποντας
  τις ραστερικές εικόνες. Ακολουθήστε αυτό το πλήρες σεμινάριο για να μετατρέψετε
  το PDF σε HTML και να αποθηκεύσετε το έγγραφο ως HTML.
og_image_alt: Screenshot showing PDF saved as HTML without images using Aspose.PDF
og_title: Αποθήκευση PDF ως HTML χωρίς εικόνες – Οδηγός βήμα‑βήμα για το Aspose.PDF
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to save PDF as HTML with Aspose.PDF, skipping raster images.
    This guide covers convert PDF to HTML and save document as HTML efficiently.
  headline: How to save PDF as HTML without images using Aspose.PDF
  type: TechArticle
tags:
- Aspose.PDF
- C#
- HTML conversion
title: Πώς να αποθηκεύσετε PDF ως HTML χωρίς εικόνες χρησιμοποιώντας το Aspose.PDF
url: /el/net/document-conversion/how-to-save-pdf-as-html-without-images-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποθηκεύσετε PDF ως HTML χωρίς εικόνες χρησιμοποιώντας Aspose.PDF

Αν χρειάζεστε να **αποθηκεύσετε PDF ως HTML** παραλείποντας όλα τα ραστρογραφικά γραφικά, αυτό το tutorial σας δείχνει ακριβώς πώς. Με τη διαμόρφωση του `HtmlSaveOptions` μπορείτε να μετατρέψετε PDF σε HTML αποδοτικά και να διατηρήσετε το αποτέλεσμα ελαφρύ—ιδανικό για έγγραφα φιλικά προς το web ή σελίδες βελτιστοποιημένες για SEO.

Εκτός από την αφαίρεση των εικόνων, ο οδηγός δείχνει επίσης τη γενικότερη ροή εργασίας **convert PDF to HTML**, ώστε να καταλήξετε με ένα καθαρό αρχείο HTML που διατηρεί το κείμενο, τα διανυσματικά γραφικά και τη διάταξη. Δεν απαιτούνται εξωτερικά εργαλεία· όλα εκτελούνται μέσα σε ένα τυπικό έργο .NET.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)
* Έγκυρη άδεια Aspose.PDF for .NET (ή δωρεάν κλειδί αξιολόγησης)
* Ένα αρχείο PDF εισόδου τοποθετημένο σε γνωστό φάκελο
* Visual Studio 2022 (ή οποιοδήποτε IDE C#)

Αυτά τα στοιχεία αρκούν για τη μεταγλώττιση και εκτέλεση του παραδείγματος κώδικα που εμφανίζεται παρακάτω.

## Βήμα 1: Εγκατάσταση του πακέτου NuGet Aspose.PDF

Το πρώτο που πρέπει να κάνετε είναι να προσθέσετε τη βιβλιοθήκη Aspose.PDF στο έργο σας:

```bash
dotnet add package Aspose.PDF
```

Η εκτέλεση αυτής της εντολής επαναφέρει την πιο πρόσφατη σταθερή έκδοση του Aspose.PDF, η οποία περιλαμβάνει την κλάση `HtmlSaveOptions` που απαιτείται για τη μετατροπή.

## Βήμα 2: Φόρτωση του πηγαίου εγγράφου PDF

Η φόρτωση ενός PDF είναι απλή με την κλάση `Document`. Αυτή η κλάση αντιπροσωπεύει ολόκληρο το αρχείο PDF στη μνήμη.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Saving;

// Step 2: Load the source PDF document
Document doc = new Document(@"C:\MyFiles\input.pdf");
```

*Γιατί αυτό το βήμα είναι σημαντικό:*  
`Document` αναλύει τη δομή του PDF, δίνοντάς σας πρόσβαση σε σελίδες, γραμματοσειρές και πόρους. Χωρίς τη φόρτωση του αρχείου, δεν μπορείτε να εφαρμόσετε επιλογές αποθήκευσης.

## Βήμα 3: Διαμόρφωση επιλογών αποθήκευσης HTML για παράλειψη ραστρογραφικών εικόνων

Το αντικείμενο `HtmlSaveOptions` σας επιτρέπει να ρυθμίσετε λεπτομερώς το αποτέλεσμα HTML. Ορίζοντας `SkipRasterImages` σε `true` λέτε στο Aspose.PDF να αγνοήσει όλες τις bitmap εικόνες (JPEG, PNG, GIF) κατά τη μετατροπή.

```csharp
// Step 3: Configure HTML save options to skip raster images
HtmlSaveOptions htmlOpts = new HtmlSaveOptions
{
    // Exclude all raster (bitmap) images from the output HTML
    SkipRasterImages = true,

    // Optional: embed fonts as Base64 to avoid external font files
    EmbedFonts = true,

    // Optional: preserve the original layout as closely as possible
    FixedLayout = true
};
```

*Γιατί αυτό το βήμα είναι σημαντικό:*  
Οι ραστρογραφικές εικόνες συχνά κυριαρχούν στο μέγεθος του αρχείου. Παραλείποντάς τες παράγετε ένα πιο ελαφρύ αρχείο HTML που φορτώνεται γρηγορότερα και είναι πιο εύκολο να το ευρετηριάσει η μηχανή αναζήτησης. Οι επιπλέον επιλογές (`EmbedFonts`, `FixedLayout`) εμφανίζονται για πληρότητα· δεν απαιτούνται για την αφαίρεση εικόνων.

## Βήμα 4: Αποθήκευση του εγγράφου ως HTML χωρίς εικόνες

Τώρα μπορείτε να γράψετε το μετατρεπόμενο περιεχόμενο στο δίσκο. Η υπερφόρτωση `Save` δέχεται τη διαδρομή προορισμού, το επιθυμητό `SaveFormat` και τις προηγουμένως διαμορφωμένες επιλογές.

```csharp
// Step 4: Save the document as HTML without raster images
doc.Save(@"C:\MyFiles\no_images.html", SaveFormat.Html, htmlOpts);
```

Όταν η κλήση ολοκληρωθεί, το `no_images.html` περιέχει το κειμενικό περιεχόμενο, τα διανυσματικά σχήματα και το CSS που αναδημιουργούν την αρχική διάταξη του PDF—χωρίς καμία bitmap εικόνα.

### Αναμενόμενο αποτέλεσμα

Ανοίξτε το `no_images.html` σε έναν περιηγητή. Θα πρέπει να δείτε:

* Όλες τις επικεφαλίδες, παραγράφους και πίνακες από το αρχικό PDF.
* Διανυσματικά γραφικά (π.χ. σχήματα SVG) που αποδίδονται σωστά.
* Καμία ετικέτα `<img>` που να αναφέρεται σε raster αρχεία· αυτές οι ετικέτες λείπουν εντελώς.

Αν εξετάσετε την πηγή HTML, θα παρατηρήσετε την απουσία στοιχείων `<img src="...">`, επιβεβαιώνοντας ότι το `SkipRasterImages` λειτούργησε όπως αναμενόταν.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω υπάρχει μια αυτόνομη εφαρμογή κονσόλας που ενώνει όλα τα βήματα. Αντιγράψτε τον κώδικα σε ένα νέο έργο .NET console και τρέξτε το.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Saving;

namespace PdfToHtmlNoImages
{
    class Program
    {
        static void Main(string[] args)
        {
            // Input and output paths – adjust to your environment
            string inputPath = @"C:\MyFiles\input.pdf";
            string outputPath = @"C:\MyFiles\no_images.html";

            // 1. Load the PDF document
            Document doc = new Document(inputPath);
            Console.WriteLine($"Loaded PDF: {inputPath}");

            // 2. Set up HTML save options to omit raster images
            HtmlSaveOptions htmlOpts = new HtmlSaveOptions
            {
                SkipRasterImages = true,
                EmbedFonts = true,
                FixedLayout = true
            };
            Console.WriteLine("Configured HtmlSaveOptions to skip raster images.");

            // 3. Save as HTML
            doc.Save(outputPath, SaveFormat.Html, htmlOpts);
            Console.WriteLine($"PDF saved as HTML without images at: {outputPath}");
        }
    }
}
```

**Η εκτέλεση του προγράμματος** εμφανίζει μηνύματα προόδου στην κονσόλα και δημιουργεί το `no_images.html`. Επαληθεύστε το αρχείο ανοίγοντάς το σε οποιονδήποτε σύγχρονο περιηγητή.

## Συχνές παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Πώς να προσαρμόσετε τον κώδικα |
|-----------|-------------------------------|
| **Διατήρηση ραστρογραφικών εικόνων** | Ορίστε `SkipRasterImages = false` (ή παραλείψτε την ιδιότητα). |
| **Μετατροπή μόνο ενός εύρους σελίδων** | Χρησιμοποιήστε `doc.Pages.Delete(pageNumber)` για να αφαιρέσετε ανεπιθύμητες σελίδες πριν την αποθήκευση, ή ορίστε `htmlOpts.PageIndex` και `htmlOpts.PageCount`. |
| **Αποθήκευση κάθε σελίδας PDF ως ξεχωριστό αρχείο HTML** | Ορίστε `htmlOpts.SplitIntoPages = true`; η βιβλιοθήκη θα δημιουργήσει `output_page1.html`, `output_page2.html`, κ.λπ. |
| **Συμπίεση του παραγόμενου HTML** | Μετά την αποθήκευση, τρέξτε έναν minifier στο αρχείο ή ορίστε `htmlOpts.Compress = true` (διαθέσιμο σε νεότερες εκδόσεις Aspose). |
| **Διαχείριση PDF με κωδικό πρόσβασης** | Περνάτε τον κωδικό στον κατασκευαστή `Document`: `new Document(inputPath, new LoadOptions { Password = "secret" })`. |

Αυτές οι παραλλαγές σας επιτρέπουν να προσαρμόσετε τη **aspose pdf to html** μετατροπή σε πολλές πραγματικές συνθήκες.

## Συμβουλές επαγγελματιών

* **Άδεια νωρίς** – Καταχωρίστε την άδεια Aspose.PDF πριν φορτώσετε το έγγραφο για να αποφύγετε υδατογραφήματα αξιολόγησης.
* **Απόδοση** – Για μεγάλα PDF, επαναχρησιμοποιήστε ένα μόνο αντικείμενο `HtmlSaveOptions` και εξετάστε το ενδεχόμενο ενεργοποίησης του `htmlOpts.UseZOrder = true` για επιτάχυνση της απόδοσης των επικαλυπτόμενων στοιχείων.
* **Δοκιμή** – Συγκρίνετε το μέγεθος του αρχείου HTML με και χωρίς εικόνες για να ποσοτικοποιήσετε το όφελος του `SkipRasterImages`.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **αποθηκεύσετε PDF ως HTML** αφαιρώντας τα ραστρογραφικά γραφικά χρησιμοποιώντας Aspose.PDF για .NET. Η πλήρης ροή—φόρτωση του PDF, διαμόρφωση του `HtmlSaveOptions` με `SkipRasterImages` και αποθήκευση του αποτελέσματος—καλύπτει τη βασική περίπτωση **convert PDF to HTML** και μπορεί να επεκταθεί για μετατροπή εύρους σελίδων, έξοδο ανά σελίδα ή πρόσθετες βελτιστοποιήσεις.

Στη συνέχεια, μπορείτε να εξερευνήσετε το **save document as HTML** με ενσωματωμένο CSS, ή να πειραματιστείτε με την κλάση `SvgSaveOptions` για δημιουργία διανυσματικών γραφικών αντί HTML. Και οι δύο προσεγγίσεις μειώνουν περαιτέρω το μέγεθος του αρχείου και βελτιώνουν την ανταπόκριση για σύγχρονες web εφαρμογές. Καλό κώδικα!

## Τι πρέπει να μάθετε στη συνέχεια;

- [Μετατροπή PDF σε HTML σε .NET χρησιμοποιώντας Aspose.PDF χωρίς αποθήκευση εικόνων](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [Μετατροπή PDF σε HTML χρησιμοποιώντας Aspose.PDF .NET: Αποθήκευση εικόνων ως εξωτερικά PNG](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)
- [Αποθήκευση PDF ως HTML με Aspose.PDF – Γρήγορος οδηγός C#](/pdf/english/net/conversion-export/save-pdf-as-html-with-aspose-pdf-quick-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}