---
category: general
date: 2026-07-20
description: Προσθήκη ορθογωνίου σε PDF χρησιμοποιώντας το Aspose.Pdf σε C#. Μάθετε
  πώς να φορτώνετε υπάρχον PDF, να δημιουργείτε χρωματιστό ορθογώνιο και να αποθηκεύετε
  το τροποποιημένο PDF σε λίγα εύκολα βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle PDF
- load existing pdf
- save modified pdf
- how to add shape pdf
- create colored rectangle
language: el
lastmod: 2026-07-20
og_description: Προσθέστε γρήγορα ορθογώνιο PDF. Αυτός ο οδηγός δείχνει πώς να φορτώσετε
  ένα υπάρχον PDF, να δημιουργήσετε ένα χρωματιστό σχήμα ορθογωνίου και να αποθηκεύσετε
  το τροποποιημένο PDF χρησιμοποιώντας το Aspose.Pdf.
og_image_alt: Screenshot showing a green rectangle added to a PDF page – add rectangle
  PDF example
og_title: Προσθήκη ορθογωνίου PDF με το Aspose.Pdf – Γρήγορος οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Add rectangle PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, create colored rectangle, and save modified PDF in a few easy steps.
  headline: Add rectangle PDF with Aspose.Pdf – Complete C# Guide
  type: TechArticle
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Προσθήκη ορθογωνίου PDF με το Aspose.Pdf – Πλήρης οδηγός C#
url: /el/net/programming-with-operators/add-rectangle-pdf-with-aspose-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη ορθογωνίου PDF – Πλήρης Οδηγός C#

Έχετε αναρωτηθεί ποτέ **πώς να προσθέσετε ορθογώνιο PDF** χωρίς να παλεύετε με ροές PDF χαμηλού επιπέδου; Δεν είστε μόνοι. Πολλοί προγραμματιστές χρειάζονται να **φορτώσουν υπάρχον PDF** αρχεία, να σχεδιάσουν ένα σχήμα και στη συνέχεια να **αποθηκεύσουν τροποποιημένο PDF**—όλα με έναν καθαρό, επαναλαμβανόμενο τρόπο. Σε αυτό το tutorial θα περάσουμε ακριβώς από αυτό, χρησιμοποιώντας τη δυνατή βιβλιοθήκη Aspose.Pdf για .NET.

Θα καλύψουμε τα πάντα, από την ανάκτηση ενός κεντρικού εγγράφου από το δίσκο, τον έλεγχο ότι το σχήμα μας ταιριάζει, τη ζωγραφική ενός πράσινου ορθογωνίου, και τέλος την αποθήκευση των αλλαγών. Στο τέλος θα έχετε ένα έτοιμο προς εκτέλεση δείγμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο C#. Ας βουτήξουμε.

## Προαπαιτούμενα

- **.NET 6.0** (ή οποιαδήποτε πρόσφατη έκδοση .NET) εγκατεστημένη.
- Πακέτο NuGet **Aspose.Pdf for .NET** (`Install-Package Aspose.Pdf`).
- Ένα αρχείο PDF για εργασία – θα υποθέσουμε ότι το `Blank.pdf` βρίσκεται στο `YOUR_DIRECTORY`.
- Βασική κατανόηση της σύνταξης C# (δεν απαιτείται κάτι περίπλοκο).

> **Συμβουλή επαγγελματία:** Αν χρησιμοποιείτε Visual Studio, κάντε δεξί κλικ στο έργο → *Manage NuGet Packages* → αναζητήστε *Aspose.Pdf* και εγκαταστήστε την πιο πρόσφατη σταθερή έκδοση.

## Βήμα 1: Φόρτωση Υπάρχοντος PDF

Το πρώτο πράγμα που πρέπει να κάνετε είναι να φορτώσετε ένα PDF στη μνήμη. Η κλάση `Document` του Aspose.Pdf το διαχειρίζεται με μία μόνο γραμμή.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System.Drawing;   // For Color

// Load the source PDF (replace the path with your actual location)
Document pdfDocument = new Document("YOUR_DIRECTORY/Blank.pdf");
```

**Γιατί είναι σημαντικό:** Η φόρτωση του αρχείου σας δίνει πρόσβαση στη συλλογή σελίδων, τα μεταδεδομένα και τις επιλογές απόδοσης. Αν το αρχείο δεν υπάρχει, το Aspose θα ρίξει ένα `FileNotFoundException`, οπότε ελέγξτε ξανά τη διαδρομή.

## Βήμα 2: Λήψη της Στόχου Σελίδας

Οι περισσότερες περιπτώσεις προσθήκης σχήματος εστιάζουν σε μία σελίδα – συνήθως την πρώτη. Μπορείτε να την ανακτήσετε με δείκτη (το Aspose χρησιμοποιεί αρίθμηση που ξεκινά από 1).

```csharp
// Access the first page (pages are 1‑based)
Page firstPage = pdfDocument.Pages[1];
```

**Σημείωση:** Η προσπάθεια πρόσβασης σε αριθμό σελίδας που δεν υπάρχει θα προκαλέσει `ArgumentOutOfRangeException`. Πάντα βεβαιωθείτε ότι το έγγραφο έχει αρκετές σελίδες πριν το δείξετε.

## Βήμα 3: Ορισμός Γεωμετρίας Ορθογωνίου

Ένα ορθογώνιο σε όρους PDF είναι απλώς μια δομή `Rectangle` με τέσσερις συντεταγμένες: `llx, lly, urx, ury` (κάτω‑αριστερό X/Y, πάνω‑δεξιό X/Y). Ας δημιουργήσουμε ένα ορθογώνιο που είναι μεγαλύτερο από μια τυπική σελίδα A4 για να δείξουμε τον έλεγχο ορίων.

```csharp
// Rectangle larger than most pages (units are points; 72 points = 1 inch)
Rectangle shapeRect = new Rectangle(0, 0, 1200, 1200);
```

Αν θέλετε ένα ορθογώνιο που ταιριάζει καλά, χρησιμοποιήστε διαστάσεις όπως `200, 200, 400, 400`. Οι συντεταγμένες μετρώνται από την κάτω‑αριστερή γωνία της σελίδας.

## Βήμα 4: Επικύρωση του Σχήματος έναντι των Ορίων Σελίδας

Η προσθήκη ενός σχήματος που ξεπροβάλλει έξω από τη σελίδα μπορεί να καταστρέψει τη διάταξη. Το Aspose παρέχει τη μέθοδο `IsShapeInsideBounds` για να το κάνει αυτό εύκολο.

```csharp
if (firstPage.IsShapeInsideBounds(shapeRect))
{
    // Shape fits – we can safely add it
}
else
{
    Console.WriteLine("Shape exceeds page boundaries – not added.");
}
```

**Γιατί να ελέγξετε;** Κάποιοι προβολείς PDF κόβουν σιωπηλά το περιεχόμενο που υπερβαίνει, ενώ άλλοι μπορεί να το εμφανίσουν περίεργα. Η επικύρωση κρατά το αποτέλεσμα προβλέψιμο.

## Βήμα 5: Προσθήκη Χρωματιστού Ορθογωνίου στη Σελίδα

Τώρα το διασκεδαστικό μέρος: δημιουργία ενός **χρωματιστού ορθογωνίου** και προσάρτησή του στη συλλογή παραγράφων της σελίδας. Θα χρησιμοποιήσουμε πράσινο γέμισμα για ορατότητα.

```csharp
if (firstPage.IsShapeInsideBounds(shapeRect))
{
    // Create the rectangle fragment with a green fill
    RectangleFragment rectFragment = new RectangleFragment(shapeRect)
    {
        FillColor = Color.Green,      // Fill the shape with green
        Border = new BorderInfo(BorderSide.All, 1) // Optional thin border
    };

    // Add the rectangle to the page
    firstPage.Paragraphs.Add(rectFragment);
}
```

**Επεξήγηση:**  
- `RectangleFragment` είναι ένα ελαφρύ αντικείμενο που αντιπροσωπεύει ένα σχήμα.  
- `FillColor` ορίζει το εσωτερικό χρώμα· μπορείτε να χρησιμοποιήσετε οποιοδήποτε `System.Drawing.Color`.  
- Η προσθήκη στο `Paragraphs` εξασφαλίζει ότι το σχήμα σέβεται τη ροή περιεχομένου της σελίδας.

### Περιπτώσεις Άκρων & Παραλλαγές

- **Διαφορετικά χρώματα:** Αντικαταστήστε το `Color.Green` με `Color.FromArgb(255, 0, 0)` για κόκκινο, ή οποιαδήποτε τιμή ARGB.  
- **Διαφάνεια:** Χρησιμοποιήστε `rectFragment.FillColor = Color.FromArgb(128, 0, 255, 0)` για διαφάνεια 50 %.  
- **Στρογγυλεμένες γωνίες:** Το Aspose δεν υποστηρίζει απευθείας στρογγυλεμένα ορθογώνια, αλλά μπορείτε να επικάψετε ένα `EllipseFragment` για να προσομοιώσετε το εφέ.  
- **Πολλαπλά σχήματα:** Απλώς επαναλάβετε το μπλοκ δημιουργίας με νέες συντεταγμένες και προσθέστε κάθε απόσπασμα στο `firstPage.Paragraphs`.

## Βήμα 6: Αποθήκευση του Τροποποιημένου PDF

Τέλος, γράψτε τις αλλαγές πίσω στο δίσκο. Μπορείτε να αντικαταστήσετε το αρχικό αρχείο ή να δημιουργήσετε ένα νέο – θα κάνουμε το δεύτερο για να διατηρήσουμε το αρχικό ανέπαφο.

```csharp
// Save the updated document
pdfDocument.Save("YOUR_DIRECTORY/ShapeValidated.pdf");
Console.WriteLine("PDF saved successfully with the green rectangle.");
```

**Γιατί ξεχωριστό αρχείο;** Η διατήρηση του αρχικού σας επιτρέπει να εκτελείτε το script πολλές φορές χωρίς συσσωρευτικές αλλαγές, κάτι που είναι χρήσιμο κατά τη δοκιμή.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες, έτοιμο προς εκτέλεση πρόγραμμα:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing;   // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Load the existing PDF
        Document pdfDocument = new Document("YOUR_DIRECTORY/Blank.pdf");

        // 2️⃣ Get the first page
        Page firstPage = pdfDocument.Pages[1];

        // 3️⃣ Define a rectangle (change dimensions as needed)
        Rectangle shapeRect = new Rectangle(0, 0, 1200, 1200);

        // 4️⃣ Verify bounds
        if (firstPage.IsShapeInsideBounds(shapeRect))
        {
            // 5️⃣ Create and add a green rectangle
            RectangleFragment rectFragment = new RectangleFragment(shapeRect)
            {
                FillColor = Color.Green,
                Border = new BorderInfo(BorderSide.All, 1)
            };
            firstPage.Paragraphs.Add(rectFragment);
        }
        else
        {
            Console.WriteLine("Shape exceeds page boundaries – not added.");
        }

        // 6️⃣ Save the modified PDF
        pdfDocument.Save("YOUR_DIRECTORY/ShapeValidated.pdf");
        Console.WriteLine("PDF saved successfully with the green rectangle.");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση, ανοίξτε το `ShapeValidated.pdf`. Θα πρέπει να δείτε ένα συμπαγές πράσινο ορθογώνιο αγκυροβολημένο στην κάτω‑αριστερή γωνία, καλύπτοντας την περιοχή που ορίζεται από τις συντεταγμένες. Αν το ορθογώνιο ήταν πολύ μεγάλο, η κονσόλα θα είχε εκτυπώσει το μήνυμα προειδοποίησης.

## Συχνές Ερωτήσεις & Επίλυση Προβλημάτων

- **«Γιατί το ορθογώνιο μου εμφανίζεται εκτός κέντρου;»**  
  Οι συντεταγμένες PDF ξεκινούν από την κάτω‑αριστερή γωνία, όχι από την πάνω‑αριστερή. Ρυθμίστε τα `llx` και `lly` για να μετακινήσετε το σχήμα προς τα πάνω ή δεξιά.

- **«Μπορώ να προσθέσω το ορθογώνιο σε συγκεκριμένο στρώμα;»**  
  Ναι. Χρησιμοποιήστε `pdfDocument.Pages[1].Resources.Layers.Add` για να δημιουργήσετε ένα στρώμα, μετά ορίστε `rectFragment.Layer = yourLayer`.

- **«Το PDF μου είναι προστατευμένο με κωδικό—μπορώ ακόμα να προσθέσω σχήμα;»**  
  Φορτώστε το με `new Document(path, password)` και ακολουθήστε τα ίδια βήματα. Θυμηθείτε να επαναεφαρμόσετε τις ρυθμίσεις ασφαλείας πριν την αποθήκευση, εάν χρειάζεται.

- **«Τι αν χρειαστεί να προσθέσω ορθογώνιο σε κάθε σελίδα;»**  
  Κάντε βρόχο μέσω `pdfDocument.Pages` και επαναλάβετε τα βήματα 3‑5 για κάθε αντικείμενο `Page`.

## Συμπέρασμα

Τώρα έχετε μια σταθερή κατανόηση του **πώς να προσθέσετε ορθογώνιο PDF** χρησιμοποιώντας το Aspose.Pdf σε C#. Από το **φόρτωμα υπάρχοντος PDF**, **την επικύρωση των ορίων του σχήματος**, **τη δημιουργία χρωματιστού ορθογωνίου**, μέχρι το **αποθήκευση του τροποποιημένου PDF**, κάθε βήμα καλύπτεται με εξηγήσεις και κώδικα που μπορείτε να αντιγράψετε απευθείας στο έργο σας.

Στη συνέχεια, μπορείτε να εξερευνήσετε την προσθήκη άλλων σχημάτων (`EllipseFragment`, `PolygonFragment`), την ενσωμάτωση εικόνων ή ακόμη και τη δημιουργία PDF από το μηδέν. Όλα αυτά τα θέματα συνδέονται με τις δευτερεύουσες λέξεις-κλειδιά **load existing pdf**, **save modified pdf**, **how to add shape pdf**, και **create colored rectangle**, οπότε βρίσκεστε σε καλή θέση για να επεκτείνετε το σύνολο εργαλείων διαχείρισης PDF σας.

Έχετε δοκιμάσει κάτι διαφορετικό; Μοιραστείτε την εμπειρία σας στα σχόλια ή ρωτήστε ό,τι απομένει. Καλό κώδικο!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Create PDF Document with Aspose.PDF – Add Page, Shape & Save](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Create Fill Rectangle Aspose Pdf Net](/pdf/english/net/images-graphics/create-fill-rectangle-aspose-pdf-net/)
- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}