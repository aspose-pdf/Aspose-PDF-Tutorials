---
category: general
date: 2026-03-27
description: Μάθετε πώς να σχεδιάζετε ορθογώνιο σε PDF χρησιμοποιώντας το Aspose.Pdf
  για C#. Προσθέστε ορθογώνιο σε PDF, προσθέστε σχήμα σε PDF και σχεδιάστε σχήμα σε
  PDF με σαφή παραδείγματα κώδικα.
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: el
og_description: Μάθετε πώς να σχεδιάζετε ορθογώνιο σε PDF χρησιμοποιώντας το Aspose.Pdf.
  Αυτό το σεμινάριο σας δείχνει πώς να προσθέσετε ορθογώνιο σε PDF, να προσθέσετε
  σχήμα σε PDF και να σχεδιάσετε σχήμα σε PDF βήμα προς βήμα.
og_title: Πώς να σχεδιάσετε ορθογώνιο σε PDF με C# – Πλήρης οδηγός
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Πώς να σχεδιάσετε ένα ορθογώνιο σε PDF με C# – Οδηγός βήμα‑βήμα
url: /el/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Σχεδιάσετε Ορθογώνιο σε PDF με C# – Οδηγός Βήμα‑Βήμα

Έχετε αναρωτηθεί ποτέ **πώς να σχεδιάσετε ορθογώνιο** σε ένα PDF χωρίς να παλεύετε με τη χαμηλού επιπέδου σύνταξη PDF; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολίες όταν χρειάζεται να οπτικοποιήσουν ένα πλαίσιο, μια περιοχή επισήμανσης ή ένα απλό διακοσμητικό στοιχείο μέσα σε ένα παραγόμενο έγγραφο. Τα καλά νέα; Με το Aspose.Pdf for .NET η διαδικασία είναι παιχνιδάκι.

Σε αυτό το tutorial θα περάσουμε από όλα όσα χρειάζεστε για να **προσθέσετε ορθογώνιο σε PDF**, **προσθέσετε σχήμα σε PDF**, και τελικά **σχεδιάσετε ορθογώνιο σε PDF** χρησιμοποιώντας καθαρό, ιδιωματικό C#. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα που παράγει ένα αρχείο PDF που περιέχει ένα καθαρό ορθογώνιο — χωρίς εξωτερικά εργαλεία.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework)
- Πακέτο NuGet Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`)
- Ένα βασικό περιβάλλον ανάπτυξης C# (Visual Studio, VS Code, Rider κ.λπ.)

Δεν χρειάζονται άλλες βιβλιοθήκες· όλα τα υπόλοιπα διαχειρίζεται το Aspose.Pdf.

## Βήμα 1: Ρύθμιση του Έργου και Εισαγωγή Ονομάτων Χώρου

Πρώτα, δημιουργήστε μια νέα εφαρμογή κονσόλας και εισάγετε το όνομα χώρου Aspose.Pdf.

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
            // We'll place the rest of the code here.
        }
    }
}
```

**Γιατί είναι σημαντικό:** Η εισαγωγή του `Aspose.Pdf.Drawing` σας δίνει πρόσβαση στην κλάση σχήματος `Rectangle` που θα χρησιμοποιήσουμε για **σχεδίαση σχήματος σε PDF**. Κρατώντας το σημείο εισόδου τακτοποιημένο, τα επόμενα βήματα γίνονται πιο εύκολα στην παρακολούθηση.

## Βήμα 2: Δημιουργία Νέου Εγγράφου PDF και Σελίδας

Ένα PDF χωρίς σελίδες δεν έχει νόημα, οπότε ξεκινάμε δημιουργώντας ένα αντικείμενο εγγράφου και προσθέτοντας μια μοναδική σελίδα.

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**Εξήγηση:** Η κλάση `Document` αντιπροσωπεύει ολόκληρο το αρχείο, ενώ η `Pages.Add()` επιστρέφει ένα νέο αντικείμενο `Page` όπου θα **προσθέσουμε ορθογώνιο σε PDF** αργότερα. Το προεπιλεγμένο μέγεθος A4 λειτουργεί στις περισσότερες περιπτώσεις, αλλά μπορείτε να περάσετε πλάτος/ύψος αν χρειάζεστε προσαρμοσμένο καμβά.

## Βήμα 3: Ορισμός του Σχήματος Ορθογωνίου

Τώρα έρχεται η ουσία του **πώς να σχεδιάσετε ορθογώνιο** — ο ορισμός της θέσης και των διαστάσεων.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**Γιατί ορίζουμε αυτές τις ιδιότητες:**  
- `BorderColor` και `BorderWidth` ελέγχουν το περίγραμμα, κάνοντας το ορθογώνιο ορατό.  
- `FillColor` του δίνει ένα ήπιο φόντο, χρήσιμο όταν θέλετε να επισημάνετε μια περιοχή.  
- Ο κατασκευαστής `(x, y, width, height)` σας επιτρέπει να **σχεδιάσετε ορθογώνιο σε PDF** ακριβώς εκεί που το χρειάζεστε.

## Βήμα 4: Προσθήκη του Ορθογωνίου στη Σελίδα

Με το σχήμα έτοιμο, τώρα **προσθέτουμε σχήμα σε PDF** προσδένοντάς το στη συλλογή `Annotations` της σελίδας. Το Aspose.Pdf επικυρώνει αυτόματα τα όρια, οπότε δεν χρειάζεται να ανησυχείτε για υπερχείλιση.

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**Τι συμβαίνει στο παρασκήνιο:** Η συλλογή `Annotations` αντιμετωπίζει το ορθογώνιο ως διανυσματικό γραφικό. Όταν το PDF αποδοθεί, η βιβλιοθήκη μετατρέπει τις συντεταγμένες μας σε ροή περιεχομένου PDF.

## Βήμα 5: Αποθήκευση του Εγγράφου

Τέλος, γράψτε το PDF στο δίσκο ώστε να μπορείτε να το ανοίξετε σε οποιονδήποτε προβολέα.

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**Αποτέλεσμα:** Το άνοιγμα του `RectangleDemo.pdf` εμφανίζει ένα ανοιχτό-γκρι ορθογώνιο με μαύρο περίγραμμα, τοποθετημένο 100 pts από την αριστερή πλευρά και 500 pts από το κάτω μέρος της σελίδας. Αυτή είναι η πλήρης λύση για **πώς να σχεδιάσετε ορθογώνιο** σε PDF χρησιμοποιώντας C#.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι το ολοκληρωμένο, έτοιμο‑για‑εκτέλεση πρόγραμμα:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Ένα αρχείο με όνομα `RectangleDemo.pdf` που περιέχει μια μοναδική σελίδα με ένα κεντραρισμένο ανοιχτό‑γκρι ορθογώνιο περιγραμμένο με μαύρο. Μπορείτε να το ανοίξετε με Adobe Reader, Chrome ή οποιονδήποτε προβολέα PDF.

## Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

### 1. Σχεδίαση Πολλαπλών Ορθογωνίων

Αν χρειάζεται να **προσθέσετε ορθογώνιο σε PDF** περισσότερες από μία φορές, απλώς δημιουργήστε επιπλέον αντικείμενα `Rectangle` και προσθέστε τα στο `page.Annotations`. Η επανάληψη πάνω σε μια συλλογή συντεταγμένων το κάνει τελείως απλό.

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. Χρήση Διαφορετικών Μονάδων

Το Aspose.Pdf λειτουργεί σε σημεία (1 pt = 1/72 inch). Αν προτιμάτε χιλιοστά, μετατρέψτε τα πρώτα:

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. Προσθήκη Ορθογωνίου ως Πεδίου Φόρμας

Όταν χρειάζεστε ένα διαδραστικό ορθογώνιο (π.χ. μια κλικ-περιοχή), χρησιμοποιήστε ένα `LinkAnnotation` αντί για ένα απλό `Rectangle`. Ο κώδικας είναι παρόμοιος αλλά προσθέτει URL ή ενέργεια JavaScript.

### 4. Ζητήματα Συμβατότητας

Η έκδοση Aspose.Pdf 23.9 (κυκλοφόρησε αρχές 2026) υποστηρίζει πλήρως τα παραπάνω API. Παλαιότερες εκδόσεις μπορεί να απαιτούν `page.AddAnnotation(rectangleShape)` αντί για `page.Annotations.Add`. Ελέγχετε πάντα τις σημειώσεις έκδοσης αν αντιμετωπίσετε σφάλματα μεταγλώττισης.

## Συμβουλές & Παγίδες

- **Συμβουλή:** Ορίστε `FillColor = Color.Transparent` αν χρειάζεστε μόνο περίγραμμα. Αυτό μειώνει ελαφρώς το μέγεθος του αρχείου.
- **Προσοχή:** Χρήση συντεταγμένων που υπερβαίνουν τις διαστάσεις της σελίδας. Το Aspose.Pdf θα κόψει σιωπηλά το σχήμα, κάτι που μπορεί να προκαλέσει σύγχυση κατά το debugging.
- **Σημείωση απόδοσης:** Η προσθήκη χιλιάδων ορθογωνίων είναι αποδεκτή, αλλά αν δημιουργείτε μεγάλες αναφορές σκεφτείτε να ομαδοποιήσετε τα σχήματα σε ένα ενιαίο αντικείμενο `Graphics` για να μειώσετε το κόστος.

## Οπτική Αναφορά

Παρακάτω υπάρχει μια γρήγορη λήψη οθόνης του παραγόμενου PDF (το ορθογώνιο είναι επισημασμένο με ανοιχτό‑γκρι). Το κείμενο alt περιλαμβάνει τη βασική λέξη-κλειδί για SEO.

![πώς να σχεδιάσετε ορθογώνιο σε PDF παράδειγμα](https://example.com/images/rectangle-demo.png "πώς να σχεδιάσετε ορθογώνιο σε PDF παράδειγμα")

## Συμπέρασμα

Καλύψαμε **πώς να σχεδιάσετε ορθογώνιο** σε PDF χρησιμοποιώντας το Aspose.Pdf for C#. Δημιουργώντας ένα `Document`, προσθέτοντας μια `Page`, ορίζοντας ένα σχήμα `Rectangle` και τελικά **προσθέτοντας σχήμα σε PDF**, μπορείτε να παράγετε γραφικά βασισμένα σε διανύσματα με μερικές μόνο γραμμές κώδικα. Είτε χρειάζεστε να **προσθέσετε ορθογώνιο σε pdf** για επισήμανση, αποσφαλμάτωση διάταξης ή UI επικάλυψη, η προσέγγιση κλιμακώνεται άψογα.

Στη συνέχεια, μπορείτε να εξερευνήσετε **σχεδίαση σχήματος σε pdf** πέρα από τα ορθογώνια — σκεφτείτε κύκλους, πολυγραμμές ή ακόμη και προσαρμοσμένες διαδρομές SVG. Ή βυθιστείτε στην απόδοση κειμένου, εισαγωγή εικόνων και διαχείριση φορμών PDF για να δημιουργήσετε πλήρη αναφορές. Η βιβλιοθήκη Aspose.Pdf προσφέρει πλούσιο API, και με τα θεμέλια που καλύψαμε εδώ είστε έτοιμοι να πειραματιστείτε.

Καλή προγραμματιστική, και εύχομαι τα PDFs σας να φαίνονται πάντα ακριβώς όπως τα φαντάζεστε!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}