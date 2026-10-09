---
category: general
date: 2026-06-05
description: Προσθήκη ορθογωνίου σε PDF χρησιμοποιώντας το Aspose.Pdf σε C#. Μάθετε
  πώς να φορτώνετε υπάρχον PDF, να επεξεργάζεστε τη σελίδα PDF και να εισάγετε σχήμα
  σε PDF σε λίγα λεπτά.
draft: false
keywords:
- add rectangle to pdf
- draw rectangle on pdf
- load existing pdf
- edit pdf page
- insert shape into pdf
language: el
og_description: Προσθέστε γρήγορα ορθογώνιο σε PDF. Αυτό το σεμινάριο δείχνει πώς
  να φορτώσετε ένα υπάρχον PDF, να επεξεργαστείτε τη σελίδα PDF και να σχεδιάσετε
  ορθογώνιο σε PDF χρησιμοποιώντας το Aspose.Pdf.
og_title: Προσθήκη Ορθογωνίου σε PDF με C# – Οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  headline: Add Rectangle to PDF with C# – Complete Programming Guide
  type: TechArticle
- description: Add rectangle to PDF using Aspose.Pdf in C#. Learn how to load existing
    PDF, edit PDF page, and insert shape into PDF in minutes.
  name: Add Rectangle to PDF with C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.6+). - Aspose.Pdf
      for .NET NuGet package (`Install-Package Aspose.Pdf`). - Basic familiarity with
      C# syntax (no deep PDF knowledge required).'
  - name: Why loading matters
    text: Before you can draw anything, the PDF must be in memory. The `Document`
      constructor reads the file, parses its internal structure, and gives you an
      object model to work with. If the file is locked or corrupted, Aspose will throw
      a descriptive exception—so you know exactly what went wrong.
  - name: Code
    text: '```csharp Document doc = new Document("YOUR_DIRECTORY/input.pdf"); ```'
  - name: Why page selection is crucial
    text: PDFs are page‑oriented; each page has its own coordinate system. Aspose
      uses a **1‑based** index, which trips up developers coming from 0‑based collections.
      Selecting the wrong page either throws an `ArgumentOutOfRangeException` or modifies
      an unintended page.
  - name: Code
    text: '```csharp Page page = doc.Pages[1]; // First page ```'
  - name: Understanding the rectangle coordinates
    text: A rectangle in Aspose.Pdf is defined by its lower‑left (`xLL`, `yLL`) and
      upper‑right (`xUR`, `yUR`) corners. The coordinate system starts at the **bottom‑left**
      of the page, with X increasing to the right and Y increasing upward. This is
      opposite of many UI frameworks, so keep an eye on the axes.
  - name: Code to add the shape
    text: '```csharp Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500,
      700); page.AddRectangle(rect); ```'
  - name: Why saving is the final step
    text: All manipulations stay in memory until you persist them. `Document.Save`
      writes the new content to disk (or stream). Overwriting the original file is
      possible, but keeping a backup (`output.pdf`) is safer.
  - name: Code
    text: '```csharp doc.Save("YOUR_DIRECTORY/output.pdf"); ```'
  type: HowTo
- questions:
  - answer: Yes—loop through `doc.Pages` and repeat the `AddRectangle` call for each
      `Page` object.
    question: Can I add the rectangle to every page automatically?
  - answer: Aspose provides `AddCircle`, `AddPolygon`, and `AddPolyline` methods.
      The same rectangle logic applies for bounding boxes.
    question: What if I need to draw a circle or a polygon?
  - answer: 'Compute the center coordinates:'
    question: Is there a way to position the rectangle relative to the page center?
  - answer: Aspose loads pages lazily, but if you’re processing thousands of pages,
      consider using `PdfExtractor` to work on subsets or stream the file to reduce
      memory footprint.
    question: Performance concerns for large PDFs?
  type: FAQPage
tags:
- pdf
- csharp
- aspose
- shape-manipulation
title: Προσθήκη Ορθογωνίου σε PDF με C# – Πλήρης Οδηγός Προγραμματισμού
url: /el/net/document-manipulation/add-rectangle-to-pdf-with-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη Ορθογωνίου σε PDF με C# – Πλήρης Οδηγός Προγραμματισμού

Έχετε χρειαστεί ποτέ να **προσθέσετε ορθογώνιο σε pdf** αλλά δεν ήσασταν σίγουροι ποιο κάλεσμα API να χρησιμοποιήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές συναντούν αυτό το εμπόδιο όταν προσπαθούν για πρώτη φορά να επεξεργαστούν ένα PDF προγραμματιστικά. Τα καλά νέα; Με λίγες γραμμές C# και τη δυνατή βιβλιοθήκη Aspose.Pdf, μπορείτε να σχεδιάσετε ένα ορθογώνιο σε οποιαδήποτε σελίδα ενός υπάρχοντος εγγράφου σε μια στιγμή.

Σε αυτόν τον οδηγό θα περάσουμε από τη φόρτωση ενός υπάρχοντος PDF, την επιλογή της σωστής σελίδας, τον ορισμό ενός ορθογωνίου που ταιριάζει, και τελικά την εισαγωγή του σχήματος στο PDF. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET. Και, φυσικά, θα αγγίξουμε και τις λεπτομέρειες του **draw rectangle on pdf** που ίσως δεν είχατε σκεφτεί.

## Τι Θα Κερδίσετε

- Μια σαφή, βήμα‑βήμα λύση που λειτουργεί αμέσως.
- Κατανόηση του πώς να **φορτώνετε υπάρχον pdf** με ασφάλεια.
- Συμβουλές για **επεξεργασία σελίδας pdf** χωρίς να καταστρέψετε το έγγραφο.
- Στρατηγικές για **εισαγωγή σχήματος στο pdf** πέρα από απλά ορθογώνια.
- Έτοιμος‑για‑εκτέλεση κώδικας C# που μπορείτε να αντιγράψετε‑επικολλήσετε αμέσως.

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+).
- Πακέτο NuGet Aspose.Pdf for .NET (`Install-Package Aspose.Pdf`).
- Βασική εξοικείωση με τη σύνταξη C# (δεν απαιτείται βαθιά γνώση PDF).

Αν έχετε αυτά, ας βουτήξουμε.

![Παράδειγμα προσθήκης ορθογωνίου σε PDF](add-rectangle-to-pdf.png "Στιγμιότυπο οθόνης που δείχνει ένα ορθογώνιο προστιθέμενο σε μια σελίδα PDF – προσθήκη ορθογωνίου σε pdf")

## Προσθήκη Ορθογωνίου σε PDF – Επισκόπηση Βήμα‑βήμα

Παρακάτω είναι το πλήρες, εκτελέσιμο παράδειγμα που ακολουθεί τη σειρά που θα συζητήσουμε:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the existing PDF file
        Document doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Select the first page (pages are 1‑based)
        Page page = doc.Pages[1];

        // 3️⃣ Define a rectangle that fits inside the page bounds
        //    (xLL, yLL, xUR, yUR) – lower‑left & upper‑right corners
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);

        // 4️⃣ Add the rectangle to the page – this draws the shape
        page.AddRectangle(rect);

        // 5️⃣ Save the modified PDF to a new file
        doc.Save("YOUR_DIRECTORY/output.pdf");
    }
}
```

Τώρα ας αναλύσουμε κάθε γραμμή ώστε να καταλάβετε **γιατί** κάνουμε ό,τι κάνουμε, όχι μόνο **τι**.

## Φόρτωση Υπάρχοντος PDF Εγγράφου

### Γιατί η φόρτωση είναι σημαντική

Πριν μπορέσετε να σχεδιάσετε οτιδήποτε, το PDF πρέπει να βρίσκεται στη μνήμη. Ο κατασκευαστής `Document` διαβάζει το αρχείο, αναλύει τη δομή του και σας παρέχει ένα αντικειμενοστραφές μοντέλο για εργασία. Αν το αρχείο είναι κλειδωμένο ή κατεστραμμένο, το Aspose θα ρίξει μια περιγραφική εξαίρεση—ώστε να ξέρετε ακριβώς τι πήγε στραβά.

### Κώδικας

```csharp
Document doc = new Document("YOUR_DIRECTORY/input.pdf");
```

- Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη ή σχετική διαδρομή προς το αρχείο προέλευσης.
- Η διαδρομή μπορεί να είναι URL εάν ενεργοποιήσετε τη δυνατότητα απομακρυσμένης φόρτωσης του Aspose (προχωρημένο σενάριο).
- **Συμβουλή:** Τυλίξτε το σε ένα μπλοκ `try/catch` για να διαχειριστείτε το `FileNotFoundException` ή το `PdfException` με χάρη.

```csharp
try
{
    Document doc = new Document("input.pdf");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load PDF: {ex.Message}");
    return;
}
```

## Επιλογή και Προετοιμασία της Σελίδας

### Γιατί η επιλογή σελίδας είναι κρίσιμη

Τα PDF είναι προσανατολισμένα κατά σελίδες· κάθε σελίδα έχει το δικό της σύστημα συντεταγμένων. Το Aspose χρησιμοποιεί δείκτη **1‑based**, κάτι που συχνά προκαλεί σύγχυση σε προγραμματιστές που προέρχονται από συλλογές 0‑based. Η επιλογή λάθος σελίδας είτε ρίχνει `ArgumentOutOfRangeException` είτε τροποποιεί μια ανεπιθύμητη σελίδα.

### Κώδικας

```csharp
Page page = doc.Pages[1]; // First page
```

Αν χρειάζεστε τη σελίδα 3, απλώς αλλάξτε τον δείκτη σε `3`. Για δυναμικά σενάρια, μπορείτε να κάνετε βρόχο:

```csharp
foreach (Page pg in doc.Pages)
{
    // Apply rectangle to every page
}
```

## Ορισμός και Σχεδίαση Ορθογωνίου σε PDF

### Κατανόηση των συντεταγμένων του ορθογωνίου

Ένα ορθογώνιο στο Aspose.Pdf ορίζεται από τις κάτω‑αριστερές (`xLL`, `yLL`) και άνω‑δεξιές (`xUR`, `yUR`) γωνίες του. Το σύστημα συντεταγμένων ξεκινά από το **κάτω‑αριστερό** της σελίδας, με το X να αυξάνεται προς τα δεξιά και το Y προς τα πάνω. Αυτό είναι αντίθετο με πολλά UI frameworks, οπότε προσέξτε τους άξονες.

- `0,0` είναι η κάτω‑αριστερή γωνία της σελίδας.
- Πλάτος = `xUR - xLL`; Ύψος = `yUR - yLL`.

Αν καταλάθος ορίσετε ορθογώνιο μεγαλύτερο από τη σελίδα, το `AddRectangle` θα ρίξει εξαίρεση. Για να το αποφύγετε, μπορείτε να ελέγξετε το μέγεθος της σελίδας:

```csharp
double pageWidth  = page.PageInfo.Width;
double pageHeight = page.PageInfo.Height;
```

Στη συνέχεια περιορίστε το ορθογώνιο σας:

```csharp
double rectWidth  = Math.Min(500, pageWidth);
double rectHeight = Math.Min(700, pageHeight);
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectWidth, rectHeight);
```

### Κώδικας για προσθήκη του σχήματος

```csharp
Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, 500, 700);
page.AddRectangle(rect);
```

- Το `AddRectangle` σχεδιάζει αυτόματα ένα λεπτό μαύρο περίγραμμα.
- Θέλετε γεμάτο ορθογώνιο; Χρησιμοποιήστε `page.AddAnnotation(new SquareAnnotation(page, rect) { FillColor = Color.Yellow });`.
- Χρειάζεστε διαφορετικό πάχος γραμμής; Ορίστε `rect.LineWidth = 2;` πριν την προσθήκη.

#### Edge case: multiple rectangles

Αν καλέσετε το `AddRectangle` επανειλημμένα, κάθε κλήση προσθέτει ένα νέο σχήμα. Για να αποφύγετε την επικάλυψη, μετατοπίστε τα επόμενα ορθογώνια:

```csharp
for (int i = 0; i < 3; i++)
{
    var offset = i * 20;
    var r = new Aspose.Pdf.Rectangle(offset, offset, 500 + offset, 700 + offset);
    page.AddRectangle(r);
}
```

## Αποθήκευση του Τροποποιημένου PDF

### Γιατί η αποθήκευση είναι το τελικό βήμα

Όλες οι τροποποιήσεις παραμένουν στη μνήμη μέχρι να τις αποθηκεύσετε. Η `Document.Save` γράφει το νέο περιεχόμενο στο δίσκο (ή σε stream). Η αντικατάσταση του αρχικού αρχείου είναι δυνατή, αλλά η διατήρηση αντιγράφου ασφαλείας (`output.pdf`) είναι πιο ασφαλής.

### Κώδικας

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

- Μπορείτε επίσης να αποθηκεύσετε σε ένα `MemoryStream` εάν χρειάζεται να στείλετε το PDF μέσω HTTP:

```csharp
using var ms = new MemoryStream();
doc.Save(ms);
byte[] pdfBytes = ms.ToArray();
// return File(pdfBytes, "application/pdf");
```

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το τελικό πρόγραμμα που μπορείτε να τρέξετε αμέσως:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;

class AddRectangleDemo
{
    static void Main()
    {
        const string inputPath  = "input.pdf";
        const string outputPath = "output.pdf";

        // Load the existing PDF
        Document doc;
        try
        {
            doc = new Document(inputPath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading PDF: {ex.Message}");
            return;
        }

        // Ensure the document has at least one page
        if (doc.Pages.Count == 0)
        {
            Console.WriteLine("PDF contains no pages.");
            return;
        }

        // Select the first page (1‑based index)
        Page page = doc.Pages[1];

        // Get page dimensions to avoid overflow
        double pageW = page.PageInfo.Width;
        double pageH = page.PageInfo.Height;

        // Define rectangle size (clamp to page bounds)
        double rectW = Math.Min(500, pageW);
        double rectH = Math.Min(700, pageH);
        Aspose.Pdf.Rectangle rect = new Aspose.Pdf.Rectangle(0, 0, rectW, rectH);

        // Optional: set line width and color
        rect.LineWidth = 2;
        rect.Color = Color.Blue;

        // Add rectangle to the page
        page.AddRectangle(rect);

        // Save the result
        doc.Save(outputPath);
        Console.WriteLine($"Rectangle added and saved to {outputPath}");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Ανοίξτε το `output.pdf` και θα δείτε ένα ορθογώνιο με μπλε περίγραμμα, τοποθετημένο στη κάτω‑αριστερή γωνία της πρώτης σελίδας, με μέγεθος έως 500 × 700 points (ή μικρότερο αν η σελίδα είναι μικρή).

## Συχνές Ερωτήσεις & Επαγγελματικές Συμβουλές

- **Μπορώ να προσθέσω το ορθογώνιο σε κάθε σελίδα αυτόματα;**  
  Ναι—κάντε βρόχο μέσω `doc.Pages` και επαναλάβετε την κλήση `AddRectangle` για κάθε αντικείμενο `Page`.

- **Τι γίνεται αν χρειαστεί να σχεδιάσω κύκλο ή πολύγωνο;**  
  Το Aspose παρέχει τις μεθόδους `AddCircle`, `AddPolygon` και `AddPolyline`. Η ίδια λογική του ορθογωνίου εφαρμόζεται για τα πλαίσια περιβάλλοντος.

- **Υπάρχει τρόπος να τοποθετήσω το ορθογώνιο σχετικά με το κέντρο της σελίδας;**  
  Υπολογίστε τις συντεταγμένες του κέντρου:  
  ```csharp
  double centerX = pageW / 2;
  double centerY = pageH / 2;
  double halfW = rectW / 2;
  double halfH = rectH / 2;
  var centeredRect = new Aspose.Pdf.Rectangle(centerX - halfW, centerY - halfH,
                                              centerX + halfW, centerY + halfH);
  page.AddRectangle(centeredRect);
  ```

- **Ανησυχίες απόδοσης για μεγάλα PDF;**  
  Το Aspose φορτώνει τις σελίδες «lazy», αλλά αν επεξεργάζεστε χιλιάδες σελίδες, σκεφτείτε τη χρήση του `PdfExtractor` για επεξεργασία υποσυνόλων ή τη ροή του αρχείου ώστε να μειώσετε το αποτύπωμα μνήμης.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να προσθέσετε ορθογώνιο

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Δημιουργία PDF Εγγράφου με Aspose.PDF – Προσθήκη Σελίδας, Σχήματος & Αποθήκευση](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)
- [Πώς να Προσθέσετε Σφραγίδες Σελίδας σε PDFs Χρησιμοποιώντας Aspose.PDF για .NET: Πλήρης Οδηγός](/pdf/english/net/watermarks-backgrounds/add-page-stamp-aspose-pdf-dotnet-guide/)
- [Προσθήκη Εικόνων & Αριθμών Σελίδων σε PDFs Χρησιμοποιώντας Aspose.PDF για .NET: Πλήρης Οδηγός](/pdf/english/net/document-manipulation/enhance-pdfs-images-page-numbers-aspose-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}