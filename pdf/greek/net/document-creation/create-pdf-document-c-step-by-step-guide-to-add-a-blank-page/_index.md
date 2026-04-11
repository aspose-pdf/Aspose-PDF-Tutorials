---
category: general
date: 2026-04-10
description: Δημιουργήστε γρήγορα έγγραφο PDF με C#. Μάθετε πώς να προσθέσετε μια
  κενή σελίδα PDF, να σχεδιάσετε ένα ορθογώνιο, να προσθέσετε σχήμα ορθογωνίου και
  να ενσωματώσετε το ορθογώνιο στο PDF με καθαρό κώδικα.
draft: false
keywords:
- create pdf document c#
- add blank page pdf
- draw rectangle pdf
- add rectangle shape
- add rectangle to pdf
language: el
og_description: Δημιουργήστε έγγραφο PDF με C# σε λίγα λεπτά. Αυτός ο οδηγός δείχνει
  πώς να προσθέσετε μια κενή σελίδα PDF, να σχεδιάσετε ένα ορθογώνιο PDF και να προσθέσετε
  σχήμα ορθογωνίου με εύκολο κώδικα.
og_title: Δημιουργία PDF Εγγράφου C# – Πλήρης Οδηγός
tags:
- C#
- PDF
- Aspose.PDF
- Document Generation
title: Δημιουργία PDF Εγγράφου C# – Οδηγός βήμα‑προς‑βήμα για την προσθήκη κενής σελίδας
  και τη σχεδίαση ενός ορθογωνίου
url: /el/net/document-creation/create-pdf-document-c-step-by-step-guide-to-add-a-blank-page/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Εγγράφου PDF C# – Πλήρης Οδηγός

Ever needed to **create PDF document C#** for a reporting feature but weren’t sure where to start? You’re not alone. In many projects the first hurdle is getting a clean, blank page PDF and then drawing simple graphics like a rectangle.  

In this tutorial we’ll solve that problem right away: you’ll see how to add a blank page PDF, draw rectangle PDF, and finally add rectangle shape to the file—all with a handful of lines of C#. By the end you’ll have a ready‑to‑use `shapes.pdf` that you can open in any viewer.

## Τι Θα Μάθετε

- Πώς να αρχικοποιήσετε ένα PDF έγγραφο χρησιμοποιώντας το Aspose.PDF for .NET.  
- Τα ακριβή βήματα για **add blank page pdf** και την τοποθέτηση ενός ορθογωνίου μέσα του.  
- Γιατί η κλάση `Rectangle` είναι η σωστή επιλογή για το σχεδιασμό σχημάτων.  
- Κοινά προβλήματα όπως ασυμφωνίες μεγέθους σελίδας και πώς να τα αποφύγετε.  

Χωρίς εξωτερικά εργαλεία, χωρίς μαγεία — μόνο καθαρός κώδικας C# που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε μια εφαρμογή console.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+).  
- Το **Aspose.PDF for .NET** πακέτο NuGet (`Install-Package Aspose.PDF`).  
- Βασική κατανόηση της σύνταξης C# (μεταβλητές, δηλώσεις `using`, κ.λπ.).  

> **Pro tip:** Αν χρησιμοποιείτε Visual Studio, ο NuGet Package Manager κάνει την εγκατάσταση του Aspose.PDF με ένα κλικ.

## Βήμα 1: Αρχικοποίηση του PDF Εγγράφου

Η δημιουργία ενός PDF ξεκινά με ένα αντικείμενο `Document`. Σκεφτείτε το ως το καμβά που θα κρατήσει κάθε σελίδα, εικόνα ή σχήμα που θα προσθέσετε αργότερα.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Initialise a new PDF document – this is the core of create pdf document c#
var pdfDocument = new Document();
```

Η κλάση `Document` σας δίνει πρόσβαση στη συλλογή `Pages`, η οποία είναι όπου θα **add blank page pdf** αργότερα.

## Βήμα 2: Προσθήκη Κενής Σελίδας στο Έγγραφο

Ένα PDF χωρίς σελίδες είναι ουσιαστικά κενό. Η προσθήκη μιας σελίδας είναι τόσο απλή όσο η κλήση του `pdfDocument.Pages.Add()`. Η νέα σελίδα κληρονομεί το προεπιλεγμένο μέγεθος (A4) εκτός αν ορίσετε κάτι διαφορετικό.

```csharp
// Add a fresh, blank page – this satisfies the add blank page pdf requirement
Page page = pdfDocument.Pages.Add();
```

> **Why this matters:** Η προσθήκη μιας σελίδας πρώτα εξασφαλίζει ότι τυχόν επόμενες εντολές σχεδίασης έχουν μια επιφάνεια για απόδοση. Η παράλειψη αυτού του βήματος θα προκαλέσει σφάλμα χρόνου εκτέλεσης όταν προσπαθήσετε να σχεδιάσετε ένα ορθογώνιο.

## Βήμα 3: Ορισμός Ορίων Ορθογωνίου

Τώρα θα **draw rectangle pdf** δημιουργώντας ένα αντικείμενο `Rectangle`. Ο κατασκευαστής παίρνει τις συντεταγμένες X/Y του κάτω‑αριστερού σημείου, ακολουθούμενες από το πλάτος και το ύψος. Στο παράδειγμά μας θέλουμε ένα ορθογώνιο που να χωράει άνετα μέσα στη σελίδα, αφήνοντας ένα μικρό περιθώριο.

```csharp
// Rectangle coordinates: (0,0) is the lower‑left corner of the page
// Width = 500, Height = 700 – fits comfortably on an A4 page
var rectangle = new Rectangle(0, 0, 500, 700);
```

Αν χρειάζεστε διαφορετικό μέγεθος, απλώς προσαρμόστε τις τιμές πλάτους/ύψους. Το αρχικό σημείο του ορθογωνίου (0,0) ευθυγραμμίζεται με την κάτω‑αριστερή γωνία της σελίδας, κάτι που συχνά προκαλεί σύγχυση στους νέους χρήστες.

## Βήμα 4: Προσθήκη Σχήματος Ορθογωνίου στη Σελίδα

Με το αντικείμενο ορθογωνίου έτοιμο, μπορούμε να **add rectangle shape** στη σελίδα. Η μέθοδος `AddRectangle` σχεδιάζει το περίγραμμα χρησιμοποιώντας την τρέχουσα κατάσταση γραφικών (η προεπιλογή είναι μια λεπτή μαύρη γραμμή).

```csharp
// Add the rectangle shape – this completes the add rectangle to pdf step
page.AddRectangle(rectangle);
```

Μπορείτε να προσαρμόσετε την εμφάνιση τροποποιώντας το αντικείμενο `Graphics` πριν καλέσετε το `AddRectangle`, π.χ., ορίζοντας `LineWidth` ή `Color`. Για γεμάτο χρώμα θα χρησιμοποιούσατε `page.AddAnnotation(new SquareAnnotation(...))`, αλλά αυτό υπερβαίνει το πεδίο αυτού του απλού οδηγού.

## Βήμα 5: Αποθήκευση του Αρχείου PDF

Τέλος, αποθηκεύστε το έγγραφο στο δίσκο. Επιλέξτε έναν φάκελο στον οποίο έχετε δικαίωμα εγγραφής και δώστε στο αρχείο ένα περιγραφικό όνομα όπως `shapes.pdf`.

```csharp
// Save the PDF – you’ll find shapes.pdf in the specified directory
pdfDocument.Save(@"C:\Temp\shapes.pdf");
```

> **Note:** Η δήλωση `using` από το αρχικό απόσπασμα δεν απαιτείται εδώ επειδή το `Document` υλοποιεί το `IDisposable`. Ωστόσο, η περιτύλιξή του σε `using` είναι καλή συνήθεια για καθαρισμό πόρων, ειδικά σε μεγαλύτερες εφαρμογές.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα αυτόνομο πρόγραμμα console που μπορείτε να εκτελέσετε αμέσως:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new PDF document
            using (var pdfDocument = new Document())
            {
                // Step 2: Add a blank page to the document
                Page page = pdfDocument.Pages.Add();

                // Step 3: Define a rectangle that fits inside the page bounds (0,0 to 500,700)
                var rectangle = new Rectangle(0, 0, 500, 700);

                // Step 4: Add the rectangle shape to the page
                page.AddRectangle(rectangle);

                // Step 5: Save the PDF file
                string outputPath = @"C:\Temp\shapes.pdf";
                pdfDocument.Save(outputPath);

                Console.WriteLine($"PDF created successfully at {outputPath}");
            }
        }
    }
}
```

**Expected output:** Μετά την εκτέλεση του προγράμματος, ανοίξτε το `C:\Temp\shapes.pdf`. Θα δείτε μια μοναδική σελίδα με ένα μαύρο περίγραμμα ορθογωνίου τοποθετημένο στην κάτω‑αριστερή γωνία, ακριβώς 500 × 700 points σε μέγεθος.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Question | Answer |
|----------|--------|
| *Μπορώ να αλλάξω το μέγεθος της σελίδας πριν προσθέσω το ορθογώνιο;* | Ναι. Δημιουργήστε ένα `Page` με προσαρμοσμένες διαστάσεις: `var page = pdfDocument.Pages.Add(); page.PageInfo.Width = 600; page.PageInfo.Height = 800;` |
| *Τι αν χρειάζομαι γεμάτο ορθογώνιο;* | Χρησιμοποιήστε ένα αντικείμενο `Graphics`: `page.Canvas.Rectangle(rectangle, Color.Blue, Color.LightBlue);` |
| *Το Aspose.PDF είναι δωρεάν;* | Προσφέρει **free trial** με πλήρη λειτουργικότητα· απαιτείται εμπορική άδεια για παραγωγική χρήση. |
| *Πώς προσθέτω πολλαπλά ορθογώνια;* | Απλώς επαναλάβετε τα βήματα 3‑4 με διαφορετικά παραδείγματα `Rectangle` ή προσαρμόστε τις συντεταγμένες. |

## Επόμενα Βήματα

Τώρα που ξέρετε πώς να **create pdf document c#**, **add blank page pdf**, και **draw rectangle pdf**, ίσως θέλετε να εξερευνήσετε:

- Προσθήκη κειμένου μέσα στο ορθογώνιο (`TextFragment`, `page.Paragraphs.Add`).  
- Εισαγωγή εικόνων (`page.Resources.Images.Add`) για δημιουργία πιο πλούσιων αναφορών.  
- Εξαγωγή του PDF σε άλλες μορφές όπως PNG ή DOCX χρησιμοποιώντας τα APIs μετατροπής της Aspose.  

Όλα αυτά τα θέματα επεκτείνονται φυσικά από τη βάση **add rectangle to pdf** που δημιουργήσαμε εδώ.

---

*Καλή προγραμματιστική!* Αν αντιμετωπίσετε οποιοδήποτε πρόβλημα, μη διστάσετε να αφήσετε ένα σχόλιο παρακάτω. Και θυμηθείτε — μόλις κυριαρχήσετε τα βασικά, η δημιουργία σύνθετων PDF γίνεται παιγνίδι.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}