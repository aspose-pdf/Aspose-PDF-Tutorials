---
category: general
date: 2026-06-05
description: Δημιουργήστε προσβάσιμο τμήμα κειμένου σε PDF χρησιμοποιώντας το Aspose.PDF
  και μάθετε πώς να μετατρέψετε PDF σε PDF/X-4. Ακολουθήστε αυτόν τον βήμα‑βήμα οδηγό
  C# για αξιόπιστη διαχείριση εγγράφων.
draft: false
keywords:
- create accessible text span
- convert pdf to pdf/x-4
- how to convert pdf to pdfx4
language: el
og_description: Δημιουργήστε προσβάσιμο τμήμα κειμένου σε PDF και ανακαλύψτε πώς να
  μετατρέψετε PDF σε PDF/X-4 χρησιμοποιώντας το Aspose.PDF. Αυτό το σεμινάριο σας
  καθοδηγεί βήμα-βήμα.
og_title: Δημιουργία Προσβάσιμου Κειμένου Span σε PDF – Πλήρης Οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create accessible text span in a PDF using Aspose.PDF and learn how
    to convert PDF to PDF/X-4. Follow this step‑by‑step C# tutorial for robust document
    handling.
  headline: 'Create Accessible Text Span in PDF with Aspose: Full C# Guide'
  type: TechArticle
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: 'Δημιουργία προσβάσιμου κειμενικού αποσπάσματος σε PDF με το Aspose: Πλήρης
  οδηγός C#'
url: /el/net/programming-with-tagged-pdf/create-accessible-text-span-in-pdf-with-aspose-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Προσβάσιμου Text Span σε PDF με το Aspose: Πλήρης Οδηγός C# 

Έχετε χρειαστεί ποτέ να **δημιουργήσετε προσβάσιμο κείμενο span** σε ένα PDF αλλά δεν ήξερτε από πού να ξεκινήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν πειραματίζονται για πρώτη φορά με την προσβασιμότητα των PDF. Τα καλά νέα είναι ότι το Aspose.PDF το κάνει απροσδόκητα απλό, και ενώ το κάνετε μπορείτε επίσης να μάθετε **πώς να μετατρέψετε PDF σε PDF/X-4** στην ίδια διαδικασία.

Σε αυτόν τον οδηγό θα φορτώσουμε ένα υπάρχον PDF, θα απαριθμήσουμε τις ψηφιακές του υπογραφές, θα μετατρέψουμε το αρχείο σε PDF/X‑4, θα προσθέσουμε ένα προσβάσιμο τοποθετημένο text span, θα ενσωματώσουμε ένα πεδίο φόρμας πολλαπλών σελίδων, θα εξάγουμε σε HTML χωρίς raster εικόνες και τέλος θα επικυρώσουμε την υπογραφή έναντι ενός διακομιστή CA. Στο τέλος θα έχετε ένα ενιαίο, αυτόνομο πρόγραμμα C# που κάνει όλα αυτά—χωρίς κομμάτια κώδικα, χωρίς συντομεύσεις «δείτε τα docs».

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας μεταγλωττίζεται επίσης σε .NET Framework 4.7+).  
- Ένα έγκυρο άδεια Aspose.PDF for .NET (η δωρεάν δοκιμή λειτουργεί, αλλά θα αντιμετωπίσετε περιορισμούς μετά από μερικές σελίδες).  
- Ένα αρχείο PDF εισόδου με όνομα `input.pdf` τοποθετημένο σε φάκελο που ελέγχετε (αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή).  
- Βασική εξοικείωση με εφαρμογές κονσόλας C#—τίποτα περίπλοκο, μόνο μια μέθοδο `Main`.  

Τα έχετε όλα; Τέλεια—ας βουτήξουμε.

## Δημιουργία Προσβάσιμου Text Span με το Aspose.PDF

Ο πρώτος συγκεκριμένος στόχος είναι να **δημιουργήσετε προσβάσιμο κείμενο span** μέσα στο tagged περιεχόμενο του PDF. Τα Tagged PDF είναι η ραχοκοκαλιά της προσβασιμότητας· επιτρέπουν στους αναγνώστες οθόνης να κατανοούν τη λογική σειρά ανάγνωσης.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Devices;
using System.Drawing;

// Load the source PDF
var sourcePdf = new Document("YOUR_DIRECTORY/input.pdf");

// Create a positioned span element
var positionedSpan = sourcePdf.TaggedContent.CreateSpanElement();
positionedSpan.SetPosition(150, 500);          // X=150, Y=500 points from bottom‑left
positionedSpan.Text = "Accessible positioned text";

// Append the span to the root of the tagged tree
sourcePdf.TaggedContent.RootElement.AppendChild(positionedSpan);
```

**Γιατί είναι σημαντικό:** Συνδέοντας το span στο `TaggedContent.RootElement`, εξασφαλίζετε ότι οι βοηθητικές τεχνολογίες το βλέπουν ως μέρος της λογικής δομής, όχι μόνο ως οπτική επικάλυψη. Η κλήση `SetPosition` σας επιτρέπει να τοποθετήσετε το κείμενο ακριβώς εκεί που χρειάζεται—ιδανικό για επικάλυψη λεζαντών σε εικόνες ή διαγράμματα.

> **Pro tip:** Αν το PDF σας περιέχει ήδη ένα δέντρο `DocumentStructure`, μπορείτε να εισάγετε το span κάτω από έναν συγκεκριμένο κόμβο `Paragraph` ή `Section` για να διατηρήσετε την ιεραρχία.

## Μετατροπή PDF σε PDF/X-4 Χρησιμοποιώντας το Aspose

Τώρα που το κομμάτι της προσβασιμότητας είναι στη θέση του, ας αντιμετωπίσουμε την απαίτηση **convert pdf to pdf/x-4**. Το PDF/X‑4 είναι ένα υποσύνολο σχεδιασμένο για αξιόπιστη εκτύπωση· ενσωματώνει όλες τις γραμματοσειρές και υποστηρίζει διαφάνεια.

```csharp
// Define conversion options: target PDF/X‑4 and delete any conversion errors
var conversionOptions = new PdfFormatConversionOptions(
    PdfFormat.PDF_X_4,            // Target format
    ConvertErrorAction.Delete); // Remove problematic objects

// Perform the conversion in‑place
sourcePdf.Convert(conversionOptions);

// Save the converted file
sourcePdf.Save("YOUR_DIRECTORY/converted_pdfx4.pdf");
```

**Γιατί το κάνετε:** Η μετατροπή σε PDF/X‑4 αφαιρεί στοιχεία που θα μπορούσαν να προκαλέσουν σφάλματα εκτύπωσης (όπως μη υποστηριζόμενα προφίλ χρώματος). Η σημαία `ConvertErrorAction.Delete` εξασφαλίζει ότι η μετατροπή δεν θα διακοπεί· τυχόν προβληματικά αντικείμενα απλώς απορρίπτονται, διατηρώντας το αρχείο λειτουργικό.

> **Edge case:** Αν χρειάζεται να διατηρήσετε το αρχικό αρχείο αμετάβλητο, κλωνοποιήστε το πρώτα (`var clone = sourcePdf.Clone();`) και εκτελέστε τη μετατροπή στο κλώνο.

## Λίστα Ψηφιακών Υπογραφών και Έλεγχος Κατάστασης Παραβίασης

Πριν επεξεργαστούμε περαιτέρω το έγγραφο, είναι σοφό να δούμε ποιες υπογραφές είναι ήδη ενσωματωμένες. Αυτό το βήμα δεν αφορά αποκλειστικά την προσβασιμότητα, αλλά δείχνει **how to convert pdf to pdfx4** με ασφάλεια—χωρίς να σπάσετε τις υπάρχουσες υπογραφές.

```csharp
// Retrieve signature information
var signatures = sourcePdf.DigitalSignatures.GetSignatureInfo();

foreach (var sig in signatures)
{
    Console.WriteLine($"{sig.Name} compromised? {sig.IsCompromised}");
}
```

Αν το `IsCompromised` επιστρέψει `true`, ίσως θελήσετε να επανα-υπογράψετε μετά τη μετατροπή, επειδή το PDF/X‑4 μπορεί να ακυρώσει ορισμένους τύπους υπογραφών.

## Προσθήκη Πεδίου Φόρμας TextBox Πολλαπλών Σελίδων

Ένα κοινό σενάριο είναι μια φόρμα που εκτείνεται σε πολλές σελίδες—π.χ. ένα πλαίσιο “Σχόλια” που εμφανίζεται σε κάθε σελίδα. Δείτε πώς να δημιουργήσετε ένα `TextBoxField` και να συνδέσετε widgets σε δύο διαφορετικές σελίδες.

```csharp
// Create a TextBox on page 1 (pages are 1‑based)
var textBox = new TextBoxField(sourcePdf.Pages[1],
    new Rectangle(100, 700, 300, 730)); // left, bottom, right, top

// Add a second widget on page 2
textBox.AddWidget(sourcePdf.Pages[2],
    new Rectangle(50, 600, 250, 630));

// Register the field in the form collection
sourcePdf.Form.Add(textBox, "MultiWidgetField");
```

**Γιατί πολλαπλά widgets:** Κάθε widget αντιπροσωπεύει μια οπτική εμφάνιση του ίδιου λογικού πεδίου. Οι χρήστες συμπληρώνουν οποιαδήποτε εμφάνιση, και η τιμή διαδίδεται σε όλες τις σελίδες—ιδανικό για μακροσκελείς έρευνες.

## Αποθήκευση ως HTML Παράλειψη Raster Εικόνων

Μερικές φορές χρειάζεστε μια έκδοση έτοιμη για web του PDF, αλλά δεν θέλετε βαριές raster εικόνες να γεμίζουν τη σελίδα. Το παρακάτω απόσπασμα δείχνει πώς να **convert pdf to pdf/x-4**‑style εξαγωγή ενώ εξάγετε σε HTML και παραλείπετε τις εικόνες.

```csharp
var htmlOptions = new HtmlSaveOptions
{
    SkipImages = true          // Do not embed raster images
};

sourcePdf.Save("YOUR_DIRECTORY/output.html", htmlOptions);
```

Το παραγόμενο `output.html` περιέχει μόνο διανυσματικά γραφικά και κείμενο, καθιστώντας το εξαιρετικά γρήγορο στη φόρτωση σε έναν περιηγητή.

## Επικύρωση της Ψηφιακής Υπογραφής μέσω Διακομιστή CA

Τέλος, ας επαληθεύσουμε την ενσωματωμένη υπογραφή έναντι μιας Αρχής Πιστοποίησης (CA). Αυτό το βήμα δείχνει **how to convert pdf to pdfx4** με ασφάλεια—επιβεβαιώνοντας ότι η υπογραφή παραμένει αξιόπιστη μετά από όλες τις μετατροπές.

```csharp
var validator = new SignatureValidator(sourcePdf);
bool isCaValid = validator.ValidateWithCaServer("https://ca.mycompany.com/validate");

Console.WriteLine($"CA validation result: {isCaValid}");
```

Αν ο διακομιστής CA επιστρέψει `false`, θα χρειαστεί να επανα-υπογράψετε το PDF μετά το βήμα της μετατροπής. Το `SignatureValidator` του Aspose αφαιρεί το βάρος της επικύρωσης της αλυσίδας πιστοποιητικών.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα έργο κονσόλας:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Devices;
using System.Drawing;

class Demo
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var sourcePdf = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ List existing digital signatures
        var signatures = sourcePdf.DigitalSignatures.GetSignatureInfo();
        foreach (var sig in signatures)
            Console.WriteLine($"{sig.Name} compromised? {sig.IsCompromised}");

        // 3️⃣ Convert to PDF/X‑4 (how to convert pdf to pdfx4)
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        sourcePdf.Convert(conversionOptions);
        sourcePdf.Save("YOUR_DIRECTORY/converted_pdfx4.pdf");

        // 4️⃣ Create an accessible positioned text span
        var positionedSpan = sourcePdf.TaggedContent.CreateSpanElement();
        positionedSpan.SetPosition(150, 500);
        positionedSpan.Text = "Accessible positioned text";
        sourcePdf.TaggedContent.RootElement.AppendChild(positionedSpan);

        // 5️⃣ Add a TextBox form field with widgets on two pages
        var textBox = new TextBoxField(sourcePdf.Pages[1],
            new Rectangle(100, 700, 300, 730));
        textBox.AddWidget(sourcePdf.Pages[2],
            new Rectangle(50, 600, 250, 630));
        sourcePdf.Form.Add(textBox, "MultiWidgetField");

        // 6️⃣ Export to HTML, skipping raster images
        var htmlOptions = new HtmlSaveOptions { SkipImages = true };
        sourcePdf.Save("YOUR_DIRECTORY/output.html", htmlOptions);

        // 7️⃣ Validate the signature against a CA server
        var validator = new SignatureValidator(sourcePdf);
        bool isCaValid = validator.ValidateWithCaServer("https://ca.mycompany.com/validate");
        Console.WriteLine($"CA validation result: {isCaValid}");
    }
}
```

**Αναμενόμενη έξοδος** (κονσόλα):

```
John Doe compromised? False
CA validation result: True
```

Θα δείτε επίσης τρία νέα αρχεία στο `YOUR_DIRECTORY`:

- `converted_pdfx4.pdf` – η έκδοση PDF/X‑4.  
- `output.html` – HTML χωρίς raster εικόνες.  
- Το αρχικό `input.pdf` τώρα περιέχει το προσβάσιμο text span και το πεδίο φόρμας.

## Συνηθισμένα Παράπονα & Πώς να τα Αποφύγετε

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Signature becomes invalid after conversion** | PDF/X‑4 strips certain objects that signatures rely on. | Re‑sign after the `Convert` step, or use `ConvertErrorAction.Keep` if you must preserve the original objects. |
| **Tagged content not recognized** | You appended the span to the wrong node. | Always attach to `TaggedContent.RootElement` *or* a specific structural element (e.g., a `Paragraph`). |
| **HTML export still contains images** | `SkipImages` only skips raster images, not vector graphics. | For pure text‑only output, also set `RasterImagesCompression = RasterImagesCompression.None`. |
| **CA validation fails due to network issues** | The validator can | Ο επαληθευτής μπορεί |

## Τι Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Create Accessible Tagged PDFs Using Aspose.PDF for .NET&#58; Enhance Titles, Alt Text, and Layout](/pdf/english/net/advanced-features/enhanced-tagged-pdfs-aspose-pdf-dot-net/)
- [How to Rotate Text in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/text-operations/rotate-text-aspose-pdf-net-guide/)
- [How to Create Bookmark Pages in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/bookmarks-navigation/create-pdf-bookmarks-aspose-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}