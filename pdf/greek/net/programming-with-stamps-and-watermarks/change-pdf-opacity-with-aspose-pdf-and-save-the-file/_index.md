---
category: general
date: 2026-11-12
description: Μάθετε πώς να αλλάζετε τη διαφάνεια PDF χρησιμοποιώντας το Aspose.Pdf,
  να προσθέτετε διαφάνεια, να ορίζετε τη λειτουργία ανάμειξης και να αποθηκεύετε το
  τροποποιημένο PDF σε C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change PDF opacity
- how to add transparency
- save modified PDF
- how to set blend mode
- set fill opacity
language: el
lastmod: 2026-11-12
og_description: Αλλάξτε τη διαφάνεια PDF με το Aspose.Pdf, μάθετε πώς να προσθέτετε
  διαφάνεια, να ορίζετε λειτουργία ανάμειξης και να αποθηκεύετε τροποποιημένα αρχεία
  PDF σε C#.
og_image_alt: Screenshot of a PDF page with altered opacity using Aspose.Pdf
og_title: Αλλάξτε την αδιαφάνεια του PDF με το Aspose.Pdf – προσθέστε διαφάνεια και
  αποθηκεύστε
schemas:
- author: Aspose
  dateModified: '2026-11-12'
  description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  headline: Change PDF opacity with Aspose.Pdf and save the file
  type: TechArticle
- description: Learn how to change PDF opacity using Aspose.Pdf, add transparency,
    set blend mode, and save modified PDF in C#.
  name: Change PDF opacity with Aspose.Pdf and save the file
  steps:
  - name: Load the PDF document
    text: Start by creating a `Document` instance that points to your source file.
      The constructor reads the entire PDF into memory, allowing you to manipulate
      its internal objects.
  - name: Access the first page’s resources
    text: Each PDF page stores a *resource dictionary* that holds objects such as
      fonts, images, and graphics states. You need to edit this dictionary to inject
      a new `ExtGState` entry.
  - name: Ensure an ExtGState dictionary exists
    text: The `ExtGState` dictionary holds custom graphics states. If it does not
      exist, the code creates one automatically.
  - name: Define a new graphics state (ExtGState)
    text: A graphics state defines how drawing operations behave. The following dictionary
      sets stroke opacity (`CA`), fill opacity (`ca`), and blend mode (`BM`).
  - name: Register the graphics state in the resource dictionary
    text: Give the new state a name (e.g., `GS0`) and add it to the `ExtGState` dictionary.
      This name will be referenced later in the page content stream.
  - name: Apply the graphics state to page content
    text: To actually see the opacity effect, insert the `/GS0 gs` operator before
      the drawing commands you want to affect. The example below draws a semi‑transparent
      rectangle.
  - name: Save the modified PDF
    text: Finally, write the updated document to disk. The `Save` method overwrites
      the target file or creates a new one if it does not exist.
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Αλλαγή της διαφάνειας του PDF με το Aspose.Pdf και αποθήκευση του αρχείου
url: /el/net/programming-with-stamps-and-watermarks/change-pdf-opacity-with-aspose-pdf-and-save-the-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αλλαγή διαφάνειας PDF με Aspose.Pdf και αποθήκευση του αρχείου

Αν χρειάζεστε να **αλλάξετε τη διαφάνεια PDF** σε ένα έγγραφο, το Aspose.Pdf παρέχει ένα απλό API για να ρυθμίσετε τόσο τη διαφάνεια του περιγράμματος όσο και του γεμίσματος. Αυτό το σεμινάριο δείχνει ακριβώς **πώς να προσθέσετε διαφάνεια**, **πώς να ορίσετε τη λειτουργία ανάμειξης**, και **να αποθηκεύσετε τροποποιημένα PDF** αρχεία με μόνο λίγες γραμμές κώδικα C#.

Θα περάσετε από κάθε βήμα—από τη φόρτωση ενός υπάρχοντος PDF μέχρι τον ορισμό μιας νέας κατάστασης γραφικών και την αποθήκευση των αλλαγών. Στο τέλος αυτού του οδηγού μπορείτε να:

* Μειώσετε την ορατότητα των διανυσματικών γραφικών ή εικόνων.
* Εφαρμόσετε μια προσαρμοσμένη λειτουργία ανάμειξης όπως *Normal* ή *Multiply*.
* Εξάγετε το ενημερωμένο αρχείο χωρίς να χάσετε κανένα άλλο περιεχόμενο.

Η μόνη προαπαιτούμενη προϋπόθεση είναι ένα λειτουργικό περιβάλλον ανάπτυξης .NET και μια αναφορά στη βιβλιοθήκη Aspose.Pdf (έκδοση 23.9 ή νεότερη). Δεν απαιτούνται εξωτερικά εργαλεία.

## Προαπαιτούμενα

| Απαιτούμενο | Γιατί είναι σημαντικό |
|-------------|------------------------|
| .NET 6.0 SDK ή νεότερο | Εγγυάται τη συμβατότητα με τα πιο πρόσφατα APIs του Aspose.Pdf. |
| Aspose.Pdf for .NET NuGet package | Παρέχει τις κλάσεις `Document`, `CosPdfDictionary` και σχετικές που χρησιμοποιούνται στον κώδικα. |
| Αρχείο PDF για επεξεργασία (π.χ., `input.pdf`) | Λειτουργεί ως πηγή για τις αλλαγές διαφάνειας. |

Εγκαταστήστε το πακέτο NuGet με:

```bash
dotnet add package Aspose.Pdf
```

## Αλλαγή διαφάνειας PDF με Aspose.Pdf

### Βήμα 1: Φόρτωση του εγγράφου PDF

Ξεκινήστε δημιουργώντας ένα αντικείμενο `Document` που δείχνει στο πηγαίο αρχείο σας. Ο κατασκευαστής διαβάζει ολόκληρο το PDF στη μνήμη, επιτρέποντάς σας να χειριστείτε τα εσωτερικά του αντικείμενα.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Operators;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;

// Load the existing PDF
var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");
```

> **Γιατί αυτό το βήμα;** Η φόρτωση του αρχείου δημιουργεί ένα διαχειρίσιμο μοντέλο αντικειμένων. Όλες οι επόμενες αλλαγές λειτουργούν πάνω σε αυτήν την αναπαράσταση στη μνήμη, εξασφαλίζοντας ότι το αρχικό αρχείο παραμένει αμετάβλητο μέχρι να το αποθηκεύσετε ρητά.

### Βήμα 2: Πρόσβαση στους πόρους της πρώτης σελίδας

Κάθε σελίδα PDF αποθηκεύει ένα *λεξικό πόρων* που περιέχει αντικείμενα όπως γραμματοσειρές, εικόνες και καταστάσεις γραφικών. Πρέπει να επεξεργαστείτε αυτό το λεξικό για να εισάγετε μια νέα καταχώρηση `ExtGState`.

```csharp
// Retrieve the first page (pages are 1‑based)
var page = pdfDoc.Pages[1];

// The DictionaryEditor simplifies access to the page's resource dictionary
var resourcesEditor = new DictionaryEditor(page.Resources);
```

> **Συμβουλή:** Εάν το PDF σας περιέχει πολλαπλές σελίδες που χρειάζονται την ίδια διαφάνεια, επαναλάβετε αυτό το βήμα για κάθε σελίδα ή μοιραστείτε ένα ενιαίο `ExtGState` μεταξύ των σελίδων.

### Βήμα 3: Διασφάλιση ύπαρξης λεξικού ExtGState

Το λεξικό `ExtGState` περιέχει προσαρμοσμένες καταστάσεις γραφικών. Εάν δεν υπάρχει, ο κώδικας δημιουργεί αυτόματα ένα.

```csharp
// Get or create the ExtGState dictionary
var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                     ?? new CosPdfDictionary(pdfDoc);
resourcesEditor["ExtGState"] = extGStateDict;
```

> **Γιατί αυτό το βήμα;** Χωρίς ένα κοντέινερ `ExtGState`, οποιαδήποτε προσπάθεια αναφοράς σε νέα κατάσταση γραφικών θα αποτύχει, με αποτέλεσμα ένα PDF που αγνοεί τις ρυθμίσεις διαφάνειας.

### Βήμα 4: Ορισμός νέας κατάστασης γραφικών (ExtGState)

Μια κατάσταση γραφικών ορίζει πώς συμπεριφέρονται οι λειτουργίες σχεδίασης. Το παρακάτω λεξικό ορίζει τη διαφάνεια του περιγράμματος (`CA`), τη διαφάνεια γεμίσματος (`ca`) και τη λειτουργία ανάμειξης (`BM`).

```csharp
// Create an empty dictionary for the new graphics state
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDoc);

// Set desired parameters
var parameters = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1.0)),   // Stroke opacity (1 = opaque)
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)), // Fill opacity (0.5 = 50% transparent)
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal")) // Blend mode
};

foreach (var param in parameters)
    newGraphicsState.Add(param);
```

> **Πώς να ορίσετε τη διαφάνεια γεμίσματος:** Η καταχώρηση `ca` ελέγχει τη διαφάνεια των γεμισμένων σχημάτων (κείμενο, διαδρομές). Ρυθμίστε την αριθμητική τιμή μεταξύ `0` (πλήρως διαφανές) και `1` (πλήρως αδιαφανές) ώστε να ανταποκρίνεται στις απαιτήσεις του σχεδίου σας.

> **Πώς να ορίσετε τη λειτουργία ανάμειξης:** Η καταχώρηση `BM` επιλέγει τον αλγόριθμο σύνθεσης. Συνηθισμένες τιμές περιλαμβάνουν `Normal`, `Multiply`, `Screen` και `Overlay`. Επιλέξτε αυτήν που ταιριάζει με την οπτική σας πρόθεση.

### Βήμα 5: Καταχώρηση της κατάστασης γραφικών στο λεξικό πόρων

Δώστε στη νέα κατάσταση ένα όνομα (π.χ., `GS0`) και προσθέστε το στο λεξικό `ExtGState`. Αυτό το όνομα θα αναφερθεί αργότερα στο ρεύμα περιεχομένου της σελίδας.

```csharp
// Add the graphics state with a symbolic name
extGStateDict.Add("GS0", newGraphicsState);
```

> **Επαγγελματική συμβουλή:** Χρησιμοποιήστε μια σύμβαση ονοματοδοσίας όπως `GS0`, `GS1`, … όταν δημιουργείτε πολλαπλές καταστάσεις. Αποτρέπει συγκρούσεις ονομάτων και κάνει τον εντοπισμό σφαλμάτων πιο εύκολο.

### Βήμα 6: Εφαρμογή της κατάστασης γραφικών στο περιεχόμενο της σελίδας

Για να δείτε πραγματικά το αποτέλεσμα της διαφάνειας, εισάγετε τον τελεστή `/GS0 gs` πριν από τις εντολές σχεδίασης που θέλετε να επηρεάσετε. Το παρακάτω παράδειγμα σχεδιάζει ένα ημιδιαφανές ορθογώνιο.

```csharp
// Build a content stream that uses the new graphics state
var content = new MemoryStream();
var writer = new StreamWriter(content);

// Activate the graphics state
writer.WriteLine("q");                 // Save graphics state
writer.WriteLine("/GS0 gs");           // Apply custom ExtGState
writer.WriteLine("0.2 0.5 0.8 rg");    // Set fill color (RGB)
writer.WriteLine("100 500 200 100 re"); // Rectangle (x y width height)
writer.WriteLine("f");                 // Fill rectangle
writer.WriteLine("Q");                 // Restore graphics state
writer.Flush();

content.Position = 0;
page.Contents.Add(new ContentStream(content));
```

> **Γιατί οι τελεστές `q` και `Q`;** Αυτοί σπρώχνουν και αφαιρούν την στοίβα κατάστασης γραφικών, διασφαλίζοντας ότι η αλλαγή διαφάνειας επηρεάζει μόνο το ορθογώνιο και όχι το υπόλοιπο της σελίδας.

### Βήμα 7: Αποθήκευση του τροποποιημένου PDF

Τέλος, γράψτε το ενημερωμένο έγγραφο στο δίσκο. Η μέθοδος `Save` αντικαθιστά το αρχείο προορισμού ή δημιουργεί ένα νέο εάν δεν υπάρχει.

```csharp
// Persist the changes
pdfDoc.Save(@"YOUR_DIRECTORY\output.pdf");
```

> **Πώς να αποθηκεύσετε το τροποποιημένο PDF:** Η κλήση `Save` γράφει όλες τις τροποποιήσεις στη μνήμη, συμπεριλαμβανομένου του νέου `ExtGState`, στην καθορισμένη διαδρομή. Μπορείτε επίσης να μεταφέρετε το αποτέλεσμα σε ένα `MemoryStream` για απαντήσεις web.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω υπάρχει ένα μοναδικό, αυτόνομο πρόγραμμα που ενσωματώνει κάθε βήμα που περιγράφηκε παραπάνω. Αντιγράψτε το σε μια εφαρμογή κονσόλας και εκτελέστε το για να επαληθεύσετε την αλλαγή διαφάνειας.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.XObjects;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Operators;

class ChangePdfOpacityDemo
{
    static void Main()
    {
        // 1. Load the PDF
        var pdfDoc = new Document(@"YOUR_DIRECTORY\input.pdf");

        // 2. Get first page and its resources
        var page = pdfDoc.Pages[1];
        var resourcesEditor = new DictionaryEditor(page.Resources);

        // 3. Ensure ExtGState dictionary exists
        var extGStateDict = resourcesEditor["ExtGState"]?.ToCosPdfDictionary()
                             ?? new CosPdfDictionary(pdfDoc);
        resourcesEditor["Ext


## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω σεμινάρια καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να αποθηκεύσετε τροποποιημένο PDF με Aspose.Pdf και να προσθέσετε διαφάνεια](/pdf/english/net/document-manipulation/how-to-save-modified-pdf-with-aspose-pdf-and-add-transparenc/)
- [Πώς να προσθέσετε διαφάνεια σε PDF χρησιμοποιώντας Aspose.PDF σε C#](/pdf/english/net/images-graphics/how-to-add-transparency-to-pdf-using-aspose-pdf-in-c/)
- [Πώς να προσθέσετε κατάσταση γραφικών PDF και να ελέγξετε τη διαφάνεια με Aspose.PDF](/pdf/english/net/images-graphics/how-to-add-graphics-state-pdf-and-control-transparency-with/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}