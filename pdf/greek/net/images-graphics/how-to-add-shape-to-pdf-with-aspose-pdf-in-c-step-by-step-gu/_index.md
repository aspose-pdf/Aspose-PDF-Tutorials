---
category: general
date: 2026-06-18
description: Πώς να προσθέσετε σχήμα σε PDF χρησιμοποιώντας το Aspose.PDF σε C# –
  φορτώστε ένα PDF, σχεδιάστε ένα ορθογώνιο και αποθηκεύστε το.
draft: false
keywords:
- how to add shape to pdf
- load pdf document in c#
- how to draw shapes in pdf
- aspose pdf add rectangle
language: el
og_description: Πώς να προσθέσετε σχήμα σε PDF με το Aspose.PDF σε C#. Μάθετε πώς
  να φορτώνετε ένα έγγραφο PDF, να σχεδιάζετε ένα ορθογώνιο και να αποθηκεύετε το
  ενημερωμένο αρχείο.
og_title: Πώς να προσθέσετε σχήμα σε PDF με το Aspose.PDF σε C#
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  headline: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  type: TechArticle
- description: How to add shape to PDF using Aspose.PDF in C# – load a PDF, draw a
    rectangle, and save it.
  name: How to Add Shape to PDF with Aspose.PDF in C# – Step‑by‑Step Guide
  steps:
  - name: What if I need to draw on multiple pages?
    text: Simply loop over `pdfDoc.Pages` and call `AddRectangle` (or any other shape)
      for each page. Remember to adjust coordinates if pages have different sizes.
  - name: Can I fill the rectangle with a color?
    text: Absolutely. Change `FillColor` from `Transparent` to any `Color` you like,
      e.g., `Color.Yellow`. The shape will appear as a solid block.
  - name: Does this work with password‑protected PDFs?
    text: 'Aspose.PDF can open encrypted files if you supply the password:'
  - name: How to add a rectangle with rounded corners?
    text: Use the `RoundedRectangle` class instead of `Rectangle`. The rest of the
      steps stay identical.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Πώς να προσθέσετε σχήμα σε PDF με το Aspose.PDF σε C# – Οδηγός βήμα‑προς‑βήμα
url: /el/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Προσθέσετε Σχήμα σε PDF με Aspose.PDF σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να προσθέσετε σχήμα σε PDF** χωρίς να παλεύετε με χαμηλού επιπέδου ροές byte; Σε πολλές πραγματικές εφαρμογές χρειάζεται να επισημάνετε μια περιοχή, να υπογραμμίσετε μια ρήτρα ή απλώς να σχεδιάσετε ένα πλαίσιο γύρω από ένα πεδίο υπογραφής. Τα καλά νέα είναι ότι το Aspose.PDF το κάνει αυτό παιχνιδάκι. Σε αυτόν τον οδηγό θα φορτώσουμε ένα έγγραφο PDF σε C#, θα σχεδιάσουμε ένα ορθογώνιο και θα αποθηκεύσουμε το αποτέλεσμα — τίποτα παραπάνω, τίποτα λιγότερο.

Θα περάσουμε από κάθε γραμμή κώδικα, θα εξηγήσουμε *γιατί* κάθε κομμάτι είναι σημαντικό, και ακόμη θα σας δείξουμε έναν γρήγορο τρόπο να επαληθεύσετε ότι το σχήμα τοποθετήθηκε ακριβώς εκεί που το περιμένετε. Στο τέλος θα είστε άνετοι με **πώς να σχεδιάζετε σχήματα σε αρχεία PDF**, και θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- **.NET 6.0** (ή οποιαδήποτε πρόσφατη έκδοση .NET) εγκατεστημένη στον υπολογιστή σας.  
- **Έγκυρη άδεια Aspose.PDF for .NET** (ή ένα δωρεάν κλειδί αξιολόγησης).  
- Visual Studio 2022, Rider ή οποιονδήποτε επεξεργαστή προτιμάτε.  
- Ένα υπάρχον αρχείο PDF (`input.pdf`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε.

> **Pro tip:** Αν κάνετε μόνο δοκιμές, η δωρεάν έκδοση αξιολόγησης είναι απολύτως επαρκής — προσθέτει ένα μικρό υδατογράφημα αλλά λειτουργεί όπως το πλήρες προϊόν.

## Βήμα 1: Ρύθμιση του Project και Εισαγωγή Namespaces

Πρώτα, δημιουργήστε ένα νέο console project (ή προσθέστε σε υπάρχον) και φέρετε τα απαραίτητα namespaces στο scope.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;   // Required for shape classes
```

Γιατί είναι σημαντικό: το `Aspose.Pdf` σας δίνει το βασικό μοντέλο εγγράφου, ενώ το `Aspose.Pdf.Drawing` περιέχει την κλάση σχήματος `Rectangle` που θα χρησιμοποιήσουμε αργότερα. Χωρίς το δεύτερο, ο μεταγλωττιστής θα παραπονιστεί ότι το `Rectangle` δεν είναι ορισμένο.

## Βήμα 2: Φόρτωση PDF Εγγράφου σε C#

Τώρα πραγματικά **φορτώνουμε το pdf έγγραφο σε c#**. Αυτή είναι η πρώτη ενέργεια που εκτελείτε πάντα όταν θέλετε να τροποποιήσετε ένα υπάρχον αρχείο.

```csharp
// Step 2: Load the PDF document
string inputPath = @"YOUR_DIRECTORY\input.pdf";
Document pdfDoc = new Document(inputPath);
Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");
```

*Εξήγηση*:  
- Το `Document` είναι η αναπαράσταση του Aspose για ολόκληρο το αρχείο.  
- Η παράδοση της πλήρους διαδρομής στον κατασκευαστή διαβάζει το αρχείο στη μνήμη.  
- Η γραμμή `Console.WriteLine` είναι προαιρετική αλλά χρήσιμη για debugging — αν ο αριθμός σελίδων είναι μηδέν, ξέρετε ότι κάτι πήγε στραβά νωρίς.

## Βήμα 3: Ορισμός του Σχήματος Rectangle

Εδώ φτάνουμε στην καρδιά του **πώς να προσθέσετε σχήμα σε PDF**. Δημιουργούμε ένα αντικείμενο `Rectangle` που καθορίζει τη θέση και το μέγεθός του χρησιμοποιώντας το σύστημα συντεταγμένων όπου το (0,0) είναι η κάτω‑αριστερή γωνία της σελίδας.

```csharp
// Step 3: Define a rectangle (left, bottom, right, top)
Rectangle rect = new Rectangle(0, 0, 200, 100)
{
    // Optional styling – you can tweak these as needed
    FillColor = Color.Transparent,          // No fill, just the border
    Border = new Border(BorderStyle.Solid, 2, Color.Red)
};
```

Γιατί ορίζουμε το `FillColor` σε διαφανές: στις περισσότερες περιπτώσεις θέλουμε μόνο το περίγραμμα (σκεφτείτε ένα πλαίσιο επισήμανσης). Η ιδιότητα `Border` σας επιτρέπει να ελέγξετε το πάχος και το χρώμα· το κόκκινο κάνει το ορθογώνιο να ξεχωρίζει σε μια τυπική λευκή σελίδα.

## Βήμα 4: Επαλήθευση ότι το Σχήμα Εντάσσεται στα Όρια της Σελίδας

Πριν **προσθέσουμε το rectangle**, είναι καλή πρακτική να βεβαιωθούμε ότι το σχήμα δεν υπερβαίνει τα άκρα της σελίδας. Το Aspose παρέχει τη μέθοδο `ValidateShapeBounds` ακριβώς για αυτόν τον σκοπό.

```csharp
// Step 4: Validate that the rectangle fits on the first page
bool fits = pdfDoc.Pages[1].ValidateShapeBounds(rect);
if (!fits)
{
    Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
    // Simple fallback: shrink to fit the page width
    rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
    rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
}
```

*Γιατί*: Η προσπάθεια σχεδίασης εκτός της σελίδας μπορεί να προκαλέσει σφάλματα απόδοσης ή ακόμη και εξαίρεση. Αυτός ο έλεγχος κάνει τον οδηγό πιο ανθεκτικό για PDF οποιουδήποτε μεγέθους.

## Βήμα 5: Προσθήκη του Rectangle στην Επιθυμητή Σελίδα

Τώρα τελικά **προσθέτουμε σχήμα στο pdf**. Η μέθοδος `AddRectangle` συνδέει το σχήμα στη συλλογή σχολίων (annotations) της σελίδας, πράγμα που σημαίνει ότι οι προβολείς PDF θα το αποδώσουν όπως οποιοδήποτε άλλο σχέδιο.

```csharp
// Step 5: Add the rectangle to the first page
pdfDoc.Pages[1].AddRectangle(rect);
Console.WriteLine("Rectangle added to page 1.");
```

Αν χρειάζεται να στοχεύσετε διαφορετική σελίδα, απλώς αντικαταστήστε το δείκτη `1` με τον αντίστοιχο αριθμό σελίδας (το Aspose χρησιμοποιεί αρίθμηση που ξεκινά από 1).

## Βήμα 6: Αποθήκευση του Τροποποιημένου PDF

Το τελευταίο βήμα είναι να γράψετε τις αλλαγές στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή να δημιουργήσετε νέο — εδώ θα δημιουργήσουμε το `output.pdf`.

```csharp
// Step 6: Save the updated PDF
string outputPath = @"YOUR_DIRECTORY\output.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved as {outputPath}");
```

*Τι να περιμένετε*: Ανοίξτε το `output.pdf` σε Adobe Reader ή οποιονδήποτε προβολέα και θα δείτε ένα καθαρό κόκκινο ορθογώνιο αγκυροβολημένο στην κάτω‑αριστερή γωνία της πρώτης σελίδας.

![Diagram showing rectangle added to PDF](https://example.com/rectangle-diagram.png "how to add shape to pdf example")

*Alt text*: "how to add shape to pdf – rectangle drawn on first page of a PDF file"

## Βήμα 7: Πλήρες Παράδειγμα Εργασίας (Ready‑to‑Copy)

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να μεταγλωττίσετε και να τρέξετε αμέσως. Θυμηθείτε να αντικαταστήσετε το `YOUR_DIRECTORY` με τη πραγματική διαδρομή φακέλου στον υπολογιστή σας.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;   // For color definitions

namespace PdfShapeDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the PDF document in C#
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            Document pdfDoc = new Document(inputPath);
            Console.WriteLine($"Loaded PDF with {pdfDoc.Pages.Count} page(s).");

            // Define the rectangle shape
            Rectangle rect = new Rectangle(0, 0, 200, 100)
            {
                FillColor = Color.Transparent,
                Border = new Border(BorderStyle.Solid, 2, Color.Red)
            };

            // Validate bounds on the first page
            if (!pdfDoc.Pages[1].ValidateShapeBounds(rect))
            {
                Console.WriteLine("Rectangle exceeds page dimensions – adjusting...");
                rect.Right = pdfDoc.Pages[1].PageInfo.Width - 10;
                rect.Top  = pdfDoc.Pages[1].PageInfo.Height - 10;
            }

            // Add the rectangle (how to add shape to pdf)
            pdfDoc.Pages[1].AddRectangle(rect);
            Console.WriteLine("Rectangle added to page 1.");

            // Save the modified PDF
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved as {outputPath}");
        }
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το `output.pdf` και θα δείτε το κόκκινο ορθογώνιο ακριβώς εκεί που το τοποθετήσαμε. Αν χρειάζεστε διαφορετικό σχήμα — έλλειψη, γραμμή ή πολύγωνο — απλώς αντικαταστήστε το `Rectangle` με `Ellipse`, `Line` ή `Polygon` διατηρώντας την ίδια ροή εργασίας. Αυτό είναι ουσιαστικά **πώς να σχεδιάζετε σχήματα σε pdf** χρησιμοποιώντας Aspose.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν χρειαστεί να σχεδιάσω σε πολλές σελίδες;
Απλώς κάντε βρόχο πάνω από το `pdfDoc.Pages` και καλέστε `AddRectangle` (ή οποιοδήποτε άλλο σχήμα) για κάθε σελίδα. Θυμηθείτε να προσαρμόσετε τις συντεταγμένες αν οι σελίδες έχουν διαφορετικά μεγέθη.

```csharp
foreach (Page page in pdfDoc.Pages)
{
    page.AddRectangle(rect);
}
```

### Μπορώ να γεμίσω το rectangle με χρώμα;
Απόλυτα. Αλλάξτε το `FillColor` από `Transparent` σε οποιοδήποτε `Color` θέλετε, π.χ. `Color.Yellow`. Το σχήμα θα εμφανιστεί ως συμπαγές μπλοκ.

### Λειτουργεί αυτό με PDF που προστατεύονται με κωδικό;
Το Aspose.PDF μπορεί να ανοίξει κρυπτογραφημένα αρχεία αν παρέχετε τον κωδικό:

```csharp
Document pdfDoc = new Document(inputPath, new LoadOptions { Password = "mySecret" });
```

### Πώς να προσθέσω rectangle με στρογγυλεμένες γωνίες;
Χρησιμοποιήστε την κλάση `RoundedRectangle` αντί για `Rectangle`. Τα υπόλοιπα βήματα παραμένουν ίδια.

## Ανακεφαλαίωση

Καλύψαμε **πώς να προσθέσετε σχήμα σε PDF** χρησιμοποιώντας Aspose.PDF σε C#. Η διαδικασία συνοψίζεται σε:

1. **Φορτώστε το pdf έγγραφο σε c#** – δημιουργήστε ένα αντικείμενο `Document`.  
2. **Ορίστε ένα rectangle** (ή οποιοδήποτε άλλο σχήμα).  
3. **Επικυρώστε τα όρια** για να αποφύγετε υπερχείλιση.  
4. **Προσθέστε το rectangle** στη στοχευμένη σελίδα.  
5. **Αποθηκεύστε** το τροποποιημένο αρχείο.

Αυτή είναι η πλήρης ροή εργασίας για **aspose pdf add rectangle**, και τώρα έχετε ένα πρότυπο που μπορείτε να προσαρμόσετε για κύκλους, γραμμές ή προσαρμοσμένα πολύγωνα.

## Τι Ακολουθεί;

- **Εξερευνήστε άλλα primitives σχεδίασης**: `Ellipse`, `Line`, `Polygon`.  
- **Προσθέστε σχολιασμούς κειμένου** δίπλα στα σχήματά σας για πιο πλούσια αλληλεπίδραση.  
- **Συνδυάστε με πεδία φόρμας PDF** αν δημιουργείτε συμβόλαιο που μπορεί να συμπληρωθεί.  
- **Δείτε τις δυνατότητες μετατροπής PDF του Aspose** για να μετατρέψετε τα σχολιασμένα PDF σε εικόνες για προεπισκοπήσεις.

Πειραματιστείτε — ίσως σχεδιάσετε υδατογράφημα, επισημάνετε ένα κελί πίνακα ή περιγράψετε ένα πεδίο υπογραφής. Το API είναι ευέλικτο, και τώρα γνωρίζετε τα βασικά.

Καλό coding, και οι PDF σας να φαίνονται πάντα ακριβώς όπως το θέλετε!

## Τι Πρέπει να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας projects.

- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Hyperlinks in PDFs Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/bookmarks-navigation/add-hyperlinks-pdf-aspose-net-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}