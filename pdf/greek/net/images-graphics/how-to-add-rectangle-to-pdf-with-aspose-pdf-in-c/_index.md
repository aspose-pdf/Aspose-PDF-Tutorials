---
category: general
date: 2026-10-10
description: Μάθετε πώς να προσθέσετε ορθογώνιο σε PDF, να σχεδιάσετε σχήμα σε PDF
  και να αποθηκεύσετε το τροποποιημένο PDF χρησιμοποιώντας το Aspose.PDF. Περιλαμβάνει
  οδηγό βήμα‑προς‑βήμα για την πρόσβαση σε συγκεκριμένη σελίδα PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add rectangle to PDF
- draw shape on PDF
- save modified PDF
- add shape to PDF
- access specific PDF page
language: el
lastmod: 2026-10-10
og_description: Προσθήκη ορθογωνίου σε PDF χρησιμοποιώντας το Aspose.PDF σε C#. Αυτό
  το σεμινάριο δείχνει πώς να σχεδιάσετε σχήμα σε PDF, να αποκτήσετε πρόσβαση σε συγκεκριμένη
  σελίδα PDF και να αποθηκεύσετε το τροποποιημένο PDF.
og_image_alt: Screenshot of a PDF page with a blue rectangle overlay created by Aspose.PDF
og_title: Προσθήκη ορθογωνίου σε PDF με το Aspose.PDF – πλήρης οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  headline: How to add rectangle to PDF with Aspose.PDF in C#
  type: TechArticle
- description: Learn how to add rectangle to PDF, draw shape on PDF, and save modified
    PDF using Aspose.PDF. Includes step‑by‑step guide to access specific PDF page.
  name: How to add rectangle to PDF with Aspose.PDF in C#
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: What if the PDF has only one page?
    text: Attempting to access `pdfDocument.Pages[1]` throws an `ArgumentOutOfRangeException`.
      Guard against this by checking `pdfDocument.Pages.Count` before indexing.
  - name: How to add multiple rectangles on different pages?
    text: Repeat Steps 2‑4 for each target page, adjusting the rectangle’s coordinates
      as needed. You can place the logic inside a loop that iterates over `pdfDocument.Pages`.
  - name: Can I use other shapes such as circles or polygons?
    text: Yes. Aspose.PDF provides `Ellipse`, `Polygon`, and `Polyline` classes that
      follow the same pattern as `Rectangle`. Replace the `new Aspose.Pdf.Drawing.Rectangle`
      call with the desired shape class.
  - name: Does the library support PDFs with rotated pages?
    text: Aspose.PDF automatically respects page rotation when rendering shapes. The
      rectangle’s coordinates are interpreted in the page’s native coordinate system,
      so no extra transformation is required.
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
title: Πώς να προσθέσετε ορθογώνιο σε PDF με το Aspose.PDF σε C#
url: /el/net/images-graphics/how-to-add-rectangle-to-pdf-with-aspose-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να προσθέσετε ορθογώνιο σε PDF με Aspose.PDF σε C#

Αν χρειάζεστε να **προσθέσετε ορθογώνιο σε PDF** αρχεία προγραμματιστικά, αυτός ο οδηγός σας δείχνει ακριβώς πώς. Θα μάθετε να **σχεδιάζετε σχήμα σε PDF**, να στοχεύετε μια συγκεκριμένη σελίδα και να **αποθηκεύετε το τροποποιημένο PDF** χωρίς σφάλματα.

Η εργασία με έγγραφα PDF είναι μια κοινή απαίτηση για αναφορές, τιμολόγηση ή σχολιασμό εγγράφων. Στο τέλος αυτού του σεμιναρίου μπορείτε με σιγουριά να **προσθέσετε σχήμα σε PDF** αρχεία, να διαχειριστείτε σφάλματα εκτός ορίων και να ενσωματώσετε τη λύση σε οποιοδήποτε έργο .NET.

## Προαπαιτούμενα

* .NET 6.0 SDK ή νεότερη έκδοση εγκατεστημένη  
* Visual Studio 2022 (ή οποιοδήποτε IDE C#)  
* Άδεια Aspose.PDF για .NET ή δωρεάν κλειδί αξιολόγησης – το API λειτουργεί με τον ίδιο τρόπο και στις δύο λειτουργίες  
* Ένα αρχείο PDF με όνομα `input.pdf` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από τον κώδικά σας  

Αυτά τα στοιχεία είναι οι μόνες εξωτερικές εξαρτήσεις για το παράδειγμα.

## Βήμα 1: Εγκατάσταση του πακέτου NuGet Aspose.PDF

Η βιβλιοθήκη Aspose.PDF παρέχει τις κλάσεις `Document`, `Rectangle` και άλλες κλάσεις σχεδίασης που χρειάζεστε.

```bash
dotnet add package Aspose.PDF
```

Η εκτέλεση αυτής της εντολής προσθέτει την πιο πρόσφατη σταθερή έκδοση του Aspose.PDF στο έργο σας, καθιστώντας τις κλάσεις PDF διαθέσιμες για μεταγλώττιση.

## Βήμα 2: Φόρτωση του εγγράφου PDF

Η πρώτη ενέργεια είναι η φόρτωση του αρχείου προέλευσης. Αυτό δημιουργεί μια αναπαράσταση στη μνήμη που μπορείτε να τροποποιήσετε.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;

class PdfRectangleExample
{
    static void Main()
    {
        // Load the PDF document from disk
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");
```

*Γιατί είναι σημαντικό*: Η φόρτωση του εγγράφου σας δίνει πρόσβαση στη συλλογή των σελίδων του, η οποία απαιτείται για **πρόσβαση σε συγκεκριμένη σελίδα PDF** αργότερα.

## Βήμα 3: Πρόσβαση στη δεύτερη σελίδα (μηδενική βάση δείκτη)

Οι σελίδες PDF έχουν δείκτη που ξεκινά από `0`. Για να τοποθετήσετε ένα ορθογώνιο στη δεύτερη σελίδα, ανακτήστε τη σελίδα με δείκτη `1`.

```csharp
        // Access the second page (pages are zero‑based)
        var page = pdfDocument.Pages[1];
```

Αν το έγγραφο έχει λιγότερες από δύο σελίδες, θα εξαχθεί μια `ArgumentOutOfRangeException`, προειδοποιώντας σας για την ανάγκη μιας προφυλακτικής ρήτρας στον κώδικα παραγωγής.

## Βήμα 4: Δημιουργία του σχήματος ορθογωνίου

Ορίστε τη θέση και το μέγεθος του ορθογωνίου χρησιμοποιώντας τη δομή `Rectangle`, στη συνέχεια τυλίξτε το σε ένα αντικείμενο σχεδίασης Aspose.

```csharp
        // Define rectangle bounds: (x, y, width, height)
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            // Optional visual styling
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };
```

*Γιατί είναι σημαντικό*: Οι ιδιότητες `BorderInfo` και `FillColor` σας επιτρέπουν να **σχεδιάσετε σχήμα σε PDF** με ορατό περίγραμμα και προαιρετικό γέμισμα, κάνοντας το ορθογώνιο να ξεχωρίζει για τους αναγνώστες.

## Βήμα 5: Προσθήκη του ορθογωνίου στη συλλογή παραγράφων της σελίδας

Το Aspose.PDF αντιμετωπίζει τα αντικείμενα σχεδίασης ως στοιχεία παραγράφου. Η προσθήκη του ορθογωνίου στη συλλογή `Paragraphs` της σελίδας το αποδίδει στην σελίδα.

```csharp
        // Add the rectangle shape to the page
        page.Paragraphs.Add(rectangleShape);
```

Σε αυτό το σημείο το έγγραφο PDF στη μνήμη περιέχει το νέο σχήμα, αλλά το αρχείο στο δίσκο παραμένει αμετάβλητο μέχρι να το αποθηκεύσετε.

## Βήμα 6: Αποθήκευση του τροποποιημένου PDF και διαχείριση σφαλμάτων εκτός ορίων

Η κλήση του `Save` γράφει το ενημερωμένο έγγραφο σε νέο αρχείο. Αν το ορθογώνιο υπερβαίνει τις διαστάσεις της σελίδας, το Aspose ρίχνει μια `PdfException`. Η σύλληψη αυτής της εξαίρεσης σας επιτρέπει να αναφέρετε το πρόβλημα με καθαρό τρόπο.

```csharp
        try
        {
            // Save the altered PDF to a new file
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            // Handle shape that does not fit on the page
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

*Γιατί είναι σημαντικό*: Το μπλοκ `try/catch` εξασφαλίζει ότι η εφαρμογή σας **αποθηκεύει το τροποποιημένο PDF** με ασφάλεια, και το μήνυμα σφάλματος σας βοηθά να προσαρμόσετε τις συντεταγμένες του ορθογωνίου εάν χρειαστεί.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα βήματα, εδώ είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using System;
using System.Drawing; // Required for Color

class PdfRectangleExample
{
    static void Main()
    {
        // Step 1: Load the PDF document
        var pdfDocument = new Document(@"YOUR_DIRECTORY\input.pdf");

        // Step 2: Access the second page (zero‑based)
        var page = pdfDocument.Pages[1];

        // Step 3: Create a rectangle shape positioned at (100,100) with width 300 and height 200
        var rectangleBounds = new Rectangle(100, 100, 300, 200);
        var rectangleShape = new Aspose.Pdf.Drawing.Rectangle(rectangleBounds)
        {
            Border = new BorderInfo(BorderSide.All, 2f, Color.Blue),
            FillColor = Color.FromArgb(30, 0, 0, 255) // semi‑transparent blue
        };

        // Step 4: Add the rectangle shape to the page's paragraph collection
        page.Paragraphs.Add(rectangleShape);

        // Step 5: Save the modified PDF, handling out‑of‑bounds cases
        try
        {
            pdfDocument.Save(@"YOUR_DIRECTORY\output.pdf");
            Console.WriteLine("PDF saved successfully with rectangle added.");
        }
        catch (Aspose.Pdf.Exceptions.PdfException ex)
        {
            Console.WriteLine($"Shape out of bounds: {ex.Message}");
        }
    }
}
```

### Αναμενόμενο αποτέλεσμα

Η εκτέλεση του προγράμματος εκτυπώνει:

```
PDF saved successfully with rectangle added.
```

και δημιουργεί το `output.pdf` που εμφανίζει το αρχικό περιεχόμενο συν ένα μπλε ορθογώνιο στις καθορισμένες συντεταγμένες στη δεύτερη σελίδα.

Αν το ορθογώνιο ήταν μεγαλύτερο από τη σελίδα, θα δείτε:

```
Shape out of bounds: The shape exceeds page margins.
```

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

### Τι γίνεται αν το PDF έχει μόνο μία σελίδα;

Η προσπάθεια πρόσβασης στο `pdfDocument.Pages[1]` ρίχνει μια `ArgumentOutOfRangeException`. Προστατέψτε το ελέγχοντας το `pdfDocument.Pages.Count` πριν κάνετε δείκτη.

```csharp
if (pdfDocument.Pages.Count < 2)
{
    Console.WriteLine("Document does not contain a second page.");
    return;
}
```

### Πώς να προσθέσετε πολλαπλά ορθογώνια σε διαφορετικές σελίδες;

Επαναλάβετε τα Βήματα 2‑4 για κάθε σελίδα-στόχο, προσαρμόζοντας τις συντεταγμένες του ορθογωνίου όπως απαιτείται. Μπορείτε να τοποθετήσετε τη λογική μέσα σε έναν βρόχο που διατρέχει το `pdfDocument.Pages`.

### Μπορώ να χρησιμοποιήσω άλλα σχήματα όπως κύκλους ή πολύγωνα;

Ναι. Το Aspose.PDF παρέχει τις κλάσεις `Ellipse`, `Polygon` και `Polyline` που ακολουθούν το ίδιο μοτίβο με το `Rectangle`. Αντικαταστήστε την κλήση `new Aspose.Pdf.Drawing.Rectangle` με την κλάση του επιθυμητού σχήματος.

### Υποστηρίζει η βιβλιοθήκη PDF με περιστρεφόμενες σελίδες;

Το Aspose.PDF σέβεται αυτόματα την περιστροφή της σελίδας κατά την απόδοση των σχημάτων. Οι συντεταγμένες του ορθογωνίου ερμηνεύονται στο εγγενές σύστημα συντεταγμένων της σελίδας, επομένως δεν απαιτείται επιπλέον μετασχηματισμός.

## Σκέψεις για την απόδοση

* **Χρήση μνήμης** – Η φόρτωση ενός μεγάλου PDF (εκατοντάδες megabytes) καταναλώνει ανάλογη μνήμη. Αν χρειάζεστε να τροποποιήσετε μόνο μία σελίδα, σκεφτείτε τη χρήση του `PdfFileInfo` για εξαγωγή της σελίδας, τροποποίηση και επανασυγχώνευση.  
* **Επεξεργασία παρτίδας** – Όταν προσθέτετε σχήματα σε πολλά έγγραφα, επαναχρησιμοποιήστε ένα μόνο αντικείμενο `License` για να αποφύγετε το επαναλαμβανόμενο κόστος επικύρωσης της άδειας.

## Επόμενα βήματα

Τώρα που μπορείτε να **προσθέσετε ορθογώνιο σε PDF**, εξερευνήστε αυτά τα συναφή θέματα:

* **draw shape on PDF** – μάθετε να επικάλυπτετε κείμενο, εικόνες και υδατογραφήματα  
* **add shape to PDF** – συνδυάστε πολλαπλά σχήματα σε ένα ενιαίο επίπεδο σχολιασμού  
* **save modified PDF** – χρησιμοποιήστε ροές (`MemoryStream`) για να επιστρέφετε PDF άμεσα από web APIs  
* **access specific PDF page** – υλοποιήστε εξαγωγή εύρους σελίδων για προσαρμοσμένες αναφορές  

Δοκιμάστε διαφορετικά χρώματα, στυλ γραμμής και επίπεδα διαφάνειας για να ταιριάζουν με τις οδηγίες της εταιρικής σας ταυτότητας.

---

*Καλό προγραμματισμό! Αν αυτό το σεμινάριο σας βοήθησε να **προσθέσετε ορθογώνιο σε PDF**, σκεφτείτε να το μοιραστείτε με συναδέλφους ή να συνεισφέρετε βελτιώσεις στην κοινότητα.*

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω σεμινάρια καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Προσθέσετε Σχήμα σε PDF με Aspose.PDF σε C# – Οδηγός Βήμα‑Βήμα](/pdf/english/net/images-graphics/how-to-add-shape-to-pdf-with-aspose-pdf-in-c-step-by-step-gu/)
- [Πώς να Προσθέσετε Αντικείμενο Γραμμή σε PDF Χρησιμοποιώντας Aspose.PDF για .NET&#58; Οδηγός Βήμα‑Βήμα](/pdf/english/net/document-manipulation/add-line-aspose-pdf-dotnet-tutorial/)
- [Πώς να Δημιουργήσετε PDF σε C# – Προσθήκη Σελίδας, Σχεδίαση Ορθογωνίου & Αποθήκευση](/pdf/english/net/document-creation/how-to-create-pdf-in-c-add-page-draw-rectangle-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}