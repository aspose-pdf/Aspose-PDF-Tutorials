---
category: general
date: 2026-10-23
description: Προσθέστε ετικέτες προσβασιμότητας σε PDF χρησιμοποιώντας το Aspose.PDF
  για .NET. Ακολουθήστε έναν πλήρη, βήμα‑βήμα οδηγό που καλύπτει την προσβασιμότητα
  του Aspose.Pdf, την ετικετοποίηση PDF με C# και τις βέλτιστες πρακτικές PDF/UA.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add accessibility tags to pdf
- Aspose.Pdf accessibility
- C# PDF tagging
- tagged PDF creation
- PDF accessibility best practices
- PDF document structure
language: el
lastmod: 2026-10-23
og_description: Προσθέστε ετικέτες προσβασιμότητας σε PDF με το Aspose.PDF για .NET.
  Αυτό το σεμινάριο σας δείχνει πώς να δημιουργήσετε ένα PDF με ετικέτες που συμμορφώνεται
  με τα πρότυπα PDF/UA.
og_image_alt: Screenshot of a PDF page with a highlighted accessibility tag overlay
og_title: Προσθήκη ετικετών προσβασιμότητας σε PDF με το Aspose.PDF – πλήρης οδηγός
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Add accessibility tags to PDF using Aspose.PDF for .NET. Follow a complete,
    step‑by‑step guide that covers Aspose.Pdf accessibility, C# PDF tagging, and PDF/UA
    best practices.
  headline: How to add accessibility tags to PDF using Aspose.PDF
  type: TechArticle
- description: Add accessibility tags to PDF using Aspose.PDF for .NET. Follow a complete,
    step‑by‑step guide that covers Aspose.Pdf accessibility, C# PDF tagging, and PDF/UA
    best practices.
  name: How to add accessibility tags to PDF using Aspose.PDF
  steps:
  - name: Prepare your development environment
    text: '1. Install the Aspose.PDF NuGet package:'
  - name: Load the source PDF
    text: The first operation opens the existing PDF that you want to tag.
  - name: Create a tagged content element (C# PDF tagging)
    text: A tagged content element describes the logical role of the text (e.g., paragraph,
      heading). Here we create a paragraph tag.
  - name: Define the tag’s location on the page
    text: Accessibility tags also need a geometric location so that the visual layout
      matches the logical structure.
  - name: Add the tag to the first page (tagged PDF creation)
    text: Now attach the tag to a specific page. In this example we use the first
      page, but you can iterate over `pdfDocument.Pages` for multi‑page documents.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The saved file now contains
      the accessibility tag.
  - name: Verify the accessibility tags
    text: You can confirm that the tag was added by opening the PDF in a viewer that
      supports structure inspection (e.g., Adobe Acrobat Pro > Tools > Accessibility
      > Read Order). The paragraph should appear in the logical structure tree.
  type: HowTo
tags:
- PDF
- C#
- Accessibility
title: Πώς να προσθέσετε ετικέτες προσβασιμότητας σε PDF χρησιμοποιώντας το Aspose.PDF
url: /el/net/programming-with-tagged-pdf/how-to-add-accessibility-tags-to-pdf-using-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να προσθέσετε ετικέτες προσβασιμότητας σε PDF χρησιμοποιώντας το Aspose.PDF

Εάν χρειάζεται να **προσθέσετε ετικέτες προσβασιμότητας σε αρχεία PDF**, αυτός ο οδηγός σας παρουσιάζει μια πλήρη λύση με το Aspose.PDF για .NET. Είτε ετοιμάζετε νομικά έγγραφα, e‑books ή αναφορές που πρέπει να συμμορφώνονται με το PDF/UA, θα μάθετε πώς να δημιουργήσετε ένα PDF με ετικέτες που μπορούν να ερμηνεύσουν οι αναγνώστες οθόνης.

Το tutorial καλύπτει τη ρύθμιση του περιβάλλοντος ανάπτυξης, τη δημιουργία ενός στοιχείου ετικέτας, την τοποθέτηση της ετικέτας σε μια σελίδα και την αποθήκευση του τελικού εγγράφου. Δεν απαιτούνται εξωτερικές αναφορές· κάθε απόσπασμα κώδικα είναι έτοιμο για αντιγραφή και εκτέλεση.

## Τι θα χρειαστείτε

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)
- Ένα ενεργό license του Aspose.PDF για .NET (ή ένα προσωρινό κλειδί αξιολόγησης)
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή C# προτιμάτε
- Ένα αρχείο PDF πηγής αποθηκευμένο στο δίσκο (το παράδειγμα χρησιμοποιεί `source.pdf`)

Αυτές οι προαπαιτήσεις εξασφαλίζουν ότι ο κώδικας εκτελείται χωρίς επιπλέον ρυθμίσεις.

## Προσθήκη ετικετών προσβασιμότητας σε PDF – οδηγός βήμα‑βήμα

Οι παρακάτω ενότητες σας καθοδηγούν μέσα από κάθε ενέργεια που απαιτείται για **προσθήκη ετικετών προσβασιμότητας σε PDF**. Κάθε βήμα περιλαμβάνει ένα πλήρες μπλοκ κώδικα, εξήγηση του λόγου για τον οποίο είναι σημαντικό και πρακτικές συμβουλές από πραγματικά έργα.

### Προετοιμασία του περιβάλλοντος ανάπτυξης

1. Εγκαταστήστε το πακέτο NuGet Aspose.PDF:

```bash
dotnet add package Aspose.PDF
```

2. Δημιουργήστε ένα νέο έργο console (ή προσθέστε τον κώδικα σε υπάρχον):

```bash
dotnet new console -n PdfTagger
cd PdfTagger
```

> **Pro tip:** Χρησιμοποιήστε τη σημαία `-n` ώστε το όνομα του φακέλου του έργου να είναι συνεπές με το σκοπό του κώδικα· βοηθά όταν το ψάχνετε αργότερα.

### Φόρτωση του PDF πηγής

Η πρώτη ενέργεια ανοίγει το υπάρχον PDF που θέλετε να ετικετοποιήσετε.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Load the PDF document
var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");
```

**Γιατί είναι σημαντικό:** Το άνοιγμα του εγγράφου δημιουργεί μια αναπαράσταση στη μνήμη που σας επιτρέπει να χειρίζεστε σελίδες, σημειώσεις και ετικέτες. Χωρίς τη φόρτωση του αρχείου, δεν μπορείτε να προσθέσετε καμία πληροφορία προσβασιμότητας.

### Δημιουργία στοιχείου ετικέτας περιεχομένου (C# PDF tagging)

Ένα στοιχείο ετικέτας περιεχομένου περιγράφει τον λογικό ρόλο του κειμένου (π.χ., παράγραφος, επικεφαλίδα). Εδώ δημιουργούμε μια ετικέτα παραγράφου.

```csharp
// Step 2: Create a tagged content element
var paragraphTag = new TaggedContent
{
    Role = TaggedRoles.Paragraph, // defines the logical role
    Text = "Hello, tagged world!" // visible text that screen readers will announce
};
```

**Γιατί είναι σημαντικό:** Η απαρίθμηση `TaggedRoles` αντιστοιχεί άμεσα σε ρόλους PDF/UA. Η χρήση του σωστού ρόλου είναι κρίσιμη για τις βέλτιστες πρακτικές προσβασιμότητας, επειδή λέει στις βοηθητικές τεχνολογίες πώς να ερμηνεύσουν το περιεχόμενο.

### Ορισμός της θέσης της ετικέτας στη σελίδα

Οι ετικέτες προσβασιμότητας χρειάζονται επίσης γεωμετρική θέση ώστε η οπτική διάταξη να ταιριάζει με τη λογική δομή.

```csharp
// Step 3: Define the location on the page (in points)
// Rectangle(left, bottom, right, top)
var tagLocation = new Rectangle(100, 500, 400, 550);
```

**Γιατί είναι σημαντικό:** Το ορθογώνιο ορίζει πού εμφανίζεται η παράγραφος στη σελίδα. Εάν η θέση δεν ταιριάζει με το οπτικό κείμενο, οι αναγνώστες οθόνης μπορεί να μεταφέρουν λανθασμένες πληροφορίες, παραβιάζοντας τις βέλτιστες πρακτικές προσβασιμότητας PDF.

### Προσθήκη της ετικέτας στην πρώτη σελίδα (δημιουργία tagged PDF)

Τώρα συνδέουμε την ετικέτα με μια συγκεκριμένη σελίδα. Στο παράδειγμα χρησιμοποιούμε την πρώτη σελίδα, αλλά μπορείτε να επαναλάβετε για `pdfDocument.Pages` σε πολυσελιδικά έγγραφα.

```csharp
// Step 4: Access the first page
var firstPage = pdfDocument.Pages[1];

// Step 5: Add the tagged content to the page at the specified position
firstPage.AddTag(paragraphTag, tagLocation);
```

> **Προσοχή:** Η συλλογή `Pages` είναι 1‑βάση στο Aspose.PDF. Η προσπάθεια χρήσης του δείκτη 0 θα προκαλέσει `ArgumentOutOfRangeException`.

### Αποθήκευση του τροποποιημένου PDF

Τέλος, γράψτε το ενημερωμένο έγγραφο στο δίσκο. Το αποθηκευμένο αρχείο περιέχει πλέον την ετικέτα προσβασιμότητας.

```csharp
// Step 6: Save the modified PDF with the new tag
pdfDocument.Save(@"YOUR_DIRECTORY\tagged_out.pdf");
```

**Γιατί είναι σημαντικό:** Η αποθήκευση διατηρεί τις πληροφορίες ετικέτας στη δομή ροής του PDF (`/StructTreeRoot`). Το αποτέλεσμα μπορεί να επαληθευτεί με ελεγκτές PDF/UA όπως το PAC (PDF Accessibility Checker).

### Επαλήθευση των ετικετών προσβασιμότητας

Μπορείτε να επιβεβαιώσετε ότι η ετικέτα προστέθηκε ανοίγοντας το PDF σε προβολέα που υποστηρίζει επιθεώρηση δομής (π.χ., Adobe Acrobat Pro > Tools > Accessibility > Read Order). Η παράγραφος θα πρέπει να εμφανίζεται στο λογικό δέντρο δομής.

Εναλλακτικά, χρησιμοποιήστε το API του Aspose.PDF για να διαβάσετε ξανά την ετικέτα:

```csharp
var savedDoc = new Document(@"YOUR_DIRECTORY\tagged_out.pdf");
var savedPage = savedDoc.Pages[1];
var tags = savedPage.Tags; // collection of TaggedContent objects

foreach (var tag in tags)
{
    Console.WriteLine($"Role: {tag.Role}, Text: {tag.Text}");
}
```

**Αναμενόμενη έξοδος:**

```
Role: Paragraph, Text: Hello, tagged world!
```

Εάν η έξοδος ταιριάζει με τον παραπάνω κώδικα, η ετικέτα προσβασιμότητας προστέθηκε επιτυχώς.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που ενσωματώνει κάθε βήμα. Αντιγράψτε τον κώδικα στο `Program.cs` και εκτελέστε `dotnet run`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

namespace PdfTagger
{
    class Program
    {
        static void Main()
        {
            // Load the source PDF
            var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

            // Create a paragraph tag
            var paragraphTag = new TaggedContent
            {
                Role = TaggedRoles.Paragraph,
                Text = "Hello, tagged world!"
            };

            // Define where the tag should appear
            var tagLocation = new Rectangle(100, 500, 400, 550);

            // Attach the tag to the first page
            var firstPage = pdfDocument.Pages[1];
            firstPage.AddTag(paragraphTag, tagLocation);

            // Save the tagged PDF
            var outputPath = @"YOUR_DIRECTORY\tagged_out.pdf";
            pdfDocument.Save(outputPath);

            // Verify the tag was added
            var savedDoc = new Document(outputPath);
            var savedPage = savedDoc.Pages[1];
            foreach (var tag in savedPage.Tags)
            {
                Console.WriteLine($"Role: {tag.Role}, Text: {tag.Text}");
            }

            Console.WriteLine("Accessibility tag added successfully.");
        }
    }
}
```

Η εκτέλεση του προγράμματος παράγει το `tagged_out.pdf`, ένα PDF που τώρα περιέχει μια ετικέτα παραγράφου. Αναγνώστες οθόνης όπως NVDA ή JAWS θα διαβάσουν “Hello, tagged world!” όταν συναντήσουν αυτήν την περιοχή.

## Συνηθισμένες παραλλαγές και περιπτώσεις άκρων

| Κατάσταση | Πώς να προσαρμόσετε τον κώδικα | Λόγος |
|-----------|------------------------------|-------|
| **Πολλές σελίδες** | Επανάληψη μέσω `pdfDocument.Pages` και εφαρμογή ετικετών σε κάθε σελίδα όπως απαιτείται. | Διασφαλίζει ότι κάθε |
| **Προσαρμοσμένο στυλ κειμένου** | Χρησιμοποιήστε `TaggedRoles.Custom` ή δημιουργήστε δικά σας `PdfStructureElement`. | Επιτρέπει πιο ακριβή περιγραφή του περιεχομένου. |
| **Απαιτήσεις PDF/UA‑2** | Προσθέστε επιπλέον ιδιότητες όπως `Alt` κειμένου για εικόνες. | Συμμορφώνεται με τις πιο πρόσφατες προδιαγραφές προσβασιμότητας. |

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Create Tagged PDFs with Aspose.PDF for .NET: A Complete Guide to Enhancing Accessibility and Document Structure](/pdf/english/net/advanced-features/create-tagged-pdfs-aspose-pdf-net/)
- [Create and Manage Tagged PDFs with Aspose.PDF for .NET: Enhance Accessibility and SEO](/pdf/english/net/advanced-features/create-manage-tagged-pdfs-aspose-pdf-dotnet/)
- [Aspose.PDF .NET: Enhancing PDF Accessibility through Tagging](/pdf/english/net/advanced-features/aspose-pdf-net-accessible-tagging-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}