---
category: general
date: 2026-08-08
description: Προσθήκη αρίθμησης Bates σε PDF χρησιμοποιώντας το Aspose.Pdf σε C#.
  Αυτό το σεμινάριο δείχνει επίσης πώς να προσθέσετε κενή σελίδα σε PDF και να δημιουργήσετε
  PDF προγραμματιστικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: el
lastmod: 2026-08-08
og_description: Προσθέστε αρίθμηση Bates σε PDF με το Aspose.Pdf σε C#. Μάθετε πώς
  να προσθέτετε κενή σελίδα σε PDF, να δημιουργείτε PDF προγραμματιστικά και να αποθηκεύετε
  το τελικό έγγραφο σε λίγα λεπτά.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Προσθήκη αρίθμησης Bates σε PDF με το Aspose – πλήρης οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Προσθήκη αρίθμησης Bates σε PDF με το Aspose – οδηγός βήμα‑προς‑βήμα
url: /el/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη αρίθμησης Bates σε PDF με Aspose – οδηγός βήμα‑βήμα

Η προσθήκη αρίθμησης Bates σε PDF με Aspose.Pdf είναι απλή μόλις κατανοήσετε τα βασικά βήματα. Εάν χρειάζεστε επίσης να προσθέσετε κενή σελίδα PDF ή να δημιουργήσετε PDF προγραμματιστικά, αυτός ο οδηγός καλύπτει όλα όσα χρειάζεστε.

Σε αυτό το tutorial θα:

* Δημιουργήσετε ένα νέο έγγραφο PDF από την αρχή.  
* Προσθέσετε μια κενή σελίδα PDF που θα φιλοξενήσει τους αριθμούς Bates.  
* Διαμορφώσετε το αντικείμενο BatesNumberingArtifact με προσαρμοσμένο πρόθεμα.  
* Αποθηκεύσετε το PDF ώστε οι αριθμοί να εμφανίζονται στο παραγόμενο αρχείο.  

Στο τέλος θα έχετε μια πλήρως λειτουργική εφαρμογή κονσόλας C# που παράγει ένα PDF που περιέχει αριθμούς Bates όπως **CASE‑1000**, **CASE‑1001**, … – μια κοινή απαίτηση για νομικές και διαδικασίες e‑discovery.

## Προαπαιτούμενα

* .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.8).  
* Visual Studio 2022 ή οποιοδήποτε IDE συμβατό με C#.  
* Ένα έγκυρο άδεια Aspose.Pdf for .NET (ή ένα δωρεάν κλειδί αξιολόγησης).  
* Βασική εξοικείωση με τη σύνταξη της C#.

> **Συμβουλή:** Εάν εκτελέσετε τον κώδικα χωρίς άδεια, το Aspose θα προσθέσει ένα μικρό υδατογράφημα στο παραγόμενο PDF.

## Βήμα 1: Ρύθμιση του έργου και εισαγωγή του Aspose.Pdf

Δημιουργήστε ένα νέο έργο κονσόλας και προσθέστε το πακέτο NuGet Aspose.Pdf:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

Οι οδηγίες `using` που απαιτούνται για το παράδειγμα είναι:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

Αυτοί οι χώροι ονομάτων σας δίνουν πρόσβαση στις κλάσεις `Document`, `Page` και `BatesNumberingArtifact` που χρησιμοποιούνται αργότερα.

## Βήμα 2: Προσθήκη κενής σελίδας PDF

Ένας αριθμός Bates πρέπει να συνδέεται με μια σελίδα, έτσι πρώτα δημιουργούμε μια κενή σελίδα που θα λάβει το αντικείμενο αρίθμησης.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

Η κλάση `Document` αντιπροσωπεύει ολόκληρο το αρχείο PDF, ενώ η μέθοδος `Pages.Add()` εισάγει μια νέα, κενή σελίδα στο τέλος της συλλογής σελίδων του εγγράφου. Επειδή το έγγραφο ξεκινά κενό, αυτή η κλήση δημιουργεί επίσης την πρώτη σελίδα.

## Βήμα 3: Διαμόρφωση του αντικειμένου BatesNumberingArtifact

Τώρα ορίζουμε πώς πρέπει να φαίνονται οι αριθμοί Bates. Το `BatesNumberingArtifact` σας επιτρέπει να ορίσετε τον αρχικό αριθμό, το πρόθεμα, το επίθημα και τις επιλογές μορφοποίησης.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Γιατί είναι σημαντικό:**  
Ο ορισμός του `StartNumber` σε **1000** ταιριάζει με τις τυπικές συμβάσεις αρχείων νομικών υποθέσεων. Το `Prefix` εξασφαλίζει ότι κάθε αριθμός εμφανίζεται ως **CASE‑1000**, **CASE‑1001**, …, κάτι που διευκολύνει την αναζήτηση και την ταξινόμηση.

## Βήμα 4: Προσθήκη του αντικειμένου στη σελίδα

Το αντικείμενο πρέπει να προστεθεί στη συλλογή `Artifacts` της σελίδας ώστε το Aspose να το αποδίδει σε κάθε σελίδα κατά την αποθήκευση.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

Όταν το έγγραφο αποθηκευτεί, το Aspose επαναλαμβάνει αυτόματα το αντικείμενο σε όλες τις σελίδες, αυξάνοντας τον αριθμό για κάθε επόμενη σελίδα.

## Βήμα 5: (Προαιρετικό) Προσθήκη επιπλέον σελίδων

Εάν χρειάζεστε περισσότερες σελίδες, απλώς επαναλάβετε `pdfDocument.Pages.Add()`. Το αντικείμενο BatesNumberingArtifact που προσθέσατε στο προηγούμενο βήμα θα εμφανίζεται αυτόματα σε κάθε νέα σελίδα.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Βήμα 6: Αποθήκευση του PDF – δημιουργία PDF προγραμματιστικά

Τέλος, αποθηκεύστε το έγγραφο στο δίσκο. Αυτό είναι το σημείο όπου οι αριθμοί Bates αποδίδονται στις σελίδες.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Αναμενόμενο αποτέλεσμα:**  
Ανοίξτε το *BatesNumberedDocument.pdf* και θα δείτε ένα PDF τριών σελίδων. Κάθε σελίδα εμφανίζει έναν αριθμό Bates στην κάτω‑δεξιά γωνία:

* Σελίδα 1 → **CASE‑1000**  
* Σελίδα 2 → **CASE‑1001**  
* Σελίδα 3 → **CASE‑1002**

Οι αριθμοί αυξάνονται αυτόματα επειδή το αντικείμενο είναι προσαρτημένο στη συλλογή σελίδων.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα, εδώ είναι ένα πλήρες πρόγραμμα κονσόλας που μπορείτε να αντιγράψετε, επικολλήσετε και να εκτελέσετε:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Εκτελέστε το πρόγραμμα με `dotnet run`. Μετά την εκτέλεση, εντοπίστε το αρχείο στην επιφάνεια εργασίας σας και επαληθεύστε τους αριθμούς Bates.

![Add bates numbering pdf example](/images/bates-numbering.png "Add bates numbering pdf example")

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

### Τι γίνεται αν χρειάζομαι διαφορετική γραμματοσειρά ή θέση;

Το `BatesNumberingArtifact` εκθέτει ιδιότητες όπως `FontSize`, `FontColor`, `HorizontalAlignment` και `VerticalAlignment`. Για παράδειγμα:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### Πώς μπορώ να εξαιρέσω μια συγκεκριμένη σελίδα από την αρίθμηση;

Δημιουργήστε ένα ξεχωριστό `BatesNumberingArtifact` για τις σελίδες που θέλετε να αριθμήσετε και προσθέστε το μόνο σε αυτές τις σελίδες. Οι σελίδες χωρίς προσαρτημένο αντικείμενο θα παραμείνουν χωρίς αριθμό.

### Λειτουργεί αυτό με υπάρχοντα PDF;

Ναι. Αντί για `new Document()`, φορτώστε ένα υπάρχον αρχείο:

```csharp
Document pdfDocument = new Document("input.pdf");
```

Στη συνέχεια, προσθέστε το αντικείμενο στις επιθυμητές σελίδες και αποθηκεύστε.

## Συμπέρασμα

Τώρα ξέρετε πώς να **προσθέσετε αρίθμηση Bates σε PDF** χρησιμοποιώντας το Aspose.Pdf, πώς να **προσθέσετε κενή σελίδα PDF**, και πώς να **δημιουργήσετε PDF προγραμματιστικά** σε μια καθαρή, επαναχρησιμοποιήσιμη λύση C#. Η προσέγγιση λειτουργεί με οποιονδήποτε αριθμό σελίδων, προσαρμοσμένα προθέματα και επιλογές στυλ, δίνοντάς σας πλήρη έλεγχο του τελικού εγγράφου.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

* Χρησιμοποιήστε **create pdf as

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Προσθέσετε και να Προσαρμόσετε Αριθμούς Σελίδων σε PDF χρησιμοποιώντας το Aspose.PDF για .NET | Οδηγός Διαχείρισης Εγγράφων](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Πώς να Προσθέσετε μια Κενή Σελίδα στο Τέλος ενός PDF χρησιμοποιώντας το Aspose.PDF για .NET | Οδηγός Βήμα‑Βήμα](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Δημιουργία Εγγράφου PDF με Aspose.PDF – Προσθήκη Σελίδας, Σχήματος & Αποθήκευση](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}