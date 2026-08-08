---
category: general
date: 2026-04-02
description: Πώς να αποδώσετε PDF χρησιμοποιώντας το Aspose.PDF σε C#. Μάθετε πώς
  να αποδίδετε PDF σε PNG, να αποθηκεύετε PDF ως HTML και να προσθέτετε αυτόματα προσαρμοζόμενες
  σφραγίδες κειμένου αποδοτικά.
draft: false
keywords:
- how to render pdf
- save pdf as html
- render pdf to png
- convert pdf page png
- export pdf page image
language: el
og_description: Πώς να αποδώσετε PDF χρησιμοποιώντας το Aspose.PDF σε C#. Αυτός ο
  οδηγός δείχνει την απόδοση PDF σε PNG, την αποθήκευση ως HTML και τη δημιουργία
  αυτοπροσαρμοζόμενων σφραγίδων κειμένου.
og_title: Πώς να αποδώσετε PDF σε C# – PNG, HTML & Αυτόματη προσαρμογή σφραγίδων
tags:
- Aspose.PDF
- C#
- PDF processing
title: Πώς να αποδώσετε PDF σε C# – Πλήρης οδηγός για PNG, HTML & σφράγιση
url: /el/net/printing-rendering/how-to-render-pdf-in-c-complete-guide-to-png-html-stamping/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποδώσετε PDF σε C# – Πλήρης Οδηγός για PNG, HTML & Σφραγίδωση

Έχετε αναρωτηθεί ποτέ **πώς να αποδώσετε PDF** σε μια εφαρμογή .NET χωρίς να χάσετε ούτε ένα γλύφη; Ίσως δοκιμάσατε γρήγορα το `PdfRenderer` και παρατηρήσατε ελλείποντες χαρακτήρες, ή χρειάζεστε ένα καθαρό PNG για μικρογραφία αλλά το αποτέλεσμα φαίνεται σκαμπό. Από την εμπειρία μου, ο σωστός συνδυασμός επιλογών απόδοσης και διαχείρισης γραμματοσειρών κάνει τη διαφορά μεταξύ μιας χαλασμένης προεπισκόπησης και μιας εικόνας pixel‑perfect.

Σε αυτό το tutorial θα περάσουμε από τρία πραγματικά σενάρια με το Aspose.PDF for .NET: απόδοση μιας σελίδας PDF σε PNG με ανάλυση γραμματοσειρών, προσθήκη ενός `TextStamp` που αυτόματα προσαρμόζει το μέγεθος της γραμματοσειράς, και αποθήκευση ενός PDF ως HTML χρησιμοποιώντας τον πίνακα CMap της γραμματοσειράς. Στο τέλος θα μπορείτε να **αποδώσετε PDF σε PNG**, **μετατρέψετε σελίδα PDF σε PNG**, **εξάγετε εικόνα σελίδας PDF**, και ακόμη **αποθηκεύσετε PDF ως HTML** χωρίς προβλήματα.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+)
- Πακέτο NuGet Aspose.PDF for .NET (`Install-Package Aspose.PDF`)
- Ένα αρχείο PDF με σύνθετες γραμματοσειρές (π.χ. `complexFonts.pdf`) για τη demo απόδοση
- Βασική εξοικείωση με C# και Visual Studio (ή οποιοδήποτε IDE προτιμάτε)

> **Pro tip:** Αν τρέχετε σε διακομιστή CI, βεβαιωθείτε ότι το αρχείο άδειας Aspose είναι είτε ενσωματωμένο ως πόρος είτε αναφέρεται μέσω μεταβλητής περιβάλλοντος για να αποφύγετε τα υδατογράμματα αξιολόγησης.

---

## ## Πώς να αποδώσετε PDF σε PNG με Ανάλυση Γραμματοσειρών

### Γιατί να αναλύσετε τις γραμματοσειρές;

Όταν ένα PDF περιέχει προσαρμοσμένες ή ενσωματωμένες γραμματοσειρές, μια αφελής απόδοση μπορεί να χάσει γλύφους που ο renderer δεν μπορεί να αντιστοιχίσει. Η ενεργοποίηση του `AnalyzeFonts` αναγκάζει το Aspose να εξετάσει τα ρεύματα γραμματοσειρών και να αντικαταστήσει τους ελλείποντες γλύφους, εξασφαλίζοντας μια πιστή εικόνα.

### Υλοποίηση βήμα‑βήμα

1. **Δημιουργήστε ένα `PngDevice` με ενεργοποιημένο το `AnalyzeFonts`.**  
2. **Φορτώστε το πηγαίο PDF** χρησιμοποιώντας το `Document`.  
3. **Επεξεργαστείτε τη ζητούμενη σελίδα** και γράψτε το PNG στο δίσκο.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using Aspose.Pdf.Text;

// 1️⃣ Set up a PNG device that will analyze fonts
var pngDevice = new PngDevice
{
    RenderingOptions = new RenderingOptions
    {
        // This flag makes sure no glyph is lost during rendering
        AnalyzeFonts = true
    }
};

// 2️⃣ Load the PDF that contains complex fonts
using (var sourcePdf = new Document("YOUR_DIRECTORY/complexFonts.pdf"))
{
    // 3️⃣ Render the first page to a PNG file
    pngDevice.Process(sourcePdf.Pages[1], "YOUR_DIRECTORY/rendered.png");
}
```

**Τι θα δείτε:** Ένα αρχείο με όνομα `rendered.png` στο `YOUR_DIRECTORY` που φαίνεται ακριβώς όπως η πρώτη σελίδα του `complexFonts.pdf`, συμπεριλαμβανομένων όλων των ειδικών χαρακτήρων και διακριτικών.

![Rendered PDF page as PNG image](rendered.png "Rendered PDF page as PNG image")

#### Συνηθισμένα προβλήματα & πώς να τα αποφύγετε

- **Έλλειψη γραμματοσειρών στον διακομιστή:** Αν το PDF αναφέρει γραμματοσειρές που δεν είναι ενσωματωμένες, τοποθετήστε αυτές τις γραμματοσειρές στη διαδρομή ανίχνευσης της εφαρμογής ή ενεργοποιήστε το `FontRepository` για να δείξει σε προσαρμοσμένο φάκελο.
- **Μεγάλα PDF:** Η απόδοση πολλών σελίδων σε βρόχο μπορεί να καταναλώσει μνήμη· απελευθερώστε άμεσα κάθε αντικείμενο `Document` ή χρησιμοποιήστε μπλοκ `using` όπως φαίνεται.

---

## ## Προσθήκη Auto‑Fit TextStamp (Απόδοση PDF με Δυναμικό Κείμενο)

### Πότε χρειάζεστε μια σφραγίδα με δυναμικό μέγεθος;

Φανταστείτε ότι δημιουργείτε τιμολόγια και πρέπει να επικάνετε ένα υδατογράφημα “PAID” που ταιριάζει σε οποιοδήποτε ορθογώνιο επιλέγετε, ανεξάρτητα από το μήκος του κειμένου. Ο υπολογισμός του μεγέθους γραμματοσειράς με το χέρι είναι επιρρεπής σε σφάλματα· το `AutoAdjustFontSizeToFitStampRectangle` του Aspose κάνει το δύσκολο μέρος.

### Υλοποίηση βήμα‑βήμα

1. **Διαμορφώστε ένα `TextStamp`** με ιδιότητες αυτόματης προσαρμογής.  
2. **Φορτώστε το PDF-στόχο** που θέλετε να σφραγίσετε.  
3. **Προσθέστε τη σφραγίδα σε μια σελίδα** και αποθηκεύστε το αποτέλεσμα.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// 1️⃣ Create a TextStamp that auto‑fits its rectangle
var autoFitStamp = new TextStamp("Important notice")
{
    // Let Aspose shrink or grow the font until it fits
    AutoAdjustFontSizeToFitStampRectangle = true,
    AutoAdjustFontSizePrecision = 0.01f, // finer precision for tighter fit
    WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
    Width = 300,   // Desired stamp width in points
    Height = 150,  // Desired stamp height in points
    // Optional styling
    Background = new BackgroundInfo(Color.Yellow),
    TextState = new TextState { FontSize = 48, Font = FontRepository.FindFont("Arial") }
};

// 2️⃣ Load the PDF you want to stamp
using (var pdfToStamp = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // 3️⃣ Add the stamp to the first page (you can choose any page)
    pdfToStamp.Pages[1].AddStamp(autoFitStamp);

    // Save the stamped PDF
    pdfToStamp.Save("YOUR_DIRECTORY/stampAutoFit.pdf");
}
```

**Αποτέλεσμα:** Το `stampAutoFit.pdf` περιέχει το κείμενο “Important notice” τέλεια προσαρμοσμένο στο ορθογώνιο 300 × 150 pt, ανεξάρτητα από το αρχικό μήκος της συμβολοσειράς.

#### Περιπτώσεις άκρων που πρέπει να ληφθούν υπόψη

- **Πολύ μεγάλες συμβολοσειρές:** Αν το κείμενο υπερβαίνει το ορθογώνιο ακόμη και στο μικρότερο μέγεθος γραμματοσειράς, το Aspose θα το περικόψει σύμφωνα με το `WordWrapMode`. Μπορείτε να ελέγξετε το μήκος εκ των προτέρων ή να αυξήσετε το μέγεθος του ορθογωνίου.
- **Πολλαπλές σφραγίδες:** Η επαναχρησιμοποίηση του ίδιου αντικειμένου `TextStamp` σε διαφορετικές σελίδες λειτουργεί, αλλά θυμηθείτε ότι οι ιδιότητες θέσης (`Left`, `Top`) διατηρούν τις τελευταίες τιμές· επαναρυθμίστε τις όπως χρειάζεται.

---

## ## Αποθήκευση PDF ως HTML Χρησιμοποιώντας τον Πίνακα CMap της Γραμματοσειράς

### Γιατί να ασχοληθείτε με τον πίνακα CMap;

Κατά τη μετατροπή ενός PDF σε HTML, η διατήρηση της αντιστοίχισης Unicode είναι κρίσιμη για κείμενο αναζητήσιμο. Η στρατηγική βασισμένη σε CMap αναγκάζει το Aspose να δώσει προτεραιότητα στον εσωτερικό χάρτη χαρακτήρων της γραμματοσειράς, κάτι που συχνά αποδίδει πιο ακριβή εξαγωγή κειμένου από έναν γενικό κωδικοποιητή.

### Υλοποίηση βήμα‑βήμα

1. **Δημιουργήστε `HtmlSaveOptions`** με τον κανόνα κωδικοποίησης βασισμένο σε CMap.  
2. **Φορτώστε το πηγαίο PDF**.  
3. **Αποθηκεύστε ως HTML** χρησιμοποιώντας τις ρυθμισμένες επιλογές.

```csharp
using Aspose.Pdf;

// 1️⃣ Prepare HTML save options that favor CMap‑based Unicode mapping
var htmlOptions = new HtmlSaveOptions
{
    // This tells Aspose to prefer the font's CMap when generating Unicode text
    FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel,
    // Optional: split each page into a separate HTML file
    SplitIntoPages = true,
    // Optional: embed CSS for better styling
    EmbedCss = true
};

// 2️⃣ Load the PDF you wish to convert
using (var pdfForHtml = new Document("YOUR_DIRECTORY/sample.pdf"))
{
    // 3️⃣ Export the PDF as HTML with the CMap‑aware options
    pdfForHtml.Save("YOUR_DIRECTORY/cmapHtml.html", htmlOptions);
}
```

**Τι θα πάρετε:** Έναν φάκελο (αν το `SplitIntoPages` είναι true) που περιέχει το `cmapHtml.html` και τους σχετικούς πόρους. Ανοίξτε το HTML σε έναν περιηγητή και θα δείτε επιλέξιμο, αναζητήσιμο κείμενο που ταιριάζει σχεδόν τέλεια με το αρχικό PDF.

#### Συμβουλές για καθαρή εξαγωγή HTML

- **Εικόνες vs. διανύσματα:** Ορίστε `RasterImagesSavingMode` σε `RasterImagesSavingMode.AsEmbeddedPartsOfPng` αν προτιμάτε PNG αντί για JPEG για πιο οξυμένες γραφικές παραστάσεις.
- **Μεγάλα PDF:** Χρησιμοποιήστε `HtmlSaveOptions.PageSavingMode = HtmlSaveOptions.HtmlPageSavingModes.SplitIntoPages` για να κρατήσετε κάθε σελίδα ελαφριά.

---

## ## Πλήρες Παράδειγμα – Και τα Τρία Σενάρια σε Ένα Έργο

Παρακάτω υπάρχει μια αυτόνομη εφαρμογή κονσόλας που δείχνει τις τρεις τεχνικές πλάι‑πλάι. Αντιγράψτε‑και‑επικολλήστε την σε ένα νέο έργο C# console, προσθέστε το πακέτο NuGet Aspose.PDF, και προσαρμόστε τις διαδρομές αρχείων.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Devices;
using Aspose.Pdf.Text;

namespace AsposePdfDemo
{
    class Program
    {
        static void Main()
        {
            // ---------------------------------------------------
            // 1️⃣ Render PDF page to PNG with font analysis
            // ---------------------------------------------------
            var pngDevice = new PngDevice
            {
                RenderingOptions = new RenderingOptions { AnalyzeFonts = true }
            };
            using (var srcPdf = new Document("YOUR_DIRECTORY/complexFonts.pdf"))
            {
                pngDevice.Process(srcPdf.Pages[1], "YOUR_DIRECTORY/rendered.png");
                Console.WriteLine("✅ PNG rendered with font analysis.");
            }

            // ---------------------------------------------------
            // 2️⃣ Add an auto‑fit TextStamp
            // ---------------------------------------------------
            var autoFitStamp = new TextStamp("Important notice")
            {
                AutoAdjustFontSizeToFitStampRectangle = true,
                AutoAdjustFontSizePrecision = 0.01f,
                WordWrapMode = TextFormattingOptions.WordWrapMode.ByWords,
                Width = 300,
                Height = 150,
                Background = new BackgroundInfo(Color.Yellow),
                TextState = new TextState { FontSize = 48, Font = FontRepository.FindFont("Arial") }
            };
            using (var pdfToStamp = new Document("YOUR_DIRECTORY/input.pdf"))
            {
                pdfToStamp.Pages[1].AddStamp(autoFitStamp);
                pdfToStamp.Save("YOUR_DIRECTORY/stampAutoFit.pdf");
                Console.WriteLine("✅ TextStamp added and PDF saved.");
            }

            // ---------------------------------------------------
            // 3️⃣ Save PDF as HTML using CMap‑based Unicode mapping
            // ---------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                FontEncodingStrategy = HtmlSaveOptions.FontEncodingRules.DecreaseToUnicodePriorityLevel,
                SplitIntoPages = true,
                EmbedCss = true
            };
            using (var pdfForHtml = new Document("YOUR_DIRECTORY/sample.pdf"))
            {
                pdfForHtml.Save("YOUR_DIRECTORY/cmapHtml.html", htmlOptions);
                Console.WriteLine("✅ PDF saved as HTML with CMap priority.");
            }

            Console.WriteLine("All tasks completed. Check YOUR_DIRECTORY for output files.");
        }
    }
}
```

Τρέξτε το πρόγραμμα και θα βρείτε:

- `rendered.png` – μια τέλεια εικόνα της πρώτης σελίδας του PDF.  
- `stampAutoFit.pdf` – το αρχικό PDF με μια σφραγίδα “Important notice” δυναμικού μεγέθους.  
- `cmapHtml.html` (συμπεριλαμβανομένων των αρχείων HTML ανά σελίδα) – μια έκδοση HTML που διατηρεί την αρχική κωδικοποίηση κειμένου.

---

## ## Συχνές Ερωτήσεις (FAQ)

**Ε: Αυξάνει το `AnalyzeFonts` το χρόνο απόδοσης;**  
Α: Λίγο, επειδή το Aspose σαρώνει κάθε ρεύμα γραμματοσειράς. Η ανταλλαγή αξίζει συνήθως για σύνθετα PDF όπου η απώλεια γλύφων είναι απαράδεκτη.

**Ε: Μπορώ να αποδώσω πολλές σελίδες σε βρόχο;**  
Α: Σίγουρα. Απλώς επαναλάβετε πάνω από `sourcePdf.Pages` και καλέστε `pngDevice.Process(page, $"page{page.Number}.png")`. Θυμηθείτε να απελευθερώσετε κάθε `Document` αν τα ανοίγετε ξεχωριστά.

**Ε: Τι γίνεται αν

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}