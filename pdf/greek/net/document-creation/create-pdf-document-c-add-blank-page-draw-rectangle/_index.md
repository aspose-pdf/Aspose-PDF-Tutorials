---
category: general
date: 2026-02-12
description: Δημιουργήστε γρήγορα έγγραφο PDF με C# προσθέτοντας μια κενή σελίδα,
  ελέγχοντας το μέγεθος της σελίδας, σχεδιάζοντας ένα ορθογώνιο και αποθηκεύοντας
  το αρχείο. Οδηγός βήμα‑βήμα με το Aspose.Pdf.
draft: false
keywords:
- create pdf document c#
- add blank page pdf
- draw rectangle pdf
- save pdf file c#
- check pdf page size
language: el
og_description: Δημιουργήστε γρήγορα έγγραφο PDF με C# προσθέτοντας μια κενή σελίδα,
  ελέγχοντας το μέγεθος της σελίδας, σχεδιάζοντας ένα ορθογώνιο και αποθηκεύοντας
  το αρχείο. Πλήρης οδηγός με κώδικα.
og_title: Δημιουργία PDF Εγγράφου C# – Προσθήκη Κενής Σελίδας & Σχεδίαση Ορθογωνίου
tags:
- PDF
- C#
- Aspose.Pdf
- Document Generation
title: Δημιουργία PDF Εγγράφου C# – Προσθήκη Κενής Σελίδας & Σχεδίαση Ορθογωνίου
url: /el/net/document-creation/create-pdf-document-c-add-blank-page-draw-rectangle/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία εγγράφου PDF C# – Προσθήκη κενής σελίδας & Σχεδίαση ορθογωνίου

Έχετε ποτέ χρειαστεί να **create PDF document C#** από το μηδέν και αναρωτηθήκατε πώς να προσθέσετε μια κενή σελίδα, να επαληθεύσετε τις διαστάσεις της σελίδας, να σχεδιάσετε ένα σχήμα και τελικά να το αποθηκεύσετε; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν αυτό το ακριβές εμπόδιο όταν αυτοματοποιούν αναφορές, τιμολόγια ή οποιοδήποτε τύπο εκτυπώσιμου αποτελέσματος.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που σας δείχνει ακριβώς πώς να **add blank page PDF**, **check PDF page size**, **draw rectangle PDF**, και **save PDF file C#** χρησιμοποιώντας τη βιβλιοθήκη Aspose.Pdf. Στο τέλος θα έχετε ένα έτοιμο προς χρήση αρχείο PDF με ένα ορθογώνιο με μπλε περίγραμμα που βρίσκεται όμορφα σε μια σελίδα μεγέθους A4.

## Προαπαιτούμενα

- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+).  
- **Aspose.Pdf for .NET** εγκατεστημένο μέσω NuGet (`Install-Package Aspose.Pdf`).  
- Βασική κατανόηση της σύνταξης C# — δεν απαιτείται τίποτα περίπλοκο.  
- Ένα IDE της επιλογής σας (Visual Studio, Rider, VS Code, κ.λπ.).

> **Συμβουλή επαγγελματία:** Αν χρησιμοποιείτε Visual Studio, το UI του NuGet Package Manager κάνει την προσθήκη του Aspose.Pdf παιχνιδάκι — απλώς αναζητήστε το “Aspose.Pdf” και κάντε κλικ στο Install.

## Βήμα 1: Create PDF Document C# – Αρχικοποίηση του Document

Το πρώτο που χρειάζεστε είναι ένα νέο αντικείμενο `Document`. Σκεφτείτε το ως έναν κενό καμβά όπου κάθε επόμενη λειτουργία θα ζωγραφίζει το περιεχόμενό του.

```csharp
using Aspose.Pdf;
using System;

// Step 1: Create a new PDF document
var pdfDocument = new Document();
```

> **Γιατί είναι σημαντικό:** Η κλάση `Document` είναι το σημείο εισόδου για κάθε λειτουργία PDF. Η δημιουργία της εκχωρεί τις εσωτερικές δομές που χρειάζονται για τη διαχείριση σελίδων, πόρων και μεταδεδομένων.

## Βήμα 2: Add Blank Page PDF – Προσθήκη νέας σελίδας

Ένα PDF χωρίς σελίδες είναι σαν ένα βιβλίο χωρίς σελίδες — άσκοπο. Η προσθήκη μιας κενής σελίδας μας δίνει κάτι πάνω στο οποίο να σχεδιάσουμε.

```csharp
// Step 2: Add a blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Τι συμβαίνει στο παρασκήνιο;** `Pages.Add()` δημιουργεί μια σελίδα που κληρονομεί το προεπιλεγμένο μέγεθος (A4 για τις περισσότερες ρυθμίσεις). Μπορείτε αργότερα να αλλάξετε τις διαστάσεις της αν χρειάζεστε προσαρμοσμένο μέγεθος.

## Βήμα 3: Ορισμός του Ορθογωνίου και Έλεγχος μεγέθους σελίδας PDF

Πριν σχεδιάσουμε, πρέπει να ορίσουμε πού θα τοποθετηθεί το ορθογώνιο και να βεβαιωθούμε ότι χωράει μέσα στη σελίδα. Εδώ μπαίνει σε δράση η λέξη-κλειδί **check PDF page size**.

```csharp
// Step 3: Define rectangle position and size (fits within a standard A4 page)
var rectangle = new Rectangle(50, 50, 550, 750);

// Step 3b: Verify that the rectangle fits inside the page boundaries
bool fitsWidth = page.PageInfo.Width >= rectangle.Width;
bool fitsHeight = page.PageInfo.Height >= rectangle.Height;

if (!fitsWidth || !fitsHeight)
{
    throw new InvalidOperationException(
        $"Rectangle (W:{rectangle.Width}, H:{rectangle.Height}) exceeds page size (W:{page.PageInfo.Width}, H:{page.PageInfo.Height}).");
}
```

> **Γιατί ελέγχουμε:** Κάποια PDF μπορεί να χρησιμοποιούν προσαρμοσμένα μεγέθη σελίδας (Letter, Legal, κ.λπ.). Αν το ορθογώνιο είναι μεγαλύτερο από τη σελίδα, η λειτουργία σχεδίασης είτε περικόπτεται είτε προκαλεί σφάλμα. Αυτό το μέτρο κάνει τον κώδικα ανθεκτικό σε τυχόν μελλοντικές αλλαγές μεγέθους σελίδας.

## Βήμα 4: Draw Rectangle PDF – Απόδοση του σχήματος

Τώρα το διασκεδαστικό κομμάτι: η πραγματική σχεδίαση ενός ορθογωνίου με μπλε περίγραμμα και διαφανή γέμισμα. Αυτό δείχνει τη δυνατότητα **draw rectangle PDF**.

```csharp
// Step 4: Draw the rectangle with a blue border and a transparent fill
page.AddRectangle(
    rectangle,
    Color.Blue,          // Border color
    Color.Transparent    // Fill color (transparent)
);
```

> **Πώς λειτουργεί:** Η `AddRectangle` παίρνει τρία ορίσματα — τη γεωμετρία του ορθογωνίου, το χρώμα του περιγράμματος (stroke) και το χρώμα γεμίσματος. Η χρήση του `Color.Transparent` εξασφαλίζει ότι το εσωτερικό παραμένει κενό, επιτρέποντας σε οποιοδήποτε υποκείμενο περιεχόμενο να φαίνεται.

## Βήμα 5: Save PDF File C# – Αποθήκευση του εγγράφου στο δίσκο

Τέλος, γράφουμε το έγγραφο σε ένα αρχείο. Αυτό είναι το βήμα **save pdf file c#** που κλείνει τη διαδικασία.

```csharp
// Step 5: Save the PDF to a file
string outputPath = @"C:\Temp\shape.pdf"; // Adjust the path as needed
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved successfully to {outputPath}");
```

> **Συμβουλή:** Τυλίξτε όλη τη διαδικασία σε ένα μπλοκ `using` (ή καλέστε `pdfDocument.Dispose()`) για να ελευθερώσετε άμεσα τους εγγενείς πόρους, ειδικά όταν δημιουργείτε πολλά PDF σε βρόχο.

## Πλήρες, Εκτελέσιμο Παράδειγμα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή console:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using (var pdfDocument = new Document())
        {
            // Add a blank page
            Page page = pdfDocument.Pages.Add();

            // Define rectangle (fits within a standard A4 page)
            var rectangle = new Rectangle(50, 50, 550, 750);

            // Ensure the rectangle fits inside the page boundaries
            if (page.PageInfo.Width >= rectangle.Width && page.PageInfo.Height >= rectangle.Height)
            {
                // Draw the rectangle with a blue border and a transparent fill
                page.AddRectangle(rectangle, Color.Blue, Color.Transparent);
            }
            else
            {
                Console.WriteLine("Rectangle does not fit on the page. Adjust dimensions.");
                return;
            }

            // Save the PDF to a file
            string outputPath = @"C:\Temp\shape.pdf"; // Change to your desired folder
            pdfDocument.Save(outputPath);
            Console.WriteLine($"PDF created at: {outputPath}");
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Ανοίξτε το `shape.pdf` και θα δείτε μια μοναδική σελίδα μεγέθους A4 με ένα ορθογώνιο με μπλε περίγραμμα τοποθετημένο 50 pts από τις αριστερές και κάτω άκρες. Το εσωτερικό του ορθογωνίου είναι διαφανές, έτσι το φόντο της σελίδας παραμένει ορατό.

![παράδειγμα δημιουργίας pdf εγγράφου c# που δείχνει ορθογώνιο](https://example.com/placeholder.png "παράδειγμα δημιουργίας pdf εγγράφου c# που δείχνει ορθογώνιο")

*(Κείμενο alt εικόνας: **create pdf document c# example showing rectangle**)  

Αν αλλάξετε το `Color.Blue` σε `Color.Red` ή προσαρμόσετε τις συντεταγμένες, το ορθογώνιο θα αντανακλά αυτές τις αλλαγές — πειραματιστείτε ελεύθερα.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν χρειάζομαι διαφορετικό μέγεθος σελίδας;

Μπορείτε να ορίσετε τις διαστάσεις της σελίδας πριν προσθέσετε περιεχόμενο:

```csharp
Page customPage = pdfDocument.Pages.Add();
customPage.SetPageSize(PageSize.Letter.Width, PageSize.Letter.Height);
```

Θυμηθείτε να επανεκτελέσετε τη λογική **check PDF page size** μετά την αλλαγή των διαστάσεων.

### Μπορώ να σχεδιάσω άλλα σχήματα;

Απολύτως. Το Aspose.Pdf προσφέρει `AddCircle`, `AddEllipse`, `AddLine` και ακόμη και ελεύθερης μορφής αντικείμενα `Path`. Το ίδιο μοτίβο — ορισμός γεωμετρίας, επαλήθευση ορίων, και στη συνέχεια κλήση της κατάλληλης μεθόδου `Add*` — ισχύει.

### Πώς να γεμίσω το ορθογώνιο με χρώμα;

Αντικαταστήστε το `Color.Transparent` με οποιοδήποτε στερεό χρώμα:

```csharp
page.AddRectangle(rectangle, Color.Blue, Color.LightGray);
```

### Υπάρχει τρόπος να προσθέσω κείμενο μέσα στο ορθογώνιο;

Βεβαίως. Μετά τη σχεδίαση του ορθογωνίου, προσθέστε ένα `TextFragment` τοποθετημένο μέσα στις συντεταγμένες του ορθογωνίου:

```csharp
var tf = new TextFragment("Hello, world!");
tf.Rect = new Rectangle(60, 60, 540, 730); // Slightly inset
page.Paragraphs.Add(tf);
```

## Συμπέρασμα

Μόλις σας δείξαμε πώς να **create PDF document C#**, **add blank page PDF**, **check PDF page size**, **draw rectangle PDF**, και τελικά **save PDF file C#** — όλα σε ένα σύντομο, ολοκληρωμένο παράδειγμα. Ο κώδικας είναι έτοιμος για εκτέλεση, οι εξηγήσεις καλύπτουν το *γιατί* πίσω από κάθε βήμα, και τώρα έχετε μια ισχυρή βάση για πιο σύνθετες εργασίες δημιουργίας PDF.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να στρώσετε πολλαπλά σχήματα, να εισάγετε εικόνες ή να δημιουργήσετε πίνακες — όλα ακολουθούν το ίδιο μοτίβο που χρησιμοποιήσαμε εδώ. Και αν χρειαστεί ποτέ να προσαρμόσετε τις διαστάσεις της σελίδας ή να μεταβείτε σε άλλη βιβλιοθήκη PDF, οι έννοιες παραμένουν ίδιες.

Καλό κώδικα, και εύχομαι τα PDF σας να αποδίδουν πάντα ακριβώς όπως το θέλετε!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}