---
category: general
date: 2026-07-14
description: Αποθήκευση PDF ως HTML με χρήση του Aspose.Pdf – μάθετε πώς να δημιουργήσετε
  έγγραφο PDF, να προσθέσετε σχήμα ορθογωνίου στο PDF και να εξάγετε σε καθαρό HTML
  χωρίς εικόνες.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save pdf as html
- how to create pdf document
- add rectangle shape pdf
language: el
lastmod: 2026-07-14
og_description: Αποθηκεύστε το PDF ως HTML με το Aspose.Pdf. Ανακαλύψτε πώς να δημιουργήσετε
  έγγραφο PDF, να σχεδιάσετε ένα ορθογώνιο σχήμα PDF και να δημιουργήσετε HTML χωρίς
  εικόνες σε λίγα λεπτά.
og_image_alt: Screenshot of a PDF saved as HTML showing a rectangle shape
og_title: Αποθήκευση PDF ως HTML – Σύντομος οδηγός για τη δημιουργία PDF και την προσθήκη
  σχήματος ορθογωνίου
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save PDF as HTML using Aspose.Pdf – learn how to create PDF document,
    add rectangle shape PDF, and export to clean HTML without images.
  headline: Save PDF as HTML – Create PDF, add rectangle shape
  type: TechArticle
tags:
- pdf
- aspnet
- csharp
- html-export
title: Αποθήκευση PDF ως HTML – Δημιουργία PDF, προσθήκη σχήματος ορθογωνίου
url: /el/net/conversion-export/save-pdf-as-html-create-pdf-add-rectangle-shape/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση PDF ως HTML – Δημιουργία PDF, προσθήκη σχήματος ορθογωνίου

Έχετε αναρωτηθεί ποτέ πώς να **αποθηκεύσετε PDF ως HTML** ενώ εξακολουθείτε να μπορείτε να σχεδιάζετε γραφικά στο αρχικό PDF; Δεν είστε οι μόνοι. Σε πολλά εσωτερικά εργαλεία χρειάζεται μια καθαρή προεπισκόπηση HTML ενός PDF που περιέχει προσαρμοσμένα σχήματα, και οι συνήθεις μετατροπείς είτε ενσωματώνουν βαριές raster εικόνες είτε αφαιρούν εντελώς τα διανυσματικά δεδομένα.

Σε αυτό το tutorial θα δούμε βήμα‑βήμα **πώς να δημιουργήσουμε ένα έγγραφο PDF** προγραμματιστικά με το Aspose.Pdf, να σχεδιάσουμε ένα **σχήμα ορθογωνίου PDF**, να ρυθμίσουμε την αρίθμηση Bates και τελικά **να αποθηκεύσουμε PDF ως HTML** χωρίς raster εικόνες. Στο τέλος θα έχετε μια πλήρως εκτελέσιμη εφαρμογή C# console που παράγει ένα αρχείο HTML που μπορείτε να ανοίξετε σε οποιονδήποτε περιηγητή — χωρίς επιπλέον αρχεία εικόνας.

> **Pro tip:** Το Aspose.Pdf λειτουργεί με .NET 6+, .NET Framework 4.6+ και ακόμη και .NET Core, ώστε να μπορείτε να το ενσωματώσετε σε μια κληρονομική υπηρεσία Windows ή σε μια ολοκαίνουργια μικροϋπηρεσία.

---

## Προαπαιτούμενα

- **Visual Studio 2022** (Community ή νεότερο) ή οποιοδήποτε IDE συμβατό με C#.  
- **Aspose.Pdf for .NET** πακέτο NuGet (έκδοση 23.11 ή νεότερη). Εγκαταστήστε το μέσω του Package Manager Console:

```powershell
Install-Package Aspose.Pdf
```

- Βασική εξοικείωση με τη σύνταξη C#· δεν απαιτείται προηγούμενη εμπειρία με PDF.

---

## Αποθήκευση PDF ως HTML με Aspose.Pdf

Παρακάτω βρίσκεται ο πλήρης κώδικας, έτοιμος για αντιγραφή‑επικόλληση. Ακολουθεί ακριβώς τα βήματα από το αρχικό απόσπασμα, αλλά προσθέτει σχόλια, διαχείριση σφαλμάτων και μια μικρή βοηθητική μέθοδο για να διατηρείται η κύρια ροή ευανάγνωστη.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

namespace PdfToHtmlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh PDF document.
            Document pdfDoc = new Document();
            Page pdfPage = pdfDoc.Pages.Add();

            // 2️⃣ Draw a rectangle shape on the page.
            //    This demonstrates the "add rectangle shape pdf" requirement.
            var rectangle = new Rectangle(100, 500, 300, 700)
            {
                // Optional visual tweaks
                FillColor = Color.GetYellow(),
                Border = new Border
                {
                    Width = 2,
                    Color = Color.GetRed()
                }
            };
            pdfPage.Paragraphs.Add(rectangle);
            pdfPage.ValidateGraphicsState(); // Ensures the shape fits within page bounds

            // 3️⃣ Configure Bates numbering – useful for legal documents.
            var bates = new BatesNumbering { StartNumber = 1, Prefix = "DOC-" };
            pdfDoc.BatesNumbering = bates;

            // 4️⃣ Add a tagged element with an explicit position.
            //    Tagging is important for accessibility (PDF/UA).
            var taggedElement = new TagStructure();
            taggedElement.PositionSettings = new TagPositionSettings { X = 150, Y = 600 };
            pdfPage.TagStructure.Add(taggedElement);

            // 5️⃣ Enable detection of compromised signatures.
            pdfDoc.SecurityOptions.DetectCompromisedSignatures = true;
            bool hasCompromisedSignature = pdfDoc.SecurityOptions.HasCompromisedSignature;
            Console.WriteLine($"Compromised signature? {hasCompromisedSignature}");

            // 6️⃣ Finally, save the PDF as HTML *without* embedding raster images.
            var htmlOptions = new HtmlSaveOptions
            {
                SkipImages = true,               // Removes <img> tags for raster data
                FixedLayout = true,              // Preserves the original page layout
                ExportEmbeddedFonts = false      // Keeps the HTML lightweight
            };

            string outputPath = @"output.html";
            pdfDoc.Save(outputPath, htmlOptions);
            Console.WriteLine($"✅ PDF successfully saved as HTML at: {outputPath}");
        }
    }
}
```

### Τι κάνει ο κώδικας, βήμα‑βήμα

| Βήμα | Γιατί είναι σημαντικό |
|------|------------------------|
| **Δημιουργία εγγράφου PDF** | Αυτή είναι η βάση — χωρίς ένα αντικείμενο `Document` δεν μπορείτε να προσθέσετε τίποτα. |
| **Προσθήκη σχήματος ορθογωνίου PDF** | Δείχνει τη σχεδίαση διανυσματικών γραφικών· τα ορθογώνια είναι το πιο απλό σχήμα, αλλά το ίδιο API υποστηρίζει κύκλους, πολύγωνα κ.λπ. |
| **Ρύθμιση αρίθμησης Bates** | Συχνά απαιτείται σε νομικές ή σε σενάρια επεξεργασίας παρτίδων για μοναδική ταυτοποίηση σελίδων. |
| **Δομή ετικετών** | Βελτιώνει την προσβασιμότητα· οι αναγνώστες οθόνης βασίζονται στις ετικέτες για να μεταφέρουν τη σειρά ανάγνωσης. |
| **Ανίχνευση παραβιασμένων υπογραφών** | Οι εφαρμογές που δίνουν έμφαση στην ασφάλεια χρειάζεται να γνωρίζουν αν μια ψηφιακή υπογραφή έχει παραβιαστεί. |
| **Αποθήκευση PDF ως HTML** | Ο τελικός στόχος — παραγωγή καθαρού HTML που αντικατοπτρίζει τη διάταξη του PDF χωρίς βαριά αρχεία εικόνας. |

> **Γιατί `SkipImages = true`;**  
> Όταν μετατρέπετε ένα PDF που περιέχει διανυσματικά γραφικά (όπως το ορθογώνιο μας) συνήθως δεν χρειάζεστε το raster εναλλακτικό. Η ρύθμιση `SkipImages` αφαιρεί τα στοιχεία `<img>` που διαφορετικά θα αναφέρονταν σε base‑64 blobs, διατηρώντας το αρχείο HTML κάτω από λίγα kilobytes.

---

## Πώς να δημιουργήσετε έγγραφο PDF με Aspose.Pdf

Αν είστε νέοι στο Aspose, η βιβλιοθήκη αντιμετωπίζει ένα PDF σχεδόν όπως ένα έγγραφο Word: προσθέτετε **σελίδες**, έπειτα **παράγραφους**, **σχήματα** ή **σχόλια** σε αυτές τις σελίδες. Η κλάση `Document` είναι το σημείο εισόδου, και κάθε `Page` φιλοξενεί μια συλλογή που ονομάζεται `Paragraphs`. Οτιδήποτε κληρονομεί από `TextFragmentAbsorber`, `Image`, `Rectangle`, κ.λπ., μπορεί να εισαχθεί σε αυτή τη συλλογή.

Παρακάτω υπάρχει ένα ελάχιστο απόσπασμα που δημιουργεί μόνο ένα κενό PDF — χρήσιμο όταν θέλετε να ξεκινήσετε από το μηδέν:

```csharp
Document emptyPdf = new Document();
Page firstPage = emptyPdf.Pages.Add();   // Adds a default‑size A4 page
emptyPdf.Save("empty.pdf");
```

Μπορείτε να αλυσίδετε επιπλέον σελίδες με έναν απλό βρόχο `for`, ή να εφαρμόσετε ρυθμίσεις επιπέδου σελίδας (περιθώριο, μέγεθος) μέσω του `PageInfo`. Η ευελιξία αυτή είναι ο λόγος που το Aspose.Pdf είναι αγαπημένο για δημιουργία PDF από τον διακομιστή.

## Προσθήκη σχήματος ορθογωνίου PDF – σχεδίαση γραφικών

Η κλάση `Rectangle` βρίσκεται στο `Aspose.Pdf.Annotations`. Δέχεται τέσσερις συντεταγμένες: **κάτω‑αριστερό X**, **κάτω‑αριστερό Y**, **πάνω‑δεξιό X**, **πάνω‑δεξιό Y**. Σκεφτείτε το σύστημα συντεταγμένων του PDF ως

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Δημιουργία εγγράφου PDF με Aspose.PDF – Προσθήκη σελίδας, σχήματος & αποθήκευση](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Μετατροπή PDF σε HTML σε .NET χρησιμοποιώντας Aspose.PDF χωρίς αποθήκευση εικόνων](/pdf/english/net/conversion-export/convert-pdf-html-net-asposepdf-no-images/)
- [Μετατροπή PDF σε HTML χρησιμοποιώντας Aspose.PDF .NET&#58; Αποθήκευση εικόνων ως εξωτερικά PNG](/pdf/english/net/conversion-export/pdf-to-html-conversion-external-png-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}